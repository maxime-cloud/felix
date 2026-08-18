# Architecture & Intégrations — [Nom du projet]

Source de vérité des schémas d'interaction. Les diagrammes sont en Mermaid (versionnables,
lisibles par l'agent de codage). Un board Miro peut en être une projection — les modifications
faites sur le board ne remontent pas ici automatiquement.

**Board Miro associé** : [URL ou "non généré — MCP Miro non connecté"]

---

## 1. Inventaire des éléments qui communiquent

Granularité : une unité fonctionnelle distincte = un élément. Jamais « un système = un élément ».

| Élément | Type | Déclencheur | Reçoit | Produit | Destinataire | Si échec |
|---|---|---|---|---|---|---|
| ... | module / workflow / webhook / API externe / cron / acteur humain | ... | ... | ... | ... | ... |

---

## 2. Vue d'ensemble

```mermaid
flowchart TD
    %% modules internes, systèmes externes, et tous les flux entre eux
```

---

## 3. Diagrammes de séquence par flux critique

(au minimum : parcours de paiement de bout en bout, chaque workflow d'automatisation, chaque
chaîne de notification)

### [Nom du flux]

```mermaid
sequenceDiagram
    %% ...
```

**Contraintes portées sur ce flux** : ...

---

## 4. Contraintes externes vérifiées

(issues du sous-agent `verificateur-contraintes-externes` — jamais supposées, toujours vérifiées
dans la documentation officielle)

### [Service externe]
- **Authentification** : ...
- **Limites de débit / quotas** : ...
- **Fenêtres temporelles** : ...
- **Formats / validations préalables imposées** : ...
- **Comportement en cas d'échec** : ...
- **Coût** : ...
- **Non vérifié** : ...
- **Implication pour l'architecture** : ...

---

## 5. Entités de données révélées par les intégrations

(à reprendre dans Modele-Donnees.md — logs d'exécution, états de synchronisation, files
d'attente, identifiants de corrélation avec les systèmes externes)
- ...

---

## 6. Fonctionnalités manquantes révélées par cette phase

(remontées vers Fonctionnalites.md pour analyse complète, puis retour ici)
- ...
