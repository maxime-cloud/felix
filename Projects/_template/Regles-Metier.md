# Règles métier — [Nom du projet]

**Destiné à l'agent de codage.** Les règles sont formulées en **invariants testables**, pas en
prose : chacune doit pouvoir devenir un test sans réinterprétation.

> Écrire « le plafond de remise est recalculé côté serveur au moment de l'écriture, et une valeur
> supérieure est rejetée », pas « il faut faire attention aux remises ».

---

## Format

Chaque règle :
- **R[n]** — énoncé impératif et vérifiable
- **Pourquoi** — la conséquence si elle est violée
- **Où** — l'entité ou l'opération concernée
- **Source** — la décision d'origine (`Decision.md`, fonctionnalité, contrainte externe)

---

## 1. Règles d'intégrité des données
- **R1** — ...
  **Pourquoi :** ... · **Où :** ... · **Source :** ...

## 2. Règles d'argent
*(Tout ce qui touche aux montants, remises, encaissements, reversements. Les invariants d'argent se
revérifient toujours côté serveur, jamais depuis une saisie ou un dialogue.)*

## 3. Règles de cycle de vie / transitions d'état
*(Quels états existent, quelles transitions sont permises, laquelle déclenche quoi.)*

## 4. Règles de permissions
*(Qui peut faire quoi, et ce qui est refusé même à un administrateur.)*

## 5. Règles imposées par une contrainte externe
*(Renvoient à `Contraintes-Techniques.md` §1.)*
