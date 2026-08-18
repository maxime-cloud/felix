# Fonctionnalités — ContexFly

Statuts : `proposée` / `validée` / `rejetée` / `à ajuster`. Une fonctionnalité rejetée n'est
jamais supprimée — elle reste avec sa raison, pour ne pas être re-proposée par erreur.

Sources : `Idee.md` (vision de Maxime), `Benchmark-Concurrents.md` + `_verifications-felix.md`
(l'existant, vérifié), `Positionnement.md` (l'angle retenu).

Effort : **S** = heures à 1 jour · **M** = plusieurs jours · **L** = 1 semaine+ ou risque
technique réel. Estimé pour un développeur solo déléguant à un agent IA sur `ai-builder-saas`.

---

## Carte des domaines

| # | Domaine | Candidates | État |
|---|---|---|---|
| A | Cœur de métier — agent vendeur & conversation | 14 | **validé** (A6, A8, A13, A14 tranchés) |
| B | Catalogue produits | 5 | **posé**, B0 arbitré |
| C | Commandes & livraison | 6 | **en validation** (C3, C4 validées) |
| D | Paiement & argent | 8 | **en validation** (D2 validée) |
| E | Boîte de réception | 6 | **en validation** |
| F | Fidélisation & sortant | 7 | **en validation** |
| G | **Structure du compte, utilisateurs & rôles** | 3 | **en validation** (G1, G2 arbitrés) |
| H | Onboarding | 6 | **en validation** |
| I | Reporting | 3 | **en validation** |
| J | Back-office ContexFly | 2 | **en validation** |
| K | Socle SaaS (couvert par `ai-builder-saas`) | — | pour mémoire |
| L | **Croissance — parrainage & réductions plateforme** | 6 | **validé** |
| P | **Passe proactive de Felix** | 4 | **validé** |

Les domaines E, H et I ont été enrichis par l'exploration concurrentielle du 17/08 — voir
`Reference-Conception-Agent.md`, qui sert de brief de conception pour A4, B0 et E.

---

# Domaine A — Cœur de métier : l'agent vendeur et la conversation

## A1 — Agent IA conversationnel de prise de commande

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **L**

**Description.** Un agent conversationnel qui, sur WhatsApp, comprend une demande en langage
naturel, identifie les produits dans le catalogue du commerçant, demande les quantités
manquantes, propose des alternatives en cas de rupture, récapitule la commande et conduit le
client jusqu'au paiement — sans intervention du commerçant.

**Rôles.** Client final (interlocuteur) · Gérant (configure) · Vendeur (peut reprendre).

**Analyse commerciale.** C'est le produit. Sans elle, ContexFly est une inbox de plus, et
`Positionnement.md` dit exactement contre quoi une inbox seule doit lutter (Waazi, 25 000 FCFA
par agent). Levier de **différenciation** vérifié et non théorique : l'agent de Fiitsa a « Prendre
des commandes » **désactivé par défaut**, son libellé interne dit *« Guider vers l'achat »*, et
son état vide parle de *« collecter des leads »* — leur produit est cadré comme un assistant de
site web. Aucun acteur local dans la bande 0–20 000 FCFA ne fait la prise de commande
conversationnelle. Levier de **monétisation** : c'est la fonctionnalité qui justifie l'abonnement
face à l'app WhatsApp Business gratuite.

**Utilité.** Résout les problèmes 1, 2, 4 et 5 de `Positionnement.md` — messages non répondus la
nuit et le dimanche, plafond humain, commande reconstituée de mémoire, total recalculé à la main.
Fréquence : **permanente**, c'est le flux principal du produit.

**Piste d'approfondissement.** Deux, dans l'ordre de valeur : (1) **la vente additionnelle
contextuelle** — proposer un produit complémentaire au moment du récapitulatif, ce qui augmente le
panier moyen sans effort du commerçant ; (2) **la mémoire inter-conversations**, déjà dans la
vision de Maxime (l'historique des conversations complétées sert de contexte). Les deux sont
reportables après le MVP.

**Source.** Vision de Maxime · segment vérifié au benchmark (Flowcart le fait mondialement,
Fiitsa partiellement, personne localement dans la bande de prix).

⚠️ **Effort L et risque réel.** C'est la fonctionnalité la plus coûteuse et la plus incertaine du
projet, et elle est aussi le cœur. Le coût d'inférence par conversation n'est pas modélisé (Q13)
et peut invalider le modèle tarifaire. **À traiter en premier, pas en dernier.**

---

## A2 — Panier construit au fil de la conversation

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Un panier persistant rattaché à la conversation, que l'agent alimente ligne par
ligne au fil des échanges (produit, quantité, prix unitaire, total courant), consultable et
modifiable à tout moment.

**Rôles.** Client final · Agent IA · Vendeur (peut corriger).

**Analyse commerciale.** ⚠️ **Attention — ce n'est PAS un différenciateur, et `Positionnement.md`
l'interdit explicitement comme argument de vente** : l'app WhatsApp Business a un panier natif et
gratuit. La valeur ici est technique, pas commerciale : c'est l'objet qui rend possible A3, D1 et
C1. **À ne jamais mettre en avant dans le discours commercial** — un commerçant informé répondra
« je l'ai déjà ».

**Utilité.** Support de tout le reste. Fréquence : à chaque commande.

**Piste d'approfondissement.** Le panier persiste-t-il si le client revient trois jours plus
tard ? Recommandé oui, et c'est peu coûteux — ça alimente directement la relance (A8).

**Source.** Vision de Maxime · le panier natif WhatsApp est vérifié comme concurrent gratuit.

---

## A3 — Page panier éditable puis paiement

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Un lien envoyé dans la conversation ouvre une page web récapitulative : le client
ajuste les quantités, supprime des lignes, choisit son mode de livraison, puis paie. Aucune
inscription, aucun mot de passe.

**Rôles.** Client final (seul utilisateur de cet écran).

**Analyse commerciale.** Levier de **conversion** plus que de différenciation. Le vrai argument
n'est pas la page en soi mais **ce qu'elle permet : un total ferme et un paiement traçable**, là
où le flux actuel s'arrête à une capture d'écran de transfert. C'est le maillon qui transforme une
conversation en revenu, et c'est ce que `Positionnement.md` désigne comme « la fin de la chaîne ».

**Utilité.** Résout les problèmes 5, 7 et 8 — total recalculé à la main, preuve de paiement
falsifiable, réconciliation impossible. Fréquence : à chaque commande payée en ligne.

**Piste d'approfondissement.** ⚠️ **Contrainte locale forte à traiter dès la conception, pas
après** : connexion instable et usage mobile-first. Cette page doit être légère, tolérante à une
coupure, et le lien doit rester valide et rouvrable. `Positionnement.md` identifie le mode dégradé
comme un vide que personne ne remplit — c'est peu coûteux ici et ça se remarque.

**Source.** Vision de Maxime · Fiitsa a un « checkout intégrable » comparable (vérifié).

---

## A4 — Configuration de l'agent par le commerçant

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** L'écran où le gérant définit le comportement de son agent : nom, ton, langue,
message d'accueil, ce qu'il a le droit de faire, ce qu'il ne doit pas faire, et les garde-fous
chiffrés (plafond de remise, comportement en rupture de stock).

**Rôles.** Gérant.

**Analyse commerciale.** Levier de **rétention** : un agent configuré aux mots du commerçant
devient difficile à remplacer. Et c'est un point d'attaque direct — chez Fiitsa, la configuration
tient en 4 préréglages de personnalité et 5 interrupteurs, sans aucune règle métier (vérifié).
⚠️ **Mais `Positionnement.md` avertit** : la profondeur de configuration ne doit pas devenir un
écran vide que personne ne remplit. Le bon design est **une configuration par défaut qui marche
tout de suite**, enrichissable ensuite.

**Utilité.** Sans elle, l'agent parle comme un robot générique et le commerçant ne lui fait pas
confiance. Fréquence : **une fois à l'installation, puis rarement** — ce qui justifie de la garder
courte.

**Piste d'approfondissement.** Un **bac à sable de test** (comme le « Tester » de Fiitsa) pour que
le commerçant essaie son agent avant de le mettre en ligne. Valeur élevée pour la confiance, effort
faible. À noter : chez Fiitsa ce testeur **ne fonctionnait pas** au moment du test — deux messages,
deux erreurs `Failed to send a request to the Edge Function`. Faire marcher le sien est un
différenciateur d'exécution gratuit.

**Source.** Vision de Maxime · Fiitsa (structure observée, faiblesses vérifiées).

---

## A5 — Accès de l'agent au catalogue, aux prix et au stock

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** L'agent interroge en temps réel le catalogue du commerçant : existence du
produit, prix, disponibilité. Il ne vend pas ce qui n'existe pas et ne vend pas ce qui est épuisé.

**Rôles.** Agent IA (consommateur) · Gérant (propriétaire de la donnée).

**Analyse commerciale.** Prérequis de crédibilité plus que différenciateur — **mais avec un angle
d'attaque vérifié** : chez Fiitsa, l'accès au **stock est désactivé par défaut**, ce qui autorise
leur agent à vendre un article épuisé. Sur une boutique camerounaise, vendre ce qu'on n'a pas
détruit la confiance plus vite que tout le reste. **Activer le stock par défaut est un choix
produit à assumer et à revendiquer.**

**Utilité.** Résout le problème 6 (vente en rupture). Fréquence : à chaque conversation.

**Piste d'approfondissement.** Que fait l'agent en rupture ? Proposer une alternative du catalogue
plutôt que de dire non — ça sauve la vente. Effort faible une fois A1 en place.

**Source.** Benchmark (Fiitsa, défaut observé et vérifié) · standard du secteur.

---

## A6 — Bascule IA ↔ humain par contact

**Statut : ✅ VALIDÉE (Maxime, 2026-08-16)** · Priorité : **Must** · Effort : **M**
**Paramètre tranché :** retour à l'IA **automatique, avec délai configurable** par le commerçant.

**Description.** Sur une conversation donnée, le commerçant reprend la main : l'agent se tait,
l'humain répond. Et inversement, il rend la main à l'agent quand il veut.

**Rôles.** Gérant · Vendeur.

**Analyse commerciale.** ⚠️ **Prérequis, pas différenciateur** — `Positionnement.md` le classe
explicitement parmi les six choses à ne jamais vendre comme un atout. Sa vraie fonction est
**assurantielle** : c'est ce qui permet à un commerçant d'accepter de laisser une IA parler à ses
clients. Sans filet, il ne l'activera jamais. Levier d'**acquisition** à ce titre, pas de
différenciation.

**Utilité.** Résout la peur, pas une tâche. Fréquence : occasionnelle, mais décisive au démarrage.

**Piste d'approfondissement.** Deux points à trancher qui comptent plus que la fonctionnalité
elle-même : **la bascule automatique** (l'agent se retire de lui-même quand il ne comprend pas ou
quand le client s'énerve) et le **retour à l'IA** — automatique après N heures, ou manuel ? Le
manuel produit des conversations orphelines quand le commerçant oublie.

**Source.** Vision de Maxime · Fiitsa (« Transférer à un humain », activé par défaut) · Waazi.

---

## A7 — Cycle de vie des conversations et historique comme contexte

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Une conversation naît quand un client écrit, porte un statut (active, complétée,
abandonnée…), et passe à complétée quand la commande aboutit. Si le client réécrit plus tard, une
nouvelle conversation démarre — et l'historique des précédentes sert de contexte à l'agent.

**Rôles.** Agent IA · Gérant · Vendeur.

**Analyse commerciale.** Fondation de F1 et F4 — sans historique structuré, **la fidélisation
pilotée par la donnée d'achat est impossible**, or c'est le différenciateur n°2 de
`Positionnement.md`. Rappel du fait vérifié : l'agent de Fiitsa **n'a aucun accès à l'historique
de commandes**, et ce n'est pas branchable sur leur architecture. C'est ici que l'écart se creuse.

**Utilité.** Résout les problèmes 10 et 12 — aucune trace exploitable des clients, impossible de
savoir qu'un client en est à sa troisième commande. Fréquence : continue, en arrière-plan.

**Piste d'approfondissement.** ⚠️ **Attention à un piège de conception.** « L'historique sert de
contexte » ne peut pas vouloir dire « on injecte toutes les conversations passées dans le prompt » :
le coût d'inférence explose (Q13) et la qualité se dégrade. Il faut un **résumé structuré par
client** — produits achetés, fréquence, panier moyen, préférences — pas un dump de transcriptions.
C'est une décision d'architecture à prendre maintenant, pas au moment de coder.

**Source.** Vision de Maxime (décision 3 du brief initial) · Chatwoot cité comme référence.

---

## A8 — Relance automatique des conversations non abouties

**Statut : ✅ VALIDÉE (Maxime, 2026-08-16)** · Priorité : **Should** · Effort : **M**
**Paramètres tranchés : deux relances — à 3 h (gratuite, dans la fenêtre de service) et à 48 h
(template Meta pré-approuvé, payante).** Le document de recherche de Maxime précise le mécanisme :
un workflow n8n s'exécute à intervalle rapproché (~1 min) pour détecter les conversations restées
`active` et décider s'il faut relancer.
⚠️ La relance à 48 h est de catégorie **Marketing** ou **Utility** selon son contenu — une relance
de panier formulée comme un rappel de commande peut passer en Utility (moins chère, hors plafond
marketing). **Ce choix de catégorie a un impact direct sur le coût et sur le plafond de fréquence.**
À trancher à `architecture-integrations`.

**Description.** Une conversation restée active sans commande depuis N heures déclenche un message
de relance automatique.

**Rôles.** Agent IA · Gérant (règle et délai).

**Analyse commerciale.** Levier de **revenu direct et mesurable** — c'est la fonctionnalité dont le
retour sur investissement se démontre le plus facilement à un commerçant (« X commandes récupérées
ce mois-ci »), donc un excellent argument de rétention d'abonnement. Standard du secteur mondial
(relance de panier abandonné présente chez la majorité du panel), absente localement dans la bande
de prix.

**Utilité.** Résout le problème 3 (panier abandonné, personne ne relance). Fréquence : quotidienne
en arrière-plan.

**Piste d'approfondissement.** ⚠️ **Contrainte de conformité à intégrer dès le départ.** Passé la
fenêtre de service de 24 h, une relance **doit** passer par un template Meta pré-approuvé et
devient **payante**. Une relance à 48 h n'est donc pas le même objet technique ni économique
qu'une relance à 3 h. À trancher : combien de relances au maximum, et à quel moment on bascule sur
un template payant.

**Source.** Vision de Maxime · standard du panel mondial.

---

## A9 — Escalade automatique vers un humain

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

**Description.** L'agent se retire et alerte le commerçant de lui-même sur signal : incompréhension
répétée, mécontentement, demande hors périmètre, ou montant inhabituel.

**Rôles.** Agent IA · Gérant (notifié).

**Analyse commerciale.** Levier de **rétention** et de réduction du risque : c'est ce qui évite la
conversation catastrophique qui fait désinstaller le produit. Peu visible commercialement, mais son
absence se paie cher. Effort **S** une fois A6 en place — bon rapport impact/effort.

**Utilité.** Occasionnelle mais critique quand elle se déclenche.

**Piste d'approfondissement.** Le déclencheur « montant inhabituel » recoupe le garde-fou D5
(plafond de remise). À traiter ensemble.

**Source.** Felix, à partir du garde-fou CLAUDE.md sur les fonctionnalités touchant à l'argent.

---

## A10 — Notes vocales entrantes

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Could** · Effort : **M**

Un client envoie un vocal ; l'agent le transcrit et le traite comme un message. `Positionnement.md`
identifie les notes vocales comme un vide d'adaptation que personne ne remplit sur ce marché, et
l'usage du vocal est courant localement. Reportable après le MVP, mais c'est un candidat sérieux
au coup d'éclat une fois le socle en place.

---

## A11 — Bilinguisme FR/EN et tolérance au pidgin

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

**Description.** L'agent détecte la langue du client et répond dans la même — français, anglais, et
tolérance au mélange français/pidgin courant au Cameroun.

**Rôles.** Agent IA · Client final.

**Analyse commerciale.** Levier d'**acquisition** sur le marché camerounais, officiellement
bilingue, et prérequis pour l'extension régionale. Coût faible : c'est une affaire de prompt et de
détection, pas de développement lourd. `Positionnement.md` classe le pidgin parmi les vides
d'adaptation non remplis. ⚠️ Honnêteté : **je n'ai pas vérifié** comment les concurrents locaux se
comportent face à du pidgin — c'est une hypothèse de valeur, pas un fait établi.

**Utilité.** Continue, sur la zone anglophone et les échanges mixtes.

**Piste d'approfondissement.** L'interface du SaaS elle-même en FR/EN — déjà couvert par Paraglide
JS dans `ai-builder-saas`, donc quasi gratuit.

**Source.** Contrainte de marché (`Idee.md`) · `Positionnement.md`.

---

## A12 — Garde-fou de conformité : l'agent est verrouillé sur sa mission métier

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **S**

**Description.** Le commerçant ne peut pas transformer son agent en assistant généraliste. La
configuration (A4) n'expose pas de champ de prompt libre et sans limite : elle encadre le
périmètre — vendre, renseigner sur les produits, prendre la commande, orienter — et l'agent refuse
poliment de sortir de ce cadre.

**Rôles.** Agent IA · Gérant (subit la contrainte) · ContexFly (porte le risque).

**Analyse commerciale.** ⚠️ **Ce n'est pas un choix de conception, c'est une obligation
réglementaire — vérifié.** Meta interdit les **chatbots IA généralistes** sur la WhatsApp Business
Platform : règle appliquée depuis le **15 octobre 2025** pour les nouveaux comptes API et étendue
à tous au **15 janvier 2026**. Est visé un bot adossé à un LLM qui traite des conversations
ouvertes sur n'importe quel sujet sans être restreint à un processus métier. Sont **explicitement
autorisés et encouragés** les agents au service d'une tâche métier : service client, prise de
commande, suivi, prise de rendez-vous.

**Et c'est un cadeau de positionnement.** ContexFly est, par construction, exactement ce que Meta
autorise. À l'inverse, un produit qui vend « une IA généraliste sur WhatsApp » est désormais hors
des clous. À noter dans le dossier concurrentiel : Fiitsa commercialise **« Leslie, ta patronne IA
qui orchestre les 7 autres agents »**, accessible **« depuis ton WhatsApp personnel »** pour gérer
son business — c'est la définition même de ce que Meta a interdit. *(Constat sur la base de leur
page tarifs ; je n'ai pas testé le comportement réel de Leslie.)*

**Utilité.** Protège le numéro du commerçant et le statut Tech Provider de ContexFly. Fréquence :
permanente, en arrière-plan.

**Piste d'approfondissement.** En faire un **argument commercial explicite** : « conforme à la
politique Meta 2026 » sur la page tarifs. C'est vrai, vérifiable, et opposable.

**Source.** Document de recherche de Maxime (§2.1) — **vérifié par Felix le 2026-08-16.**

## A13 — Horaires connus de l'agent : ouverture ET livraison

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **S**

**Description.** Deux jeux d'horaires distincts, et c'est la distinction qui compte :
- **horaires d'ouverture** — quand le commerçant est joignable et prépare les commandes ;
- **horaires et jours de livraison** — quand il livre réellement.

L'agent doit connaître les seconds pour répondre au client qui veut être livré la nuit, un
dimanche, ou un jour où le commerçant ne livre pas. **Trois comportements à configurer**, au choix
du commerçant, par cas : refuser et proposer le prochain créneau disponible · accepter en
signalant le délai réel · **remonter la demande au commerçant** plutôt que de trancher seul.

**Rôles.** Gérant (déclare) · Agent IA (applique) · Client final.

**Analyse commerciale.** Zoko a des « Business Hours » ; **personne n'a d'horaires de livraison
séparés**. Or c'est la question qui revient le plus après le prix et la disponibilité — et c'est
exactement le genre de détail où un agent qui répond mal coûte une vente **et** de la confiance.
Un agent qui promet une livraison dimanche alors que le commerçant ne livre pas dimanche produit
un litige, pas une commande. Effort **S** pour un gain direct sur le taux d'autonomie.

**Utilité.** Sollicité sur une grande partie des conversations de livraison.

**Piste d'approfondissement.** ⭐ **L'agent doit demander ces horaires lui-même** pendant la
configuration, plutôt que de les attendre d'un formulaire — c'est le même mécanisme que B0
appliqué au paramétrage. Et le troisième comportement (« remonter au commerçant ») est le plus
sûr par défaut : mieux vaut une escalade qu'une promesse fausse.

**Source.** Maxime · manque identifié chez Zoko (Business Hours sans volet livraison).

## A14 — Mode absence imprévue

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

**Description.** Un interrupteur qui déclare une **fermeture non planifiée** (boutique fermée,
imprévu, voyage), assorti d'une **consigne en texte libre** que le commerçant dicte à l'agent :
quoi répondre, et quoi faire des commandes pendant ce temps — refuser, enregistrer sans promettre
de date, ou proposer une reprise à telle date.

**Analyse commerciale.** **C'est le pendant indispensable de A13.** Les horaires couvrent le
prévisible ; l'imprévu est le cas où l'agent est le plus dangereux, parce qu'il continue à vendre
et à promettre pendant que personne ne prépare les commandes. Zoko a des « Away Messages », mais
c'est un message d'absence statique — pas une consigne qui change le **comportement de vente** de
l'agent. Différence réelle, effort **S**.

**Utilité.** Ponctuelle mais critique. Fréquence faible, coût de l'absence très élevé.

✅ **Activation depuis WhatsApp — VALIDÉE (Maxime, 2026-08-17).** Le commerçant active son mode
absence **en écrivant à son propre agent depuis WhatsApp**, sans ouvrir l'application. C'est
précisément dans ces moments-là qu'il n'est pas devant un ordinateur.

⚠️ **Conséquence de conception non triviale : l'agent doit distinguer son propriétaire de ses
clients** sur le même numéro, et basculer en mode « commande du patron » plutôt qu'en mode vente.
Cela crée un second registre de conversation à sécuriser — le numéro du gérant doit être vérifié,
sinon n'importe qui pouvant usurper un numéro ferme la boutique. → à porter en exigence
non-fonctionnelle. L'effort passe de **S** à **M** de ce fait.
Cohérent avec la cible mobile-first (rappel : Ayweu, 3 000+ vendeurs, est mobile-only).

**Source.** Maxime · à rapprocher des « Welcome & Away Messages » de Zoko, en plus riche.

---

# Domaine B — Catalogue produits

## B0 — Enregistrement de produit assisté par agent, avec mémoire de champs apprise ⭐

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **L**
**Source : idée originale de Maxime.**

⚠️ **Correction du 2026-08-16, après exploration de Wazzap.ai.** Ma première formulation — « aucun
équivalent identifié dans le benchmark » — était trop forte. **Wazzap fait de la configuration
conversationnelle adaptative au secteur**, avec des suggestions cliquables générées d'abord depuis
le métier déclaré, puis **depuis les réponses précédentes de l'utilisateur**. Leurs propositions
incluaient littéralement « Tailles / couleurs ».

**B0 reste distinct, mais la frontière doit être décrite honnêtement :**

| | Wazzap | B0 |
|---|---|---|
| Objet configuré | la **FAQ et le comportement** de l'agent | le **modèle de données produit** |
| Adaptation | au secteur déclaré | au **type de produit**, produit par produit |
| Mémoire | dans la session d'onboarding | **persistante, par catégorie et par commerçant**, enrichie à chaque ajout |
| Attributs structurés | ❌ aucun | ✅ pointure, couleur, variante |

**Vérifié :** à « je vends des chaussures et des sacs », leur agent a répondu *« envoie-moi 2-3
photos, je vais les ajouter avec une description et un prix »* — **sans jamais demander les
pointures ni les couleurs**, alors qu'il savait qu'il s'agissait de chaussures. Ils génèrent du
texte depuis une photo ; ils ne construisent pas de modèle d'attributs.

→ **Le différenciateur se formule mieux ainsi : ils configurent ce que l'agent *dit*, B0 configure
ce que l'agent *sait*.** Corollaire : le pré-remplissage par photo, listé plus bas en piste
d'approfondissement, n'est pas un « bonus pour plus tard » — c'est un standard en train de
s'installer.

✅ **Arbitrages de Maxime (2026-08-17) :**
- **B0 couvre les deux** — ce que l'agent *dit* (FAQ, ton, comportement) **et** ce qu'il *sait*
  (attributs produits structurés). Le périmètre de B0 s'élargit donc à la configuration du
  discours de l'agent, pas seulement à celle du modèle de données.
- **Le pré-remplissage par photo entre dans le MVP** — ce n'est plus une piste d'approfondissement.
  L'effort **L** est confirmé, voire tendu : il ajoute une brique de vision par ordinateur à une
  fonctionnalité qui en contenait déjà deux (agent de saisie + mémoire apprenante).

🎯 **Confirmation externe de la prémisse (Zoko, 2026-08-17).** Le scénario que Zoko met en
vitrine dans son compte de démonstration est : *« Do you have the blue running shoes in size 9? »*
→ *« Yes, the blue runners are in stock in size 9 »* → carte produit « Blue Runner - Size 9 » →
commande. **La question canonique du commerce sur WhatsApp est une question de variante.** C'est
l'argument le plus concret en faveur de B0 rencontré jusqu'ici — et exactement ce à quoi l'agent
de Fiitsa ne peut pas répondre.

**Description.** L'enregistrement d'un produit se fait en deux temps.
1. **Champs génériques** communs à tous les produits : nom, prix, photo, catégorie, stock.
2. **Bouton « Suivant » → un agent conversationnel s'ouvre** et pose des questions *précises et
   propres au type de produit* : pointure et couleurs disponibles pour une chaussure, composition
   et allergènes pour un plat, contenance pour un cosmétique. **Uniquement ce qui servira à
   répondre à un client** — pas une fiche technique exhaustive. L'agent termine en demandant si le
   commerçant a d'autres détails à ajouter pour ce produit.

**La mémoire, qui est le vrai sujet.** Une base de **modèles de champs par type d'activité** est
pré-remplie côté ContexFly. Dès qu'un commerçant décrit son activité à l'inscription, l'agent
instancie **son** jeu de modèles. Ensuite, **la mémoire apprend** : si le commerçant ajoute
spontanément un détail à la fin du questionnaire, l'agent met à jour le modèle **de cette catégorie
et pour ce commerçant** — et à l'enregistrement suivant, la question est posée d'office.

**Rôles.** Gérant (renseigne) · Agent de catalogue (interroge et apprend) · Agent vendeur
(consomme la donnée produite).

**Analyse commerciale.** **Différenciation forte, et à un endroit inattendu.** Je n'ai identifié
aucun équivalent dans le benchmark, ni local ni mondial : partout ailleurs, l'ajout de produit est
un formulaire figé. Trois leviers :
- **Acquisition.** Le catalogue vide est le point de mortalité n°1 de ce type de produit — un
  commerçant qui doit remplir 40 fiches à la main abandonne avant la première vente. Une saisie
  conversationnelle, en français, sur mobile, abaisse cette marche. C'est directement l'objectif
  mesurable n°3 de `Idee.md` : le délai inscription → première commande encaissée.
- **Rétention par accumulation.** Chaque produit enregistré enrichit la mémoire du commerçant.
  Plus il utilise ContexFly, plus la saisie devient rapide et plus le départ coûte cher. C'est
  exactement le seul avantage que `Positionnement.md` identifie comme grandissant avec le temps.
- **Qualité de l'agent vendeur.** C'est le point que je trouve le plus fort : **cette
  fonctionnalité est ce qui rend A1 réellement bon.** Un agent vendeur ne vaut que ce que vaut la
  donnée produit derrière lui. Aujourd'hui, quand un client demande « vous l'avez en 42 ? », un
  agent alimenté par un catalogue nom/prix/photo doit escalader vers un humain. Ici, il répond.
  **Le gain se mesure directement sur le taux d'autonomie**, la métrique n°1 du projet.

**Utilité.** Résout un problème que je n'avais pas inventorié dans `Positionnement.md` et qu'il
faut y ajouter : *le service client est sollicité pour des détails produits que l'agent ne connaît
pas.* Fréquence : intense à l'installation, puis à chaque nouveau produit.

**Piste d'approfondissement.**
- **Boucle de retour depuis les conversations réelles** — si l'agent vendeur bute trois fois sur
  « quelles couleurs ? » pour une catégorie, il propose au commerçant d'ajouter ce champ au
  modèle. La mémoire n'apprend plus seulement de la saisie, mais des vraies questions des clients.
  C'est la version aboutie de l'idée, et elle est spectaculaire — **mais hors MVP**.
- Pré-remplissage à partir d'une photo du produit.

⚠️ **Trois réserves à traiter avant de coder.**
1. **Effort L, pas M.** Il y a deux agents distincts (catalogue et vente), un schéma de données à
   attributs dynamiques, et une logique d'apprentissage. Ce n'est pas un formulaire.
2. **Le modèle de données doit être pensé pour ça dès le départ** : attributs variables par
   catégorie, valeurs multiples (tailles, couleurs), et stock potentiellement par variante. Une
   table `produit` à colonnes fixes rend la fonctionnalité impossible. **À porter en priorité au
   skill `donnees-et-roles`.**
3. **Coût d'inférence.** Chaque enregistrement de produit devient un échange avec un LLM. Sur un
   commerçant qui charge 50 produits le premier jour, ça compte — et ça s'ajoute au coût des
   conversations de vente déjà non modélisé (Q13).
4. **🔴 Risque de corruption silencieuse du catalogue.** Observé en conditions réelles chez
   Wazzap : à la question « comment veux-tu appeler ton agent ? », la réponse « Vendeuse IA » a été
   enregistrée comme **une prestation vendue par le commerçant**, puis réutilisée comme telle au
   tour suivant. L'agent avait perdu le fil de ce qu'il collectait. **Un agent de saisie
   conversationnelle qui se trompe de contexte écrit de fausses données dans le catalogue, sans
   que le commerçant s'en aperçoive.** → exigence non-fonctionnelle : confirmation explicite avant
   toute écriture en base, et annulation possible.

## B1 — CRUD produits, collections et catégories

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Must** (produits) / **Could** (collections) · Effort : **S**
Fonctionnalités évidentes, groupées : créer, modifier, désactiver, dupliquer un produit ; le
ranger dans une catégorie. Aucun enjeu de décision — le socle `ai-builder-saas` couvre l'essentiel.
Prérequis de B0 (les champs génériques) et de A5.

## B2 — Stock et décrément à la commande

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**
Voir A5 : l'accès au stock est activé par défaut, contrairement à Fiitsa. À trancher :
décrément à la commande ou au paiement, et gestion du stock **par variante** (une chaussure en 42
peut être épuisée alors que le 43 est disponible) — ce qui découle directement de B0.

## B3 — Synchronisation avec le catalogue WhatsApp natif

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**
Pousser le catalogue ContexFly vers le catalogue WhatsApp de Meta, pour que le client puisse
parcourir les produits dans l'interface native. Vérifié : Fiitsa le fait (leur bundle charge
`useWhatsAppCatalog`). Intérêt réel — c'est l'expérience que les clients connaissent déjà — mais
c'est un **alignement**, pas une différenciation.

## B4 — Import en masse de produits

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Could** · Effort : **M**
Import CSV ou depuis une liste existante. Utile pour un commerçant qui a déjà un fichier, mais la
cible (boutique informelle) en a rarement un — B0 traite mieux le cas réel.

---

---

# Domaine C — Commandes & livraison

## C1 — Objet Commande, distinct de la conversation

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Une commande est une entité propre : lignes (produit, variante, quantité, prix
unitaire), total, politique de paiement appliquée, montant payé, reste dû, statut, adresse de
livraison, conversation d'origine. Elle survit à la conversation qui l'a créée.

**Rôles.** Gérant · Vendeur · Agent IA (crée et modifie) · Client final (indirect).

**Analyse commerciale.** **Ce n'est pas une fonctionnalité, c'est le socle de la promesse.** Le
benchmark le montre par l'absence : **Zoko n'a aucune section « commandes »** — elles vivent dans
Shopify, et c'est pour ça que Zoko exige Shopify. L'app WhatsApp Business, elle, produit un panier
qui est **un message, pas une commande** : rien n'est réconciliable, rien n'est relançable, rien
n'est mesurable. Ngavix a des commandes mais pas de conversation. **ContexFly est le seul point du
marché local où la conversation produit un objet Commande** — c'est littéralement la revendication
retenue dans `Positionnement.md`.
Sans C1, il n'y a ni A8 (relance), ni F (fidélisation par historique d'achat), ni I (reporting),
ni le taux d'autonomie. **Tout en dépend.**

**Utilité.** Résout les problèmes 4, 5, 8 et 12 de `Positionnement.md` : commande reconstituée de
mémoire, total recalculé à la main, réconciliation, et mémoire client inexistante.
Fréquence : à chaque vente.

**Piste d'approfondissement.** Modification d'une commande **après** validation (le client rappelle
pour ajouter un article) — fréquent en vente informelle, et cela impose de savoir rejouer un
paiement partiel. **Hors MVP**, mais le modèle de données doit le permettre.

**Source.** Idée structurante déduite du benchmark (absence chez Zoko, incomplétude chez Ngavix).

## C2 — Statuts de commande

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **S**

**Description.** Cycle : `en attente → confirmée → expédiée → livrée`, plus `annulée`. C'est le
modèle exact relevé chez Ngavix, et il est bon — inutile d'en inventer un autre.

**Analyse commerciale.** Aucune différenciation : c'est un **prérequis mécanique** des choix de
paiement déjà validés. Sans statut « livrée », on ne peut pas boucler l'encaissement en paiement à
la livraison ni solder un acompte. Effort S pour débloquer tout le domaine D.

**Utilité.** Permanente. **Piste :** notification WhatsApp automatique à chaque changement de
statut — Ngavix le fait, et c'est un template `utility`, donc **gratuit dans la fenêtre de service**.
Bon rapport valeur/effort, à évaluer pour le MVP.

**Source.** Ngavix (vérifié) · conséquence mécanique de D2/D3.

## C3 — Export de la fiche livreur

**Statut : ✅ VALIDÉE (Maxime, 2026-08-16)** · Priorité : **Should** · Effort : **S**

**Description.** Export des données à remettre au livreur : coordonnées du client, adresse,
contenu de la commande, **montant restant dû**. Pas de gestion de livreurs, pas de suivi.

**Analyse commerciale.** Peu différenciant en soi, mais **c'est le geste quotidien du commerçant**
— aujourd'hui recopié à la main (problème 13 de `Positionnement.md`). Fiitsa a un module Logistique
entier ; ContexFly répond au même besoin en une fraction de l'effort. Le montant restant dû est le
champ qui compte : c'est lui qui rend le paiement à la livraison et l'acompte praticables.

**Utilité.** À chaque livraison. **Piste :** format directement partageable sur WhatsApp au livreur
plutôt qu'un fichier à télécharger — plus proche de l'usage réel. Effort S.

**Source.** Décision de Maxime · périmètre délimité contre le module Logistique de Fiitsa.

## C4 — Adresse de livraison : ville et quartier structurés + détail libre

**Statut : ✅ VALIDÉE avec correction (Maxime, 2026-08-17)** · Priorité : **Must** · Effort : **M**

⚠️ **Correction d'une erreur de Felix.** J'avais écrit « champ texte libre, jamais un formulaire
structuré ». **C'est faux**, et Maxime l'a démontré avec la capture d'un site e-commerce
camerounais à forte audience. Le modèle réellement utilisé sur ce marché est **hybride** :

- **Nom, Prénom, Numéro de téléphone** — obligatoires. E-mail **facultatif**.
- **Ville** (liste déroulante) et **Quartier** (liste déroulante) — **obligatoires tous les deux**.
- **Informations complémentaires**, facultatives : un **second numéro de téléphone, « ou celui
  d'un proche »**, et un **contact WhatsApp distinct**.
- Puis, en étapes séparées : méthode de livraison, mode de paiement.

**Le modèle retenu pour ContexFly** : **le commerçant déclare les villes où il livre et, pour
chacune, les quartiers**. Le client choisit sa ville, puis son quartier dans la liste, puis précise
librement son emplacement (« carrefour X, derrière la pharmacie Y ») dans un champ **facultatif**.

**Pourquoi ce modèle est meilleur que celui que je proposais — trois raisons, pas une :**
1. **Il rend le périmètre de livraison opposable.** Si le quartier du client n'est pas dans la
   liste, l'agent le sait immédiatement et le dit, au lieu d'accepter une commande non livrable.
   Aucun texte libre ne permet ça.
2. **Il débloque les frais de livraison par zone** — voir C5. Un tarif au quartier est impossible
   sur du texte libre.
3. **Il structure la donnée sans demander l'impossible.** Le repère parlé — qui est la vraie
   manière de s'orienter à Douala — reste présent, mais en complément facultatif, pas comme seule
   source de vérité.

**Rôles.** Commerçant (déclare villes et quartiers) · Client final (choisit) · Agent IA (vérifie
la couvrabilité) · Livreur (via C3).

**Analyse commerciale.** Peu différenciant en apparence, **mais c'est un marqueur de crédibilité
locale immédiat**. Un formulaire d'adresse postale à l'occidentale signale à un commerçant
camerounais que le produit n'a pas été pensé pour lui. À l'inverse, « ville → quartier → repère »
est le geste qu'il connaît. C'est exactement le type d'adaptation locale que `Positionnement.md`
identifie comme la vraie nature de la différenciation de ContexFly.

**Utilité.** À chaque commande livrée.

✅ **Mémorisation de l'adresse — VALIDÉE (Maxime, 2026-08-17).** L'adresse de livraison du client
est conservée et **proposée par défaut à la commande suivante** (« on livre au même endroit que la
dernière fois ? »). Effort S, et c'est le geste qui fait le plus sentir au client que le commerçant
le reconnaît. À noter pour `donnees-et-roles` : l'adresse appartient au **client**, pas à la
commande — donc une entité `adresse` rattachée au contact, avec plusieurs adresses possibles et une
adresse par défaut. Cohérent avec la mémoire client de B0/F.

**Source.** Capture d'un site e-commerce camerounais fournie par Maxime (2026-08-17).

## C5 — Zones de livraison et frais par zone

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Le commerçant gère sa liste de villes et de quartiers desservis, et peut associer
**un frais de livraison à chaque zone**. L'agent annonce le frais au moment où le client donne son
quartier, avant la validation du panier.

**Analyse commerciale.** Conséquence directe de C4, et **indispensable à la fiabilité du total**.
Sans frais par zone, le total annoncé par l'agent est faux dès que la livraison est payante — et
un total faux annoncé par une IA détruit la confiance plus sûrement qu'une absence de réponse.
Le benchmark ne montre aucun acteur local qui le fasse dans la conversation.

**Utilité.** À chaque commande livrée. **Piste :** livraison gratuite au-dessus d'un montant de
panier — levier de panier moyen classique, effort S une fois C5 en place. `Should`.

## C6 — Contacts secondaires du destinataire

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

Second numéro de téléphone (« ou celui d'un proche ») et contact WhatsApp distinct du numéro de
commande. **Détail typiquement local et loin d'être cosmétique** : sur ce marché, l'acheteur n'est
souvent pas le destinataire, et le livreur qui ne joint personne perd la course. Une ligne dans le
modèle de données, un vrai gain sur le taux de livraison.

**Source.** Capture fournie par Maxime — le site l'expose explicitement.

---

# Domaine D — Paiement & argent

## D1 — Moteur de paiement unique, cinq politiques au choix du commerçant

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **L**

**Description.** Un seul moteur, dont le déclenchement dépend d'un réglage choisi par chaque
entreprise cliente :

| Mode | Comportement | Paiement en ligne |
|---|---|---|
| Paiement avant commande | obligatoire pour valider | requis |
| Choix laissé au client | payer maintenant ou à la livraison | requis + branche « plus tard » |
| Paiement à la livraison | commande marquée à encaisser, vendeur notifié | non requis |
| Transfert à un humain | bascule vers un opérateur dès que le client veut payer | non requis |
| **⭐ Acompte** | versement partiel qui confirme, solde à la livraison | requis (partiel) |

**Rôles.** Gérant (choisit la politique) · Client final · Agent IA · Administrateur ContexFly.

**Analyse commerciale.** **C'est la brique où se gagne ou se perd le produit.** `Positionnement.md`
identifie « l'exécution sur la brique argent » comme l'un des quatre espaces réels : personne
localement n'a prouvé qu'il encaisse, réconcilie et gère le paiement à la livraison de façon
fiable. Le concurrent à battre n'est pas un SaaS, c'est **la capture d'écran de transfert Mobile
Money** — gratuite, universellement comprise, et invérifiable.
⚠️ **Contrepartie honnête : c'est aussi le mode le plus coûteux à défendre.** Toute commission
ajoutée à un panier de 15 000 FCFA donne au commerçant une raison rationnelle de revenir à la
capture d'écran. D'où le 0 % de commission retenu.

**Utilité.** Résout les problèmes 7, 8 et 9 de `Positionnement.md`. Fréquence : à chaque commande.

**Piste d'approfondissement.** Réconciliation automatique du paiement à la livraison quand le
vendeur encaisse en espèces (marquer « payé en espèces » depuis la fiche commande) — sinon le
reste dû reste faux indéfiniment. **À inclure au MVP**, c'est le corollaire de C2.

**Source.** Document de recherche de Maxime (4 modes) + Fiitsa (l'acompte, vérifié).

## D2 — L'acompte : nom affiché et explication personnalisables

**Statut : ✅ VALIDÉE (Maxime, 2026-08-16)** · Priorité : **Should** · Effort : **M**

**Description.** Pourcentage réglable **par produit**. Deux champs libres côté commerçant : le
**nom affiché** au client (à la place du mot « acompte ») et **l'explication** de ce à quoi sert le
versement.

**Analyse commerciale.** Repris de Fiitsa, où c'est la meilleure idée observée. Leur propre libellé
l'explique : *« le mot acompte fait hésiter — nomme le versement comme tu le dis en live »*. C'est
un travail sur la **formulation côté acheteur**, pas sur la mécanique — et c'est exactement ce qui
manque aux produits conçus ailleurs. Ça règle le risque du paiement à la livraison (client absent,
livreur payé pour rien) sans imposer le prépaiement intégral, qui est le principal frein à l'achat
sur ce marché.
**Ce n'est pas une différenciation — c'est un rattrapage.** À ne pas vendre comme une innovation.

**Utilité.** Sur chaque commande d'un commerçant qui livre. **Piste :** pourcentage variable selon
la valeur du panier (20 % en dessous de 20 000 FCFA, 50 % au-dessus) — utile, mais `Could`.

**Source.** Fiitsa, vérifié dans le produit.

## D3 — Encaissement Mobile Money via Notch Pay Sync

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **L**

**Description.** Collecte MTN MoMo et Orange Money, sous-comptes marchands, reversement au
commerçant. **Les fonds ne transitent jamais par ContexFly** (décision Q23) : ContexFly orchestre,
Notch Pay détient.

**Analyse commerciale.** Prérequis absolu, zéro différenciation — tous les acteurs locaux
encaissent en Mobile Money. Mais c'est le point de défaillance le plus coûteux : un paiement perdu
détruit la confiance plus vite que n'importe quel bug. **Effort L assumé** : webhooks, idempotence,
états intermédiaires, réconciliation.
Deux arguments de discours en découlent, tous deux vrais : **0 % de commission sur les ventes**, et
le fait de rester intermédiaire technique sans détenir les fonds — ce qui évite un agrément EME.

**Utilité.** À chaque paiement en ligne. **Piste :** GeniusPay (vu chez Ngavix) et PawaPay (vu chez
Fiitsa) comme solutions de repli si Notch Pay tombe — **à ne pas construire au MVP**, mais
l'abstraction doit être prévue dans le code.

**Source.** Décision Q20/Q23 · agrégateurs relevés au benchmark.

## D4 — Confirmation automatique par message WhatsApp à réception du paiement

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **S**

Sur webhook de paiement, l'application envoie un message de confirmation. **Ce qui disparaît, c'est
l'étape humaine** — vérifier la réception, revenir sur WhatsApp, confirmer — et donc le délai et le
doute post-paiement côté client. Template `utility`, **gratuit dans la fenêtre de service**.
Effort S, valeur immédiate, et c'est le moment où le client décide s'il refera confiance.

**Source.** Document de recherche de Maxime.

## D5 — Plafond de remise contraint côté serveur

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **S**

Garde-fou de Q9 : l'agent peut proposer une réduction, **le plafond est appliqué dans le code,
jamais dans le prompt**. Sinon un client négocie -80 % en conversation. À définir : plafond absolu,
plafond par palier de fidélité, produits exclus. Effort S, conséquence potentiellement chère si omis.

## D6 — Réconciliation et solde par commerçant

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Le commerçant voit ce qui a été encaissé, ce qui reste dû, ce qui a été reversé et quand.
Conséquence directe de l'option B : dès que ContexFly orchestre l'argent d'autrui, l'absence de
vue claire génère du support et de la défiance. Fiitsa a une page « Revenus » avec solde et
retrait ; ici les fonds sont chez Notch Pay, donc la vue est un miroir, pas un portefeuille.

## D7 — Remboursement / annulation

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

Annuler une commande payée et rembourser. Conséquence inévitable de l'option B (Q19). Souvent
oublié au MVP, et découvert au premier litige. À arbitrer : remboursement automatisé, ou procédure
manuelle assumée avec traçabilité.

## D8 — Abonnement ContexFly et facturation du commerçant

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Paliers, prélèvement en Mobile Money, relance en cas d'échec, suspension. ⚠️ **Le prix n'est pas
tranché** — il dépend de la modélisation du coût d'inférence (Q13), qui doit ouvrir le skill
`tarification`. À noter : **aucune facturation client-final n'est au programme** (décision Maxime,
scope OUT) — D8 ne concerne que l'abonnement de ContexFly.

---

# Domaine G — Structure du compte, utilisateurs & rôles

## G1 — ⭐ Un compte, plusieurs activités, un agent par activité

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **L**

**Description.** Un utilisateur ContexFly peut gérer **plusieurs activités** (plusieurs commerces).
**Chaque activité a son propre agent à configurer**, son catalogue, ses commandes, ses clients, sa
politique de paiement et ses zones de livraison. **Le nombre d'agents — donc d'activités — est
plafonné par le palier d'abonnement.**

**Rôles.** Gérant multi-activités · Vendeur (rattaché à une activité, pas au compte) ·
Administrateur ContexFly.

**Analyse commerciale.** ⚠️ **C'est la décision la plus structurante depuis l'option B, et elle
arrive tard.** Trois conséquences, dans l'ordre de gravité :

1. **Modèle de données.** Ce n'est plus `commerçant → produits`, c'est
   `compte → activité → {agent, catalogue, commandes, clients, zones, numéro WhatsApp}`. **Presque
   toutes les entités déjà décrites gagnent une clé d'activité.** Si ce n'est pas fait dès le
   départ, la reprise coûte plus cher que la fonctionnalité. → **priorité absolue au skill
   `donnees-et-roles`.**
2. **Tarification.** Le nombre d'agents devient un **levier de prix**, ce qui change la structure
   des paliers envisagée. Fiitsa fait exactement ça : 1 business sur tous les plans, illimité
   uniquement sur le plan Agence avec marque blanche. C'est donc une pratique validée localement.
3. **Meta.** Chaque activité a **son propre numéro WhatsApp**, donc son propre WABA et son propre
   portefeuille — sinon les activités se partagent le plafond d'envoi (constat du 07/10/2025).
   Le multi-activités multiplie donc les onboardings Meta, qui sont déjà le facteur limitant (Q22).

### ⚠️ Architecture Meta — la préférence de Maxime, et la bonne réponse

**Maxime (2026-08-17) :** préférence pour **des applications Meta développeur distinctes** par
activité, afin de ne pas recevoir le webhook « des deux côtés » à chaque message, même si un filtre
côté plateforme est possible.

**Le besoin est légitime, mais une app Meta par activité est le mauvais moyen — et ce serait
coûteux.** Vérifié le 2026-08-17 :
- Le tableau de bord Meta **n'expose qu'une seule URL de rappel par application**, et c'est le
  modèle **voulu** : tous les WABA et tous les numéros abonnés à une app envoient leurs événements
  à la même URL, distingués par le `phone_number_id` présent dans les métadonnées du message.
- **Chaque application Meta exige sa propre App Review** pour `whatsapp_business_management` et
  `whatsapp_business_messaging`. Multiplier les applications multiplie donc les revues Meta —
  plusieurs semaines chacune, avec possibilité de rejet. **Cela attaque directement la seule
  barrière défendable du projet, l'onboarding (Q22).** Et le statut Tech Provider avec Embedded
  Signup est précisément conçu pour qu'**une seule** application onboarde de nombreux clients.
- Des applications séparées ne se justifient que pour une **isolation d'infrastructure réelle**
  (serveurs distincts, équipes d'astreinte distinctes, aucun chemin de code partagé) — ce qui n'est
  pas le besoin exprimé ici.

**✅ La bonne réponse existe et donne à Maxime exactement ce qu'il veut : les *alternate webhook
endpoints*.** Meta permet de configurer une **URL de webhook propre à un WABA ou à un numéro**,
à l'intérieur d'une seule application — et la documentation cite explicitement ce cas :
*« si vous êtes un partenaire et souhaitez utiliser des points de terminaison uniques pour chacun
de vos clients onboardés »*.

→ **Architecture retenue : une seule application Meta (une App Review, un statut Tech Provider, un
Embedded Signup), avec un endpoint de webhook distinct par activité.** Séparation nette des flux,
sans aucun coût d'onboarding supplémentaire. → à figer au skill `architecture-integrations`.

**Utilité.** Réelle sur ce marché : un commerçant camerounais gère fréquemment plusieurs négoces
en parallèle. Et cela ouvre un segment que le benchmark montre rentable — **les agences et
revendeurs**, qui gèrent les comptes de plusieurs commerçants (Fiitsa a un plan Agence, Genuka WA
vend des « comptes tiers pour vos clients », Ozirus et les agences camerounaises sont déjà le
concurrent n°2 identifié). **Les servir plutôt que les combattre est une option de distribution
sérieuse.**

**Piste d'approfondissement.** Marque blanche pour ces revendeurs — présente chez Fiitsa (plan
Agence) et chez Genuka WA dès 10 000 FCFA/mois. **Hors MVP**, mais à ne pas rendre impossible.

⚠️ **Réserve d'effort.** Noté **L**, et c'est un L qui pèse sur les 3-4 semaines : le
multi-locataire touche l'authentification, les permissions, le routage des webhooks WhatsApp par
numéro, et l'isolation des données. ✅ **Arbitrage retenu (Maxime, 2026-08-17) : modéliser le multi-activités dès maintenant dans les
données, mais ne livrer qu'une seule activité par compte au MVP.** Le coût d'ajout ultérieur
devient alors faible ; l'inverse n'est pas vrai.

**Source.** Maxime · pratique confirmée chez Fiitsa (limite de business par palier).

## G2 — Points de vente

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

**Description.** Enregistrement des points de vente physiques d'une activité.

**Analyse commerciale.** L'intérêt dépend entièrement d'une question non tranchée — **à quoi sert
le point de vente pour l'agent ?** Trois lectures possibles, d'effort très différent :
- *simple information* — l'agent peut dire où se trouvent les boutiques et leurs horaires. Effort
  **S**, valeur réelle et immédiate.
- *point de retrait* — le client choisit de venir chercher au lieu de se faire livrer. Effort
  **M**, et cela ajoute un mode à C5 (retrait = frais nul).
- *stock par point de vente* — l'agent sait que le 42 est disponible à Akwa mais pas à Bonamoussadi.
  Effort **L**, et **cela change le modèle de stock de B2, qui est déjà par variante**. Stock par
  variante **et** par point de vente est un produit à part entière.

✅ **Arbitrage de Maxime (2026-08-17) : les trois lectures sont retenues, et le stock par point de
vente entre dans le MVP.** Ma recommandation était de l'exclure ; elle n'est pas suivie.

⚠️ **Je le signale une fois, puis j'avance.** Le stock devient alors indexé **par variante ET par
point de vente** — le 42 disponible à Akwa mais pas à Bonamoussadi. Trois conséquences concrètes,
toutes à absorber dans les 3-4 semaines :
1. **Modèle de données** — la ligne de stock devient `(produit, variante, point de vente)`. Combiné
   aux attributs dynamiques de B0, c'est la partie la plus délicate du schéma. **À traiter en tête
   du skill `donnees-et-roles`.**
2. **Conversation** — l'agent ne peut plus répondre « oui, disponible ». Il doit dire *où*, et
   savoir quoi faire quand c'est disponible ailleurs qu'au point le plus proche du client : proposer
   le retrait dans l'autre boutique, proposer un transfert, ou refuser. **Cela ajoute une branche
   de décision à A1, qui est déjà la fonctionnalité la plus coûteuse du projet.**
3. **Décrément à la commande (B2)** — il faut désormais décider *de quel point de vente* on décompte,
   ce qui n'est pas déductible automatiquement.
4. **Charge d'exploitation pour le commerçant** — tenir un stock par boutique à jour est un travail
   réel. Si ce n'est pas tenu, l'agent devient moins fiable qu'un agent sans stock du tout, parce
   qu'il affirme au lieu de vérifier. → à couvrir par une exigence : **un point de vente peut être
   déclaré « stock non suivi »**, et l'agent se rabat alors sur une réponse prudente.

**Le périmètre G2 retenu est donc :** information (adresse et horaires des boutiques) + point de
retrait (mode de livraison à frais nul dans C5) + **stock par point de vente**.
**Effort révisé : L.**

**Utilité.** Dépend du commerçant : forte pour un multi-boutiques, nulle pour un vendeur unique —
d'où l'importance de l'option « stock non suivi » pour ne pas pénaliser le second.

**Source.** Maxime.

## G3 — Équipe et permissions

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Gérant / vendeur, rattachement à une activité (pas au compte), invitation, retrait. Découle de la
décision multi-utilisateur du 2026-08-16 et de G1. Détail au skill `donnees-et-roles`.

---

---

# Domaine E — Boîte de réception

Brief de conception détaillé dans `Reference-Conception-Agent.md` §3 — le modèle observé chez Zoko
est repris presque tel quel.

## E1 — Inbox de supervision

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Vues `Toutes` / `Non assignées` / `Mes conversations` / `Conversations des autres`,
filtres `Toutes` / `Non lues` / `Sans réponse`, assignation à un vendeur, et le fil de conversation
avec envoi de messages.

**Rôles.** Gérant · Vendeur.

**Analyse commerciale.** ⚠️ **Ce n'est PAS un différenciateur** — Waazi vend l'inbox seule à
25 000 FCFA/agent à Douala. C'est un **prérequis de crédibilité** : sans elle, la bascule IA↔humain
(A6) n'a pas d'écran, et le commerçant ne peut pas vérifier ce que son agent a dit en son nom.
`Positionnement.md` l'interdit explicitement comme argument de vente.
⚠️ **Périmètre à tenir (Q6) : inbox de supervision, pas helpdesk multi-canal.** Le brief initial
disait « remplace l'app WhatsApp » — un Chatwoot est un produit à part entière, hors budget.

**Utilité.** Quotidienne dès qu'un humain reprend une conversation.

✅ **Arbitrage final (Maxime, 2026-08-17) : mobile-first, avec un responsive sérieusement
travaillé pour ordinateur et tablette.** *(Renverse la position « bureau d'abord » exprimée plus
tôt le même jour — voir `Changelog.md`.)*

**C'est le bon choix, et le benchmark le soutient :** Ayweu, le concurrent local qui revendique
3 000+ vendeurs, est **mobile-only** — il a jugé que sa cible ne travaille pas sur ordinateur. Un
commerçant de quartier gère son commerce depuis son téléphone ; une inbox conçue pour le bureau
risquait de n'être simplement jamais ouverte, et la bascule IA↔humain (A6) serait restée théorique.

⚠️ **Ce que « mobile-first » impose et qu'il ne faut pas sous-estimer :** une inbox tient mal sur un
écran de téléphone. Les trois écrans du modèle Zoko (liste des conversations · fil · panneau
contact) ne peuvent pas coexister — il faut une navigation à niveaux, et décider **ce qui reste
visible en permanence**. Ma recommandation : l'indicateur de fenêtre 24 h (E2) et l'accès à
l'historique de commandes ne doivent jamais être à plus d'un geste.
**Web responsive, pas application native** — sinon on ajoute une distribution par les stores au
chemin critique, qui est déjà contraint par Meta (Q22).

**Source.** Vision de Maxime · modèle Zoko (vérifié) · Waazi comme comparable de prix.

## E2 — ⭐ Indicateur de fenêtre de service 24 h

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **S**

**Description.** Dans chaque conversation, l'état de la fenêtre Meta affiché en clair : « tu peux
répondre librement encore 6 h » vs « hors fenêtre — seul un message pré-approuvé peut partir, et il
sera facturé ».

**Analyse commerciale.** Vu chez Zoko sous forme d'un badge `TEMPORARILY ALLOWED`, et **c'est le
meilleur détail d'interface de tout le benchmark**. Sans lui, un vendeur ne comprend jamais pourquoi
son message part parfois librement et parfois échoue ou coûte de l'argent — il conclut que le
produit est cassé. Effort **S**, effet direct sur la perception de fiabilité et sur la maîtrise du
coût par le commerçant.

**Utilité.** Permanente, sur chaque conversation.

**Piste d'approfondissement.** Aller plus loin que Zoko : proposer directement le template
pré-approuvé adapté quand la fenêtre est fermée, plutôt que de laisser le vendeur découvrir l'échec.

**Source.** Zoko, vérifié.

## E3 — Panneau contact dans la conversation

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Téléphone, ville/quartier, adresses connues, étiquettes, médias échangés, **historique de commandes
du client**, et accès au catalogue sans quitter la conversation.

**Analyse commerciale.** L'historique de commandes est le point qui compte : **c'est exactement ce
que l'agent de Fiitsa ne peut pas voir** (aucune case d'accès aux commandes dans sa configuration).
C'est aussi ce qui rend F1 et F2 possibles. Zoko l'a ; Fiitsa non. Effort M, valeur structurante.

## E4 — Réponses rapides

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

Messages pré-composés pour l'opérateur humain. Standard chez Zoko, trivial à construire, très
utilisé en pratique. Aucune différenciation, bon rapport valeur/effort.

## E5 — Étiquettes de conversation et de contact

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

Étiquettes libres (`VIP`, `panier abandonné`, `litige`…), posées à la main ou automatiquement.
Prérequis de F1 : sans elles, la segmentation manuelle est impossible et tout repose sur les règles.

## E6 — Notes internes

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Could** · Effort : **S**

Notes visibles par l'équipe, invisibles du client. Résout le problème 14 de `Positionnement.md` —
la rupture de contexte quand un vendeur reprend la conversation d'un autre. Faible coût, utile dès
qu'il y a deux vendeurs.

---

# Domaine F — Fidélisation & sortant

⚠️ **Contrainte transverse à tout ce domaine, vérifiée :** Meta plafonne les messages marketing à
**~2 par utilisateur final et par jour, tous expéditeurs confondus**, au niveau de l'utilisateur et
non de l'entreprise. Erreur `131049`. **La délivrance d'une campagne ne peut donc jamais être
garantie** — le produit doit gérer cet échec sans le présenter comme une faute du commerçant.

## F1 — Segments fondés sur l'historique d'achat

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Groupes de clients calculés sur la donnée de commande : nombre de commandes,
panier moyen, date de dernière commande, produits ou catégories achetés, ville/quartier.

**Analyse commerciale.** **C'est le socle du seul différenciateur produit sérieux.** Un outil de
campagne générique ne peut pas segmenter sur « a commandé 3 fois » parce qu'il n'a pas la donnée de
commande — ContexFly la produit lui-même (C1). Vérifié : **l'agent de Fiitsa n'a aucun accès à
l'historique de commandes**, ce n'est même pas branchable sur leur architecture. Zoko a des
« Segments », mais les commandes vivent chez Shopify.
Levier de **rétention** : plus le produit tourne, plus la segmentation devient précise, plus le
départ coûte cher. C'est le seul avantage que `Positionnement.md` identifie comme grandissant avec
le temps.

**Utilité.** Résout les problèmes 10, 11 et 12 — aucune trace exploitable des clients passés,
ciblage impossible, incapacité à récompenser au bon moment.

**Piste d'approfondissement.** Segments prédéfinis et nommés en clair (« clients fidèles »,
« clients endormis depuis 45 jours », « gros paniers ») plutôt qu'un constructeur de requêtes —
même logique que F3.

## F2 — ⭐ Remise automatique proposée en conversation

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** L'agent propose spontanément une réduction à un client qui a franchi un seuil
(nombre de commandes, montant cumulé), **pendant** qu'il discute des produits — pas par message
séparé.

**Analyse commerciale.** **Le différenciateur le plus net du dossier.** Vérifié : la section
Réductions de Fiitsa est un gestionnaire de codes promo classique, sans aucun déclencheur
comportemental, et leur agent n'a pas accès à l'historique — donc ce n'est pas seulement absent,
c'est **non branchable** chez le concurrent local le plus sérieux. Flowcart le fait mondialement,
mais rejette les numéros camerounais à l'inscription.
Levier de rétention côté client final **et** de rétention côté commerçant.

**Utilité.** À chaque conversation d'un client récurrent.

⚠️ **Dépendance dure : D5. ✅ Validée par Maxime (2026-08-17).** Le plafond de remise est contraint
côté serveur, jamais dans le prompt — sinon un client négocie -80 % en conversation. **F2 n'est pas
livrée sans D5.**

## F3 — ⭐ Automatisations pré-écrites, activables en un clic

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** Une bibliothèque de 5-6 automatisations prêtes à l'emploi, chacune activable en un
clic avec 2-3 paramètres : « client sans commande depuis N jours → message de relance », « après
N commandes → remise de X % proposée », « panier abandonné depuis N heures → relance », « nouveau
client après sa première commande → message de remerciement ».

**Analyse commerciale.** **Différenciateur d'exécution, démontré par l'échec du concurrent.**
Vérifié dans le produit : l'onglet Templates de Fiitsa contient exactement deux entrées, dont une
nommée « Workflow Santé et Business **(copie)** » — un résidu de développement — à **0 utilisation**,
**0 avis**, et **30 minutes** de configuration estimée. Le leader local a livré un moteur de règles
générique et **aucune automatisation utilisable**.
Livrer 5-6 automatisations qui fonctionnent suffit à dépasser tout leur module, pour un effort M.
C'est le meilleur rapport valeur/effort du dossier.

**Utilité.** Continue, en arrière-plan. Fréquence d'usage du commerçant : quasi nulle après
activation — ce qui est précisément le but.

**Piste d'approfondissement.** Mesurer le revenu généré par chaque automatisation et l'afficher :
c'est ce qui transforme une fonctionnalité en argument de renouvellement d'abonnement.

## F4 — Campagnes de réengagement vers une base opt-in

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

Envoi d'un template marketing à un segment (F1). **Jamais vers des listes froides** — décision
actée du 2026-08-15. Le produit doit gérer l'erreur `131049` (plafond de fréquence atteint chez le
destinataire), réessayer le lendemain, et expliquer l'échec en clair au commerçant.

## F5 — Consentement et désabonnement

**Statut : ✅ ORDRE VALIDÉ (Maxime, 2026-08-17) — F5 précède F4, sans exception.**
Priorité : **Must** · Effort : **S**

Conservation de la preuve d'opt-in (date, source) et désabonnement facile dans chaque message
sortant. **Ce n'est pas une fonctionnalité, c'est une obligation Meta** — et le taux de blocage des
destinataires est ce qui fait chuter le *quality rating* du numéro du commerçant jusqu'au
bannissement. Effort S, conséquence maximale si omis. **Doit précéder F4.**

## F7 — ⭐ Pédagogie des règles WhatsApp dans le produit

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

**Description.** Le produit **explique au commerçant les règles de Meta au moment où elles le
concernent**, en langage clair, plutôt que de les subir ou de les masquer. Quatre endroits :
- **le plafond de fréquence** — « Meta limite les messages promotionnels à environ 2 par jour et
  par client, tous commerces confondus. C'est une protection contre le spam : ton message n'a pas
  été refusé par nous, il attendra demain. »
- **la fenêtre de 24 h** (E2) — pourquoi répondre est gratuit dans les 24 h et payant après ;
- **la note de qualité du numéro** — pourquoi trop de blocages de la part des clients dégrade son
  numéro, et ce que ça finit par coûter ;
- **les catégories de templates** — pourquoi un message « commande » coûte moins cher qu'un message
  « promotion ».

**Rôles.** Gérant · Vendeur.

**Analyse commerciale.** **Posture opposée à celle du concurrent, et vérifiable.** Fiitsa
revendique sur sa page tarifs *« 0 risque de blocage par Meta »* — une affirmation intenable,
puisque la note de qualité dépend du taux de blocage des destinataires et non de l'outil d'envoi.
Promettre l'impossible prépare une déception ; expliquer la règle construit la confiance et réduit
le support.
C'est aussi de la **rétention par compétence** : un commerçant qui comprend pourquoi ses messages
partent ou non attribue les échecs à Meta, pas à ContexFly — et il devient meilleur utilisateur.
Effort **S**, c'est du texte bien placé, pas de la technique.

**Utilité.** Au premier échec `131049`, à la première campagne, à la première sortie de fenêtre.
Fréquence : ponctuelle mais aux moments exacts où le commerçant risque d'accuser le produit.

**Piste d'approfondissement.** Afficher au commerçant **la note de qualité de son propre numéro**
telle que Meta la renvoie (vert / jaune / rouge), avec ce qu'il peut faire pour la remonter.
Personne dans le benchmark ne le fait. → candidat sérieux pour `Should` plutôt que `Could`.

**Source.** Maxime · à l'opposé direct de la revendication « 0 risque de blocage » de Fiitsa
(vérifiée sur leur page tarifs).

## F6 — Constructeur de règles générique

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Could** · Effort : **L**

Conditions / déclencheurs / actions libres. **Position de Felix (Q6bis) : jamais avant F3, et
probablement jamais tout court au MVP.** L'écran vide d'un rule builder reste vide — c'est
démontré chez Fiitsa. Si ça arrive un jour, ça arrive **après** la bibliothèque, jamais à sa place.

---

---

# Domaine H — Onboarding

Brief de conception dans `Reference-Conception-Agent.md` §2. C'est le domaine qui porte la **seule
barrière durable identifiée** dans `Positionnement.md` — « ce n'est pas l'agent IA qui protégera
ContexFly, c'est l'onboarding ».

## H1 — Connexion du numéro par Embedded Signup

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **L**

Flux Meta intégré : le commerçant se connecte depuis ContexFly, son WABA est créé et lié sans
quitter l'interface, il possède ses actifs et ajoute son propre moyen de paiement Meta.

**Analyse commerciale.** **C'est la fonctionnalité la plus stratégique du produit après A1.** Toute
la thèse de `Positionnement.md` repose dessus. Effort L, et le risque n'est pas dans le code : il
est dans la validation Meta (App Review, vérification d'entreprise) qui est hors du contrôle de
Maxime et **hors du chemin de développement** (Q22).
Architecture actée : **une seule application Meta**, plusieurs numéros, endpoints de webhook
distincts par WABA.

## H2 — Onboarding conversationnel avec miroir de valeur

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

Séquence `profil → secteur → structure → objectif → miroir de valeur → configuration`, chaque
question justifiant sa présence en une ligne, et l'écran qui renvoie ses propres chiffres au
commerçant avant tout engagement (« tu réponds à ~N messages par jour, soit X heures par
semaine »).

**Analyse commerciale.** Repris de Wazzap, où c'est la meilleure mécanique observée. Ce n'est pas
une fonctionnalité produit mais un **levier d'activation** — et l'activation est l'objectif
mesurable n°3 de `Idee.md` (délai inscription → première commande encaissée). Le secteur déclaré
alimente directement la mémoire de B0.

## H3 — Compte de démonstration pré-rempli

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

Conversations et produits fictifs réalistes, explorables **avant** de connecter un numéro et avant
de payer. Modèle Zoko (7 jours, bandeau permanent « connecte ton numéro »).

**Analyse commerciale.** Réponse peu coûteuse à la **mortalité n°1 de ce type de produit — le
catalogue vide**. Sert aussi de support de démonstration commerciale sur le terrain, ce qui compte
face aux agences camerounaises qui vendent en face-à-face. Découplage à reprendre de Fiitsa : **ne
jamais bloquer l'inscription sur la connexion Meta**.

## H4 — Tutoriel vidéo intégré

**Statut : ✅ VALIDÉE (Maxime, 2026-08-15)** · Priorité : **Should** · Effort : **S**

Vidéo expliquant la configuration du numéro. Décidée au cadrage. Effort S, à condition de ne pas
produire la vidéo soi-même dans le périmètre du MVP.

## H5 — KYC du commerçant

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Collecte et transmission des pièces exigées par Notch Pay pour ouvrir un sous-compte marchand.
Conséquence directe de l'option B. **Le régime KYC personne physique est ce qui rend la cible
« commerçant sans société » atteignable** — c'est l'argument qui a fait retenir Notch Pay contre
PawaPay. Les pièces exactes restent à confirmer au contrat (Q21).

## H6 — État d'avancement de l'installation

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**

Une liste visible en permanence : numéro connecté ✓, catalogue rempli ✓, politique de paiement
choisie ✓, compte de collecte validé ✓, première commande reçue. Chaque étape non faite est un
point de fuite ; Fiitsa laisse un commerçant utiliser le produit sans jamais connecter Meta, et
c'est exactement le trou à ne pas reproduire. Effort S, effet direct sur l'activation.

---

# Domaine I — Reporting

## I1 — Tableau de bord commerçant

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

Commandes, chiffre d'affaires, panier moyen, taux de conversion conversation → commande payée, sur
7 / 30 / 90 jours. Standard chez tous les acteurs. Aucune différenciation, mais son absence se
remarque immédiatement.

## I2 — ⭐ Taux d'autonomie

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

**Description.** La part des commandes payées obtenues **sans reprise humaine**, plus le nombre de
conversations reprises et pourquoi.

**Analyse commerciale.** **C'est la métrique n°1 de `Idee.md`, et sans I2 elle reste déclarative.**
Deux usages, l'un interne et l'autre commercial : elle dit à Maxime si son agent tient sa promesse
(si le taux est bas, ContexFly est une inbox, pas un vendeur), et elle donne au commerçant la
preuve chiffrée de ce que son abonnement lui rapporte — donc l'argument de renouvellement.
Zoko a une « Agent Analytics » en BETA (temps de réponse, taux de résolution) ; personne ne mesure
l'autonomie d'un agent IA de vente. Effort M.

**Piste d'approfondissement.** Croiser avec les motifs de reprise pour identifier ce que l'agent ne
sait pas faire — et alimenter directement la mémoire de B0. C'est la boucle d'amélioration du
produit.

## I3 — Suivi de la consommation et du coût

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**

Nombre de conversations, messages sortants par catégorie de template, coût Meta associé. Deux
raisons : le commerçant paie Meta directement (il doit comprendre sa facture), et **Maxime a besoin
de cette donnée pour modéliser le coût d'inférence (Q13)** — sans quoi la tarification reste une
supposition. À instrumenter dès le premier jour, même sans écran.

---

# Domaine J — Back-office ContexFly

## J1 — Administration des comptes et instruction du KYC

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Vue des commerçants, instruction des dossiers KYC, état des sous-comptes Notch Pay, suspension.
⚠️ **L'option B en fait un vrai produit interne, pas un accès superutilisateur bricolé** — c'est une
obligation opérationnelle, pas un confort.

## J2 — Supervision des paiements et des litiges

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**

Suivi des encaissements, des reversements, des échecs et des remboursements (D6, D7). Sans cette
vue, le premier litige se traite dans la base de données.

---

# Domaine K — Socle SaaS

Couvert par `ai-builder-saas` (TanStack Start, Convex, Better Auth, Zod, shadcn/ui, Tailwind,
Paraglide JS) : authentification, multi-locataire, internationalisation FR/EN, thème, composants.
Pour mémoire — à vérifier point par point au skill `integration-base`, notamment ce que Better Auth
couvre réellement pour la structure `compte → activité → membre` de G1.

---

---

# Passe proactive de Felix

Quatre propositions, aucune issue de la vision de Maxime ni d'une demande. Toutes tirées du
benchmark et de `Positionnement.md`. Aucune n'a d'équivalent identifié chez les acteurs explorés.

## P1 — ⭐ Mode brouillon : l'agent propose, l'humain valide en un geste

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Must** · Effort : **M**
**Source : Felix (proactif).**

**Description.** Un troisième réglage entre « IA active » et « humain seul » : l'agent **rédige la
réponse mais ne l'envoie pas**. Le commerçant la voit dans son inbox, l'envoie d'un geste, la
modifie, ou l'ignore. Réglable par activité, et **désactivable automatiquement** une fois qu'un
seuil de confiance est atteint (« tu as validé 50 réponses sans modification — tu passes en
automatique ? »).

**Rôles.** Gérant · Vendeur · Agent IA.

**Analyse commerciale.** **C'est une réponse au plus gros obstacle d'adoption du produit, et il
n'est pas technique : c'est la peur.** On demande à un commerçant de laisser une IA parler à ses
clients, en son nom, sur le numéro qui *est* son fonds de commerce. Le benchmark montre que
personne ne traite cette peur : Fiitsa livre « prendre des commandes » **désactivé par défaut** —
c'est-à-dire qu'ils ont constaté le problème et ont choisi de reculer plutôt que de le résoudre.
Le mode brouillon le résout : le commerçant obtient la vitesse de l'IA en gardant le dernier mot,
puis lâche prise quand il a vu que ça marche.
Levier d'**acquisition** (l'objection « je ne veux pas qu'un robot parle à mes clients » tombe) et
de **conversion vers l'usage réel** — c'est ce qui fait passer du compte créé à l'agent actif,
l'objectif mesurable n°3 de `Idee.md`.
Bonus : c'est **le mode le plus compatible avec le mobile-first** retenu en E1 — valider une
réponse en un geste sur téléphone est exactement ce qu'un commerçant peut faire entre deux clients.

**Utilité.** Sur toute la période d'adoption, puis à la demande sur les conversations sensibles.
Fréquence : intense les premières semaines, décroissante — ce qui est le but.

**Piste d'approfondissement.** Mesurer le **taux de modification** des brouillons : c'est le
meilleur indicateur avancé de la qualité de l'agent, et il alimente directement P2 et I2. À
afficher au commerçant comme preuve de progression.

## P2 — ⭐ L'agent apprend des reprises humaines

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**
**Source : Felix (proactif).**

**Description.** Chaque fois qu'un humain reprend une conversation (A6) ou corrige un brouillon
(P1), le système propose : *« Tu as répondu ça. Je l'ajoute à ce que je sais, pour la prochaine
fois ? »* La réponse validée alimente la base de connaissance de l'agent — et, quand elle porte sur
un produit, **le modèle de champs de B0 pour cette catégorie**.

**Analyse commerciale.** **C'est la boucle qui ferme le système, et c'est le seul avantage qui
grandit avec le temps.** `Positionnement.md` est explicite : la différenciation de ContexFly est
géographique et tarifaire, et toutes ses barrières tombent si un concurrent mieux financé descend
en gamme. Les deux seules choses défendables dans la durée sont l'onboarding et **la donnée
accumulée**. P2 est le mécanisme qui transforme l'usage quotidien en avantage cumulatif : au bout
de six mois, l'agent d'un commerçant connaît son métier, et repartir de zéro ailleurs coûte cher.
Aucun acteur exploré ne le fait — Wazzap et Landbot font apprendre l'agent **pendant la
configuration**, jamais **pendant l'exploitation**.
Levier de **rétention** au sens fort, et levier direct sur le **taux d'autonomie** (I2).

**Utilité.** À chaque reprise humaine. Fréquence : décroissante par construction, ce qui est
exactement le signal de succès.

**Piste d'approfondissement.** Version aboutie : si l'agent bute **trois fois sur la même question**
pour une catégorie de produits, il propose de lui-même d'ajouter le champ manquant au modèle B0
(« tes clients demandent souvent la matière pour tes sacs — je l'ajoute à la fiche produit ? »).
La mémoire n'apprend plus seulement de la saisie, mais des vraies questions des clients. **Hors
MVP**, mais c'est la version qui rend B0 spectaculaire.

## P3 — Alerte de retour en stock

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **M**
**Source : Felix (proactif).**

**Description.** Quand l'agent doit répondre « je n'ai plus le 42 », il propose : *« je te préviens
dès qu'il revient ? »*. Le client accepte, et le retour en stock déclenche un message
automatique.

**Analyse commerciale.** **Transforme une vente perdue en vente différée, sur la question la plus
fréquente du commerce WhatsApp.** Le benchmark l'établit : la conversation que Zoko met en vitrine
est *« do you have the blue running shoes in size 9? »* — la question de variante est la question
canonique, et la rupture est donc un cas fréquent, pas marginal.
Trois choses la rendent possible et peu coûteuses : le stock par variante (B2), le consentement
explicite du client dans la conversation (F5 — opt-in propre et daté), et le fait que le message
de retour en stock est un template **utility**, donc **hors du plafond marketing** de 2 messages
par jour. C'est le rare message sortant qui ne consomme pas le quota et que le client a
explicitement demandé — donc à taux de blocage quasi nul, ce qui protège la note de qualité du
numéro.
Aucun acteur local ne le fait. Levier de **revenu direct**, mesurable.

**Utilité.** À chaque rupture rencontrée en conversation. **Piste :** dire au commerçant *combien
de clients attendent* un produit — c'est un signal de réassort qu'aucun de ses outils actuels ne
lui donne.

## P4 — Lien produit partageable qui ouvre WhatsApp

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité pressentie : **Should** · Effort : **S**
**Source : Felix (proactif).**

**Description.** Chaque produit a un lien public léger (photo, prix, description) avec un bouton
« Commander sur WhatsApp » qui ouvre une conversation **pré-remplie sur ce produit précis**.
L'agent sait immédiatement de quoi on parle. Le commerçant partage ces liens dans son statut
WhatsApp, ses groupes, sa page Facebook.

**Analyse commerciale.** **Comble le seul vrai manque du produit : ContexFly sait traiter les
conversations, mais ne fait rien pour en créer.** Et `Positionnement.md` désigne « le commerçant
sans site web » comme le segment le plus défendable — or ce commerçant n'a aucun endroit où
envoyer les gens. Son canal d'acquisition réel, c'est le **statut WhatsApp** et les **groupes**,
documentés au benchmark comme ses outils actuels.
Le lien pré-rempli élimine aussi le premier tour de conversation le plus coûteux (« bonjour, c'est
pour quel produit ? »), ce qui améliore mécaniquement le taux d'autonomie et réduit le coût
d'inférence — deux points sensibles du dossier (I2, Q13).
Effort **S**, et c'est un levier d'acquisition pour le commerçant, donc un argument de vente pour
ContexFly. Zoko a un « click-to-chat button », mais destiné à un **site web** que la cible n'a pas.

**Utilité.** Permanente côté commerçant. **Piste :** QR code imprimable pour la devanture et les
emballages — coût nul, très adapté au commerce physique local. Et à terme, la base d'une campagne
Click-to-WhatsApp payante, mais **hors MVP**.

---

---

# Domaine L — Croissance : parrainage et réductions (plateforme ContexFly)

⚠️ **Ce domaine concerne ContexFly lui-même, pas les commerçants.** Il s'agit d'acquérir des
commerçants abonnés, pas de faire vendre les commerçants. À ne pas confondre avec F (fidélisation
des clients finaux) ni avec les codes promo produits de C.

Source : demande de Maxime (2026-08-17), enrichie par une recherche sur les pratiques d'affiliation
SaaS. Toutes validées d'office sur consigne de Maxime.

## L1 — ⭐ Programme de parrainage avec commission

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Should** · Effort : **L**

**Description.** Un parrain reçoit un **lien unique**. Tout commerçant qui s'inscrit via ce lien
lui est attribué, et le parrain touche soit un **pourcentage de l'abonnement**, soit un **montant
fixe**, au choix de ContexFly et paramétrable par campagne. Commission **ponctuelle ou récurrente**.

**Rôles.** Parrain (nouveau rôle, extérieur au produit) · Administrateur ContexFly · Commerçant
filleul (passif).

**Analyse commerciale.** **C'est le canal d'acquisition le plus adapté au marché visé.** Le
benchmark a identifié les agences camerounaises (Ozirus et consorts) comme le **concurrent n°2** —
« ce sont elles qui prendront tes 50 premiers clients », parce qu'il y a quelqu'un à appeler.
L1 permet de **les recruter comme parrains plutôt que de les affronter**, ce qui transforme la
principale menace de distribution en force de vente. Et G1 (multi-activités) va déjà dans ce sens.
Repères de marché relevés : **20-30 % de commission récurrente**, ou un CPA plafonné à environ un
mois de revenu. Ces bandes sont des repères mondiaux, à confronter à la marge réelle une fois le
coût d'inférence modélisé (Q13) — **une commission récurrente de 25 % sur un abonnement à
15 000 FCFA n'est soutenable que si la marge le permet.**

**Utilité.** Continue, côté acquisition. Fréquence d'usage produit : faible, mais l'effet est sur
le volume de clients.

**Piste d'approfondissement.** ⭐ **Déclencher la commission sur la première commande encaissée du
filleul, pas sur son inscription.** L'inscription ne coûte rien et ne prouve rien ; entre elle et
la première vente il y a la connexion Meta et le KYC, c'est-à-dire tout ce qui fait échouer
l'activation. Payer sur l'activation aligne le parrain avec la seule chose qui compte — et
c'est directement l'objectif mesurable n°3 de `Idee.md`. **Recommandation forte de Felix.**

## L2 — Attribution serveur-à-serveur, pas par cookie

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Must (si L1)** · Effort : **M**

**Description.** L'identifiant de clic est porté dans l'URL, capté et stocké côté serveur au moment
du clic, puis rattaché à l'inscription et aux événements de conversion depuis le backend.

**Analyse commerciale.** ⚠️ **Ce n'est pas un raffinement technique, c'est une condition de
fonctionnement sur ce marché précis.** Les liens de parrainage circuleront **dans WhatsApp** — ils
s'ouvriront donc dans le navigateur intégré de WhatsApp, où les cookies sont peu fiables, souvent
cloisonnés, et perdus dès que l'utilisateur bascule vers son navigateur habituel. Une attribution
par cookie perdrait une grande partie des parrainages, et un parrain non payé ne parraine plus
jamais. Les sources consultées convergent : les programmes sérieux s'appuient sur du
serveur-à-serveur plutôt que sur les cookies, qui « tombent, sont bloqués et sont triviaux à
manipuler ».

**Utilité.** Invisible pour l'utilisateur, structurante pour la confiance des parrains.

## L3 — Liens et codes de réduction sur l'abonnement

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Should** · Effort : **M**

Réduction en **pourcentage ou en montant fixe** sur l'abonnement ContexFly, sous forme de code ou
de lien direct. Paramètres : durée d'application (premier mois, N mois, à vie), date d'expiration,
plafond du nombre d'utilisations, et restriction éventuelle aux nouveaux comptes.

**Analyse commerciale.** Outil d'acquisition classique et peu coûteux, utile pour les lancements,
les partenariats et les campagnes locales. **Attention au couplage avec L1** : un filleul qui
utilise en plus un code de réduction peut rendre la commission supérieure à la marge. Le moteur
doit interdire le cumul, ou plafonner le total consenti.

## L4 — Anti-fraude et clawback

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Must (si L1)** · Effort : **M**

**Description.** Détection de l'**auto-parrainage** (le commerçant qui se parraine lui-même avec un
second numéro), des fermes de faux comptes, et **reprise de la commission (clawback)** en cas de
remboursement ou de résiliation du filleul dans les N premiers mois.

**Analyse commerciale.** **Sans L4, L1 est une fuite de trésorerie, pas un canal d'acquisition.**
Les sources sont explicites : le modèle de commission récurrente est précisément ce qui fait des
programmes d'affiliation SaaS une cible, et la détection doit **bloquer avant le versement**, pas
après. Contexte aggravant ici : ContexFly dispose déjà du **KYC des commerçants** (H5) et du numéro
de téléphone vérifié — le recoupement identité/numéro/moyen de paiement rend l'auto-parrainage
détectable à faible coût. **C'est un avantage que la plupart des SaaS n'ont pas ; il faut s'en
servir.**
Combiné à la piste de L1 (commission sur la première commande encaissée), la surface de fraude se
réduit encore : fabriquer un faux commerçant qui encaisse réellement une commande coûte plus cher
que la commission.

## L5 — Versement des commissions en Mobile Money

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Must (si L1)** · Effort : **M**

Versement des gains par Mobile Money via Notch Pay, avec **seuil de versement bas** et calendrier
annoncé.

**Analyse commerciale.** **Point d'adaptation locale décisif, et invisible dans les outils
d'affiliation existants** — ils versent en PayPal, virement ou Stripe, dont aucun n'est praticable
pour un parrain camerounais. Le rail de reversement existe déjà (D3), donc l'effort marginal est
faible. Le **seuil bas** compte autant que le rail : le parrain typique ici n'est pas un affilié
professionnel, c'est une connaissance qui amène deux ou trois commerçants — un seuil à
50 000 FCFA tuerait le programme.
Les sources insistent sur la fiabilité des versements comme premier critère de jugement d'un
programme par les affiliés : **ne jamais manquer une échéance annoncée.**

## L6 — Portail du parrain

**Statut : ✅ VALIDÉE (Maxime, 2026-08-17)** · Priorité : **Should** · Effort : **M**

Page dédiée : son lien, le nombre de clics, d'inscriptions, d'activations, les gains acquis, en
attente et versés, et l'historique. **Mobile-first**, comme le reste (décision E1).

**Analyse commerciale.** La transparence en temps réel est ce qui distingue un programme suivi d'un
programme abandonné. Effort modéré, et cela réduit mécaniquement les sollicitations de support
(« combien j'ai gagné ? »).

**Piste d'approfondissement.** Faire du **commerçant lui-même un parrain par défaut** : un bouton
« parraine un autre commerçant » dans son application, avec son lien pré-rempli, partageable en un
geste sur WhatsApp. Coût quasi nul une fois L1-L6 en place, et c'est le canal le plus naturel — un
commerçant satisfait parle à d'autres commerçants du même marché.

---

**Inventaire des candidates : clos.** Domaines A à L validés, passe proactive P1-P4 validée.
Prochaine étape : `modularisation`.
