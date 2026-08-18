# Guide de Validation des Fonctionnalités — Méthodologie

Utilisé par le skill `fonctionnalites`. C'est, de l'aveu de Maxime, **la partie la plus
importante de tout le processus** — plus de détail et de rigueur ici vaut plus que de la vitesse.

## Le triptyque d'analyse — calibré selon la priorité

Le triptyque complet est obligatoire pour les fonctionnalités **Must et Should**. Les **Could**
reçoivent une seule ligne de justification, et les fonctionnalités **évidentes** (CRUD standard
sans enjeu de décision) sont groupées sous une analyse commune.

Cette calibration n'est pas un relâchement : produire quarante analyses commerciales sincères est
impossible, et au-delà d'un certain volume elles se ressemblent toutes et deviennent du
remplissage — exactement ce que ce guide interdit. Mieux vaut dix analyses qui éclairent
réellement une décision que quarante qui cochent une case.

Pour les Must et Should, ces trois éléments s'ajoutent à la description/rôle/priorité/effort :

1. **Analyse commerciale** — en quoi cette fonctionnalité sert le business : différenciation vs
   les concurrents du benchmark, levier d'acquisition, levier de rétention, ou levier de
   monétisation (justifie un palier payant plus élevé). Une fonctionnalité sans aucun de ces
   quatre angles est suspecte — le dire à Maxime plutôt que de l'inventer.
2. **Utilité** — quel problème concret ça résout, pour qui, à quelle fréquence d'usage estimée
   (quotidien, hebdomadaire, occasionnel). Si l'utilité est faible ou hypothétique, le signaler
   clairement plutôt que de gonfler artificiellement l'argumentaire.
3. **Piste d'approfondissement** — est-ce qu'on peut aller plus loin avec cette fonctionnalité
   (une variante plus poussée, une automatisation, une intégration) qui la rendrait plus forte —
   sans la complexifier inutilement pour un MVP. Si non, le dire simplement.

**Effort (S/M/L)** : estimation du coût de développement pour un développeur solo déléguant à un
agent IA sur la base `ai-builder-saas`. S = quelques heures à un jour ; M = plusieurs jours ;
L = une semaine ou plus, ou risque technique réel. L'effort corrige la priorité : une
fonctionnalité à impact moyen et effort S passe souvent avant une à impact élevé et effort L dans
un MVP — signaler explicitement ces croisements à Maxime.

**Source** : si la fonctionnalité s'inspire de ce qui a été vu dans `Benchmark-Concurrents.md`,
cite quel(s) produit(s) la propose(nt). Si c'est une idée originale de Maxime ou de Felix sans
équivalent identifié dans le benchmark, le dire aussi — ça fait partie de l'honnêteté sur
l'origine de l'information.

## Ne jamais halluciner

Si l'analyse commerciale ou l'utilité d'une fonctionnalité repose sur une affirmation factuelle
(ex: "70% des salons utilisent déjà ce type d'outil") que tu n'as pas vérifiée par une vraie
recherche, ne l'écris pas. Dis "je pense que..." avec ton raisonnement, ou fais la recherche, ou
demande à Maxime — jamais une statistique ou un fait inventé pour rendre l'argumentaire plus
convaincant.

## Le déroulé en boucle

1. **Génération de la liste initiale** — à partir de la vision (`Idee.md`) et du benchmark
   (`Benchmark-Concurrents.md`), génère le plus de fonctionnalités candidates possible, organisées
   par domaine.
2. **Validation une par une** — présente chaque fonctionnalité avec son triptyque complet, dans
   un ordre logique par domaine (voir skill `fonctionnalites` pour les domaines typiques ; pas
   nécessairement une par message si plusieurs sont très liées, mais jamais une liste plate de 20
   fonctionnalités sans détail d'un coup). Attends la réaction
   de Maxime (validée / rejetée / à ajuster) avant de la marquer comme telle dans le fichier.
3. **Question de relance** — une fois toutes les fonctionnalités candidates traitées, demande
   explicitement : *"Est-ce qu'il y a des fonctionnalités que tu voudrais ajouter ?"*
4. **Si oui** — Maxime donne une liste. Chaque fonctionnalité de cette liste reçoit le même
   triptyque d'analyse complet (recherche si besoin pour l'analyse commerciale/utilité) avant
   d'être présentée à validation.
5. **Boucle** — retour à l'étape 3 après chaque lot ajouté, jusqu'à ce que Maxime dise
   explicitement qu'il n'a plus rien à soumettre.
6. **Sortie** — une fois la boucle fermée, passe au skill `tarification` pour structurer les
   offres à partir des fonctionnalités maintenant validées.

## Stockage

Chaque fonctionnalité dans `Fonctionnalites.md` porte un statut explicite : `proposée` /
`validée` / `rejetée` / `à ajuster`. Ne supprime jamais une fonctionnalité rejetée du fichier —
garde-la avec son statut et la raison du rejet, ça évite de la re-proposer plus tard par erreur.
