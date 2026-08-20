# Exigences non-fonctionnelles — ContexFly

Revue des **17 catégories** de `Knowledge/Checklist-SaaS-Essentiels.md`, déroulée le
**2026-08-19**. Chaque item a l'une de trois issues : **applicable et détaillé**, **écarté et
justifié**, ou **à trancher** (parti en question ouverte). Aucun item laissé sans issue.

🎁 = déjà couvert par `ai-builder-saas`.

---

## 1. Identité, comptes et rôles — ✅ applicable

- **Création de compte** : auto-inscription libre. **Ne jamais bloquer l'inscription sur la
  connexion Meta** — c'est le trou observé chez Fiitsa qu'on ne reproduit pas.
- **Rôles** : `owner` (🔴 exactement 1 par activité) · `manager` · `member`. 🎁
- **Multi-appartenance** : oui, un utilisateur est membre de plusieurs activités (option A). 🎁
- **Mot de passe, e-mail, 2FA** : 🎁 Better Auth. 2FA optionnel côté locataire, **obligatoire pour
  l'administrateur plateforme** — décision déjà prise dans le socle, et cohérente : cette console
  lit les données de tous les commerçants.
- **Le client final n'a aucun compte.** Son identification est son numéro WhatsApp.

## 2. Multi-tenant — ✅ applicable, et c'est la règle la plus critique

- **Cloisonnement** : `organizationId` sur chaque ligne métier. 🎁
- 🔴 **R8 est le point le plus sensible du produit** : l'agent IA parle à un **inconnu**. L'identifiant
  d'activité vient du contexte, **jamais des arguments d'un outil** — sinon une injection de prompt
  franchit la frontière entre commerçants.
- **Limites par plan** : 🎁 mécanisme d'entitlements. Valeurs à fixer à `tarification`.

## 3. Facturation et revenus — ✅ applicable

- **SaaS payant**, abonnement en **Mobile Money**. 🎁 `plans`, `planPrices`, `subscriptions`.
- 🔴 **ContexFly manipule l'argent de ses utilisateurs** — la checklist le classe Must : traçabilité
  et sécurité renforcées. D'où le **registre d'écritures append-only** (`merchantLedger`), la
  **réconciliation active** (P5w) et le **back-office de supervision** (J2).
- **Frais visibles** : les 3 % Notch Pay sont affichés au commerçant, jamais absorbés (R7bis).

## 4. Notifications — ✅ applicable

| Événement | Canal |
|---|---|
| Nouvelle commande, paiement reçu | WhatsApp + in-app |
| Reversement exécuté / revenu en arrière | in-app + e-mail |
| KYC rejeté, template rejeté, note de qualité dégradée | in-app + e-mail |
| **Connexion WhatsApp rompue** (changement de téléphone, N10) | in-app + e-mail — **urgent** |
| Perte d'accès subie (R31) | in-app **et** e-mail |
| Commande expédiée depuis trop longtemps sans « livrée » | in-app |

🎁 domaine `notifications`, avec préférences par membre.
**Le commerçant configure ce qu'il reçoit**, sauf les alertes de rupture de service.

## 5. Onboarding — ✅ applicable

- Détaillé dans `Parcours.md` §1 : miroir de valeur, liste d'avancement permanente, découplage de
  la connexion Meta.
- **Import de données existantes** : ✅ **retenu → B5** *(mis à jour le 19/08)*. Barrière d'opt-in :
  un contact importé ne reçoit aucune campagne tant qu'il n'a pas écrit lui-même.

## 6. 🔴 Recherche, filtres et volumétrie — ⚠️ **ANGLE MORT COMPLET**

**Aucune des ~90 fonctionnalités validées ne traite ce sujet.** Or dès le troisième mois d'un
commerçant actif : 200 produits, 500 clients, 1 500 commandes, des milliers de messages.

À prévoir, et ce n'est pas optionnel :
- **Recherche et filtres** sur produits (catégorie, stock, point de vente), commandes (statut,
  période, client, zone), clients (segment, dernière commande), conversations (déjà partiellement
  couvert par E1).
- **Pagination partout.** Une liste non paginée casse d'abord sur mobile, en connexion lente.
- **Export CSV** des commandes et des clients — 🔴 **et c'est aussi la réponse à la catégorie 17**
  (fin d'abonnement).
→ **Nouvelle fonctionnalité I4**, priorité **Must**, effort **M**.

## 7. Historique et audit — ✅ applicable

- 🎁 domaine `audit`. À y verser : changement de prix, remise accordée par l'agent, changement de
  statut de commande, encaissement en espèces, transfert de propriété, archivage.
- **Annulation d'une suppression** : ✅ garantie par construction — **R29, aucune suppression
  réelle**. L'administrateur ContexFly réactive.
- ⭐ **`agentToolCalls` est la piste d'audit du produit** : chaque appel d'outil de l'agent est
  journalisé. C'est ce qui permet de répondre à un litige *« l'IA m'a promis -30 % »*.

## 8. Sécurité et confidentialité — ✅ applicable, détaillé

- **Coffre de secrets par activité** (N8) : PIN 2FA Meta, `verifyToken`, business token. Chiffrés.
- **Vérification de signature** : Meta (`X-Hub-Signature-256`) et Notch Pay (`x-notch-signature`),
  **sur le corps brut**, en comparaison à temps constant.
- 🔴 **Notch Pay ne fournit aucune protection anti-rejeu** → déduplication persistante obligatoire.
- **Vérification du numéro du gérant** avant de lui accorder le registre « propriétaire » sur
  WhatsApp (R11) — sinon une usurpation de numéro ferme la boutique.
- **Cloisonnement par rôle** : un `member` ne voit ni les revenus, ni la configuration de l'agent,
  ni les paramètres d'encaissement.
- **Loi camerounaise n°2024/017**, extraterritoriale, **déjà en vigueur**.

## 9. Disponibilité, performance, connectivité — ⚠️ partiellement à trancher

- **Page panier tolérante à la coupure** : ✅ spécifié (`Parcours.md` §2).
- **Saisie B0 non perdue hors ligne** : ✅ spécifié.
- ✅ **Mode dégradé : retenu → K1** *(mis à jour le 19/08)*. PWA installable, consultation hors
  ligne, saisies simples mises en file. **Pas de conversation hors ligne.** Effort L.
- **Volumétrie MVP** : quelques dizaines de commerçants, quelques centaines de conversations/jour.
  **Ne pas sur-architecturer.** Les vrais plafonds sont ceux de Meta, pas ceux de l'infrastructure.

## 10. Back-office ContexFly — ✅ applicable

🎁 domaine `admin` + `requirePlatformAdmin`. Contenu : instruction du KYC, supervision des
paiements et litiges, relance d'un processus échoué, **réactivation d'une activité archivée**
(R29), **compteur glissant d'onboarding Meta sur 7 jours** (N3).

## 11. Intégrations externes — ✅ applicable

**Must** : Meta WhatsApp Cloud API · Notch Pay Sync · Gemini · transcription vocale (X13).
**Could** : catalogue WhatsApp natif (B3).
**Écarté** : n8n (abandonné, raison consignée) · comptabilité · ERP.
**API publique ContexFly** : ⚠️ **écartée du MVP**, justifié — aucun client ne l'a demandée, et
elle figerait des contrats internes encore mouvants.

## 12. Internationalisation — ✅ applicable

🎁 `localizedTextValidator` + Paraglide JS. **Français d'abord, anglais prévu.**
**Devise XAF en entiers** — pas de subdivision. Fuseau Afrique/Douala. Format de date local.
⭐ Le **pidgin** est traité côté agent (A11), pas comme une locale d'interface.

## 13. États d'interface — ✅ applicable

Détaillé par écran dans `Parcours.md`. Trois règles absolues, toutes tirées de défauts **observés**
chez les concurrents :
- **Aucun écran sans état vide.** Sur cette cible, l'état vide *est* l'activation.
- **Aucune erreur technique brute affichée.**
- **Confirmation avant toute écriture issue d'une saisie conversationnelle** (R15).

## 14. Support et aide — ⚠️ **angle mort**

Rien n'était prévu. Décision : **F7 (pédagogie des règles WhatsApp) couvre l'essentiel du support
prévisible** — c'est là que les questions se concentreront. S'y ajoute un **contact direct par
WhatsApp**, cohérent avec le produit et avec la cible. **Pas de FAQ ni de chat au MVP.**
→ **Nouvelle fonctionnalité H7**, priorité **Should**, effort **S**.

## 15. Légal et conformité — ⚠️ à produire

- **CGU/CGV et politique de confidentialité** : obligatoires — ContexFly traite les données de
  **clients de ses clients**. Module **déclinable par pays**, faute de cadre africain unifié.
- **Mentions du rôle d'intermédiaire de paiement** dans les CGU.
- → **Q39** : rédaction à prévoir, hors périmètre de Felix.

## 16. Sauvegarde et continuité — ⚠️ à trancher

- Convex assure la durabilité et les sauvegardes de la plateforme. **Mais la question réelle est
  autre : qui peut restaurer, et à quelle granularité ?**
- 🔴 **R29 traite déjà 90 % du besoin** : rien n'est jamais supprimé, donc rien à restaurer dans le
  cas courant. Reste le cas de la corruption de données ou de l'erreur de masse. → **Q40**.

## 17. Cycle de vie et fin d'abonnement — ✅ applicable

- **Abonnement expiré** : l'activité passe en lecture seule — **l'agent cesse de répondre**, mais
  les données restent. Jamais de suppression (R29).
- **Export des données** : couvert par **I4** (§6). C'est ce qui rend un départ propre possible.
- **Rétention** : R32 — conversations 24 mois, médias 6 mois, commandes et registre sans limite,
  clients anonymisés après 24 mois sans activité.
- ⚠️ **Le commerçant garde son numéro WhatsApp et son WABA** — ils lui appartiennent (Embedded
  Signup). Le départ ne le prive pas de son fonds de commerce. **C'est un argument commercial**,
  à dire explicitement.

---

## Ce que cette revue a fait apparaître

| # | Manque | Traitement |
|---|---|---|
| **I4** | **Recherche, filtres, pagination, export** — angle mort complet | Nouvelle fonctionnalité, **Must**, M |
| **H7** | **Support** — rien n'était prévu | Nouvelle fonctionnalité, **Should**, S |
| **Q37** | Import d'une base clients existante | ✅ Retenu → **B5** |
| **Q38** | Mode dégradé | ✅ Retenu → **K1**, effort L |
| **Q39** | CGU, CGV, politique de confidentialité | ✅ Brouillons rédigés → `_documents-juridiques.md` |
| **Q40** | Restauration : qui, et à quelle granularité | Question ouverte |
