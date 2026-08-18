---
name: parcours-utilisateur
description: Cartographie des parcours utilisateurs, écrans et états (chargement, vide, erreur, succès) d'un SaaS. À utiliser dès que la conversation porte sur les flux d'utilisation, l'enchaînement d'écrans, l'expérience utilisateur, ou l'onboarding. S'appuie sur les fonctionnalités et le modèle de données déjà cadrés.
---

# Skill : Parcours Utilisateur

## Quand ce skill s'applique

- Discussion sur "comment l'utilisateur fait pour..." / l'enchaînement d'actions à l'écran.
- Question sur l'onboarding, la première utilisation.
- Prérequis avant `analyse-approfondie` : au moins les parcours minimaux définis ci-dessous.

## Parcours minimaux à cartographier (jamais sauter ceux-ci)

1. **Inscription / onboarding** — du tout premier écran jusqu'au moment où l'utilisateur peut
   accomplir sa première action utile. Que voit-il s'il n'a encore aucune donnée ?
2. **Parcours de valeur principal** — l'action cœur de métier identifiée dans `cadrage`, du
   déclencheur jusqu'au résultat obtenu, pour le rôle principal.
3. **Parcours de gestion/admin** — comment un rôle avec plus de droits gère les données de
   référence, les autres utilisateurs, les paramètres.

Ajoute ensuite tout autre parcours jugé important par Maxime ou identifié comme Must dans
`Fonctionnalites.md`.

## Pour chaque parcours

1. Décris la séquence d'écrans/étapes en une liste numérotée simple (pas besoin de wireframes —
   du texte structuré suffit pour un agent de codage).
2. Pour chaque étape qui affiche des données, vérifie explicitement les états suivants et
   demande à Maxime ce qu'il attend pour chacun s'il n'est pas évident :
   - **Vide** (aucune donnée pour l'instant) — que propose l'écran de faire ?
   - **Chargement** — rien de spécial à préciser en général, mais le signaler.
   - **Erreur** (échec réseau, action refusée) — message affiché, action de secours.
   - **Confirmation** — pour toute action destructive ou irréversible (suppression, annulation,
     encaissement), une étape de confirmation est-elle nécessaire ?
3. Note les règles de navigation ou de permission qui changent le parcours selon le rôle.

## Recherche

Si un flux est spécifique à un secteur avec des conventions établies (ex: parcours de
réservation, de paiement), vérifie rapidement les pratiques courantes plutôt que d'inventer un
flux atypique sans raison.

## Vérification incrémentale

Avant de passer à la suite, lance le sous-agent **`verificateur-coherence`**. À ce stade, il
vérifie surtout que chaque fonctionnalité Must apparaît dans au moins un parcours, et que les
rôles utilisés dans les parcours existent bien. Même logique qu'après le modèle de données :
attraper l'incohérence quand elle coûte peu à corriger.

## Mise à jour des fichiers

Mets à jour `Projects/<slug>/Parcours.md`, un parcours = une section, avec la liste d'étapes et
les états couverts. Coche l'item 9 de `Progress.md` quand les 3 parcours minimaux (+ tout Must
identifié) sont cartographiés avec leurs états.

## Sortie

Une fois les parcours posés, passe (ou repasse) par `saas-essentiels` pour la revue transverse,
puis `analyse-approfondie` quand tout est prêt.
