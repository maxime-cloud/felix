---
name: redaction-prd
description: Rédaction de la PRD complète (objectifs, parcours, exigences fonctionnelles, limites du MVP, métriques, critères d'acceptation) et du document marketing final, une fois la direction validée par analyse-approfondie. Vérifie ensuite avec Maxime que la PRD correspond bien au produit voulu.
---

# Skill : Rédaction PRD

## Quand ce skill s'applique

- Maxime a choisi "continuer vers la PRD" à la fin de `analyse-approfondie` — déclencheur unique.
  Ne jamais déclencher ce skill autrement : la direction doit être officiellement validée avant
  de rédiger quoi que ce soit ici.

## Étape 1 — Rédaction de la PRD

Génère `Output/<slug>/PRD.md` à partir de tout ce qui est réellement dans `Projects/<slug>/` —
jamais d'improvisation pour combler un trou (s'il y en a un, c'est que `analyse-approfondie` a
laissé passer quelque chose, retourne-y). Structure (voir aussi
`Knowledge/Guide-Documents-Livrables.md`) :

1. **Résumé & objectifs** — ce que le produit fait, pour qui, objectifs mesurables (`Idee.md`)
2. **Positionnement** — synthèse de `Positionnement.md` + `La-Verite-Difficile.md` (ce qui est
   réellement différenciant, en toute honnêteté)
3. **Périmètre** — scope IN/OUT
4. **MVP** — contenu et limites assumées, repris de `MVP.md`
5. **Fonctionnalités** — organisées MoSCoW, avec leur triptyque résumé
6. **Modules et ordre de construction** — repris de `Modules.md` : les modules, ce que chacun
   couvre, isolé/semi-isolé, leurs dépendances et l'ordre dans lequel les construire
7. **Architecture & intégrations** — repris d'`Architecture.md` : l'inventaire des éléments
   communicants, les contraintes des services externes, et les diagrammes Mermaid **repris tels
   quels** (ils sont directement lisibles par l'agent de codage, ne les reformule pas en prose)
8. **Modèle de tarification** — grille de paliers
9. **Parcours utilisateurs** — les flux cartographiés
10. **Exigences fonctionnelles et non-fonctionnelles** — y compris sécurité/connectivité/etc.
11. **Modèle de données (vue fonctionnelle)**
12. **Métriques de succès** — comment on saura que le produit fonctionne (issu des objectifs
    mesurables de `Idee.md`, affiné si besoin avec Maxime à ce stade)
13. **Critères d'acceptation globaux** — ce qui doit être vrai pour que le MVP soit considéré
    comme livré
14. **Hypothèses & risques**
15. **Glossaire**

## Étape 2 — Document marketing

Génère `Output/<slug>/Marketing.md` : version formalisée et prête à réutiliser de
`Positionnement.md` + `La-Verite-Difficile.md` — le "pourquoi", les problèmes résolus, la
différenciation réelle (pas gonflée), un pitch court réutilisable. C'est un document honnête,
pas un document commercial enjolivé : s'il y a des limites à la différenciation, elles y restent.

## Étape 3 — Compléter les autres livrables produit

Génère aussi `Output/<slug>/User-Stories.md` (une entrée par fonctionnalité Must/Should, format
standard, critères d'acceptation), `Output/<slug>/Modele-Donnees-Technique.md` (traduction du
modèle fonctionnel en entités/champs/relations exploitables pour un schéma Prisma/Convex — voir
`Knowledge/Guide-Documents-Livrables.md`), et `Output/<slug>/Brief-Agent-Codeur.md` (résumé dense
pour démarrage rapide d'un agent de codage).

## Étape 4 — Vérification avec Maxime

Une fois les 5 documents générés, demande explicitement : *"Est-ce que ça correspond au produit
que tu veux créer ?"*

- **Oui** → coche l'item 13 de `Progress.md`, log la validation dans `Decision.md`, propose de
  passer à `integration-base`.
- **Non** → demande précisément ce qui ne va pas. Selon la réponse :
  - Si c'est un problème de fonctionnalité/priorité/détail → retour à `fonctionnalites`
  - Si c'est un problème plus profond (la vision elle-même, la cible, le problème résolu) →
    retour à `cadrage`
  - Ne choisis jamais cette redirection toi-même sans que Maxime ait précisé le problème.

## Mise à jour des fichiers

Log chaque document généré dans `Journal.md`. Toute correction demandée par Maxime à cette étape
va dans `Changelog.md`.
