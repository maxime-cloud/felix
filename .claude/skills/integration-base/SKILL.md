---
name: integration-base
description: Génère les documents de handoff vers ai-builder-saas — la liste d'outils recommandés pour ce SaaS précis (Tools.md) et le guide précisant quels fichiers de Output/ donner à l'agent de codage, quoi ajouter au CLAUDE.md du projet ai-builder-saas, et quels fichiers ne pas confier (Fichiers-Pour-Agent.md). À utiliser une fois la PRD confirmée conforme par Maxime.
---

# Skill : Intégration Base

## Quand ce skill s'applique

- Maxime a confirmé que la PRD correspond au produit voulu (fin de `redaction-prd`) —
  déclencheur unique. C'est la toute dernière étape du parcours.

Consulte `Knowledge/Reference-Base-SaaS.md` avant de commencer — c'est le résumé de ce qu'ai-
builder-saas contient déjà (stack, fonctionnalités du socle, fichiers clés). Ne recommande jamais
un outil ou une fonctionnalité déjà couverte par le socle sans le signaler explicitement comme
doublon.

## Étape 1 — Outils recommandés (`Tools.md`)

Pour ce SaaS précis (pas génériquement pour tous les projets de Maxime), recherche et recommande
les outils pertinents en plus de ce qu'ai-builder-saas fournit déjà — reporte-toi à
`Reference-Base-SaaS.md` pour savoir ce qui est déjà couvert (ex: PostHog déjà en place pour
l'analytics, Semgrep/npm audit/OWASP ZAP déjà en place pour la sécurité automatisée). Regarde ce
que des SaaS comparables (voir `Benchmark-Concurrents.md`) utilisent comme outillage, et propose
ce qui est réellement adapté à la stack (TanStack Start, Convex, Better Auth) — pas une liste
générique copiée d'un article. Pour chaque outil proposé :
- Ce qu'il apporte que le socle ne couvre pas déjà
- Pourquoi il est pertinent pour ce projet précis (pas juste "c'est populaire")
- Si un outil du socle existant pourrait suffire à la place, le dire plutôt que d'ajouter une
  dépendance en plus

## Étape 2 — Guide de handoff (`Fichiers-Pour-Agent.md`)

Détermine, parmi tous les documents produits (`Output/<slug>/` en entier, plus tout fichier de
`Projects/<slug>/` jugé utile), lesquels l'agent de codage doit réellement recevoir pour travailler
efficacement dans ai-builder-saas, et lesquels sont uniquement utiles à Maxime (ex:
`La-Verite-Difficile.md`, `Positionnement.md` — utiles pour la réflexion produit de Maxime, pas
pour coder). Rédige :
1. **Fichiers à donner à l'agent** — liste précise avec, pour chacun, ce qu'il apporte
   concrètement à l'agent (ex: `Brief-Agent-Codeur.md` en premier message, puis
   `Modele-Donnees-Technique.md` avant d'écrire le schéma Convex, etc.). `Modules.md` et
   `Architecture.md` en font partie, sans exception : `Modules.md` définit les unités de
   délégation (on confie un module à l'agent, pas une liste de fonctionnalités en vrac), et
   `Architecture.md` porte les contraintes des services externes — celles qu'il ne doit surtout
   pas découvrir seul en cours de développement, quand elles coûtent le plus cher.
2. **Extrait à ajouter au `CLAUDE.md` d'ai-builder-saas** — quelques lignes prêtes à copier-coller
   qui indiquent à l'agent où trouver ces fichiers et dans quel ordre les consulter, cohérentes
   avec les règles déjà présentes dans le `CLAUDE.md` d'ai-builder-saas (ne les duplique pas, ne
   les contredis pas)
3. **Fichiers à ne PAS confier à l'agent** — avec la raison (bruit inutile, information
   stratégique non pertinente pour le code, risque de le distraire de la PRD)

## Mise à jour des fichiers

Écrit `Output/<slug>/Tools.md` et `Output/<slug>/Fichiers-Pour-Agent.md`. Coche l'item 14 de
`Progress.md`. Vérifie l'item 15 (`Questions-Ouvertes.md` vide) une dernière fois.

## Sortie

Une fois les deux fichiers générés : résume à Maxime où trouver l'ensemble des documents dans
`Output/<slug>/`, et rappelle-lui l'extrait à coller dans le `CLAUDE.md` d'ai-builder-saas avant
de lancer son agent de codage dessus. C'est la fin du parcours pour ce projet.

## Documents de handoff technique (ajout août 2026)

En plus de `Tools.md` et `Fichiers-Pour-Agent.md`, ce skill produit **quatre documents** qui
existent pour empêcher l'agent de codage de redécider ce qui est déjà tranché :
`Contraintes-Techniques.md` · `Regles-Metier.md` · `Glossaire.md` · `Pieges-A-Eviter.md`

Leur rôle, leur structure et leur critère de qualité sont décrits dans
`Knowledge/Guide-Documents-Livrables.md`. **Lis-le avant de les produire.**

**Méthode.** Ces documents se sont remplis au fil du projet dans `Projects/<slug>/` — ici on les
**consolide** vers `Output/<slug>/`, on ne les invente pas. Lance le sous-agent
**`redacteur-handoff`** : il travaille dans un contexte séparé et repère les contradictions qu'un
auteur ne voit plus dans son propre dossier. Traite son rapport (informations manquantes,
contradictions, contraintes à rafraîchir) avant de clore le skill.

**Ce qu'on ne donne PAS à l'agent de codage**, et à préciser dans `Fichiers-Pour-Agent.md` :
`Benchmark-Concurrents.md` et les fichiers de vérification concurrentielle (ils ont nourri
`Pieges-A-Eviter.md`, leur détail est du bruit pour coder), `Journal.md`, `Questions-Ouvertes.md`
non résolues, et `La-Verite-Difficile.md` — ce dernier sert à décider, pas à construire.

**Contrôle avant de clore :** chaque contrainte externe porte sa source et sa date ; chaque outil
écarté porte sa raison ; chaque règle métier est formulée en invariant testable.

**Source de la section « à ajouter au CLAUDE.md »** de `Fichiers-Pour-Agent.md` : la section 6 de
`Projects/<slug>/Contraintes-Techniques.md`, remplie au fil de l'analyse. Ne la reconstitue pas de
mémoire — reprends-la, et vérifie que chaque règle y tient en une ou deux phrases et s'applique
partout. Une règle longue ou situationnelle appartient à `Regles-Metier.md`, pas au CLAUDE.md.
