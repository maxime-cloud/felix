# La vérité difficile — ContexFly

Écrit le **2026-08-19**, après le passage du sous-agent `critique-produit` — un regard adverse qui
n'a participé ni au cadrage ni à la conception. Chaque point ci-dessous a été **vérifié
indépendamment** avant d'être écrit.

---

## 0. Un manquement du benchmark, à dire avant le reste

**Le 3 juin 2026, Meta a lancé mondialement le Meta Business Agent.** Le benchmark de ce dossier a
été réalisé les **15-17 août 2026** — dix semaines après — et **ne le mentionne nulle part**.

Trois volets de recherche, quatre produits explorés en conditions réelles, et le lancement du
concurrent le plus important n'est pas remonté. C'est une défaillance de la méthode, pas un détail :
le benchmark cherchait des *produits comparables* et n'a pas cherché ce que **la plateforme
elle-même** allait faire.

**Leçon à porter dans Felix :** un benchmark doit systématiquement inclure un volet
« que fait la plateforme sur laquelle le produit repose ? ». Quand un SaaS est bâti sur WhatsApp,
Shopify ou Stripe, le concurrent le plus dangereux n'est jamais dans la liste des concurrents.

---

## 1. 🔴 Ce qui n'est plus vrai

`Positionnement.md` revendiquait : *« ce qui n'existe nulle part entre 0 et 49 990 FCFA, c'est
l'agent qui répond, qualifie, construit le panier et encaisse dans le fil WhatsApp. »*

**La première moitié de cette phrase est fausse depuis le 3 juin 2026.** Vérifié :

| Fait | Source |
|---|---|
| Lancement **mondial**, sans déploiement progressif — iOS, Android et Business Platform | Meta, 03/06/2026 |
| Répond aux questions produit, **recommande depuis le catalogue**, prend des rendez-vous, qualifie, **peut conclure la transaction**, passe la main à un humain | Meta |
| Disponible **depuis l'app WhatsApp Business**, sans développeur, sans Tech Provider, sans App Review | Meta |
| **Gratuit jusqu'au 31 juillet 2026**, puis facturé **2 $ par million de tokens** | Meta |
| Pour les petites entreprises, facturé via **WhatsApp Business Premium** | Meta |

**Correspondance directe avec des fonctionnalités déclarées « cœur de métier » :** A1 (prise de
commande), A4 (configuration), A5 (catalogue, prix), A6 (bascule IA↔humain), A9 (escalade),
A11 (bilinguisme).

### Et une lecture d'A12 qu'il faut renverser

Le dossier traite l'interdiction des IA généralistes du 15/01/2026 comme *« un cadeau de
positionnement »*. La lecture inverse est plus probable : **Meta a dégagé la couche qu'il voulait
occuper, puis l'a occupée cinq mois plus tard.** Le même acteur qui autorise aujourd'hui les agents
« au service d'un processus métier » peut resserrer cette définition quand il veut.

---

## 2. Ce qui survit, et c'est réel

**Meta ne fait pas l'argent au Cameroun.** Les paiements natifs WhatsApp ne sont vivants qu'en
**Inde, Brésil et Singapour**. Meta *guide vers* un checkout qu'il ne fournit pas ici.

Ce qui reste, vérifié et non contredit :

- **L'encaissement Mobile Money bouclé** — du lien de paiement à la confirmation automatique.
- **L'objet Commande**, établi par une double absence : **Zoko n'a aucune section « commandes »**
  (elles vivent dans Shopify) et **Ngavix a des commandes mais aucune conversation**.
- **La réconciliation, l'acompte, le reste dû, la fiche livreur** — personne ne les fait de bout en
  bout ici.
- **La remise déclenchée par l'historique d'achat, dans la conversation** — l'agent de Fiitsa n'a
  **aucune case** d'accès à l'historique de commandes : ce n'est pas absent, c'est **non
  branchable**.
- **A13/A14** — horaires de **livraison** distincts des horaires d'ouverture, mode absence imprévue
  qui change le comportement de vente, activable depuis WhatsApp. **Aucun équivalent trouvé, ni
  local ni mondial.** Effort S/M.
- **C4/C5/C6** — ville → quartier → repère, frais par zone, second numéro « ou celui d'un proche ».
- **Tout le domaine N.** La maîtrise des contraintes Meta n'a pas pu être prise en défaut. Ce n'est
  pas de la différenciation — c'est la différence entre un produit qui marche et un produit qui
  échoue en silence.

### ⭐ Un contre-argument que la critique n'a pas fait

**L'agent de Meta est plus cher que le vôtre.** À 2 $/M de tokens, une conversation de vente coûte
**≈ 0,04 à 0,24 $**, soit **24 à 144 FCFA**. Le modèle Gemini 2.5 Flash retenu ici revient à
**≈ 10 FCFA**. ContexFly opère donc sa propre inférence **2 à 14 fois moins cher** que la solution
de Meta.

Cela ne rachète pas la perte de la revendication — Meta gagne sur la friction, pas sur le prix —
mais cela signifie que **la conversation n'est pas économiquement perdue**, seulement banalisée.

---

## 3. Le repositionnement qui s'impose

> **Ancien pitch :** « un agent IA qui vend sur WhatsApp ».
> **Nouveau pitch :** « ce que WhatsApp et Meta ne feront pas ici : **l'argent et la commande** ».

Concrètement : Meta répond, ContexFly **encaisse, enregistre, réconcilie, livre et fidélise**.
C'est un produit **plus petit et différemment positionné** — mais dont la revendication résiste à
la vérification, ce que l'ancienne ne fait plus.

⚠️ **`Positionnement.md` est à réécrire avant la PRD, pas après.**

---

## 4. Le modèle économique est à l'envers

**Le chiffre de 15 000 FCFA n'est jamais passé par le skill censé le produire.**
`Modele-Tarification.md` est **un template vide**. Ce nombre était une *recommandation* issue du
benchmark ; il a ensuite servi de **donnée** à la modélisation d'inférence, au parrainage et à
toute la marge. C'est une supposition promue en fait.

Quatre défauts, tous vérifiables dans le dossier :

**a) « Conversations illimitées » à prix fixe inverse la marge.** À 20 conversations/jour :
6 000 FCFA d'inférence, 60 % de marge. **À 60/jour : ~18 000 FCFA, soit plus que l'abonnement.**
Le modèle sélectionne à l'envers — les seuls commerçants pour qui 15 000 FCFA est manifestement
rentable sont ceux qui détruisent la marge. Et le PAYG de Fiitsa, moqué comme « absurde au
volume », est en réalité **la structure qui survit au volume**.

**b) Les 10 FCFA sont un plancher, pas un coût.** Le modèle ne couvre que le chemin de vente. Il
exclut **B0** (agent de saisie + vision), **N7** (transcription), la classification d'intention, les
réessais — et surtout **P1, le mode brouillon, qui génère 100 % des réponses sans en envoyer** :
coût plein, revenu nul, pendant toute la période d'adoption. Et P1 est **Must**.

**c) « 0 % de commission » est déjà pris.** Fiitsa écrit littéralement *« 0 % de commission
Fiitsa »* sur sa page Cameroun. C'est le **troisième** argument du dossier déjà occupé par un
local, après « 0 % de marge sur tes messages » (Genuka WA). Un argument que trois acteurs
revendiquent n'est pas un argument. Et les 3 % Notch Pay étant **visibles** par construction
(R7bis), le commerçant appellera cet écart une commission quel que soit le vocabulaire.

**d) Le prix filtre la cible qu'on revendique.** `Positionnement.md` désigne « le commerçant sans
site web et sans société formelle » comme le segment le plus défendable. **Un abonnement fixe est
le pire modèle pour lui : il coûte avant de rapporter.** Fiitsa à 5 % et Ayweu à **0 % en paiement
à la livraison** sont gratuits à zéro vente. Le dossier a choisi la cible la plus pauvre **et** la
structure de prix qui la filtre — défendables séparément, contradictoires ensemble.

**e) Le parrainage ne boucle pas.** 20-30 % récurrents = 3 000-4 500 FCFA sur 15 000, contre
~9 000 FCFA de marge brute **avant** infrastructure, support, et codes de réduction cumulables.

---

## 5. Le périmètre et le calendrier

**Huit fonctionnalités en effort L**, pas six : A1, B0, D1, D3, G1, **G2** (révisé de M à L),
H1, L1 — plus **M14** (PWA) créé le 19/08. Et les 13 du domaine N ont été **validées en bloc**,
donc sans arbitrage individuel. `MVP.md` est **un template vide** : l'arbitrage qui devait couper
n'a pas eu lieu.

**La décision la plus coûteuse n'a pas été instruite.** Le stock par point de vente est entré au
MVP contre ma recommandation. Conséquence écrite dans le dossier lui-même : la ligne de stock
devient `(produit, variante, point de vente)` **par-dessus** les attributs dynamiques de B0, et
**une branche de décision s'ajoute à A1**, déjà la fonctionnalité la plus coûteuse. J'ai noté
« je le signale une fois, puis j'avance » — et j'ai avancé. Cette décision vaut probablement plus
d'une semaine sur un budget de trois.

**🔴 Le calendrier de 3-4 semaines est arithmétiquement impossible.** L'objectif est « une première
version en main d'un vrai commerçant ». Or Meta plafonne l'onboarding à **10 nouveaux clients par
7 jours glissants après App Review — et 0 avant approbation**. **Il n'existe aucun chemin vers un
vrai commerçant sans approbation Meta préalable.** Et aucun code d'encaissement n'est testable
avant signature du contrat Notch Pay Sync, qui n'est pas en libre-service.

**Scénario réaliste : 2 à 4 mois** jusqu'au premier commerçant qui encaisse réellement, si Meta et
Notch Pay disent oui du premier coup.

---

## 6. 🔴 L'angle mort : personne n'a demandé à un commerçant s'il paierait

**Nulle part dans ce dossier il n'y a un commerçant qui a dit qu'il paierait.** Les quatorze
problèmes de `Positionnement.md` sont **déduits, pas observés** — pas un entretien, pas une
citation, pas un nom. Et tout s'y adosse : la volumétrie, les 15 000 FCFA, le taux d'autonomie,
l'économie du parrainage.

Plus précisément, **le JTBD central n'a jamais été vérifié** : *« je veux qu'une commande complète
et payée arrive sans que j'aie à taper un message »*. Il est déduit d'une friction, pas d'un désir.

Or sur ce marché, **la relation *est* la vente** : on négocie, on reconnaît un habitué, on fait
crédit, on dit « je te fais un prix parce que c'est toi ». Le dossier admet ce fait par ses propres
fonctionnalités, sans jamais le nommer :

- **P1 (mode brouillon) existe parce que le commerçant ne lâchera pas.** La question suivante n'est
  jamais posée : **et s'il ne lâche jamais ?** Si P1 reste activé durablement, ContexFly est un
  assistant de frappe, pas un vendeur — coût d'inférence entier, promesse non tenue, et la
  justification du prix (« ça remplace un employé ») s'effondre.
- **D5 existe pour empêcher le client de négocier avec l'IA** — sur un marché où négocier **est**
  la façon normale d'acheter.
- **F2 automatise une remise que le commerçant accorde traditionnellement lui-même**, comme geste
  relationnel. L'automatiser peut détruire ce qui la rendait efficace.

**Symptôme le plus net : le taux d'autonomie est déclaré métrique n°1 et n'a aucune cible
chiffrée.** 40 % ? 80 % ? **Une métrique sans seuil ne peut pas échouer — donc elle ne mesure
rien.**

### L'hypothèse la plus dangereuse n'est pas Q29

Q29 (garde des fonds) est grave mais **binaire et connaissable en un e-mail déjà rédigé**, avec une
porte de sortie (l'option A, ma recommandation initiale). Un risque qui se résout par un courrier
n'est pas le risque principal.

**Le plus dangereux est l'hypothèse de demande** — et elle n'a même pas de numéro de question.

---

## 7. Ce que je recommande, sans détour

**Deux choses, une semaine chacune, avant d'écrire la PRD :**

1. **Refaire le benchmark en intégrant Meta Business Agent**, et réécrire `Positionnement.md`
   autour de « l'argent et la commande ».
2. **Trouver trois commerçants qui disent oui à un prix.** Pas un sondage — trois personnes, avec
   des noms, à qui on montre le parcours et qui répondent à « tu paierais combien pour ça ? ».

**Puis, dans l'ordre :** `tarification` pour de vrai (le skill n'a jamais tourné), avec un modèle
qui **ne soit pas illimité à prix fixe** ; puis `MVP.md`, avec une cible chiffrée pour le taux
d'autonomie et une coupe franche dans les huit efforts L.

**Ce dossier mérite d'être construit — sur un périmètre plus petit et un positionnement différent
de celui qu'il décrit aujourd'hui.**
