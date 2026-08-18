# Felix

**Transforme Claude Code en Felix, ton Analyste Produit senior spécialisé SaaS.**

Felix t'accompagne sur la partie que tu voulais fiabiliser : le passage d'une idée de SaaS
(étude de marché déjà faite) à une PRD complète et honnête — positionnement, benchmark
concurrentiel, fonctionnalités validées une par une, tarification, modèle de données, parcours,
exigences, analyse de viabilité — jusqu'aux documents prêts à donner à ton agent de codage sur
**ai-builder-saas**. Un seul outil, réutilisable pour tous tes projets.

## Installation

```bash
# 1. Place ce dossier où tu veux sur ta machine
mv Felix ~/Felix
cd ~/Felix

# 2. (optionnel mais recommandé) initialise un dépôt git pour garder l'historique
git init && git add -A && git commit -m "Init Felix"

# 3. Ouvre avec Claude Code
claude
```

Claude Code charge automatiquement `CLAUDE.md` à l'ouverture. Les 13 skills dans
`.claude/skills/` sont détectés automatiquement et s'activent selon ce dont parle la
conversation, tu n'as jamais besoin de les invoquer par leur nom.

**Important — navigation** :
- Recherche web générale : plusieurs skills s'appuient dessus.
- **Benchmark concurrentiel** (`benchmark-concurrents`) : exige une **navigation réelle** sur les
  sites concurrents (les grilles tarifaires sont souvent en JavaScript ou derrière un clic). Deux
  options, par ordre de préférence : **l'extension Chrome de Claude**, ou le **MCP Playwright**
  (`claude mcp add playwright npx @playwright/mcp@latest`). Si aucun n'est disponible, Felix te le
  dira avec la commande à lancer plutôt que de compenser silencieusement.
- **MCP Miro** (*optionnel*) : utilisé uniquement par `architecture-integrations` pour projeter
  les schémas d'architecture sur un board (`/plugin marketplace add miroapp/miro-ai` puis
  `/plugin install miro@miro-ai`). S'il n'est pas connecté, Felix te le signale en une phrase et
  continue avec le Mermaid seul — rien n'est bloqué.

## Sous-agents

Felix délègue à six sous-agents spécialisés (`.claude/agents/`), chacun avec son propre contexte :

| Sous-agent | Rôle |
|---|---|
| `chercheur-mondial` | Recherche concurrentielle mondiale, navigation réelle |
| `chercheur-local` | Recherche sur ton périmètre (pays/région), y compris concurrents non-numériques |
| `arbitre-pertinence` | Tranche si les acteurs mondiaux comptent pour ton projet, et extrait ce qu'il faut en garder même s'ils ne comptent pas |
| `verificateur-contraintes-externes` | Vérifie dans la doc officielle les contraintes réelles d'un service externe (limites de débit, fenêtres temporelles, coûts) avant de dessiner une interaction avec lui |
| `verificateur-coherence` | Vérification mécanique de cohérence entre documents |
| `critique-produit` | Regard adverse indépendant — attaque la différenciation et la valeur |

`critique-produit` existe parce que Felix propose lui-même une partie des fonctionnalités : il ne
peut pas juger sa propre production sans complaisance. Ce sous-agent n'a pas participé à la
conception, c'est toute sa valeur.

## Utilisation

Ouvre simplement une conversation et parle — comme avec un consultant. Tes descriptions de
départ peuvent être aussi détaillées que tu veux : Felix extrait ce que tu as déjà donné avant
de poser des questions. Il ne valide jamais par défaut — s'il pense que ton idée est dispersée,
qu'une fonctionnalité est faible, ou que le produit manque de valeur réelle, il te le dit,
quitte à te contredire.

## Le déroulé complet

`cadrage` (extraction + dispersion + socle vision) → `benchmark-concurrents` (3 volets :
mondial, local, arbitrage) → retour à `cadrage` (approfondissement informé) → `positionnement-marketing`
(différenciation, "pourquoi") → `fonctionnalites` (génération + boucle de validation + passe
proactive de Felix) → `modularisation` (découpage en modules isolés/semi-isolés, dépendances,
ordre de construction) → `architecture-integrations` (inventaire détaillé de tout ce qui
communique, contraintes externes vérifiées, schémas Mermaid + Miro optionnel) → `tarification` →
`donnees-et-roles` → `parcours-utilisateur` →
`saas-essentiels` (en continu) → `analyse-approfondie` (cohérence croisée, comparaison finale,
"La vérité difficile", questions dures, MVP à vraie valeur, boucle de décision) → `redaction-prd`
(PRD + marketing final) → `integration-base` (préparation du handoff vers ai-builder-saas).

La boucle de `analyse-approfondie` peut te renvoyer vers `fonctionnalites` ou `cadrage` autant de
fois que nécessaire — Felix compare à chaque passage ce qui a changé plutôt que de tout
recommencer. Elle offre aussi une quatrième issue : **arrêter le projet**, que Felix te proposera
explicitement si l'analyse ne montre pas de valeur distinctive suffisante.

## Ce que tu obtiens à la fin (`Output/<slug>/`)

| Document | À quoi il sert |
|---|---|
| `PRD.md` | Le document de référence complet : objectifs, positionnement, MVP, fonctionnalités, tarification, données, parcours, exigences, métriques, critères d'acceptation |
| `Marketing.md` | Positionnement et différenciation finalisés, honnêtes |
| `User-Stories.md` | Les fonctionnalités en user stories avec critères d'acceptation |
| `Modele-Donnees-Technique.md` | Les entités/champs/relations, prêtes pour Convex/Prisma |
| `Brief-Agent-Codeur.md` | Le prompt de démarrage condensé à coller à ton agent de codage |
| `Tools.md` | Outils recommandés pour ce SaaS précis, en plus de ce qu'ai-builder-saas fournit déjà |
| `Fichiers-Pour-Agent.md` | Quels fichiers donner à l'agent, l'extrait pour le `CLAUDE.md` d'ai-builder-saas, et ce qu'il ne faut PAS lui confier |

Ces documents ne sont générés que lorsque les jalons requis sont cochés dans `Progress.md` —
l'outil refuse volontairement de livrer un dossier troué, incohérent, ou pas encore validé par
toi.

## Structure

```
Felix/
├── CLAUDE.md                ← le cerveau : principes, routing, checklist (15 pts)
├── Knowledge/                 ← méthodologie et référentiels : checklist SaaS-Essentiels,
│                                 guides de benchmark/validation/architecture & intégrations/
│                                 analyse approfondie/livrables, référence d'ai-builder-saas
├── .claude/skills/            ← les 13 spécialités
├── .claude/agents/            ← les 6 sous-agents spécialisés
├── Projects/<slug>/           ← l'état vivant de chaque idée (dont Changelog.md et Decision.md)
└── Output/<slug>/             ← les 7 documents finaux, une fois l'analyse validée
```

## Personnaliser

- `Knowledge/Checklist-SaaS-Essentiels.md` — angles morts classiques, à enrichir avec le temps.
- `Knowledge/Reference-Base-SaaS.md` — résumé d'ai-builder-saas ; **mets-le à jour toi-même si tu
  fais évoluer ton projet de base**, sinon `integration-base` travaillera sur une image obsolète.
- `CLAUDE.md` contient les hypothèses de contexte (marché camerounais) — ajuste si besoin.
