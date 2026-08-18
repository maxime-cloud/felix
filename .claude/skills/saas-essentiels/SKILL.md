---
name: saas-essentiels
description: Revue systématique des angles morts classiques d'un SaaS (facturation, sécurité, notifications, multi-tenant, conformité, connectivité...) à partir de la checklist de référence. À utiliser une fois les fonctionnalités principales et le modèle de données posés, avant de clôturer l'analyse — et à chaque fois que Maxime demande explicitement "à quoi je n'ai peut-être pas pensé".
---

# Skill : SaaS-Essentiels

## Quand ce skill s'applique

- Explicitement demandé par Maxime ("qu'est-ce que j'oublie ?").
- Automatiquement, une fois que `Fonctionnalites.md` et `Modele-Donnees.md` ont une base solide,
  avant de considérer l'analyse comme prête pour `analyse-approfondie` — ne laisse jamais l'analyse se
  clôturer sans être passé par ce skill au moins une fois.

## Méthode

1. Ouvre `Knowledge/Checklist-SaaS-Essentiels.md` — c'est la liste de référence, ne la réécris
   pas de mémoire.
2. Déroule les catégories avec Maxime **une ou deux à la fois**, jamais les 17 d'un coup. Pour
   chaque item, présente-le sous forme de question concrète adaptée à SON projet (pas la
   question générique du fichier telle quelle — reformule avec le vocabulaire de son produit).
3. Pour chaque item, obtiens une des trois issues (voir en-tête du fichier de checklist) :
   Applicable+détaillé / Écarté+justifié / À trancher (→ `Questions-Ouvertes.md`).
4. Priorise les catégories qui touchent à l'argent, aux données sensibles et à la sécurité —
   ce sont celles qu'on ne veut surtout pas découvrir après coup.
5. Garde en tête le contexte camerounais de Maxime : connectivité, mobile money, usage mobile,
   bilinguisme — ce sont des points où le réflexe "par défaut" (carte bancaire, email comme
   canal principal, etc.) ne s'applique souvent pas tel quel. Signale-le explicitement quand
   c'est pertinent plutôt que de supposer.

## Mise à jour des fichiers

Consigne chaque décision dans `Projects/<slug>/Exigences-Non-Fonctionnelles.md`, organisé selon
les mêmes catégories que la checklist de référence. Si un item révèle une fonctionnalité
manquante, ajoute-la aussi dans `Fonctionnalites.md` avec sa priorité. Coche l'item 10 de
`Progress.md` seulement quand les 17 catégories ont une issue consignée.

## Sortie

Une fois la checklist entièrement passée en revue et `Questions-Ouvertes.md` traité, propose à
Maxime de passer à `analyse-approfondie` pour la comparaison finale, "La vérité difficile" et la
décision de passer ou non à la PRD.
