---
name: donnees-et-roles
description: Modélisation des données (entités, champs, relations) et des rôles/permissions d'un SaaS. À utiliser dès que la conversation touche à la structure des données, aux entités métier, au multi-tenant, aux rôles utilisateurs ou aux permissions. S'appuie sur les fonctionnalités déjà listées par le skill fonctionnalites.
---

# Skill : Données & Rôles

## Quand ce skill s'applique

- Discussion sur les entités du produit (ex: "qu'est-ce qu'un rendez-vous doit contenir ?").
- Questions de rôles, permissions, cloisonnement multi-tenant.
- Le skill `analyse-approfondie` en a besoin comme prérequis avant la comparaison finale.

## Méthode

1. **Repère les entités dans `Fonctionnalites.md`.** Chaque fonctionnalité Must/Should implique
   généralement une ou plusieurs entités de données — extrait-les une par une plutôt que de
   partir d'une page blanche.

   **Puis reprends les entités révélées par les intégrations** listées dans `Architecture.md`
   (section 5) : logs d'exécution de workflow, états de synchronisation, files d'attente,
   identifiants de corrélation avec les systèmes externes. Elles ne découlent d'aucune
   fonctionnalité visible, donc elles sont faciles à oublier — et leur absence bloque le
   développement au moment de brancher l'intégration.

   **Rattache chaque entité à son module propriétaire** (`Modules.md`) : un seul module est
   responsable de son cycle de vie, les autres la lisent. Sans ça, on obtient un modèle de données
   où tout référence tout, et le découpage en modules ne tient plus.

2. **Pour chaque entité**, détermine avec Maxime :
   - Les champs essentiels (nom, type conceptuel : texte, nombre, date, choix limité, montant...)
   - Obligatoire ou optionnel
   - Les relations avec les autres entités (1-1, 1-N, N-N) et leur sens métier
   - Si l'entité est propre à une organisation (cloisonnement multi-tenant) ou globale

   Ne descends pas encore au niveau du type SQL/Prisma exact ici — reste au niveau conceptuel,
   la traduction technique se fait dans `redaction-prd`.

3. **Rôles et permissions.** Pour chaque rôle identifié dans `cadrage` :
   - Quelles entités peut-il créer / lire / modifier / supprimer ?
   - Y a-t-il des restrictions au niveau des champs (ex: un employé voit le rendez-vous mais pas
     le prix payé) ?
   - Un utilisateur peut-il changer de rôle, ou appartenir à plusieurs organisations ?

4. **Multi-tenant.** Vérifie explicitement : est-ce que deux clients du SaaS de Maxime (deux
   entreprises différentes qui utilisent le produit) doivent être totalement cloisonnés l'un de
   l'autre ? C'est presque toujours "oui" pour un SaaS B2B — le confirmer explicitement évite un
   trou de sécurité découvert trop tard.

5. **Recherche si besoin.** Si le secteur a des règles métier spécifiques et non triviales (ex:
   règles de facturation, de stock, de réglementation locale), vérifie rapidement plutôt que de
   supposer.

## Vérification incrémentale

Avant de passer à la suite, lance le sous-agent **`verificateur-coherence`**. À ce stade, il
vérifie surtout que chaque fonctionnalité Must/Should manipulant de l'information persistante a
bien ses entités, et que les rôles utilisés existent dans `Idee.md`. Corriger une entité
manquante maintenant coûte quelques minutes ; la découvrir en `analyse-approfondie` implique de
retravailler plusieurs documents à la fois.

## Mise à jour des fichiers

Mets à jour `Projects/<slug>/Modele-Donnees.md`, une section par entité + une section rôles avec
une matrice simple rôle × action (créer/lire/modifier/supprimer) par entité sensible, et le module
propriétaire de chaque entité. Coche l'item 8 de `Progress.md` quand toutes les entités des
fonctionnalités MVP **et celles révélées par les intégrations** sont couvertes, et que la matrice
de permissions existe pour chaque rôle.

## Sortie

Enchaîne vers `parcours-utilisateur` pour cartographier comment ces données sont réellement
manipulées à l'écran, dans quel ordre, par qui.
