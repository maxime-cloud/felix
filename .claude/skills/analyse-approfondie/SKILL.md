---
name: analyse-approfondie
description: Vérification de cohérence croisée, comparaison finale approfondie avec la concurrence, génération de "La vérité difficile" (ce qui n'est pas unique / ce qui reste distinctif), questions dures sur la viabilité, proposition d'un MVP à vraie valeur, puis boucle de décision (continuer vers la PRD / retour aux fonctionnalités / retour au cadrage). À utiliser une fois fonctionnalites, tarification, donnees-et-roles, parcours-utilisateur et saas-essentiels terminés. Jamais de réponse rapide ici — une vraie recherche et un vrai temps d'analyse.
---

# Skill : Analyse Approfondie

## Quand ce skill s'applique

- Tout le reste est posé (fonctionnalités, tarification, données, parcours, saas-essentiels) —
  déclencheur naturel.
- Retour ici après un passage par `fonctionnalites` ou `cadrage` suite à une boucle précédente
  (voir étape 5).
- Maxime demande explicitement "est-ce que ce produit a du sens ?" ou équivalent.

**Pas de réponse rapide sur ce skill.** Consacre une analyse réellement approfondie — un vrai
plan de vérification et une vraie recherche, pas une synthèse improvisée en une passe. Consulte
`Knowledge/Guide-Analyse-Approfondie.md` avant de commencer.

## Étape 1 — Cohérence croisée (jamais supposée)

Lance le sous-agent **`verificateur-coherence`** sur le dossier du projet. Il vérifie
mécaniquement que les documents ne se contredisent pas (fonctionnalités ↔ données,
fonctionnalités ↔ parcours, tarification ↔ fonctionnalités, rôles, positionnement ↔
fonctionnalités, MVP ↔ fonctionnalités, questions ouvertes bloquantes) et rend, pour chaque
problème, sa gravité et l'étape de retour recommandée.

**Si des incohérences bloquantes ou à corriger sont remontées** :
1. Présente-les à Maxime, groupées par étape de retour, avec la modification précise à apporter
   pour chacune.
2. Décide de l'étape à laquelle relancer l'analyse (`cadrage`, `fonctionnalites`,
   `modularisation`, `architecture-integrations`, `tarification`, `donnees-et-roles` ou
   `parcours-utilisateur`) — si plusieurs étapes sont concernées, reprends à la plus amont,
   puisque les corrections en amont se propagent en aval.
3. Annonce clairement à Maxime : à quelle étape on repart, ce qui doit y être corrigé, et que
   l'analyse approfondie reprendra ensuite là où elle s'est arrêtée.
4. Relance effectivement le skill concerné, log les corrections dans `Changelog.md`.
5. **Une fois les corrections faites, reviens ici et relance `verificateur-coherence`** — pas la
   totalité de l'analyse approfondie, juste cette vérification. Quand elle passe, l'analyse
   continue à l'étape 2.

Les incohérences mineures sont notées dans `Questions-Ouvertes.md` sans bloquer la suite.

**Vérification incrémentale** : `verificateur-coherence` est aussi lancé plus tôt dans le
parcours (à la fin de `donnees-et-roles` et de `parcours-utilisateur`), pour attraper les
problèmes quand ils coûtent peu à corriger. Ce passage-ci est le contrôle final, pas le premier.

## Étape 2 — Comparaison finale approfondie

Reprends `Benchmark-Concurrents.md` et `Positionnement.md`, mais avec la liste **définitive** de
fonctionnalités et la tarification réelle en main (contrairement au premier passage de
`positionnement-marketing`, qui travaillait sur une vision encore provisoire). Recherche à
nouveau si besoin — les infos du premier benchmark peuvent avoir vieilli ou ne plus suffire vu le
niveau de détail atteint. Détermine, fonctionnalité par fonctionnalité et palier par palier, ce
qui tient la comparaison et ce qui ne la tient pas.

## Étape 3 — "La vérité difficile"

**Lance d'abord le sous-agent `critique-produit`.** Il n'a pas participé à la conception du
produit — c'est précisément sa valeur. Il attaque activement la différenciation, la valeur des
fonctionnalités Must, les hypothèses tacites, et formule le scénario d'échec le plus probable.
Tu ne peux pas produire ce regard toi-même de façon fiable : tu as proposé une partie des
fonctionnalités, et personne ne juge sévèrement son propre travail.

Intègre son rapport, puis génère et **affiche intégralement dans la conversation** (pas juste
"c'est dans le fichier"), en plus de l'écrire dans `Projects/<slug>/La-Verite-Difficile.md` :

```
# La vérité difficile — [Nom du projet]

## Ce qui n'est pas unique dans ce SaaS
- [fonctionnalité/aspect] — déjà fait par [concurrent(s)], au même niveau ou mieux

## Ce qui reste réellement distinctif
- [fonctionnalité/aspect] — pourquoi c'est vraiment différent, et quels concurrents du
  benchmark ne le font PAS (citation obligatoire)

## Hypothèses non vérifiées traitées comme des faits
- [hypothèse] — ce sur quoi elle repose, ce qui la confirmerait

## Scénario d'échec le plus probable
- ...
```

**Règle stricte sur la colonne "distinctif"** : chaque ligne doit citer explicitement les
produits du benchmark qui ne font pas cette chose. Une affirmation de différenciation non sourcée
bascule automatiquement dans "pas unique" — c'est la seule protection contre l'auto-complaisance.

## Étape 4 — Questions dures

À partir de ce qui ressort de l'étape 3, pose les questions qui restent réellement ouvertes et
qui n'appartiennent qu'à Maxime — une à la fois. Exemples de nature (pas un script figé, adapte
au projet réel) :
- Un concurrent fait déjà mieux sur l'essentiel de ce qui n'est pas distinctif — Maxime veut-il
  quand même continuer, et si oui sur quelle base (exécution, marché local, prix, autre) ?
- Quelle échelle vise le produit (ordre de grandeur d'utilisateurs/mois) — ça conditionne des
  choix d'architecture et de coût que Maxime devra valider avec son agent de codage ensuite.
- Faut-il pouvoir analyser le comportement des utilisateurs finaux (au-delà de ce qui est déjà
  dans `Exigences-Non-Fonctionnelles.md`) ?
- Toute autre question de fond sur le produit qui n'a pas de réponse évidente ou objective.

## Étape 5 — MVP à vraie valeur

Propose un MVP délibérément limité mais qui délivre une vraie valeur — pas une coquille vide, pas
non plus toutes les fonctionnalités "Must". Le test à appliquer à chaque fonctionnalité pour
décider si elle est dans ce MVP : *si je l'enlève, est-ce que la promesse centrale du produit
s'effondre ?* Si non, elle attend une version suivante, même si elle est taguée "Must" dans
`Fonctionnalites.md` (le MoSCoW indique l'importance générale, pas ce qui rentre dans le tout
premier MVP). Documente les limites assumées explicitement — ce que ce MVP ne fait volontairement
pas encore.

Écris ça dans `Projects/<slug>/MVP.md` et présente-le à Maxime.

## Étape 6 — Boucle de décision

Demande explicitement : *"On continue vers la PRD, on retouche les fonctionnalités, on retourne au
cadrage, ou on arrête ce projet ?"*

- **Continuer vers la PRD** → validation officielle de la direction. Passe au skill
  `redaction-prd`.
- **Retour aux fonctionnalités** → redirige vers `fonctionnalites`, en résumant précisément quoi
  ajuster (issu des étapes 3/4/5) plutôt qu'un renvoi vague.
- **Retour au cadrage** → demande explicitement à Maxime ce qui ne va pas ou quel aspect du
  produit a été oublié, avant de rediriger vers `cadrage`. Ne présume jamais la raison toi-même.
- **Arrêter ce projet** → issue pleinement légitime, pas un échec. Si "La vérité difficile" et
  le rapport de `critique-produit` montrent que le produit n'a pas de valeur distinctive
  suffisante, ou que le scénario d'échec est très probable, **c'est à toi de le proposer
  explicitement** — ne laisse pas Maxime investir des semaines de développement sans avoir posé
  cette option sur la table. Si elle est retenue : consigne la décision et ses raisons dans
  `Decision.md`, note dans `Journal.md` ce qui pourrait rouvrir le dossier plus tard (un
  changement de marché, une fonctionnalité repensée), et archive le projet en l'état. Le travail
  d'analyse reste disponible si Maxime veut y revenir.

## Mise à jour des fichiers

`La-Verite-Difficile.md` et `MVP.md` à chaque passage (écrase la version précédente, mais logue
le changement dans `Changelog.md`). Coche l'item 12 de `Progress.md` seulement quand toutes les
étapes sont faites ET que Maxime a choisi "continuer vers la PRD".
