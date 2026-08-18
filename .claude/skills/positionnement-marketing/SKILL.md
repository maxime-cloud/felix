---
name: positionnement-marketing
description: Analyse de différenciation et de positionnement — en quoi le produit se distingue des concurrents (prix, fonctionnalités, cible), quels problèmes il résout vraiment, pourquoi il devrait exister. À utiliser juste après que le benchmark concurrentiel et l'approfondissement de la vision (cadrage, Temps 2) sont terminés, avant de générer les fonctionnalités.
---

# Skill : Positionnement Marketing

## Quand ce skill s'applique

- Juste après `benchmark-concurrents` et le Temps 2 de `cadrage` — déclencheur naturel.
- Maxime pose une question sur la différenciation, le pricing relatif, ou "pourquoi ça
  marcherait".

Placé volontairement **avant** `fonctionnalites` : ce positionnement doit informer l'analyse
commerciale de chaque fonctionnalité qui suivra, pas être fait après coup dans le vide.

## Méthode

1. **Le "pourquoi"** — pourquoi ce produit devrait exister maintenant, pour cette cible.
   Distingue une bonne réponse ("les outils existants ratent X, notre cible fait encore Y à la
   main") d'une réponse faible ("parce que c'est un marché porteur" — ça, c'est déjà couvert par
   l'étude de marché de Maxime, pas le rôle de ce skill).
2. **Les problèmes réellement résolus** — dresse une liste concrète et assez complète des
   problèmes que la solution de Maxime cherche à résoudre (pas juste 1-2, un vrai inventaire),
   en t'appuyant sur `Idee.md` et en posant les questions qui manquent une à la fois.
3. **Différenciation face au benchmark** — reprends `Benchmark-Concurrents.md` et confronte,
   point par point :
   - Sur le **prix** : où se situerait Maxime par rapport à la fourchette observée, et pourquoi.
   - Sur les **fonctionnalités** : qu'est-ce que Maxime propose que personne du benchmark ne
     fait (vraie différenciation), et qu'est-ce qui n'est qu'un alignement sur l'existant (pas
     une différenciation, juste un prérequis pour être crédible).
   - Sur la **cible** : est-ce que Maxime vise un segment que les concurrents étudiés négligent
     (ex: PME camerounaises spécifiquement, vs des outils pensés pour un marché occidental) ?
4. **Sois honnête si la différenciation est faible.** Si après ce travail la différenciation
   tient surtout à la localisation/adaptation locale plutôt qu'à autre chose, dis-le clairement —
   ce n'est pas forcément un problème (une bonne adaptation locale est une vraie valeur), mais ça
   ne doit pas être présenté comme plus que ce que c'est.

## Mise à jour des fichiers

Consigne tout dans `Projects/<slug>/Positionnement.md`. Ce fichier n'est **pas figé** : il sera
repris et approfondi plus tard par `analyse-approfondie` une fois les fonctionnalités et la
tarification connues — note-le en tête de fichier pour que ce ne soit pas pris pour une version
finale. Coche l'item 3 de `Progress.md` une fois le premier passage complet.

## Sortie

"Positionnement posé — [1-2 lignes de synthèse]. On passe aux fonctionnalités, avec ça en tête ?"
→ bascule vers `fonctionnalites`.
