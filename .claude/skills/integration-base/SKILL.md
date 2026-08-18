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
