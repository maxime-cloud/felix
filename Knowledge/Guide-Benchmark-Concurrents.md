# Guide du Benchmark Concurrentiel — Méthodologie

Utilisé par le skill `benchmark-concurrents`. Objectif : construire une vraie base de
connaissance sur ce que des produits existants font concrètement, pour poser des questions
pertinentes à Maxime et nourrir la génération de fonctionnalités — jamais pour juger si le
marché existe (ça, c'est déjà fait, ce n'est pas le rôle de Felix).

## Architecture en trois volets

Le benchmark n'est pas une recherche unique mais trois travaux distincts, menés par trois
sous-agents :

| Sous-agent | Périmètre | Ce qu'il apporte |
|---|---|---|
| `chercheur-mondial` | Le monde entier | L'état de l'art du secteur, les standards de fonctionnalité, les fourchettes de prix de référence |
| `chercheur-local` | Le périmètre défini par Maxime | Les concurrents réellement rencontrés sur le terrain, y compris non-numériques |
| `arbitre-pertinence` | — | Tranche si les acteurs mondiaux comptent pour ce projet, et extrait ce qu'il faut en garder même s'ils ne comptent pas |

Les deux chercheurs reçoivent **exactement les mêmes consignes de fond** — mêmes champs, même
exigence de navigation réelle, même règle anti-invention. Seul le périmètre change. C'est ce qui
rend les deux rapports comparables.

## Pourquoi l'arbitrage est indispensable

Un SaaS pour PME camerounaises n'est pas forcément en concurrence avec un leader mondial du même
secteur : si celui-ci n'accepte pas le mobile money, ne fonctionne pas en connexion instable, ou
facture à un tarif hors de portée de la cible, ce n'est pas un concurrent — le traiter comme tel
fausserait tout le positionnement et rendrait le verdict de différenciation artificiellement
sévère.

Mais l'inverse est un piège symétrique : écarter les acteurs mondiaux d'un revers de main ferait
perdre des standards de fonctionnalité que les utilisateurs attendent implicitement, des bonnes
pratiques d'ergonomie, et des erreurs documentées à ne pas répéter. D'où le troisième volet, qui
extrait ces enseignements **indépendamment** du verdict de concurrence.

## Sélection des produits

- **Établis** — acteurs installés ou dominants sur le segment le plus proche de l'idée.
- **Émergents** — produits récents (typiquement moins de 3 ans) qui gagnent du terrain :
  mentions récentes, comparatifs "alternatives à X", levées de fonds, présence croissante dans
  les résultats. Ils prennent souvent des paris produit plus risqués que les établis — utile pour
  repérer des différenciateurs émergents plutôt que des standards déjà connus.

Si le secteur est trop de niche pour trouver 5+5 produits comparables sur un périmètre, élargir à
des produits adjacents (même mécanique métier dans un secteur voisin) plutôt que d'inventer des
concurrents — et le dire explicitement à Maxime.

## Navigation réelle, pas de résumé

Les grilles tarifaires et les listes de fonctionnalités sont fréquemment chargées en JavaScript
ou masquées derrière un sélecteur de plan qu'il faut cliquer. Un extrait de moteur de recherche
donne une image approximative et souvent périmée. Les sous-agents doivent donc **ouvrir les pages
et lire ce qui s'y trouve réellement** — via l'extension Chrome de Claude en priorité, ou le MCP
Playwright à défaut.

Si aucun outil de navigation n'est disponible, le signaler à Maxime plutôt que de compenser
silencieusement par de la recherche générique.

## Ce qu'il faut extraire, par produit

Nom, URL, année de lancement approximative, fonctionnalités clés (ce que le produit fait, pas son
slogan), offre et tarifs (paliers, inclus, essai gratuit), cible, intégrations, ce qui semble
différenciant, marchés réellement desservis. Pour le volet local, ajouter l'**adaptation locale
observée** (mobile money, langue, connexion instable, tarification adaptée au pouvoir d'achat).

**Règle stricte** : n'affirmer jamais qu'un produit a une fonctionnalité, un prix ou une
caractéristique sans l'avoir réellement vu. Une information inaccessible se note « non trouvé »,
jamais une estimation plausible.

## Fraîcheur

Le benchmark porte une date. Au-delà de 4 semaines, il doit être rafraîchi avant d'être réutilisé
par une étape aval — les tarifs et les fonctionnalités concurrentes changent, et une donnée
périmée se propage silencieusement jusqu'à « La vérité difficile » et à la tarification. Le skill
signale ce rafraîchissement à Maxime plutôt que de le faire en silence.

## Après le benchmark

Retour au skill `cadrage` (Temps 2) pour approfondir l'idée **à la lumière de ce qui a été
trouvé** — des questions informées par les écarts et opportunités identifiés, pas de nouvelles
questions génériques.
