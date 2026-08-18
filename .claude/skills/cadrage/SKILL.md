---
name: cadrage
description: Cadrage de la vision d'un projet SaaS — extraction de l'idée, vérification de dispersion, problème résolu, cible, proposition de valeur, périmètre. À utiliser dès que Maxime évoque une NOUVELLE idée de SaaS (crée automatiquement le dossier projet), ou pose une question sur le "pourquoi" du produit, sa cible, ce qu'il inclut ou exclut. Toujours consulter en tout début d'analyse d'un projet, avant benchmark-concurrents et fonctionnalites.
---

# Skill : Cadrage

## Quand ce skill s'applique

- Maxime décrit une idée qui ne correspond à aucun projet dans `Projects/` → **bootstrap d'abord**.
- Question sur le problème résolu, la cible, la proposition de valeur, le scope IN/OUT, les
  objectifs du produit.
- Maxime doute de la pertinence d'une direction ("est-ce que ça a du sens d'ajouter... ?").
- Retour depuis `benchmark-concurrents` pour approfondir la vision à la lumière du benchmark.

## Étape 0 — Bootstrap d'un nouveau projet

1. Propose un slug court (kebab-case) basé sur le nom du projet, ex : `saas-salon-beaute`.
2. Copie la structure de `Projects/_template/` vers `Projects/<slug>/`.
3. Mets à jour `Projects/_current.md` avec ce slug.
4. Initialise `Journal.md` avec la date et un résumé d'une phrase de l'idée de départ.
5. Enchaîne directement sur l'étape 1 — ne demande pas confirmation pour créer le dossier, fais-le
   et continue naturellement la conversation.

## Étape 1 — Extraction & vérification de dispersion

Les descriptions de départ de Maxime sont en général déjà détaillées, avec une vision claire du
quoi et du comment. **Ne repose jamais une question dont la réponse est déjà dans ce qu'il vient
de donner.** Avant toute question :

1. Relis sa description et extrait tout ce qui répond déjà aux points de l'interview
   (problème, cible, JTBD, proposition de valeur, rôles, contraintes...) — remplis `Idee.md`
   directement avec ce qui est déjà là.
2. Vérifie la **cohérence/dispersion** de l'idée : est-ce qu'elle poursuit un seul objectif clair
   pour une cible identifiable, ou est-ce que plusieurs directions peu reliées sont mélangées
   (ex: un outil de gestion de salon qui inclut aussi un module de comptabilité générale
   multi-secteur ET un réseau social pour clients — trois produits en un). Si ça semble dispersé,
   dis-le clairement et précisément (montre QUOI te semble éclaté, pas juste "c'est trop vague"),
   propose un recadrage, et laisse Maxime trancher — ne décide jamais à sa place.
3. Ne pose des questions que sur les vrais trous restants, dans l'ordre de l'interview ci-dessous.

## Interview de cadrage — deux temps

### Temps 1 — avant le benchmark (le socle minimal pour savoir quoi rechercher)

1. **Le problème** — Quelle tâche/douleur concrète ce produit résout-il ? Pour qui précisément
   (quel métier, quelle taille d'entreprise) ? Comment ces gens font-ils aujourd'hui sans le
   produit (cahier papier, Excel, WhatsApp, rien du tout) ?
2. **Le déclencheur (JTBD)** — Formuler avec Maxime : *"Quand [situation], le gérant veut
   [action], afin de [résultat]."* Un JTBD par rôle utilisateur principal.
3. **La proposition de valeur** — En une phrase, qu'est-ce que ce produit permet de faire que
   l'utilisateur ne pouvait pas bien faire avant ? Si la réponse est floue, creuse — c'est le
   pivot de tout le reste du cadrage.

Dès que ces trois points sont clairs, **passe la main au skill `benchmark-concurrents`** — pas
besoin d'aller plus loin dans l'interview avant d'avoir cette base de comparaison réelle.

### Temps 2 — après le benchmark (approfondissement informé)

Reviens ici une fois `Benchmark-Concurrents.md` rempli. Les questions qui suivent doivent
maintenant s'appuyer sur ce qui a été trouvé (ex: *"Chez [concurrent émergent], la prise de
rendez-vous inclut un rappel automatique par SMS — c'est un axe que tu veux couvrir aussi ?"*)
plutôt que d'être génériques :

4. **Les rôles utilisateurs** — Qui utilise le produit, et est-ce qu'il y a plusieurs profils
   avec des besoins différents (ex: gérant vs employé vs client final) ?
5. **Objectifs mesurables** — Comment saura-t-on que le produit fonctionne, une fois lancé
   (nombre de rendez-vous pris, temps gagné, taux d'adoption...) ? Pas besoin d'être précis à la
   décimale, mais un ordre de grandeur oriente les priorités.
6. **Contraintes connues** — Budget de développement, délai visé, contrainte technique déjà
   actée (ex: doit tourner sur mobile bas de gamme, doit fonctionner hors-ligne par moments).
7. **Scope IN / OUT explicite** — Une fois les points précédents clairs, propose une première
   version du périmètre : ce qui est clairement dedans, ce qui est clairement dehors pour l'
   instant, et ce qui reste à trancher (→ `Questions-Ouvertes.md`).

## Mise à jour des fichiers

Après chaque échange utile, mets à jour `Projects/<slug>/Idee.md` (structure déjà présente dans
le template) et coche l'item 1 de `Progress.md` seulement quand : problème, cible, JTBD,
proposition de valeur, rôles, objectifs, contraintes et scope IN/OUT sont tous renseignés, et que
la vérification de dispersion a été faite.

## Sortie

- Dès la fin du **Temps 1** : "La base de l'idée est posée. Je pars faire le benchmark
  concurrentiel avant d'aller plus loin." → bascule vers `benchmark-concurrents`.
- Dès la fin du **Temps 2** : "La vision est complète. On regarde comment se positionner face à
  la concurrence avant les fonctionnalités ?" → bascule vers `positionnement-marketing`.
