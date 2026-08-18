---
name: fonctionnalites
description: Génération du plus grand nombre possible de fonctionnalités candidates, validation une par une avec triptyque d'analyse complet (valeur commerciale, utilité, piste d'approfondissement), en boucle jusqu'à ce que Maxime n'ait plus rien à ajouter, puis une passe proactive où Felix propose lui-même des fonctionnalités auxquelles Maxime n'aurait pas pensé. À utiliser une fois positionnement-marketing terminé. La partie la plus importante de tout le processus — priorité à la rigueur sur la vitesse.
---

# Skill : Fonctionnalités

## Quand ce skill s'applique

- `positionnement-marketing` est terminé — c'est le déclencheur naturel pour démarrer ce skill.
- Maxime propose une fonctionnalité, à tout moment.
- Maxime répond "oui" à la question de relance ("des fonctionnalités à ajouter ?") avec une liste.

Si `Idee.md`, `Benchmark-Concurrents.md` ou `Positionnement.md` ne sont pas remplis, reviens
d'abord vers ces skills — générer des fonctionnalités sans vision claire, base de comparaison, ni
positionnement produit un résultat pauvre et non justifié.

Consulte `Knowledge/Guide-Validation-Fonctionnalites.md` pour la méthodologie complète (le
triptyque d'analyse, la boucle, la règle anti-hallucination) avant de commencer.

## Étape 1 — Génération de la liste candidate

Génère le plus de fonctionnalités possible, organisées par domaine typique d'un SaaS métier :
- Cœur de métier (l'action centrale que le produit permet)
- Gestion des utilisateurs/rôles
- Gestion des données de référence (clients, produits, catalogue...)
- Planification / rendez-vous / réservation (si pertinent)
- Facturation / paiement (si pertinent)
- Reporting / tableaux de bord
- Communication / notifications
- Administration / back-office

Base-toi sur `Idee.md` (ce que Maxime veut), `Benchmark-Concurrents.md` (ce que fait l'existant)
ET `Positionnement.md` (l'angle différenciant retenu) — chaque fonctionnalité candidate doit
pouvoir se justifier par l'un de ces trois, ou plusieurs. N'ajoute pas de fonctionnalité "parce
que ça se fait en général" sans lien avec l'un d'eux.

## Étape 2 — Validation, calibrée selon la priorité

Le niveau d'analyse dépend de la priorité pressentie de la fonctionnalité. Produire quarante
analyses commerciales distinctes et sincères est impossible : au-delà d'un certain volume, elles
se ressemblent toutes et deviennent du remplissage — exactement ce que
`Knowledge/Guide-Validation-Fonctionnalites.md` interdit.

**Fonctionnalités Must et Should — triptyque complet :**
- Description fonctionnelle courte
- Rôle(s) concerné(s)
- **Analyse commerciale** — différenciation / acquisition / rétention / monétisation, en
  cohérence avec `Positionnement.md` (une fonctionnalité qui contredit le positionnement retenu
  doit être signalée comme telle)
- **Utilité** — problème résolu, fréquence d'usage estimée
- **Piste d'approfondissement** — peut-on aller plus loin, et est-ce que ça vaut le coup
- **Source** — vue chez quel(s) concurrent(s) du benchmark, ou idée originale
- **Effort** — estimation S / M / L (voir plus bas)

**Fonctionnalités Could — une ligne de justification** suffit : à quoi ça sert et pour qui. Pas
de triptyque. Si l'une d'elles remonte plus tard en Should ou Must, elle reçoit alors le
traitement complet.

**Fonctionnalités évidentes — groupées.** Les fonctionnalités standard sans enjeu de décision
(gestion CRUD des clients, des produits, du catalogue…) sont regroupées sous une seule analyse
commune plutôt que détaillées une par une. Personne n'a besoin d'une analyse commerciale
individuelle pour "modifier une fiche client".

Présente chaque fonctionnalité (ou groupe) avec son niveau de détail approprié, dans un ordre
logique par domaine. Attends la réaction de Maxime (validée / rejetée / à ajuster) avant de fixer
son statut dans le fichier — ne présume jamais son accord.

Pousse sur le flou comme d'habitude : toute fonctionnalité formulée vaguement ("dashboard
intelligent", "IA qui aide à décider") doit être reformulée en actions concrètes avant même de
recevoir son analyse.

### Estimation d'effort (S / M / L)

Chaque fonctionnalité Must et Should reçoit une estimation d'effort de développement, du point de
vue d'un développeur solo qui délègue le codage à un agent IA sur la base `ai-builder-saas` :

- **S** — quelques heures à un jour : CRUD simple, écran de liste, champ supplémentaire, ce que
  le socle couvre déjà en grande partie
- **M** — plusieurs jours : logique métier propre, plusieurs écrans liés, calculs, une
  intégration bien documentée
- **L** — une semaine ou plus, ou risque technique réel : intégration tierce fragile,
  synchronisation, temps réel complexe, dépendance à une API mal documentée ou instable

L'effort ne détermine pas seul la priorité, mais il la corrige : une fonctionnalité à impact
moyen et effort S mérite souvent de passer avant une fonctionnalité à impact élevé et effort L
dans un MVP. Signale explicitement à Maxime tout croisement de ce type — c'est exactement le
genre d'arbitrage qu'un développeur solo ne peut pas se permettre de rater.

## Étape 3 — Boucle de relance (Maxime)

Une fois toutes les fonctionnalités candidates traitées, demande explicitement : *"Est-ce qu'il y
a des fonctionnalités que tu voudrais ajouter ?"*

- Si Maxime donne une liste : chaque fonctionnalité reçoit le même triptyque complet (fais une
  recherche si besoin pour étayer l'analyse commerciale/utilité — ne l'invente jamais), puis
  passe par la même validation individuelle.
- Répète cette question après chaque lot traité.
- La boucle se ferme uniquement quand Maxime dit explicitement qu'il n'a plus rien à soumettre.

## Étape 4 — Passe proactive de Felix

Une fois la boucle de Maxime fermée, ne t'arrête pas là. Prends le temps de penser au-delà de ce
qui a été discuté : à partir de `Benchmark-Concurrents.md` (ce que d'autres font que personne n'a
mentionné ici) et de `Positionnement.md` (ce qui renforcerait la différenciation), propose
toi-même des fonctionnalités auxquelles Maxime n'a probablement pas pensé. Même triptyque
complet, même présentation détaillée, même validation individuelle — la seule différence est la
source (`Felix (proactif)` plutôt que Maxime ou le benchmark direct). Ne force pas un nombre
minimum : mieux vaut 2-3 propositions solides et bien justifiées qu'une longue liste creuse.

Si Maxime valide une ou plusieurs de ces propositions, redemande une dernière fois s'il a
d'autres idées suite à ça avant de considérer que cette étape est close.

## Priorisation

Une fois une fonctionnalité validée, tague-la MoSCoW (Must/Should/Could/Won't) avec la
justification d'impact qui découle de son triptyque d'analyse. Si la liste "Must" dépasse ce qui
semble raisonnable pour un premier lancement, dis-le à Maxime et propose de reclasser certains
items en Should.

## Mise à jour des fichiers

Mets à jour `Projects/<slug>/Fonctionnalites.md` en continu, un statut explicite par
fonctionnalité (`proposée` / `validée` / `rejetée` / `à ajuster`) — ne supprime jamais une
fonctionnalité rejetée, garde-la avec sa raison. Consigne toute fonctionnalité validée comme
décision dans `Decision.md`. Coche l'item 4 de `Progress.md` seulement quand la boucle Maxime ET
la passe proactive de Felix sont toutes deux closes, et que toutes les fonctionnalités validées
"Must" ont leur triptyque complet.

## Sortie

Une fois tout fermé : "Plus aucune fonctionnalité à traiter — [N] validées, [N] écartées. On
découpe tout ça en modules ?" → bascule vers le skill `modularisation`.
