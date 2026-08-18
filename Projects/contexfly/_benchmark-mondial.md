# Benchmark mondial — ContexFly (commerce conversationnel / agents IA de vente sur WhatsApp)

> Volet **mondial** du benchmark. Aucune restriction géographique.
> Date de collecte : 15 août 2026.

---

## Avertissement méthodologique — À LIRE AVANT D'EXPLOITER CE RAPPORT

**Aucun outil de navigation avec exécution JavaScript n'était disponible** dans cette session :
ni MCP Playwright, ni extension Chrome de Claude, ni computer-use chargé. Je n'ai eu que
`WebFetch` (récupération HTML + conversion markdown, **sans JS, sans clic, sans sélecteur de
plan**).

Conséquences concrètes :

- Les grilles tarifaires rendues côté client (Manychat, Whautomate, Bik, Chatarmin partiellement)
  n'ont **pas pu être lues**. Marqué explicitement à chaque fois.
- Les prix affichés derrière un toggle mensuel/annuel ou un sélecteur de devise ont pu être
  captés partiellement (une seule variante visible dans le HTML).
- Certaines pages ont renvoyé 404 alors que la page existe probablement sous une autre URL
  (Wati Astra, Zoko AI agents, Yalo about, charles pricing). Noté à chaque fois.
- Quand j'ai dû utiliser une source secondaire (blog tiers, presse, agrégateur), **c'est signalé
  en toutes lettres** et le fait est marqué comme non vérifié à la source.

Pour un benchmark tarifaire fiable, il faudra relancer ce volet avec :
`claude mcp add playwright npx @playwright/mcp@latest`

**Contexte réglementaire vérifié à la source** (utile pour tout le rapport) : Meta facture le
WhatsApp Business Platform **au message délivré depuis le 1er juillet 2025** (et non plus à la
conversation de 24 h). Les messages non-template envoyés dans une fenêtre de service ouverte sont
**gratuits**, les templates *utility* délivrés dans une fenêtre de service ouverte sont gratuits,
et une entrée via pub Click-to-WhatsApp ouvre une fenêtre de **72 h entièrement gratuite**.
Source : https://developers.facebook.com/docs/whatsapp/pricing

---

# PARTIE 1 — 5 PRODUITS ÉTABLIS

---

## 1. Wati

**URL** : https://www.wati.io — tarifs : https://www.wati.io/pricing/
**Année de lancement** : 2019 (Hong Kong). *Source secondaire (Crunchbase via recherche), non
confirmée sur wati.io.*

### Fonctionnalités clés réelles
Vu sur https://www.wati.io/pricing/ :
- Accès API officielle WhatsApp Business, « zero-fee WhatsApp setup »
- **Boîte de réception partagée omnicanale** (WhatsApp, Facebook, Instagram, QR code), avec
  attribution aux agents
- Diffusions/campagnes (15 k/mois sur Growth, illimitées sur Pro/Business)
- Intégration pubs **Click-to-WhatsApp (CTWA)**
- **Catalogue WhatsApp** pour l'e-commerce (mentionné comme fonctionnalité transverse)
- Constructeur de chatbot, formulaires, qualification de leads
- Déclencheurs d'automatisation quotés (1 000 / 2 000 / 5 000 par mois selon palier)
- **AI Co-pilot** avec crédits mensuels inclus (250 / 500 / 1 500)
- **« Astra AI Agents » listés comme add-on facturé séparément** — prix non affiché sur la page
  tarifs

Vu sur https://www.wati.io/ai-agents/ — six types d'agents IA préconstruits :
FAQ, qualification de leads, prise de rendez-vous (bout en bout), **recommandation de produits**,
**gestion de commande (suivi, retours, échanges)**, agent pédagogique.

- **Agent IA qui construit un panier / prend une commande ?** → **NON trouvé.** La page agents IA
  décrit « recommande des produits » et « suit les commandes », jamais « crée une commande » ni
  « construit un panier ». Le paiement n'est pas mentionné.
- **Bascule IA ↔ humain** → **non trouvé** explicitement sur les pages ouvertes (l'inbox d'équipe
  avec assignation existe, mais le mécanisme de handover IA→humain n'est pas décrit).
- **Relance de panier abandonné** → **non trouvé** sur les pages ouvertes.
- **Automatisations basées sur l'historique d'achat** → **non trouvé.**

### Offre et tarifs
Source : https://www.wati.io/pricing/
- **Growth** : 3 utilisateurs, pas d'utilisateur additionnel, 15 k diffusions/mois, 1 000
  déclencheurs, 2 intégrations commerce/CRM, 10 k appels API, 250 crédits AI Co-pilot.
  **Prix non lisible sans JS.**
- **Pro** (« Best Value ») : 5 utilisateurs, +24 $/utilisateur/mois, diffusions illimitées,
  2 000 déclencheurs, 5 intégrations dont HubSpot, 200 k appels API, 500 crédits IA.
  **Prix non lisible sans JS.**
- **Business** : 5 utilisateurs, +69 $/utilisateur/mois, diffusions illimitées avec remises
  volume, 5 000 déclencheurs, intégrations illimitées dont Salesforce, 20 M appels API,
  1 500 crédits IA, add-on « Blitz » (12 k messages/minute). **Prix non lisible sans JS.**
- **Pay-As-You-Go mono-utilisateur** : ₹999 une fois, sans abonnement, avec ₹999 de crédits
  messages.
- **Essai gratuit : 7 jours**, sans frais de setup.
- Add-ons : intégration Shopify **4,99 $/mois**, crédits AI Co-pilot, déclencheurs
  supplémentaires, numéros WhatsApp additionnels (prix non précisé), services pro à l'heure.
- Annuel : jusqu'à 25 % d'économie. **Pas de remboursement en cas d'annulation.**

⚠️ **Les prix de base des 3 paliers principaux n'ont pas pu être lus** (grille en JS). À
revérifier avec un navigateur.

### Traitement du coût des messages Meta
**Répercuté au client, facturé au message.** Citation de la page :
« You're billed per message, making costs easier to predict, control, and optimize. »
Le tarif dépend du pays du destinataire et du type de template (marketing / utility /
authentication). Le client est renvoyé au barème WhatsApp. **Marge Wati sur les messages : non
trouvée** (rien n'indique une marge, rien ne l'exclut non plus).

### Cible déclarée
PME et équipes de vente/support ; secteurs non restreints. La présence d'un plan PAYG mono-
utilisateur à ₹999 signale un tropisme fort petites structures / marché indien.

### Intégrations
Shopify (add-on payant), HubSpot (à partir de Pro), Salesforce (Business), « 2 à 5 intégrations
commerce/CRM » selon palier, API + webhooks. **Passerelles de paiement : non trouvées.**

### Différenciant apparent
Le découplage explicite « plateforme » / « crédits IA » / « agents IA en add-on » : Wati vend l'IA
à la consommation par-dessus un socle inbox+campagnes, plutôt que de l'intégrer au prix.

### Marchés desservis
Tarification en **USD et INR** observée. **Aucune mention de l'Afrique subsaharienne, du mobile
money ou du XAF sur les pages ouvertes — non trouvé.**

---

## 2. Interakt (by Jio Haptik)

**URL** : https://www.interakt.shop — tarifs : https://www.interakt.shop/pricing/
**Année de lancement** : **non trouvée** sur le site. Appartient à Jio Haptik (mention en en-tête
du site).

### Fonctionnalités clés réelles
Vu sur https://www.interakt.shop/pricing/ et https://www.interakt.shop/ :
- **Catalogues produits** (inclus dès Growth)
- **Paiements natifs WhatsApp** (« native payments », inclus dès Growth)
- **« Checkout bot »** — bot de finalisation de commande
- **Panneau de gestion des commandes**
- **Relance automatique de panier abandonné** ← explicitement listé
- **Boîte de réception partagée** WhatsApp/Instagram, agents illimités sur tous les paliers payants
- Chatbots linéaires (Growth) puis **chatbots à branches + auto-assignation des chats + webhooks**
  (Advanced)
- Campagnes de masse avec ciblage, suivi de clics et de conversions, relances automatiques de
  campagne, Click-to-WhatsApp
- **Agents IA en add-on** : qualification de leads, support client, **agents de vente**
- CRM commercial autonome (pipeline, auto-assignation)
- RCS en fallback de WhatsApp (palier Enterprise)

- **Agent IA qui construit le panier ?** L'add-on mentionne des « sales agents » mais **la
  construction de panier par l'IA n'est pas décrite explicitement — non trouvé.** Le parcours
  commerce décrit passe par le catalogue + checkout bot, pas par l'agent IA.
- **Bascule IA ↔ humain** : auto-assignation des chats présente (Advanced) ; **le handover
  IA→humain n'est pas décrit explicitement — non trouvé.**
- **Automatisations basées sur l'historique d'achat** : campagnes « avec ciblage » mentionnées,
  mais le critère « habitude d'achat » n'est pas décrit — **non trouvé.**

### Offre et tarifs
Source : https://www.interakt.shop/pricing/
- **Starter** : **gratuit**, Instagram uniquement, agents illimités (rôle propriétaire),
  campagnes de masse, inbox partagée, automatisations simples
- **Growth** : **55 $/mois** (ou ₹4 347/mois avec 8 % de remise trimestrielle) — WhatsApp +
  Instagram, agents illimités tous rôles, campagnes avancées, **catalogues, paiements natifs**,
  chatbots linéaires, analytics
- **Advanced** : **69 $/mois** — ajoute chatbots à branches, auto-assignation, webhooks
- **Enterprise** : sur devis — WhatsApp + Instagram + RCS, **« no markup charges »**, account
  manager dédié
- **Sales CRM autonome** : **₹2 499/mois** (≈30 $), 5 agents commerciaux, conversations
  illimitées ; agent supplémentaire ₹499/mois
- **Add-on Agents IA** : **74,99 $/mois** (pour Growth & Advanced) ← plus cher que la plateforme
  elle-même
- **Essai gratuit** : disponible (durée non précisée)

### Traitement du coût des messages Meta
**Répercuté, facturé séparément**, barème affiché pour l'Inde :
marketing ₹0,949 · authentication ₹0,127 · utility ₹0,140 · **service : gratuit**.
Autres régions : barème régional renvoyé par lien.
⚠️ Point important : la mention **« no markup charges »** réservée au palier Enterprise implique
**qu'une marge existe sur les paliers inférieurs**. C'est le seul acteur du panel où cette marge
est aussi lisible en creux.

### Cible déclarée
« 50 000+ entreprises dans le monde ». Secteurs listés : retail, hôtellerie, immobilier, vente
B2B. Profil PME e-commerce.

### Intégrations
WhatsApp Pay, catalogue, Shopify/e-commerce (implicite via « catalogues » et « cart recovery » —
liste exacte **non trouvée**), webhooks, Instagram, RCS. **Passerelles de paiement précises :
non trouvées sur la page tarifs.**

### Différenciant apparent
C'est le produit du panel dont la **chaîne commerce est la plus complète et la plus explicitement
packagée à bas prix** : catalogue + paiement natif + checkout bot + panneau commandes + relance
panier abandonné, tout ça dès **55 $/mois**.

### Marchés desservis
Facturation **USD et INR**, barème messages détaillé pour l'Inde uniquement. Fortement centré
Inde. **Afrique subsaharienne, mobile money, XAF : non trouvés.**
⚠️ Réserve majeure : « WhatsApp Payments » natif est **limité géographiquement** (lancé en Inde,
extension progressive) — un guide Interakt ouvert à
https://www.interakt.shop/features/whatsapp-payments/ indique « Not all countries support
WhatsApp Payments » et mentionne UPI comme méthode principale. **Le paiement natif dans WhatsApp
n'est donc pas transposable au Cameroun.**

---

## 3. AiSensy

**URL** : https://aisensy.com — tarifs : https://aisensy.com/pricing/
**Année de lancement** : **non trouvée** (Inde). *Note : le domaine `www.aisensy.com` a été
bloqué au fetch ; `aisensy.com` sans www a fonctionné.*

### Fonctionnalités clés réelles
Vu sur https://aisensy.com/ et https://aisensy.com/pricing/ :
- Diffusion / broadcast WhatsApp à grande échelle
- Constructeur de chatbot **drag & drop** (5 chatbots inclus, génération IA : 3 gratuites)
- **Partage de catalogue** et **gestion du panier** (« catalog & cart management ») ← explicite
  sur la page tarifs
- **Encaissement via WhatsApp Pay + intégrations Razorpay, PayU**
- **Agents IA WhatsApp** (offre séparée) avec **base de connaissances, mémoire long terme et
  tool calling** ← le tool calling est le point notable : l'agent peut appeler des fonctions
  externes
- WhatsApp Forms pour la capture de leads
- **Live chat multi-agents** (inbox partagée)
- Click-to-WhatsApp ads, analytics temps réel, suivi de clics

- **Agent IA qui construit le panier ?** Le « cart management » et l'« AI Agent Builder » sont
  vendus dans **deux offres différentes**. Que l'agent IA construise lui-même le panier n'est
  **pas affirmé — non trouvé.** Le tool calling le rendrait techniquement possible.
- **Bascule IA ↔ humain** : **non trouvée** explicitement.
- **Relance panier abandonné / automatisations sur historique d'achat** : **non trouvées.**

### Offre et tarifs
Source : https://aisensy.com/pricing/ (tarifs Inde 2026)
- **Drag & Drop Chatbot Builder** : **₹2 500/mois** (mensuel) ou **₹2 250/mois** (annuel, −10 %)
  → 5 chatbots, 3 générations IA gratuites, partage de catalogue, gestion du panier
- **WhatsApp AI Agent Builder** : **₹3 500/mois** (mensuel) ou **₹3 150/mois** (annuel, −10 %)
  → 3 500 messages IA/mois, base de connaissances, mémoire long terme, tool calling
- **Add-on numéro virtuel indien** : ₹2 000 + GST/an, ou ₹299/trimestre
- **Plan gratuit disponible** avec fonctionnalités limitées
- **Toute la facturation est prépayée**

### Traitement du coût des messages Meta
**Répercuté, déduit d'un crédit prépayé.** Barème Inde affiché :
marketing **₹1,09/message**, utility et authentication **₹0,145/message**, service **gratuit**
dans la fenêtre de 24 h.
**Marge AiSensy sur les messages : non trouvée** (aucune marge annoncée, aucune démentie).

### Cible déclarée
« 210 000+ entreprises dans 68+ pays » (page d'accueil). PME, très volumétrique.

### Intégrations
WhatsApp Pay, **Razorpay, PayU**, Meta Ads (CTWA), API. Liste complète **non trouvée**.

### Différenciant apparent
**Le découpage tarifaire par capacité et non par volume de contacts** : on achète « le
constructeur de chatbot » ou « le constructeur d'agent IA » comme deux produits distincts, à des
prix très bas (~26 $ et ~37 $/mois au taux courant). C'est le modèle le moins cher du panel.

### Marchés desservis
Facturation et barème **exclusivement en INR** sur les pages ouvertes. « 68+ pays » revendiqués
mais **aucune liste**. **Afrique subsaharienne, mobile money, XAF : non trouvés.**

---

## 4. Zoko

**URL** : https://www.zoko.io — tarifs : https://www.zoko.io/pricing
**Année de lancement** : **non trouvée sur le site**. *Source secondaire (recherche) : fondée en
2017, Bangalore — non vérifiée à la source.*

### Fonctionnalités clés réelles
Vu sur https://www.zoko.io/ :
- **Synchronisation du catalogue Shopify vers WhatsApp** : « Sync your Shopify store catalog with
  WhatsApp and automatically sell products to customers right inside WhatsApp »
- Diffusions WhatsApp personnalisées à l'échelle
- **Zoko Flows** : automatisations, de la simple confirmation de commande COD (paiement à la
  livraison) aux workflows multi-étapes connectés à Shopify et à d'autres apps (ex. judge.me)
- Hub de communication partagé pour le support

Vu sur https://www.zoko.io/pricing — **trois agents IA nommés et facturés séparément** :
- **Guru** : assistant FAQ — 0,09 $/résolution (100 premières gratuites)
- **Wismo** : suivi de commande (« where is my order ») — 0,09 $/résolution (100 premières
  gratuites)
- **Sello** : **agent de vente** — **3 % de la valeur de la commande** (100 premières commandes
  gratuites)
- Coût de base des agents IA : **24,99 $/mois par agent**
- **Appels vocaux** inclus par palier (500 à 4 000 minutes) puis 0,005 à 0,002 $/min

- **Agent IA qui construit le panier / prend la commande ?** L'existence de « Sello », facturé
  **au pourcentage de la valeur de commande**, implique fortement une attribution de vente — mais
  **le détail de ce que Sello fait concrètement n'a pas pu être lu** (page
  https://www.zoko.io/zoko-ai-agents en 404). **À revérifier.**
- **Paiement dans le flux WhatsApp** : **non trouvé.** La page tarifs ne mentionne « ni liens de
  paiement natifs, ni inbox partagée, ni panier/catalogue comme fonctionnalités payantes
  distinctes ». La page d'accueil ne décrit ni liens de paiement, ni checkout, ni relance de
  panier abandonné.
- **Bascule IA ↔ humain** : **non trouvée.**

### Offre et tarifs
Source : https://www.zoko.io/pricing (mensuel)

| Palier | Prix | Conversations | Appels | Agents |
|---|---|---|---|---|
| Starter | **49,99 $** | marge de 0,015 $/conversation | 500 min + 0,005 $/min | illimités, gratuits |
| Plus | **79,99 $** | 5 k incluses puis 0,00199 $ | 1 k min + 0,004 $/min | 5 puis +15 $ |
| Elite | **139,99 $** | 100 k incluses puis 0,00099 $ | 2 k min + 0,003 $/min | 10 puis +12 $ |
| Max | **499,99 $** | 5 M incluses puis 0,00049 $ | 4 k min + 0,002 $/min | 30 puis +9 $ |

- **Essai gratuit : 7 jours**, sans contrat, annulable à tout moment
- **Zoko Flows** : 11 flux essentiels gratuits ; flux personnalisés premium **5,99 $/mois chacun**
  (500 k étapes/mois incluses)

### Traitement du coût des messages Meta
**Répercuté** (barème Meta séparé) **AVEC marge explicitement affichée** : le palier Starter
indique une **marge de 0,015 $ par conversation**, qui décroît fortement avec le palier
(0,00199 → 0,00049 $). C'est le **seul acteur du panel qui affiche publiquement et chiffre sa
marge sur les messages**. Fait notable et directement utile pour ContexFly.

### Cible déclarée
Marchands **Shopify** en priorité (D2C e-commerce). Taille : de la petite boutique (Starter) au
gros volume (Max, 5 M conversations).

### Intégrations
**Shopify** (centrale), judge.me, autres apps via Flows. **Passerelles de paiement : non
trouvées.**

### Différenciant apparent
**La facturation de l'agent de vente au pourcentage du chiffre d'affaires généré (3 %)** — modèle
à la performance, unique dans ce panel. Et la transparence sur la marge par conversation.

### Marchés desservis
Prix affichés en **USD** uniquement. **Aucune mention d'Afrique, de mobile money ou de XAF —
non trouvé.** Une fonctionnalité « confirmation de commande COD » (paiement à la livraison)
suggère une orientation marchés émergents, mais rien de géographiquement explicite.

---

## 5. Yalo

**URL** : https://www.yalo.ai
**Année de lancement** : **non trouvée sur le site** (page /about-us en 404). *Source secondaire
(presse, PRNewswire/CX Today) : fondée en 2015 par Javier Mata, ~97 M$ levés, 50 M$ en Série C —
non vérifiée à la source.*

### Fonctionnalités clés réelles
Vu sur https://www.yalo.ai/ :
- Se positionne comme « the first intelligent sales platform with agents »
- **Agent IA de vente nommé « Oris »** — « recrée la performance des meilleurs vendeurs »
- **Commerce conversationnel** multicanal : WhatsApp, applications mobiles, **appels**
- **Recommandations produits par machine learning** pour augmenter le panier moyen
- Plateforme modulaire de gestion du parcours client complet
- Métriques revendiquées : 3× de conversion vs e-commerce traditionnel, +40 % de panier moyen,
  +49 % de SKU par commande, **4 md+ de transactions traitées, 4,4 M de boutiques actives**

- **Agent IA qui construit une commande** : **fortement suggéré** par « +49 % de SKU par commande »
  et le positionnement B2B de réassort, mais **le mécanisme n'est pas décrit — non trouvé.**
- **Paiement dans le flux, inbox partagée, bascule IA↔humain, relance panier abandonné** :
  **non trouvés** sur la page ouverte.

### Offre et tarifs
**Aucune information tarifaire publiée.** Vente enterprise, sur devis. **Pas d'essai gratuit
visible.**

### Cible déclarée
**Grandes entreprises**, très clairement : services financiers, télécoms, e-commerce.
Clients cités : Nestlé, Coca-Cola FEMSA, Mondelez, PepsiCo, Unilever, Heineken.
Modèle typique : **B2B de distribution** (la marque vend à ses détaillants via WhatsApp), pas B2C.

### Intégrations
**Non trouvées** sur la page ouverte.

### Différenciant apparent
Le seul acteur du panel positionné sur le **B2B distribution à grande échelle** (marque → réseau
de détaillants), avec un agent IA de vente comme produit principal, pas comme add-on.

### Marchés desservis
Revendique une présence dans **« 40+ pays en Amérique latine, Afrique et Europe »** (page
d'accueil yalo.ai). ⚠️ **L'Afrique est mentionnée explicitement sur leur site** — c'est le seul
du panel établi dans ce cas. *Note : une source secondaire (presse) situe leurs opérations aux
USA, Mexique, Brésil et Inde, sans mention d'Afrique — contradiction non résolue.*
**Mobile money / XAF : non trouvés.**

---

# PARTIE 2 — 5 PRODUITS ÉMERGENTS

---

## 6. Flowcart (ex-Sukhiba) — **le plus proche de ContexFly de tout le panel**

**URL** : https://www.flowcart.ai — tarifs : https://www.flowcart.ai/pricing
**Année de lancement** : marque **Flowcart lancée en 2025** (rebranding). *Source secondaire
(Techmoonshot, techparley) : société d'origine Sukhiba, fondée en 2020/2021 au Kenya par Ananth
Gudipati et Abhinav Reddy, 1,55 M$ d'extension de seed en août 2024 mené par EQ2 Ventures avec
Accion Venture Lab, Musha Ventures, Quona Capital, CRE Ventures — non vérifié à la source.*
Opéré par **10Agrow Technologies** (mention sur leur blog).

### Fonctionnalités clés réelles
Vu sur https://www.flowcart.ai/ et https://www.flowcart.ai/blog/what-is-flowcart :
- **« Close every sale inside WhatsApp »** — sans redirection hors de WhatsApp
- **Catalogue complet chargé en Webview dans WhatsApp** : le client parcourt, choisit des
  variantes, **ajoute au panier et paie sans quitter l'app** — revendiqué « en moins de 90
  secondes » ← **c'est exactement la page panier éditable de ContexFly**
- **Checkout et paiement in-chat**, **50+ passerelles de paiement** mondiales
- **Construction et partage de panier depuis la conversation**
- **Agents IA spécialisés** : agent de récupération de panier, agent de winback (clients dormants),
  agent d'upsell, agent d'avis, chat IA
- **Recommandations produits dynamiques** basées sur le comportement et le stock, questions de
  qualification, guidage produit visuel
- **« AI handles first responses, tags queries, and prepares drafts »** + **« Human agents can
  jump in at any point »** ← **bascule IA↔humain confirmée**
- **Inbox multi-agents**
- **Programme de fidélité automatisé** : récompenses et offres VIP pour clients récurrents,
  points, notifications de paliers, relances personnalisées ← **c'est le volet fidélisation de
  ContexFly, déjà fait**
- Pop-ups d'opt-in WhatsApp, pubs Click-to-WhatsApp, campagnes de diffusion segmentées
- Gamification : sondages de découverte produit, roues de la fortune, cartes à gratter
- Notifications de commande, intégrations ERP
- Meta Business Solution Partner officiel, **certifié SOC 2 Type II**

**Réponse à toutes les questions du cahier des charges : OUI sur tout** — agent IA, catalogue,
panier construit en conversation, paiement dans le flux, inbox partagée, bascule IA↔humain,
relance de panier abandonné, fidélité sur historique d'achat.

### Offre et tarifs
Source : https://www.flowcart.ai/pricing

| Palier | USD | INR | Frais transaction |
|---|---|---|---|
| **Growth** | **69,99 $/mois** | ₹6 500/mois | gratuit jusqu'à 3 k$ de CA WhatsApp/mois, puis **1,5 %** |
| **Pro** | **139,99 $/mois** | ₹13 000/mois | gratuit jusqu'à 5 k$, puis **1 %** |
| **Advanced** | **199,99 $/mois** | ₹18 500/mois | gratuit jusqu'à 10 k$, puis **0,5 %** |

- **Devises additionnelles proposées : KES, NGN, ZAR** ← shilling kényan, naira nigérian, rand
  sud-africain. **Aucune mention de XAF — non trouvé.**
- Tous les paliers : flux de récupération de panier, notifications de commande, **AI chat-to-search**,
  campagnes de diffusion, inbox multi-agents
- Paliers supérieurs : **agents IA de vente personnalisés**, données externes temps réel
- **Essai gratuit** : bouton « Start Free Trial » présent, **durée non précisée**
- Support dédié sur Growth et Pro

### Traitement du coût des messages Meta
**Non trouvé sur la page tarifs.** Ni marge, ni pass-through, ni mention du compte Meta du client.
**À revérifier — c'est une lacune importante.**

### Cible déclarée
Marques **D2C et retail** en marchés émergents. « 500+ entreprises » (page d'accueil), « 300+
marques » (source secondaire) dont **L'Oréal et Masoko (marketplace de Safaricom)**.
Les paliers vont de la boutique modeste (3 k$/mois de CA WhatsApp) au gros volume.

### Intégrations
**Liens de paiement générés via Razorpay, Stripe ou PayPal** (confirmé sur leur blog),
**50+ passerelles de paiement** (page d'accueil), **app Shopify**, ERP, passerelles diverses.
⚠️ **M-Pesa** : mentionné par des **sources secondaires** (avodagroup, résumés de recherche)
comme intégration Flowcart/Sukhiba — **je ne l'ai PAS vu sur une page flowcart.ai que j'ai
ouverte**. Leur page /integrations et /features/payments renvoient 404. **À vérifier
impérativement.**
**MTN MoMo / Orange Money : non trouvés.**

### Différenciant apparent
Deux choses. D'abord, **le seul produit du panel dont l'architecture est identique à celle de
ContexFly** : catalogue en Webview + panier éditable + paiement dans le fil + fidélité. Ensuite,
**la tarification hybride abonnement + commission dégressive sur le CA généré** (1,5 % → 0,5 %),
qui aligne le prix sur la valeur réellement produite.

### Marchés desservis
**Le meilleur du panel sur l'Afrique.** Page d'accueil : « Served Markets: Africa, India, and
global regions », « built for ecommerce brands operating in emerging markets ». Blog : présence
en Inde, **Afrique de l'Est**, Asie du Sud-Est, MENA, Amérique latine ; cas client Uncover
Skincare (Kenya). Devises **KES, NGN, ZAR** dans la grille tarifaire.
**Afrique francophone / Cameroun / XAF / Orange Money / MTN MoMo : non trouvés.** Leur expansion
annoncée (source secondaire) vise le Nigeria, l'Inde et les EAU — pas l'Afrique francophone.

> **Signal fort pour ContexFly** : un concurrent financé, certifié SOC 2, partenaire Meta, avec
> exactement la même proposition de valeur, déjà installé en Afrique de l'Est et en expansion
> vers le Nigeria. Le vide restant est l'**Afrique francophone + mobile money XAF**.

---

## 7. Wassist

**URL** : https://wassist.app — tarifs : https://wassist.app/pricing
**Année de lancement** : **2025** (Londres). Levée de **1,1 M$ en pre-seed menée par Playfair**,
annoncée en juin 2026, avec Charlie Songhurst (board Meta), Paul Forster (co-fondateur Indeed),
Barney Hussey-Yeo (fondateur Cleo). Fondateur : Josh Warwick.
Sources : https://wassist.app/news/wassist-raises-1-1m-pre-seed/ (source primaire) et Dealroom.

### Fonctionnalités clés réelles
Vu sur https://wassist.app/ :
- **Agent IA déployé sur WhatsApp en quelques minutes, sans ingénieur** — on saisit l'URL de la
  boutique et l'agent est entraîné dans le ton de la marque
- Réponses aux questions pré-achat, **conseil de taille**, **recommandations produits**
- **Gestion de commande** : suivi, retours, mises à jour de livraison **sans que le client ait à
  se connecter**
- **Commerce in-chat** : découverte produit et **checkout dans la conversation WhatsApp**
- **Récupération de panier abandonné** avec relance personnalisée
- **Human handover** : escalade des conversations complexes vers le support
- **Intent data** : capture et structuration des questions clients pour le SEO et la stratégie
  de contenu ← inhabituel
- Programmable : **API REST, webhooks, SDK**

⚠️ **Nuance importante trouvée dans l'annonce de levée** : « Payments flow through the website
checkout but are surfaced within the WhatsApp thread itself. » → **le paiement passe par le
checkout du site web**, simplement exposé dans le fil WhatsApp. **Ce n'est pas un paiement natif
dans WhatsApp.** Différence structurante avec ContexFly.
- **Catalogue produits propre** : **non trouvé** (l'agent est entraîné depuis l'URL de la
  boutique, ce qui suggère une dépendance à un site e-commerce existant).
- **Automatisations basées sur l'historique d'achat** : **non trouvées.**
- **Inbox partagée** : **non trouvée** explicitement (le handover existe, l'interface non décrite).

### Offre et tarifs
Source : https://wassist.app/pricing — **facturation en livres sterling, au crédit**
(« Each message sent by an agent uses one credit »)

| Palier | Prix | Crédits inclus | Dépassement |
|---|---|---|---|
| **Free** (FR-00) | **0 £** | 1 000 crédits | — |
| **Starter** (ST-01) | **30 £/mois HT** | 10 000 crédits | 0,004 £/crédit |
| **Pro** (PR-02) | **300 £/mois HT** | 100 000 crédits | 0,003 £/crédit |
| **Business** (BZ-03) | sur devis | volume personnalisé | 0,0025 £/crédit |

- Free : agents illimités, accès API, historique 7 jours, compte WhatsApp lié
- Starter : + historique 1 mois, **numéros WhatsApp dédiés**, personnalisation du profil
- Pro : + partage d'agents, mirroring de messages, historique illimité, **jusqu'à 5 comptes
  WhatsApp**, **profils en marque blanche**, business proxy API, **options de monétisation**
- Business : + sièges personnalisés, SLA, account manager
- Génération d'images et lignes téléphoniques : coûts en crédits séparés
- **Pas d'essai gratuit à durée limitée** — il y a un **palier gratuit permanent**

### Traitement du coût des messages Meta
**Non divulgué sur la page tarifs — non trouvé.** Le modèle « 1 crédit = 1 message envoyé par
l'agent » brouille volontairement la frontière entre coût plateforme et coût Meta.

### Cible déclarée
Marques **D2C** en mode, beauté, bien-être, lifestyle. Exemples affichés : Gymshark, Glossier,
Allbirds, Charlotte Tilbury (⚠️ affichés comme exemples/inspirations, **rien n'indique que ce
soient des clients**).

### Intégrations
**API REST, webhooks, SDK**. **Aucune intégration nommée (paiement, e-commerce, CRM) trouvée.**

### Différenciant apparent
Le **palier gratuit permanent avec agents illimités et accès API**, et la **marque blanche +
options de monétisation** au palier Pro — c'est-à-dire un positionnement d'infrastructure
revendable par des agences, pas seulement d'outil final.

### Marchés desservis
**Royaume-Uni et marchés anglophones** (facturation en GBP, TVA UK). Meta Business Partner.
**Afrique subsaharienne, mobile money, XAF : non trouvés.**

---

## 8. Zipchat AI

**URL** : https://zipchat.ai — tarifs : https://zipchat.ai/pricing
**Année de lancement** : **non trouvée sur le site** (page /about ouverte, ne donne pas l'année).
Fondateurs : Ruslan Leteyski (CEO, ex-CheckoutX), Luca Borreani (CMO, ex-Udroppy), Carlo Bellati
(CTO, ex-Oracle/Salesforce). Positionné comme récent et en forte croissance.

### Fonctionnalités clés réelles
Vu sur https://zipchat.ai/pricing et https://zipchat.ai/about :
- **Agent IA de vente multicanal** : chat site web, **WhatsApp**, Instagram DM, Messenger, email
- **Agentic search** dans la base de connaissances/catalogue
- **Recommandations produits**
- **Engagement proactif** (l'agent initie la conversation)
- **Escalade vers un humain** ← bascule IA↔humain confirmée
- **AI inbox** avec transfert d'email
- Multilingue : **95+ langues** revendiquées
- Tableau de bord analytique
- Membres d'équipe illimités sur tous les paliers

- **Construction de panier par l'agent / paiement dans le flux WhatsApp** : **non trouvés.** Le
  produit est un agent conversationnel de vente et support, pas une chaîne de commande. Le
  paiement reste sur la boutique Shopify/Woo.
- **Catalogue propre** : **non trouvé** — l'agent s'entraîne sur les pages (1 000 à 300 000 pages
  selon palier), donc dépendance à une boutique existante.
- **Relance de panier abandonné / automatisations sur historique d'achat** : **non trouvées.**

### Offre et tarifs
Source : https://zipchat.ai/pricing (USD, mensuel)

| Palier | Prix | Réponses/mois | Conversations | Pages d'entraînement | Boutiques |
|---|---|---|---|---|---|
| Starter | **49 $** | 500 | ~200 | 1 000 | 2 |
| Growth | **129 $** | 1 500 | ~600 | 15 000 | 5 |
| Pro | **249 $** | 3 000 | ~1 250 | 75 000 | 10 |
| Scale | **499 $** | 6 000 | ~2 500 | 300 000 | 20 |
| Unlimited | **999 $+** | sur mesure | sur mesure | sur mesure | sur mesure |

- **Annuel : −20 %**
- Réponses supplémentaires : **49 $ pour 250 réponses**
- **Essai gratuit : 7 jours** sur chaque palier
- **Garantie satisfait ou remboursé 30 jours** sur le premier paiement, sans engagement

### Traitement du coût des messages Meta
**Non trouvé.** Le modèle est facturé « à la réponse IA » indépendamment du canal, ce qui laisse
le coût WhatsApp hors périmètre.

### Cible déclarée
Marchands e-commerce (Shopify, WooCommerce, BigCommerce, Wix) en mode, beauté, animalerie,
électronique, santé/bien-être. Secondairement : éditeurs SaaS. « 2 000+ entreprises »,
clients cités : Jackery, Police, Tropicfeel.

### Intégrations
**Shopify, WooCommerce, BigCommerce, Wix**, et **« Integrate Any External API »**.
**Passerelles de paiement : non trouvées** (hors périmètre du produit).

### Différenciant apparent
**Le seul du panel dont la métrique de facturation est la réponse IA, pas le contact ni le
message** — et le seul qui affiche une **garantie de remboursement à 30 jours**. Couverture
linguistique revendiquée (95+ langues, 40+ pays) supérieure aux autres.

### Marchés desservis
**40+ pays** revendiqués, 95+ langues. Facturation **USD**. **Afrique subsaharienne, mobile money,
XAF : non trouvés.**

---

## 9. Wizybot

**URL** : https://www.wizybot.com — tarifs : https://www.wizybot.com/pricing
**Année de lancement** : **juillet 2023** (app Shopify publiée le 4 juillet 2023). *Source
secondaire (annuaires d'apps Shopify) — non vérifiée sur wizybot.com.* Éditeur : Wizybot Inc.

### Fonctionnalités clés réelles
Vu sur https://www.wizybot.com/pricing :
- **Agents de support client illimités**
- **Campagnes WhatsApp illimitées**
- Multicanal : **WhatsApp, Instagram, Facebook, email**
- **Automatisations WhatsApp illimitées**
- **Commentaires réseaux sociaux gérés par IA** (réponse automatique aux commentaires)
- **Workflows et tunnels IA illimités**
- Chats humains et tickets illimités
- **Génération de liens de panier** (« generates cart links ») ← le produit crée un lien panier
  pré-rempli
- Handover humain (chats humains illimités)
- Inbox / gestion de tickets
- App Shopify

- **Paiement dans le flux WhatsApp** : **non trouvé.** Le lien panier renvoie vers le checkout
  Shopify.
- **Recommandation produit** : **non spécifié** sur la page tarifs — non trouvé.
- **Automatisations sur historique d'achat / relance panier abandonné** : **non trouvées** sur
  la page ouverte.

### Offre et tarifs
Source : https://www.wizybot.com/pricing
- **Basic : 69,99 $/mois** — « idéal pour les boutiques en croissance ». Inclut 1 250 messages IA
  + 2 500 commentaires IA par mois. Dépassement : **0,07 $/message IA** au-delà de 1 250 et
  **0,05 $/commentaire IA** au-delà de 2 500.
- **Custom** : sur devis, contact par WhatsApp.
- **Essai** : « le premier mois, messages IA illimités », avec **garantie de remboursement si le
  ROI n'est pas atteint**. Durée d'essai gratuit classique : **non trouvée**.

### Traitement du coût des messages Meta
**Non trouvé** sur la page tarifs.

### Cible déclarée
Boutiques **Shopify** en croissance. Un seul palier public → cible clairement PME/petite boutique.

### Intégrations
**Shopify** (app dédiée), WhatsApp, Instagram, Facebook, email. Autres : **non trouvées**.
**Passerelles de paiement : non trouvées.**

### Différenciant apparent
**Un seul palier public à 69,99 $** avec tout en « illimité » sauf les messages IA, plus une
**garantie de remboursement adossée au ROI**. C'est le modèle tarifaire le plus simple du panel.
Et l'**automatisation des commentaires sur réseaux sociaux** comme canal d'acquisition n'apparaît
chez aucun autre.

### Marchés desservis
Facturation **USD**. Site disponible en anglais et espagnol (`/en/`) → orientation
Amérique latine probable, **non confirmée**. **Afrique subsaharienne, mobile money, XAF : non
trouvés.**

---

## 10. Chatarmin

**URL** : https://chatarmin.com — tarifs : https://chatarmin.com/pricing-marketing et
https://chatarmin.com/pricing-service
**Année de lancement** : **non trouvée sur le site**. *Source secondaire : société basée à
Vienne, fondée en 2022 — non vérifiée à la source.* (À la limite haute du critère « moins de
3 ans ».)

### Fonctionnalités clés réelles
Vu sur https://chatarmin.com/pricing-marketing :
- **Contacts, flux, campagnes et membres d'équipe illimités** sur tous les paliers
- Constructeur de newsletter **drag & drop** avec personnalisation et **A/B testing**
- **Flux d'automatisation déclenchés par événement**, avec **déclencheurs webhook**
- **Pop-ups site web, widgets, opt-ins au checkout**
- **Flux panier abandonné, post-achat et winback** ← relance panier abandonné confirmée,
  automatisations basées sur le comportement d'achat confirmées
- **Chatbot IA avec recommandations produits**
- **Segmentation et tagging CRM**
- **Tableau de bord KPI avec attribution du revenu**
- **WhatsApp Flows** avec formulaires natifs, sélecteur de calendrier, listes de navigation
  (*mentionné dans leur contenu comparatif — source : leur propre blog, donc partiale*)

- **Paiement dans le flux WhatsApp / panier construit par l'IA / catalogue produits** : **non
  trouvés.** Chatarmin est un outil de **marketing et rétention** WhatsApp branché sur Shopify,
  pas une chaîne de commande.
- **Inbox partagée / bascule IA↔humain** : une offre « Customer Service » distincte existe
  (https://chatarmin.com/pricing-service) mais **son contenu n'a pas été lu**.

### Offre et tarifs
Source : https://chatarmin.com/pricing-marketing
Trois paliers : **Growth**, **Scale**, **Global**.
⚠️ **Aucun prix affiché** — chaque palier renvoie à « Demo buchen » (réserver une démo).
Différences entre paliers :
- **Growth** : 2 intégrations, auto-onboarding, 1 numéro WhatsApp
- **Scale** : 3 intégrations, onboarding accompagné, canal Slack dédié
- **Global** : intégrations illimitées, support d'urgence 24/7, **numéros WhatsApp illimités**,
  configuration multi-boutiques
- **Essai gratuit : non mentionné sur la page tarifs — non trouvé.**
- *Source secondaire (leur propre blog) : crédits IA à 0,10–0,25 € pièce sur l'offre service —
  non vérifié sur la page tarifs.*

### Traitement du coût des messages Meta
**Point le plus intéressant, et c'est écrit noir sur blanc sur leur page tarifs** :
« Business Initiated Conversation: **€0,05 - €0,11** » avec une marge de **« €0,00 »** par
conversation, **sur tous les paliers**. → **Pass-through intégral, marge zéro, revendiquée comme
argument commercial.** À l'opposé exact du modèle Zoko.

### Cible déclarée
Marques **e-commerce européennes**, en particulier **DACH** (site en allemand, CTA en allemand).
Écosystème Shopify + Klaviyo.

### Intégrations
**Shopify et Klaviyo nativement intégrés, sans add-on séparé** (*source : leur blog comparatif,
donc partiale*). Webhooks. Nombre d'intégrations limité par palier (2 / 3 / illimité).
**Passerelles de paiement : non trouvées.**

### Différenciant apparent
**Marge zéro affichée sur les messages Meta** + **argument souveraineté des données** : serveurs
UE, société viennoise, DPA disponible dès le jour 1, aucun transfert vers un pays tiers. C'est un
positionnement RGPD/conformité, pas fonctionnel.

### Marchés desservis
**Europe, principalement DACH.** Prix en **EUR**. Serveurs UE exclusivement.
**Afrique subsaharienne, mobile money, XAF : non trouvés — et le positionnement « aucun transfert
hors UE » suggère un désintérêt structurel pour ces marchés.**

---

# PARTIE 3 — PRODUITS EXAMINÉS ET ÉCARTÉS (avec raison)

| Produit | Raison de l'écart |
|---|---|
| **Respond.io** (https://respond.io/pricing) | Établi et pertinent sur l'inbox + agents IA, mais **aucune fonctionnalité commerce** (catalogue, panier, paiement) trouvée sur la page tarifs. Positionné gestion de conversation multicanal, pas vente. Données conservées en annexe ci-dessous. |
| **SleekFlow** (https://sleekflow.io/en-gb/pricing) | Proche mais commerce limité : « custom catalog support » et **liens de paiement Stripe** seulement, pas de panier construit en conversation. Données en annexe. |
| **charles / hello-charles** (https://www.hello-charles.com/) | Établi, très proche fonctionnellement (agent IA RAG, recommandations produits, relance panier abandonné, inbox), mais **aucun tarif public** (page /pricing en 404, « Talk to us »), et positionnement enterprise DACH/EU. Données en annexe. |
| **Gupshup** (https://www.gupshup.ai) | **Page tarifs inaccessible** (302 vers gupshup.ai puis 404 sur /pricing). Modèle purement CPaaS au message. Aucun fait vérifié à la source → écarté plutôt que documenté sur des sources tierces. |
| **Manychat** (https://manychat.com/pricing) | **HTTP 403** — aucun fait vérifiable. Écarté par principe. |
| **Rasayel** (https://www.rasayel.io/pricing/) | Données tarifaires solides obtenues, mais **« aucune fonctionnalité commerce/catalogue ou traitement de paiement mentionnée »**. Hors segment. Données en annexe. |
| **Periskope** (https://periskope.app/pricing) | Inbox WhatsApp multi-numéros et gestion de groupes ; **aucune fonctionnalité commerce**. Hors segment. |
| **DoubleTick** (https://doubletick.io/pricing) | Dans le segment (catalogue, bot de commande) mais **positionné très haut en prix pour ce qu'il offre** ; conservé en annexe plutôt que dans le top 5 émergents car ni récent ni proche du modèle panier+paiement. |
| **Bik.ai** (https://bik.ai/pricing) | **Aucun prix public**, page tarifs sans grille (« Book a demo »). Fonctionnalités non vérifiables sur la page. |
| **Whautomate** (https://whautomate.com/pricing/) | **Grille tarifaire non lisible sans JS.** Seules des mentions de nav captées (inbox omnicanal, chatbots IA, workflows no-code, facturation/paiements, Shopify/WooCommerce). Insuffisant pour une fiche. |
| **AgentCraftr** (https://agentcraftr.com/) | Site **rendu entièrement en JS** — seul le titre a été capté. Positionnement affiché exactement dans le segment (« answers customers from their own catalogue, takes orders, hands over to teams »). **À revérifier en priorité avec un navigateur.** |
| **Uptail** | Domaine `www.uptail.io` **inexistant** (DNS ENOTFOUND). Piste à corriger. |
| **Zoko** | *Conservé* dans les établis, mais noter que sa page d'accueil ne mentionne « ni liens de paiement, ni checkout, ni relance de panier abandonné comme offres distinctes ». |

### Annexe — données collectées sur les écartés (utiles pour le calibrage tarifaire)

**Respond.io** — https://respond.io/pricing
Starter **79 $/mois** (948 $/an, −20 %), 1 000 contacts actifs mensuels, 5 utilisateurs de base
puis +12 $/utilisateur. Growth **159 $/mois** (1 908 $/an), 1 000 MAC, 10 utilisateurs puis
+20 $. Advanced **279 $/mois** (3 348 $/an), MAC sur mesure, 10 utilisateurs puis +24 $.
Enterprise sur devis. **Essai 7 jours sans carte.** Dépassement de contacts facturé à la demande :
**12 $ par 100 contacts** (Growth), **15 $ par 100** (Advanced). **Agents IA** (dont appels
vocaux à partir de Growth), AI Assist, résumés de conversation, **inclus sans surcoût**.
Messages WhatsApp : **frais Meta séparés**, avec possibilité de **recharger son crédit WhatsApp
depuis la plateforme**.

**SleekFlow** — https://sleekflow.io/en-gb/pricing
Pro AI **79 $/mois** (mensuel) ou 99 $/mois (annuel), 500 contacts actifs (extensible à 2 000),
3 utilisateurs. Premium AI **249 $/mois** (mensuel) ou 299 $/mois (annuel), 1 000 contacts
(extensible à 12 000), 10 utilisateurs. Enterprise AI sur devis. **Essai 7 jours** sur Pro AI.
**Réponses d'agents IA illimitées** (fair use) sur tous les paliers, base de connaissances,
**actions d'agent IA** (messagerie, assignation de contact, scoring de leads), copilote d'inbox.
**Catalogue personnalisé, liens de paiement Stripe, intégration Shopify.** Messages WhatsApp :
**frais d'hébergement mensuels + frais par message séparés**.

**charles** — https://www.hello-charles.com/
Agents IA à base de **RAG** (recherche dans une base de connaissances avant réponse), Campagnes
(1:1 à l'échelle), **Customer Journeys** (acquisition, conversion, rétention),
**recommandations produits**, **récupération de panier abandonné avec relances personnalisées**,
prise de rendez-vous bout en bout, automatisation FAQ, inbox service client conforme RGPD,
intégrations catalogue et CRM. Canaux : WhatsApp, Instagram, Messenger, Livechat, RCS, Chat Ads.
Secteurs : e-commerce, retail, automobile. Clients affichés : Fashionette, SNOCKS, Dermalogica,
Jack Wolfskin, Takko, Volkswagen, BMW. Marchés : Allemagne, Europe (localisations UK, FR, IT).
**Tarifs : non publics.**

**Rasayel** — https://www.rasayel.io/pricing/
Start **30 $/utilisateur/mois** (minimum 5), Grow **40 $/utilisateur/mois** (minimum 10),
Enterprise **à partir de 2 000 $/mois** (engagement annuel). **Essai 7 jours sans carte.**
Numéro WhatsApp additionnel **20 $/mois**, intégration Salesforce **300 $/mois**.
Messages WhatsApp : **« WhatsApp messaging fees are paid by you to WhatsApp/Meta directly »** →
pass-through pur, facturation directe par Meta.

**DoubleTick** — https://doubletick.io/pricing
Starter **169,90 $/mois** (facturé annuellement), Pro **217,80 $/mois** (facturé annuellement),
Enterprise sur devis. Inbox partagée 5 / 10 / sur mesure agents. Partage de produits et
catalogues sur tous les paliers. **« Automated ordering bot » à partir de Pro.** « AI and ChatGPT
bots » sur Enterprise seulement. **Aucune fonctionnalité de paiement mentionnée.** Frais Meta par
conversation additionnels, barème par pays, **marge non précisée**.

**Periskope** — https://periskope.app/pricing
Starter **20 $/utilisateur/mois**, Pro **30 $/utilisateur/mois**, Enterprise sur devis (minimum
50 utilisateurs ou numéros). Devises **USD, INR, BRL**. Premier numéro WhatsApp gratuit, puis
20–30 $/mois par numéro. Inbox multi-numéros, groupes et chats illimités, masquage de contacts,
résumés/réponses/flagging IA, autorépondeur IA, bot de support, moteur de règles d'automatisation,
ticketing, 3 000 crédits de messages en masse par licence/mois **sans validation de template**,
intégrations HubSpot, Google Sheets, Freshdesk, Zohodesk, Zapier. **Essai 7 jours sur Pro.**
RGPD, ISO/IEC 27001.
⚠️ L'envoi en masse « sans validation de template » suggère une connexion **non officielle** —
**non confirmé, à vérifier.**

---

# PARTIE 4 — SYNTHÈSE

## A. Fonctionnalités quasi universelles (le socle attendu implicitement)

Présentes chez la quasi-totalité des produits ouverts :

1. **Accès à l'API officielle WhatsApp Business Cloud** avec statut Meta Business/Solution
   Partner mis en avant comme gage de sérieux — c'est devenu un prérequis de crédibilité, pas un
   différenciant.
2. **Boîte de réception partagée multi-agents** avec assignation. Universelle. Le nombre d'agents
   inclus est un levier de tarification chez presque tous.
3. **Campagnes / diffusions sortantes** avec templates approuvés par Meta, segmentation et suivi
   de clics.
4. **Constructeur de chatbot ou de flux** (no-code, drag & drop) — présent partout, souvent
   distinct de l'« agent IA ».
5. **Agent IA / assistant IA** — devenu standard en 2025-2026, mais **presque toujours vendu en
   add-on payant** (Wati Astra, Interakt 74,99 $, Zoko 24,99 $/agent, AiSensy offre séparée).
   Seuls SleekFlow, Respond.io et Zipchat l'incluent dans l'abonnement.
6. **Intégration pubs Click-to-WhatsApp (CTWA)** — quasi systématique, cohérent avec la fenêtre
   gratuite de 72 h de Meta.
7. **Intégration Shopify** — c'est *l'*intégration commerce par défaut du secteur, souvent la
   seule vraiment aboutie.
8. **Répercussion des frais Meta au client, facturés séparément de l'abonnement.** Universel :
   **aucun produit du panel n'inclut le coût des messages Meta dans son prix d'abonnement.**
9. **Essai gratuit de 7 jours** — c'est la norme absolue (Wati, Respond.io, Zoko, Rasayel,
   Zipchat, SleekFlow, Periskope). Rares exceptions : palier gratuit permanent (Interakt Starter,
   AiSensy, Wassist Free).
10. **Catalogue / partage de produits** — très fréquent chez les acteurs à orientation commerce,
    mais le plus souvent sous forme de **catalogue WhatsApp natif Meta** ou de **synchro Shopify**,
    pas de catalogue propriétaire éditable dans le SaaS.

## B. Différenciateurs rares (ce que presque personne ne fait)

1. **Le paiement réellement finalisé dans le fil WhatsApp, avec panier éditable en Webview.**
   **Un seul produit du panel le décrit clairement : Flowcart.** Wassist expose le checkout du
   site dans le fil (ce n'est pas la même chose). Interakt/AiSensy s'appuient sur WhatsApp Pay,
   **géographiquement limité (Inde/UPI)**. Zipchat, Wizybot, Chatarmin, Zoko renvoient vers le
   checkout de la boutique. **C'est le point de différenciation le plus rare du secteur, et c'est
   précisément le cœur de ContexFly.**
2. **La facturation à la performance sur le CA généré.** Deux occurrences seulement :
   Zoko (**Sello à 3 % de la valeur de commande**) et Flowcart (**1,5 % → 0,5 % au-delà d'un
   seuil de CA WhatsApp**). Tout le reste facture à l'abonnement, au contact ou au message.
3. **La transparence affichée sur la marge appliquée aux messages Meta.** Zoko affiche sa marge
   (0,015 $ → 0,00049 $/conversation selon palier), Chatarmin affiche **0,00 € de marge** comme
   argument de vente, Interakt révèle en creux qu'il applique une marge (« no markup » réservé à
   Enterprise), Rasayel fait payer Meta en direct par le client. Les autres restent muets.
4. **Un programme de fidélité automatisé natif (points, paliers, offres VIP, winback).**
   Trouvé uniquement chez **Flowcart** (fidélité + winback complets) et partiellement chez
   **Chatarmin** (flux winback et post-achat). Absent partout ailleurs.
5. **La bascule IA ↔ humain décrite explicitement.** Étonnamment rare à l'affichage : confirmée
   seulement chez **Flowcart** (« Human agents can jump in at any point »), **Wassist**
   (escalade), **Zipchat** (escalade humaine), **Wizybot** (chats humains illimités). Les
   plateformes établies (Wati, Interakt, AiSensy, Zoko) ne la documentent pas sur leurs pages
   publiques.
6. **La marque blanche / revente par agences.** Uniquement **Wassist** (profils whitelabel +
   « monetisation options » au palier Pro).
7. **Le positionnement souveraineté des données.** Uniquement **Chatarmin** (serveurs UE, aucun
   transfert pays tiers, DPA jour 1).
8. **La certification SOC 2 Type II** — uniquement **Flowcart** dans ce panel.
9. **Le multi-devises réel dans la grille tarifaire.** Flowcart (USD, INR, KES, NGN, ZAR) et
   Periskope (USD, INR, BRL). Tout le reste est mono-devise (USD, INR, EUR ou GBP).

## C. Fourchette de prix mondiale observée et modèle de facturation dominant

**Modèle dominant : abonnement mensuel par palier + frais Meta répercutés + add-on IA.**
Les axes de scaling varient : nombre de contacts actifs mensuels (Respond.io, SleekFlow), nombre
d'utilisateurs/sièges (Rasayel, Periskope, Zoko), volume de conversations (Zoko), volume de
réponses IA (Zipchat, Wizybot), volume de crédits (Wassist), ou capacités fonctionnelles
(AiSensy, Interakt).

**Fourchette d'entrée de gamme (prix public le plus bas d'un palier payant) :**

| Segment | Prix observés |
|---|---|
| Très bas de gamme / Inde | AiSensy **₹2 250–3 500/mois** (~26–41 $) · Interakt Sales CRM **₹2 499/mois** (~30 $) · Wati PAYG **₹999** une fois |
| Entrée de gamme international | Wassist **30 £/mois** · Zipchat **49 $/mois** · Zoko **49,99 $/mois** · Interakt Growth **55 $/mois** |
| Milieu de gamme | Interakt Advanced **69 $** · Wizybot **69,99 $** · Flowcart Growth **69,99 $** · Respond.io Starter **79 $** · SleekFlow Pro AI **79 $** · Zoko Plus **79,99 $** |
| Haut de gamme PME | Zipchat Growth **129 $** · Flowcart Pro **139,99 $** · Zoko Elite **139,99 $** · Respond.io Growth **159 $** · DoubleTick **169,90–217,80 $** · Flowcart Advanced **199,99 $** |
| Segment supérieur | SleekFlow Premium **249 $** · Zipchat Pro **249 $** · Respond.io Advanced **279 $** · Wassist Pro **300 £** · Zipchat Scale **499 $** · Zoko Max **499,99 $** · Zipchat Unlimited **999 $+** · Rasayel Enterprise **2 000 $+/mois** |
| Sur devis uniquement | Yalo, charles, Bik, Chatarmin, Gupshup |

**Fourchette globale utile : ~30 $ à ~250 $/mois pour une PME**, avec un point de gravité très
net **entre 49 $ et 80 $/mois** pour le palier d'entrée d'un produit commerce complet.

**Add-ons IA facturés en plus (à ne pas oublier dans la comparaison) :**
Interakt **74,99 $/mois** (soit plus cher que la plateforme), Zoko **24,99 $/mois par agent** +
0,09 $/résolution ou 3 % du CA, Wati crédits AI Co-pilot + Astra en add-on, AiSensy
**₹3 150–3 500/mois** pour l'agent IA.

**Coût variable IA au message/résolution observé** : 0,05–0,07 $ (Wizybot), 0,09 $/résolution
(Zoko Guru/Wismo), 0,196 $/réponse (Zipchat, extrapolé du pack 49 $/250 réponses),
0,004–0,0025 £/crédit (Wassist), 0,10–0,25 € par crédit IA (Chatarmin, *source secondaire*).

## D. Ce que ces produits font pour l'Afrique et le mobile money — ou ne font pas

**Constat central : le secteur mondial ignore quasi totalement l'Afrique francophone et le mobile
money.**

- **Aucun produit du panel — zéro sur dix — ne mentionne Orange Money, MTN MoMo, le franc CFA
  (XAF/XOF), le Cameroun ou l'Afrique francophone sur une page que j'ai ouverte.**
- **Deux acteurs seulement mentionnent l'Afrique** :
  - **Flowcart** — sérieusement : « Served Markets: Africa, India, and global regions », origine
    kényane (ex-Sukhiba), devises **KES, NGN, ZAR** dans la grille tarifaire, cas clients est-
    africains, clients L'Oréal et Masoko (Safaricom). Mais : **anglophone, Afrique de l'Est et
    Nigeria**, expansion annoncée vers Nigeria/Inde/EAU. **M-Pesa évoqué uniquement par des
    sources secondaires, jamais confirmé sur leur propre site** (pages /integrations et
    /features/payments en 404).
  - **Yalo** — « 40+ pays en Amérique latine, Afrique et Europe » sur la page d'accueil, mais
    **aucun détail**, et une source secondaire liste leurs opérations sans l'Afrique. Cible
    grands comptes exclusivement. Contradiction non résolue.
- **Les passerelles de paiement citées par le secteur sont toutes non-africaines** : Stripe,
  PayPal, Razorpay, PayU, Cashfree, UPI/WhatsApp Pay. **Aucun agrégateur mobile money
  (Flutterwave, Paystack, CinetPay, Notch Pay, Campay, MeSomb...) n'apparaît nulle part.**
- **WhatsApp Pay natif est un piège** : la page Interakt ouverte indique « Not all countries
  support WhatsApp Payments », lancé en Inde et étendu progressivement, reposant sur UPI. Le
  modèle « paiement natif dans WhatsApp » des acteurs indiens **n'est pas transposable au
  Cameroun** — il faudra un lien de paiement vers une page hébergée, ce qui est exactement
  l'approche « page panier éditable » de ContexFly.
- **Aucune mention de gestion de la connectivité dégradée, de mode léger, ou de bilinguisme
  FR/EN** dans le panel. Chatarmin et charles localisent en FR/IT/UK pour l'Europe, rien d'autre.
- **Facturation** : mono-devise USD/INR/EUR/GBP chez 8 produits sur 10. Flowcart est le seul à
  proposer des devises africaines, et **XAF n'en fait pas partie**.

## E. Erreurs et limites récurrentes observées

1. **L'IA vendue en add-on plus cher que la plateforme.** Interakt : plateforme à 55–69 $/mois,
   agents IA à 74,99 $/mois. Structure tarifaire qui décourage l'usage de la fonctionnalité
   centrale. Wati suit le même schéma (crédits IA quotés par palier, Astra en add-on séparé).
2. **L'opacité sur la marge appliquée aux messages Meta.** La majorité du panel écrit « frais
   Meta séparés » sans jamais chiffrer sa propre marge. Interakt le trahit en réservant
   « no markup charges » au palier Enterprise. Deux acteurs (Zoko, Chatarmin) ont fait de la
   transparence un argument — ce qui confirme que c'est un point de friction du marché.
3. **Le fossé entre le discours « vendre sur WhatsApp » et la réalité technique.** Presque tous
   promettent la vente conversationnelle mais **s'arrêtent au lien vers le checkout de la
   boutique**. Zoko : sa page d'accueil ne décrit ni checkout, ni liens de paiement, ni relance
   de panier abandonné. Zipchat, Wizybot, Wassist : le paiement sort du fil.
4. **La dépendance structurelle à Shopify.** Zipchat, Wizybot, Zoko, Chatarmin, et en partie
   Flowcart sont architecturés autour d'une boutique e-commerce préexistante. **Un commerçant
   sans site web n'est pas leur client** — c'est un angle mort massif du secteur, et la
   population exacte que vise ContexFly.
5. **Le sur-entraînement au marché indien.** Interakt, AiSensy, Wati, Zoko, DoubleTick affichent
   des barèmes en INR, des méthodes de paiement UPI/Razorpay et des numéros virtuels indiens. Ce
   qu'ils appellent « commerce WhatsApp » est calibré sur une infrastructure de paiement
   (UPI + WhatsApp Pay) qui n'existe pas en Afrique centrale.
6. **La bascule IA↔humain rarement documentée** alors qu'elle est indispensable en production —
   signal que beaucoup de plateformes traitent l'IA comme un chatbot à part, pas comme un agent
   intégré à l'inbox.
7. **Les tarifs cachés derrière une démo.** Yalo, charles, Bik, Chatarmin, Gupshup ne publient
   rien. Sur un marché PME, c'est un frein d'acquisition — et une opportunité de différenciation
   par la transparence.
8. **Le changement de modèle de facturation Meta (per-message depuis le 1er juillet 2025)** n'est
   pas répercuté uniformément : certaines pages parlent encore en « conversations » (Zoko,
   Chatarmin, DoubleTick) là où Meta facture au message délivré. Écart à surveiller dans la
   modélisation des coûts de ContexFly.

---

## Fiabilité de ce rapport — récapitulatif

| Produit | Fiabilité fonctionnalités | Fiabilité tarifs |
|---|---|---|
| Wati | Bonne (2 pages ouvertes) | **Faible — prix de base non lisibles sans JS** |
| Interakt | Bonne (2 pages) | Bonne |
| AiSensy | Bonne (2 pages) | Bonne (INR uniquement) |
| Zoko | Moyenne (page agents IA en 404) | Bonne |
| Yalo | Faible (1 page, /about-us en 404) | **Nulle — aucun tarif public** |
| Flowcart | Bonne (3 pages) | Bonne |
| Wassist | Bonne (2 pages + annonce de levée) | Bonne |
| Zipchat | Bonne (2 pages) | Bonne |
| Wizybot | Moyenne (1 page) | Bonne (1 palier public) |
| Chatarmin | Moyenne (1 page tarifs marketing) | **Faible — aucun prix affiché** |

**À revérifier en priorité avec un navigateur JS :**
1. Prix de base des paliers Wati (Growth/Pro/Business)
2. Ce que fait exactement l'agent Sello de Zoko (facturé 3 % du CA)
3. Les passerelles de paiement de Flowcart et la présence réelle de M-Pesa / mobile money
4. AgentCraftr (site 100 % JS, positionnement pourtant exactement dans le segment)
5. Whautomate et Bik.ai (grilles non lisibles)
6. Les tarifs Chatarmin et charles (non publics — nécessitent une démarche commerciale)
