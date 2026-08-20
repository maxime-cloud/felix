# Modules — ContexFly

Découpage **fonctionnel/métier** des fonctionnalités validées. Aucun choix d'implémentation ici —
ni structure de dossiers, ni découpage de fichiers, ni noms de composants : c'est le travail de
l'agent de codage.

Les modules sont les **unités de délégation** à l'agent de codage, et les nœuds internes du schéma
d'architecture à venir.

---

## Vue d'ensemble

| # | Module | Type | Effort agrégé |
|---|---|---|---|
| **M1** | Socle multi-activités | isolé | L |
| **M2** | Catalogue & vitrine | semi-isolé | L |
| **M3** | Canal WhatsApp | isolé (adaptateur) | L |
| **M4** | Conversations & inbox | semi-isolé | M |
| **M5** | Agent de vente | semi-isolé | L |
| **M6** | Commandes & livraison | semi-isolé | M |
| **M7** | Paiement & encaissement | semi-isolé | L |
| **M8** | Fidélisation & campagnes | semi-isolé | M |
| **M9** | Onboarding & activation | semi-isolé | M |
| **M10** | Abonnement ContexFly | semi-isolé | M |
| **M11** | Croissance & parrainage | isolé | M |
| **M12** | Mesure & reporting | isolé en écriture | M |
| **M13** | Back-office ContexFly | semi-isolé | M |
| **M14** | **Application installable & hors ligne** | transverse | L |

---

## M1 — Socle multi-activités
**Type : isolé.** Ne dépend d'aucun module ; **tout dépend de lui.**
**Couvre :** G1 (compte → activités, quota par abonnement), G2 (points de vente), G3 (équipe et
permissions).
**Rôle métier :** porter la structure `compte → activité → membre` et l'**isolation des données**.
C'est le module qui définit ce que « appartenir à un commerçant » veut dire.
**Sortantes :** aucune. **Entrantes :** tous les autres modules.
⚠️ **À construire en premier et correctement.** Une clé d'activité oubliée dans une entité se
paie en reprise sur tout le reste. R8, R9 et R10 vivent ici.

## M2 — Catalogue & vitrine
**Type : semi-isolé** — dépend de M1.
**Couvre :** B0 (enregistrement assisté par agent + mémoire de champs apprise), B1, B2 (stock par
variante **et** par point de vente), B3 (synchro catalogue WhatsApp natif), B4, **P4** (lien produit
partageable qui ouvre WhatsApp).
**Rôle métier :** la connaissance produit. C'est ce qui rend l'agent de vente capable de répondre.
**Entrantes :** M5, M6, M7, M8.
*Note :* P4 est ici parce que c'est une **projection publique en lecture seule** du catalogue. Elle
crée un point d'entrée de conversation, mais ne connaît pas les conversations.

## M3 — Canal WhatsApp
**Type : isolé — c'est un adaptateur vers Meta.** Dépend de M1.
**Couvre :** H1 (Embedded Signup, connexion du WABA), envoi et réception de messages, gestion de la
fenêtre de service 24 h, catégories et approbation de templates, **limitation de débit sortante**,
traitement de l'erreur `131049`, **F7** (pédagogie des règles WhatsApp).
**Rôle métier :** être le **seul composant qui parle à Meta**, et le seul endroit où les règles
WhatsApp sont appliquées.
**Entrantes :** M4, M5, M8, M9.
⚠️ **Aucun autre module ne doit appeler l'API Meta directement.** C'est ce qui rend R17, R18 et
R20 vérifiables en un seul endroit.

## M4 — Conversations & inbox
**Type : semi-isolé** — dépend de M1, M3.
**Couvre :** A6 (bascule IA↔humain), A7 (cycle de vie, historique comme contexte), E1 (inbox
mobile-first), E2 (indicateur de fenêtre 24 h), E3 (panneau contact), E4, E5, E6.
**Rôle métier :** le fil de discussion et sa supervision humaine.
**Entrantes :** M5, M12.
*Note d'absence de cycle :* A6 **écrit un état** (« ce contact est en mode humain ») que M5 lit.
M4 n'appelle jamais M5. La dépendance est à sens unique.

## M5 — Agent de vente
**Type : semi-isolé** — dépend de M2, M4, M6, M7, M8 (par ses outils) et M3 (pour émettre).
**Couvre :** A1, A2 (panier), A4 (configuration), A5 (accès aux données), A9 (escalade), A10 (notes
vocales), A11 (FR/EN/pidgin), A12 (verrou de conformité), A13 (horaires), A14 (mode absence piloté
depuis WhatsApp), **P1** (mode brouillon), **P2** (apprentissage des reprises humaines).
**Rôle métier :** le raisonnement. C'est le module qui décide *quoi faire*, jamais celui qui écrit
directement en base — il agit par des outils étroits exposés par les autres modules.
**Entrantes :** aucune. **C'est le module le plus dépendant, et personne ne dépend de lui.**
⚠️ **Effort L, risque le plus élevé du projet**, et son coût d'inférence n'est pas modélisé (Q13).

## M6 — Commandes & livraison
**Type : semi-isolé** — dépend de M1, M2.
**Couvre :** C1 (objet Commande), C2 (statuts), C3 (export fiche livreur), C4 (adresse ville +
quartier + repère), C5 (zones et frais), C6 (contacts secondaires).
**Rôle métier :** transformer une intention en objet durable et livrable.
**Entrantes :** M5, M7, M8, M12.
⚠️ **C1 est le pivot du produit.** Sans lui : pas de relance, pas de fidélisation, pas de
reporting, pas de taux d'autonomie.

## M7 — Paiement & encaissement
**Type : semi-isolé** — dépend de M1, M6.
**Couvre :** A3 (page panier éditable puis paiement), D1 (moteur à 5 politiques dont l'acompte),
D2, D3 (Notch Pay Sync), D4 (confirmation automatique), D5 (plafond de remise côté serveur), D6
(réconciliation et solde), D7 (remboursement).
**Rôle métier :** l'argent. R1 à R5 vivent ici.
**Entrantes :** M5, M9, M12, M13.
⚠️ **D5 doit exister avant que M5 puisse proposer une remise** (R1). Et **ContexFly ne détient
jamais les fonds** (R3).

## M8 — Fidélisation & campagnes
**Type : semi-isolé** — dépend de M6 (historique d'achat), M3 (envoi), M2 (stock pour P3).
**Couvre :** F1 (segments), F2 (remise automatique en conversation), F3 (automatisations
pré-écrites), F4 (campagnes opt-in), F5 (consentement), F6 (constructeur générique — `Could`),
**P3** (alerte de retour en stock).
**Rôle métier :** faire revenir un client déjà connu.
**Entrantes :** M5 (l'outil de remise lit le palier de fidélité ici).
⚠️ **F5 avant F4**, sans exception (R18).

## M9 — Onboarding & activation
**Type : semi-isolé** — dépend de M1, M3, M7.
**Couvre :** H2 (onboarding conversationnel + miroir de valeur), H3 (compte de démo pré-rempli),
H4 (tutoriel vidéo), H5 (KYC commerçant), H6 (état d'avancement de l'installation).
**Rôle métier :** amener un commerçant de l'inscription à sa première commande encaissée.
**Entrantes :** M11, M12.
⚠️ **C'est le module qui porte la seule barrière durable du projet.** Son risque n'est pas dans le
code mais dans la validation Meta, hors du contrôle de Maxime (Q22).

## M10 — Abonnement ContexFly
**Type : semi-isolé** — dépend de M1, M3 (prélèvement Mobile Money via le rail de M7).
**Couvre :** D8 (paliers, prélèvement, relance, suspension), **L3** (liens et codes de réduction
sur l'abonnement).
**Rôle métier :** faire payer le commerçant.
**Entrantes :** M11, M13.
⚠️ **Les paliers et les prix ne sont pas tranchés** — renvoyés à `tarification` après modélisation
du coût d'inférence (Q13).
*Note :* L3 est ici et non dans M11 parce qu'une réduction **modifie le prix de l'abonnement** ; le
confondre avec la remise commerçant (F2) serait une erreur de modèle (voir `Glossaire.md`).

## M11 — Croissance & parrainage
**Type : isolé.** Observe des événements de M9 (activation) et M10 (abonnement) ; **personne ne
dépend de lui.**
**Couvre :** L1 (programme de parrainage), L2 (attribution serveur-à-serveur), L4 (anti-fraude et
clawback), L5 (versement en Mobile Money), L6 (portail parrain).
**Rôle métier :** acquérir des commerçants par des tiers.
⚠️ **Retirable sans casser le produit** — donc parfaitement reportable après le MVP.

## M12 — Mesure & reporting
**Type : isolé en écriture** — lit M4, M6, M7, M9, M3 ; n'écrit dans aucun.
**Couvre :** I1 (tableau de bord commerçant), I2 (taux d'autonomie), I3 (consommation et coût).
**Rôle métier :** rendre mesurable la promesse du produit.
⚠️ **I3 doit être instrumenté dès le premier jour, même sans écran** — c'est ce qui alimentera la
modélisation du coût d'inférence dont dépend toute la tarification (Q13).

## M13 — Back-office ContexFly
**Type : semi-isolé** — dépend de M1, M7, M9, M10.
**Couvre :** J1 (administration des comptes, instruction du KYC), J2 (supervision des paiements et
des litiges).
**Rôle métier :** l'exploitation quotidienne côté ContexFly.
⚠️ **L'option B en fait un vrai produit interne**, pas un accès superutilisateur bricolé.

---

## Cartographie des dépendances

*(Complétée le 2026-08-19 depuis `architecture-integrations`. Diagramme : `Architecture.md` §9.6.)*

**Aucun cycle.** Toutes les dépendances vont dans un seul sens.

| Module | Dépend de | Dont dépendent |
|---|---|---|
| **M1** Socle multi-activités | — | M2, M3, M4, M6, M7 (et indirectement tout) |
| **M3** Canal WhatsApp | M1 | M4, M8, M9 |
| **M2** Catalogue | M1 | M5, M6 |
| **M4** Conversations & inbox | M1, M3 | M5, M12 |
| **M6** Commandes & livraison | M1, M2 | M5, M7, M8, M12 |
| **M5** Agent de vente | M2, M4, M6 | — |
| **M7** Paiement | M1, M6 | M9, M10, M13, M12 |
| **M9** Onboarding | M3, M7 | M13 |
| **M8** Fidélisation | M3, M6 | — |
| **M10** Abonnement | M7 | M11 |
| **M13** Back-office | M7, M9 | — |
| **M12** Mesure | M4, M6, M7 *(lecture seule)* | — |
| **M11** Parrainage | M10 | — |

```
M1 Socle
 ├─→ M2 Catalogue ──────────────┐
 ├─→ M3 Canal WhatsApp ───┐     │
 │        ↑               │     │
 ├─→ M4 Conversations ────┘     │
 │        ↑                     │
 ├─→ M6 Commandes ←─────────────┘
 │        ↑
 ├─→ M7 Paiement
 │        ↑
 ├─→ M8 Fidélisation
 │        ↑
 └─→ M5 Agent de vente  (dépend de M2, M3, M4, M6, M7, M8 — personne n'en dépend)

M9 Onboarding   → M1, M3, M7
M10 Abonnement  → M1, M7
M11 Croissance  → observe M9, M10        (isolé)
M12 Reporting   → lit M3, M4, M6, M7, M9 (isolé en écriture)
M13 Back-office → M1, M7, M9, M10
```

**Aucun cycle.** Deux points qui auraient pu en créer, et pourquoi ils n'en créent pas :
- **M4 ↔ M5.** La bascule IA↔humain (A6) **écrit un état** que M5 lit ; M4 n'appelle jamais M5.
- **M5 ↔ M8.** L'agent appelle un outil de M8 pour connaître le palier de fidélité ; M8 ne déclenche
  jamais l'agent — les campagnes passent par M3, pas par M5.

---

## Ordre de construction

1. **M1** — socle multi-activités. Tout en dépend, et le rétrofit coûte plus cher que la
   fonctionnalité elle-même (G1).
2. **M3** et **M2** en parallèle — le canal et le catalogue ne dépendent que du socle.
3. **M4** et **M6** — conversations et commandes.
4. **M5** et **M7** — l'agent et le paiement, les deux plus coûteux. Ils arrivent en quatrième
   position **par nécessité, pas par confort** : l'agent a besoin du catalogue et des commandes
   pour avoir des outils à appeler.
5. **M9, M8, M10, M13** — onboarding, fidélisation, abonnement, back-office.
6. **M12** et **M11** — mesure et parrainage, en lecture seule sur le reste.

⚠️ **Alerte de séquencement : M9 (onboarding) est en position 5 dans l'ordre technique, alors que
c'est la seule barrière durable du produit et que sa dépendance externe — l'App Review Meta — est
la plus longue de tout le projet.**
**→ La démarche administrative Meta doit démarrer au jour 1**, pendant qu'on construit M1. Le code
de M9 arrivera bien assez tôt ; l'approbation Meta, non.

| Vague | Modules | Pourquoi |
|---|---|---|
| **1** | **M1** | Tout en dépend. Une clé d'activité oubliée ici se paie partout |
| **2** | **M3**, **M2** | Parallélisables. Le canal et la connaissance produit ne se connaissent pas |
| **3** | **M4** | A besoin du canal |
| **4** | **M6** | A besoin du catalogue |
| **5** | **M7** | A besoin des commandes |
| **6** | **M5** | A besoin de tout ce qui précède pour avoir des outils à appeler |
| **7** | **M9**, **M10** | Rendent le produit vendable |
| **8** | **M8**, **M12** | Ont besoin d'un historique de commandes pour avoir du sens |
| **9** | **M13**, **M11** | Exploitation et croissance |

### ⚠️ Deux observations à porter à `MVP.md`

**1. Le chemin critique vers « un commerçant encaisse sa première commande » traverse sept modules**
— M1 → M3 → M2 → M4 → M6 → M7 → M5 — dont **cinq des six efforts L du projet**. C'est l'arbitrage
central du MVP, et il ne se règle pas ici.

**2. M5 est dernier dans l'ordre de dépendance, mais c'est le plus risqué et son coût est inconnu.**
Attendre la vague 6 pour découvrir que le coût d'inférence rend le modèle tarifaire intenable
(Q13) serait une erreur coûteuse.
→ **Recommandation : construire très tôt une tranche verticale minimale de M5** — un seul type de
question, sur un catalogue de trois produits — uniquement pour **mesurer le coût réel d'une
conversation**. Pas pour livrer, pour savoir. C'est quelques heures qui peuvent éviter de
reconstruire le modèle économique après trois semaines.


---

## Rattachement des fonctionnalités ajoutées après le découpage initial

⚠️ **Corrigé le 2026-08-19.** Les domaines N, ainsi que I4, H7, B5, K1 et A8, avaient été validés
**après** la modularisation et n'appartenaient à aucun module. Or les modules sont les unités de
délégation à l'agent de codage : une fonctionnalité sans module n'est jamais construite.

| Fonctionnalité | Module | Pourquoi |
|---|---|---|
| **N1** second routeur de webhooks (WABA ID) | **M3** | Entrée du canal WhatsApp |
| **N2** administration des templates | **M3** | Les templates appartiennent au WABA |
| **N3** file d'attente d'onboarding + compteur 7 j | **M9** | Contrainte d'activation |
| **N4** 🔴 agrégateur de réponse (1 message/tour) | **M3** | S'applique à **tout** envoi, pas seulement à l'agent |
| **N5** état « retenu par Meta » | **M3** | Machine à états du message sortant |
| **N6** ré-hébergement et compression des médias | **M3** | Entrée et sortie du canal |
| **N7** transcription vocale (X13) | **M3** | Traitement d'un message entrant |
| **N8** coffre de secrets par activité | **M1** | Transverse, adossé au socle multi-activités |
| **N9** vérification du moyen de paiement Meta | **M9** | Étape bloquante d'onboarding |
| **N10** santé de connexion et reconnexion | **M3** + alerte **M9** | Détection au canal, remédiation à l'onboarding |
| **N11** 🔴 verrou d'envoi (anti-double-débit) | **M7** | Concerne l'appel de paiement |
| **N12** pagination catalogue + libellé court | **M2** | Contrainte de présentation du catalogue |
| **N13** réconciliation active des paiements | **M7** | C'est P5w |
| **I4** recherche, filtres, pagination, export | **M1** *(transverse)* | S'applique à toutes les listes de tous les modules |
| **H7** support par WhatsApp | **M9** | Aide et prise en main |
| **B5** import d'une base clients | **M2** | Données de référence |
| **K1** PWA et consultation hors ligne | **M14** *(nouveau)* | Touche tous les écrans — ne peut appartenir à aucun module métier |
| **A8** relance des conversations non abouties | **M8** | C'est un envoi sortant déclenché par une règle, pas une conversation |

**Effort agrégé révisé :** M3 passe de **L** à **L+** (il porte désormais sept contraintes Meta
structurantes), M7 reste **L**, et **M14 est un L entier qui n'existait pas**.

---

## Correction de la cartographie des dépendances (2026-08-19)

Le texte descriptif des modules et le tableau divergeaient. **Le tableau et le diagramme
`Architecture.md` §9.6 font foi**, avec ces corrections :

- **M5 (agent de vente)** dépend de **M2, M4, M6** — et **non** de M3, M7, M8. L'agent lit le
  catalogue, la conversation et les commandes ; il n'appelle jamais le canal ni le paiement
  directement, il **retourne une intention** que M3 envoie et que M7 exécute.
- **M10 (abonnement)** dépend de **M7**, pas de M3.
- **M9 (onboarding)** dépend de **M1, M3, M7**.

⚠️ **L'ordre « D5 avant F2 » n'est porté par aucune arête** : D5 vit dans M7, F2 dans M8, et M8 ne
dépend pas de M7. Il n'est donc respecté que par l'ordre des vagues. **À rendre explicite dans le
brief de l'agent de codage** : *ne jamais livrer F2 (remise en conversation) avant que D5 (plafond
serveur) soit en place* — sinon un client négocie -80 % pendant la fenêtre où la règle n'existe pas.
