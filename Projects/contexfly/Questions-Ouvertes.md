# Questions Ouvertes — ContexFly

(chaque question reste ici jusqu'à résolution — cochée = tranchée, avec la décision notée)

## Résolues

- [x] **Q1 — Verticale précise.**
  Décision (Maxime, 2026-08-15) : **produits physiques à catalogue** (boutiques, cosmétique,
  prêt-à-porter, distribution). Pas la restauration/livraison, pas les services sur rendez-vous.

- [x] **Q2 — Poids et nature du volet sortant.**
  Décision (Maxime, 2026-08-15) : recadrage accepté. Le sortant devient un **moteur de
  fidélisation piloté par la donnée d'achat** (ciblage par habitude, remise automatique en
  conversation au-delà d'un seuil de commandes, automatisations configurables). Démarchage à
  froid vers listes non opt-in = scope OUT définitif.

- [x] **Q3 — Propriété du numéro WhatsApp.**
  Décision (Maxime, 2026-08-15) : **le client apporte son propre numéro**, avec tutoriel vidéo
  intégré. Le pool de numéros pré-configurés reste indécis → voir Q3bis.

## Issues de `saas-essentiels` (2026-08-19)

- [x] **Q37 — Import d'une base clients existante.** ✅ **Retenu (Maxime, 2026-08-19).**
  → fonctionnalité **B5**, import de contacts clients. ⚠️ Contrainte forte : un contact importé
  **n'a pas d'opt-in WhatsApp** — il entre en base pour la mémoire client et l'historique, mais
  **ne peut recevoir aucune campagne** tant qu'il n'a pas écrit lui-même (R18, F5). Sans cette
  barrière, l'import devient une porte d'entrée vers le démarchage à froid qu'on a écarté au
  cadrage, et il fait bannir le numéro du commerçant.

- [x] **Q38 — Mode dégradé.** ✅ **Retenu (Maxime, 2026-08-19) : faire comme Ngavix** — application
  installable en **PWA**, consultable **hors connexion**.
  *(Lecture de Felix de la consigne « fais la même chose ». Si tu voulais dire autre chose,
  corrige — c'est une addition de périmètre non triviale.)*
  → fonctionnalité **K1**. Périmètre volontairement borné : **consultation hors ligne** (catalogue,
  commandes du jour, fiches clients, fiche livreur) et **saisie mise en file** pour les actions
  simples. ❌ **Pas de conversation hors ligne** — un agent qui répond suppose le réseau, et une
  réponse différée de deux heures est pire que pas de réponse.

- [x] **Q39 — CGU, CGV, politique de confidentialité.** ✅ **Rédigées (2026-08-19)** →
  `_documents-juridiques.md`. ⚠️ **Brouillons de travail, à faire relire par un juriste** avant
  publication : ContexFly intervient dans un flux de paiement et traite les données de clients de
  ses clients, ce qui engage une responsabilité réelle.

- [ ] **Q40 — Restauration : qui, et à quelle granularité ?** R29 (aucune suppression réelle)
  couvre le cas courant — il n'y a rien à restaurer. Reste la corruption de données ou l'erreur de
  masse. Qui peut restaurer, et jusqu'à quel niveau de finesse ?
  Décision : ...

## Ouvertes — bloquantes ou structurantes

- [ ] **🔴 Q29 — RÉOUVERTURE DE Q23 : qui détient juridiquement les fonds chez Notch Pay ?**
  Q23 avait été close le 16/08 sur la base « l'argent est stocké chez eux, donc on passe ». **La
  vérification documentaire du 19/08 ne confirme pas cette hypothèse — elle la contredit
  plutôt.** Rien dans la documentation Notch Pay, la page produit Sync, le contrat marchand ni le
  contrat partenaire n'énonce qui est titulaire du solde avant reversement. Et trois indices
  convergent vers un **transit par un solde plateforme** : `GET /balance` renvoie le solde du compte
  authentifié, les transferts exigent « sufficient funds in **your** Notch Pay account », et le
  split déduit l'`application_fee` **puis** transfère le reste.
  ⚠️ **Si confirmé, ContexFly détient les fonds au sens économique — R3 est violée et un agrément
  EME/établissement de paiement BEAC devient nécessaire.**
  **À obtenir par écrit de Notch Pay avant toute ligne de code d'encaissement.**
  *Atténuation immédiate, sans attendre la réponse :* modéliser le solde commerçant comme un
  **registre d'écritures append-only**, jamais comme un champ `solde` — cette structure survit aux
  deux montages possibles.
  Décision : ...

- [ ] **🔴 Q30 — Notch Pay Sync n'est pas en libre-service et n'est pas dans l'OpenAPI.**
  « Contact our sales team to enable Sync » + vérifications de conformité. Et `/accounts`, `/sync`,
  `/refunds` sont **absents de la spécification OpenAPI officielle**.
  **Conséquence de planning : deuxième dépendance externe bloquante, à côté de la validation Meta
  (Q22).** Aucun code d'encaissement n'est testable avant accord commercial signé.
  **À engager immédiatement, en parallèle du développement.**
  Décision : ...

- [ ] **Q31 — Type de compte connecté : Standard, Express ou Custom ?**
  Standard (dashboard direct, payouts par le titulaire) · Express (onboarding 2-3 min, dashboard
  limité, payouts par la plateforme) · Custom (invisible, marque blanche, tout géré par ContexFly).
  **Choix structurant et quasi irréversible.** Custom donne la meilleure expérience mais concentre
  toute la charge KYC et support sur ContexFly. *Position de Felix : Express, sauf si Notch Pay
  démontre que Custom n'alourdit pas les obligations.*
  Décision : ...

- [ ] **Q32 — Les plafonds Cameroun s'appliquent à qui ?** 500 000 XAF/jour et 5 000 000 XAF/mois,
  rattachés au régulateur BEAC dans la doc. Client final, commerçant, ou **compte plateforme** ?
  **Si c'est au compte plateforme, c'est un plafond de croissance dur pour ContexFly.**
  Décision : ...

- [ ] **Q33 — Pas de clé d'idempotence sur `POST /payments`.** Risque de **double débit du client
  final** si un appel expire côté réseau et qu'on le rejoue. Le `reference` personnalisé offre
  peut-être une déduplication implicite, mais **ce n'est pas documenté**. À valider en bac à sable
  **avant de coder le moindre réessai automatique sur un POST**.
  Décision : ...

- [ ] **Q34 — Le remboursement mobile money est-il automatisable ?** Non confirmé. **Si MoMo n'est
  pas remboursable par API, D7 devient un processus manuel** — écran d'administration et procédure
  opérationnelle, pas une fonctionnalité.
  Décision : ...

- [x] **Q35 — Frais Notch Pay.** **Tranché (Maxime, 2026-08-19) : 2 % à l'encaissement + 1 % au
  reversement = 3 % au total.** Maxime a une connaissance directe du fonctionnement de Notch Pay.
  **Obligation produit associée :** les 3 % sont **visibles du commerçant** dans le produit et
  expliqués dans la documentation de la plateforme (règle R7bis).
  *(La page tarifs publique affiche 1 % + 1 % — divergence signalée, non arbitrée.)*

- [ ] **Q36 — Friction KYC sous-estimée.** Le compte connecté personne physique exige pièce
  d'identité **+ selfie + justificatif de domicile**. Le justificatif de domicile est une friction
  réelle pour un commerçant informel camerounais, sur un parcours mobile. **À intégrer au parcours
  H5 et à confirmer avec Notch Pay** (obligatoire ou non).
  Décision : ...


- [x] **Q3bis — Numéros pré-configurés fournis par ContexFly.**
  Décision (Maxime, 2026-08-15) : **abandonnés**. Le client apporte toujours son propre numéro.
  Raison retenue : plafond d'envoi Meta partagé au niveau du portefeuille depuis le 07/10/2025 ;
  le numéro est le fonds de commerce du client ; responsabilité d'émission portée par ContexFly.
  *(Le numéro de démo pour essai n'est pas retenu non plus à ce stade — à rouvrir seulement si
  l'onboarding s'avère bloquant en conditions réelles.)*

- [x] **Q6bis — Forme du moteur de fidélisation.** **Tranché : automatisations pré-écrites** — F3
  est Must et validée, F6 (constructeur générique) est Could avec « jamais avant F3 ».
  *(Cochée le 19/08.)*

<!-- **Q6bis — Forme du moteur de fidélisation.** Automatisations pré-écrites activables en un
  clic avec 2-3 paramètres (position de Felix) vs constructeur de règles générique « tout
  configurable » (demande de Maxime). Argument : un gérant de boutique ne configurera pas un
  moteur de segmentation ; l'écran vide d'un rule builder reste vide. À trancher au skill
  `fonctionnalites`. -->

- [ ] **Q9 — Plafond de remise contraint dans le code.** L'agent IA propose des réductions : le
  plafond doit être appliqué côté serveur, jamais confié au prompt. Définir la règle exacte
  (plafond absolu, plafond par palier de fidélité, produits exclus). → à inscrire dans
  `Exigences-Non-Fonctionnelles.md`.
  Décision : ...

## Issues du benchmark — bloquantes, par ordre de conséquence

- [x] **Q16 — ContexFly entre-t-il dans le flux d'argent ?**
  Décision (Maxime, 2026-08-15) : **oui — option B.** ContexFly encaisse et reverse, via Notch Pay
  (payin + payout). Conséquences ouvertes → Q18, Q19, et réouverture du modèle tarifaire.

- [ ] **Q18 — CGU de Notch Pay sur l'agrégation de sous-marchands.** Encaisser pour le compte de
  commerçants tiers est un usage *marketplace*, souvent conditionné à une convention spécifique.
  Qui est marchand de référence ? Un compte unique ContexFly avec sous-comptes est-il autorisé ?
  *Se lit dans les CGU et se confirme par un échange commercial, pas dans la doc d'API.*
  Décision : ...

- [ ] **Q19 — Conséquences opérationnelles de l'option B.** KYC des commerçants par ContexFly,
  détention de trésorerie de tiers, litiges et remboursements, calendrier de reversement,
  exposition réglementaire (BEAC/COBAC). → à traiter en exigences non-fonctionnelles et à
  arbitrer dans le périmètre MVP.
  Décision : ...

- [x] **Q23 — ContexFly détient-il les fonds ?** **Décision (Maxime, 2026-08-16) : non.** Les fonds
  restent stockés chez l'agrégateur (Notch Pay) dans tous les cas de figure. ContexFly reste donc
  **intermédiaire technique connecté à un agrégateur agréé**, ce qui est cohérent avec la contrainte
  §4.3 du document de recherche et écarte le besoin d'un agrément EME / établissement de paiement.
  L'option B se lit donc comme un encaissement **piloté** par ContexFly, sans détention.
  *Reste à confirmer au contrat (Q21), sans caractère bloquant : qui est titulaire juridique du
  solde avant reversement.*

<!-- **Q23 (version initiale) — 🔴 BLOQUANTE, JURIDIQUE : ContexFly détient-il les fonds ?**
  Le document de recherche de Maxime (§4.3) pose une contrainte qu'aucun de nos échanges n'avait
  reprise : **« Ne jamais détenir les fonds. Rester intermédiaire technique connecté à des
  agrégateurs déjà agréés évite d'avoir besoin d'un agrément de type EME ou établissement de
  paiement (BEAC, BCEAO, CBN selon la zone). »**
  **Cela contredit frontalement la décision Q16 / option B** (« ContexFly encaisse et reverse »),
  et va dans le sens de la réserve réglementaire que Felix avait posée et que Maxime avait écartée.
  **Réconciliation probable, à confirmer :** les deux positions sont compatibles **si** Notch Pay
  Sync fait atterrir les fonds directement dans un **sous-compte au nom du marchand**, ContexFly
  n'étant qu'orchestrateur — encaissement *piloté* sans *détention*. C'est précisément ce qui
  distinguerait ContexFly de Fiitsa, dont l'interface affiche « Fiitsa encaisse pour vous » avec un
  solde retirable, ce qui **est** de la détention.
  **Question exacte à poser à Notch Pay :** avec Sync, les fonds transitent-ils par un compte
  ContexFly, ou sont-ils cantonnés dès l'encaissement sur un sous-compte au nom du marchand ? Qui
  est titulaire juridique du solde avant reversement ?
  ⚠️ **Si les fonds transitent par ContexFly, il faut un agrément.**
  → **Tranché : les fonds restent chez l'agrégateur.** -->

- [ ] **Q24 — Coexistence : contradiction à lever.** Le document de Maxime (§4.2) décrit la
  migration vers l'API comme destructive — perte des contacts, de l'historique et des paramètres,
  retour arrière possible mais avec jusqu'à 30 jours d'inactivité — et recommande de **dédier un
  second numéro à l'API** en gardant le numéro personnel pour les groupes. Les sources sur la
  **Coexistence** disent l'inverse : même numéro sur l'app et l'API, 6 mois d'historique
  synchronisé, groupes non supportés (seul point commun).
  Deux lectures : soit le document précède la Coexistence, soit celle-ci n'est pas disponible au
  Cameroun. **Enjeu direct : la Coexistence est le verrou n°1 levé dans `Positionnement.md`** — si
  elle n'est pas disponible ici, l'argument d'onboarding s'effondre et il faut revenir au discours
  « second numéro dédié ». → fusionner avec Q8, à vérifier sur la documentation Meta officielle.
  Décision : ...

- [ ] **Q25 — Plafond de fréquence marketing : 2 messages par utilisateur et par jour, tous
  expéditeurs confondus.** Vérifié. Meta applique ce plafond **au niveau de l'utilisateur final**,
  pas de l'entreprise : un message peut échouer (**erreur 131049**) parce qu'une autre marque a
  déjà écrit à ce client aujourd'hui. **Conséquence sur le volet fidélisation : la délivrance d'une
  campagne ne peut jamais être garantie.** Le produit doit gérer l'erreur 131049, ne pas la
  présenter comme un échec du commerçant, et probablement réessayer le lendemain. À intégrer aux
  fonctionnalités du domaine F et aux exigences non-fonctionnelles.
  Décision : ...

- [ ] **Q26 — Paliers d'envoi : divergence à arbitrer.** Le document de Maxime indique
  250 → 1 000 → 10 000 → 100 000 → illimité ; la source consultée par Felix indiquait un premier
  palier à 2 000. Faible enjeu à ce stade, mais à figer sur la documentation Meta officielle avant
  d'écrire quoi que ce soit qui en dépende.
  Décision : ...

- [ ] **Q21 — Conditions exactes du contrat Notch Pay Sync.** *(Reformulée : le blocage KYB de
  PawaPay est résolu par le choix de Notch Pay, qui pratique le KYC personne physique.)* À
  confirmer au moment de contractualiser, pas à découvrir en production : pièces exactes exigées
  pour un sous-marchand personne physique, plafond de volume éventuel associé à ce régime, délai
  de reversement, et répartition de responsabilité en cas de litige ou de fraude d'un marchand.
  Décision : ...

- [x] **Q27 — Passer par Genuka WA ?** **Décision (Maxime, 2026-08-17) : non.** ContexFly va
  directement au statut Meta Tech Provider. Conséquence : **Q22 reste le facteur limitant du délai**
  — la validation Meta est sur le chemin critique et doit être engagée immédiatement.

<!-- **Q27 (version initiale) — Passer par Genuka WA plutôt que par le statut Meta Tech Provider ?**
  Découverte du 2026-08-17 : `wa.genuka.com` n'est pas un concurrent mais un **BSP camerounais**.
  Palier **Scale à 30 000 FCFA/mois** = marque blanche + **comptes tiers pour vos clients** + API
  REST + webhooks + jusqu'à 100 numéros, facturé **en mobile money**. C'est l'architecture
  multi-locataire dont ContexFly a besoin, **et ça retire du chemin critique la validation Meta
  qui est aujourd'hui le vrai facteur limitant du délai (Q22)**.
  **À peser contre :** dépendance à un intermédiaire jeune ; **Genuka est simultanément un
  concurrent potentiel** (leur produit principal est un ERP avec inbox pour commerçants) et
  disposerait de la visibilité sur les volumes et les clients de ContexFly ; quotas de 30 000
  messages/numéro/mois à vérifier ; et à terme, être Tech Provider en direct reste meilleur.
  **Lecture possible :** démarrer sur Genuka WA pour tenir les 3-4 semaines, engager le statut
  Tech Provider en parallèle, migrer ensuite.
  → **Tranché : non, Tech Provider en direct.** -->

- [ ] **Q28 — L'argument « 0 % de marge sur tes messages » est déjà pris localement.** Genuka WA
  l'affiche mot pour mot dans son produit. `Positionnement.md` prévoyait d'en faire un argument
  de vente : à reformuler pour ne pas paraître suiveur, ou à abandonner au profit d'un autre.
  Décision : ...

- [ ] **Q22 — ⚠️ Lancer dès maintenant les deux démarches de tiers.** Le délai de 3-4 semaines
  n'est pas contraint par le développement mais par deux validations externes :
  (a) **Meta — statut Tech Provider + Embedded Signup** : app Meta, App Review des permissions
  `whatsapp_business_management` / `whatsapp_business_messaging`, vérification d'entreprise de
  ContexFly. Se compte en semaines, peut être rejeté.
  (b) **Notch Pay — contrat Sync** : négociation commerciale + KYB de ContexFly comme plateforme.
  **À démarrer en parallèle du développement, pas après.**
  Décision : ...

<!-- **Q21 (version initiale) — régime KYC allégé pour les micro-marchands chez PawaPay ?**
  Le Schedule 2 « Intermediary Merchants » impose à ContexFly de collecter, pour **chaque**
  sous-marchand, certificat d'incorporation + statuts + identification des dirigeants, de les
  transmettre sous une semaine, et de produire un reporting mensuel. **Cela réintroduit la
  barrière RCCM que l'option B devait supprimer, cette fois du côté de ContexFly.**
  Question à poser à PawaPay : existe-t-il un régime simplifié pour les micro-marchands ou
  entrepreneurs individuels (pièce d'identité + numéro mobile money, sans documents de société),
  et sous quel plafond de volume ?
  *Si la réponse est non, deux issues seulement : viser les commerces formalisés (ce qui réduit la
  cible), ou revenir vers Notch Pay et négocier un cadre sur mesure.*
  → **Résolu par le choix de Notch Pay (KYC personne physique).** -->

- [x] **Q20 — Notch Pay vs PawaPay.** ⚠️ **Réponse finale : NOTCH PAY.** *(Corrigé le 19/08 — cette
  entrée affirmait encore « PawaPay », décision annulée le 15/08 au soir.)* Historique : Felix avait
  d'abord tranché pour **PawaPay**, principalement parce que le cadre contractuel sous-marchands existe par écrit
  (Schedule 2) et que le prix est identique (1 % encaissement, 1 % reversement). Détail des
  raisons et du coût de ce choix dans `Decision.md`. **Conditionné à Q21.**

<!-- **Q20 — Notch Pay vs PawaPay.** Fiitsa utilise **PawaPay** (mobile money) + **Stripe**
  (cartes) — vérifié dans leur bundle applicatif. PawaPay gère collecte et reversements à
  l'échelle panafricaine. → **Tranché : PawaPay.** -->

- [x] **Q17 — Le mode « acompte ».** Décision (Maxime, 2026-08-15) : **ajouté** comme cinquième
  politique de paiement. Pourcentage réglable par produit, libellé affiché au client final
  personnalisable.

<!-- ancienne formulation de Q16, conservée pour la traçabilité du raisonnement -->
<!-- **Q16 — ⚠️ LA question structurante : ContexFly entre-t-il dans le flux d'argent ?**
  Découverte du 2026-08-15 : **Fiitsa encaisse à la place du commerçant** (« Fiitsa encaisse pour
  vous »), qui n'a donc aucun compte marchand à ouvrir — ni RCCM, ni NIU. La barrière que
  l'arbitrage désignait comme le seul actif défendable de ContexFly est déjà franchie par le
  concurrent local, et c'est aussi ce qui justifie ses 5 %.
  - **Option A — hors du flux.** Le commerçant branche son propre compte Notch Pay. Abonnement
    fixe, 0 % de commission, aucune exposition réglementaire, aucune trésorerie de tiers. Mais
    l'onboarding est plus lourd que chez Fiitsa, et Q11 redevient bloquante.
  - **Option B — dans le flux.** ContexFly encaisse et reverse, comme Fiitsa. Onboarding trivial,
    commission possible. Mais Maxime devient encaisseur pour compte de tiers : trésorerie
    d'autrui, litiges, reversements, exposition réglementaire (BEAC/COBAC), et une charge
    opérationnelle lourde pour un développeur seul.
  *Position de Felix : l'option A reste la bonne pour un dev solo — mais elle impose de résoudre
  l'onboarding autrement.* → **Tranché : option B.** -->

<!-- **Q17 — Le mode « acompte » manque aux politiques de paiement.** Fiitsa propose un versement
  partiel qui confirme la commande, le reste payé à la livraison — pourcentage réglable par
  produit, avec nom et explication personnalisables côté acheteur. Les quatre politiques retenues
  au cadrage de ContexFly ne le contiennent pas. → **Tranché : ajouté.** -->

- [ ] **Q11 — Prérequis d'inscription chez un agrégateur Mobile Money.** *(Notch Pay retenu par
  Maxime le 2026-08-15 — reste à vérifier ses prérequis d'ouverture de compte marchand, et cette
  question ne se pose que si l'option A de Q16 est retenue.)* RCCM ? NIU ? compte
  bancaire d'entreprise ? Aucun agrégateur ne le documente en ligne (CamPay affiche ses
  commissions mais pas ses prérequis ; Notch Pay a un SSL cassé sur ses pages tarifs ; CinetPay
  renvoie 403). **Se tranche par un appel, pas par une recherche.** *Enjeu : si les documents
  d'entreprise sont obligatoires, l'onboarding self-service d'un commerçant informel est
  impossible — et c'est la seule barrière défendable du projet qui disparaît.*
  Décision : ...

- [x] **Q12 — Profondeur réelle de l'agent vendeur de Fiitsa.** *Répondu le 2026-08-15 par
  exploration du produit connecté.* La configuration d'un agent tient en : nom, message d'accueil,
  personnalité en 4 préréglages, langue, et **5 interrupteurs** — dont « Prendre des commandes »,
  **désactivé par défaut**. Aucun rattachement au catalogue, aucune base de connaissance, aucune
  règle métier. L'état vide de la section parle de « collecter des leads », pas de vendre.
  **L'espace produit sur la profondeur de l'agent est réel.**
  *Réserve : formulaire de création uniquement ; une configuration plus profonde peut exister
  après création. → Q12bis, test à faire par Maxime.*

- [ ] **Q12bis — Configuration post-création de l'agent Fiitsa.** Créer un chatbot avec « Prendre
  des commandes » activé et vérifier ce que la configuration avancée offre réellement (catalogue,
  règles, paiement). Non fait : écrit dans le compte de Maxime.
  Décision : ...

- [x] ✅ **Q13 — Coût d'inférence.** **Modélisé le 2026-08-19** (`Contraintes-Techniques.md` §5).
  Fournisseur imposé : Gemini. **Sur Gemini 2.5 Flash (0,30 $/2,50 $ par million), une conversation
  de vente coûte ≈ 10 FCFA, soit ≈ 6 000 FCFA/mois pour un commerçant à 20 conversations/jour.**
  → **Un abonnement à 15 000 FCFA avec conversations illimitées tient**, avec ~60 % de marge brute.
  🔴 **Mais il ne tient pas sur Gemini 3.7 Flash** (≈ 24 FCFA/conv. au tarif d'introduction, ≈ 48
  après le 01/01/2027 quand ce tarif double).
  *Chiffres fondés sur des hypothèses de volumétrie non mesurées — I3 à instrumenter dès le premier
  jour pour les remplacer par des mesures réelles avant de figer la tarification.*

- [ ] **Q14 — Ngavix.** Module « boutique WhatsApp » revendiqué à partir de 10 000 FCFA/mois
  (source secondaire non confirmée). S'il existe vraiment, il est pile dans le trou de prix
  identifié comme l'espace de ContexFly. À ouvrir avant tout autre concurrent.
  Décision : ...

- [ ] **Q15 — AgentCraftr.** Site 100 % JS, positionnement affiché exactement dans le segment
  (« own catalogue », « takes orders »). Seul concurrent mondial potentiel non évalué.
  Décision : ...

## À vérifier au benchmark / plus tard

- [ ] **Q4 — Tarif Meta exact pour le Cameroun.** Relever sur la grille officielle « Rest of
  Africa » les taux marketing / utility / authentication en vigueur, pour chiffrer la marge.
  Décision : ...

- [ ] **Q5 — Agrégateur Mobile Money.** Quel prestataire pour encaisser Orange Money et MTN MoMo
  (Campay, Notch Pay, MeSomb, CinetPay, Flutterwave, Pawapay…) : commissions, délai de
  reversement, API de callback, disponibilité réelle. À creuser avec `saas-essentiels`.
  Décision : ...

- [x] **Q6 — Périmètre réel de l'inbox.** **Tranché : inbox de supervision, pas helpdesk** (E1,
  et scope OUT d'`Idee.md`). *(Cochée le 19/08 — elle était restée ouverte à tort.)*

<!-- **Q6 — Périmètre réel de l'inbox.** Inbox minimale de supervision ou vraie boîte de
  réception « qui remplace WhatsApp » ? À trancher au skill `fonctionnalites`.
  Décision : ... -->

- [ ] **Q7 — Qui porte le coût des messages sortants.** Piste forte : en statut **Tech Provider**,
  le client ajoute son propre moyen de paiement sur son propre WABA — Meta le facture directement,
  ContexFly n'avance rien. À confirmer et à arbitrer au skill `tarification`.
  Décision : ...

- [ ] **Q8 — Coexistence disponible au Cameroun ?** Les sources qui annoncent une disponibilité
  mondiale sont des éditeurs tiers, pas Meta. À confirmer sur la documentation officielle avant
  d'en faire un argument commercial — c'est le levier n°1 de réduction de la friction d'onboarding.
  Décision : ...

- [ ] **Q10 — Statut Tech Provider : délai et conditions d'obtention.** Prérequis, durée de
  validation, et ce que ça implique côté vérification de ContexFly en tant qu'entreprise.
  Décision : ...
