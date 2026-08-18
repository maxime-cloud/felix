# Décisions — ContexFly

Registre des décisions structurantes prises pendant l'analyse (produit, business, technique),
pour ne jamais re-débattre un sujet déjà tranché sans une bonne raison de le rouvrir.

## 2026-08-15 — cadrage (Temps 1)

- **Décision :** Le projet est créé sous le slug `contexfly`, `Projects/_current.md` mis à jour.
- **Raison :** Nouvelle idée sans rapport avec un projet existant (aucun projet actif).
- *Prise à l'initiative de Felix (procédure standard de bootstrap).*

- **Décision :** Les cinq choix apportés par Maxime (API officielle Meta, inbox intégrée, cycle de
  vie des conversations, relance automatique, quatre politiques de paiement) sont enregistrés
  comme **propositions à valider**, pas comme acquis — conformément à sa demande explicite.
- **Raison :** Demande de Maxime au démarrage : « remets-les en question si tu vois un problème,
  ne les valide pas par défaut ».

- **Décision (position de Felix, en attente de confirmation) :** Le choix de l'**API officielle
  WhatsApp Business de Meta** plutôt qu'une connexion non officielle est validé.
- **Raison :** Trois arguments factuels, pas de préférence. (1) L'automatisation via WhatsApp Web
  non officiel viole les conditions d'utilisation et le bannissement du numéro est le mode
  d'échec normal, pas le cas rare — inacceptable quand le numéro est le point de vente du client.
  (2) Les types de messages riches (boutons, listes, CTA, catalogue) ne sont accessibles que par
  l'API officielle et sont fonctionnellement structurants pour un agent de prise de commande.
  (3) La friction d'onboarding redoutée est plus faible qu'attendu : la vérification d'entreprise
  Meta n'est **pas** requise pour envoyer, un nouveau portefeuille démarre à 250 destinataires
  uniques / 24 h, ce qui suffit très largement à une PME camerounaise pour démarrer.
- *Prise à l'initiative de Felix. Confirmation demandée à Maxime.*

- **Décision ✅ ACCEPTÉE par Maxime :** Recadrer le volet « démarchage
  commercial / envoi en masse » en **réengagement d'une base de contacts opt-in** (clients ayant
  déjà écrit ou commandé), et exclure explicitement l'envoi vers des listes froides.
- **Raison :** Le démarchage à froid viole la politique Meta (opt-in explicite et spécifique au
  canal exigé) ; la sanction est algorithmique (chute du quality rating sur le taux de blocage,
  réduction des limites, bannissement) et frappe le numéro du client — donc le support et le
  churn de ContexFly. Par ailleurs le template marketing est facturé par message délivré sans
  palier dégressif : la version froide est aussi la plus coûteuse et la moins convertissante.
- *Proposée à l'initiative de Felix, validée par Maxime le 2026-08-15 (réponse Q2).*

## 2026-08-15 — cadrage (Temps 1, suite — réponses de Maxime)

- **Décision (Maxime) :** Verticale primaire = **vente de produits physiques à catalogue**
  (boutiques, cosmétique, prêt-à-porter, distribution). Restauration/livraison et services sur
  rendez-vous ne sont pas la cible primaire.
- **Raison :** Réponse directe de Maxime à la question Q1. Cohérent avec la mécanique déjà décrite
  (panier, quantités, page récapitulative).

- **Décision (Maxime) :** Le volet sortant devient un **moteur de fidélisation piloté par la
  donnée d'achat** (ciblage par habitude d'achat, remise automatique proposée en conversation
  au-delà d'un seuil de commandes, automatisations configurables par l'entreprise cliente).
- **Raison :** Extension apportée par Maxime. Felix la retient comme le candidat le plus sérieux
  au rôle de différenciateur produit : la règle « a commandé 3 fois » n'est déclenchable que
  parce que ContexFly produit lui-même la donnée de commande — un outil de campagne générique
  ne l'a pas. Deux réserves posées (voir `Idee.md` et Q6bis/Q9).

- **Décision (Maxime) :** L'**entreprise cliente apporte son propre numéro WhatsApp**, avec un
  tutoriel vidéo intégré à l'application pour la configuration.
- **Raison :** Réponse directe de Maxime à la question Q3.

- **Décision (position de Felix, confirmation attendue) :** **Ne pas** proposer de pool de numéros
  pré-configurés appartenant à ContexFly. Exception unique envisageable : un numéro de démonstration
  pour l'essai, sur un portefeuille Meta séparé, avec migration vers le numéro du client à la
  conversion.
- **Raison :** Quatre arguments, par ordre de poids. (1) **Décisif** — depuis le 07/10/2025, le
  plafond d'envoi Meta est calculé **au niveau du portefeuille** et partagé par tous les numéros
  qu'il contient : mutualiser les numéros des clients sous le portefeuille de ContexFly leur
  ferait partager un unique quota de destinataires uniques / 24 h, qu'un seul client peut épuiser.
  (2) Le numéro est le fonds de commerce du commerçant (devanture, flyers, page Facebook,
  répertoire de ses clients) — lui en donner un neuf lui demande de refaire son audience à zéro et
  crée un lock-in par contrainte, pas par valeur. (3) Si le numéro appartient à ContexFly, ContexFly
  est l'émetteur des messages et porte les signalements en cas d'abus d'un de ses clients.
  (4) Coût et exploitation d'un vrai numéro par client.
- **Alternative recommandée à la place :** Embedded Signup (statut Tech Provider) pour supprimer la
  friction sans mutualiser, et **Coexistence** pour que le client garde son app WhatsApp Business
  et son historique sur le même numéro.
- *Prise à l'initiative de Felix, à la demande explicite de Maxime (« apporte un avis critique »).*

## 2026-08-15 — après exploration du produit Fiitsa

- **Décision (Maxime) :** Pas de pool de numéros pré-configurés. Le client apporte toujours son
  propre numéro. *(Réponse Q3bis.)*

- **Décision (Maxime) — STRUCTURANTE : ContexFly entre dans le flux d'argent (option B de Q16).**
  ContexFly encaisse les paiements des clients finaux et reverse au commerçant, comme Fiitsa,
  plutôt que de faire brancher au commerçant son propre compte marchand.
- **Raison (Maxime) :** Notch Pay gère à la fois le *payin* et le *payout*, ce qui couvre
  techniquement le besoin.
- **Réserve posée par Felix, non bloquante :** la capacité technique de Notch Pay ne dit rien du
  cadre **contractuel**. Encaisser pour le compte de commerçants tiers relève de l'agrégation de
  sous-marchands, que beaucoup d'agrégateurs conditionnent à une convention *marketplace*
  spécifique, avec la question de savoir qui est marchand de référence. À vérifier dans les CGU de
  Notch Pay, pas dans la documentation d'API. → Q18.
- **Conséquences en aval à traiter :** KYC des commerçants par ContexFly, gestion de la trésorerie
  de tiers, litiges et remboursements, calendrier de reversement. Et la recommandation tarifaire
  issue du benchmark change de statut → voir `Changelog.md`.

- **Décision (Maxime) :** Ajout d'une **cinquième politique de paiement — l'acompte** : versement
  partiel qui confirme la commande, le solde payé à la livraison. *(Réponse Q17.)*
- **Raison :** Mode observé chez Fiitsa, le mieux adapté au terrain — il règle le problème de
  confiance du paiement à la livraison sans imposer le prépaiement intégral. Le pourcentage doit
  être réglable par produit, et le libellé affiché au client final personnalisable.

- **Fait vérifié (non une décision) :** Fiitsa utilise **PawaPay** pour le mobile money et
  **Stripe** pour les cartes.

- **⛔ DÉCISION ANNULÉE le 2026-08-15 — voir la décision suivante. Conservée pour la traçabilité.**
  ~~**Décision (Felix, à la demande de Maxime — arbitrage délégué) : PawaPay**, pas Notch Pay.~~
- **Raison, par ordre de poids :**
  1. **Le critère qui tranche — le cadre contractuel sous-marchands existe et il est écrit.** Les
     conditions marchands de PawaPay contiennent un **Schedule 2 « Intermediary Merchants »**,
     explicitement prévu pour « les marchands qui onboardent des sous-marchands sur leur
     plateforme, telles que les plateformes e-commerce ». C'est exactement l'option B. Chez Notch
     Pay, la page tarifs ne documente **aucune** condition marketplace ou sous-marchands — ce qui
     ne veut pas dire que c'est interdit, mais qu'il faudrait négocier un cadre qui n'existe pas
     sur étagère, avec le risque de découvrir la contrainte après le lancement.
  2. **Aucun avantage de prix à Notch Pay sur le flux cœur.** Les deux facturent **1 % sur
     l'encaissement mobile money et 1 % sur le reversement**, sans frais d'installation ni frais
     mensuels. Le choix ne se joue donc pas sur le coût. (PawaPay ajoute les frais de l'opérateur ;
     à confirmer côté Notch Pay.)
  3. **Un seul contrat couvre 19 marchés africains** et tous les opérateurs. L'expansion
     « Cameroun puis Afrique francophone » inscrite au cadrage ne demandera pas de renégocier
     pays par pays. PawaPay revendique 85 % des transactions mobile money sur ces marchés.
  4. **Le risque d'exécution est déjà levé par un tiers :** Fiitsa fait tourner exactement ce cas
     d'usage sur PawaPay, en production, au Cameroun. Et Maxime connaît déjà l'acteur.
- **Ce que ce choix coûte, et qu'il faut assumer :** Notch Pay est **camerounais** — support local,
  relation commerciale de proximité, interlocuteur joignable, et probablement plus de souplesse
  pour négocier un arrangement sur mesure. PawaPay est une entité étrangère, contrat en anglais,
  et le support du plan Standard passe par un serveur Discord communautaire. Pour un développeur
  seul à Douala, ce n'est pas rien. **Si le point de blocage ci-dessous ne se règle pas avec
  PawaPay, Notch Pay redevient le bon choix** — d'où la nécessité de trancher Q21 avant de coder.

- **⚠️ Point de blocage découvert en tranchant, et il touche au cœur du projet :** le Schedule 2 de
  PawaPay impose à la plateforme de **vérifier l'identité de chaque sous-marchand** et de collecter
  « certificat d'incorporation, statuts, documentation d'identification des directeurs », de
  transmettre ces pièces à PawaPay **sous une semaine**, et de fournir un **reporting mensuel** de
  ses sous-marchands.
  **Conséquence :** l'option B ne supprime pas le problème du commerçant sans RCCM — **elle le
  déplace sur ContexFly**. Or c'était la raison principale de choisir l'option B. À vérifier
  directement auprès de PawaPay : existe-t-il un régime allégé pour les micro-marchands ou les
  entrepreneurs individuels (pièce d'identité seule) ? → **Q21, à traiter avant tout
  développement.**
  *Observation qui rend la question encore plus intéressante : l'onboarding de Fiitsa ne demande
  qu'un nom de business, une description et un numéro de téléphone. Soit ils collectent ces pièces
  plus tard, soit ils ont un contrat sur mesure, soit ils ne respectent pas ce Schedule 2.*

- **✅ DÉCISION RETENUE (Maxime, 2026-08-15) : Notch Pay**, via son offre **Notch Pay Sync**.
- **Raison (Maxime) :** Notch Pay Sync est une offre marketplace dédiée aux sous-marchands, et
  Notch Pay pratique le **KYC** (vérification d'une personne physique) là où PawaPay n'accepte que
  le **KYB** (vérification d'une entreprise).
- **Pourquoi Felix se range à cet arbitrage :** il répond frontalement au point de blocage Q21, qui
  était le seul vrai défaut de la recommandation PawaPay. Si un sous-marchand peut être vérifié en
  tant que personne physique, **le commerçant informel sans RCCM peut être onboardé** — et c'est
  toute la raison d'être de l'option B. Le critère « cadre contractuel sous-marchands écrit », qui
  m'avait fait pencher pour PawaPay, est également satisfait : Notch Pay Sync est documenté comme
  solution de paiement pour marketplaces, avec **comptes sous-marchands, split payment et
  reversements de masse automatisés** (vérifié). S'y ajoutent les avantages déjà notés : entreprise
  camerounaise, support local, interlocuteur joignable, tarif identique (1 % encaissement,
  1 % reversement, sans frais fixes).
## 2026-08-17 — arbitrages produit

- **Décision (Maxime) :** Ne **pas** passer par Genuka WA comme fournisseur d'accès à l'API
  WhatsApp. ContexFly va directement au **statut Meta Tech Provider**.
- **Conséquence :** la validation Meta reste sur le chemin critique du délai de 3-4 semaines (Q22).
  À engager immédiatement.

- **Décision (Maxime) — STRUCTURANTE : un compte peut porter plusieurs activités, chacune avec son
  propre agent**, le nombre d'agents étant plafonné par le palier d'abonnement (G1).
- **Conséquences à traiter en priorité :** toutes les entités gagnent une clé d'activité
  (`donnees-et-roles`) ; le nombre d'agents devient un levier de prix (`tarification`) ; chaque
  activité a son propre numéro WhatsApp et donc son propre portefeuille Meta, sous peine de
  partager le plafond d'envoi.
- **Réserve de Felix :** modéliser le multi-activités dès maintenant, mais ne livrer qu'une seule
  activité par compte au MVP — l'ajout ultérieur est alors peu coûteux, l'inverse ne l'est pas.

- **Décision (Maxime) :** Ajout des **horaires de livraison** distincts des horaires d'ouverture
  (A13) et d'un **mode absence imprévue** avec consigne de réponse dictée à l'agent (A14).

- **Décision (Maxime, confirmée 2026-08-17) : une seule application Meta contenant plusieurs
  numéros.** La piste des applications Meta séparées par activité est abandonnée. Séparation des
  flux assurée par des endpoints de webhook distincts par WABA à l'intérieur de cette application.

- **Décision (Maxime) :** Les paliers et le prix de l'abonnement (D8) ne sont **pas** traités au
  skill `fonctionnalites`. Ils sont renvoyés à `tarification`, **après** la modélisation du coût
  d'inférence par conversation (Q13).
- **Raison :** chiffrer un palier avant de connaître le coût d'une conversation revient à deviner —
  et le benchmark montre que c'est précisément là que le modèle peut s'effondrer (Fiitsa facture
  100 FCFA par conversation et par jour, pour un marché qui accepte 9 900–20 000 FCFA/mois).

- **Décision (Maxime) :** L'**adresse de livraison est mémorisée par client** et proposée par
  défaut à la commande suivante. Conséquence de modélisation : l'adresse appartient au contact, pas
  à la commande — entité `adresse` avec plusieurs adresses possibles et une adresse par défaut.

- **Décision (Maxime) :** Le **mode absence imprévue s'active depuis WhatsApp**, sans ouvrir
  l'application (A14).
- **Réserve de Felix, non bloquante :** l'agent doit alors distinguer son propriétaire de ses
  clients sur le même numéro, et le numéro du gérant doit être vérifié — sinon une usurpation de
  numéro permet de fermer la boutique. Effort A14 révisé de S à M.

- **Décision (Maxime) — architecture Meta : une seule application, endpoints de webhook distincts
  par activité.** Maxime préférait des applications Meta développeur séparées par activité, pour
  éviter de recevoir les webhooks « des deux côtés ».
- **Ce que la vérification a établi (2026-08-17) :** une application Meta n'expose qu'une seule URL
  de rappel — c'est le modèle voulu, le tri se fait sur le `phone_number_id` des métadonnées. Et
  **chaque application exige sa propre App Review**, ce qui multiplierait les revues Meta et
  attaquerait directement la seule barrière défendable du projet (Q22). Le statut Tech Provider est
  conçu pour qu'une seule application onboarde de nombreux clients.
- **La solution qui satisfait le besoin sans le coût :** Meta permet des **« alternate webhook
  endpoints »**, c'est-à-dire une URL de webhook propre à un WABA ou à un numéro, à l'intérieur
  d'une seule application — la documentation cite explicitement le cas du partenaire qui veut un
  point de terminaison unique par client onboardé. **Séparation nette des flux, une seule App
  Review.** → à figer au skill `architecture-integrations`.

- **Décision (Maxime) :** **Stock par point de vente dès le MVP** (G2), en plus du stock par
  variante. Felix recommandait de l'exclure du MVP ; arbitrage non suivi.
- **Conséquences actées :** ligne de stock indexée `(produit, variante, point de vente)` ; branche
  de décision supplémentaire dans A1 (où est le stock, et que faire s'il est ailleurs) ; choix du
  point de décrément à la commande ; effort G2 révisé de M à **L**.
- **Garde-fou ajouté par Felix :** un point de vente doit pouvoir être déclaré **« stock non
  suivi »**, l'agent se rabattant alors sur une réponse prudente — sinon un stock mal tenu rend
  l'agent moins fiable qu'un agent sans stock, puisqu'il affirme au lieu de vérifier.

- **Décision (Maxime) — correction d'une erreur de Felix sur l'adresse de livraison (C4).** Le
  modèle retenu est **ville + quartier en listes déroulantes définies par le commerçant, plus un
  champ libre facultatif** pour le repère. Felix avait recommandé du texte libre seul.
- **Raison :** capture d'un site e-commerce camerounais à forte audience fournie par Maxime. Le
  modèle structuré rend le périmètre de livraison opposable, débloque les frais par zone (C5), et
  reste fidèle à l'usage local en gardant le repère parlé en complément.

## 2026-08-16 — intégration du document de recherche de Maxime

*(`ContexFly-decisions-produit.pdf`, antérieur à l'analyse avec Felix. Consigne de Maxime : en cas
de recoupement, ce qui a été décidé ensemble prime.)*

- **Décision (Maxime, antérieure, confirmée) :** ne **pas** construire de connexion non officielle
  (QR code / WhatsApp Web) en parallèle, même en offre d'entrée de gamme.
- **Raison :** cela diluerait l'avantage de conformité, qui est l'axe de différenciation retenu
  face à des concurrents dont beaucoup reposent sur des connexions non officielles. *(Cohérent
  avec le constat de Felix au benchmark : Vendeur.ci propose ouvertement du « QR Code (Baileys) ».)*

- **Décision (Maxime, antérieure, retenue) :** **aucun système de facturation intégré** au produit.
  La piste (facture adaptable par entreprise, activable, templates) a été explorée puis abandonnée.
  → à porter en scope OUT.

- **Décision (Maxime, antérieure, retenue — structurante) : architecture application ↔ n8n.**
  L'application est le point d'entrée et de sortie, n8n l'orchestrateur du raisonnement métier, et
  **l'application est le seul composant qui parle à l'API WhatsApp**. Détail et justification
  reportés dans `Idee.md`, à reprendre au skill `architecture-integrations`.

- **Fait vérifié par Felix (2026-08-16), issu du document :** Meta interdit les chatbots IA
  généralistes sur la WhatsApp Business Platform (15/10/2025 pour les nouveaux comptes API,
  15/01/2026 pour tous) et autorise explicitement les agents scopés à un processus métier.
  → nouvelle fonctionnalité **A12** (garde-fou de conformité) et argument de positionnement.

- **Fait vérifié par Felix (2026-08-16), issu du document :** plafond d'environ 2 messages
  marketing par utilisateur final et par jour, tous expéditeurs confondus, erreur `131049`.
  → contrainte à intégrer au domaine F (Q25).

- **⚠️ Contradiction relevée, non tranchée :** le document pose « ne jamais détenir les fonds »
  (§4.3) alors que la décision Q16 prise avec Felix retient que ContexFly encaisse et reverse.
  → **Q23, bloquante, à trancher avant tout développement du module de paiement.**

- **Décision (Maxime, 2026-08-16) :** nouvelle fonctionnalité **B0 — enregistrement de produit
  assisté par agent, avec mémoire de champs apprise par catégorie et par commerçant**.
- **Raison :** idée originale de Maxime, sans équivalent identifié au benchmark. Felix la retient
  comme candidate sérieuse au rôle de différenciateur principal : elle abaisse la marche du
  catalogue vide (mortalité n°1 de ce type de produit), elle crée le seul effet d'accumulation que
  `Positionnement.md` identifie comme grandissant avec le temps, et surtout **elle est ce qui rend
  l'agent vendeur réellement autonome** — un agent alimenté par un catalogue nom/prix/photo doit
  escalader dès qu'un client demande une pointure ou une couleur.

- **Décisions (Maxime, 2026-08-16) sur le domaine A :** A6 validée avec retour à l'IA
  **automatique et délai configurable** ; A8 validée avec **deux relances, à 3 h et à 48 h**.

- **Ce qui reste à confirmer au moment de contractualiser** (non bloquant pour le cadrage, mais à
  ne pas découvrir en production) : la nature exacte des pièces exigées pour un sous-marchand
  personne physique, le plafond de volume éventuel associé à ce régime, le délai de reversement,
  et qui porte la responsabilité en cas de litige. → Q21 reformulée.

## 2026-08-17 — clôture du skill `fonctionnalites`

- **Décision (Maxime) :** validation en bloc de l'ensemble des domaines A à J, de la passe
  proactive P1-P4, et du domaine L. Aucune fonctionnalité rejetée à ce stade.
- **Décision (Maxime) :** ajout du **domaine L — parrainage et réductions au niveau de la
  plateforme ContexFly** (liens de parrainage rémunérés en pourcentage ou montant fixe, liens et
  codes de réduction sur l'abonnement).
- **Apports proactifs de Felix sur ce domaine, validés d'office sur consigne de Maxime :**
  attribution serveur-à-serveur plutôt que par cookie (les liens circulent dans WhatsApp, où les
  cookies sont peu fiables) ; anti-fraude et clawback sans lesquels le programme est une fuite de
  trésorerie ; versement en Mobile Money à seuil bas ; portail parrain mobile-first ; et surtout
  **déclenchement de la commission sur la première commande encaissée du filleul plutôt que sur son
  inscription**, pour aligner le parrain sur l'activation réelle.
- **Lecture stratégique retenue :** L1 permet de **recruter les agences camerounaises comme
  parrains** plutôt que de les affronter — le benchmark les avait identifiées comme le concurrent
  n°2, celui qui prendra les 50 premiers clients.

## 2026-08-17 — architecture de l'agent

- **Décision (Maxime) : n8n est abandonné pour ce projet.** L'agent est implémenté **dans le
  code**. Une utilité pourra lui être retrouvée plus tard, mais il ne fait pas partie du projet.
- **Raison (Maxime) :** l'architecture envisagée était un workflow unique pour tous les clients,
  récupérant le prompt de l'agent configuré et appelant des liens de la plateforme pour lire les
  conversations et le stock, créer les commandes… En détaillant ces interactions, il est apparu que
  **les seuls nœuds réellement utilisés seraient l'agent et les requêtes HTTP** — n8n n'apportait
  plus qu'un saut réseau.
- **Ce que ça annule :** la décision d'architecture `application ↔ n8n` du document de recherche
  antérieur. La partie « l'application est le seul composant qui parle à l'API WhatsApp » **reste
  valide** et devient triviale, puisqu'il n'y a plus qu'un composant.
- *Analyse technique complète dans `Reference-Technique-Agent.md`, à reprendre au skill
  `architecture-integrations`.*

- **Composants retenus (vérifiés dans la documentation officielle) :**
  - **`@convex-dev/agent`** — contexte d'agent typé (la réponse au multi-activités de G1),
    `needsApproval` statique ou dynamique (couvre nativement **D5** et **P1**), définition des
    outils à plusieurs niveaux avec hiérarchie (mécanique d'**A4** et **A12**), gestion des fils et
    de l'historique (**A7**).
  - **`@convex-dev/workflow`** — `step.sleep`, `runAt`, reprises, `awaitEvent`. Durable, survit aux
    redémarrages. Couvre **A8, D1, D7, P3, F4, H5**.
  - **`@convex-dev/workpool`** — non envisagé par Maxime, mais **nécessaire** : limitation du débit
    des envois sortants pour respecter les trois plafonds Meta simultanés. Sans lui, une campagne
    F4 de 500 contacts brûle le quota et dégrade la note de qualité du numéro du commerçant.

- **Correction apportée au document de recherche antérieur :** A8 y était décrit comme un scan des
  conversations actives toutes les ~1 minute. Avec `step.sleep`, **il n'y a plus de scan** — chaque
  conversation programme sa propre échéance. Moins de charge, pas de dérive, comportement exact.

- **Principe de sécurité retenu : le modèle ne choisit jamais le périmètre, seulement l'intention.**
  Quatre couches : (1) l'identifiant d'activité est injecté dans le contexte de l'outil et n'est
  **jamais** un argument acceptable — l'interlocuteur étant un client final inconnu sur WhatsApp,
  une injection de prompt suffirait sinon à franchir la frontière entre commerçants ; les fonctions
  appelées sont des `internalQuery`/`internalMutation`, jamais publiques. (2) Un outil est une
  action métier étroite, jamais un accès base générique. (3) Tout invariant d'argent est
  **recalculé côté serveur** au moment de l'écriture, jamais repris du dialogue — `needsApproval`
  s'ajoute mais ne remplace pas. (4) Le jeu d'outils transmis à l'agent découle de la configuration
  du commerçant (A4/A5/A12) : ce qui est désactivé n'existe pas dans son contexte.
