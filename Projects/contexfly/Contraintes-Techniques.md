# Contraintes techniques & décisions d'outillage — ContexFly

**Destiné à l'agent de codage.** Tout ce qui est écrit ici a été **vérifié à une source**, pas
supposé. Chaque fait porte sa date de vérification. Ce qui n'a pas été vérifié est marqué comme tel.

> ⚠️ **Ne pas redécider ce qui est ici.** Ces points ont été tranchés avec leur raison. Si une
> contrainte semble fausse, la vérifier à la source citée avant de s'en écarter — et signaler
> l'écart, ne pas le contourner silencieusement.

---

## 1. Contraintes externes non négociables

### 1.1 WhatsApp / Meta *(vérifié les 15-17 août 2026)*

| Contrainte | Détail | Conséquence pour le code |
|---|---|---|
| **Fenêtre de service 24 h** | Hors fenêtre, seuls des templates pré-approuvés partent | Toujours connaître l'état de la fenêtre par conversation ; l'exposer dans l'UI (E2) |
| **Tarification par message délivré** | Depuis le 01/07/2025. Service gratuit dans la fenêtre depuis le 01/11/2024 ; *utility* gratuit dans la fenêtre ; **marketing facturé, sans dégressivité** | Choisir la catégorie de template consciemment — un rappel de commande formulé en *utility* est gratuit, en *marketing* il est payant et plafonné |
| **Plafond d'envoi** | Démarrage à **250 destinataires uniques / 24 h**. **Calculé au niveau du portefeuille**, partagé par tous les numéros qu'il contient (depuis le 07/10/2025) | Un numéro peut épuiser le quota des autres. Ne compte **que** les messages hors fenêtre de service — la prise de commande entrante n'est jamais plafonnée |
| **Plafond de fréquence marketing** | **~2 messages marketing par utilisateur final et par jour, tous expéditeurs confondus**, appliqué au niveau de l'utilisateur | **Erreur `131049`.** La délivrance d'une campagne ne peut jamais être garantie. Gérer l'échec, réessayer plus tard, ne pas le présenter comme une faute du commerçant (F7) |
| **Note de qualité** | Vert / jaune / rouge, calculée sur le **taux de blocage des destinataires** | Dégradation → réduction des limites → bannissement. Algorithmique, sans revue humaine |
| **🔴 Interdiction des IA généralistes** | Depuis le **15/10/2025** (nouveaux comptes API) et le **15/01/2026** (tous). Les agents scopés à un **processus métier** sont explicitement autorisés | **A12** : pas de champ de prompt libre illimité. Le périmètre de l'agent est verrouillé par son jeu d'outils, pas par une consigne |
| **Opt-in** | Explicite, spécifique au canal, preuve conservée (date, source), désabonnement facile | **F5 avant F4**, sans exception |
| **Une app Meta, plusieurs numéros** | Une seule URL de rappel par application — modèle voulu. **Chaque app exige sa propre App Review** | **Une seule application Meta** (confirmé) |
| ⚠️ **Alternate webhook endpoints — couverture partielle** *(corrigé le 19/08)* | Une URL propre par WABA ou par numéro est possible, **mais uniquement pour le trafic conversationnel** (`messages`, `message_echoes`, `history`…). **NON surchargeables** : `message_template_status_update`, `message_template_quality_update`, `template_category_update`, `account_update`, `account_review_update`, `account_alerts` | 🔴 **Deux chemins d'entrée obligatoires** : (1) un routeur multi-tenant sur l'**URL par défaut**, dispatchant sur `entry[].id` = **WABA ID** — ces webhooks ne contiennent **aucun** `phone_number_id` ; (2) des endpoints par tenant pour `messages`. **→ Table `WABA_ID → commerçant` obligatoire**, en plus de `phone_number_id → commerçant`. URL ≤ 200 car. ; `verify_token` **par commerçant** |
| **Débit d'envoi** | 80 mps par défaut · **20 mps en coexistence** · 🔴 **1 message toutes les 6 s vers le même utilisateur** (erreur `131056`) | **Agréger la réponse de l'agent en un seul message.** Limiteur **par paire** (numéro commerçant, numéro client), pas seulement par numéro. ⚠️ L'erreur `4` (limite d'appel de l'app) est **partagée par tous les commerçants** |
| **Portfolio pacing** | Lissage par lots des templates sous 500 K/365 j → **tous les commerçants concernés**. Statut `held_for_quality_assessment`, échec `135000` | **Un `200 OK` ne veut pas dire envoyé.** État « retenu par Meta » distinct de `sent` et `failed` |
| **Onboarding plafonné** | **10 nouveaux clients / 7 jours glissants** avant App Review (et **0 avant approbation**), **200** après | **Le rythme d'acquisition est plafonné par Meta**, pas par la capacité commerciale. File d'attente + compteur glissant |
| **Embedded Signup** | v2 **déprécié le 15/10/2026** · code d'échange TTL **30 s** · PIN 2FA 6 chiffres à conserver · le client ajoute **son propre** moyen de paiement Meta | Construire en **v4**. Échange serveur-à-serveur synchrone. **Coffre de secrets par commerçant** |
| **Médias** | Image sortante **≤ 5 MB, 8-bit RGB** · ID reçus expirent **7 j**, URL **5 min**, téléchargement **authentifié** | **Ré-hébergement systématique** de tout média entrant ; **compression serveur** de tout média sortant |
| **Messages interactifs** | 3 boutons max, libellé **20 car. unique** · liste : **10 lignes au total toutes sections confondues**, titre de ligne **24 car.** | **Pagination du catalogue** ; **libellé court** distinct du nom produit ; **valider les libellés générés par le LLM** avant envoi |
| **Fenêtre 24 h** | v24.0+ : l'objet `conversation` est **omis** des webhooks de statut | **Calculer l'état de la fenêtre soi-même** depuis le `timestamp` du dernier message entrant |
| **Coexistence** | App WhatsApp Business + Cloud API sur le même numéro, 6 mois d'historique synchronisé. Groupes non supportés | ⚠️ **Disponibilité au Cameroun non confirmée** (Q8/Q24) — ne pas en faire un argument commercial avant vérification |

### 1.2 Paiement *(Notch Pay, retenu le 16/08/2026)*

- **Notch Pay Sync** — offre marketplace : comptes sous-marchands, split payment, reversements de
  masse automatisés. **KYC de personne physique**, ce qui permet d'onboarder un commerçant sans
  société (contrairement au KYB seul de PawaPay).
- **🔴 ContexFly ne détient jamais les fonds.** Ils restent chez l'agrégateur. ContexFly est
  intermédiaire technique — c'est ce qui évite un agrément EME / établissement de paiement
  (BEAC, BCEAO, CBN). **Toute conception qui ferait transiter les fonds par un compte ContexFly est
  à refuser.**
- Encaissement **MTN MoMo + Orange Money**, en **XAF**.
- **💰 Frais retenus (Maxime, 2026-08-19) : 2 % à l'encaissement + 1 % au reversement = 3 % au
  total.** Ces frais sont **connus et assumés** ; Maxime a une connaissance directe du
  fonctionnement de Notch Pay, c'est la raison de ce choix d'agrégateur.
  *(Note : la page tarifs publique affiche 1 % + 1 %. Les chiffres retenus ici sont ceux de Maxime
  et font foi — la divergence est signalée pour qu'elle ne surprenne personne, pas pour être
  arbitrée.)*
  🔴 **Obligation produit qui en découle : les 3 % doivent être visibles du commerçant**, dans le
  produit et documentés dans la documentation de la plateforme. Ce n'est pas un détail de
  transparence — c'est ce qui évite que le commerçant découvre l'écart entre le montant encaissé et
  le montant reversé, et attribue la différence à ContexFly.
- ⚠️ Non confirmé au contrat (Q21) : pièces exactes pour un sous-marchand personne physique,
  plafond de volume, délai de reversement, répartition de responsabilité en cas de fraude.

### 1.3 Juridique

- **Loi camerounaise n°2024/017**, applicable au 23 juin 2026 — **déjà en vigueur** — à portée
  **extraterritoriale** : elle s'applique dès qu'une donnée de citoyen camerounais est traitée,
  quel que soit le lieu d'immatriculation. Politique de confidentialité et recueil du consentement
  à concevoir comme un **module déclinable par pays**, faute de cadre africain unifié.

### 1.4 Terrain

- Connectivité instable, usage **mobile-first**, bilinguisme FR/EN et pidgin fréquent.
- Adresse = **ville + quartier structurés** (listes définies par le commerçant) **+ repère libre
  facultatif**. Jamais une adresse postale à l'occidentale.
- Le paiement à la livraison est massivement pratiqué — toute conception qui l'exclut se coupe du
  marché.

---

## 2. Décisions d'outillage — quoi, et pourquoi

### 2.1 Retenus

| Outil | Rôle | Pourquoi |
|---|---|---|
| **`ai-builder-saas`** | Socle | TanStack Start, Convex, Better Auth, Zod, shadcn/ui, Tailwind, Paraglide JS |
| **`@convex-dev/agent`** | L'agent vendeur | **Contexte d'agent typé** → isolation multi-activités (§3.1) · **`needsApproval`** statique ou dynamique → couvre **D5** et **P1** nativement · **outils définis à plusieurs niveaux** → jeu d'outils dérivé de la configuration (**A4/A12**) · fils et historique → **A7** |
| **`@convex-dev/workflow`** | Processus longs | `step.sleep`, `runAt`, reprises, `awaitEvent`. **Durable, survit aux redémarrages.** Couvre **A8** (relance 3 h / 48 h), **D1** (acompte → solde), **D7**, **P3**, **F4**, **H5** |
| **`@convex-dev/workpool`** | Limitation de débit sortant | **Obligatoire, pas optionnel.** Applique en un seul endroit les trois plafonds Meta simultanés. Sans lui, une campagne de 500 contacts brûle le quota et dégrade la note de qualité du numéro du commerçant |
| **AI SDK (`ai`)** | Socle du composant Agent | Permet de **changer de modèle sans réécrire les outils** — soupape économique face au coût d'inférence |
| **Gemini 2.5 Flash** | Modèle principal de l'agent | Décision Maxime : le fournisseur est **Gemini**. Tarif vérifié le 19/08/2026 : **0,30 $/M en entrée, 2,50 $/M en sortie** — le seul qui tienne dans la bande de prix locale (voir §5) |
| **Gemini 3.1 Flash-Lite** | Tâches à fort volume et faible enjeu (classification d'intention, routage) | **0,25 $/M · 1,50 $/M**. Environ 20 % moins cher que 2.5 Flash sur un profil dominé par l'entrée |
| **Zod** | Schémas d'arguments d'outils | ⚠️ **Les descriptions Zod font partie du prompt** : c'est ce que le modèle lit pour décider quand appeler un outil. Ce n'est pas de la documentation |

### 2.2 Écartés — ne pas les réintroduire

| Écarté | Raison |
|---|---|
| **n8n** | Architecture initialement prévue, abandonnée le 17/08/2026. En détaillant les interactions, seuls l'agent et les requêtes HTTP restaient utilisés → n8n n'ajoutait qu'un saut réseau et un service à héberger. Le multi-activités (G1) l'aurait de toute façon mal supporté, et les invariants d'argent (D5) sont plus difficiles à garantir à distance |
| **Connexion WhatsApp non officielle** (QR code, Baileys) | Bannissement = mode d'échec normal, pas cas rare. Diluerait l'avantage de conformité, qui est l'axe de différenciation |
| **Applications Meta séparées par activité** | Chaque app exige sa propre App Review → multiplierait les délais Meta, qui sont déjà le facteur limitant du lancement |
| **Genuka WA comme fournisseur d'API** | Écarté le 17/08/2026. ContexFly va directement au statut Meta Tech Provider |
| **Système de facturation client-final** | Exploré puis abandonné avant l'analyse |
| **Détention des fonds par ContexFly** | Imposerait un agrément EME / établissement de paiement |
| **Scan périodique des conversations (~1 min)** pour A8 | Remplacé par `step.sleep` — chaque conversation programme sa propre échéance. Moins de charge, pas de dérive |

### 2.3 À trancher, non décidé

- Observabilité et coût par conversation (I3, Q13) — plusieurs solutions existent, **non évaluées**.
- Streaming partiel et annulation d'une génération en cours (utile pour P1 et A6).
- Ce que **Better Auth** couvre réellement de la structure `compte → activité → membre` (G1/G3).
- Compatibilité des composants avec **TanStack Start** telle qu'utilisée dans `ai-builder-saas`.

---

## 3. Sécurité — règles d'implémentation

> **Le modèle ne choisit jamais le périmètre. Il ne choisit que l'intention.**

### 3.1 🔴 L'identifiant d'activité vient du contexte, jamais des arguments

```ts
const agent = new Agent<{ activiteId: string }>(...)
type MyCtx = ToolCtx & { activiteId: string }
```

**Aucun outil ne doit accepter `activiteId`, `commercantId` ou `clientId` en paramètre d'entrée.**

L'interlocuteur de l'agent est un **client final inconnu, sur WhatsApp**. Si le périmètre transitait
par les arguments, une injection de prompt suffirait à franchir la frontière entre commerçants.

**Corollaire :** les fonctions appelées par les outils sont des `internalQuery` / `internalMutation`
Convex — **jamais des fonctions publiques**.

### 3.2 Un outil = une action métier étroite

❌ `queryDatabase(sql)` · `getTable(name)` · `updateRecord(table, id, data)`
✅ `chercherProduitsDisponibles({ categorie, taille })` · `ajouterAuPanier({ produitId, variante,
quantite })` · `calculerFraisLivraison({ quartierId })` · `proposerRemise({ pourcentage })`

Le périmètre est dans le code de l'outil, pas dans le prompt. C'est aussi ce qui rend **A12**
applicable : un agent qui n'a que des outils de vente ne peut pas devenir généraliste.

### 3.3 Tout invariant d'argent est recalculé côté serveur

`proposerRemise` ne fait **pas** confiance au pourcentage décidé par l'agent : elle recalcule le
plafond depuis l'historique réel du client et le palier de fidélité, et rejette au-delà.
`needsApproval` s'ajoute par-dessus — **il ne remplace pas la revérification**.

Même règle pour : total du panier, frais de livraison, pourcentage d'acompte, stock à la validation.
**Tout ce qui touche à l'argent est recalculé à l'écriture, jamais repris du dialogue.**

### 3.4 Le jeu d'outils dérive de la configuration du commerçant

Les interrupteurs d'**A4** et les accès aux données d'**A5** se traduisent en liste d'outils
transmise à l'agent. Ce qui est désactivé **n'existe pas** dans son contexte.
Stock non suivi sur un point de vente (**G2**) → l'outil de vérification n'est pas fourni, l'agent
répond prudemment au lieu d'affirmer.

### 3.5 Journalisation de chaque appel d'outil

Arguments, résultat, durée, coût. Trois usages : **I2** (calcul du taux d'autonomie), **P2**
(apprentissage des reprises humaines), et la **piste d'audit** en cas de litige sur une commande ou
une remise.

### 3.6 Le propriétaire écrit à son propre agent

**A14** permet au commerçant de piloter son agent depuis WhatsApp. L'agent doit donc **distinguer
son propriétaire de ses clients sur le même numéro** et basculer de registre. **Le numéro du gérant
doit être vérifié** — sinon une usurpation de numéro permet de fermer la boutique.

---

## 4. Ordres de dépendance à respecter

Ces enchaînements ne sont pas des préférences, ce sont des conditions de correction :

- **F5 (consentement) avant F4 (campagnes)** — obligation Meta.
- **D5 (plafond serveur) avant F2 (remise en conversation)** — sinon un client négocie -80 %.
- **C1 (objet Commande) avant A8, F1, F2, I2** — tout en dépend.
- **C2 (statuts) avant D1** — sans statut « livrée », l'encaissement à la livraison et le solde
  d'acompte ne se bouclent pas.
- **C4/C5 (zones) avant C3 (fiche livreur)** — sans zone, pas de frais ni de couvrabilité.
- **B0 avant A1 en qualité** — un agent vendeur ne vaut que la donnée produit derrière lui.


---

## 5. 💰 Coût d'inférence — modélisation (répond à Q13)

**Fournisseur imposé : Gemini** (décision Maxime, 2026-08-19). Tarifs **vérifiés le 19/08/2026**.

### Tarifs relevés

| Modèle | Entrée / M tokens | Sortie / M tokens |
|---|---|---|
| **Gemini 2.5 Flash** | **0,30 $** | **2,50 $** |
| Gemini 3.1 Flash-Lite | 0,25 $ | 1,50 $ |
| Gemini 3.7 Flash | 0,75 $ | 3,75 $ ⚠️ **doublent le 01/01/2027** |
| Gemini 3.5 Flash | 1,50 $ | 9,00 $ |
| Gemini 2.5 Pro | 1,25 $ | 10,00 $ (≤200 K contexte) |

### Hypothèses de charge — **ce sont des hypothèses, pas des mesures**

Une conversation de vente type : **10 tours**. Par tour, environ **4 500 tokens en entrée**
(prompt système + configuration de l'agent + extrait de catalogue + historique + résultats d'appels
d'outils) et **150 tokens en sortie** (N4 impose une réponse unique et courte).
→ **≈ 45 000 tokens en entrée, 1 500 en sortie par conversation.** Conversion à ~600 FCFA/$.

### Coût par conversation, et à 20 conversations/jour

| Modèle | Par conversation | Par mois (600 conv.) | Marge sur un abonnement à 15 000 FCFA |
|---|---|---|---|
| **Gemini 2.5 Flash** | **≈ 10 FCFA** | **≈ 6 000 FCFA** | **≈ 60 %** avant infra et Notch Pay |
| Gemini 3.1 Flash-Lite | ≈ 8 FCFA | ≈ 4 800 FCFA | ≈ 68 % |
| Gemini 3.7 Flash (intro) | ≈ 24 FCFA | ≈ 14 400 FCFA | **≈ 4 % — intenable** |
| Gemini 3.7 Flash (2027) | ≈ 48 FCFA | ≈ 28 800 FCFA | **perte** |

### Ce que ça tranche

- ✅ **Un abonnement à 15 000 FCFA/mois avec conversations illimitées tient — sur 2.5 Flash.**
  Le pari signalé au benchmark n'en est pas un, à condition de choisir le bon modèle.
- 🔴 **Le même abonnement est intenable sur Gemini 3.7 Flash**, et devient une perte après le
  1er janvier 2027 quand son tarif d'introduction double. **Ne jamais budgéter sur un tarif
  d'introduction.**
- **Point de comparaison :** Fiitsa facture **100 FCFA par conversation et par jour**. Le coût réel
  sur 2.5 Flash est de **~10 FCFA par conversation**. Leur tarification est donc environ **10×**
  le coût — ce qui laisse une marge de manœuvre commerciale confortable à ContexFly.

### Les deux leviers d'optimisation, par ordre d'effet

1. **La mise en cache du prompt.** Le prompt système, la configuration de l'agent et l'extrait de
   catalogue se répètent à chaque tour et représentent **l'essentiel des 45 000 tokens d'entrée**.
   C'est de loin le premier levier — à instrumenter dès le départ.
2. **Le routage par modèle.** Flash-Lite pour la classification d'intention et le routage,
   2.5 Flash pour la conversation. L'AI SDK rend ce basculement possible sans réécrire les outils.

⚠️ **Ces chiffres reposent sur des hypothèses de volumétrie non mesurées.** I3 (suivi de
consommation) doit être instrumenté **dès le premier jour**, même sans écran, pour les remplacer
par des mesures réelles avant de figer la tarification.

---

## 6. Règles pour le `CLAUDE.md` de l'agent de codage

Directives **courtes et toujours applicables**, à porter dans le `CLAUDE.md` du projet de code —
pas seulement ici. Une règle qui doit être respectée à *chaque* fichier écrit doit vivre là où
l'agent la relit à chaque session.

1. **🔴 Jamais de suppression réelle.** Toute « suppression » demandée par un utilisateur est un
   **changement de statut** (`deleted`, `archived`) : la donnée disparaît pour lui, reste visible et
   **réactivable par l'administrateur ContexFly**, et n'est jamais effacée de la base. Seule
   transformation destructive autorisée : l'**anonymisation** des données personnelles au terme du
   délai de rétention.
2. **Tout montant est recalculé côté serveur au moment de l'écriture.** Total, frais de livraison,
   remise, acompte, reste dû. Jamais repris d'une saisie ni d'un dialogue avec l'agent IA.
3. **L'identifiant d'activité vient du contexte, jamais des arguments.** Aucun outil d'agent IA
   n'accepte `organizationId` en paramètre d'entrée. Les fonctions appelées par les outils sont
   `internalQuery` / `internalMutation`, jamais publiques.
4. **Un outil d'agent IA est une action métier étroite**, jamais un accès base générique. Le
   périmètre est dans le code de l'outil, pas dans le prompt.
5. **Tout webhook entrant est idempotent.** Meta et Notch Pay annoncent tous deux des doublons.
   Déduplication persistante en base avec contrainte d'unicité, jamais un cache mémoire.
6. **Répondre 200 immédiatement à un webhook, traiter en asynchrone.** Jamais d'appel au modèle
   dans le cycle de requête d'un webhook.
7. **Une réponse de l'agent = un seul message WhatsApp.** Limite Meta d'un message toutes les 6
   secondes vers le même destinataire.
8. **Aucun réessai automatique sur un `POST` de paiement.** Ni Meta ni Notch Pay ne fournissent de
   clé d'idempotence : la référence est générée et enregistrée **avant** l'appel.
9. **Un `200 OK` d'envoi ne signifie pas « envoyé ».** L'état `retenu par Meta`
   (`held_for_quality_assessment`) existe et doit être modélisé.
10. **Montants en FCFA entiers.** Le XAF n'a pas de subdivision en usage.
