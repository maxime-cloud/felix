# Guide de l'Analyse Approfondie — Méthodologie

Utilisé par le skill `analyse-approfondie`. C'est le dernier filtre honnête avant que Maxime
n'engage du temps de développement réel — mieux vaut un constat dur ici qu'après des semaines de
code.

## Pourquoi "pas de réponse rapide"

Maxime a été explicite : il ne veut pas une synthèse improvisée, mais quelque chose construit sur
un vrai plan et une vraie recherche. Concrètement, ça veut dire : revérifier les faits du
benchmark plutôt que de se fier à ce qui a été noté au début (les informations peuvent avoir
changé, ou le niveau de détail atteint peut révéler des nuances ratées la première fois),
recouper plusieurs sources plutôt qu'une seule, et prendre le temps d'examiner chaque
fonctionnalité "Must" individuellement plutôt que de juger le produit dans son ensemble d'un
coup d'œil.

## Le test qui structure tout : la promesse centrale

Emprunté aux cadres actuels de validation de MVP (Lean Canvas, Value Proposition Canvas) : *"une
promesse claire, un problème résolu mieux que quiconque"*. Applique ce test à chaque
fonctionnalité candidate au MVP : *si je l'enlève, est-ce que la promesse centrale du produit
s'effondre ?* Si la réponse est non, elle n'a pas sa place dans le MVP, même si elle est taguée
"Must" dans `Fonctionnalites.md` — le MoSCoW indiquait l'importance générale pour le produit final,
pas ce qui doit exister dès le premier jour.

## Le regard adverse est délégué, pas improvisé

`analyse-approfondie` lance le sous-agent `critique-produit` avant de rédiger
`La-Verite-Difficile.md`. Ce n'est pas une formalité : Felix a lui-même proposé une partie des
fonctionnalités lors de la passe proactive, et personne ne juge sévèrement son propre travail
après des heures d'effort commun. Le sous-agent n'a pas participé à la conception — c'est toute
sa valeur.

Son rapport (différenciation attaquée avec preuves, hypothèses tacites, scénario d'échec le plus
probable) est la matière première de "La vérité difficile", pas un avis parmi d'autres.

## "La vérité difficile" — comment juger l'unicité

Pour chaque fonctionnalité/aspect du produit, pose la question dans cet ordre :
1. Est-ce que ça existe déjà, identique ou presque, chez un des 10 produits du benchmark ? →
   liste "pas unique".
2. Si non identique, est-ce une variation superficielle (même mécanique, présentation
   différente) ? → toujours "pas unique", ne pas se laisser impressionner par une UI différente.
3. Est-ce que ça résout un problème qu'aucun des concurrents pertinents ne résout, ou le résout
   d'une façon fondamentalement différente (pas juste "en mieux") ? → liste "distinctif",
   seulement si la réponse est clairement oui **et** que tu peux nommer les concurrents du
   benchmark qui ne le font pas.

**Règle de sourçage** : toute ligne de la colonne "distinctif" cite explicitement les produits du
benchmark qui ne font pas cette chose. Une affirmation non sourcée bascule automatiquement dans
"pas unique". C'est la seule protection structurelle contre l'auto-complaisance — sans elle, la
colonne "distinctif" se remplit par élimination plutôt que par preuve.

Une adaptation locale sincère (paiement mobile money, langue, connectivité) compte comme
distinctive si le benchmark montre que les concurrents étudiés ne le font pas ou mal — ce n'est
pas un critère de second rang, c'est une vraie barrière à l'entrée sur ce marché précis.

## Questions dures — ce qui les déclenche

Une question dure vaut la peine d'être posée quand :
- Elle n'a pas de réponse objective trouvable par la recherche (c'est un choix de risque, de
  positionnement, ou de préférence personnelle de Maxime).
- La réponse change significativement le MVP ou la direction du produit.
- Le constat de "La vérité difficile" rend la question incontournable (ex: peu de choses
  distinctives → la question de continuer ou non se pose légitimement).

Ne pose pas de question dure sur ce qui a déjà une réponse claire ailleurs dans le dossier — ça
diluerait le sérieux des vraies questions.

## L'arrêt est une issue légitime

La boucle de décision propose quatre issues, pas trois : continuer vers la PRD, retoucher les
fonctionnalités, retourner au cadrage, **ou arrêter le projet**. Cette dernière n'est pas un
échec de l'analyse — c'est parfois son résultat le plus utile.

Si "La vérité difficile" et le rapport de `critique-produit` convergent vers l'absence de valeur
distinctive suffisante, ou vers un scénario d'échec très probable, c'est à Felix de **proposer
explicitement l'arrêt**, pas d'attendre que Maxime y pense. Laisser quelqu'un investir des
semaines de développement sans avoir posé cette option sur la table est un manquement, pas une
délicatesse.

En cas d'arrêt : consigner la décision et ses raisons dans `Decision.md`, noter dans `Journal.md`
ce qui pourrait rouvrir le dossier plus tard, archiver le projet en l'état. Le travail d'analyse
reste disponible.

## Bookkeeping de la boucle

Chaque retour vers ce skill après un passage par `fonctionnalites` ou `cadrage` doit commencer
par lire `Changelog.md` et répondre explicitement : qu'est-ce qui a changé depuis le dernier
passage, et est-ce que ça résout ce qui posait problème ? Ne relance jamais une analyse complète
depuis zéro comme si c'était la première fois — ça userait la patience de Maxime et cacherait si
le vrai problème a été traité ou juste contourné.
