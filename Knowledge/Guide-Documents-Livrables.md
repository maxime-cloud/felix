# Guide des Documents Livrables

`redaction-prd` génère les 5 premiers documents dans `Output/<slug>/`, `integration-base` génère
les 2 derniers, une fois les jalons requis atteints (voir `CLAUDE.md`). Ce fichier décrit ce que
chacun doit contenir — sers-t'en comme plan, pas comme texte à copier tel quel : le contenu vient
toujours du dossier `Projects/<slug>/`.

## 1. PRD.md — le document maître (généré par `redaction-prd`)

Structure :
1. **Résumé & objectifs** — le problème résolu, pourquoi maintenant, objectifs mesurables.
2. **Positionnement** — synthèse de `Positionnement.md` + `La-Verite-Difficile.md`, honnête sur
   ce qui est réellement différenciant et ce qui ne l'est pas.
3. **Périmètre** — scope IN détaillé, scope OUT explicite avec justification.
4. **MVP** — contenu et limites assumées, repris de `MVP.md`.
5. **Fonctionnalités** — organisées par priorité MoSCoW, chacune avec sa description
   fonctionnelle et son triptyque d'analyse (valeur commerciale, utilité) résumé en 1-2 phrases
   (pas de jargon technique ici, ce sera dans le Brief-Agent-Codeur).
6. **Modules et ordre de construction** — repris de `Modules.md` : les modules retenus, ce que
   chacun couvre, isolé ou semi-isolé, leurs dépendances et l'ordre de construction proposé. Ce
   sont les unités de délégation à l'agent de codage.
7. **Architecture & intégrations** — repris d'`Architecture.md` : l'inventaire des éléments
   communicants, les contraintes vérifiées de chaque service externe, et les diagrammes Mermaid
   repris **tels quels** (ils sont directement lisibles par l'agent de codage — ne pas les
   reformuler en prose).
8. **Modèle de tarification** — les offres/paliers définis dans `Modele-Tarification.md`.
9. **Parcours utilisateurs clés** — les flux cartographiés dans `Parcours.md`.
10. **Exigences fonctionnelles et non-fonctionnelles** — sécurité, performance, connectivité,
    conformité (issues de la checklist SaaS-Essentiels).
11. **Modèle de données (vue fonctionnelle)** — entités, relations, rôles — version lisible, pas
    encore du Prisma/Convex.
12. **Métriques de succès** — comment on saura que le produit fonctionne.
13. **Critères d'acceptation globaux** — ce qui doit être vrai pour que le MVP soit livré.
14. **Hypothèses & risques**.
15. **Glossaire**.

## 2. Marketing.md (généré par `redaction-prd`)

Version formalisée de `Positionnement.md` + `La-Verite-Difficile.md` : le "pourquoi", les
problèmes réellement résolus, la différenciation réelle, un pitch court réutilisable. Document
honnête, pas commercial-enjolivé — les limites de la différenciation y restent si elles existent.

## 3. User-Stories.md (généré par `redaction-prd`)

Une entrée par fonctionnalité Must/Should, format :

```
### [ID] Titre court
**En tant que** <rôle>, **je veux** <action>, **afin de** <bénéfice>.
**Priorité** : Must / Should / Could
**Critères d'acceptation :**
- [ ] ...
- [ ] ...
**Entités concernées** : renvoie vers Modele-Donnees-Technique.md
```

Groupées par domaine fonctionnel (ex: "Gestion des rendez-vous", "Facturation", "Administration").

## 4. Modele-Donnees-Technique.md (généré par `redaction-prd`)

Traduction du modèle fonctionnel en un format directement exploitable pour écrire un schéma
Convex/Prisma : une section par entité, avec champs (nom, type, obligatoire/optionnel, valeur par
défaut) et relations (1-1, 1-N, N-N) explicites. Pas de code généré ici — juste la matière brute,
claire et complète.

Exemple de format par entité :
```
### RendezVous
- id (uuid, PK)
- organizationId (FK → Organization, obligatoire)
- clientId (FK → Client, obligatoire)
- employeId (FK → Utilisateur, optionnel)
- dateHeure (datetime, obligatoire)
- statut (enum: planifie / confirme / annule / termine)
- creeLe, modifieLe (timestamps)
Relations : Organization 1—N RendezVous, Client 1—N RendezVous
```

## 5. Brief-Agent-Codeur.md (généré par `redaction-prd`)

Le plus court et le plus dense : conçu pour être collé directement en prompt de démarrage à un
agent de codage. Contient : résumé du produit en 3-4 phrases, scope MVP uniquement (lien vers la
PRD pour la suite), liste des entités principales, les 3-5 parcours utilisateurs non
négociables, les exigences non-fonctionnelles qui ne doivent jamais être contournées, liens vers
les autres documents pour le détail.

## 6. Tools.md (généré par `integration-base`)

Liste d'outils recommandés pour ce SaaS précis, en plus de ce qu'ai-builder-saas fournit déjà
(voir `Knowledge/Reference-Base-SaaS.md`). Pour chaque outil : ce qu'il apporte que le socle ne
couvre pas, pourquoi il est adapté à ce projet précis, et un signalement explicite si un outil du
socle pourrait suffire à la place.

## 7. Fichiers-Pour-Agent.md (généré par `integration-base`)

Guide de handoff : quels fichiers de `Output/` (et éventuellement de `Projects/`) donner à
l'agent de codage et dans quel ordre, l'extrait à ajouter au `CLAUDE.md` d'ai-builder-saas, et la
liste des fichiers à ne PAS confier à l'agent (utiles à la réflexion de Maxime, pas au code).
