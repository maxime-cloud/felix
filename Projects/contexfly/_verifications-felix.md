# Vérifications faites par Felix lui-même (navigateur intégré, JS exécuté)

Ce fichier complète les rapports des sous-agents, qui n'avaient pas de navigateur capable
d'exécuter le JavaScript. Tout ce qui suit a été lu sur la page rendue, pas sur un extrait de
moteur de recherche ni sur un blog tiers.

---

## Fiitsa — vérification du 2026-08-15 (https://fiitsa.com/pricing)

### Correction majeure au rapport local : Fiitsa n'est pas un concurrent focalisé

Le sous-agent local l'a décrit comme « la promesse de ContexFly ». La page de tarifs rendue dit
autre chose : Fiitsa est une **suite business généraliste à 8 agents IA**, dont la vente sur
WhatsApp n'est qu'une brique parmi d'autres. Les 8 agents nommés sur la page :

| Agent | Rôle affiché |
|---|---|
| Leslie | « patronne IA », orchestre les 7 autres |
| Claude | factures, devis, contrats |
| Alex | construction de workflows d'automatisation |
| Naïrobi | campagnes Facebook/Instagram Ads |
| Joyce | community management, publications réseaux sociaux |
| Tommy | création de templates WhatsApp conformes Meta |
| Audrey | création de site web et de tunnels de vente |
| *(agent support personnalisé)* | **« ton vendeur 24/7 » — c'est le seul qui correspond au cœur de ContexFly** |

S'y ajoutent : calendriers de prise de rendez-vous, formulaires WhatsApp, CRM avec segments et
tags, gestion d'équipe, documents générés par IA, et **Fiitsa Studio** — une prestation de
production de vidéos et visuels publicitaires **faite par des humains** (« montée par nos soins à
partir de tes rushs »), facturée en crédits.

**Lecture produit :** Fiitsa fait de la vente conversationnelle, de la pub, du community
management, de la facturation, du site web et de la production vidéo. C'est très large pour un
produit jeune. Un outil qui fait une seule chose — encaisser une commande sur WhatsApp — et qui
la fait mieux, a de l'espace. **C'est le premier angle de différenciation crédible identifié.**
À confronter au verdict de `critique-produit` avant d'en faire une conviction.

### Tarifs relevés sur la page rendue (5 formules)

| Formule | Prix | Commission sur les ventes | Notable |
|---|---|---|---|
| Découverte | Gratuit | **5 %** | 1 business, 500 contacts, **3 produits max**, 1 Go |
| Pay As You Go | Gratuit + crédits | **5 %** | contacts illimités, 10 Go, domaine perso |
| Premium | **49 990 FCFA/mois** | 0 % | 20 Go, 20 workflows, 10 000 exéc./mois |
| Entreprise | **99 990 FCFA/mois** | 0 % | 50 Go, + Fiitsa Studio (1 vidéo + 3 visuels/mois) |
| Agence | **Gratuit** | 0 % | businesses illimités, 200 Go, **White Label** |

- Essai gratuit de 14 jours sur les plans payants, sans engagement.
- Paiement : Mobile Money (Orange Money, MTN, Wave, Moov, Airtel, M-Pesa) ou carte.
- **Crédit PAYG = 100 FCFA.** Coûts unitaires affichés : agent vendeur **1 crédit / conversation
  / jour** (100 FCFA), campagne WhatsApp 10 crédits (1 000 FCFA), exécution d'automatisation
  0,5 crédit, génération de document IA 3 crédits, vidéo Studio 200 crédits (20 000 FCFA).

### Ce que ces chiffres impliquent pour la tarification de ContexFly

1. **Le vrai prix d'entrée du marché, ce n'est pas 49 990 FCFA — c'est 5 % du chiffre d'affaires.**
   Un commerçant à 500 000 FCFA/mois de ventes paie 25 000 FCFA de commission sur le plan gratuit.
   C'est l'ancrage réel auquel ContexFly sera comparé, et il est **variable** : indolore au
   démarrage, punitif quand ça marche. Un abonnement fixe est un contre-argument commercial fort
   auprès d'un commerçant qui commence à bien vendre.
2. **Le PAYG devient absurde au volume**, et Fiitsa l'assume dans son propre simulateur : 20
   conversations/jour = 60 000 FCFA/mois d'agent IA seul, soit plus cher que Premium. Le
   simulateur pousse explicitement vers Premium. À l'inverse, un commerçant à faible volume paie
   presque rien — c'est un modèle d'acquisition, pas de monétisation.
3. **Le plan Agence gratuit avec White Label et businesses illimités est incohérent** avec le
   reste de la grille (pourquoi payer Premium ?). Signe d'un produit encore en construction — pas
   d'une position défendue.

### Incohérences relevées (signal de maturité, à ne pas surinterpréter)

- Cette page annonce **« +500 entrepreneurs africains »**. Le rapport du sous-agent citait
  3 000-4 000 clients depuis d'autres sources. Les deux ne peuvent pas être vrais en même temps
  → les chiffres d'adoption de Fiitsa ne sont pas fiables, ne pas les utiliser comme référence.
- Le calculateur de ROI affiche des gains inventés (« +40 % de ventes », « rentable en 6 jours »)
  sans source. C'est du marketing, pas une donnée de marché — à ne pas reprendre.
- Revendication **« 0 risque de blocage par Meta »** sur les campagnes WhatsApp. Aucun
  fournisseur ne peut garantir cela : le *quality rating* dépend du taux de blocage des
  destinataires, pas de l'outil d'envoi. Promesse intenable.

### Non vérifié — à ne pas conclure

- **La profondeur réelle de l'agent vendeur.** Impossible à évaluer sans créer un compte : la
  page ne dit pas si l'IA négocie une commande en langage naturel ou se contente d'envoyer un
  catalogue et un formulaire. La ligne « Formulaires WhatsApp — achats, réservations » suggère un
  parcours par **formulaire** plutôt que par conversation, mais **ce n'est pas une preuve.**
  → C'est LA question à trancher, elle décide s'il reste un espace produit. Test réel nécessaire.
- Le contenu des réponses de la FAQ (dont « Puis-je connecter mon propre numéro WhatsApp
  Business ? ») n'est pas dans le DOM tant qu'on ne déplie pas — non lu.

---

## 🎯 Genuka WA — ce n'est pas un concurrent, c'est un fournisseur possible (2026-08-17)

**Correction majeure du benchmark.** `_benchmark-local.md` classait Genuka comme « ERP + inbox ».
C'est vrai du produit principal (genuka.com), mais **`wa.genuka.com` est un produit
complètement différent : un fournisseur d'accès à l'API WhatsApp officielle** — un BSP
camerounais, orienté développeurs.

Menu du produit : Vue d'ensemble, **Numéros**, **Webhooks**, **Journaux**, **Clés API**,
Facturation, Documentation. Pas d'inbox, pas d'agent, pas de catalogue, pas de commandes.
Métriques : messages envoyés / livrés / échoués, nombre de templates.

### Leur grille tarifaire (relevée dans le produit)

| Palier | Prix | Ce qu'il contient |
|---|---|---|
| **Starter** | **5 000 FCFA/mois** | 1 numéro (+2 500/numéro supp.), jusqu'à 5 numéros, **500 msg/numéro/mois**, 1 utilisateur, 7 j de journaux, API REST, webhooks |
| **Growth** | **10 000 FCFA/mois** | 1 numéro (+2 200 supp.), jusqu'à 15 numéros, **5 000 msg/numéro/mois**, 5 utilisateurs, 30 j de journaux, **marque blanche** |
| **Scale** | **30 000 FCFA/mois** | 1 numéro (+1 800 supp.), jusqu'à 100 numéros, **30 000 msg/numéro/mois**, 15 utilisateurs, 90 j de journaux, marque blanche, **⭐ comptes tiers pour vos clients** |
| Enterprise | Sur devis | Numéros illimités, SLA contractuel |

Facturation **par mobile money via Genuka Pay (XAF/XOF)**. Carte bancaire « bientôt ».

Leur argument, mot pour mot : *« 0 % de marge sur vos messages — leur coût passe directement de
Meta au compte WhatsApp Business qui les a envoyées, au tarif Meta. Pas de crédits, pas de
portefeuille — vous payez l'abonnement, rien d'autre. »*
C'est **exactement** l'argument que `Positionnement.md` prévoit de reprendre. Il est donc déjà
occupé localement, et par un acteur crédible. À reformuler pour ne pas paraître suiveur.

### ⚠️ Ce que ça ouvre — une alternative au statut Tech Provider

Le palier **Scale à 30 000 FCFA/mois** offre **marque blanche + comptes tiers pour vos clients +
API REST + webhooks + jusqu'à 100 numéros**. C'est-à-dire, en pratique, l'architecture
multi-locataire dont ContexFly a besoin.

**Q22 identifiait la validation Meta (Tech Provider, App Review des permissions
`whatsapp_business_management` / `whatsapp_business_messaging`, vérification d'entreprise) comme
le vrai facteur limitant du délai de 3-4 semaines — plusieurs semaines, et rejet possible.
Passer par Genuka WA supprimerait ce blocage du chemin critique.**

**Ce que ça coûte, et il faut le peser :**
- **Dépendance à un intermédiaire jeune** — si Genuka WA tombe ou change ses conditions, tout
  ContexFly s'arrête.
- **⚠️ Risque stratégique réel : Genuka est simultanément un concurrent potentiel.** Leur produit
  principal est un ERP avec inbox pour commerçants camerounais. Bâtir sur l'infrastructure d'une
  entreprise qui peut décider demain d'entrer sur ton segment — avec la visibilité sur tes volumes
  et tes clients que lui donne son rôle de fournisseur — n'est pas neutre.
- **Quotas par numéro** — 30 000 messages/numéro/mois au palier Scale. À confronter au volume
  réel d'un commerçant actif avant de conclure que ça suffit.
- **Économiquement**, à terme, être Tech Provider en direct reste meilleur (contrôle, marge,
  relation Meta).

→ **Piste sérieuse pour accélérer le lancement, à ne pas confondre avec la cible long terme.**
Une lecture possible : démarrer sur Genuka WA pour livrer en 3-4 semaines, et engager le statut
Tech Provider en parallèle pour migrer ensuite. → **Q27**, à arbitrer par Maxime.

---

## Landbot — exploration impossible (2026-08-17)

Onboarding non réalisé. Le widget « AI Copilot » vit dans une iframe dont le champ de saisie
n'est pas atteignable par l'arbre d'accessibilité ; la saisie se vide sans que la conversation
avance. En parallèle, la capture d'écran a expiré à répétition (renderer bloqué, application
lourde). Le clic sur « Create your first agent » n'a jamais abouti.

**Rien n'a donc été observé — aucune conclusion n'est tirée de Landbot.** Ce qui était visible :
la navigation du produit (Agent builder, Inbox, WhatsApp, Contacts, Channels, Integrations,
Metrics) et le fait que **leur onboarding est lui aussi un agent conversationnel qui construit
l'agent** (« I'll build a custom Agent based on your answers »), ce qui confirme, sans plus, que
le motif de B0 est en train de devenir un standard.

À reprendre avec le **MCP Playwright** (installé), mieux armé pour ce genre d'application.

---

## Ngavix — Q14 tranchée (2026-08-17, compte réel)

**Ngavix n'est pas un produit de commerce WhatsApp.** C'est une suite de gestion d'entreprise :
Projets, Tâches, CRM, Finance, Facturation, Stock, Objectifs, Agenda, **Boutique**, Fournisseurs,
Équipe, Reporting, RH, Analytics, Business Intelligence, Entités & Filiales. Tous les modules sont
`OFF` tant qu'un abonnement n'est pas actif. Essai gratuit 14 jours, sans carte.

### Le module « Boutique en ligne » — le tarif revendiqué est confirmé

| Palier | Prix |
|---|---|
| **Starter** | **10 000 FCFA/mois** |
| Pro | 25 000 FCFA/mois |
| Business | 55 000 FCFA/mois |

Paiement par **GeniusPay** — Wave, Orange Money, MTN MoMo ou carte. *(Un agrégateur local de plus
à verser au dossier Q20.)*

Contenu du module : tableau de bord, **catalogue produits**, **commandes**, **codes promo**,
paramètres boutique. Statuts de commande : *En attente · Confirmée · Expédiée · Livrée · Annulée*.

### 🎯 Ce que ça change pour le positionnement — précision, pas invalidation

Phrase relevée dans le produit : *« Les notifications WhatsApp sont envoyées automatiquement à
chaque changement de statut. »*

**WhatsApp n'est utilisé que pour des notifications sortantes de statut.** Il n'y a ni agent
conversationnel, ni boîte de réception, ni panier construit dans la conversation. C'est une
boutique en ligne classique avec des notifications WhatsApp greffées dessus.

**Le trou de prix survit, mais sa formulation doit être corrigée.** Il est faux de dire « à 10 000
FCFA/mois personne ne fait rien » : à ce prix, un commerçant camerounais a déjà une boutique, un
catalogue, des commandes avec statuts, des codes promo, l'encaissement Mobile Money et des
notifications WhatsApp.

→ **La revendication exacte de ContexFly n'est pas « la chaîne complète à ce prix », c'est
« la *conversation* à ce prix ».** Ce qui n'existe nulle part entre 0 et 49 990 FCFA, c'est
l'agent qui répond, qualifie, construit le panier et encaisse **dans le fil WhatsApp** — pas la
boutique. À corriger dans `Positionnement.md`.

### Deux détails à retenir

- **Ngavix est installable en PWA** avec la promesse « même hors connexion ». Le **mode dégradé en
  connexion instable**, que j'avais listé comme un vide que personne ne remplit, est en train
  d'être adressé par un acteur local. À reclasser : ce n'est plus un espace libre.
- Les montants du tableau de bord s'affichent en **€**, ceux de la boutique en **FCFA** —
  incohérence de devise dans le même produit.

---

## Zoko — compte démo exploré (2026-08-17)

### Le pattern d'activation, à l'opposé de Wazzap

Zoko ouvre un **compte de démonstration pré-rempli de conversations réalistes**, valable 7 jours,
avec un bandeau permanent « Connect My number ». On explore le produit complet **avant** de
brancher son numéro et **avant** de payer — l'inverse exact de Wazzap qui place son paywall en
étape 3 sur 5, avant même la connexion WhatsApp.

**C'est directement pertinent pour ContexFly** : le catalogue vide est la mortalité n°1 de ce type
de produit, et un compte de démo pré-rempli est une réponse peu coûteuse à ce problème. → à
verser au débat sur le placement du paiement (`tarification`, `parcours-utilisateur`).

### 🎯 La conversation de démo confirme la prémisse de B0

Le scénario que Zoko a choisi comme représentatif de son produit :

> — *« Hi! Do you have the blue running shoes in size 9? »*
> — *« Hi Emma! Yes, the blue runners are in stock in size 9. Would you like me to share the link? »*
> *(carte produit : « Blue Runner - Size 9 »)*
> — *« Looks great! How much is it? »* — *« They're $79.99, and we have free shipping this week 🎉 »*
> — *« Perfect, I'll place the order »*

**La question canonique du commerce sur WhatsApp est une question de variante.** Zoko l'a mise en
vitrine ; Fiitsa ne peut pas y répondre (pas d'accès stock ni d'attributs). C'est l'argument le
plus concret en faveur de B0 rencontré jusqu'ici.

### Le panneau de conversation — modèle à reprendre pour le domaine E

Onglets **Profile / Catalog** à droite de la conversation :
- Téléphone, **pays et heure locale du client**, e-mail
- **TAGS** éditables — dans la démo : `VIP`, `cart_abandoned`, `SUPPORT`
- **MEDIA** (tous les fichiers échangés)
- **ORDERS** — historique de commandes, avec bascule **« Current customer » / « All Customers »**
- **Catalog** accessible sans quitter la conversation
- En-tête : **« Assign to: [agent] »**

⭐ **Détail à ne pas rater : un badge `TEMPORARILY ALLOWED` à côté du numéro** — c'est
l'indicateur de la **fenêtre de service de 24 h**. L'opérateur voit d'un coup d'œil s'il peut
écrire librement ou s'il doit passer par un template payant. **À reprendre tel quel dans l'inbox
de ContexFly** : sans ça, un vendeur ne comprend pas pourquoi son message part ou ne part pas.

Vues de l'inbox : `All Chats` / `Unassigned` / `My Chats` / `Other Agents' Chats`, et filtres
`All` / `Unread` / `Unreplied`.

### Surface fonctionnelle complète (page « All Features »)

- **AI & Automation** — compétences IA, **constructeur visuel de workflows en glisser-déposer**,
  **moteur de règles** (les deux coexistent), **messages de bienvenue et d'absence**,
  **réponses rapides**
- **WhatsApp** — profil du compte, **Broadcast**, **Templates**, **Catalog**,
  publicités Click-to-WhatsApp, appels WhatsApp
- **Organize Customers** — Contacts, **Segments** (entité distincte des contacts)
- **Shopify Website** — bouton click-to-chat, campagnes pop-up → **dépendance Shopify confirmée**
- **Agents & équipes** — permissions, **Business Hours**, fuseau horaire,
  **Agent Analytics** (temps de réponse, taux de résolution) — en BETA
- **Autres** — Webhooks & API, 2FA, facturation et usage, intégrations

**Trois manques dans mon inventaire de fonctionnalités, à combler :**
1. **Horaires d'ouverture + message d'absence** — l'agent répond 24h/24, mais le commerçant doit
   pouvoir annoncer ses horaires réels de préparation et de livraison. Effort S, valeur immédiate.
2. **Réponses rapides** pour l'opérateur humain — trivial à construire, très utilisé.
3. **Analytique par agent** (temps de réponse, taux de résolution) — c'est la brique qui permet de
   mesurer le **taux d'autonomie**, objectif n°1 de `Idee.md`. Sans elle, la métrique reste
   déclarative.

**Absence notable : aucune section « commandes » dans leur produit** — les commandes vivent dans
Shopify. Cela confirme le trou que ContexFly occupe.

---

## Trois inscriptions impossibles — et ce que ça dit (2026-08-17, testé par Maxime)

- **🎯 Flowcart refuse les numéros WhatsApp camerounais à l'inscription.** Le numéro est
  obligatoire, un +237 est rejeté avec un simple « numéro invalide », alors qu'un numéro français
  quelconque passe. **C'est plus fort que le constat précédent** (« pas de XAF dans le sélecteur
  de devises ») : Flowcart ne peut **pas** onboarder un commerçant camerounais aujourd'hui, même
  s'il le voulait. Le verdict « concurrent à 12-24 mois, haut de marché » est confirmé et
  renforcé.
- **Ayweu est une application mobile uniquement** — pas d'accès web. Cohérent avec un marché
  mobile-first, et à retenir comme signal produit : leur cible ne travaille pas sur ordinateur.
  ⚠️ **À verser au débat sur l'inbox de ContexFly** (Q6) : si le concurrent local qui revendique
  3 000+ vendeurs est mobile-only, une inbox pensée d'abord pour le bureau est peut-être un
  contresens.
- **Chatarmin ne propose pas d'inscription en libre-service** — démonstration commerciale
  uniquement. Signal de positionnement : ils vendent à des marques, pas à des commerçants.

---

## Wazzap.ai — onboarding et configuration d'agent parcourus (2026-08-16, compte réel de Maxime)

Parcours complet réalisé jusqu'au paywall. **Le produit le plus instructif rencontré jusqu'ici
pour ContexFly** — pas par ses fonctionnalités, mais par la façon dont il fait entrer un
commerçant.

### La structure de l'onboarding

`Modèle → Configuration → Plan → WhatsApp → Prêt`, précédé de 7 questions de profil.

1. **Profil** (Entrepreneur / Cadre / **Commerçant** / Freelance / Étudiant)
2. **Identité** — prénom, nom, numéro WhatsApp **optionnel** (indicatif +237 auto-détecté)
3. Attribution (« tu nous as trouvés comment ? »)
4. **« Tu as un site web ? »** — *« ça nous permettra de mieux configurer ton assistant »*
5. **Secteur** — *« ton assistant sera calé sur ton métier dès le départ »*
6. **Taille d'équipe** — *« on adapte les automatisations à ta structure »*
7. **Objectif n°1** (répondre 24h/24 / générer des leads / automatiser le SAV / **booster les
   ventes**) — *« ton assistant sera configuré pour ça en premier »*

Puis **branchement selon l'objectif** : 3 questions supplémentaires (volume de messages/jour,
temps passé par semaine, résultat attendu).

### 🎯 Trois mécaniques à reprendre pour ContexFly

**1. L'écran miroir de valeur.** Après les questions, ils recalculent les réponses de
l'utilisateur et les lui renvoient : *« Tu passes 10h par semaine sur ça. Soit 65 jours entiers
par an. »* avec trois compteurs (10h/semaine, 520h/an, 9 000 messages à traiter cette année).
Aucune demande, aucun prix — juste le problème chiffré avec ses propres chiffres, juste avant
l'engagement. Bouton : « Récupérer ce temps ». C'est très bien fait et directement transposable.

**2. Chaque question justifie sa présence en une ligne.** « Ça nous permettra de mieux configurer
ton assistant », « on adapte les automatisations à ta structure ». Sur une cible peu technique,
c'est ce qui évite l'abandon en cours de formulaire.

**3. La configuration de l'agent est elle-même conversationnelle**, avec des **suggestions
cliquables générées à deux niveaux** : d'abord depuis le secteur déclaré, puis **depuis les
réponses précédentes de l'utilisateur**. Concrètement : à la question « quelles questions tes
clients posent le plus souvent ? », les propositions étaient *Prix et disponibilités · Délais de
livraison · **Tailles / couleurs** · Suivi de commande · Retours et remboursements*. Deux tours
plus tard, à « quelles tâches doit gérer ton agent ? », les propositions étaient devenues
*Répondre aux prix · Vérifier disponibilités · Donner délais livraison* — **dérivées de ma réponse
en texte libre**. C'est exactement le mécanisme de mémoire visé par B0, en fonctionnement.

Autre dimension de configuration à retenir, absente de chez Fiitsa : **la longueur de réponse**
(concises 1-2 phrases / explicatives / formelles / naturelles). Sur WhatsApp, c'est un réglage
qui compte plus que la « personnalité ».

### ⚠️ Correction à apporter à l'analyse de B0

**L'affirmation « aucun équivalent identifié dans le benchmark » était trop forte.** Wazzap fait
de la configuration conversationnelle adaptative au secteur, avec suggestions apprises des
réponses. B0 reste distinct, mais la frontière doit être décrite honnêtement :

| | Wazzap | B0 de Maxime |
|---|---|---|
| Objet configuré | la **FAQ et le comportement** de l'agent | le **modèle de données produit** |
| Adaptation | au secteur déclaré | au **type de produit**, produit par produit |
| Mémoire | dans la session d'onboarding | **persistante, par catégorie et par commerçant**, enrichie à chaque ajout |
| Attributs structurés | ❌ aucun | ✅ pointure, couleur, variante |

**Vérifié : leur création de catalogue ne demande aucun attribut spécifique produit.** À
« chaussures et sacs », l'agent a répondu : *« Envoie-moi 2-3 photos de tes produits phares, je
vais les ajouter au catalogue avec une description et un prix. »* — **il n'a jamais demandé les
pointures ni les couleurs**, alors même qu'il savait qu'il s'agissait de chaussures. Ils génèrent
une description depuis une photo ; ils ne construisent pas de modèle d'attributs.

→ **B0 tient**, et le vrai différenciateur se formule mieux ainsi : *ils configurent ce que
l'agent dit ; B0 configure ce que l'agent sait*. À noter aussi : le pré-remplissage par photo,
que j'avais listé en piste d'approfondissement de B0, existe déjà chez eux — ce n'est donc pas un
« plus tard » gratuit, c'est un standard en train de s'installer.

### Défauts d'exécution relevés

- **Bug de la configuration conversationnelle, répété.** À la question « comment veux-tu
  l'appeler ? », ma réponse « Vendeuse IA » a été enregistrée comme **une prestation vendue par le
  commerçant** : *« ✓ Service ajouté : Vendeuse IA — Vendeuse IA ajouté à tes prestations. »*, puis
  au tour suivant *« ✓ Service déjà existant réutilisé : Vendeuse IA »*. L'agent a perdu le fil de
  ce qu'il collectait et a écrit une donnée fausse dans le catalogue du commerçant.
  ⚠️ **C'est précisément le risque de B0** : un agent de saisie conversationnelle qui se trompe de
  contexte corrompt le catalogue, silencieusement. À traiter en exigence non-fonctionnelle —
  confirmation explicite avant écriture, et possibilité d'annuler.
- Les suggestions cliquables **régressent** vers des valeurs génériques après quelques tours
  (« Je vends des produits / Je propose un service / Les deux »), signe d'une machine à états
  fragile.

### Décision produit à noter

**Le paywall est placé AVANT la connexion WhatsApp** (`Plan` en étape 3, `WhatsApp` en étape 4).
Le commerçant paie avant d'avoir branché son numéro — donc avant d'avoir vu la moindre valeur
réelle. Choix agressif, à opposer au modèle de Fiitsa qui laisse créer un business sans jamais
connecter Meta. **Question ouverte pour ContexFly** : où placer le paiement par rapport à la
première commande encaissée ? → à trancher à `tarification` et `parcours-utilisateur`.

*(Exploration arrêtée à l'étape 3 — paywall, aucun achat effectué.)*

---

## Fiitsa — exploration du produit connecté (2026-08-15, compte réel de Maxime)

Navigation dans l'application, extension Chrome, compte Découverte. **Répond à Q12.**

### 1. ⚠️ Le fait le plus important du dossier : Fiitsa encaisse à la place du commerçant

Texte lu dans Paramètres → Paiements : *« Aucune configuration supplémentaire requise. **Fiitsa
encaisse pour vous, donc aucune configuration nécessaire de votre part.** Tous les paiements de
vos clients (Mobile Money, Carte bancaire) sont automatiquement traités par Fiitsa. Votre solde
est disponible sur la page Revenus. Vous pouvez le retirer via Mobile Money. »*

**Fiitsa est encaisseur pour compte de tiers.** Le commerçant n'a **aucun** compte marchand à
ouvrir — donc ni RCCM, ni NIU, ni compte bancaire d'entreprise. C'est aussi ce qui justifie
économiquement les 5 % de commission : ils sont dans le flux d'argent.

**Conséquence directe sur le verdict de l'arbitrage :** la « seule barrière durable candidate »
identifiée — onboarder un commerçant informel sur un rail de paiement — **est déjà franchie par
Fiitsa**, et par le contournement le plus simple qui soit. Q11 change de nature : la question
n'est plus « est-ce que Notch Pay exige un RCCM ? » mais « ContexFly entre-t-il, oui ou non, dans
le flux d'argent ? ». → nouvelle question **Q16**, structurante, arbitrage de Maxime requis.

Méthodes de paiement proposées : **Mobile Money** (Orange Money, MTN Mobile Money, Wave),
**carte bancaire via Stripe**, **paiement à la livraison**. Plus un « checkout intégrable »
(script à coller sur son propre site).

### 2. La fonctionnalité « Acompte » — une idée locale que le cadrage de ContexFly n'a pas

Paramètres → Paiements → section ACOMPTE. Le commerçant définit un **versement partiel** qui
confirme la commande, le reste étant payé à la livraison. Le pourcentage se règle **produit par
produit**. Deux champs de texte libre : le **nom affiché** (« le mot *acompte* fait hésiter —
nomme le versement comme tu le dis en live ») et **à quoi sert ce versement** (exemple fourni :
« Confirme ta commande et réserve le livreur. Le reste se paie à la livraison. »).

C'est bien pensé : ça règle le problème de confiance du paiement à la livraison (le commerçant
risque un client absent) sans imposer le prépaiement intégral, et ça travaille la formulation
côté acheteur.

⚠️ **Les quatre politiques de paiement retenues au cadrage de ContexFly ne contiennent pas ce
mode.** L'acompte est probablement le plus adapté au terrain camerounais des cinq. → à trancher
au skill `fonctionnalites`.

### 3. Réponse à Q12 — la profondeur de l'agent vendeur

Le formulaire de création d'un agent (Agents IA → Mes ChatBots → Créer) contient **exactement** :
nom, message d'accueil, **personnalité en 4 préréglages** (Amical / Professionnel / Décontracté /
Formel), langue, et **cinq interrupteurs** :

| Fonctionnalité | Par défaut |
|---|---|
| Collecter des leads | ✅ activé |
| Répondre aux FAQ | ✅ activé |
| **Prendre des commandes** | ❌ **désactivé** |
| Réserver des RDV | ❌ désactivé |
| Transférer à un humain | ✅ activé |

Puis « Créer le chatbot ». **C'est tout.** Aucun rattachement au catalogue, aucune base de
connaissance, aucune règle métier, aucune politique de paiement, aucun ton libre.

L'état vide de la section annonce par ailleurs : *« Créez votre premier chatbot IA pour engager
vos visiteurs 24/7 et **collecter des leads** automatiquement »* — un cadrage de **chatbot de site
web pour capter des leads**, pas d'un vendeur WhatsApp qui construit une commande.

**Lecture : la prise de commande est une case à cocher parmi cinq, désactivée par défaut, dans un
produit dont le discours par défaut est la capture de leads.**

⚠️ **Limite honnête de cette vérification :** c'est le formulaire de *création* (« Configurez les
bases »). Une configuration plus profonde existe peut-être **après** création — je n'ai pas créé
d'agent, ça écrit dans le compte de Maxime. Ne pas conclure définitivement avant ce test.

### 3bis. Q12bis — la configuration avancée de l'agent (agent créé et testé)

Un agent créé ouvre une configuration en **7 onglets** : Identité, Personnalité, Connaissances,
Données, Fonctions, Apparence, Tester. Ma réserve était fondée : il y a bien de la profondeur
au-delà du formulaire de création. Détail de ce qui compte :

**Identité** — nom, avatar, message de bienvenue, et un sélecteur **« Objectif de l'agent »**
(valeur par défaut : *Assistant complet – Toutes les fonctionnalités*) qui « définit le
comportement et les outils disponibles ».

**Connaissances** — FAQ personnalisée (paires question/réponse), **scan d'un site web** pour
alimenter le bot, et une base de connaissances libre (titre + contenu). Correct et classique.

**Fonctions** — les mêmes cinq interrupteurs, avec leurs sous-titres. Celui qui compte :
**« Prendre des commandes — *Guider vers l'achat* »**. Le libellé interne dit *guider vers*
l'achat, pas *prendre* la commande. Faible, mais convergent avec tout le reste.

**Données — « Choisissez quelles données de votre business le bot peut utiliser » :**

| Donnée | Par défaut |
|---|---|
| Données business (nom, description, contact) | ✅ |
| **Produits** (catalogue) | ✅ |
| **Prix** | ✅ |
| **Stock** (quantités disponibles) | ❌ **désactivé** |
| Réservations | ❌ |
| Livraison | ✅ |

Deux observations :
- **Le stock est coupé par défaut** — l'agent peut donc vendre un article épuisé. Pour ContexFly,
  c'est un défaut à ne pas reproduire : sur une boutique camerounaise, vendre ce qu'on n'a pas
  détruit la confiance plus vite que tout le reste.
- ⚠️ **Il n'existe aucune case donnant à l'agent l'accès à l'historique de commandes du client.**
  Ni « Commandes », ni « Historique client », ni « Contacts ». **L'agent de Fiitsa est
  structurellement incapable de savoir qu'un client en est à sa troisième commande.** La remise
  de fidélité proposée en conversation — l'idée de Maxime — n'est pas seulement absente du
  produit : elle n'est pas branchable sur l'architecture actuelle de leur agent.

**Tester — l'agent ne répond pas.** Deux messages envoyés dans le testeur intégré (une commande
détaillée, puis un simple « Bonjour ») : **deux échecs**, avec l'erreur brute
**« Failed to send a request to the Edge Function »** affichée telle quelle à l'utilisateur.

Réserves honnêtes : c'est le testeur intégré au module de configuration, pas la boutique en
production ni WhatsApp ; le compte n'a ni produits ni connexion Meta. Mais l'échec sur un simple
« Bonjour » pointe vers l'appel au modèle lui-même, pas vers un manque de données. Et faire fuiter
une erreur d'infrastructure Supabase jusque dans l'interface d'un commerçant est un défaut en soi.

**Bilan Q12 + Q12bis :** l'agent de Fiitsa a bien accès au catalogue et aux prix, et sa
configuration est plus fournie que le formulaire de création ne le laissait croire. Mais il est
cadré comme un assistant de site web, il ne connaît pas l'historique d'achat, il ignore le stock
par défaut, et il ne répondait pas au moment du test. **L'espace produit tient.**

### 3ter. Réponse à la question de Maxime — quel prestataire de paiement utilise Fiitsa ?

Vérifié par inspection du bundle JavaScript de l'application (`index-CZwXWBPJ.js`), qui charge
notamment :

- `PawaPayPendingStatus-*.js` et `pawapayCountries-*.js` → **PawaPay** pour le mobile money
- `StripePayment-*.js` → **Stripe** pour les cartes (cohérent avec le libellé « via Stripe » lu
  dans les paramètres)
- `PaymentCheckout-*.js`, `currencyConverter-*.js`
- Accessoirement : `useWhatsAppCatalog-*.js` → ils exploitent bien le **catalogue WhatsApp natif**

**Fiitsa = PawaPay (mobile money) + Stripe (cartes).** PawaPay est un agrégateur mobile money
panafricain qui gère la collecte **et** les reversements — exactement l'architecture nécessaire
pour encaisser au nom de commerçants tiers, ce qui est cohérent avec le « Fiitsa encaisse pour
vous » et avec la commission de 5 %.

### 4. Réponse à Q6bis — le constructeur de règles est vide, et c'est démontré

Section Automatisations : **0 automatisation, 0 run.** L'onglet **Templates** contient exactement
deux entrées :

1. **« Workflow Santé et Business (copie) »** — le mot « (copie) » dans un template public est un
   résidu de développement, pas un modèle conçu pour l'utilisateur.
2. **« Nouvelle automatisation »** — un template vide.

Les deux affichent **0,0 étoile, 0 avis, 0 utilisation**, et un temps de mise en place estimé de
**30 minutes**.

**Le leader local a livré un moteur de règles générique et n'a aucune automatisation prête à
l'emploi.** C'est la démonstration factuelle de la réserve posée dans `Idee.md` : l'écran vide
d'un rule builder reste vide. Un commerçant à qui on demande 30 minutes de configuration ne
créera jamais sa première automatisation.

→ **C'est un angle d'attaque concret et immédiat pour ContexFly** : livrer 5-6 automatisations de
fidélisation pré-écrites, activables en un clic avec 2-3 paramètres, suffit à dépasser tout le
module d'automatisation de Fiitsa. Ça renforce la position de Felix sur Q6bis.

### 5. Réductions — les remises de fidélité ne sont pas couvertes

La section Réductions est un **gestionnaire de codes promo classique** (total / actives /
expirées). Rien qui déclenche sur un comportement d'achat.

→ **La remise automatique proposée en conversation au-delà d'un seuil de commandes — l'idée de
Maxime — n'existe pas chez Fiitsa.** C'est le point où son extension du volet fidélisation tient
le mieux face au concurrent local le plus sérieux.

### 6. Onboarding réel

Création du business en **3 étapes** : nom, description, numéro WhatsApp. Mais ce numéro n'est
qu'un **contact** — le tableau de bord affiche ensuite en permanence *« Aucun compte Meta
connecté »*, et la connexion Meta Business (WhatsApp + Pixels + comptes publicitaires) est une
étape **séparée et ultérieure**, dans Paramètres → Intégrations.

**Fiitsa a donc découplé « je crée ma boutique » de « je connecte WhatsApp ».** On peut utiliser
le produit sans jamais brancher l'API officielle — ce qui explique comment ils onboardent vite,
et suggère qu'une partie de leur base n'utilise pas WhatsApp du tout. Modèle intéressant à
reprendre : ne pas bloquer l'inscription sur la connexion Meta.

*(Bouton « Connecter Meta » non cliqué — flux OAuth sur le compte réel de Maxime.)*

### 7. La dispersion, mesurée

Barre latérale complète — **20 sections** en 7 groupes : Tableau de bord, Abonnement | Messagerie,
Formulaires, Automatisations | Ventes, Revenus, **Logistique** | Contacts, Prospects | Produits,
Collections, **Réservations** | Marketing, **Réseaux sociaux**, Réductions | **Agents IA**,
Calendriers, **Documents**, **Membres du personnel**, Gestionnaire de fichiers | Académie, Centre
d'aide, Suggestions, Paramètres.

Le Paramètres seul compte 10 onglets (Général, Apparence, Paiements, Fiscalité, Horaires,
Livraison, Notifications, Domaine, Intégrations, Règles).

**La thèse de dispersion est confirmée par la mesure, plus par la page marketing.** Et le prix
s'en ressent : le commerçant paie 49 990 FCFA pour 20 sections dont il en utilisera trois.

### 8. Défauts d'exécution relevés

- L'onglet **« Mes agents IA » est totalement vide** — pas de liste, pas d'état vide, pas de
  bouton. Écran blanc. La section **Réductions** est également blanche sous ses compteurs.
  Plusieurs écrans sont livrés **sans état vide**, alors que c'est exactement là que se joue
  l'adoption d'un outil pour commerçant peu technique.
- Le sélecteur de langue de l'interface affiche un **drapeau américain** sur un produit qui se
  revendique pour l'Afrique francophone.

→ À retenir pour `parcours-utilisateur` : les états vides ne sont pas un détail cosmétique ici,
c'est le principal levier d'activation. C'est un standard que le concurrent local ne tient pas.

---

## Flowcart (ex-Sukhiba) — vérification du 2026-08-15 (https://flowcart.ai/pricing et /in-chat-checkout)

Le rapport mondial le présente comme « un quasi-clone de ContexFly, déjà en Afrique ». Vérifié sur
les pages rendues : **fonctionnellement, c'est exact. Commercialement, il ne vise pas la même
population.**

### Ce qui est confirmé

- **Paliers :** Growth **69,99 $/mois**, Pro **139,99 $/mois**, Advanced **199,99 $/mois**.
- **Commission dégressive sur le CA WhatsApp :** gratuit jusqu'à 3 000 / 5 000 / 10 000 $ de CA
  mensuel selon le palier, puis **1,5 % / 1 % / 0,5 %** au-delà. Slogan affiché : « No growth tax ».
- **Fonctionnalités :** *One Click In-Chat Checkout* sur les trois paliers, agents IA de vente
  entraînés sur mesure, relances de panier abandonné, notifications de commande, upsell
  post-achat, campagnes illimitées, inbox multi-agents, recherche conversationnelle dans le
  catalogue, et « Buy for Customer — Build & send carts on WhatsApp ».
- **SOC 2 Type II**, « Trusted by 300+ companies » sur la page tarifs, « 500+ Global Ecommerce
  Brands » sur la page checkout (les deux chiffres ne concordent pas).
- Numéro de contact WhatsApp en **+254 (Kenya)**. Témoignages clients kényans et indiens.

### Ce qui l'exclut du terrain de ContexFly — trois faits, pas une opinion

1. **Sélecteur de devises : USD, INR, KES, NGN, ZAR.** Pas de XAF, pas de FCFA, aucune devise
   d'Afrique francophone. Leur Afrique, c'est le Kenya, le Nigeria et l'Afrique du Sud.
2. **Le seul chemin d'inscription en libre-service affiché est « Install on Shopify ».** Les deux
   boutons d'appel à l'action de tout le site sont « Install on Shopify » et « Request a Demo ».
   Un commerçant de Douala sans boutique Shopify n'a aucun moyen de s'inscrire seul.
3. **Le prix d'entrée est 69,99 $/mois, soit environ 42 000 FCFA** — hors du marché local observé
   (0 à 20 000 FCFA/mois). Et le discours cible explicitement des marques (« For brands building a
   WhatsApp experience that matches their identity »), pas des commerçants individuels.

### Non vérifié

- **Le mobile money.** Aucune page ouverte ne nomme de moyen de paiement — ni M-Pesa, ni carte,
  ni passerelle. Vu la clientèle kényane et le checkout in-chat, le support de M-Pesa est
  plausible, **mais je ne l'ai pas vu écrit et je ne l'affirme pas.**
- Les statistiques de performance affichées (« 22–27 % de paniers récupérés », « +40 % de
  ventes ») sont des témoignages sans méthodologie — à ne pas reprendre comme données de marché.

### Lecture pour ContexFly

Flowcart prouve que le produit est **techniquement faisable et commercialement viable** — c'est
rassurant. Mais il valide aussi le constat du rapport mondial : **le secteur suppose que le
marchand a déjà une boutique en ligne.** Flowcart est une couche d'optimisation de conversion
posée sur un Shopify existant. ContexFly s'adresse à un commerçant **dont WhatsApp est la seule
boutique**. Ce n'est pas le même produit malgré des fonctionnalités qui se ressemblent.

Risque à ne pas minimiser : rien n'empêche Flowcart de descendre en gamme et d'ajouter le XAF.
Ils ont levé des fonds et sont en expansion. Ce n'est pas un concurrent aujourd'hui ; c'en est un
candidat crédible à 12-24 mois. → à reprendre dans `La-Verite-Difficile.md`.

---

## App WhatsApp Business gratuite — catalogue et panier (vérification du 2026-08-15)

**Confirmé : le panier est une fonctionnalité native et gratuite de l'app WhatsApp Business.**
Le client ajoute des articles du catalogue à un panier (ajout, suppression, modification des
quantités), puis **envoie son panier sous forme de message** au commerçant. Le commerçant
l'active dans Réglages → Outils professionnels → Catalogue → Plus → Réglages → « Afficher Ajouter
au panier ». Source : pages d'aide officielles WhatsApp.

### Conséquence directe pour le positionnement de ContexFly

⚠️ **« Le client construit un panier » n'est pas un argument de vente.** C'est gratuit et déjà
là. Un commerçant informé répondra « je l'ai déjà ».

Mais le mur est net, et c'est là qu'est la valeur : **le panier WhatsApp est un message, pas une
commande.** Une fois le panier envoyé, plus rien n'est automatisé — le commerçant doit lire,
recalculer, confirmer, réclamer le paiement, vérifier la capture d'écran MoMo, et noter la
commande quelque part. Il n'y a ni total validé, ni paiement, ni enregistrement de commande, ni
relance, ni historique exploitable.

**L'argument de ContexFly n'est donc pas le panier — c'est tout ce qui vient après le panier**, et
le fait que ça se passe sans le commerçant. À reprendre tel quel dans `positionnement-marketing`.
