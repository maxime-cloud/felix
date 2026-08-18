---
name: modularisation
description: Découpage des fonctionnalités validées en modules isolés ou semi-isolés, avec leurs dépendances et leur ordre de construction. À utiliser une fois la boucle de validation des fonctionnalités fermée (skill fonctionnalites), avant architecture-integrations. Découpage au niveau fonctionnel/métier uniquement — jamais au niveau de l'implémentation.
---

# Skill : Modularisation

## Quand ce skill s'applique

- La boucle de validation des fonctionnalités est fermée (boucle Maxime + passe proactive de
  Felix) — déclencheur naturel.
- Maxime demande comment découper le produit, ou par quoi commencer à construire.

Si `Fonctionnalites.md` n'a pas de fonctionnalités au statut « validée », reviens d'abord vers
`fonctionnalites` — on ne découpe pas une liste encore mouvante.

## Pourquoi cette étape existe

Deux raisons concrètes, à garder en tête pour ne pas la transformer en exercice théorique :

1. **Les modules sont les unités de délégation à l'agent de codage.** Maxime confie « le module
   Facturation » à Claude Code, pas une liste de 40 fonctionnalités en vrac. Sans modules, le
   développement incrémental n'est pas réellement possible.
2. **Les modules sont les nœuds internes du schéma d'architecture** qui suit. Sans eux, l'app
   serait une seule boîte opaque dans le diagramme, et celui-ci perdrait l'essentiel de sa
   valeur.

## Limite stricte : niveau fonctionnel, jamais implémentation

Un module se définit par **ce qui appartient au même domaine métier et ce qui peut évoluer
indépendamment**. Tu ne décides jamais de structure de dossiers, de découpage de fichiers, de
noms de composants ou d'organisation du code — c'est le travail de l'agent de codage, et le
contraindre ici lui nuirait sans bénéfice.

Si tu te surprends à écrire un chemin de fichier ou un nom de composant, tu es descendu trop bas.

## Méthode

1. **Regrouper par domaine métier.** Parcours `Fonctionnalites.md` et regroupe les fonctionnalités
   validées par cohérence métier : ce qui manipule les mêmes concepts, ce qui sert le même
   objectif utilisateur, ce qui évoluerait ensemble. Un module qui ne contient qu'une seule
   fonctionnalité est suspect — soit elle appartient ailleurs, soit c'est un vrai module et il
   faut le justifier.

2. **Qualifier chaque module :**
   - **Isolé** — ne dépend d'aucun autre module directement ; communique par contrat ou par
     événement ; pourrait être retiré ou remplacé sans casser le reste.
   - **Semi-isolé** — partage des entités ou lit directement dans un autre module ; la dépendance
     est assumée et documentée **dans un sens précis** (A dépend de B, jamais l'inverse).

3. **Cartographier les dépendances et traquer les cycles.** Si le module A dépend de B et B
   dépend de A, c'est un défaut de découpage — signale-le explicitement à Maxime et propose une
   correction (fusionner les deux modules, ou extraire ce qui est partagé dans un troisième
   module dont les deux dépendent). Ne laisse jamais passer une dépendance circulaire en la
   documentant simplement.

4. **Proposer un ordre de construction.** Les modules dont personne ne dépend se construisent en
   dernier ; ceux dont tout dépend se construisent en premier. Croise cet ordre avec les
   estimations d'effort (S/M/L) et le contenu de `MVP.md` s'il existe déjà : Maxime doit savoir
   par quel module commencer pour avoir quelque chose d'utilisable au plus tôt.

5. **Poser les questions restées ouvertes.** Certains découpages n'ont pas de réponse objective
   (deux fonctionnalités peuvent légitimement aller dans deux modules différents). Applique la
   règle habituelle : si tu peux trancher par le raisonnement, tranche et explique ; si c'est un
   vrai arbitrage qui appartient à Maxime, pose la question.

## Mise à jour des fichiers

Écris `Projects/<slug>/Modules.md` : une section par module (nom, rôle métier, fonctionnalités
couvertes, isolé/semi-isolé, dépendances entrantes et sortantes, effort agrégé), puis la
cartographie des dépendances et l'ordre de construction proposé. Consigne le découpage retenu
dans `Decision.md`. Coche l'item 5 de `Progress.md`.

## Sortie

"Le produit est découpé en [N] modules — [1 ligne sur le découpage et l'ordre de construction].
On passe à l'architecture et aux interactions entre systèmes ?" → bascule vers
`architecture-integrations`.
