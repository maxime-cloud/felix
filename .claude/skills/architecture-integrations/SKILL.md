---
name: architecture-integrations
description: Identification détaillée de tous les éléments qui communiquent dans et autour de l'application (modules, workflows n8n, webhooks, API externes), vérification des contraintes réelles de chaque service externe, puis génération des schémas d'interaction en Mermaid et, si le MCP Miro est connecté, sur un board Miro. À utiliser une fois le découpage en modules terminé (skill modularisation), avant tarification et donnees-et-roles.
---

# Skill : Architecture & Intégrations

## Quand ce skill s'applique

- `modularisation` est terminé — déclencheur naturel.
- Maxime pose une question sur la façon dont deux systèmes communiquent, ou sur une intégration
  externe.

Placé volontairement **avant** `donnees-et-roles` : les intégrations génèrent des entités qu'on
ne listerait jamais autrement (log d'exécution de workflow, état de synchronisation d'un webhook,
file de messages en attente, identifiant de corrélation avec un système externe). Le modèle de
données en hérite ensuite naturellement.

Consulte `Knowledge/Guide-Architecture-Integrations.md` avant de commencer.

## Étape 1 — L'inventaire des éléments qui communiquent (la partie la plus importante)

C'est le cœur du skill, et le reste n'a de valeur que si cette étape est faite sérieusement. Ne
la survole pas pour arriver plus vite aux schémas.

**Granularité exigée : chaque unité fonctionnelle distincte est un élément, pas chaque système.**
Dire « l'app parle à n8n » n'apprend rien. Il faut : *quel workflow n8n précis, déclenché par
quoi, lisant quelles données, appelant quels services, produisant quoi, et que se passe-t-il s'il
échoue*.

Recense exhaustivement :
- **Les modules internes** définis dans `Modules.md` et ce qu'ils s'échangent entre eux
- **Chaque workflow d'automatisation** (n8n ou équivalent) individuellement — un workflow = un
  élément, avec son propre déclencheur et son propre rôle
- **Chaque webhook entrant**, nommé individuellement (paiement, message reçu, statut de livraison…)
- **Chaque API ou service externe** utilisé, et pour quel usage précis (une même API peut servir
  à deux choses très différentes — les compter séparément)
- **Chaque tâche planifiée** (cron) et ce qu'elle déclenche
- **Les acteurs humains** quand ils font partie du flux (un administrateur qui valide, un client
  qui confirme un paiement sur son téléphone)

Pour chaque élément recensé, documente : nom, rôle, déclencheur, données entrantes, données
sortantes, destinataire, comportement en cas d'échec.

## Étape 2 — Vérification des contraintes réelles (jamais supposées)

Pour **chaque interaction impliquant un service externe**, lance le sous-agent
`verificateur-contraintes-externes` avant de dessiner quoi que ce soit. Il vérifie dans la
documentation officielle : authentification, limites de débit, quotas, contraintes de format,
**fenêtres temporelles**, comportement en cas d'échec, coût par appel, et exigences de validation
préalable.

C'est ce qui sépare un schéma exploitable d'un schéma inconstructible. Exemple typique : dessiner
« workflow n8n → envoie un rappel WhatsApp à J-3 » paraît impeccable, mais l'API WhatsApp Business
impose une fenêtre de 24h — passé ce délai depuis le dernier message du client, seul un template
pré-approuvé par Meta peut être envoyé. Sans cette vérification, le schéma est faux et l'erreur
n'apparaît qu'en développement, quand elle coûte cher.

Les contraintes trouvées sont **portées en notes sur le diagramme lui-même**, pas reléguées dans
un document annexe que l'agent de codage ne lira pas.

**Si une contrainte révèle une fonctionnalité manquante** (il faut administrer les templates
WhatsApp, donc il faut un écran pour ça), remonte vers `fonctionnalites` pour l'ajouter avec son
analyse, puis reviens ici. Log l'aller-retour dans `Changelog.md`.

## Étape 3 — Questions sur les points non abordés

L'inventaire fait toujours apparaître des zones jamais discutées : que se passe-t-il si un
paiement est confirmé mais que le webhook n'arrive jamais ? Qui a le droit de relancer un
workflow échoué ? Combien de temps garde-t-on un message non délivré en file ? Les données
transitant par un service externe peuvent-elles y rester ?

Applique la règle habituelle : tranche et explique quand tu peux le faire par le raisonnement ou
la recherche ; pose la question quand c'est un arbitrage qui appartient à Maxime. Une à la fois.

## Étape 4 — Génération des schémas

Écris `Projects/<slug>/Architecture.md` avec les diagrammes en **Mermaid** — c'est la source de
vérité : versionnable, relu automatiquement à chaque session, et directement lisible par l'agent
de codage. Au minimum :

1. **Vue d'ensemble** — modules internes, systèmes externes, et tous les flux entre eux
2. **Un diagramme de séquence par flux critique** — au minimum : le parcours de paiement de bout
   en bout, chaque workflow d'automatisation, et chaque chaîne de notification
3. **Le tableau d'inventaire** de l'étape 1, complet
4. **Les contraintes externes** vérifiées à l'étape 2, rattachées à chaque intégration

Chaque diagramme porte en note les contraintes qui le concernent (fenêtres temporelles, limites
de débit, points de défaillance).

## Étape 5 — Projection sur Miro (optionnelle)

Si le MCP Miro est connecté, génère une projection des schémas sur un board Miro — le MCP
comprend nativement la notation Mermaid, donc c'est une projection directe, pas une réécriture.
C'est là que Maxime regarde, annote et repère qu'un flux est absurde, ce qu'on voit mal dans du
texte.

**Si le MCP Miro n'est pas connecté, saute simplement cette étape** et signale-le à Maxime en une
phrase — sans bloquer, sans insister. Le Mermaid seul est pleinement suffisant pour continuer.

Précise à Maxime que le board est une projection : s'il y déplace ou modifie des choses, ces
changements ne remontent pas automatiquement dans `Architecture.md`, il faut le lui dire.

## Mise à jour des fichiers

`Architecture.md` au fur et à mesure. Toute entité de données révélée par une intégration est
notée dans le fichier pour que `donnees-et-roles` la reprenne. Décisions d'architecture dans
`Decision.md`. Coche l'item 6 de `Progress.md`.

## Sortie

"Architecture posée — [N] éléments communicants, [N] contraintes externes identifiées dont [la
plus structurante]. On passe à la tarification ?" → bascule vers `tarification`.
