---
name: benchmark-concurrents
description: Recherche concurrentielle en trois volets lancés via sous-agents — un volet mondial, un volet restreint au périmètre géographique du projet, puis un arbitrage de pertinence. Navigation réelle sur les sites (MCP Playwright ou extension Chrome), jamais de résumé de moteur de recherche. À utiliser juste après que le Temps 1 du skill cadrage a posé le problème/la cible/la proposition de valeur d'un nouveau projet. Ce n'est PAS une étude de marché — c'est un benchmark produit.
---

# Skill : Benchmark Concurrents

## Quand ce skill s'applique

- Juste après que `cadrage` (Temps 1) a posé le problème, la cible et la proposition de valeur
  d'un nouveau projet.
- Si Maxime demande explicitement "à quoi ressemble l'existant sur ce secteur ?"
- **Rafraîchissement obligatoire** : si le benchmark existant date de plus de 4 semaines et que
  l'analyse reprend, voir la section "Fraîcheur" plus bas.

Consulte `Knowledge/Guide-Benchmark-Concurrents.md` pour la méthodologie détaillée.

## Avant de commencer : vérifier l'outillage de navigation

Ce benchmark exige une **navigation réelle** sur les sites — ouvrir les pages, cliquer sur les
sélecteurs de plan tarifaire, lire ce qui est effectivement affiché. Un extrait de moteur de
recherche ne suffit pas : les grilles de prix et les listes de fonctionnalités sont souvent
chargées en JavaScript ou masquées derrière une interaction.

Deux options, dans l'ordre de préférence :
1. **L'extension Chrome de Claude** — permet de naviguer et d'agir directement dans le navigateur
   de Maxime, y compris sur des pages qui résistent au scraping automatisé.
2. **Le MCP Playwright** (`claude mcp add playwright npx @playwright/mcp@latest`) — navigation
   pilotée, adaptée quand l'extension n'est pas disponible.

Si aucun des deux n'est disponible, dis-le explicitement à Maxime avec la commande à lancer, et
**ne compense pas par de la recherche web générique** sans l'avoir signalé comme une dégradation
de la fiabilité.

## Étape 1 — Définir le périmètre géographique

Avant de lancer quoi que ce soit, confirme avec Maxime le périmètre visé pour ce projet précis
(pays, région, continent). Ne le suppose pas à partir des projets précédents : un même
développeur peut viser le Cameroun sur un projet et l'Afrique centrale sur un autre.

## Étape 2 — Lancer les deux recherches en parallèle

Lance **en parallèle** deux sous-agents, avec exactement les mêmes consignes de fond (mêmes
champs à extraire, même exigence de navigation réelle, même règle anti-invention) — seul le
périmètre change :

- **`chercheur-mondial`** — 5 établis + 5 émergents, sans restriction géographique
- **`chercheur-local`** — 5 établis + 5 émergents dans le périmètre défini à l'étape 1, y compris
  les acteurs peu référencés et les **concurrents non-numériques** (cahier papier, Excel partagé,
  groupe WhatsApp) qui sont souvent les vrais concurrents à battre sur ces marchés

Transmets à chacun : l'idée du projet, la cible, la proposition de valeur, et pour le second, le
périmètre géographique. Si le chercheur local ne trouve pas 10 acteurs, c'est une information en
soi — ne le pousse pas à compléter avec des produits mondiaux.

## Étape 3 — Arbitrage de pertinence

Une fois les deux rapports rendus, lance **`arbitre-pertinence`** avec les deux rapports et le
contexte du projet. Son rôle : déterminer si les concurrents mondiaux sont réellement des
concurrents pour ce projet (disponibilité, adéquation économique et opérationnelle, présence
effective sur le marché visé) — et surtout, **extraire ce qu'il ne faut pas perdre d'eux même
quand ils ne sont pas pertinents** (standards du secteur attendus implicitement, bonnes pratiques
d'ergonomie, erreurs à ne pas répéter).

C'est ce troisième volet qui évite les deux erreurs symétriques : traiter un leader mondial
inaccessible à la cible comme un concurrent direct, ou balayer son expérience produit sous
prétexte qu'il n'opère pas sur le marché.

## Étape 4 — Consolidation

Rassemble les trois rapports dans `Projects/<slug>/Benchmark-Concurrents.md` : les fiches
mondiales, les fiches locales, la section concurrents non-numériques, les verdicts de pertinence,
les enseignements à conserver, puis une synthèse (fonctionnalités quasi universelles,
différenciateurs rares, fourchettes de prix mondiale et locale, et une conclusion nette sur qui
sont les vrais concurrents à battre).

Note en tête de fichier la **date de réalisation du benchmark** — elle sert au contrôle de
fraîcheur.

## Fraîcheur — obligation de rafraîchir

Au démarrage de toute session sur un projet existant, compare la date du benchmark à la date du
jour. **Si plus de 4 semaines se sont écoulées**, signale-le explicitement à Maxime dès le début
de la session :

> "Le benchmark de ce projet date du [date], soit [N] semaines. Les tarifs et fonctionnalités des
> concurrents ont pu changer. Je relance une vérification avant de continuer."

Puis relance effectivement les recherches (au minimum une vérification ciblée des tarifs et des
fonctionnalités clés des concurrents jugés pertinents) avant d'utiliser ces données dans une
étape aval. Ce n'est pas optionnel : `positionnement-marketing`, `tarification` et
`analyse-approfondie` s'appuient toutes sur ces chiffres, et une donnée périmée s'y propage
silencieusement.

Log le rafraîchissement dans `Changelog.md`.

## Mise à jour des fichiers

`Benchmark-Concurrents.md` au fur et à mesure. Coche l'item 2 de `Progress.md` quand les trois
volets sont consolidés.

## Sortie

"Benchmark terminé — [1-2 lignes des enseignements clés, dont le verdict sur la pertinence des
acteurs mondiaux]. On reprend le cadrage pour finir la vision avec ça en tête ?" → retour au
skill `cadrage` (Temps 2).
