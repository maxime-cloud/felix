# Contraintes techniques Meta — WhatsApp Cloud API / Tech Provider

**Vérifié le 2026-08-19, uniquement sur `developers.facebook.com`.** Toute valeur absente de la
documentation officielle est écrite **non documenté** — jamais devinée.

---

## 1. 🔴 Alternate webhook endpoints — confirmés, mais **partiellement**

Source : https://developers.facebook.com/documentation/business-messaging/whatsapp/webhooks/override/

| Contrainte | Valeur documentée | Conséquence code |
|---|---|---|
| Existence | Priorité : **numéro → WABA → URL par défaut de l'app** | Une URL par WABA **et** par numéro est possible dans une seule app. Le modèle « une app, plusieurs commerçants » tient |
| Config WABA | `POST /<WABA_ID>/subscribed_apps` `{override_callback_uri, verify_token}` | À appeler juste après l'abonnement. **Stocker le `verify_token` par commerçant** |
| Config numéro | `POST /<PHONE_NUMBER_ID>` `{webhook_configuration:{override_callback_uri, verify_token}}` | Le niveau numéro écrase le niveau WABA |
| Longueur d'URL | **200 caractères max** ; `verify_token` sans limite | `https://api.contexfly.com/wh/<tenantId>` passe. Pas de query string longue |
| Lecture | `GET /<PHONE_NUMBER_ID>?fields=webhook_configuration` | Écran de diagnostic : afficher les 3 niveaux effectifs |
| Suppression | WABA : re-souscrire sans corps. Numéro : `override_callback_uri: ""` | Dé-configuration au départ d'un commerçant |
| Prérequis | L'endpoint alternatif « must successfully receive/process webhooks » | Chaque URL par tenant doit répondre au handshake `hub.challenge` → **gérer le `GET`** |
| Nombre max d'overrides | **non documenté** | À revalider au-delà de quelques centaines de tenants |

### 🔴 Champs NON surchargeables — la limite qui casse le design prévu

Toujours envoyés à l'**URL par défaut de l'application** :
`message_template_status_update` · `message_template_quality_update` ·
`message_template_components_update` · `template_category_update` · `account_update` ·
`account_review_update` · `account_alerts`.

Surchargeables : `messages` · `message_echoes` · `calls` · `consumer_profile` ·
`messaging_handovers` · `group_*` · `smb_message_echoes` · `smb_app_state_sync` · `history` ·
`account_settings_update`.

**→ Deux chemins d'entrée dans l'application, pas un :**
1. un **routeur multi-tenant sur l'URL par défaut**, qui dispatche via `entry[].id` = **WABA ID**
   (les webhooks de template ne contiennent **aucun** `phone_number_id`) ;
2. des endpoints par tenant pour `messages`, optionnels.

**→ Une table de correspondance `WABA_ID → commerçant` est obligatoire**, en plus de
`phone_number_id → commerçant`.

⚠️ **Corrige `Contraintes-Techniques.md` §1.1** : « séparation des flux par alternate webhook
endpoints » n'est vrai que pour le **trafic conversationnel**.

---

## 2. Webhooks entrants — garanties de livraison

| Contrainte | Valeur | Conséquence |
|---|---|---|
| Réessais | « with decreasing frequency until the request succeeds, **for up to 7 days** » | Un webhook peut arriver **7 jours plus tard** → **toujours horodater sur le `timestamp` du payload**, jamais sur l'heure de réception |
| ⚠️ Contradiction Meta | La doc Graph API générique dit « **36 hours** » puis « dropped » | **Deux pages officielles se contredisent.** Concevoir sur l'hypothèse basse et **ne jamais compter sur le réessai Meta** comme rattrapage métier |
| Doublons | « These retries can result in **duplicate webhook notifications** » | Idempotence obligatoire |
| Clé de dédup | Le message porte un `id` unique (**WAMID**) | W1 : dédup sur `wamid`. W2 : plusieurs statuts partagent le wamid → clé composite **`(wamid, status, timestamp)`** *(déduit — Meta ne fournit pas de clé d'idempotence explicite)* |
| Ordre | **non documenté** | Traiter comme **non garanti**. Machine à états **monotone** : ignorer un `sent` reçu après un `delivered`. **Jamais d'upsert naïf du dernier statut** |
| Regroupement | « batch with a **maximum of 1000 updates** » ; « batching cannot be guaranteed » | Itérer sur `entry[] × changes[] × messages[]/statuses[]` |
| Taille max du payload | **3 MB** | Limite de corps de la route HTTP ≥ 3 MB |
| Délai de réponse attendu | **non documenté** — répondre `200` | **Accuser réception en 200 immédiatement, traiter en asynchrone.** Ne **jamais** appeler le LLM dans le cycle de requête du webhook |
| TLS | Certificat valide ; « **Self-signed certificates are not supported** » | Pas de tunnel auto-signé en préprod partagée |

## 3. Vérification de signature

- **Handshake `GET`** : `hub.mode`, `hub.challenge`, `hub.verify_token` → répondre **200 + la valeur
  de `hub.challenge`**. Le `verify_token` doit être **cherché par tenant**, pas une constante.
- **`POST`** : `X-Hub-Signature-256: sha256=<hash>`, **HMAC-SHA256 sur le corps brut**, clé = **app
  secret**. Vérifier **avant tout parsing**.
- ⚠️ **Non documenté** que la signature reste celle de l'app secret sur une URL surchargée.
  *Déduit* : une seule app = un seul app secret. **À valider par un test réel avant production.**

---

## 4. Envoi de messages — débit

| Contrainte | Valeur | Conséquence |
|---|---|---|
| Débit par défaut | **80 messages/seconde**, jusqu'à 1 000 par montée automatique | Le workpool plafonne à 80 mps. Les 1 000 mps exigent 100 K destinataires uniques/24 h — hors de portée |
| 🔴 **Limite par paire** | « **1 message every 6 seconds to the same WhatsApp user** » (~10/min, 600/h) | **La contrainte la plus dangereuse pour un agent conversationnel.** Un agent qui répond en 3 bulles déclenche `131056` → **agréger la réponse en un seul message**, et un limiteur **par paire (numéro commerçant, numéro client)** |
| Rafale | « up to **45 messages in a 6-second** window », mais emprunte sur le quota futur (20 messages ≈ 2 min d'attente) | Tolérée mais coûteuse — inacceptable dans un fil actif |
| Coexistence | **20 mps** fixes | Le workpool doit connaître le **mode** du numéro |
| Codes d'erreur | `131056` (trop vers le même destinataire) · `130429` (débit Cloud API) · `80007` (limite WABA) · **`4` (limite d'appel de l'app)** | **4 limiteurs distincts.** ⚠️ Le `4` est **partagé par tous les commerçants** — un seul peut saturer l'app entière |
| Idempotence à l'envoi | **non documenté** — aucun en-tête d'idempotence | 🔴 **Un réessai après timeout réseau peut envoyer deux fois.** Verrou + enregistrement de l'envoi **avant** l'appel HTTP |
| Réponse d'envoi | `message_status` ∈ `accepted`, **`held_for_quality_assessment`**, `paused` | **Un `200 OK` ne veut pas dire envoyé.** État « retenu » obligatoire dans la machine à états |
| Texte | corps **max 4096 caractères** | — |

### 🔴 Business portfolio pacing — contrainte non prévue
Source : https://developers.facebook.com/docs/whatsapp/portfolio-pacing/

Mécanisme de **lissage par lots** des templates, appliqué aux portefeuilles sous **500 K messages
template / 365 jours glissants** → **tous les commerçants de ContexFly sont concernés**.
Statut `held_for_quality_assessment` ; en cas de détection : `failed`, code **`135000`**.
**Durée de rétention : non documentée.**

**→ P4w ne peut pas mesurer son avancement sur les réponses d'API.** Une campagne de 200 contacts
part par vagues, avec une latence non spécifiée. L'écran de campagne doit distinguer
**« en cours d'évaluation par Meta »** de « envoyé » et de « échec ».

## 5. Médias

| Type | Formats | Taille max |
|---|---|---|
| Audio | `.aac`, `.amr`, `.mp3`, `.m4a`, `.ogg` (**OPUS mono uniquement**) | **16 MB** |
| Document | `.txt`, `.xls(x)`, `.doc(x)`, `.ppt(x)`, `.pdf` | 100 MB |
| Image | `.jpeg`, `.png` — **8-bit RGB ou RGBA obligatoire** | **5 MB** |
| Sticker | `.webp` | 100 KB statique / 500 KB animé |
| Vidéo | `.3gp`, `.mp4` — **H.264 + AAC**, un seul flux audio ou aucun | **16 MB** |

- **ID médias uploadés : expirent après 30 jours.** Ré-upload à la demande ; ID + date stockés sur
  le produit.
- 🔴 **ID médias reçus par webhook : expirent après 7 jours.** **URL valide 5 minutes.**
- **Téléchargement authentifié obligatoire** — « clicking this URL will not return the media ; you
  must include an access token ». **→ Aucune URL Meta n'est utilisable dans l'UI : ré-hébergement
  systématique.** Chaîne : webhook → download avec le business token → stockage → URL propre.
- ⚠️ **Image sortante ≤ 5 MB** : les photos prises au téléphone au Cameroun dépassent souvent.
  **Compression/redimensionnement serveur obligatoire** avant upload (module catalogue).
- Note vocale sortante : `.ogg` **OPUS** + `"voice": true` ; l'icône de lecture n'apparaît que si le
  fichier fait **≤ 512 KB**.

## 6. Notes vocales entrantes

- Objet `audio` : `id`, `mime_type`, `sha256`, `voice` (booléen), `url`.
  Distinguer **note vocale** (`voice: true`) d'un fichier joint — le registre de réponse diffère.
- ⚠️ Le champ `url` est déployé **progressivement depuis le 12 novembre 2025** et **peut être
  absent** → **implémenter les deux voies** : `url` directe, et repli `GET /<media_id>` puis `GET`
  sur l'URL retournée.
- **Rétention 7 jours** → télécharger dans le traitement asynchrone immédiat.
- **Meta ne fournit aucune transcription** → service externe à ajouter (**X13**, absent de
  l'inventaire), avec son coût par minute.

## 7. Templates

| Contrainte | Valeur | Conséquence |
|---|---|---|
| API | `POST /<WABA_ID>/message_templates` (`name`, `category`, `language`, `components`) | **X2 faisable sans WhatsApp Manager** |
| Nom | max 512 car., **minuscules alphanumériques + underscores** | Slugifier la saisie du commerçant |
| Quota | **250 templates/WABA** si portefeuille non vérifié ; **6 000** si vérifié avec nom d'affichage approuvé | 250 suffit, sauf multiplication FR/EN qui double la consommation |
| Paramètres | Nommés `{{first_name}}` **ou** positionnels `{{1}}` — **jamais les deux** | Erreur `132000` si le nombre de valeurs ne correspond pas |
| Délai d'approbation | « **up to 24 hours** », automatisé + revue manuelle | **Un commerçant ne peut pas lancer de campagne le jour de son inscription.** À dire dans l'onboarding |
| Appel | Décision « within 24 hours », échantillon requis | Fonctionnalité d'appel, ou renvoi explicite vers WhatsApp Manager |
| Motifs de rejet | `ABUSIVE_CONTENT` · `INCORRECT_CATEGORY` · `INVALID_FORMAT` · `NONE` · `PROMOTIONAL` · `SCAM` · `TAG_CONTENT_MISMATCH` · `CATEGORY_NOT_AVAILABLE` (déprécié) | **Table de traduction FR à écrire** — le commerçant ne comprendra pas `TAG_CONTENT_MISMATCH` |
| Notification de statut | Webhook `message_template_status_update` — **14 états** : `APPROVED`, `ARCHIVED`, `UNARCHIVED`, `DELETED`, `DISABLED`, `FLAGGED`, `IN_APPEAL`, `LIMIT_EXCEEDED`, `LOCKED`, `PAUSED`, `PENDING`, `REINSTATED`, `PENDING_DELETION`, `REJECTED` | **14 états, pas 3.** `PAUSED` et `DISABLED` sont des états d'**exécution**, pas de création |
| Détail du rejet | `rejection_info {reason, recommendation}`, `disable_info`, `other_info` | Meta fournit une **recommandation textuelle** — l'afficher telle quelle au commerçant |
| 🔴 Routage | **Non surchargeable**, `entry[].id` = **WABA ID** | Routage par WABA ID obligatoire (§1) |
| Pause qualité | Pause pour retours négatifs récurrents ou faible taux de lecture — **durées non documentées** | **Revérifier le statut au moment de l'envoi**, pas seulement à la création |

## 8. Embedded Signup / Tech Provider

**Prérequis :** app Meta avec le cas d'usage WhatsApp · **vérification d'entreprise** ·
**App Review** avec vidéos démontrant l'envoi de message et la création de template ·
**Advanced access** à `whatsapp_business_messaging` et `whatsapp_business_management` ·
webhooks configurés.

### 🔴 Limite d'onboarding — et elle est basse

| Phase | Limite |
|---|---|
| Avant vérification + App Review | **10 nouveaux clients par fenêtre glissante de 7 jours** — et **0 avant approbation** |
| Après | **200 par fenêtre glissante de 7 jours** (~800/mois) |
| Au-delà | Statut **Meta Business Partner** requis |

**→ Le rythme d'acquisition est plafonné par Meta, pas par la capacité commerciale.**
File d'attente d'onboarding + compteur glissant 7 jours au back-office + date d'activation
communiquée au prospect.

### Étapes techniques
1. `GET /oauth/access_token` (`client_id`, `client_secret`, `code`) → **business token**
2. `POST /<WABA_ID>/subscribed_apps`
3. `POST /<PHONE_NUMBER_ID>/register` avec `messaging_product: "whatsapp"` et **`pin` à 6 chiffres**
4. Message de test (optionnel)
5. **Le client ajoute son propre moyen de paiement** via WhatsApp Manager

| Contrainte | Valeur | Conséquence |
|---|---|---|
| 🔴 TTL du code d'échange | **30 secondes** | Échange serveur-à-serveur **synchrone et instrumenté**. Un échec = reprise complète du flux par le commerçant |
| Webhook prérequis | `account_update` obligatoire — **non surchargeable** | URL par défaut |
| PIN 2FA | 6 chiffres, requis à l'enregistrement | **Générer, chiffrer et conserver un PIN par numéro** (nécessaire au ré-enregistrement). Entité sensible absente du modèle |
| Facturation | Tech Provider : « clients **must provide their own payment method**… Meta will then bill these clients » | **Étape bloquante** : sans moyen de paiement chez Meta, pas de template payant. À vérifier **avant** de proposer une campagne |
| ⏳ Version | « **Embedded signup v2 will be deprecated on October 15, 2026.** Migrate to v4 » | **Construire directement en v4.** Ne jamais suivre un tutoriel v2/v3 |
| Expiration du business token | **non documentée** (le template de config s'appelle « With 60 Expiration Token » — **non retenu comme fait**) | Détecter le token invalide (`PARTNER_APP_UNINSTALLED` dans `account_update`) + parcours de reconnexion |
| Délai d'App Review | **non documenté** | C'est pourtant le facteur limitant du lancement → **question au support Meta** |
| Causes de rejet d'App Review | **non documenté** | Idem |
| Config app requise | Domaines HTTPS dans « Allowed domains » + « Valid OAuth redirect URIs » ; toggles Client/Web OAuth login, Enforce HTTPS, Embedded Browser OAuth Login, Strict Mode, Login with the JavaScript SDK | Configuration manuelle au dashboard, à documenter dans le brief agent |

## 9. Statuts de message

- Valeurs : `sent`, `delivered`, `read`, `failed`, **`played`** (note vocale lue, disponible depuis
  le 17 mars 2026). **Surchargeables** (font partie de `messages`).
- 🔴 **`delivered` n'est pas garanti** : « the message is both delivered and read at the same time…
  the **`delivered` webhook is not sent** because it's implied ». **Ne jamais exiger `delivered`
  avant `read`** — la machine à états doit accepter la transition directe. Impact direct sur le taux
  de délivrance affiché.
- `read` garanti ? **non documenté** — traiter comme non garanti (accusés de lecture désactivables).
- Le coût réel par message est dans l'objet **`pricing`** — **seule source fiable pour I3 / Q13**.
- ⚠️ **v24.0+ : l'objet `conversation` est omis**, sauf fenêtre d'entrée gratuite ouverte.
  **→ L'état de la fenêtre 24 h doit être calculé par ContexFly** depuis le `timestamp` du dernier
  message entrant, pas lu de `conversation`.

## 10. 🔴 Coexistence au Cameroun — **NON TRANCHABLE**

**La page officielle de la coexistence ne contient aucune mention de pays, de région ni
d'éligibilité géographique.** Le Cameroun n'y est ni autorisé ni exclu.

Ce qui est documenté : les pays **exclus de la plateforme** sont Cuba, Iran, Corée du Nord, Syrie
et trois régions d'Ukraine — **le Cameroun n'y figure pas**, donc la Cloud API est utilisable. Mais
cela ne dit **rien** de la coexistence.

⚠️ Des résultats de recherche évoquaient une restriction pour les portefeuilles à adresse Brésil ou
Inde et un support ajouté au Nigeria et à l'Afrique du Sud — **la page officielle n'a pas pu être
rendue** (changelog Meta en erreur 500 répétée). **Non retenu comme fait.**

**Contraintes de coexistence documentées :**
- App WhatsApp Business **2.24.17+**
- **20 mps** fixes
- Historique **180 jours** en 3 phases ; **médias uniquement des 14 derniers jours** →
  **l'historique arrive par vagues asynchrones**, l'inbox doit accepter l'insertion rétroactive
- 🔴 **Fenêtre de synchro : 24 h après l'onboarding, sinon ré-enregistrement complet.** Sur un marché
  à connectivité instable, l'échec est probable → détection + relance dans P7w
- **Groupes non synchronisés** → les commerçants qui vendent en groupe sont hors périmètre
- Messages éphémères, vue unique, position en direct désactivés ; listes de diffusion en lecture
  seule → **perte de fonctionnalité pour le commerçant, argument de rétention à anticiper**
- Webhooks spécifiques `smb_message_echoes`, `smb_app_state_sync`, `history` — **surchargeables**
- 🔴 `ACCOUNT_OFFBOARDED` = « offboarded due to a **device change or phone number reregistration** » ;
  `ACCOUNT_RECONNECTED`. **Un commerçant qui change de téléphone casse son intégration.** Sur ce
  marché, c'est un mode d'échec **normal**, pas rare → alerte + parcours de reconnexion obligatoires

## 11. Messages interactifs — limites exactes

**Boutons de réponse :** max **3** · libellé **20 car.** et **unique** · `id` 256 · corps 1024 ·
pied 60 · en-tête `document`/`image`/`text`/`video`.

**Messages liste :** max **10 sections**, mais **10 lignes au total toutes sections confondues** ·
en-tête 60 · corps 4096 · pied 60 · bouton 20 · **titre de ligne 24** · description 72 · `id` 200 ·
titre de section 24.

**Bouton CTA URL :** `display_text` **20 car.** · corps 1024 · pied 60 · en-tête 60.
Nombre de boutons et longueur d'URL **non documentés**.

**Conséquences :**
- 🔴 **10 lignes maximum au total** — pas 10 par section. **Un catalogue de 40 produits ne peut pas
  être présenté en une liste** → pagination (« Voir plus » en 10ᵉ ligne) ou catalogue natif (X4).
- **Titre de ligne 24 caractères** : « Robe wax taille 42 bleu » est tronqué. Le modèle produit doit
  stocker un **libellé court séparé**, jamais dériver du nom complet.
- **Bouton 20 caractères** : « Confirmer ma commande » = 21 → rejeté. **Valider les libellés générés
  par le LLM avant envoi**, et dédoublonner (boutons non uniques = rejet).

---

## Contraintes qui imposent une fonctionnalité non prévue

| # | Contrainte | Fonctionnalité manquante |
|---|---|---|
| **N1** | `message_template_status_update` et `account_update` non surchargeables, sans `phone_number_id` | **Second routeur de webhooks** indexé sur le **WABA ID**. Correspondance `WABA_ID → commerçant` |
| **N2** | 14 états de template, 8 motifs de rejet, `recommendation` textuelle, appel sous 24 h | **Écran d'administration des templates** par commerçant : statut, motif traduit, recommandation Meta, correction et resoumission |
| **N3** | Onboarding **10 puis 200 clients / 7 jours glissants** | **File d'attente d'onboarding** + compteur glissant au back-office + date d'activation communiquée |
| **N4** | **1 message / 6 s** vers le même utilisateur | **Agrégateur de réponse** : un seul message par tour. Le workpool doit plafonner **par paire**, pas seulement par numéro |
| **N5** | `held_for_quality_assessment` + portfolio pacing | **État « retenu par Meta »** distinct de `sent` et `failed`, affiché dans l'écran de campagne |
| **N6** | Médias : URL 5 min, ID webhook 7 j, auth obligatoire | **Pipeline de ré-hébergement** de tout média entrant + **compression** de tout média sortant. Coût de stockage non modélisé |
| **N7** | Pas de transcription fournie par Meta | **X13 — service de transcription vocale**, avec son coût par minute |
| **N8** | PIN 2FA, `verify_token`, business token | **Coffre de secrets par commerçant** → `Exigences-Non-Fonctionnelles.md` |
| **N9** | Le commerçant ajoute **son propre** moyen de paiement chez Meta | **Étape bloquante d'onboarding + vérification avant toute campagne payante** |
| **N10** | `ACCOUNT_OFFBOARDED` sur changement d'appareil | **Surveillance de santé de connexion + parcours de reconnexion.** Mode d'échec fréquent ici |
| **N11** | Aucune idempotence à l'envoi | **Verrou d'envoi + enregistrement avant appel HTTP** |
| **N12** | 10 lignes max, titre 24 car. | **Pagination de catalogue** + **libellé court** distinct du nom produit |
| **N13** | Embedded Signup v2 déprécié le 15/10/2026 | Construire en **v4** dès le départ |

---

## Ce qui n'a pas pu être vérifié

1. 🔴 **Disponibilité de la coexistence au Cameroun** — aucune page officielle ne liste de pays ;
   changelog Meta en erreur 500. **Ne pas construire l'onboarding en supposant la coexistence
   disponible.**
2. **Délai d'App Review Tech Provider et causes de rejet** — non documenté, alors que c'est le
   facteur limitant du lancement.
3. **Expiration du business token** — non documentée.
4. **Délai maximal de réponse attendu du webhook** — non documenté.
5. **Garantie d'ordre des webhooks** — aucune déclaration Meta.
6. **Contradiction 7 jours / 36 heures** entre deux pages officielles — non résolue.
7. **Durée de rétention du portfolio pacing** — non documentée.
8. **Signature sur les endpoints alternatifs** — hypothèse à valider par un test réel.
9. **Nombre maximal d'alternate webhook endpoints** — non documenté.
10. **Nombre de boutons CTA URL et longueur max d'URL** — non documentés.
