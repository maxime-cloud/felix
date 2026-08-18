# Modules — [Nom du projet]

Découpage au **niveau fonctionnel/métier uniquement** — aucune structure de dossiers, aucun
découpage de fichiers : c'est le travail de l'agent de codage.

## Modules

### [Nom du module]
- **Rôle métier** : ...
- **Type** : isolé / semi-isolé
- **Fonctionnalités couvertes** : ... (renvoi vers Fonctionnalites.md)
- **Dépend de** : ... (aucune si isolé)
- **Est utilisé par** : ...
- **Effort agrégé** : ... (somme des estimations S/M/L des fonctionnalités couvertes)

## Cartographie des dépendances

| Module | Dépend de | Type |
|---|---|---|
| ... | ... | isolé / semi-isolé |

**Dépendances circulaires détectées** : aucune / [décrire + correction proposée]
(une dépendance circulaire est un défaut de découpage à corriger, pas une réalité à documenter)

## Ordre de construction proposé

1. [Module] — pourquoi en premier (tout en dépend / effort faible / débloque l'usage du MVP)
2. ...

Croisé avec : effort (S/M/L), contenu de MVP.md si déjà défini.
