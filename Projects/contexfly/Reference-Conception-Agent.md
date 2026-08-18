# Référence de conception — configuration de l'agent, onboarding et inbox

Distillation des quatre produits explorés en conditions réelles les 15-17 août 2026 : **Fiitsa**
(compte connecté), **Wazzap.ai** (onboarding complet), **Zoko** (compte démo), **Ngavix** (compte
connecté). Détail brut et sources dans `_verifications-felix.md`.

Ce fichier n'est pas un benchmark — c'est un **brief de conception** : ce qui marche, ce qui rate,
et ce que ContexFly doit faire. Il alimente **A4** (configuration de l'agent), **B0**
(enregistrement de produit), le domaine **E** (inbox) et le skill `parcours-utilisateur`.

---

## 1. Les trois niveaux de configuration d'agent observés

| | Fiitsa | Wazzap | Ce que ContexFly doit faire |
|---|---|---|---|
| **Forme** | Formulaire | **Conversation** | Conversation |
| **Personnalité** | 4 préréglages | 3 préréglages | Préréglages + **longueur de réponse** |
| **Périmètre** | 5 interrupteurs | tâches déduites des réponses | Interrupteurs **verrouillés** (A12) |
| **Accès aux données** | 6 interrupteurs (stock ❌ par défaut) | — | Stock ✅ **par défaut** + **historique de commandes** |
| **Base de connaissance** | FAQ + scan de site + texte libre | déduite de la conversation | FAQ + texte libre, **alimentée par B0** |
| **Test intégré** | oui — **mais cassé** | non | oui, et il doit marcher |

**Le constat qui compte : aucun des deux ne donne à l'agent l'accès à l'historique de commandes du
client.** Chez Fiitsa, il n'existe même pas de case pour ça. C'est le trou dans lequel ContexFly
s'installe, et c'est ce qui rend possibles la remise de fidélité et le vrai taux d'autonomie.

### Réglages à reprendre tels quels

1. **La longueur de réponse** (Wazzap) — *concises 1-2 phrases / explicatives / formelles /
   naturelles*. Sur WhatsApp, c'est plus déterminant que la « personnalité ». Absent chez Fiitsa.
2. **Le périmètre par interrupteurs** (Fiitsa) — répondre aux FAQ, prendre les commandes,
   transférer à un humain. Lisible pour un commerçant, et compatible avec l'obligation Meta de
   scoper l'agent (A12). **Mais : « prendre des commandes » doit être activé par défaut chez
   ContexFly**, alors que Fiitsa le livre éteint.
3. **L'accès aux données par interrupteurs** (Fiitsa) — la bonne idée, mal réglée. ContexFly doit
   ajouter deux lignes que Fiitsa n'a pas : **historique de commandes** et **statut de livraison**.

### Erreurs à ne pas répéter

- **Stock coupé par défaut** (Fiitsa) → l'agent vend ce qui n'existe plus. Sur ce marché, c'est la
  confiance qui part la première.
- **Un test intégré qui échoue** (Fiitsa : `Failed to send a request to the Edge Function`, deux
  fois, y compris sur un simple « Bonjour ») → si le testeur ne marche pas, le commerçant n'a
  aucun moyen de savoir ce que son agent dira à ses clients. **Le test doit être un chemin
  critique, pas une fonctionnalité annexe.**
- **Un écran sans état vide** (Fiitsa : l'onglet « Mes agents IA » est une page blanche) → sur une
  cible peu technique, l'état vide *est* l'activation.

---

## 2. L'onboarding — ce qui fait entrer un commerçant

### Le squelette à reprendre (Wazzap)

`Profil → Identité → Secteur → Structure → Objectif n°1 → [branchement] → miroir de valeur → configuration conversationnelle`

Quatre principes qui font la différence :

1. **⭐ Le miroir de valeur.** Après les questions, on recalcule les réponses de l'utilisateur et on
   les lui renvoie chiffrées : *« Tu passes 10h par semaine sur ça. Soit 65 jours entiers par
   an. »* Trois compteurs, aucune demande, aucun prix — juste son problème avec ses chiffres, juste
   avant l'engagement. **C'est la meilleure chose vue dans les quatre produits.**
   Version ContexFly : *« Tu réponds à ~N messages par jour. À M minutes chacun, ça fait X heures
   par semaine — et Y conversations qui n'ont jamais eu de réponse. »*
2. **Chaque question justifie sa présence en une ligne** — « ça nous permettra de mieux configurer
   ton assistant », « on adapte les automatisations à ta structure ». C'est ce qui évite l'abandon
   en cours de formulaire.
3. **Le secteur déclaré pilote la configuration initiale** — *« ton assistant sera calé sur ton
   métier dès le départ »*. C'est le point d'entrée de la mémoire de B0.
4. **L'objectif n°1 déclenche un sous-questionnaire dédié.** Un onboarding qui branche paraît
   court tout en collectant beaucoup.

### Le placement du paiement — deux écoles opposées

| | Placement | Effet |
|---|---|---|
| **Wazzap** | paywall en **étape 3 sur 5, avant la connexion WhatsApp** | le commerçant paie avant d'avoir vu la moindre valeur |
| **Fiitsa** | jamais bloquant — on crée un business sans jamais connecter Meta | onboarding rapide, mais une partie de la base n'utilise probablement pas WhatsApp |
| **Zoko** | **compte de démonstration pré-rempli, 7 jours**, avant paiement et avant connexion de numéro | on explore le produit complet avant de s'engager |

**Recommandation : le modèle Zoko.** Le catalogue vide est la mortalité n°1 de ce type de produit ;
un compte de démonstration pré-rempli de conversations et de produits réalistes est une réponse
peu coûteuse, et elle sert aussi de support de démonstration commerciale. → à trancher à
`tarification` et `parcours-utilisateur`.

**Découplage à reprendre de Fiitsa :** ne **pas** bloquer l'inscription sur la connexion Meta. Le
commerçant crée son compte, charge son catalogue, découvre le produit — et connecte son numéro
quand il est prêt. Avec un rappel permanent tant que ce n'est pas fait (Zoko affiche un bandeau
« Connect My number » sur toutes les pages).

---

## 3. L'inbox — le modèle Zoko, à reprendre presque tel quel

**Vues :** `Toutes` / `Non assignées` / `Mes conversations` / `Conversations des autres agents`.
**Filtres :** `Toutes` / `Non lues` / `Sans réponse`.
**En-tête de conversation :** « Assigner à : [agent] ».

**Panneau latéral, onglets Profil / Catalogue :**
- téléphone, **pays et heure locale du client**, e-mail
- **étiquettes** éditables (chez eux : `VIP`, `cart_abandoned`, `SUPPORT`)
- **médias** échangés
- **historique de commandes**, avec bascule « ce client » / « tous les clients »
- **catalogue accessible sans quitter la conversation**

### ⭐ Le détail le plus important de tout ce document

Zoko affiche un badge **`TEMPORARILY ALLOWED`** à côté du numéro du client. C'est l'état de la
**fenêtre de service de 24 h**.

Sans cet indicateur, un vendeur ne comprend jamais pourquoi son message part parfois librement et
parfois pas — et il ne comprend pas non plus pourquoi certains envois coûtent de l'argent.
**ContexFly doit afficher cet état en permanence dans la conversation**, en clair : « tu peux
répondre librement pendant encore 6 h » vs « hors fenêtre — seul un message pré-approuvé peut
partir, et il sera facturé ». → à porter en exigence de conception du domaine E.

### La question ouverte que ça soulève

**Ayweu, le concurrent local qui revendique 3 000+ vendeurs, est une application mobile
uniquement.** Une inbox pensée d'abord pour le bureau est peut-être un contresens sur ce marché.
→ Q6, à trancher au domaine E.

---

## 4. Les automatisations — la leçon la plus exploitable

**Fiitsa a livré un constructeur de règles générique et son onglet « Templates » contient deux
entrées factices** — dont une nommée « Workflow Santé et Business **(copie)** », résidu de
développement — à **0 utilisation**, **0 avis**, et **30 minutes** de mise en place estimée.

Zoko, à l'autre bout, a **deux** systèmes qui coexistent : un constructeur visuel en
glisser-déposer **et** un moteur de règles. C'est un produit qui s'adresse à des marques.

→ **Position confirmée pour ContexFly (Q6bis) : des automatisations pré-écrites, activables en un
clic, avec 2-3 paramètres chacune.** Livrer 5-6 automatisations qui fonctionnent suffit à dépasser
tout le module d'automatisation du leader local. Le constructeur générique est `Could`, jamais
`Must` — et si un jour il arrive, il arrive **après** la bibliothèque, jamais à sa place.

---

## 5. Les cinq fonctionnalités qui manquaient à mon inventaire

Toutes issues de l'observation, toutes à effort faible :

| # | Fonctionnalité | Source | Effort |
|---|---|---|---|
| 1 | **Horaires d'ouverture + message d'absence** | Zoko | S |
| 2 | **Réponses rapides** pour l'opérateur humain | Zoko | S |
| 3 | **Analytique par agent** (temps de réponse, taux de résolution) — la brique qui rend le **taux d'autonomie** mesurable | Zoko (BETA) | M |
| 4 | **Indicateur de fenêtre de service 24 h** dans la conversation | Zoko | S |
| 5 | **Compte de démonstration pré-rempli** | Zoko | M |

L'analytique (n°3) n'est pas cosmétique : sans elle, l'objectif n°1 de `Idee.md` — la part de
commandes payées obtenues sans intervention humaine — reste déclaratif.

---

## 6. Ce que l'exploration a appris sur le discours

- **« 0 % de marge sur tes messages » est déjà pris** — Genuka WA l'affiche mot pour mot. À
  reformuler ou abandonner (Q28).
- **« Le panier » n'est pas un argument** — l'app WhatsApp Business le donne gratuitement.
- **« Une boutique à 10 000 FCFA » n'est pas un argument** — Ngavix la vend déjà, avec catalogue,
  commandes, codes promo et notifications WhatsApp.
- **Ce qui reste : la conversation.** L'agent qui répond, qualifie, construit le panier et encaisse
  *dans le fil*, à un prix de commerçant. C'est la seule revendication que le benchmark ne
  contredit pas.
- **Un argument nouveau et vérifiable : la conformité Meta 2026.** Les chatbots IA généralistes
  sont interdits sur la plateforme depuis janvier 2026 ; les agents scopés à un processus métier
  sont explicitement autorisés. ContexFly est du bon côté par construction — et « Leslie, ta
  patronne IA accessible depuis ton WhatsApp personnel » de Fiitsa ressemble beaucoup à ce qui est
  désormais interdit.
