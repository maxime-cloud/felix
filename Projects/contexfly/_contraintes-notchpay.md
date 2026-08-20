# Contraintes Notch Pay — vérification documentaire du 2026-08-19

Rendu par le sous-agent `verificateur-contraintes-externes`. Documentation officielle uniquement.
Ce qui n'y figure pas est marqué **non documenté**, jamais deviné.

## 🔴 Verdict

**Le point juridique n°1 — « qui détient les fonds » — n'est documenté nulle part.** Ni la doc
développeur, ni la page produit Sync, ni le contrat marchand, ni le contrat partenaire.
**Et l'offre Sync est absente de la spécification OpenAPI officielle** (`/accounts`, `/sync`,
`/refunds` n'y figurent pas) — c'est donc une brique non contractualisée publiquement.

---

## 1. 🔴 Garde des fonds — le bloquant

| Question | Ce que dit la documentation |
|---|---|
| Titulaire juridique du solde avant reversement ? | **Rien** |
| Comptes cantonnés / ségrégués ? | **Rien** |
| Agrément BEAC/COBAC de Notch Pay ? | **Rien** — et la phrase « Notch Pay maintains all necessary licenses and registrations required to operate as a payment service provider » est **commentée dans le source** de leur page conformité, donc non publiée |
| Merchant of record ? | Terme absent des contrats |
| Période de règlement | « Funds will be held in accordance with our policies » — **durée jamais chiffrée** |
| Réserves | « reserves, security interest and credit support requirements » — mécanique non détaillée |

**Trois indices convergents (déduction, non documenté) pointent vers un transit par un solde
plateforme :**
1. `GET /balance` renvoie le solde du **compte authentifié** ;
2. les transferts exigent « sufficient funds in **your Notch Pay account** » ;
3. le split déduit l'`application_fee` **puis** transfère le reste au compte connecté.

⚠️ **Si c'est confirmé, ContexFly détient les fonds au sens économique — et R3 est violée.**
Le seul montage sûr est l'inverse : les fonds atterrissent directement sur le sous-compte du
commerçant, ContexFly n'ayant qu'un droit à commission. **La documentation ne permet pas de
trancher.**

**Conséquence retenue :** modéliser le solde commerçant comme un **registre d'écritures
append-only avec statut de reversement**, jamais comme un champ `solde`. Cette structure survit
aux deux montages possibles.

## 2. Sync — non self-serve, et hors OpenAPI

| Contrainte | Valeur | Conséquence |
|---|---|---|
| Activation | « Contact our sales team to enable Sync » + vérifications de conformité | **Dépendance externe bloquante du planning.** Aucun code Sync testable avant accord commercial |
| OpenAPI | `/accounts`, `/sync`, `/refunds` **absents** | Ne pas générer de client typé depuis l'OpenAPI. Adaptateur maison + tests manuels |
| Création de compte | `POST /accounts` `{ type, business_profile, email, phone, metadata }` | Stocker `accountId` sur le Commerçant. **Utiliser `metadata.seller_id`** pour porter l'ID interne |
| Onboarding hébergé | `POST /accounts/{id}/onboarding` `{ callback }` → URL de redirection, reprenable | Écran « compte non vérifié » + bouton « reprendre ». **Un commerçant à moitié onboardé est un état persistant à modéliser** |
| **3 types de comptes** | **Standard** (dashboard direct, payouts par le titulaire) · **Express** (onboarding 2-3 min, dashboard limité, payouts par la plateforme) · **Custom** (invisible, marque blanche, tout géré par la plateforme) | **Choix structurant et quasi irréversible.** Custom = meilleure UX mais toute la charge KYC/support sur ContexFly. Express = compromis. À trancher avec Notch Pay |
| Split | `application_fee` + `destination: { account, amount }` | **La commission ContexFly se prélève nativement.** `amount = application_fee + destination.amount`, calculé serveur |
| Frais plateforme | Fixe, pourcentage, ou combiné | Taux de commission = attribut **du commerçant**, pas constante globale |
| KYC personne physique | Nom, date de naissance, adresse, téléphone, e-mail + **pièce d'identité + selfie + justificatif de domicile** | ⚠️ **Le selfie et le justificatif de domicile sont une friction réelle** sur un onboarding mobile camerounais. À intégrer au parcours H5, pas à découvrir en production |
| Statuts de vérification | `verified` / `pending` / `rejected` (avec motif) | 3 états à refléter dans l'UI ; le motif doit remonter au commerçant |
| Capacités | `payments`, `transfers`, `payouts` activables séparément | **Ne jamais présumer qu'un compte `verified` peut encaisser.** Vérifier la capacité `payments` avant de laisser l'agent générer un lien |
| Plafond personne physique | **Non documenté** | Pas de bascule automatique avant confirmation |

## 3. Authentification

- **Trois en-têtes** : `Authorization: CLÉ_PUBLIQUE` (toutes requêtes) · `X-Grant: CLÉ_PRIVÉE`
  (opérations sensibles) · `X-Sync: sync_xxx` (opérations au nom d'un compte connecté).
- ⚠️ **La clé publique voyage dans `Authorization`** — contre-intuitif, source classique de bug.
- `X-Grant` requis sur `/balance`, `/transfers/*`, `/beneficiaries/*`, `/webhooks/*` → **ce code ne
  s'exécute jamais côté client ni dans une fonction publique**.
- **Prévoir un wrapper `forMerchant(syncAccountId)`** plutôt que des appels ad hoc : un oubli de
  `X-Sync` impute la transaction au mauvais compte, **silencieusement**.
- Clés de test préfixées `test_` → garde au démarrage refusant une clé de test en production.

## 4. Encaissement mobile money

- Flux : initialisation → le client **saisit son numéro** → invite USSD/app sur son téléphone →
  confirmation. **Deux appels** : `POST /payments` puis `POST /payments/{ref}` avec `channel`
  (`cm.mtn` / `cm.orange`) et `account_number` → **état intermédiaire persistant obligatoire**.
- Traitement annoncé : 5-30 s.
- **6 statuts** : `pending` · `processing` · `complete` · `failed` · `canceled` · `expired`.
  `expired` et `canceled` sont distincts de `failed` — messages client différents.
- ⚠️ **Délai d'expiration : non documenté.** La doc conseille seulement « après 2-3 min, invitez le
  client à vérifier son téléphone », puis un réessai à 5 min. **Ne pas coder de timeout arbitraire.**
- Code d'erreur `TIMEOUT` = « client n'a pas répondu » → relancer sur WhatsApp avec un nouveau lien,
  pas un message d'échec sec.
- ⚠️ **Plafonds Cameroun : 500 000 XAF/jour, 5 000 000 XAF/mois**, rattachés au régulateur BEAC.
  **À qui s'appliquent-ils** — client final, commerçant, ou compte plateforme ? Non tranché.
  **Si c'est au compte plateforme, c'est un bloquant de croissance majeur.**
- ⚠️ La table indique **XOF** pour `cm.orange` au Cameroun — probable coquille, à confirmer.

## 5. Webhooks

- Signature `x-notch-signature`, **HMAC SHA-256 sur le corps JSON brut** → **conserver le body brut
  avant tout parsing** ; un middleware qui parse automatiquement casse la vérification.
  Comparaison en temps constant obligatoire.
- ⚠️ **Aucun horodatage dans la signature, aucune protection anti-rejeu documentée.** Un payload
  capté reste rejouable indéfiniment.
- ⚠️ **Doublons explicitement possibles** : « the same event might be delivered multiple times ».
  → **Handler idempotent obligatoire**, avec table de déduplication persistante et contrainte
  d'unicité — pas un cache mémoire.
- Réessais : « several times with increasing delays » — **nombre et intervalles non documentés**.
  → **Concevoir la réconciliation comme si les réessais n'existaient pas.**
- **Ordre non garanti** (non documenté). → transitions à sens unique : une fois `complete`,
  ignorer un `processing` arrivé après.
- Répondre **200 immédiatement**, traiter en tâche de fond — sinon réessais donc doublons.
- ⚠️ **Contradiction dans leur propre doc** : la page Sync annonce `payment.succeeded`, toutes les
  autres `payment.complete`. → **`default` qui journalise l'inconnu, indispensable.**
- Pas de liste d'IP publiée → la signature est la seule barrière.

## 6. Si le webhook n'arrive jamais

- `GET /payments/{reference}` — et **leur propre doc dit** : « Always verify the payment status by
  calling the Retrieve a Payment endpoint before fulfilling the order ».
  → **P5w (réconciliation) est confirmé nécessaire par l'éditeur lui-même.**
- Champ `reference` personnalisable → **générer la référence côté ContexFly avant l'appel**
  (`cfly_<commandeId>_<tentative>`). Sans ça, un appel qui échoue en réseau devient une
  transaction orpheline.
- `GET /payments` permet un balayage de rattrapage — utile vu la connectivité locale.

## 7. Reversement

- **Bénéficiaire à créer au préalable** → entité distincte du Commerçant. ⚠️ Un chiffre faux dans
  le numéro envoie l'argent chez un inconnu, **sans recours**.
- `POST /transfers`, requiert `X-Grant`.
- ⚠️ « Ensure your Notch Pay account has **sufficient funds** » → indice fort de transit par un
  solde plateforme (§1).
- **Les frais s'ajoutent au montant**, ils ne s'en déduisent pas : transfert de 5 000 + 100 de
  frais = 5 100 débités.
- Statuts : `pending` · `sent` · `processing` · `complete` · `failed` · **`reversed`**.
  → ⚠️ **Un reversement réputé fait peut revenir en arrière** : le solde commerçant doit être un
  **registre d'écritures**, pas un champ numérique.
- Délai « most transfers within minutes » — formulation non contractuelle, **ne rien promettre dans
  l'UI**.
- Payouts programmés Sync (quotidien/hebdo/mensuel) annoncés, **mais aucun endpoint documenté** pour
  les configurer.
- **Montants minimum/maximum : non documentés** → bloque le choix de la fréquence de reversement.

## 8. Remboursement

- `POST /refunds` `{ payment, amount }` — ⚠️ **absent de l'OpenAPI**, à traiter comme non garanti
  tant que non testé en bac à sable.
- Partiel supporté. Fenêtre « typically 90 days ». Délai constaté 5-7 jours ouvrés.
- Les frais de traitement initiaux **ne sont pas remboursés** → un remboursement intégral coûte 1 %
  à quelqu'un. À trancher dans le modèle tarifaire.
- ⚠️ **Remboursement mobile money non confirmé** : « Some payment methods may have restrictions ».
  **Si MoMo n'est pas remboursable par API, tout le parcours litige (D7) devient manuel** — un
  écran d'administration et un processus opérationnel, pas une ligne de code.

## 9. Limites de débit et idempotence

- En-têtes `X-RateLimit-Limit` / `-Remaining` / `-Reset`. ⚠️ La valeur 100 vient d'un **exemple** et
  **la période n'est jamais précisée** → lire les en-têtes à l'exécution, ne rien dimensionner en dur.
- `429` avec `Retry-After` → back-off exponentiel respectant l'en-tête.
- 🔴 **Aucune clé d'idempotence documentée sur `POST /payments`.**
  → **Risque de double débit du client final.** Un POST qui expire côté réseau ne peut pas être
  rejoué sans risque. Le `reference` personnalisé offre *peut-être* une déduplication implicite —
  **déduction, non documentée**. À valider en bac à sable **avant de coder le moindre réessai
  automatique sur un POST**.

## 10. Frais

- Payin mobile money local : **1 %**. Payout local : **1 %**.
  → **≈ 2 % sur un aller-retour**, avant marge ContexFly.
- Pas de frais d'installation ni mensuels.
- ⚠️ **Qui supporte les frais : non documenté.** Impossible de savoir si le client paie 10 000 et le
  commerçant reçoit 9 900, ou autre chose. **À confirmer avant de coder le calcul du net.**
- ⚠️ **Tarification Sync : non documentée publiquement.** Le coût réel de l'architecture ContexFly
  est donc inconnu.

## 11. Éligibilité

- Cameroun couvert, XAF supportée. Interroger `/countries` et `/channels` au démarrage plutôt que
  de coder une liste en dur.
- Contrat marchand : « reserved for **natural persons** aged 18 and over, residing in French-speaking
  Africa », droit camerounais applicable. Cohérent avec la cible, mais **le contrat des comptes
  connectés Sync n'est pas le même** et n'a pas été trouvé.

---

## 22 questions à poser à Notch Pay

**Bloquantes — la conception ne peut pas avancer sans réponse :**
1. Sur une charge de destination, **sur quel compte les fonds atterrissent-ils** ? Qui en est le
   **titulaire juridique** entre l'encaissement et le reversement ?
2. ContexFly peut-il être **strictement intermédiaire technique**, sans jamais détenir les fonds,
   afin de ne pas relever d'un agrément EME/établissement de paiement BEAC ? **Par écrit.**
3. Notch Pay dispose-t-il d'un **agrément en zone CEMAC** ? Sous quel régime les comptes connectés
   sont-ils opérés ?
4. Les fonds des comptes connectés sont-ils **cantonnés** ?
5. En cas de défaillance de ContexFly, les commerçants récupèrent-ils leur solde **directement**
   auprès de Notch Pay ?
6. **Pièces exactes** pour un compte connecté personne physique (commerçant informel camerounais,
   sans registre de commerce) ? Le justificatif de domicile est-il obligatoire ?
7. **Plafond de volume** au régime personne physique ? Que se passe-t-il au dépassement ?
8. Les plafonds (500 000 XAF/jour, 5 000 000/mois) s'appliquent-ils au **client final**, au
   **commerçant**, ou au **compte plateforme** ?

**Structurantes — elles changent le code, pas la faisabilité :**
9. Délai d'expiration exact d'un paiement mobile money en attente ?
10. Politique de réessai des webhooks : combien de tentatives, quels intervalles, quelle durée ?
11. La signature webhook inclut-elle un horodatage ? Protection anti-rejeu ? **Identifiant
    d'événement unique** exploitable pour la déduplication ?
12. Événement de succès en mode Sync : `payment.complete` ou `payment.succeeded` ? (vos pages se
    contredisent)
13. Mécanisme d'**idempotence** sur `POST /payments` ? Un `reference` déjà utilisé renvoie-t-il 409 ?
14. **Remboursement mobile money** possible par API au Cameroun ? Total et partiel ?
15. Montants minimum et maximum d'un transfert ?
16. Les payouts programmés Sync se configurent-ils **par API** ?
17. Le 1 % est-il **déduit du montant** ou facturé au compte ? Idem pour le payout.
18. **Tarification Sync** ? Surcoût par compte connecté ou par split ?
19. Limite de débit réelle : 100 requêtes par quelle période ?
20. `cm.orange` au Cameroun : XAF ou XOF ?
21. `/accounts`, `/sync/*` et `/refunds` sont-ils **stables et supportés** ? Pourquoi absents de
    l'OpenAPI ?
22. Le **bac à sable couvre-t-il Sync** (comptes connectés, splits, payouts) ?

→ Questions 1 à 8 à envoyer à `hello@notchpay.co` / `compliance@notchpay.co`.
**La réponse à la question 1 conditionne la validité de toute l'architecture d'encaissement.**
