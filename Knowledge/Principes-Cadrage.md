# Principes de Cadrage — Référentiel Méthodologique

Ce fichier est la doctrine que tous les skills appliquent. Relis-le dès que tu hésites sur une
méthode à employer.

## 1. Chaque fonctionnalité doit servir un cas d'usage, pas l'inverse

Ne jamais lister une fonctionnalité *uniquement* parce qu'elle "existe chez les concurrents" ou
"ça fait professionnel". Le benchmark (`benchmark-concurrents`) est une source légitime
d'inspiration — mais chaque fonctionnalité qui en découle doit quand même passer la question :
*quel cas d'usage précis résout-elle pour Maxime et ses utilisateurs, et pour quel rôle ?* Un cas
d'usage trop vague ("améliorer la gestion") n'est pas actionnable ; un cas d'usage trop précis
devient une solution déguisée. Le bon niveau : observable, concret, lié à une situation vécue par
l'utilisateur cible — que l'idée vienne du benchmark ou de Maxime lui-même.

## 1bis. Le triptyque d'analyse n'est pas une formalité

Analyse commerciale, utilité, piste d'approfondissement (voir
`Knowledge/Guide-Validation-Fonctionnalites.md`) doivent être des jugements réels, pas un exercice
de remplissage. Une fonctionnalité dont le triptyque est faible doit être présentée comme telle à
Maxime, pas maquillée pour paraître plus solide qu'elle ne l'est.

## 1ter. Dispersion — un objectif clair avant tout le reste

Avant même de creuser un problème ou une cible, vérifier que l'idée de départ tient sur une
direction cohérente. Une idée qui mélange plusieurs objectifs peu reliés produit un cadrage
incohérent quel que soit le soin apporté ensuite — le recadrage se fait tôt (voir skill
`cadrage`, étape 1), jamais après coup une fois les fonctionnalités déjà listées.

## 2. Priorisation MoSCoW + impact/effort

Chaque fonctionnalité est taguée :
- **Must** : le produit n'a pas de sens sans elle (souvent : gestion des rôles, sécurité,
  l'action cœur de métier).
- **Should** : forte valeur mais contournable temporairement.
- **Could** : confort, différenciateur, mais reportable sans douleur.
- **Won't (for now)** : explicitement exclue du périmètre actuel, notée pour plus tard.

Pour arbitrer Must vs Should, croiser deux axes : est-ce que ça débloque l'usage central ou une
vente (impact), et quel est le coût de développement relatif (effort). Un MVP qui livre tout
d'un coup retarde la mise en usage réelle sans garantir que les bonnes fonctionnalités ont été
choisies — mieux vaut un socle non négociable (rôles, sécurité, action cœur de métier, une
intégration clé) enrichi ensuite par itérations.

## 3. Le socle non négociable d'un SaaS B2B

Même pour un MVP réduit, trois familles ne se négocient pas : les rôles et permissions, la
sécurité des données, et au moins une intégration/action clé qui rend le produit réellement
utilisable en conditions réelles (pas juste une démo). Un logiciel B2B est acheté par une
organisation, pas par un individu isolé — il y a toujours plusieurs utilisateurs avec des
niveaux d'accès différents, même dans une PME de 5 personnes.

## 4. Jobs To Be Done (JTBD) plutôt que personas décoratifs

Un persona ("Marie, 34 ans, gérante de salon") n'est utile que s'il est attaché à un "job" :
la tâche que l'utilisateur essaie d'accomplir, indépendamment de l'outil. Formuler systéma-
tiquement : *"Quand [situation], je veux [action], afin de [résultat attendu]."* C'est ce format
qui devient ensuite la base des user stories.

## 5. Toujours vérifier la prémisse, même après l'étude de marché

L'étude de marché de Maxime est faite en amont — on ne la refait pas. Mais au niveau du cadrage
fonctionnel, il reste utile de vérifier ponctuellement qu'une fonctionnalité envisagée répond à
un problème réellement vécu (et pas supposé) avant de la faire monter en priorité Must. Si un
doute apparaît sur ce terrain, le signaler à Maxime plutôt que de trancher à sa place — le
cadrage fonctionnel n'a pas vocation à repasser derrière l'étude de marché, seulement à
signaler les incohérences flagrantes qui apparaissent en creusant les détails.

## 6. Scope IN / scope OUT explicite

La plus grande source de dérive de projet n'est pas ce qu'on a oublié de faire, c'est ce qu'on
n'a pas explicitement décidé de ne pas faire. Chaque dossier de cadrage doit lister aussi
clairement les fonctionnalités volontairement exclues (et pourquoi) que celles qui sont incluses.

## 7. Les documents servent un objectif : nourrir un agent de codage

Toute la matière produite ici n'est pas un exercice académique — elle doit finir sous forme
exploitable par un agent IA qui va coder (Claude Code). Ça veut dire : des entités de données
précises et nommées clairement (pas de "des trucs comme ça"), des règles métier explicites, des
user stories avec critères d'acceptation vérifiables, et un scope MVP clairement délimité pour
éviter qu'un agent de codage n'improvise des décisions produit à ta place.
