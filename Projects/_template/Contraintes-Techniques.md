# Contraintes techniques & décisions d'outillage — [Nom du projet]

**Destiné à l'agent de codage.** Tout ce qui est écrit ici doit avoir été **vérifié à une source**,
jamais supposé. Chaque fait porte sa date de vérification. Ce qui n'est pas vérifié est marqué
comme tel.

> ⚠️ **Ne pas redécider ce qui est ici.** Si une contrainte semble fausse, la vérifier à la source
> citée avant de s'en écarter — et signaler l'écart, ne pas le contourner silencieusement.

Se remplit **au fil de l'eau**, dès qu'une contrainte ou une décision d'outil apparaît. Jamais
reconstitué en fin de parcours.

---

## 1. Contraintes externes non négociables

*(Une sous-section par service externe ou domaine réglementaire. Format : contrainte · détail ·
conséquence pour le code · date de vérification · source.)*

### 1.1 [Service externe]
| Contrainte | Détail | Conséquence pour le code |
|---|---|---|
| ... | ... | ... |

### 1.2 Juridique / conformité
- ...

### 1.3 Terrain (connectivité, usages locaux, langue, moyens de paiement)
- ...

---

## 2. Décisions d'outillage — quoi, et pourquoi

### 2.1 Retenus
| Outil | Rôle | Pourquoi |
|---|---|---|
| ... | ... | ... |

### 2.2 Écartés — ne pas les réintroduire
| Écarté | Raison |
|---|---|
| ... | ... |

*(Cette section vaut souvent plus que la précédente : sans elle, un agent de codage « optimise » et
réintroduit ce qui a été éliminé.)*

### 2.3 À trancher, non décidé
- ...

---

## 3. Sécurité — règles d'implémentation
*(Isolation multi-locataire, périmètre des accès, invariants à revérifier côté serveur,
journalisation.)*

---

## 4. Ordres de dépendance à respecter
*(Enchaînements qui ne sont pas des préférences mais des conditions de correction.)*
- **[X] avant [Y]** — parce que ...

---

## 6. Règles pour le `CLAUDE.md` de l'agent de codage

Directives **courtes et toujours applicables**, à porter dans le `CLAUDE.md` du projet de code —
pas seulement dans un document de spécification qu'on lit une fois. Une règle qui doit être
respectée à *chaque* fichier écrit doit vivre là où l'agent la relit à chaque session.

Critère d'entrée : la règle tient en une ou deux phrases, s'applique partout, et sa violation ne se
voit pas à la relecture d'un diff.

- ...
