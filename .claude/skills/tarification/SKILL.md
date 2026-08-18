---
name: tarification
description: Structuration des offres/paliers d'abonnement à partir des fonctionnalités validées, des coûts d'infrastructure et d'API externes identifiés dans Architecture.md, et des prix observés dans le benchmark concurrentiel. À utiliser une fois architecture-integrations terminé, ou si Maxime pose une question sur les prix/paliers/offres à tout moment.
---

# Skill : Tarification

## Quand ce skill s'applique

- `architecture-integrations` est terminé — c'est le déclencheur naturel (les coûts variables des
  services externes y sont identifiés, et ils conditionnent les paliers).
- Maxime pose une question sur les prix, les paliers, ce qui devrait être gratuit vs payant.

Si `Fonctionnalites.md` n'a pas encore de fonctionnalités validées, ou si
`Benchmark-Concurrents.md` n'a pas de section "fourchette de prix observée", reviens d'abord vers
ces skills — structurer une tarification sans ces deux bases produit un résultat arbitraire.

## Méthode

1. **Repartir du benchmark** — relis la fourchette de prix observée et la structure de paliers
   des concurrents (nombre de paliers, ce qui différencie chaque palier, présence ou non d'un
   essai gratuit / freemium). Ne pas la copier telle quelle, mais s'en servir de point de repère
   réaliste pour le secteur.
2. **Trier les fonctionnalités validées par palier** — typiquement 2 à 4 paliers pour un premier
   lancement (au-delà, la grille devient illisible pour un client PME) :
   - Ce qui doit être dans TOUS les paliers (le cœur de la proposition de valeur — sans ça, le
     produit ne se vend pas)
   - Ce qui pousse vers un palier supérieur (fonctionnalités identifiées comme leviers de
     monétisation dans leur triptyque d'analyse)
   - Ce qui reste en option/à la carte si pertinent (ex: SMS supplémentaires, utilisateurs
     supplémentaires)
3. **Poser les questions de structuration avec Maxime**, une à la fois :
   - Facturation par organisation, par utilisateur/siège, ou hybride (base + par siège) ?
   - Essai gratuit, freemium limité, ou aucun des deux ?
   - Palier d'entrée pensé pour quelle taille de PME (nombre d'employés/de rendez-vous/de
     transactions typique) ?
   - Tarifs en FCFA ou multi-devise dès le départ (cohérent avec la décision billing/mobile money
     déjà actée pour ce projet si elle existe) ?
4. **Intégrer les coûts variables** — reprends dans `Architecture.md` les coûts d'infrastructure
   et d'API externes identifiés (SMS, WhatsApp, appels d'API facturés à l'usage, stockage) et
   estime le coût variable par client pour chaque palier. **Un palier dont le coût variable
   dépasse le prix est une erreur à détecter ici, pas après le lancement** — signale-le
   explicitement à Maxime et propose une correction (quota inclus, refacturation à l'usage, prix
   relevé).
5. **Vérifier la cohérence avec le triptyque commercial** — chaque fonctionnalité placée en
   palier payant supérieur doit avoir un triptyque qui le justifie (levier de monétisation
   explicite) ; sinon, questionner ce placement avec Maxime plutôt que de le fixer par défaut.

## Mise à jour des fichiers

Mets à jour `Projects/<slug>/Modele-Tarification.md` : un tableau paliers × fonctionnalités
incluses, la logique de facturation (organisation/siège/hybride), la politique d'essai, et les
tarifs si Maxime les a déjà en tête (sinon, laisser en `Questions-Ouvertes.md` s'il veut y
réfléchir plus tard sans bloquer le reste du cadrage). Coche l'item 7 de `Progress.md` quand la
grille de paliers est complète et cohérente avec les fonctionnalités validées.

## Sortie

Une fois la grille posée : "La tarification est structurée. On passe au modèle de données ?" →
bascule vers le skill `donnees-et-roles`.
