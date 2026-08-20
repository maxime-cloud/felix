# Avancement — ContexFly

Checklist de complétude (voir CLAUDE.md pour la définition complète de chaque point) :

1. [x] **Vision & problème validés** — 2026-08-15. Dispersion vérifiée et recadrée (volet sortant
   redéfini en fidélisation opt-in). `Idee.md` complet.
2. [x] **Benchmark concurrentiel** — 2026-08-15. Trois volets consolidés dans
   `Benchmark-Concurrents.md`, plus l'exploration réelle de 4 produits (`_verifications-felix.md`).
3. [x] **Positionnement marketing** — 2026-08-15, `Positionnement.md`. Premier passage, à reprendre
   par `analyse-approfondie`.
4. [x] **Fonctionnalités validées** — 2026-08-17, complété le 2026-08-19. Boucle Maxime fermée,
   passe proactive de Felix (P1-P4) traitée. Domaines A à N — le domaine N (13 fonctionnalités
   imposées par les contraintes externes Meta / Notch Pay) validé en bloc par Maxime le 19/08.
5. [x] **Découpage en modules** — 2026-08-19. 13 modules, dépendances sans cycle, ordre de
   construction dans `Modules.md`.
6. [x] **Architecture & intégrations** — 2026-08-19. 31 éléments communicants inventoriés,
   contraintes Meta et Notch Pay vérifiées et portées en note, 5 diagrammes Mermaid dans
   `Architecture.md`, projetés sur un board Miro.
7. [ ] Modèle de tarification défini, cohérent avec les fonctionnalités validées
8. [x] **Modèle de données & rôles** — 2026-08-19, `Modele-Donnees.md`. Option A (activité = organisation), 3 rôles, entités par domaine. Couvre le MVP — y compris les entités révélées par les intégrations —
   rôles & permissions définis
9. [x] **Parcours utilisateurs** — 2026-08-19, `Parcours.md`. 6 parcours avec états
10. [x] **Checklist SaaS-Essentiels** — 2026-08-19. Les 17 catégories déroulées dans
    `Exigences-Non-Fonctionnelles.md`, chacune avec son issue. A révélé 2 fonctionnalités
    manquantes (I4, H7) et 4 questions ouvertes (Q37-Q40).
11. [x] **Cohérence croisée** — 2026-08-19. 2 blocantes et 13 incohérences relevées par le
    sous-agent `verificateur-coherence`, **toutes corrigées**.
12. [ ] Analyse approfondie complète (comparaison finale, `La-Verite-Difficile.md`, questions dures,
    `MVP.md`) et direction validée par Maxime pour passer à la PRD
13. [ ] PRD rédigée et confirmée conforme au produit voulu par Maxime
14. [ ] Intégration base faite (`Tools.md`, `Fichiers-Pour-Agent.md`) et les quatre documents de
    handoff technique consolidés dans `Output/`
15. [ ] `Questions-Ouvertes.md` vide ou tout résolu

**Statut global : 9/15.**

Étape suivante : `tarification` — **désormais débloquée**. Ses deux prérequis sont levés : le
**coût d'inférence par conversation** est modélisé (Q13, `Contraintes-Techniques.md` §5) et les
**frais Notch Pay** sont tranchés (Q35 : 2 % à l'encaissement + 1 % au reversement).

---

## 🔴 Hors périmètre Felix, mais bloquant pour le lancement

À engager **maintenant**, en parallèle du développement — ce sont les deux vraies contraintes de
calendrier, et aucune ne dépend du code :

1. **Meta — statut Tech Provider** (Q22). App Meta, vérification d'entreprise, App Review avec
   vidéos, advanced access. Délai non documenté, rejet possible. **Et l'onboarding est plafonné à
   10 nouveaux commerçants par 7 jours glissants avant approbation — 0 avant.**
2. **Notch Pay — contrat Sync** (Q30). Non self-serve : « contact our sales team » + vérifications
   de conformité. **Aucun code d'encaissement n'est testable avant accord signé.**
   Email rédigé et prêt dans `_email-notchpay.md`.

## ⚠️ Hypothèse de travail assumée

L'analyse se poursuit en considérant que Meta et Notch Pay couvrent le besoin (décision Maxime,
2026-08-19). Côté Meta, tout est vérifié. **Côté Notch Pay, la garde des fonds reste non
documentée** — vérifiée trois fois, jamais trouvée. Elle est **supposée favorable, pas établie**
(Q29). À confirmer par écrit avant mise en production.
