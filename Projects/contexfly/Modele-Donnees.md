# Modèle de données & rôles — ContexFly

Établi le **2026-08-19**, après lecture du schéma Convex réel d'`ai-builder-saas`.
Niveau **métier** : entités, champs signifiants, relations, règles d'intégrité. Le détail
technique (index, validateurs) revient à l'agent de codage — le socle donne déjà les conventions.

---

## 1. 🎁 Ce que le socle couvre déjà — et ça change le périmètre

`ai-builder-saas` est bien plus avancé que ce que le dossier supposait. **Cinq domaines entiers de
ContexFly sont déjà construits.**

| Domaine ContexFly | Ce qui existe déjà | Reste à faire |
|---|---|---|
| **G1** multi-activités | `organizations`, `memberships`, `invitations` | Voir §2 — une décision à prendre |
| **G3** équipe & permissions | `rolePermissions` avec surcharge par organisation, rôles `owner`/`admin`/`member`, permissions nommées `domaine:action` | Ajouter les permissions métier ContexFly |
| **D8** abonnement | `plans`, `planPrices`, `subscriptions`, **entitlements avec quotas** | Définir les paliers et les quotas |
| **L1-L6** parrainage | `affiliatePrograms`, `affiliates`, commissions, versements | **Quasiment rien** — voir §1.2 |
| **L3** réductions plateforme | `coupons`, `promotionCodes`, `promotionRedemptions` | Rien |
| **Paiement Notch Pay** | `payments` avec `reference` **comme clé d'idempotence**, `providerReference`, et un **cron de réconciliation indexé par statut** | Voir §1.3 |
| Audit, notifications, documents, back-office plateforme | domaines dédiés | À réutiliser |

### 1.1 Conventions déjà posées, à ne pas réinventer
- **Multi-locataire par `organizationId` sur chaque ligne métier** — exactement la règle R8.
- **Montants en FCFA entiers** — « XAF has no minor unit ». Confirme le Glossaire.
- **Textes localisés** (`localizedTextValidator`) — le bilinguisme FR/EN est déjà outillé.
- **Permissions nommées `domaine:action`**, résolues par rôle, surchargeables par organisation.
- **Entitlements** : les quotas de plan sont **lus en direct**, jamais figés sur l'abonnement.

### 1.2 ⭐ Le domaine L est déjà construit
Le schéma d'affiliation couvre **tout** ce que j'avais spécifié, et parfois mieux :

| Ce que j'avais spécifié | Ce qui existe |
|---|---|
| Commission en % ou montant fixe | `rewardRule.kind` : `percent` / `fixed` |
| Commission ponctuelle ou récurrente | `rewardScope` : `first_payment`, `first_n_payments`, `duration_months`, `lifetime` |
| **Clawback** (L4) | `commissionStatus.reversed` + `maturationDays` — « days before a commission may be paid: the refund window » |
| **Seuil de versement bas** (L5) | `payoutThreshold` |
| **Versement en Mobile Money** (L5) | `payoutMethod`, `payoutPhone` |
| Attribution serveur (L2) | `cookieDays` sur le programme, `referral` écrit en base à l'inscription |
| Règle figée à l'attribution | **Copie gelée de la règle sur le `referral`** — un parrain garde ses conditions d'origine |

⚠️ **Un écart à traiter** : la commission se déclenche sur **le paiement**, alors que L1
recommandait de la déclencher sur **la première commande encaissée du filleul** — pour aligner le
parrain sur l'activation réelle, pas sur l'inscription. C'est un ajustement de règle, pas de schéma.

### 1.3 ⚠️ Deux flux d'argent à ne jamais confondre
Le socle gère **l'abonnement du commerçant à ContexFly** (`payments.organizationId` → l'organisation
paie ContexFly). ContexFly ajoute **l'encaissement du client final pour le compte du commerçant**
(D1/D3), qui est un flux différent : autre payeur, autre bénéficiaire, sous-comptes Notch Pay Sync.

**Deux tables distinctes.** Les fusionner mélangerait le chiffre d'affaires du commerçant avec ce
qu'il doit à ContexFly — et rendrait la réconciliation illisible.

Les **patterns**, en revanche, se reprennent tels quels : référence générée avant l'appel,
`providerReference` séparé, index par statut pour le cron de réconciliation (P5w).

---

## 2. ✅ Décision tranchée : une activité **est** une organisation (option A)

**Décision de Maxime, 2026-08-19.** Le multi-activités se réalise par appartenance à plusieurs
organisations. Aucune modification du socle, isolation garantie sur **une seule clé** — ce qui
protège R8, la règle qui empêche qu'une injection de prompt fasse fuiter les données d'un
commerçant vers un autre.

**Conséquences actées :**
- **Un abonnement par activité.** Trois commerces distincts = trois abonnements. Un commerçant à
  trois *points de vente* du même commerce relève de G2, pas de trois activités.
- Si un geste commercial est souhaité sur le multi-activités, il se fait avec `coupons` et
  `restrictedToOrganizationId` — **tarif dégressif à partir de la deuxième activité**, sans toucher
  au schéma.
- Chaque activité porte **son** numéro WhatsApp, **son** WABA, **son** sous-compte Notch Pay et
  **son** KYC.

---

## 3. Entités ContexFly

Toutes portent `organizationId` (= l'activité, option A).

### 3.1 Catalogue
- **`products`** — nom, **`shortLabel`** (≤ 24 car., imposé par les listes interactives, N12),
  description, catégorie, prix de base, images, actif. `categoryTemplateId` → le modèle de champs
  appris (B0).
- **`productAttributes`** — attributs **dynamiques** par produit : clé, libellé, type, valeurs
  possibles. C'est ce qui rend B0 possible ; une table à colonnes fixes le rendrait impossible.
- **`variants`** — combinaison d'attributs (pointure 42 + bleu), prix propre éventuel, référence.
- **`stockLevels`** — 🔴 **`(variantId, outletId)` → quantité.** Le stock est indexé par variante
  **et** par point de vente (G2). Un point de vente peut être `stockNotTracked` (R14).
- **`outlets`** — points de vente : nom, adresse, horaires, `stockTracked`.
- **`categoryFieldTemplates`** — ⭐ **la mémoire de B0** : par activité et par catégorie, la liste
  des champs à demander. Enrichie à chaque produit enregistré. C'est l'entité qui porte le
  différenciateur du produit.

### 3.1bis Réglages de vente de l'activité *(ajouté le 19/08 — manquait)*
- **`sellingSettings`** — **une ligne par activité** : politique de paiement retenue parmi les 5
  (D1), **pourcentage d'acompte par défaut** et **libellé affiché** au client (D2), **horaires
  d'ouverture** et **horaires de livraison, distincts** (A13), comportement hors horaires de
  livraison (refuser / accepter avec délai / remonter au gérant), **mode absence imprévue** avec sa
  consigne en texte libre (A14).
  ⚠️ Le **pourcentage d'acompte est aussi surchargeable par produit** → champ `depositPercent`
  optionnel sur `products`.

### 3.2 Clients & conversations
- **`customers`** — le client final. Téléphone (identifiant naturel), nom, langue, `optInAt`,
  `optInSource`, `optOutAt` (R18). **Jamais un utilisateur du SaaS.**
- **`customerAddresses`** — 🔴 **l'adresse appartient au client, pas à la commande** (R25). Ville,
  quartier, repère libre, `isDefault`, contacts secondaires (C6).
- **`conversations`** — statut `active`/`completed`, `lastInboundAt` (**seule source de la fenêtre
  24 h**, l'objet `conversation` de Meta n'étant plus fourni), régime `ia`/`brouillon`/`humain`,
  `assignedTo`, `autoReturnToAiAt`.
- **`messages`** — direction, contenu, `wamid` (**clé de déduplication**), statut avec l'état
  `retenu`, catégorie de template, coût réel lu dans `pricing`.
- **`carts`** *(ajouté le 19/08 — manquait)* — panier rattaché à la conversation, **persistant**
  entre deux échanges (A2). Lignes provisoires, total courant. Devient une `order` à la validation.
  Le `Glossaire` et `Architecture.md` §9.2 le nommaient sans qu'aucune entité ne le porte.
- **`mediaAssets`** *(ajouté le 19/08 — manquait)* — médias **ré-hébergés** (N6) : origine, type,
  taille, date. R32 fixait leur rétention à 6 mois sur une table qui n'existait pas.
- **`conversationTags`**, **`internalNotes`** (E5, E6).

### 3.3 Commandes & livraison
- **`orders`** — statut C2, politique de paiement appliquée, total, **montant payé**, **reste dû**,
  adresse retenue, conversation d'origine, point de vente de décrément.
- **`orderLines`** — variante, quantité, **prix unitaire figé au moment de la commande**.
- **`deliveryZones`** — ville, quartier, frais (C5). L'absence d'un quartier rend la commande non
  livrable (R22).

### 3.4 Argent (encaissement pour le compte du commerçant)
- **`merchantPayments`** — distincte de `payments` (§1.3). Référence propre générée **avant**
  l'appel, `providerReference`, statut à 6 valeurs Notch Pay, `applicationFee`.
- **`merchantLedger`** — 🔴 **registre d'écritures append-only**, jamais un champ `solde`. Imposé
  par le statut `reversed` des transferts : un reversement réputé fait peut revenir en arrière.
  Survit aussi aux deux montages possibles de Q29.
- **`merchantAccounts`** — sous-compte Notch Pay : `accountId`, statut KYC, capacités
  (`payments`/`transfers`/`payouts`), pièces transmises.
- **`disputes`** *(ajouté le 19/08 — manquait)* — litige sur une commande : motif, statut,
  résolution. **R28 refuse l'archivage d'une activité « si litige ouvert »** — condition
  invérifiable sans cette entité.
- **`webhookEvents`** — 🔴 **table de déduplication persistante**, identifiant externe unique.
  Obligatoire des deux côtés : Meta annonce des doublons, Notch Pay aussi.

### 3.5 WhatsApp & agent
- **`whatsappAccounts`** — `wabaId`, `phoneNumberId`, **`WABA_ID → activité`** (N1), mode
  coexistence, note de qualité, palier d'envoi, santé de connexion (N10).
- **`secrets`** — 🔴 **coffre chiffré par activité** : PIN 2FA, `verifyToken`, business token (N8).
- **`templates`** — nom, catégorie, **14 états**, motif de rejet, recommandation Meta (N2).
- **`agentConfigs`** — objectif, personnalité, **longueur de réponse**, langues, interrupteurs de
  périmètre (A4/A12), accès aux données (A5), plafond de remise (D5).
- **`agentToolCalls`** — arguments, résultat, durée, coût (R16). Alimente I2, I3 et P2.
- **`outboundQueue`** — file soumise à limitation de débit, **avec le couple (numéro, destinataire)**
  pour appliquer la limite par paire (N4).

### 3.6 Fidélisation
### 3.5bis Exploitation *(ajouté le 19/08 — manquait)*
- **`workflowRuns`** — exécutions de processus durables (P1w-P9w) : type, état, tentatives, date de
  reprise. Nécessaire à U25 « relancer un processus échoué » (back-office).
- **`onboardingSlots`** — compteur glissant sur 7 jours des commerçants onboardés chez Meta (N3).
  Le plafond (10 puis 200) est une contrainte de croissance à suivre, pas à découvrir.
- **`referralClicks`** *(corrige L2)* — 🔴 identifiant de clic **capté côté serveur au moment du
  clic, avant toute inscription**. L2 rejette explicitement l'attribution par cookie : les liens
  circulent dans WhatsApp, dont le navigateur intégré perd les cookies. `cookieDays` du socle ne
  suffit donc pas — il faut cette table.

- **`segments`**, **`automations`** (pré-écrites, activables), **`campaigns`**,
  **`stockAlerts`** (P3).

---

## 4. Rôles & permissions

**Décision de Maxime, 2026-08-19 :** **trois rôles.** Le rôle `admin` est abandonné au profit de
`manager` — un seul rôle intermédiaire, pas deux aux droits identiques.

| Rôle | Droits | Cardinalité |
|---|---|---|
| **`owner`** | Tout : facturation, suppression de l'activité, transfert de propriété | 🔴 **exactement 1 par activité** |
| **`manager`** (gérant) | Tout sauf facturation, suppression et transfert | plusieurs |
| **`member`** (vendeur) | Inbox, commandes, fiche livreur. Jamais l'argent ni la configuration | plusieurs |

⚠️ **Écart avec le socle, mineur :** `ai-builder-saas` définit `owner` / `admin` / `member`.
ContexFly **renomme `admin` en `manager`** — une valeur dans `roleValidator` et les lignes
correspondantes de `rolePermissions`. Aucune modification du mécanisme d'autorisation.

### R26 — Une activité a exactement un `owner`, à tout instant

Ni zéro, ni deux. Deux chemins seulement :

**Transfert de propriété.** L'`owner` désigne un successeur ; dans la **même transaction**, le
nouveau devient `owner` et **l'ancien devient `manager`**.
⚠️ **Un nouveau KYC est nécessaire** *(confirmé par Maxime, 2026-08-19)* : le sous-compte
d'encaissement est au nom de l'ancien `owner`. Ce n'est pas un changement de rôle, c'est un
**changement de marchand**. À traiter comme une étape du parcours, avec l'activité en encaissement
suspendu tant que le nouveau KYC n'est pas validé.

**Départ de l'`owner` sans successeur → l'activité passe en `deleted`.** On lui demande de
confirmer explicitement. Il n'existe pas d'état « en attente de reprise ».

🔴 **Ce n'est JAMAIS une suppression réelle** *(décision Maxime, 2026-08-19)* : l'activité passe au
statut `deleted`, **disparaît pour l'utilisateur**, et reste **visible et réactivable par
l'administrateur ContexFly**. Rien n'est effacé en base.

**Trois conditions avant d'autoriser ce passage en `deleted` :**

1. ✅ **Aucun argent en vol** — paiement en cours, reste dû, reversement non exécuté, litige
   ouvert : **refusé**, avec la liste de ce qui bloque. Supprimer une activité qui doit de l'argent
   crée un passif sans titulaire — et comme ContexFly est dans le flux, c'est lui qui en hérite.
2. ✅ **Aucune suppression réelle des données importantes** — registre d'écritures, commandes,
   paiements restent intacts. Les données personnelles des clients finaux sont **anonymisées** au
   terme du délai de rétention (loi camerounaise n°2024/017), ce qui est une transformation, pas
   une suppression.
3. ✅ **Les autres membres sont prévenus** — **notification dans l'application ET e-mail**. Un
   `manager` ou un vendeur perd son accès du fait d'une décision qui n'est pas la sienne.

*Pourquoi cette règle existe :* l'`owner` est **la personne physique vérifiée au KYC Notch Pay** et
le titulaire du WABA. Une activité sans `owner` est une activité dont le compte d'encaissement n'a
plus de titulaire identifié.

### Hors rôles de locataire, et c'est normal
- **Client final** — aucun compte. Sa seule identification est son numéro WhatsApp.
- **Admin ContexFly** — traité par `requirePlatformAdmin`, hors rôles d'organisation.
- **Parrain** — un compte Better Auth, pas un membre. Déjà le cas dans `affiliates`.

### Permissions métier à ajouter
`product:manage` · `product:read` · `order:read` · `order:manage` · **`order:mark_delivered`** ·
`conversation:read` · `conversation:reply` · `conversation:takeover` · `agent:configure` ·
`campaign:manage` · `payout:read` · `merchant_account:manage` · `outlet:manage` ·
`delivery_zone:manage` · `activity:transfer_ownership` et `activity:archive` *(réservées à l'`owner`)*

⚠️ **`order:mark_delivered` est isolée délibérément** : c'est le geste qui solde un acompte et clôt
un paiement à la livraison. Le confier à un vendeur est légitime, mais ce doit être un **choix
explicite**, pas un effet de bord du rôle.

## 5. Deux points tranchés par Felix

### 5.1 Rétention — et la distinction qui compte

**L'erreur à ne pas faire : confondre ce qu'on conserve et ce que l'agent lit.** Ce sont deux
durées différentes, pour deux besoins différents.

| Donnée | Conservation | Pourquoi |
|---|---|---|
| **Conversations `completed` et messages** | **24 mois** | Au-delà, l'historique de commandes suffit comme mémoire client, et une conversation de deux ans n'apporte rien |
| **Médias ré-hébergés** | **6 mois** | Coût de stockage réel. Meta n'en garde que 7 jours de son côté — au-delà, plus personne n'y accède |
| **Commandes, paiements, registre d'écritures** | **conservés** | Pièces comptables et trace de litige (R29) |
| **Données personnelles d'un client final** | **anonymisées après 24 mois sans activité** | Loi camerounaise n°2024/017. C'est une transformation, pas une suppression |

⭐ **Ce que l'agent lit est bien plus court : les 3 à 5 dernières conversations complétées, pas 24
mois.** La raison est économique autant que fonctionnelle — chaque token d'historique est facturé à
chaque tour, et une conversation d'il y a huit mois n'améliore pas la réponse. **Ce que l'agent
consomme comme contexte est un réglage de coût, pas une politique de rétention.**

### 5.2 Le libellé court est **dérivé par l'agent**, corrigeable par le commerçant

Le `shortLabel` (≤ 24 caractères, imposé par les listes interactives) est **proposé par l'agent B0**
au moment de l'enregistrement, et modifiable.

**Pourquoi pas une saisie :** demander deux noms par produit double la friction sur l'étape
exactement où se joue la mortalité du produit — le catalogue vide. Et raccourcir « Robe wax taille
42 bleu » en « Robe wax bleue » est précisément ce qu'un modèle fait bien.
**Validation côté serveur obligatoire** : ≤ 24 caractères, non vide, unique dans une même liste
envoyée (Meta rejette les libellés dupliqués).

---

## 6. Points restant à trancher

1. **Reprise du sous-compte Notch Pay au transfert de propriété** — un nouveau KYC est acté (R30) ;
   reste à savoir si le sous-compte se reprend ou se recrée. → question à Notch Pay.
2. **Quotas d'entitlements** — produits, points de vente, membres, conversations, campagnes.
   Le mécanisme existe ; les valeurs relèvent de `tarification`.
3. **Historisation de l'ancienne valeur** sur prix, stock et montants, pour permettre une
   restauration chirurgicale (Q40).

*(Les points « rétention » et « libellé court » ont été tranchés en §5 — retirés d'ici le 19/08.)*
