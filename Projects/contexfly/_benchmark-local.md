# Benchmark concurrentiel — Volet LOCAL (Cameroun / Afrique francophone)

**Projet :** ContexFly
**Périmètre :** Cameroun en priorité, puis Afrique francophone, avec élargissement signalé quand nécessaire
**Date de la recherche :** 15 août 2026
**Méthode :** recherche web + ouverture réelle des pages via WebFetch (pas d'exécution JavaScript). Toute page non lisible ou inaccessible est signalée comme telle. Aucun prix, aucune fonctionnalité n'est affirmé sans avoir été lu sur une page ouverte.

---

## Avertissement méthodologique (à lire avant les fiches)

Trois limites qui pèsent sur la fiabilité de ce rapport :

1. **Pas de navigateur JS.** Plusieurs grilles tarifaires (Genuka, CinetPay, Ngavix, Zura) ne rendent rien en HTML brut. Elles sont marquées « non lisible sans JS — à revérifier ».
2. **Le contenu SEO local est massif et pollue tout.** Une grande partie des résultats de recherche sur « chatbot WhatsApp Cameroun » sont des articles de blog d'agences (digicommunicate.com, sangobureau.com, alivaon.com, sinedev.com, mboageek.com, whakup.com/blog...) qui décrivent des « cas clients » invérifiables. **Aucun chiffre issu de ces sources n'a été retenu comme fait.**
3. **Auto-comparatifs biaisés.** Le « comparatif complet des meilleurs chatbots WhatsApp au Cameroun » qui classe NéoBot premier est publié par NéoBot lui-même (neobot-ai.com). Traité comme du matériel marketing, pas comme une source.

---

# PARTIE 1 — Acteurs numériques

## Note de cadrage : il n'y a pas vraiment d'« établis » sur ce marché

La distinction « 5 établis / 5 émergents » demandée ne tient pas honnêtement sur ce périmètre. **Aucun acteur du commerce conversationnel WhatsApp en Afrique francophone n'a l'ancienneté, la traction vérifiable ou la notoriété qui justifierait le label « établi »** au sens du benchmark mondial. Les plus avancés (Genuka, Ayweu) revendiquent 3 000 à 4 000 clients — auto-déclaré, non audité — et existent depuis ~3-4 ans au maximum.

J'ai donc classé selon la **maturité observable** (produit vivant, tarifs publics, traction revendiquée, couverture multi-pays) plutôt que selon un statut d'« établi » qui serait une fiction.

---

## A. Les plus matures / structurés (5)

### A1. Fiitsa — le concurrent le plus direct de ContexFly, de loin

- **URL :** https://www.fiitsa.com/ — tarifs : https://www.fiitsa.com/pricing
- **Origine :** fondateur identifié comme **Galus Fotso** (source secondaire : agrégateur LinkedIn warmr.io — *non confirmé sur le site Fiitsa lui-même*). Nom camerounais, contenu 100 % français, ciblage « entrepreneurs africains ».
- **Année :** non trouvée sur le site. Tutoriels YouTube en français (« Comment créer et mettre en ligne un business sur Fiitsa ? », « Comment ajouter un produit physique sur Fiitsa ? ») → produit vivant et documenté.

**Fonctionnalités lues sur le site :**
- « Ton catalogue, tes prix, **ton panier** — tout dans la conversation WhatsApp »
- **API officielle WhatsApp Business de Meta** : « Fiitsa utilise l'API officielle WhatsApp Business de Meta. Ton numéro est vérifié et sécurisé »
- Assistants IA nommés (Leslie, Tommy, Alex, Joyce, Audrey, Naïrobi, Claude) — répartis par fonction (gestion globale, modèles de messages, formulaires…)
- **Paiement Mobile Money et carte sans quitter WhatsApp**
- **WhatsApp Flows** (formulaires et commandes natives)
- Campagnes avec modèles de messages approuvés par Meta

**Tarifs (page /pricing, lus) :**

| Plan | Prix | Commission ventes | Limites |
|---|---|---|---|
| Découverte | Gratuit | **5 %** | 1 business, 500 contacts, 1 Go |
| Pay As You Go | Gratuit à l'entrée, « 1 crédit = 100 FCFA » | **5 %** | 1 business, contacts illimités, 10 Go |
| Premium | **49 990 FCFA/mois** (~85 $ / ~80 €) | **0 %** | 1 business, 20 Go |
| Entreprise | **99 990 FCFA/mois** (~170 $ / ~160 €) | **0 %** | 1 business, 50 Go, Fiitsa Studio (1 vidéo verticale 45 s + 3 visuels 1:1) |
| Agence | Gratuit | 0 % | Businesses illimités, 200 Go, marque blanche |

14 jours d'essai gratuit, Mobile Money / Visa / Mastercard, « Annulation à tout moment, sans frais ».
*Note : la page d'accueil mentionne « commission minimum 7 % » alors que la page tarifs indique 5 % — incohérence réelle du site, non résolue.*

**Adaptation locale :** Orange Money, MTN MoMo, Wave, Moov Money, Airtel Money, Free Money, M-Pesa + Visa/Mastercard. **13 pays africains** revendiqués. Interface FR. Tarification en FCFA. Publie son propre guide sur les tarifs de l'API WhatsApp en Afrique.

**Différenciant apparent :** c'est **exactement le positionnement de ContexFly** — catalogue + panier + paiement dans la conversation WhatsApp, sur l'API officielle Meta, avec IA. Le modèle freemium à commission (5 % sur les ventes) est agressif et adapté au pouvoir d'achat : un commerçant démarre à 0 FCFA.

**Ce qui n'a PAS pu être vérifié :** la profondeur réelle de l'IA (prend-elle vraiment la commande en langage naturel, ou se contente-t-elle d'envoyer un catalogue ?), l'existence d'une boîte de réception avec bascule IA↔humain, le volet fidélisation. Les pages `/tarifs` et `/fonctionnalites` renvoient 404 ; seule `/pricing` existe.

> **C'est l'acteur à étudier en priorité, compte ouvert.** Le benchmark documentaire ne suffit pas ici : il faut s'inscrire au plan Découverte (gratuit) et tester le parcours réel.

---

### A2. Vendeur.ci — le plus complet fonctionnellement, tarification la plus basse

- **URL :** https://vendeur.ci/
- **Positionnement affiché :** « Plateforme SaaS · Côte d'Ivoire », opérationnel « en moins d'1 heure, sans compétence technique »
- **Éditeur :** non identifié sur le site (aucune mention légale trouvée) — **incertitude à noter**

**Fonctionnalités lues :**
- « Chatbot IA WhatsApp » connecté via **« API Meta officielle ou QR Code (Baileys) »** ← point important, voir plus bas
- **« Prise de commande »** automatique
- Messages vocaux : **Whisper STT + TTS Français** — l'IA comprend les vocaux, ce qui est très pertinent sur ce marché
- Boutique en ligne, catalogue illimité, gestion des stocks
- Commandes avec suivi de statuts et notifications clients
- Broadcast (images, vidéos, PDF), segmentation par groupes WhatsApp
- **Factures FNE certifiées conformes (DGI Côte d'Ivoire)** — conformité fiscale locale
- API REST développeur

**Tarifs (lus, en XOF) :**

| Plan | Prix |
|---|---|
| Gratuit | 0 XOF + 300 crédits |
| Starter | 5 000 XOF/mois |
| Docs | 12 000 XOF/mois |
| Pro | 15 000 XOF/mois (marqué « populaire ») |
| Entreprise | 35 000 XOF/mois |
| Entreprise Plus | 45 000 XOF/mois |

Consommation à l'usage : messages 5→3 XOF, **réponses IA 10→6 XOF**, documents 15→10 XOF.

**Adaptation locale :** Orange Money, Wave, MTN, Moov. Tarification XOF. Conformité FNE ivoirienne. Support des vocaux (STT) — adaptation réelle à un marché où beaucoup de clients envoient des notes vocales plutôt que du texte.

**Point critique — Baileys :** proposer une connexion **« QR Code (Baileys) »** signifie une bibliothèque non officielle qui pilote WhatsApp Web. C'est **contraire aux conditions d'utilisation de Meta** et expose au bannissement du numéro. Que ce soit proposé publiquement en dit long sur la barrière réelle à l'entrée de l'API officielle en Afrique francophone (voir Partie 3). ContexFly, sur l'API officielle uniquement, sera plus lent à onboarder mais plus solide.

**Marché desservi :** Côte d'Ivoire clairement. **Rien ne prouve une présence camerounaise** (facturation FNE = spécifique CI, devise XOF ≠ XAF même parité).

---

### A3. Genuka + Genuka WA — l'acteur camerounais le plus installé

- **URL :** https://genuka.com/fr et **https://wa.genuka.com/**
- **Origine :** Cameroun. Fondateur **Wilfried Djopa** (source secondaire : Wing Press Africa). Contact WhatsApp affiché : +237 657 389 005.
- **Traction revendiquée :** « plus de 4000 entrepreneurs en Afrique francophone » (auto-déclaré)

**Genuka (plateforme principale) :** « Le système tout-en-un pour faire grandir votre business, en ligne et en boutique » — ventes/commandes, stock, service client & avis, statistiques, comptabilité, facturation, vitrine en ligne, marketing. Plans **Light / Business / Premium / Scale**. Tarifs affichables en **FCFA XAF / EUR / USD**, semestriel ou annuel (-20 %), essai gratuit 7 jours.
> **Prix exacts : NON TROUVÉS.** La grille est rendue en JavaScript, illisible en HTML brut. *(Une recherche secondaire évoque 10 000 FCFA/mois pour 2 utilisateurs et 20 000 FCFA pour 5 utilisateurs — **non vérifié sur le site, ne pas retenir comme fait**.)*

**Genuka WA (produit séparé, tarifs lus) :** se présente comme **« API WhatsApp officielle »**, fournisseur technologique Meta accrédité.

| Plan | Prix/mois | Numéros | Messages/mois |
|---|---|---|---|
| Starter | **5 000 FCFA** | jusqu'à 5 | 500/numéro |
| Growth | **10 000 FCFA** | jusqu'à 15 | 5 000/numéro |
| Scale | **30 000 FCFA** | jusqu'à 100 | 30 000/numéro |
| Enterprise | Sur devis | Illimité | Négocié |

Fonctions : envoi/réception (« Un POST, un message »), templates, webhooks signés avec retry, multi-numéro, monitoring des états (envoyé/livré/lu), API REST. Positionnement affiché : **« Nous ne revendons pas vos conversations »**, facturation au tarif Meta sans marge. 14 jours d'essai sans carte.
**Aucune mention d'IA, de panier ou de paiement intégré sur Genuka WA.**

Sur son blog, Genuka décrit son **inbox partagée** (« un seul numéro, plusieurs agents, avec attribution des conversations ») « connectée officiellement à l'API WhatsApp Business » et se dit **« Meta Tech Partner »**. *Source : le blog de Genuka lui-même — statut de partenaire non vérifié auprès de Meta.*

**Adaptation locale :** FCFA, mentions fiscales locales (NIU, TVA — mentionné en recherche secondaire), Mobile Money, français, support WhatsApp direct.

**Lecture pour ContexFly :** Genuka WA est un **fournisseur d'infrastructure**, pas un concurrent frontal — il pourrait même être un partenaire technique (accès API officielle à 5 000 FCFA/mois). Genuka principal est un ERP/commerce léger : il chevauche le catalogue et les commandes, **pas la vente conversationnelle autonome par IA**.

---

### A4. Ayweu — le plus gros volume revendiqué sur le commerce social

- **URL :** https://ayweu.com/
- **Accroche :** « Arrête de te noyer dans tes messages WhatsApp. Gère tes commandes en paix. »
- **Traction revendiquée :** **3 000+ vendeurs, 3 pays : Sénégal, Côte d'Ivoire, Cameroun** (auto-déclaré)

**Fonctionnalités lues :** organisation automatique des commandes/paiements/livraisons pour vendeurs sur **WhatsApp, Instagram et TikTok** ; enregistrement des paiements Wave, Orange Money, MTN Money et cartes ; suivi de livraison avec rappels automatiques ; 6 thèmes de boutique (Bannière, Sidebar, Éditorial, Galerie, Vitrine, Mosaïque) ; « Boost produits » (publicités Facebook/Instagram gérées par Ayweu). Résumé du produit : **« le catalogue et les commandes pour vendeurs sur WhatsApp, Instagram et TikTok. Un seul lien à partager partout. »**

**Tarifs (lus) :**

| Plan | Prix/mois | Contenu |
|---|---|---|
| Gratuit | 0 FCFA | 5 commandes, 20 produits max |
| Essentiel | **5 000 FCFA** | 50 commandes, produits illimités |
| Pro | **10 000 FCFA** | Commandes illimitées, 3 utilisateurs |
| Créateur | **20 000 FCFA** | Produits digitaux, envoi automatique |

Boost : Performance 14 000 / Croissance 24 000 / Maximum 38 000 FCFA pour 7 jours. **-25 % en annuel.**
Frais : **paiement à la livraison = 0 frais ; paiement en ligne = 2 % de commission.**

**Adaptation locale :** exemplaire — Wave (Sénégal), Orange Money, MTN Money, prix en FCFA, palier gratuit réel, **prise en compte du paiement à la livraison** (dominant sur ce marché) avec 0 frais.

**Ce qui n'a PAS pu être vérifié :** les pages `/tarifs`, `/fonctionnalites` et `/comment-ca-marche` renvoient 404. **Aucune preuve d'un agent IA, d'une prise de commande conversationnelle, ni d'une API WhatsApp officielle.** Le modèle lu est celui d'un **lien boutique externe partagé dans WhatsApp** + back-office de commandes. Le client sort de WhatsApp pour commander.

**Lecture pour ContexFly :** Ayweu est le concurrent le plus crédible **en traction**, mais **sur un modèle différent** — il organise l'après-conversation, il ne tient pas la conversation. C'est précisément la frontière que ContexFly prétend franchir.

---

### A5. Waazi — boîte de réception omnicanale pour l'Afrique

- **URL :** https://waazi.io/
- **Fonctionnalités lues :** centralisation « WhatsApp Business, email, chat web, SDK mobile. Tout au même endroit ». **IA Claude** pour automatiser les réponses, chatbots no-code, tableaux de bord temps réel (temps de réponse, satisfaction, volume), gestion multi-agents avec assignation automatique et SLA.

**Tarifs (lus) :**

| Plan | Prix |
|---|---|
| Starter | Gratuit (1 agent, 1 canal, 100 conversations/mois) |
| Pro | **25 000 FCFA/mois par agent** (agents illimités, 5 canaux) |
| Business | **75 000 FCFA/mois par agent** (canaux illimités) |
| Enterprise | Sur devis (SSO, on-premise, support 24/7) |

-20 % en annuel, essai 14 jours sans carte.

**Adaptation locale :** « conçue pour l'Afrique de l'Ouest », français, Mobile Money accepté, facturation FCFA, **« support local 7j/7 »**.

**Différenciant :** c'est un **helpdesk**, pas un point de vente. Pas de catalogue, pas de panier, pas de paiement. Tarification **par agent** — modèle SaaS occidental transposé, cher pour un commerçant camerounais seul (25 000 FCFA/mois pour un agent).

**Lecture pour ContexFly :** confirme que la brique « inbox + bascule IA/humain » est déjà vendue seule à 25 000 FCFA/agent sur ce marché. Ce n'est donc **pas** un différenciant de ContexFly — c'est un prérequis.

---

## B. Émergents / plus fragiles (5)

### B1. NéoBot — Yaoundé, agent IA WhatsApp

- **URL :** https://www.neobot-ai.com/ — © 2026, contact@neobot-ai.com
- **Fonctionnalités lues :** « répond et relance automatiquement vos prospects sur WhatsApp, 24h/24 » ; réponses instantanées ; relances automatiques ; base de connaissances (texte + PDF) ; génération de prompt par IA ; tableau de bord analytique (historique 30 jours) ; **5 types d'agents** (Ventes, Rendez-vous, Support, FAQ, Qualification).
- **Tarifs (lus) :** plan Essentiel **20 000 FCFA/mois** (présenté comme « environ 700 FCFA par jour »). **« Offre Fondateur » à 10 000 FCFA/mois limitée à 10 premiers clients**, « prix définitivement bloqué ». 14 jours gratuits sans carte.
- **Adaptation locale :** FCFA, français, cible « entreprises africaines », **compréhension du pidgin camerounais revendiquée** (source : leur propre article comparatif — marketing, non vérifié dans le produit). Mobile Money évoqué.
- **Maturité réelle : très faible.** Une offre « limitée aux 10 premiers clients » en 2026 signale un produit **quasiment sans client**. Aucune mention de panier, de paiement en conversation ni de catalogue. Positionné qualification de leads / support, pas point de vente.

### B2. ReplyPro — Douala, Media System SARL

- **URL :** https://replypro.cm/ — éditeur **MEDIA SYSTEM SARL** (© 2024–2026), support WhatsApp +237 673 940 405, site corporate https://www.mediasystem.cm/
- **Fonctionnalités lues :** assistant IA 24/7, base de connaissances configurable (tarifs, stocks, horaires, FAQ), réponses en langage naturel, **escalade intelligente vers l'humain**, simulation avant lancement, multicanal.
- **Tarifs (lus, XAF) :** crédit gratuit **500 XAF** à l'inscription ; à l'usage **9 XAF/réponse** minimum ; SOLO **9 900 XAF** (500 messages) ; PRO **19 900 XAF** (2 000 messages) ; BUSINESS **34 900 XAF** (6 000 messages) ; ENTREPRISE sur devis.
- **Adaptation locale : excellente.** Recharge **dès 2 000 XAF via Orange Money et MTN MoMo** — c'est le modèle prépayé/recharge, exactement le réflexe local. Support WhatsApp local.
- **Fait décisif observé :** **le canal WhatsApp est « momentanément indisponible (validation en cours) »**. Seuls le widget web, Telegram et Messenger sont opérationnels. Un chatbot « WhatsApp » camerounais qui n'a pas encore obtenu sa validation Meta — **c'est le meilleur indicateur de la vraie barrière à l'entrée sur ce marché** (voir Partie 3).
- Pas de catalogue, pas de panier, pas de paiement en conversation.

### B3. Sira — Dakar, en beta

- **URL :** https://www.sirra.org/
- **Fonctionnalités lues :** « automatisez votre WhatsApp Business avec l'IA », qualification de leads, réponses 24/7, campagnes de diffusion, temps de réponse < 2 s, installation en 2 minutes. « 1M+ messages traités ».
- **Statut affiché : « Disponible en beta ».** Essai gratuit sans carte.
- **NON TROUVÉ sur le site :** tarifs (aucun prix affiché), mention d'API WhatsApp officielle, mobile money, panier/commande/paiement.
- **Note de fiabilité :** les « clients de confiance » listés (Sénégal Logistics, Dakar Tech, Sira-Pay, WestAfrica AI) sont des noms génériques non vérifiables. Prudence.

### B4. Ozirus Agency — Cameroun (agence, pas SaaS)

- **URL :** https://ozirus.agency/
- **Nature :** **agence de services IA**, pas un produit. « Solutions concrètes, accessibles et rentables, spécialement conçues pour les réalités des PME camerounaises. »
- **Ce qu'elle vend (lu) :** agents WhatsApp qui répondent 24h/24, **acceptent les commandes**, **gèrent les paiements Mobile Money (MTN, Orange)**, mettent à jour les stocks, envoient des relances de paiement.
- **Tarifs (lus, FCFA) :** Diagnostic gratuit ; **Pilote IA 75 000–150 000** ; **Déploiement complet 150 000–400 000** ; **Suivi mensuel 15 000–30 000**. Par secteur, tout compris : Commerce/supérettes 149 000–349 000 ; Restauration 119 000–299 000 ; Pharmacies 159 000–399 000 ; Artisans 99 000–249 000.
- **Traction revendiquée :** « 35+ PME accompagnées » (auto-déclaré). Cameroun + Afrique francophone subsaharienne.
- **Lecture pour ContexFly : c'est le concurrent le plus insidieux.** Une agence qui vend exactement la promesse de ContexFly, en projet sur mesure, à 150 000–400 000 FCFA de setup + 15 000–30 000 FCFA/mois. Un commerçant qui a déjà payé un déploiement sur mesure ne s'abonnera pas à un SaaS. Et ce modèle rassure : il y a quelqu'un à appeler.

### B5. Krexora — Douala (agence e-commerce)

- **URL :** https://krexora.com/secteurs/ecommerce-retail/ — Douala, WhatsApp +237 6 76 32 77 83
- **Nature :** **agence de développement sur mesure**, « code propriétaire », pas de SaaS.
- **Tarifs (lus, FCFA) :** Boutique Starter **950 000** (jusqu'à 100 produits) ; Boutique Pro **1 500 000** (produits illimités) ; Marketplace sur devis ; **maintenance mensuelle optionnelle 55 000 FCFA/mois**.
- **Fonctionnalités :** e-commerce avec Mobile Money natif (API Orange Money et MTN MoMo), stock temps réel, tableau de bord vendeur mobile-first, **« intégration des commandes WhatsApp »** — les commandes WhatsApp et en ligne unifiées dans un seul tableau de bord.
- **Argument commercial affiché :** « 62 % des transactions e-commerce camerounaises passent par Mobile Money », que Shopify et WooCommerce ne supportent pas nativement.
- **Lecture :** ne fait pas de vente conversationnelle par IA. Utile surtout comme **repère de prix** : le marché camerounais accepte de payer ~1 000 000 FCFA pour une boutique en ligne, et 55 000 FCFA/mois de maintenance.

---

## C. Acteurs écartés, et pourquoi (important)

| Acteur | URL | Raison de l'écart |
|---|---|---|
| **Whakup** | whakup.com | Se présente comme ciblant l'Afrique francophone (CI, SN, CM, Maroc) mais **tarifs affichés en EUR uniquement** : 30 €/mois (10 000 msgs), 90 €, 450 €. ≈ 20 000 / 59 000 / 295 000 FCFA. Pas d'adaptation tarifaire ni de mobile money observé → présence commerciale réelle douteuse au Cameroun. |
| **Ngavix** | ngavix.com | Revendique un module « boutique WhatsApp » et « à partir de 10 000 FCFA/mois » (recherche secondaire). **Page non lisible sans JS.** Rien n'a pu être vérifié. À revérifier avec un navigateur. |
| **Zura** | zura.africa | « AI-Powered Marketplace for Africa », vendre sur WhatsApp. **HTTP 403** — inaccessible. Non vérifiable. |
| **WapiWay** | wapiway.tech | Basé à Cotonou (Bénin), « agents IA WhatsApp ». Page non exploitable en HTML brut (uniquement en-tête/pied de page). Rien de vérifiable. |
| **Essingan Systems** | essingansystems.com | Yaoundé, assistants IA + automatisations WhatsApp, « enregistré officiellement en 2026 ». Structure très jeune, non ouverte. |
| **Wazion** | wazion.com | Publie des comparatifs FR sur les agents IA WhatsApp e-commerce. Origine et présence africaine non établies — probablement acteur non africain faisant du SEO francophone. |
| **Jangaan Tech, CLASOFT MEDIA, 3Vision-Group, Ivoire Agent IA, Sinedev, MboaGeek, Pixl Studio** | divers | Agences de développement vendant du chatbot au projet. Pas de produit, pas de tarif public. Existent en nombre — c'est un signal (voir synthèse) mais aucune n'est un concurrent produit. |
| **Bumpa, Catlog** (Nigeria) | — | **Élargissement Afrique anglophone.** Bumpa : suite de gestion pour vendeurs sociaux, plan Premium évoqué à ₦2 000/mois (source secondaire non vérifiée sur le site). Catlog : boutique « menu » simple. Aucun des deux n'opère en zone FCFA ni ne fait de vente conversationnelle par IA. Non pertinents pour le Cameroun. |
| **Kipps.AI, SmartBizSystems, HelloDuty** (Kenya) | — | **Élargissement Afrique de l'Est.** Agents IA WhatsApp avec déclenchement de **STK Push M-Pesa** dans la conversation. Modèle intéressant techniquement mais **M-Pesa n'existe pas au Cameroun** et ces acteurs n'y opèrent pas. |

---

# PARTIE 2 — Agrégateurs de paiement Mobile Money (fournisseurs, pas concurrents)

ContexFly devra en intégrer un. Voici ce qui a été **réellement lu**, et ce qui ne l'a pas été.

### CamPay — https://www.campay.net/
- **Commissions affichées :** **2 % au dépôt (encaissement)**, **1 % au retrait**, **5 000 F par virement bancaire**
- **Opérateurs :** MTN et Orange Cameroun — « across all networks (MTN & Orange) »
- **Reversement :** « to your bank or momo by the next business day » → **J+1 ouvré**
- **Pays :** Cameroun uniquement
- **Prérequis d'inscription : NON TROUVÉ** (la page dit seulement « Sign up and subscribe to your desired API », sans détailler les documents d'entreprise exigés)
- Démo publique : https://demo.campay.net/fr/

### EnCash — https://www.encashpay.com/
- Liens de paiement personnalisés **partageables sur WhatsApp/SMS/réseaux**, QR code, collecte de fonds, tableau de bord
- **MTN MoMo + Orange Money**, Cameroun
- Affiche **« 0 % Frais cachés »** et « 2s Délai paiement »
- **Grille tarifaire réelle : NON TROUVÉE.** « Zéro frais » est une accroche marketing, pas une grille — à ne pas prendre pour argent comptant
- **Prérequis d'inscription : NON TROUVÉ.** Contact uniquement par WhatsApp (+237 694 28 91 52) ou email → **signal d'un acteur très petit / peu industrialisé**

### Lygos — https://lygosapp.com/ (inscription : pay.lygosapp.com)
- **Liens de paiement envoyés via WhatsApp**, IBAN virtuel pour virements internationaux vers wallets mobiles, API, facturation
- **13+ pays africains, 21 opérateurs mobiles connectés**
- Revendiqué : 700 000+ transactions, **97,2 % de succès en paiement instantané**, 5 000+ entreprises actives, 4,4/5 sur Trustpilot
- Inscription gratuite « en moins de 3 minutes »
- **Commissions : NON TROUVÉES** sur la page ouverte
- Publie explicitement du contenu sur « recevoir des paiements via WhatsApp Business au Cameroun » → ciblage assumé

### MeSomb — https://mesomb.com/ (éditeur : Hachther)
- Paiements en ligne, liens de paiement, **SecurePay (séquestre/escrow)**, paiements en masse et récurrents, collecte de fonds, API/SDK/webhooks, checkout hébergé, apps mobiles
- « Multiple countries »
- **Commissions, opérateurs précis, délais de reversement, prérequis : NON TROUVÉS** sur la page d'accueil (renvoi vers la doc)

### CinetPay — https://cinetpay.com/
- **Page /pricing : HTTP 403, inaccessible.** Aucun tarif vérifié.
- *Source secondaire (blog kamer-android.com, non officiel) : « MoMo 2 %, OM 2,2 %, cartes 3,5 % », dégressif de 1,5 % à 3,5 % selon volume. **À traiter comme non vérifié.***
- Acteur panafricain (levée de 1,3 Md XAF selon Business in Cameroon)

### Notch Pay — https://www.notchpay.co/
- **Page tarifs inaccessible** (erreur de certificat SSL sur notchpay.co/fr/pricing et /en/pricing — problème réel du site, à signaler)
- Page d'accueil : « Mobile Money, cards, wallets — one integration covers them all ». **Aucun chiffre, aucun pays, aucun délai affiché.**
- Doc développeur : https://developer.notchpay.co/accept-payments/mobile-money

### Autres repérés, non ouverts
CamerPay (camerpay.biz, revendique un mode BYOK à 0 % de commission sur le plan Pro — non vérifié), Monetbil, Diool, Enkap/smobilpay (enkap.cm), BKApay, CleanPay, MMGate, Paynote, kkiaPay (Afrique de l'Ouest), Flutterwave, Pawapay — **aucun tarif vérifié**.

### Coûts opérateurs sous-jacents (contexte, sources secondaires)
Frais MTN MoMo Cameroun cités : transfert 0,5 % (max 500 F), retrait 2 % (min 50 F, max 3 500 F), taxe de 0,2 % sur transferts et retraits. *Sources : cameroon-tribune, infospratiques.cm, digitalbusiness.africa — secondaires, non vérifiées auprès de MTN.*

### ⚠️ Le trou le plus dangereux du dossier
**Aucune source n'a permis de vérifier les prérequis d'inscription marchand** (RCCM, NIU, pièce d'identité du gérant, compte bancaire d'entreprise ?) chez le moindre agrégateur. C'est pourtant **le point qui décidera si ContexFly peut onboarder un commerçant informel en self-service ou non**. Un salon de coiffure ou une boutique de prêt-à-porter camerounaise n'a souvent **ni RCCM ni NIU**. Si CamPay exige un dossier d'entreprise, tout le parcours « je m'inscris et je vends dans l'heure » tombe.
→ **À trancher par contact direct avec CamPay et Notch Pay avant toute décision produit.**

---

# PARTIE 3 — Concurrents NON NUMÉRIQUES

**C'est la section décisive.** Le vrai concurrent de ContexFly au Cameroun n'est aucun des SaaS ci-dessus : c'est ce que le commerçant fait aujourd'hui, gratuitement, et qui marche assez bien pour qu'il n'ait jamais envisagé de payer.

## 3.1 L'app WhatsApp Business gratuite — le concurrent n°1

### Ce qu'elle fait déjà, gratuitement (vérifié)

| Fonction | Détail | Source |
|---|---|---|
| **Catalogue produits** | **Jusqu'à 500 articles**, « importez jusqu'à 500 articles ». 1 à 10 images ou une vidéo par produit, prix, description, lien, code. Catégories. Un seul catalogue par compte. | Page officielle Meta (whatsappbusiness.com, FR) |
| **Panier** | **Le panier existe.** Meta documente : « Clients can add up to 99 units of each single catalog item to a shopping cart, but there is no limit on the number of distinct items ». La doc développeur précise même que les messages envoyés **via la Cloud API n'affichent PAS l'icône panier** dans l'en-tête de conversation — contrairement à l'app. | developers.facebook.com (doc catalogs) |
| **Profil professionnel** | Adresse, horaires, description, site, catégorie | Meta |
| **Messages automatiques** | Message d'accueil + message d'absence | Meta |
| **Réponses rapides** | Raccourcis de réponses fréquentes | Meta / respond.io |
| **Étiquettes** | Classement des conversations (nouvelle commande, payé, expédié…) | Meta / respond.io |
| **Diffusion (broadcast)** | Listes de **256 contacts maximum par liste**, listes multiples possibles | Sources secondaires convergentes |
| **Statut** | Vitrine passive 24 h, visible des contacts qui vous ont enregistré | Sources secondaires |
| **Multi-appareils** | 1 téléphone principal + **4 appareils liés** (5 accès au total) | Sources secondaires convergentes |
| **Lien wa.me / QR code** | Point d'entrée direct en conversation | Usage courant |
| Coût | **0 FCFA** | — |

### ⚠️ Correction importante pour le cadrage de ContexFly

**Le panier n'est pas un différenciant.** L'app gratuite a un catalogue de 500 produits ET un panier où le client empile des articles et envoie sa commande. Si ContexFly se positionne sur « le panier dans WhatsApp », il vend quelque chose que Meta donne gratuitement.
*Réserve honnête : je n'ai pas pu confirmer sur une page d'aide Meta en français que le panier est activé au Cameroun spécifiquement — la disponibilité des fonctions commerce varie par région. **À vérifier sur un vrai téléphone camerounais avec un vrai compte WhatsApp Business.** C'est une vérification de 10 minutes qui peut invalider une partie du positionnement.*

### Le mur exact que l'app gratuite atteint

Voici où elle s'arrête, précisément — **c'est là et seulement là que ContexFly a le droit de facturer** :

1. **Personne ne répond quand le commerçant dort.** L'app n'a qu'un message d'absence statique. Elle ne conseille pas, ne cherche pas dans le catalogue, ne construit pas une commande. **C'est le mur n°1 et le plus rentable.**
2. **Aucun paiement.** WhatsApp Pay n'existe **qu'en Inde, au Brésil et à Singapour** (paiements marchands). **Pas disponible au Cameroun ni ailleurs en Afrique** (sources secondaires convergentes : Infobip, Fevad, AeroChat). Le commerçant doit donc dicter son numéro MoMo, attendre une capture d'écran, la lire, la croire.
3. **Le panier ne devient jamais une commande gérée.** L'app envoie un message de commande. Après, plus rien : pas de statut, pas de stock décrémenté, pas d'historique client, pas de confirmation automatique.
4. **Diffusion plafonnée à 256 contacts par liste** — et surtout : **un message de diffusion n'arrive QUE si le destinataire a enregistré votre numéro.** Les autres sont silencieusement ignorés, sans erreur. Un commerçant qui « diffuse » à 200 personnes peut n'en toucher que 40 sans jamais le savoir.
5. **Aucun ciblage.** Impossible de dire « mes clients qui ont acheté 3 fois ce trimestre ». Les étiquettes sont manuelles, jamais calculées sur l'historique d'achat. **C'est le mur qui justifie le volet fidélisation de ContexFly.**
6. **Multi-agents dégradé.** 4 appareils liés, mais tout le monde voit tout, pas d'attribution, pas de trace de qui a répondu, pas de métriques.
7. **Zéro donnée.** Pas de chiffre d'affaires, pas de panier moyen, pas de produits qui tournent.

## 3.2 Le cahier papier

Toujours dominant. Le commerçant note commandes, dettes et clients à la main.
- **Avantages réels** : 0 FCFA, zéro apprentissage, fonctionne sans réseau ni batterie, personne d'autre ne peut le lire.
- **Limite documentée** : « Si le cahier est perdu, on perd tout » ; retrouver une commande passée ou les coordonnées d'un client dans le cahier est impraticable. *(Sources : blogs d'éditeurs locaux — alivaon.com, logementmeuble.com. Sources intéressées, mais le constat est cohérent avec la pratique.)*
- **Contre ContexFly** : le cahier ne coûte rien et ne tombe jamais en panne. Un outil qui exige une connexion pour consulter une commande d'hier est **objectivement moins fiable** qu'un cahier. → exigence non fonctionnelle : consultation hors ligne des commandes récentes.

## 3.3 Le tableur partagé (Excel / Google Sheets)

Le palier « au-dessus » pour les commerçants un peu structurés.
- **Limites documentées** : saisie sur téléphone en 4G laborieuse, formules cassées, fichiers qui se multiplient, synchronisation entre plusieurs personnes compliquée. *(Source : alivaon.com — éditeur local, source intéressée.)*
- Modèles Excel de gestion de stock gratuits largement diffusés ; on trouve même des offres locales hybrides comme **GESCOMXEL** (ibigsoft.com), « logiciel de gestion commerciale Excel + Web » — preuve que le tableur est un standard local assez fort pour qu'on construise des produits *autour* de lui.

## 3.4 Le groupe WhatsApp et le statut comme vitrine

- **Statut WhatsApp** : la vitrine passive dominante. Visible 24 h par les contacts qui vous ont enregistré et autorisé. Le client regarde quand il veut, **sans se sentir démarché**. C'est gratuit, immédiat, et c'est le canal promotionnel principal des commerçantes camerounaises.
- **Groupes WhatsApp** : diffusion de photos de nouveaux arrivages, réactions et commandes dans le fil.
- **Format standard d'une annonce efficace**, tel que documenté localement : photo produit nette + **prix visible en FCFA** + appel à l'action clair + **canal de paiement direct (MTN MoMo / Orange Money)**. *(Source : sangobureau.com — blog d'agence, source secondaire.)*
- **Pourquoi c'est un vrai concurrent** : le statut a un coût marginal nul et un taux d'exposition que ContexFly ne peut pas égaler. **ContexFly ne remplacera pas le statut — au mieux il récupère la conversation que le statut déclenche.** À intégrer dans le parcours plutôt qu'à combattre.

## 3.5 Le paiement Mobile Money manuel avec capture d'écran

Le processus réel aujourd'hui, de bout en bout :
1. Le client voit un produit en statut ou dans le catalogue
2. Il écrit au commerçant
3. Négociation, disponibilité, livraison — au fil de la discussion
4. Le commerçant **dicte son numéro MTN MoMo ou Orange Money**
5. Le client paie **depuis son app MoMo**, hors de WhatsApp
6. Le client **renvoie une capture d'écran** de la confirmation dans la conversation
7. Le commerçant vérifie (ou pas) sur son propre solde, puis confirme

**Ce que ContexFly doit comprendre de ce flux :**
- Il est **gratuit côté outil** (seuls les frais MoMo standards s'appliquent)
- Il est **universellement compris** — aucune formation
- La capture d'écran est une preuve sociale acceptée, **falsifiable mais rarement falsifiée** dans un contexte de relation de proximité
- Le paiement à la livraison reste très répandu — Ayweu le reconnaît explicitement en le facturant **0 %**

→ **Un paiement automatisé n'est un gain que s'il est plus rapide ET moins cher que ce flux.** Si ContexFly ajoute 2 % de commission d'agrégateur sur une vente de 15 000 FCFA (300 FCFA) là où la capture d'écran est gratuite, **le commerçant a une raison rationnelle de refuser**. Le gain doit venir d'ailleurs : la confirmation automatique, la réconciliation, le fait de ne pas avoir à vérifier soi-même.

## 3.6 L'agence locale (concurrent hybride)

Entre le non-numérique et le SaaS : **Ozirus (149 000–349 000 FCFA pour le commerce), Krexora (950 000–1 500 000 FCFA), Essingan, MboaGeek, Wapiway, Jangaan Tech, CLASOFT, 3Vision-Group, Ivoire Agent IA, Pixl Studio, Media System…**

Ce modèle gagne aujourd'hui pour trois raisons : il y a **quelqu'un à appeler**, on paie **une fois** (pas d'abonnement récurrent qui inquiète), et la solution est **installée pour vous**. Contre l'abonnement ContexFly, c'est un adversaire sérieux, et il est nombreux.

---

# SYNTHÈSE

## 1. Y a-t-il un concurrent direct au Cameroun / en Afrique francophone ?

**Oui — un seul, et il est sérieux : Fiitsa.**

C'est la réponse nette. Fiitsa vend littéralement la promesse de ContexFly : catalogue + panier + paiement Mobile Money dans la conversation WhatsApp, sur l'API officielle Meta, avec des assistants IA, en français, en FCFA, sur 13 pays africains, avec un palier gratuit. **Il faut cesser de considérer ce marché comme vierge.**

Nuances qui comptent :
- La **profondeur réelle** de l'IA de Fiitsa n'a pas pu être vérifiée. Envoyer un catalogue via WhatsApp Flows n'est pas la même chose que négocier une commande en langage naturel. **Cette différence est peut-être tout l'espace de ContexFly — ou peut-être qu'elle n'existe pas.** Seul un test en compte réel tranchera.
- Fiitsa a **deux prix incohérents sur son propre site** (5 % vs 7 %) et des pages 404 : produit jeune, pas une forteresse.
- **Aucun autre acteur ne fait la vente conversationnelle autonome de bout en bout.** Ayweu organise l'après-conversation (lien boutique + back-office). Genuka fait de l'ERP + une inbox. Waazi fait du helpdesk. NéoBot, ReplyPro et Sira font de la qualification de leads et du support — **aucun des trois n'a de catalogue, de panier ni de paiement.**
- Sur les **10 acteurs numériques documentés, un seul (Fiitsa) couvre le périmètre complet de ContexFly.** C'est une information en soi : le marché est identifié par plusieurs équipes, mais la promesse complète n'est presque pas servie.

**Le vrai concurrent reste WhatsApp Business gratuit + le cahier + la capture d'écran MoMo.** C'est contre ça que l'abonnement doit se justifier, pas contre Fiitsa.

## 2. Fourchette de prix locale observée (FCFA)

Tout ce qui suit a été lu sur les pages des éditeurs.

| Segment | Fourchette observée |
|---|---|
| **Palier d'entrée SaaS** | Gratuit → 5 000 FCFA/mois (Ayweu Essentiel 5 000 ; Vendeur.ci Starter 5 000 XOF ; Genuka WA Starter 5 000) |
| **Cœur de marché PME** | **9 900 – 25 000 FCFA/mois** (ReplyPro SOLO 9 900 / PRO 19 900 ; Ayweu Pro 10 000 ; NéoBot 20 000 ; Ayweu Créateur 20 000 ; Waazi Pro 25 000/agent) |
| **Haut de gamme** | 34 900 – 75 000 FCFA/mois (ReplyPro BUSINESS 34 900 ; Vendeur.ci Entreprise Plus 45 000 XOF ; Waazi Business 75 000/agent) |
| **Aberration haute** | Fiitsa Premium **49 990** et Entreprise **99 990 FCFA/mois** — très au-dessus de tout le reste du marché |
| **Modèle à la commission** | Fiitsa 5 % sur ventes (plan gratuit) ; Ayweu 2 % sur paiement en ligne, **0 % au paiement à la livraison** |
| **Modèle à l'usage / prépayé** | ReplyPro 9 XAF/réponse, recharge dès 2 000 XAF ; Vendeur.ci 6–10 XOF/réponse IA |
| **Agence, one-shot** | 99 000 – 400 000 FCFA (Ozirus) ; 950 000 – 1 500 000 FCFA (Krexora) |
| **Maintenance agence** | 15 000 – 55 000 FCFA/mois |
| **Encaissement Mobile Money** | CamPay **2 % au dépôt**, 1 % au retrait, reversement J+1 ouvré |

**Ce qu'un commerçant camerounais paie aujourd'hui pour un outil comparable : entre 0 et 20 000 FCFA/mois.** Au-delà de 25 000 FCFA/mois, on quitte le commerçant individuel pour la PME structurée. **Fiitsa à 49 990 FCFA/mois est hors marché pour la cible de ContexFly** — c'est une ouverture réelle, à condition de ne pas s'y engouffrer par le bas au point de ne plus couvrir le coût de l'IA et des messages Meta.

Repère de coût : Meta facture **au message depuis le 1er juillet 2025** ; les messages de service (initiés par le client) sont gratuits, les messages utilitaires sont gratuits dans la fenêtre de service client de 24 h, les messages marketing sont toujours facturés. *Les tarifs Afrique cités par Fiitsa (utility/auth 0,0040 USD ≈ 2,4 FCFA ; marketing 0,0225 USD ≈ 13,5 FCFA) proviennent du blog d'un concurrent — **non vérifiés sur la grille officielle Meta**, que je n'ai pas pu ouvrir.*
→ **Structurellement favorable à ContexFly** : un agent IA qui répond à un client qui a écrit le premier est dans la fenêtre gratuite. C'est le volet fidélisation (marketing) qui coûtera.

## 3. Adaptations locales considérées comme acquises

Ce ne sont pas des différenciants. Ce sont des **billets d'entrée**. Tous les acteurs crédibles les ont :

1. **Prix affiché en FCFA/XAF**, pas en USD ni EUR. Whakup, qui n'affiche qu'en euros, est de fait hors marché.
2. **Paiement de l'abonnement par Mobile Money.** ReplyPro et Waazi l'affichent explicitement. Un SaaS payable uniquement par carte est mort ici.
3. **Palier gratuit ou très bas (≤ 5 000 FCFA).** Ayweu, Fiitsa, Vendeur.ci, Waazi, ReplyPro en ont tous un.
4. **Recharge prépayée plutôt qu'abonnement.** ReplyPro (dès 2 000 XAF) et Vendeur.ci (crédits) l'ont compris : le commerçant camerounais préfère recharger comme du crédit téléphonique qu'engager un prélèvement mensuel.
5. **Français d'abord.** Toutes les interfaces observées sont en français.
6. **Support par WhatsApp avec un numéro local visible.** Krexora, Genuka, ReplyPro, EnCash affichent tous un +237. Waazi va jusqu'à afficher « support local 7j/7 ».
7. **Multi-opérateurs par pays** : MTN MoMo **et** Orange Money au Cameroun — jamais un seul.
8. **Prise en compte du paiement à la livraison.** Ayweu le facture 0 %. **Ignorer ce mode, c'est ignorer une grande partie des transactions réelles.**
9. **Mobile-first.** Le commerçant gère depuis son téléphone, pas depuis un bureau.

Deux adaptations que **presque personne** ne fait, et qui sont des ouvertures réelles :
- **Le fonctionnement en connexion instable.** Aucun acteur observé ne communique sur un mode hors ligne ou dégradé. Le cahier papier, lui, marche toujours.
- **Les langues locales.** Seul NéoBot revendique le pidgin camerounais (revendication marketing non vérifiée). Le pidgin et le franglais sont pourtant la langue réelle de beaucoup de conversations commerciales à Douala.

## 4. Ce que l'app WhatsApp Business gratuite fait déjà — et le mur exact

**Elle fait déjà :** catalogue de 500 produits avec photos et prix, **panier**, profil pro, message d'accueil et d'absence, réponses rapides, étiquettes, diffusion à 256 contacts par liste, statut comme vitrine, 4 appareils liés, lien wa.me et QR. **Pour 0 FCFA.**

**Le mur, en une phrase :** l'app gratuite est un **présentoir**, pas un **vendeur**.

Les quatre points de rupture précis, dans l'ordre de leur valeur pour un commerçant :

1. **Elle ne vend pas quand il dort.** Le message d'absence ne conseille pas, ne cherche pas dans le catalogue, ne construit pas de commande, ne relance pas. **C'est le seul argument qui vaut clairement un abonnement.**
2. **Elle n'encaisse rien.** WhatsApp Pay n'existe pas au Cameroun. Le paiement sort de WhatsApp, revient en capture d'écran, et n'est jamais réconcilié.
3. **Elle ne sait rien de ses clients.** Les étiquettes sont manuelles. Impossible de calculer « clients ayant commandé 3 fois » — donc impossible de faire ce que le volet fidélisation de ContexFly propose. **C'est le deuxième argument le plus solide.**
4. **Sa diffusion est un piège silencieux.** 256 contacts par liste, et les destinataires qui n'ont pas enregistré le numéro ne reçoivent rien, sans erreur affichée. Le commerçant croit toucher 200 personnes et en touche 40.

**Le corollaire inconfortable :** le catalogue et le panier ne sont **pas** des arguments de vente pour ContexFly, contrairement à ce que suggère l'accroche « page panier éditable ». Meta les donne. Si le pitch commercial met le panier en avant, un commerçant un peu informé répondra « je l'ai déjà ». **Le pitch doit porter sur : vendre pendant que tu dors, encaisser sans capture d'écran, et savoir qui sont tes bons clients.**

## 5. Barrière à l'entrée sous-estimée : l'accès à l'API officielle

Deux observations concordantes, et elles pèsent lourd :
- **ReplyPro (Douala) affiche que son canal WhatsApp est « momentanément indisponible (validation en cours) »** alors que Telegram, Messenger et le widget web fonctionnent. Un éditeur camerounais structuré (Media System SARL) bloqué sur la validation Meta.
- **Vendeur.ci propose ouvertement une connexion « QR Code (Baileys) »** — une bibliothèque non officielle, contraire aux CGU de Meta, avec risque de bannissement du numéro. On ne propose ça que quand la voie officielle est trop lente ou trop lourde pour ses clients.

**Traduction pour ContexFly :** le choix de l'API officielle Meta est le bon choix technique et le seul défendable, mais il transforme **l'onboarding en goulot d'étranglement** — vérification Meta Business, vérification du numéro, approbation des templates. Cette friction est un **fossé défensif** face aux bricolages Baileys, et en même temps **le principal risque d'échec commercial** : un commerçant qui doit attendre deux semaines pour envoyer son premier message n'attendra pas.
→ **Le parcours d'onboarding mérite autant d'attention produit que l'agent IA lui-même.**

## 6. Les trois vérifications à faire avant d'aller plus loin

Ce rapport ne peut pas les trancher depuis un terminal.

1. **Ouvrir un compte Fiitsa gratuit et faire une commande complète de bout en bout.** C'est le seul moyen de savoir si l'IA vend vraiment ou si elle envoie juste un catalogue. Toute la différenciation de ContexFly en dépend.
2. **Vérifier le panier WhatsApp Business sur un téléphone camerounais réel.** S'il est actif au Cameroun, une partie du pitch « page panier » tombe.
3. **Contacter CamPay et Notch Pay pour connaître les documents exigés à l'ouverture d'un compte marchand.** Si RCCM/NIU sont obligatoires, l'inscription en self-service d'un commerçant informel est impossible, et le modèle d'acquisition doit être repensé.

---

## Sources principales ouvertes

Produits : [Fiitsa](https://www.fiitsa.com/) · [Fiitsa /pricing](https://www.fiitsa.com/pricing) · [Vendeur.ci](https://vendeur.ci/) · [Genuka](https://genuka.com/fr) · [Genuka WA](https://wa.genuka.com/) · [Ayweu](https://ayweu.com/) · [Waazi](https://waazi.io/) · [NéoBot](https://www.neobot-ai.com/) · [ReplyPro](https://replypro.cm/) · [Sira](https://www.sirra.org/) · [Ozirus](https://ozirus.agency/) · [Krexora](https://krexora.com/secteurs/ecommerce-retail/) · [Whakup](https://whakup.com/)

Paiement : [CamPay](https://www.campay.net/) · [EnCash](https://www.encashpay.com/) · [Lygos](https://lygosapp.com/) · [MeSomb](https://mesomb.com/) · [Notch Pay](https://www.notchpay.co/) · [CinetPay](https://cinetpay.com/) *(pricing 403)*

Meta/WhatsApp : [Tarification Cloud API](https://developers.facebook.com/docs/whatsapp/pricing/) · [Catalogs overview](https://developers.facebook.com/documentation/business-messaging/whatsapp/catalogs/catalogs-overview/) · [Catalogue WhatsApp Business (FR, officiel)](https://whatsappbusiness.com/fr/resources/resource-library/whatsapp-business-app-resources-whatsapp-business-catalog/) · [Platform pricing](https://whatsappbusiness.com/products/platform-pricing/)

Contexte (sources secondaires, signalées comme telles) : [Genuka blog WhatsApp](https://genuka.com/fr/blogs/ameliorer-service-client-whatsapp-business-vendeurs-africains) · [Fiitsa – tarifs API WhatsApp Afrique](https://www.fiitsa.com/articles/tarifs-whatsapp-business-api-afrique-2025) · [SangoBureau – promotions WhatsApp commerçantes Cameroun](https://sangobureau.com/blog/promotions-whatsapp-commercantes-cameroun) · [Alivaon – logiciels gestion commerciale Cameroun](https://www.alivaon.com/blog/meilleurs-logiciels-gestion-commerciale-cameroun) · [Infobip – WhatsApp payments](https://www.infobip.com/blog/whatsapp-payments) · [Wing Press Africa – Genuka](https://wingpressafrica.com/cameroun-une-solution-numerique-pour-mieux-gerer-les-pme/)
