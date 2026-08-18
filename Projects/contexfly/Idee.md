# Idée — ContexFly

> État : Temps 1 du cadrage. Les sections marquées ⏳ attendent une réponse de Maxime.
> Les sections marquées 🔎 seront reprises au Temps 2, après le benchmark.

## Vérification de dispersion

**Constat : l'idée contient deux produits qui partagent un canal, pas un job.**

- **Produit A — commerce conversationnel entrant.** Un client final écrit, l'agent IA qualifie,
  construit le panier, encaisse, confirme. Job du commerçant : *vendre sans avoir à répondre
  soi-même*. C'est de l'opérationnel/vente. Le revenu du client est directement mesurable
  (commandes abouties).
- **Produit B — envoi de messages en masse / démarchage sortant.** Listes de contacts,
  campagnes, templates, segmentation, gestion du consentement. Job du commerçant : *toucher des
  gens qui ne m'ont pas écrit*. C'est du marketing. Acheteur, métrique et rythme d'usage
  différents.

Les deux ne sont pas étrangers l'un à l'autre — même canal, même base de contacts, et B alimente
A. Ce qui les sépare vraiment, ce sont **trois régimes différents** :

1. **Régime de conformité.** A vit majoritairement dans la fenêtre de service de 24 h, ouverte
   par le client lui-même : consentement implicite, aucun risque. B au sens « démarchage » — des
   numéros qui n'ont jamais écrit — est une violation directe de la politique Meta (opt-in
   explicite et spécifique au canal WhatsApp exigé). La sanction n'est pas un courrier
   d'avertissement : le *quality rating* du numéro (vert/jaune/rouge) chute automatiquement sur
   le taux de blocage, les limites d'envoi sont réduites, puis le numéro est banni — de façon
   algorithmique, sans revue humaine.
2. **Régime de coût.** Depuis le 1er juillet 2025, Meta facture **par message template délivré**,
   plus par conversation. Les messages de service (réponses dans la fenêtre client ouverte) sont
   **gratuits** depuis le 1er novembre 2024 ; les templates *utility* sont gratuits dans cette
   même fenêtre. Le template **marketing** est facturé à chaque envoi délivré et n'a **aucun
   palier de dégressivité**. Autrement dit : A est quasi gratuit en coût Meta, B a un coût
   variable proportionnel au volume. Deux économies opposées dans un même produit.
3. **Régime de risque pour ContexFly.** Si ContexFly outille le démarchage à froid, les numéros
   bannis de ses clients deviennent son problème de support et son churn — et potentiellement un
   risque sur son propre statut de fournisseur technique auprès de Meta.

**Recadrage — ✅ ACCEPTÉ par Maxime le 2026-08-15.** Le volet sortant est conservé mais redéfini :
pas « démarchage à froid vers des listes de numéros », mais **fidélisation et réengagement de la
base de clients qui ont déjà écrit / déjà commandé** — précisément la base que le produit A
construit tout seul, avec son historique de conversations et de commandes. L'envoi vers des
listes achetées ou scrapées passe en **scope OUT explicite**, pas en « plus tard ».

**Extension apportée par Maxime au même moment — le volet B devient un moteur de fidélisation
piloté par la donnée d'achat**, et non un simple outil d'envoi. Trois mécaniques citées :
1. **Ciblage par habitude d'achat** — envoyer un message à certains clients et pas à d'autres
   selon ce qu'ils achètent, à quelle fréquence, à quel panier moyen.
2. **Remise automatique en cours de conversation** — l'agent propose spontanément une réduction à
   un client qui a dépassé un seuil de commandes, pendant qu'il discute des produits.
3. **Automatisations de fidélisation** configurables par l'entreprise cliente.

C'est structurant, et c'est une **bonne nouvelle pour la différenciation** : un outil de campagne
générique ne peut pas déclencher sur « a commandé 3 fois » parce qu'il n'a pas la donnée de
commande. Ici, ContexFly la produit lui-même. Cette boucle donnée-de-commande → automatisation est
à ce stade le candidat le plus sérieux au rôle de vrai différenciateur produit.

⚠️ **Deux réserves posées par Felix sur cette extension** (à trancher au skill `fonctionnalites`) :
- **« Tout configurable par l'utilisateur » est un piège.** Un constructeur de règles générique
  (conditions / segments / déclencheurs / actions) est un produit à lui seul, et un gérant de
  boutique à Douala ne le configurera jamais — l'écran vide d'un rule builder reste vide. Forme
  réaliste : des automatisations **pré-écrites, activables en un clic, avec 2-3 paramètres
  chacune**. Le moteur de règles générique est Could, jamais Must. → `Questions-Ouvertes.md` Q6bis.
- **La remise automatique, c'est de l'argent manipulé par un LLM.** Le plafond de remise doit être
  contraint dans le code, jamais dans le prompt de l'agent — sinon un client négocie -80 % en
  conversation. À inscrire dans `Exigences-Non-Fonctionnelles.md` (garde-fou CLAUDE.md §9).

**Second point de dispersion, plus léger — la boîte de réception.** « Remplacer l'app WhatsApp »
est un objectif de produit à part entière (un Chatwoot). L'inbox est nécessaire ici, mais au
service d'un seul besoin : voir ce que l'agent IA a fait et reprendre la main. À cadrer comme
*inbox minimale de supervision*, pas comme *helpdesk multi-canal*. → à trancher au moment des
fonctionnalités.

## Problème

⏳ *À confirmer/préciser par Maxime — voici ce que j'extrais de sa description, non encore validé.*

Les commerçants et PME au Cameroun vendent déjà massivement sur WhatsApp, mais **à la main** :
le gérant (ou un employé) répond lui-même à chaque client, recopie la commande dans un cahier ou
un tableur, calcule le total, envoie son numéro Mobile Money, attend une capture d'écran de
confirmation, et confirme. Conséquences observées à documenter au benchmark : conversations non
répondues hors horaires ou en pic d'activité → ventes perdues ; commandes incomplètes ou erronées
parce que reconstituées de mémoire ; aucune trace exploitable des clients passés ; impossibilité
de traiter plus de conversations sans embaucher.

- **Cible déclarée :** PME et commerçants au Cameroun, puis Afrique francophone.
- ✅ **Verticale tranchée (2026-08-15) : vente de produits physiques à catalogue** — boutiques,
  cosmétique, prêt-à-porter, distribution. Exclut donc restauration/livraison et services sur
  rendez-vous comme cible primaire.
- **Aujourd'hui, sans le produit :** WhatsApp Business (app gratuite) + cahier/Excel + Mobile
  Money manuel (Orange Money, MTN MoMo) + capture d'écran comme preuve de paiement. 🔎 À
  confirmer au benchmark, y compris les concurrents non-numériques.

## Jobs To Be Done

⏳ *Formulations proposées, à valider avec Maxime.*

- **Gérant / propriétaire.** Quand mes clients m'écrivent sur WhatsApp plus vite que je ne peux
  répondre, je veux qu'une commande complète et payée arrive sans que j'aie à taper un message,
  afin de ne plus perdre de ventes ni embaucher quelqu'un pour répondre.
- **Employé / vendeur.** Quand une conversation dérape ou sort du cadre que l'agent sait traiter,
  je veux reprendre la main sur ce contact précis depuis un seul écran, afin de sauver la vente
  sans perdre le contexte de ce qui a déjà été dit.
- **Client final (acheteur).** Quand je veux commander chez un commerçant, je veux le faire dans
  WhatsApp que j'utilise déjà, être sûr du total et payer par Mobile Money, afin de ne pas avoir
  à installer une application ni à faire confiance à un site que je ne connais pas.

## Proposition de valeur

⏳ *Proposition à valider.*

> ContexFly transforme le numéro WhatsApp d'un commerçant en un point de vente qui fonctionne
> seul : l'agent IA prend la commande, encaisse par Mobile Money et confirme — 24 h/24, sans
> qu'un humain ait à répondre, et sans que le client ait à quitter WhatsApp.

Ce que l'utilisateur ne pouvait pas bien faire avant : **encaisser une commande complète sans
être présent**. Répondre, il savait faire (l'app WhatsApp Business existe). Ce que le manuel ne
permet pas, c'est le débit — traiter 50 conversations simultanées à 22 h — et la fiabilité de
l'encaissement.

⚠️ **Point de vigilance à vérifier au benchmark et à `analyse-approfondie` :** cette proposition
de valeur n'est pas propre à ContexFly au niveau mondial. Des dizaines de produits font
« agent IA + commerce sur WhatsApp ». Le différenciateur crédible est probablement local
(Mobile Money natif de bout en bout, onboarding d'un commerçant sans documents d'entreprise,
français/pidgin, prix compatible avec une PME camerounaise) et non fonctionnel. À trancher avec
`positionnement-marketing` et le sous-agent `critique-produit`, jamais par confort.

## Rôles utilisateurs

*Proposition de Felix (Temps 2) — à confirmer par Maxime.*

- **Gérant / propriétaire** (entreprise cliente) — accès complet : catalogue, politique de
  paiement, configuration de l'agent, revenus et reversements, abonnement, connexion Meta,
  invitation d'employés. C'est lui qui achète.
- **Vendeur / employé** — inbox et reprise de conversation, consultation et traitement des
  commandes. **Pas** d'accès aux revenus, à l'abonnement, ni à la configuration de l'agent.
  ✅ **Confirmé par Maxime (2026-08-15) : le multi-utilisateur est dans le périmètre.** Donc rôles
  et permissions dès le modèle de données, et question de facturation par siège à traiter au skill
  `tarification`.
- **Client final (acheteur)** — n'est **pas** utilisateur du SaaS mais acteur central du parcours :
  il vit dans WhatsApp et ne voit qu'une page web, celle du panier et du paiement. Aucune
  inscription, aucun mot de passe — c'est une contrainte de conception, pas un détail.
- **Administrateur ContexFly** — ⚠️ **l'option B en fait un rôle produit, plus seulement une
  fonction de support.** Il doit instruire le KYC des commerçants (obligation contractuelle
  PawaPay), superviser les reversements, traiter les litiges et les remboursements, et produire
  le reporting mensuel des sous-marchands. À modéliser comme un vrai back-office, pas comme un
  accès superutilisateur bricolé.

## Objectifs mesurables

*Proposition de Felix (Temps 2) — ordres de grandeur à valider, pas des engagements.*

La métrique qui juge vraiment le produit n'est pas le nombre de conversations, c'est **la part de
commandes encaissées sans qu'un humain intervienne**. Tout le reste en découle.

1. **Taux d'autonomie** — part des commandes payées obtenues sans reprise humaine. C'est la
   promesse même du produit ; si elle est basse, ContexFly est une inbox, pas un vendeur.
2. **Taux de conversion conversation → commande payée.**
3. **Délai inscription → première commande encaissée (activation).** Métrique critique compte
   tenu du fait que l'onboarding (Meta + KYC PawaPay) est la vraie barrière du projet. Si ce
   délai se compte en jours, le produit ne s'installera pas.
4. **Part des commerçants inscrits qui connectent effectivement leur numéro Meta.** Chez Fiitsa,
   il est possible d'utiliser le produit sans jamais brancher WhatsApp — c'est le point de fuite
   à surveiller.
5. **Temps de réponse médian de l'agent** (contrainte de connectivité locale).

## Contraintes connues

- **Techniques (déjà actées par Maxime, à challenger) :** API officielle WhatsApp Business de Meta
  (Cloud API), pas de connexion non officielle par QR code / WhatsApp Web.
- **Marché :** connectivité parfois limitée, Mobile Money (Orange Money, MTN MoMo) plutôt que
  carte bancaire, sensibilité forte au coût, usage mobile-first, bilinguisme FR/EN.
- **Coût Meta répercuté :** modèle par message délivré depuis le 01/07/2025. Le Cameroun relève
  de la zone tarifaire « Rest of Africa ». Le taux exact reste à relever sur la grille officielle
  → `Questions-Ouvertes.md`.
- **Plafond d'envoi initial :** un nouveau portefeuille Meta démarre à **250 destinataires uniques
  par 24 h**. La vérification d'entreprise (documents légaux) n'est **pas** requise pour envoyer :
  elle est l'un des trois chemins pour passer à 2 000, le troisième étant 2 000 templates de
  qualité délivrés en 30 jours. Conséquence directe : une boutique informelle **peut** démarrer.
- **Portée exacte du plafond (vérifié le 2026-08-15, doc Meta) :** le plafond ne compte que les
  messages envoyés **hors fenêtre de service client**. Les réponses aux conversations initiées par
  le client **n'y comptent pas**. Donc le volet A (prise de commande entrante) n'est pas plafonné ;
  seul le volet B (fidélisation/réengagement sortant) l'est.
- **Le plafond est au niveau du portefeuille Meta, pas du numéro** — partagé par tous les numéros
  d'un même portefeuille (changement du 07/10/2025). Un numéro peut consommer tout le quota des
  autres. Argument décisif contre la mutualisation de numéros sous le portefeuille de ContexFly.
- **Coexistence (à confirmer pour le Cameroun) :** Meta permet qu'un même numéro soit actif
  simultanément sur l'app WhatsApp Business et sur la Cloud API, avec synchronisation de
  l'historique des 6 derniers mois et miroir temps réel des messages. Supprime le principal
  blocage d'onboarding (« si je passe à l'API je perds mon app et mes conversations »). Limites
  connues : pas de groupes ; messages éphémères, vue unique et localisation en direct désactivés
  en 1:1. → Q8 dans `Questions-Ouvertes.md`.
- **Statut Meta visé : Tech Provider + Embedded Signup.** Le client onboardé possède ses actifs
  WhatsApp et **ajoute son propre moyen de paiement sur son propre WABA** — les coûts de messages
  Meta sont donc facturés au client, pas à ContexFly. Enlève un risque de trésorerie majeur.
  Au-delà de 200 nouveaux clients par semaine, il faut passer Meta Business Partner.
- **🔴 Conformité Meta — l'agent doit rester verrouillé sur sa mission métier.** Meta interdit les
  chatbots IA **généralistes** sur la WhatsApp Business Platform : appliqué depuis le 15/10/2025
  pour les nouveaux comptes API, étendu à tous au 15/01/2026. Les agents au service d'un processus
  métier (vente, prise de commande, support, rendez-vous) sont explicitement autorisés et
  encouragés. *(Source : document de recherche de Maxime, vérifié par Felix le 2026-08-16.)*
- **Plafond de fréquence marketing :** environ **2 messages marketing par utilisateur final et par
  jour, tous expéditeurs confondus**, appliqué au niveau de l'utilisateur et non de l'entreprise.
  Erreur `131049` quand le plafond est atteint. La délivrance d'une campagne ne peut donc jamais
  être garantie. *(Vérifié.)*
- **Architecture retenue — application ↔ n8n.** L'application est le point d'entrée et de sortie ;
  **n8n est l'orchestrateur du raisonnement métier**, avec plusieurs workflows coexistants.
  Décision structurante : **l'application est le seul composant qui parle à l'API WhatsApp.** n8n
  lui envoie une requête indiquant le type de message et ses arguments, et ne manipule jamais les
  identifiants WhatsApp. Trois raisons : ne pas exposer les jetons de chaque client aux workflows
  et aux logs n8n, garder une boîte de réception cohérente puisque tout message passe par le même
  point, et appliquer les règles WhatsApp (fenêtre de 24 h, catégories de templates, plafonds) en
  un seul endroit. *(Source : document de recherche de Maxime, §3. À reprendre au skill
  `architecture-integrations`.)*
- **🔴 Contrainte juridique — ne jamais détenir les fonds.** Rester intermédiaire technique
  connecté à des agrégateurs déjà agréés évite d'avoir besoin d'un agrément EME ou établissement
  de paiement (BEAC, BCEAO, CBN selon la zone). ⚠️ **Cette contrainte est en tension avec la
  décision Q16 (option B) — voir Q23, bloquante.**
- **Protection des données :** loi camerounaise **n°2024/017**, applicable au 23 juin 2026 —
  **donc déjà en vigueur** — et à portée **extraterritoriale** : elle s'applique dès qu'une donnée
  de citoyen camerounais est traitée, quel que soit le lieu d'immatriculation de l'entreprise. La
  politique de confidentialité et le recueil du consentement sont à concevoir comme un **module
  déclinable par pays**, faute de cadre africain unifié. → `Exigences-Non-Fonctionnelles.md`.
- **Développement :** Maxime seul, codage délégué à un agent IA, base de départ `ai-builder-saas`
  (TanStack Start, Convex, Better Auth, Zod, shadcn/ui, Tailwind, Paraglide JS).
- **Délai visé : 3 à 4 semaines** jusqu'à une première version en main d'un vrai commerçant
  (confirmé par Maxime le 2026-08-16, après une hésitation à une semaine — l'estimation à une
  semaine ne permettait pas de tenir A1 et B0, tous deux à effort L, avec le module de paiement).
  (développement intégralement délégué à Claude Code).
  ⚠️ **Le facteur limitant n'est pas la vitesse de développement, ce sont deux validations de
  tiers qui ont leur propre calendrier et qui ne s'accélèrent pas :**
  1. **Meta — statut Tech Provider + Embedded Signup.** Création de l'app Meta, App Review pour
     les permissions `whatsapp_business_management` et `whatsapp_business_messaging`, et
     vérification d'entreprise de ContexFly lui-même. Se compte en semaines et peut être rejeté.
     S'y ajoute l'approbation du nom d'affichage pour chaque commerçant onboardé.
  2. **Notch Pay — contrat Sync sous-marchands.** Une offre marketplace se négocie
     commercialement, ce n'est pas une inscription en libre-service ; le KYB de ContexFly en tant
     que plateforme est un préalable.
  **Conséquence opérationnelle : ces deux démarches doivent être lancées maintenant, en parallèle
  du développement, pas à la fin.** Sinon le code sera prêt et le produit ne pourra pas tourner.
- **Contrainte de périmètre induite :** 3-4 semaines imposent un MVP sévère. Les candidats
  naturels à la coupe sont le moteur de fidélisation, le volet campagnes sortantes et les
  permissions fines multi-utilisateur — à arbitrer au skill `analyse-approfondie` / `MVP.md`, pas
  ici.

## Périmètre

*(première esquisse — sera figée au Temps 2)*

### Dedans (scope IN)
- Agent IA conversationnel qui prend la commande sur WhatsApp (entrant).
- Panier construit au fil de la conversation + page récapitulative éditable avant paiement.
- Encaissement Mobile Money et confirmation automatique par message WhatsApp.
- Inbox de supervision avec bascule IA ↔ humain par contact.
- Cycle de vie des conversations + historique servant de contexte à l'agent.
- Relance automatique des conversations actives non abouties.
- **Fidélisation pilotée par la donnée d'achat** : ciblage par habitude d'achat, remise
  automatique proposée en conversation au-delà d'un seuil de commandes, automatisations
  activables par l'entreprise cliente.
- **Onboarding : le client apporte son propre numéro**, via Embedded Signup, avec tutoriel vidéo
  intégré.
- **Encaissement par ContexFly** (option B) via **Notch Pay Sync** : collecte, comptes
  sous-marchands, reversement au commerçant. Cinq politiques de paiement au choix du commerçant,
  dont l'**acompte** (pourcentage réglable par produit, libellé personnalisable).
- **Back-office administrateur ContexFly** : instruction du KYC des commerçants, supervision des
  reversements, litiges et remboursements.
- **Export des données de livraison** — fiche à remettre au livreur : coordonnées du client,
  adresse de livraison, contenu de la commande, montant restant dû. ✅ *Décision Maxime
  (2026-08-15).*
- **Statut de commande** minimal (à livrer / livrée / annulée) — nécessaire pour boucler
  l'encaissement en paiement à la livraison et en acompte.

### Dehors pour l'instant (scope OUT)
- ✅ **Démarchage à froid vers des listes non opt-in** (raison : violation de la politique Meta,
  bannissement algorithmique du numéro du client, risque de réputation pour ContexFly).
  *Recadrage accepté par Maxime le 2026-08-15.*
- **Pool de numéros mutualisés sous le portefeuille Meta de ContexFly** (raison : le plafond
  d'envoi est partagé au niveau du portefeuille ; le numéro est le fonds de commerce du client ;
  responsabilité d'émission portée par ContexFly). *Position de Felix, confirmation attendue —
  seule exception envisagée : un numéro de démo pour essai, sur un portefeuille dédié.*
- Helpdesk multi-canal complet à la Chatwoot (raison : effort disproportionné, hors du job cœur).
- **Gestion des livreurs et suivi de livraison** (raison : décision Maxime du 2026-08-15 — on
  s'arrête à l'export des données à remettre au livreur. Fiitsa a un module Logistique entier ;
  ContexFly ne le suit pas sur ce terrain).
- **Prise de rendez-vous / réservations** (raison : verticale produits physiques à catalogue,
  pas services).
- **Système de facturation intégré** — facture adaptable par entreprise, templates, import de
  modèle (raison : piste explorée puis abandonnée par Maxime avant l'analyse ; confirmée).
- **Connexion non officielle WhatsApp (QR code / Baileys)**, même en offre d'entrée de gamme
  (raison : diluerait l'avantage de conformité, qui est l'axe de différenciation retenu).
- Design/UI et code (raison : hors périmètre de Felix).

### À trancher
→ voir `Questions-Ouvertes.md`.
