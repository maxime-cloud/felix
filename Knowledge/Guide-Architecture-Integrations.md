# Guide Architecture & Intégrations — Méthodologie

Utilisé par les skills `modularisation` et `architecture-integrations`. Ces deux étapes se
suivent immédiatement et forment un ensemble : la modularisation pose les composants,
l'architecture pose les câbles.

## Pourquoi la modularisation précède l'architecture

Un schéma d'architecture a besoin de nœuds internes. Sans modules, l'application est une seule
boîte opaque qui parle à des systèmes externes — le diagramme perd l'essentiel de sa valeur, et
on ne voit pas les échanges internes qui sont souvent la source des vrais problèmes de
conception. On ne dessine pas les câbles avant d'avoir posé les composants.

## Ce qu'est un module, et ce qu'il n'est pas

Un module est une **frontière métier** : un ensemble de fonctionnalités qui manipulent les mêmes
concepts, servent le même objectif utilisateur, et évolueraient ensemble.

Un module n'est **pas** une structure de dossiers, un découpage de fichiers, ni un choix
d'organisation du code. Cette frontière est stricte : descendre au niveau de l'implémentation
contraindrait l'agent de codage sans bénéfice, et sortirait du rôle de Felix.

**Isolé** : aucune dépendance directe vers un autre module ; communication par contrat ou
événement ; retirable ou remplaçable sans casser le reste.
**Semi-isolé** : partage des entités ou lit directement dans un autre module ; dépendance assumée
et orientée (A dépend de B, jamais l'inverse).

Les dépendances circulaires sont un **défaut de découpage**, pas une réalité à documenter. Face à
un cycle, deux corrections possibles : fusionner les deux modules, ou extraire ce qu'ils
partagent dans un troisième module dont les deux dépendent.

## Le niveau de détail de l'inventaire d'architecture

La règle : **une unité fonctionnelle distincte = un élément**, jamais « un système = un élément ».

« L'application communique avec n8n » est une information vide. Ce qui est utile :

> *Workflow « relance paiement échoué » — déclenché par le webhook `payment.failed`, lit
> l'abonnement et le contact facturé, envoie un message WhatsApp (template pré-approuvé si
> hors fenêtre 24h), réécrit le statut de relance ; en cas d'échec d'envoi, réessaie à J+1 puis
> bascule sur SMS.*

Ce niveau révèle les entités de données manquantes (un statut de relance, un historique de
tentatives) et les contraintes réelles — c'est précisément à quoi sert cette étape.

Éléments à recenser individuellement : modules internes et leurs échanges, chaque workflow
d'automatisation, chaque webhook entrant, chaque usage distinct d'une API externe (une même API
qui sert à deux choses compte pour deux), chaque tâche planifiée, et les acteurs humains quand
ils font partie du flux.

## Les contraintes externes se vérifient, ne se supposent jamais

Chaque interaction avec un service externe passe par le sous-agent
`verificateur-contraintes-externes` **avant** d'être dessinée. La catégorie la plus souvent
ratée est celle des **fenêtres temporelles** : elles sont rarement mises en avant dans une
documentation, et ce sont elles qui invalident silencieusement un flux entier.

Les contraintes trouvées sont portées **en notes sur les diagrammes eux-mêmes**. Un document
annexe de contraintes ne sera pas lu par l'agent de codage au moment où il en a besoin.

Quand une contrainte révèle une fonctionnalité manquante, retour à `fonctionnalites` pour
l'ajouter avec son analyse complète, puis retour ici. C'est un aller-retour normal, pas un échec
de planification.

## Mermaid fait autorité, Miro est une projection

`Architecture.md` en Mermaid est la source de vérité : versionnable, diffable, relu
automatiquement à chaque reprise de session, et directement lisible par l'agent de codage. Un
board Miro demande une extraction supplémentaire et dépend d'une connexion qui peut échouer.

Miro garde un vrai rôle : c'est le support où Maxime regarde, annote, et repère qu'un flux est
absurde — ce qui se voit mal dans du texte. Le MCP Miro comprend nativement Mermaid, donc la
projection est directe.

Si le MCP Miro n'est pas connecté, l'étape est simplement sautée avec une phrase de signalement.
Le Mermaid seul suffit pour continuer — ne jamais bloquer le parcours là-dessus.

Les modifications faites à la main sur le board ne remontent pas automatiquement dans le `.md` :
le préciser à Maxime au moment de la génération.


---

## Les diagrammes de synthèse (ajout août 2026)

Un dossier d'architecture qui ne contient que des flux est incomplet. Trois familles sont
nécessaires, et elles répondent à trois questions différentes :

| Famille | Question à laquelle elle répond |
|---|---|
| **Flux** — vue d'ensemble, diagrammes de séquence | *Comment ça circule ?* |
| **Cas d'utilisation** | *Qui peut faire quoi ?* |
| **États** — un par entité à cycle de vie | *Quels états existent, et quelles transitions sont permises ?* |
| **Dépendances entre modules** | *Par quoi commencer, et y a-t-il un cycle ?* |

**Le critère qui distingue un diagramme utile d'un diagramme décoratif : qu'est-ce qu'il empêche ?**
S'il n'empêche rien — ni une invention, ni une transition illégale, ni un mauvais ordre de
construction — il ne sert qu'à remplir le dossier, et il sera ignoré par l'agent de codage comme
par le lecteur humain.

**Le diagramme de cas d'utilisation est celui qu'on oublie le plus souvent, et c'est dommage :**
c'est le seul qui rende visible d'un coup d'œil l'asymétrie entre les rôles. Voir qu'un acteur n'a
que quatre capacités quand un autre en a vingt-deux en dit plus long sur le produit qu'une liste de
soixante-dix fonctionnalités.

**Les diagrammes d'états portent les contraintes externes mieux que tout autre support.** Un état
comme « retenu par le fournisseur » ou « en attente de confirmation du client sur son téléphone »
n'existe que parce qu'un service tiers l'impose — et c'est exactement le genre d'état qu'un
développeur n'invente jamais spontanément, mais qu'il doit gérer.

**Frontières à respecter :** le modèle entité-relation appartient à `donnees-et-roles`, les
parcours d'écrans à `parcours-utilisateur`, et tout ce qui touche aux composants, au déploiement ou
à l'infrastructure est de l'implémentation — hors périmètre de Felix.
