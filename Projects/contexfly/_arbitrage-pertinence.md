# Arbitrage de pertinence concurrentielle — ContexFly

> Troisième volet du benchmark. Tranche une seule question : **parmi tous les acteurs listés par
> les deux chercheurs, lesquels sont réellement des concurrents pour un commerçant camerounais de
> produits physiques à catalogue — et qu'est-ce qu'il faut garder des autres ?**
> Date : 2026-08-15.

---

## Méthode et statut des sources

**Hiérarchie appliquée** (imposée par le brief) :
1. `_verifications-felix.md` (navigateur avec JS) — **fait foi** en cas de contradiction.
2. Pages ouvertes par les deux chercheurs.
3. Vérifications complémentaires faites dans ce volet — toutes sourcées ci-dessous.
4. Tout le reste : **non vérifié**, marqué comme tel.

**Vérifications ajoutées dans ce volet** (elles changent des conclusions, notamment sur Flowcart) :

| Fait | Source | Statut |
|---|---|---|
| Grille Flowcart en 5 devises : USD, INR, **KES, NGN, ZAR** — Growth 69,99 $ / KES 9 100 / ₦100 000 / R 1 200 ; Pro 139,99 $ ; Advanced 199,99 $ | https://www.flowcart.ai/pricing (rendu) | **Vérifié. Aucune devise d'Afrique francophone. XAF/XOF absents.** |
| Commission Flowcart : gratuite jusqu'à 3 k$ / 5 k$ / 10 k$ de CA WhatsApp mensuel, puis **1,5 % / 1 % / 0,5 %** | https://www.flowcart.ai/pricing | Vérifié |
| Passerelles de paiement nommées par Flowcart : **Stripe, Paystack, Apaya, DPO Pay, Airtel Money, Flutterwave, Payfast, PayMob, Razorpay** — « every major gateway across Africa », « 50+ Payment Gateways » | https://www.flowcart.ai/ (rendu) | **Vérifié — corrige le rapport mondial qui n'avait pas pu lire cette liste** |
| Flowcart : **« Install on Shopify »** comme chemin d'intégration principal ; onboarding décrit en 5 étapes dont « Connect your store or CRM » ; « 20 minutes si votre catalogue et CRM sont déjà numérisés » | https://www.flowcart.ai/ et /blog/what-is-flowcart | Vérifié |
| Flowcart / Sukhiba : M-Pesa confirmé (doc produit + presse), expansion déclarée vers **Nigeria, Inde, EAU**, consolidation Kenya + Afrique du Sud | flowcart.ai/blog, Accion, AVODA Group, wazoplus | Vérifié (sources primaires + secondaires convergentes) |
| Partenariat Apaya × Flowcart : couverture **MENA** (Tap, Telr, Tabby, Stripe, Checkout.com). **Aucune mention d'Afrique francophone, du Cameroun ni du XAF.** | https://www.apaya.io/post/apaya-partners-with-flowcart... | Vérifié |
| **Flutterwave collecte MTN Mobile Money ET Orange Money au Cameroun, en XAF** | mtn.cm (communiqué MTN Cameroun), flutterwave.com/ci/support/payment-methods/pay-with-mobile-money | **Vérifié — fait le plus lourd de conséquences de ce rapport** |
| Yalo : présence africaine — la page d'accueil revendique « 40+ pays… Afrique », les sources tierces (Tracxn, siège San Francisco, 342 employés) ne la confirment pas | recherche | **Contradiction non résolue. Non vérifié.** |

**Taux de conversion utilisé** : ≈ **590 FCFA/USD** (taux implicite du rapport local, qui convertit
49 990 FCFA ≈ 85 $). Approximatif, à revérifier avant tout calcul de tarification fin. Le XAF est
arrimé à l'euro à 655,957.

**Contradiction signalée entre les deux rapports** : le rapport local place Fiitsa comme « le
concurrent le plus direct de ContexFly, de loin » sur la foi de la page d'accueil ;
`_verifications-felix.md` montre une suite généraliste à 8 agents. **Le fichier de vérifications
fait foi** — mais la contradiction n'est pas une erreur du chercheur local : les deux lectures
sont vraies, Fiitsa *fait* de la vente conversationnelle, elle n'est simplement pas focalisée
dessus. C'est exactement l'objet de la section 2.2.

---

## Les cinq filtres d'arbitrage

Un acteur mondial n'est un concurrent pour ce projet que s'il passe **les cinq** :

| # | Filtre | Seuil |
|---|---|---|
| 1 | **Disponibilité effective** | Le commerçant peut souscrire depuis le Cameroun sans intermédiaire |
| 2 | **Encaissement** | Collecte MTN MoMo **et** Orange Money en XAF (WhatsApp Pay natif ne compte pas : indisponible en Afrique) |
| 3 | **Économie** | Abonnement dans la bande locale observée : **0 – 25 000 FCFA/mois** (cœur : 9 900 – 20 000). Au-delà de 25 000, on quitte le commerçant individuel |
| 4 | **Prérequis d'accès** | Ne suppose **ni boutique Shopify/Woo, ni site web, ni documents d'entreprise** |
| 5 | **Langue** | Interface et agent en **français** |

Le filtre 3 est celui que le brief demandait d'arbitrer : le point de gravité mondial est à
**49–80 $/mois** soit **29 000 – 47 000 FCFA**, c'est-à-dire **2 à 5× au-dessus** du cœur de marché
local. Cet écart n'est pas un détail de conversion, c'est une incompatibilité structurelle : un
produit conçu pour un marchand Shopify américain à 69 $/mois ne descendra pas à 12 000 FCFA sans
refaire son modèle.

**Une seule exception, à noter honnêtement : AiSensy.** À ₹2 250–3 500/mois (≈ **15 000 – 24 000
FCFA**), c'est le seul acteur mondial dont la structure de prix est *déjà* compatible avec le
pouvoir d'achat camerounais. Il échoue sur les quatre autres filtres, mais il prouve qu'un
éditeur indien sait construire un produit conversationnel WhatsApp rentable à ce niveau de prix.
C'est le contre-exemple qui empêche de dire « personne ne peut faire ce produit à 15 000 FCFA ».

---

# PARTIE 1 — Verdicts, acteur par acteur

## 1.1 Panel mondial

| Acteur | Filtres passés | Verdict | Raison |
|---|---|---|---|
| **Wati** | 0/5 | **Non-concurrent** | USD/INR, aucune mention Afrique/MoMo/XAF, agent IA en add-on non tarifé, et **l'IA ne prend pas la commande** (elle recommande et suit, elle ne crée pas). Prix de base non lisibles. |
| **Interakt** | 0/5 | **Non-concurrent** | Chaîne commerce la plus complète du panel — mais adossée à **WhatsApp Pay / UPI**, dont leur propre page dit « Not all countries support WhatsApp Payments ». Inutilisable au Cameroun. Coût réel : 55 $ + add-on IA 74,99 $ = **~76 500 FCFA/mois**, 4× la bande locale. |
| **AiSensy** | 1/5 (prix) | **Non-concurrent** | Seul acteur mondial dont le prix passe (15 000–24 000 FCFA). Échoue sur tout le reste : INR uniquement, encaissement via Razorpay/PayU/WhatsApp Pay (aucun ne collecte le MoMo XAF), numéro virtuel indien, anglais. **À garder en tête comme preuve de faisabilité économique, pas comme menace.** |
| **Zoko** | 0/5 | **Non-concurrent** | Le produit *est* la synchronisation du catalogue Shopify → boutique Shopify obligatoire. 49,99–499,99 $, USD. Aucun paiement dans le fil trouvé. |
| **Yalo** | 0/5 pour cette cible | **Non-concurrent sur la cible — concurrent indirect de segment** | Vente enterprise sur devis, clients Nestlé/Coca-Cola FEMSA/Unilever, modèle **B2B de distribution** (la marque commande à ses détaillants). Si Yalo arrive au Cameroun, ce sera via les Brasseries ou un opérateur télécom, pas via un salon de beauté. **Sa revendication de présence africaine est contredite par les sources tierces — non résolu.** Effet indirect réel : il normalise la commande par WhatsApp chez les détaillants, ce qui prépare le terrain de ContexFly plutôt que de le lui prendre. |
| **Flowcart** | 2/5 aujourd'hui | **Non-concurrent aujourd'hui / menace directe à 12–24 mois** | → **Section 2.1, traité en profondeur.** |
| **Wassist** | 0/5 | **Non-concurrent** | GBP, TVA UK, marché anglophone. Et surtout : **« Payments flow through the website checkout »** — un site e-commerce est requis, l'agent est entraîné depuis l'URL de la boutique. Population cible opposée à celle de ContexFly. |
| **Zipchat AI** | 0/5 | **Non-concurrent** | Shopify/Woo/BigCommerce/Wix requis (l'agent s'entraîne sur les pages du site). Ni panier construit, ni paiement : c'est un agent de vente-conseil, pas une chaîne de commande. 49–999 $. |
| **Wizybot** | 0/5 | **Non-concurrent** | App Shopify. Le « cart link » renvoie au checkout Shopify. 69,99 $ (≈ 41 000 FCFA), palier unique. |
| **Chatarmin** | 0/5 | **Non-concurrent** | DACH, EUR, **positionnement explicite « aucun transfert de données hors UE »** — c'est un désintérêt structurel pour l'Afrique, pas une absence conjoncturelle. Pas de panier, pas de paiement : c'est du marketing/rétention branché sur Shopify. |
| **Écartés du panel mondial** (Respond.io, SleekFlow, charles, DoubleTick, Periskope, Rasayel, Gupshup, Manychat, Bik, Whautomate) | 0/5 | **Non-concurrents en bloc** | Soit hors segment commerce (pas de catalogue/panier/paiement), soit devise + prix + langue incompatibles. Aucun ne mentionne l'Afrique. |
| **AgentCraftr** | **inconnu** | **Non tranché — à revérifier** | Le rapport mondial n'a pu lire que le titre (site 100 % JS), mais le positionnement affiché est *exactement* le segment : « answers customers from their own catalogue, **takes orders**, hands over to teams ». « Own catalogue » = pas de Shopify requis. **C'est le seul trou du panel mondial qui pourrait cacher un concurrent réel. À ouvrir avec un navigateur avant de clore le benchmark.** |

**Bilan mondial : 0 concurrent direct aujourd'hui. 1 menace à horizon 12–24 mois (Flowcart).
1 inconnue à lever (AgentCraftr).** Le constat du chercheur mondial tient : *zéro produit sur dix
ne mentionne Orange Money, MTN MoMo, le XAF, le Cameroun ou l'Afrique francophone.*

⚠️ **Mais la lecture « donc le mobile money est notre fossé » est fausse, et il faut le dire tout
de suite.** Flowcart intègre **Flutterwave**, et Flutterwave collecte MTN MoMo et Orange Money au
Cameroun en XAF (vérifié, communiqué MTN Cameroun). **Le rail de paiement existe déjà dans la
stack d'un concurrent.** Ce qui protège ContexFly n'est donc pas la technique du mobile money —
c'est la langue, le prix, l'absence de prérequis boutique, et le fait qu'aucun de ces acteurs n'a
décidé d'aller sur ce marché. Ce sont des barrières **commerciales**, pas techniques. Une barrière
commerciale tombe en une décision de comité ; une barrière technique tient des années.

## 1.2 Panel local

| Acteur | Verdict | Raison |
|---|---|---|
| **Fiitsa** | **Concurrent direct n°1 (numérique)** | Seul acteur à passer les 5 filtres : français, FCFA, OM/MTN/Wave/Moov/Airtel/M-Pesa, palier gratuit, API officielle Meta, 13 pays. → **Section 2.2.** |
| **Ozirus Agency** | **Concurrent direct** | Vend *littéralement* la promesse ContexFly (agent WhatsApp qui répond 24/7, **accepte les commandes**, **gère les paiements MTN/Orange**, met à jour le stock, relance) — mais en projet sur mesure : 149 000–349 000 FCFA de setup commerce + 15 000–30 000/mois. Cameroun, français, 35+ PME revendiquées. **C'est le concurrent qui prendra les 50 premiers clients de ContexFly**, parce qu'il y a quelqu'un à appeler et qu'on paie une fois. |
| **Ayweu** | **Concurrent indirect fort — direct dès qu'il ajoute un agent IA** | 3 000+ vendeurs revendiqués sur 3 pays **dont le Cameroun**, 5 000–20 000 FCFA/mois, OM/MTN/Wave, **0 % sur le paiement à la livraison**. Modèle différent (lien boutique externe + back-office) : il organise l'après-conversation, il ne la tient pas. Mais il occupe le même budget, la même douleur affichée (« arrête de te noyer dans tes messages WhatsApp ») et la même tête. Il a la traction et la base clients pour ajouter un agent IA ; ContexFly n'a ni l'une ni l'autre. |
| **Genuka / Genuka WA** | **Concurrent indirect — et fournisseur potentiel** | ERP camerounais installé (4 000+ entrepreneurs revendiqués), catalogue + commandes + stock + inbox partagée, FCFA, se dit Meta Tech Partner. Pas de vente conversationnelle par IA aujourd'hui. **Genuka WA à 5 000 FCFA/mois est de l'infrastructure API — un raccourci d'onboarding possible, pas un adversaire.** Menace réelle : c'est l'acteur local le mieux placé pour ajouter l'agent manquant (il a déjà catalogue, commandes, base clients, accès API et la marque locale). Le classer non-concurrent serait une erreur. |
| **Vendeur.ci** | **Concurrent indirect aujourd'hui — direct à l'expansion** | Le plus complet fonctionnellement du panel local (prise de commande, **STT/TTS français sur les vocaux**, boutique, stock, facturation FNE) et le moins cher (5 000–15 000 XOF). Mais **Côte d'Ivoire, XOF, conformité fiscale ivoirienne** — aucune preuve de présence camerounaise. Problème : la Côte d'Ivoire est le marché n°2 naturel de ContexFly, et Vendeur.ci y est déjà installé avec un temps d'avance. Rien ne l'empêche de traverser vers le Cameroun (même langue, parité de fait XOF/XAF) plus vite que ContexFly ne traverse vers Abidjan. |
| **Waazi** | **Non-concurrent sur le job — référence de prix** | Helpdesk omnicanal, pas de catalogue, pas de panier, pas de paiement. Sa seule utilité ici : il prouve que la brique « inbox + IA + bascule humain » se vend **seule à 25 000 FCFA/agent** sur ce marché. **L'inbox de supervision de ContexFly n'est donc pas un différenciant, c'est un prérequis.** |
| **ReplyPro** | **Non-concurrent aujourd'hui — indirect une fois validé** | Éditeur structuré (Media System SARL, Douala), excellent modèle de recharge (dès 2 000 XAF par OM/MoMo, 9 XAF/réponse). Mais **son canal WhatsApp est « momentanément indisponible, validation en cours »**, et il n'a ni catalogue, ni panier, ni paiement. Positionné support/qualification. |
| **NéoBot** | **Non-concurrent** | Pas de catalogue, pas de panier, pas de paiement. Une « offre Fondateur limitée aux 10 premiers clients » en 2026 signale un produit quasiment sans client. Seul point à surveiller : la revendication pidgin camerounais (non vérifiée). |
| **Sira** | **Non-concurrent** | Beta, Dakar, aucun tarif, aucune fonction commerce, « clients » aux noms génériques invérifiables. |
| **Krexora** | **Non-concurrent — repère de prix** | Agence e-commerce sur mesure, 950 000–1 500 000 FCFA + 55 000/mois de maintenance. Pas de vente conversationnelle. Utile pour une seule chose : montrer que **le marché camerounais accepte de payer ~1 M FCFA une fois** pour un actif commercial. Le problème de ContexFly n'est donc pas le pouvoir d'achat absolu, c'est la **résistance au récurrent**. |
| **Agences en nombre** (Jangaan, CLASOFT, 3Vision, Sinedev, MboaGeek, Pixl, Essingan, WapiWay) | **Concurrent direct collectif, individuellement négligeable** | Aucune n'est un produit. Mais leur nombre est un signal de demande **et** une couche de bruit à l'acquisition : le commerçant qui cherche « chatbot WhatsApp Cameroun » tombe sur elles avant de tomber sur un SaaS. |
| **Whakup** | **Non-concurrent** | Prétend cibler l'Afrique francophone mais n'affiche qu'en **EUR** (30/90/450 €). Hors marché de fait. |
| **Ngavix** | **Non tranché — à revérifier** | Revendique un module « boutique WhatsApp » **à partir de 10 000 FCFA/mois** (source secondaire). Si c'est exact, c'est pile dans la bande locale et sur le segment. Page illisible sans JS. **À ouvrir.** |
| **Zura** | **Non tranché** | HTTP 403, non vérifiable. |
| **Bumpa, Catlog** (Nigeria) | **Non-concurrents** | Hors zone FCFA, anglophones, pas de vente conversationnelle par IA. |
| **Kipps.AI, SmartBizSystems, HelloDuty** (Kenya) | **Non-concurrents** | M-Pesa n'existe pas au Cameroun, pas de présence. Enseignement technique conservé (STK Push in-chat). |

## 1.3 Concurrents non numériques — la vraie base de comparaison

| Acteur | Verdict | Raison |
|---|---|---|
| **App WhatsApp Business gratuite** | **Concurrent direct n°1, toutes catégories** | 0 FCFA. Catalogue 500 produits + **panier natif confirmé** (`_verifications-felix.md`). C'est Meta : elle ne disparaîtra pas, elle s'améliorera, et elle est déjà installée sur le téléphone du commerçant. |
| **Paiement MoMo manuel + capture d'écran** | **Concurrent direct sur le job « encaisser »** | Gratuit, universellement compris, aucune formation. C'est la baseline économique : **si ContexFly ajoute 2 % d'agrégateur sur une vente de 15 000 FCFA (300 F) là où la capture est gratuite, le commerçant a une raison rationnelle de refuser.** |
| **Cahier papier** | **Concurrent direct sur la fiabilité** | 0 FCFA, marche sans réseau ni batterie. Impose une exigence non fonctionnelle : **consultation hors ligne des commandes récentes**, sinon ContexFly est objectivement moins fiable qu'un cahier. |
| **Tableur / Excel** | **Concurrent indirect** | Palier au-dessus, pour les commerçants structurés. |
| **Statut WhatsApp + groupes** | **Non-concurrent — canal à intégrer** | Coût marginal nul, exposition inégalable. ContexFly ne le remplacera pas : il récupère la conversation que le statut déclenche. À traiter comme point d'entrée du parcours, jamais comme cible à battre. |

---

# PARTIE 2 — Les deux cas décisifs

## 2.1 Flowcart — concurrent dans 12 mois, pas aujourd'hui

### Ce qui est établi

Flowcart est le seul produit au monde, dans ces deux panels, dont l'architecture est identique à
celle de ContexFly : catalogue en Webview dans WhatsApp, panier éditable, checkout et paiement
dans le fil, bascule IA↔humain explicite (« Human agents can jump in at any point »), inbox
multi-agents, **programme de fidélité automatisé avec paliers, offres VIP et winback** — c'est-à-
dire aussi le volet fidélisation de ContexFly, déjà livré. Financé (1,55 M$ d'extension de seed),
certifié SOC 2 Type II, Meta Business Solution Partner, 300–500 marques revendiquées dont L'Oréal
et Masoko (marketplace de Safaricom). Origine kényane (ex-Sukhiba), rebrandé en 2025.

**Sur le mobile money, la réponse manquante est maintenant trouvée : oui, et au-delà de M-Pesa.**
Leur page d'accueil rendue nomme **Flutterwave, Paystack, DPO Pay, Airtel Money, Payfast, PayMob,
Apaya, Stripe, Razorpay** et revendique « every major gateway across Africa ». Et Flutterwave
collecte MTN MoMo **et** Orange Money au Cameroun en XAF. **Techniquement, Flowcart peut encaisser
une commande camerounaise en mobile money demain matin.**

### Pourquoi ce n'est pourtant pas un concurrent aujourd'hui

Quatre obstacles, dans l'ordre de solidité :

1. **Le prix, et il n'est pas négociable.** Growth 69,99 $ = **~41 000 FCFA/mois**, Pro ~82 500,
   Advanced ~118 000. La bande locale est 0–25 000, cœur 9 900–20 000. Flowcart Growth est **2 à
   4× au-dessus du cœur de marché**, et c'est leur *entrée de gamme*. Pire : leur grille en KES
   (9 100 KES ≈ 70 $) montre qu'ils ne font **pas** d'adaptation au pouvoir d'achat local — ils
   convertissent le prix dollar. Un acteur qui affiche déjà des devises africaines et n'ajuste pas
   le prix a fait un choix de segment, pas un oubli.
2. **La commission s'ajoute au-dessus, pas à la place.** 1,5 % au-delà de 3 000 $/mois de CA
   WhatsApp. Le seuil de gratuité (3 000 $ ≈ 1 770 000 FCFA de CA mensuel) est généreux pour la
   cible — mais l'abonnement, lui, est dû dès le premier mois.
3. **Le prérequis boutique.** « Install on Shopify » est le chemin d'intégration mis en avant ;
   l'onboarding documenté est « Connect your store or CRM », « 20 minutes **si votre catalogue et
   votre CRM sont déjà numérisés** ». Leur client type a déjà un e-commerce. **Le commerçant
   camerounais qui n'a ni site ni CRM n'est pas dans leur parcours d'onboarding** — et c'est
   exactement la population de ContexFly.
4. **La langue et l'axe d'expansion.** Aucun élément francophone trouvé. Expansion déclarée :
   Kenya + Afrique du Sud consolidés, **Nigeria, Inde, EAU** visés. Le partenariat paiement le
   plus récent (Apaya) couvre la **MENA**. Tous les axes déclarés évitent l'Afrique francophone.
   Leur clientèle affichée (L'Oréal, Safaricom, Spar, Darling Group) est corporate, pas
   micro-commerce.

### Verdict

**Non-concurrent aujourd'hui au Cameroun. Concurrent direct probable à 12–24 mois si — et
seulement si — une décision commerciale est prise.** Ce n'est pas un acteur qui « ne descendra
jamais » : il a le rail de paiement, l'implantation africaine, le financement et le produit exact.
Ce qui manque est la traduction, une grille XAF et un onboarding sans boutique. Trois chantiers de
quelques mois.

**Ce qui protège réellement ContexFly n'est pas le mobile money — c'est le segment.** Flowcart
vend à L'Oréal Kenya, pas à une boutique de Douala. Descendre à 12 000 FCFA/mois casserait leur
économie unitaire et leur modèle de vente (démo, account manager, support dédié). Le risque n'est
donc pas qu'ils arrivent sur le segment de ContexFly ; c'est qu'ils **prennent le haut du marché
camerounais** (les 5 % de clients à gros volume qui auraient été les plus rentables pour ContexFly)
et laissent le bas.

**Signaux à surveiller — s'ils apparaissent, réévaluer immédiatement** :
- Ajout de XAF ou XOF au sélecteur de devise de flowcart.ai/pricing
- Version française du site ou de la documentation
- Mention du Sénégal, de la Côte d'Ivoire ou du Cameroun dans un communiqué ou un cas client
- Un palier tarifaire sous 30 $/mois
- Une intégration CinetPay, Notch Pay ou CamPay (agrégateurs francophones)

## 2.2 Fiitsa — la dispersion est-elle une faiblesse ou ce que veut le marché ?

C'est la question la plus importante du rapport, et la réponse honnête est : **les deux, et ça
dépend d'une chose que tu ne sais pas encore.**

### Ce que dit le marché en faveur de la suite généraliste

Il faut prendre l'argument au sérieux, parce que les faits locaux le soutiennent :

- **L'acteur local le plus installé est un généraliste.** Genuka revendique 4 000+ entrepreneurs
  avec « le système tout-en-un » (ventes, stock, service client, statistiques, comptabilité,
  facturation, vitrine, marketing). Ce n'est pas un spécialiste qui a gagné.
- **Le second par la traction est aussi un agrégateur de canaux.** Ayweu (3 000+ vendeurs) unifie
  WhatsApp, Instagram **et** TikTok. Sa promesse est « un seul lien à partager partout ».
- **Vendeur.ci, le plus complet du panel local, dérive lui aussi vers le généraliste** : boutique,
  stock, broadcast, **et facturation fiscale FNE**.
- **L'arithmétique du commerçant.** À 500 000 FCFA/mois de chiffre d'affaires, personne ne
  souscrit cinq abonnements. Un outil à 15 000 FCFA qui fait cinq choses bat cinq outils à 10 000
  qui en font une chacun, même si chacun la fait mieux.
- **Le job réel n'est pas « vendre sur WhatsApp », c'est « faire tourner ma boutique ».** La
  facturation, le stock et la conformité fiscale sont des besoins adjacents authentiques, pas des
  gadgets.

Trois sources locales indépendantes convergent vers le généraliste. **C'est un signal, pas du
bruit.** Prétendre que « le commerçant camerounais veut un outil focalisé » serait une conviction
de développeur, pas une observation.

### Ce qui rend la dispersion de Fiitsa attaquable malgré tout

- **Huit agents IA construits par une équipe jeune, c'est huit produits superficiels.** Sur la page
  rendue : pub Facebook/Instagram, community management, facturation/devis/contrats, création de
  site web, workflows, templates WhatsApp, orchestration — **et un seul agent vendeur**. La vente
  conversationnelle n'a droit qu'à un huitième de l'attention de l'équipe.
- **Fiitsa Studio est de la prestation humaine facturée en crédits** (« montée par nos soins à
  partir de tes rushs », 200 crédits = 20 000 FCFA par vidéo). Ce n'est pas du SaaS, c'est une
  agence déguisée. Une entreprise qui vend du montage vidéo n'itère pas vite sur un moteur de prise
  de commande.
- **L'asymétrie du risque n'est pas la même selon la fonction.** Un mauvais post de community
  management ne coûte rien. Un agent qui rate une commande à 40 000 FCFA fait perdre une vente
  réelle et la confiance du commerçant. **La fiabilité compte de façon disproportionnée sur la
  brique argent** — c'est là qu'un spécialiste peut gagner sans être « meilleur partout ».
- **Les signaux de maturité sont mauvais** : 5 % vs 7 % de commission contradictoires sur son
  propre site, plan Agence gratuit avec white label qui cannibalise Premium à 49 990, chiffres
  d'adoption incohérents (500 sur la page tarifs vs 3 000–4 000 ailleurs), promesse intenable
  « 0 risque de blocage par Meta ». **Ce n'est pas une forteresse.**
- **La grille est trouée au milieu.** Fiitsa propose gratuit-avec-5 %, ou 49 990 FCFA. Il n'y a
  **rien entre 0 et 49 990** — et le cœur du marché local est à 9 900–20 000. C'est un trou béant,
  et c'est la meilleure nouvelle du rapport local.

### Verdict sur la question posée

**La dispersion de Fiitsa est une faiblesse exploitable sur une seule dimension : la profondeur de
l'agent vendeur.** Elle n'est *pas* exploitable comme argument marketing — « nous ne faisons qu'une
chose » ne convainc pas un commerçant qui compte ses abonnements. Le pitch « outil focalisé » est
un argument d'ingénieur ; le marché local répond au contraire par le tout-en-un.

Et il faut ajouter deux choses inconfortables :

1. **La focalisation n'est pas un fossé défensif.** Fiitsa peut approfondir son agent vendeur en un
   trimestre. ContexFly ne peut pas ajouter sept agents en un trimestre. La focalisation achète du
   **temps**, pas de la **défense**.
2. **Le différenciateur principal identifié dans `Idee.md` — la fidélisation pilotée par la donnée
   d'achat — n'est pas neuf mondialement.** Flowcart l'a déjà (paliers, VIP, winback, agent de
   winback), Chatarmin partiellement. Il est neuf **localement** : ni Fiitsa (non vérifié sur ce
   point), ni Ayweu, ni Genuka, ni Waazi, ni ReplyPro ne l'ont. **La différenciation de ContexFly
   est géographique, pas fonctionnelle. Il faut l'assumer plutôt que de se raconter l'inverse.**

### La question qui décide, et elle n'est toujours pas tranchée

`_verifications-felix.md` le dit et je le confirme : **on ne sait pas si l'agent vendeur de Fiitsa
négocie une commande en langage naturel ou envoie un catalogue et un formulaire WhatsApp Flows.**
La ligne « Formulaires WhatsApp — achats, réservations » penche vers le formulaire, mais ce n'est
pas une preuve.

**Cette réponse décide de l'existence de l'espace produit :**
- Si Fiitsa fait du **formulaire** → il reste un espace réel, et il est large : personne en Afrique
  francophone ne fait de la prise de commande conversationnelle autonome.
- Si Fiitsa fait de la **vraie conversation** → l'espace de ContexFly se réduit au prix (le trou
  entre 0 et 49 990) et à la qualité d'exécution. C'est encore un espace, mais c'est un espace
  d'exécution, pas de produit — et il faut le dire à Maxime dans ces termes.

→ **Ouvrir un compte Fiitsa Découverte (gratuit) et passer une commande de bout en bout.** C'est
un test de 45 minutes qui vaut plus que tout ce rapport.

---

# PARTIE 3 — Ce qu'il ne faut pas perdre

Cette partie est indépendante des verdicts. Un acteur classé non-concurrent reste une source.

## 3.1 Les standards implicites — leur absence sera perçue comme un défaut

**Standards mondiaux** (présents chez la quasi-totalité du panel) :

| # | Standard | Preuve |
|---|---|---|
| 1 | **API officielle Meta + statut de partenaire affiché** | 10/10. C'est un gage de crédibilité, pas un différenciant. ContexFly l'a déjà acté. |
| 2 | **Inbox partagée multi-agents avec assignation** | Universelle mondialement, **et vendue seule à 25 000 FCFA/agent localement (Waazi)**. Prérequis, pas argument. |
| 3 | **Frais Meta répercutés, facturés séparément de l'abonnement** | **10/10. Aucun produit du panel n'inclut le coût des messages Meta dans son prix.** Toute autre structure sera perçue comme opaque. |
| 4 | **Campagnes/diffusions avec templates approuvés Meta** | Universel. |
| 5 | **Relance de panier abandonné** | Interakt, Flowcart, Wassist, Chatarmin, charles. Standard commerce — son absence se verra. |
| 6 | **Intégration Click-to-WhatsApp Ads (CTWA)** | Quasi systématique, et cohérent avec la fenêtre gratuite de 72 h de Meta. **⚠️ Absent du scope IN de `Idee.md` — c'est un manque à signaler : c'est le canal d'acquisition standard du secteur et il est économiquement gratuit côté Meta.** |
| 7 | **Analytics avec attribution du revenu** | Chatarmin, Interakt, Zoko. Le commerçant attendra « combien l'agent m'a fait gagner ». |
| 8 | **Essai gratuit** | **7 jours est la norme mondiale ; 14 jours est la norme locale** (Fiitsa, Genuka WA, NéoBot, Waazi, ReplyPro sans carte). → **ContexFly doit faire 14 jours, pas 7.** |

**Standards locaux — billets d'entrée, aucun n'est un différenciant** : prix en FCFA (jamais
USD/EUR — Whakup est hors marché pour cette seule raison) · abonnement payable par Mobile Money ·
palier gratuit ou ≤ 5 000 FCFA · **recharge prépayée plutôt que prélèvement** (ReplyPro dès 2 000
XAF, Vendeur.ci en crédits — le commerçant recharge comme du crédit téléphonique) · français
d'abord · **support WhatsApp avec un numéro +237 visible** · MTN **et** Orange, jamais un seul ·
**paiement à la livraison pris en charge** (Ayweu le facture 0 %) · mobile-first.

**Deux vides que personne ne remplit — les seules ouvertures « adaptation » réelles** :
- **Le fonctionnement en connexion instable.** Aucun acteur, local ou mondial, ne communique sur un
  mode dégradé ou hors ligne. Le cahier papier, lui, marche toujours.
- **Les langues locales.** Seul NéoBot revendique le pidgin (non vérifié). Le pidgin et le franglais
  sont la langue réelle de beaucoup de conversations commerciales à Douala.

## 3.2 Bonnes pratiques d'ergonomie et de parcours, produit par produit

| Source | Ce qu'il faut prendre | Pourquoi |
|---|---|---|
| **Flowcart** | Le catalogue en **Webview dans WhatsApp** avec variantes, ajout au panier et paiement — « en moins de 90 secondes ». Et leur communication centrée sur le **time-to-value** (« live en 20 minutes », « première campagne sous 48 h ») plutôt que sur les fonctionnalités. | 90 secondes est le repère de vitesse à battre sur le parcours acheteur. Et le time-to-value est la bonne métrique produit interne pour ContexFly, dont le vrai risque est l'onboarding Meta. |
| **Wassist** | **On saisit l'URL de la boutique et l'agent est entraîné tout seul, dans le ton de la marque.** Zéro configuration initiale. | C'est le contournement de l'écran vide. Transposition directe : **importer le catalogue depuis le catalogue WhatsApp Business existant du commerçant** (il l'a déjà, jusqu'à 500 produits avec photos et prix). Le commerçant ne ressaisit rien. |
| **NéoBot** | **Génération du prompt par IA** + base de connaissances par texte et PDF. | Le commerçant ne rédigera jamais un prompt. Il répond à 5 questions, l'IA écrit la personnalité de l'agent. |
| **ReplyPro** | La **simulation de l'agent avant mise en production**. | Le commerçant teste l'agent sans risquer son numéro ni un vrai client. Réduit massivement l'angoisse du « et s'il dit n'importe quoi à mes clients ». |
| **Vendeur.ci** | **Whisper STT + TTS français** — l'agent comprend les notes vocales. | ⚠️ **Standard local naissant que ContexFly ignore aujourd'hui.** Une part importante des conversations commerciales camerounaises passe par la note vocale. Si l'agent ne les comprend pas, la conversation casse là où elle est la plus chaude. À classer au minimum Should, argumentablement Must. |
| **Zoko** | **11 flux essentiels pré-écrits gratuits**, flux personnalisés en option payante à 5,99 $. | Validation directe de la réserve posée dans `Idee.md` : des automatisations **pré-écrites activables en un clic**, jamais un rule builder générique. Un acteur mondial a déjà tranché dans ce sens. |
| **Chatarmin** | Les **pop-ups d'opt-in, widgets et opt-in au checkout** comme composants produit. | Le consentement WhatsApp n'est pas une case juridique, c'est une brique fonctionnelle. Le volet fidélisation de ContexFly en dépend (Meta exige un opt-in explicite et spécifique au canal). |
| **Interakt** | **Checkout bot + panneau de gestion des commandes** comme objets distincts. | Confirme le mur identifié : la commande a une vie **après** la conversation. Le panneau de commandes n'est pas un bonus, c'est la moitié du produit. |
| **Ayweu** | « **Un seul lien à partager partout** » + **0 % de frais sur le paiement à la livraison**. | Reconnaît que le point d'entrée réel est le statut / Instagram / TikTok, pas le SaaS. Et que le COD est une réalité qu'on ne taxe pas. Deux leçons de terrain, pas de théorie. |
| **Genuka WA** | « **Nous ne revendons pas vos conversations** » + facturation au tarif Meta sans marge. | L'argument de confiance est **déjà posé localement**. ContexFly doit au minimum l'égaler, sinon il paraîtra moins net qu'un concurrent camerounais. |
| **Zipchat / Wizybot** | **Garantie satisfait ou remboursé 30 jours** (Zipchat) et **garantie adossée au ROI** (Wizybot). | Sur un marché méfiant envers l'abonnement récurrent, une garantie explicite lève plus de frein qu'une remise. Levier de conversion sous-exploité localement. |
| **Kipps.AI / HelloDuty** (Kenya) | Le **déclenchement d'un STK Push M-Pesa dans la conversation** — le client valide le paiement par une notification opérateur, sans quitter le fil. | Le modèle d'interaction à répliquer avec MTN MoMo / Orange Money via un agrégateur. C'est ce qui remplace la capture d'écran. |
| **Wizybot** | L'**automatisation des réponses aux commentaires sur les réseaux sociaux** comme canal d'acquisition. | Personne d'autre ne le fait. Sur un marché où l'acquisition se joue sur Facebook et TikTok, c'est une piste d'acquisition à coût nul à garder en réserve. |

## 3.3 Erreurs documentées à ne pas répéter

1. **Vendre l'IA en add-on plus cher que la plateforme.** Interakt : 55 $ de plateforme, **74,99 $
   d'add-on IA**. Wati : crédits IA quotés + Astra en add-on non tarifé. Structure qui décourage
   l'usage de la fonctionnalité centrale. → **Chez ContexFly l'IA *est* le produit. Jamais en
   add-on, jamais quotée en « crédits » opaques.**
2. **L'opacité sur la marge appliquée aux frais Meta.** La majorité du panel écrit « frais Meta
   séparés » sans chiffrer. Interakt se trahit en réservant « no markup charges » au palier
   Enterprise. → Voir 3.4 : ContexFly a une réponse structurellement propre à cette question.
3. **Promettre « vendre sur WhatsApp » et s'arrêter au lien vers le checkout de la boutique.**
   Zipchat, Wizybot, Wassist, Zoko. C'est **le fossé discours/réalité du secteur entier**. → Ne
   jamais annoncer « paiement dans WhatsApp » si c'est une page hébergée ouverte en Webview.
   Formuler exactement ce qui se passe : la crédibilité vaut plus que le superlatif, surtout sur
   un marché où la méfiance est le réflexe.
4. **La dépendance structurelle à Shopify.** Zipchat, Wizybot, Zoko, Chatarmin, Wassist et en
   partie Flowcart supposent une boutique préexistante. **Un commerçant sans site web n'est pas
   leur client** — c'est l'angle mort massif du secteur et c'est la population de ContexFly. → Le
   catalogue interne ne doit jamais être un citoyen de seconde zone dans l'architecture.
5. **Cacher les tarifs derrière une démo.** Yalo, charles, Bik, Chatarmin, Gupshup. Sur un marché
   PME, c'est un frein d'acquisition net et une occasion de se différencier par la transparence.
6. **Promettre ce que personne ne peut garantir.** Fiitsa affiche « **0 risque de blocage par
   Meta** ». C'est intenable : le *quality rating* dépend du taux de blocage par les destinataires,
   pas de l'outil d'envoi. → Une promesse invérifiable détruit la confiance au premier incident.
7. **Une grille tarifaire incohérente avec elle-même.** Fiitsa : 5 % sur la page tarifs vs 7 % sur
   l'accueil ; plan Agence **gratuit** avec white label et businesses illimités, qui cannibalise
   Premium à 49 990. → Ne jamais offrir gratuitement le palier qui délivre le plus de valeur ; la
   cohérence de la grille est lue comme un signal de sérieux.
8. **Le canal non officiel (Baileys) comme réponse à un onboarding lent.** Vendeur.ci le propose
   ouvertement. Risque de bannissement du numéro — donc du fonds de commerce du client. → À ne
   jamais imiter, **mais à comprendre** : c'est la réponse à une douleur réelle. Le contournement
   à construire est un **onboarding accéléré sur la voie officielle**, pas un canal parallèle.
9. **La tarification par siège.** Waazi facture 25 000 FCFA **par agent**. Modèle SaaS occidental
   transposé tel quel, inadapté à un commerçant qui est seul ou à deux. → Ne pas facturer au siège.
10. **Bâtir sur WhatsApp Pay natif.** Interakt et AiSensy en font un socle ; il n'existe qu'en
    Inde, Brésil et Singapour. → Confirme le choix de ContexFly (lien de paiement + page hébergée).
11. **Reprendre des chiffres d'adoption de concurrents comme repère.** Fiitsa annonce 500
    entrepreneurs sur une page et 3 000–4 000 ailleurs. → Aucune projection de ContexFly ne doit
    s'appuyer dessus.
12. **Facturer en « conversations » alors que Meta facture au message délivré depuis le
    01/07/2025.** Zoko, Chatarmin et DoubleTick parlent encore en conversations. → Écart de
    modélisation de coût à ne pas hériter.

## 3.4 Modèle économique — quel modèle est le plus défendable pour ContexFly

### Les quatre postures observées

| Posture | Qui | Ce que ça dit |
|---|---|---|
| **Marge affichée sur les frais Meta** | **Zoko** (0,015 $/conversation sur Starter, dégressif jusqu'à 0,00049 $) | Transparence assumée, mais la marge existe |
| **Marge zéro affichée comme argument** | **Chatarmin** (« €0,00 » sur tous les paliers), **Rasayel** (Meta facture le client en direct), **Genuka WA** (« au tarif Meta sans marge ») | Le pass-through est devenu un argument de vente |
| **Marge cachée** | **Interakt** (« no markup » réservé à Enterprise → donc marge ailleurs), et le silence général du panel | Point de friction reconnu du marché |
| **Facturation à la performance** | **Zoko Sello** (3 % de la valeur de commande), **Flowcart** (1,5 %→0,5 % au-delà d'un seuil de CA), **Fiitsa** (5 % sur le plan gratuit), **Ayweu** (2 % sur paiement en ligne, **0 % en COD**) | Le prix suit la valeur produite |

### Sur les frais Meta : la question est déjà tranchée par l'architecture de ContexFly

`Idee.md` acte **Tech Provider + Embedded Signup** : le client possède son WABA et **ajoute son
propre moyen de paiement Meta**. Les messages sont donc facturés au client par Meta, directement.
ContexFly **ne peut pas** appliquer de marge, et **n'a pas** de risque de trésorerie.

→ **La posture Chatarmin/Rasayel/Genuka n'est pas un choix pour ContexFly : c'est un fait. Il faut
l'afficher explicitement, chiffré, sur la page tarifs.** « Tu paies Meta directement, nous ne
touchons pas un franc sur tes messages » est un argument vrai, vérifiable, aligné avec le standard
local le plus crédible (Genuka), et immédiatement opposable à des concurrents qui restent muets.
Ne pas l'écrire serait laisser de la valeur sur la table.

### Sur la commission sur les ventes : à écarter, et pour des raisons factuelles

**Recommandation : abonnement fixe en FCFA, 0 % de commission sur les ventes, revendiqué comme tel
contre les 5 % de Fiitsa.** Quatre raisons, par ordre de solidité :

1. **Une commission est structurellement incollectable sur ce marché.** Le paiement à la livraison
   est massivement pratiqué — **Ayweu le facture 0 % précisément parce qu'il ne voit pas passer
   l'argent**. Une commission sur les ventes ne peut porter que sur les transactions en ligne. Elle
   pousse donc ContexFly à contraindre le commerçant vers le paiement en ligne, contre l'habitude
   de son propre client final. **C'est le modèle qui s'oppose au terrain.**
2. **Elle punit exactement le client qu'on veut garder.** Le brief le dit et c'est vérifiable sur
   les chiffres de Fiitsa : un commerçant à 500 000 FCFA/mois de ventes paie **25 000 FCFA/mois de
   commission** sur le plan gratuit. Le commerçant qui réussit — le seul qui a une raison de rester
   — est celui à qui le modèle donne le plus de raisons de partir. Sélection adverse.
3. **Elle impose d'être dans le flux d'argent.** Réconcilier chaque transaction pour prélever une
   commission suppose une dépendance totale à l'agrégateur, une gestion de litiges et une exposition
   réglementaire. Pour un développeur solo, c'est un coût de complexité disproportionné.
4. **C'est un argument commercial immédiat.** Face à Fiitsa, « chez nous ta commission est de 0 %,
   quel que soit ton chiffre d'affaires » est une phrase qu'un commerçant comprend en trois
   secondes. C'est le seul angle où ContexFly peut être **objectivement moins cher** que le leader
   local dès que le commerçant vend un peu.

**L'objection honnête, et il faut la traiter** : le 5 % de Fiitsa est une arme d'acquisition
redoutable — barrière d'entrée nulle, le commerçant ne paie que s'il vend. Un abonnement fixe
demande de payer avant d'avoir gagné.
→ **La réponse n'est pas la commission, c'est un palier d'entrée gratuit plafonné en volume** (N
conversations IA par mois, N produits), plus **la recharge prépayée** que ReplyPro et Vendeur.ci ont
déjà validée localement. Le commerçant recharge 2 000 FCFA comme du crédit téléphonique. Barrière
d'entrée aussi basse, sans le piège de la commission.

**Ce que Flowcart fait de plus intelligent que Fiitsa, et qui reste transposable** : la commission
**dégressive** et **au-dessus d'un seuil de gratuité** (1,5 % au-delà de 3 000 $ de CA, 0,5 % au
palier haut). Elle n'existe que pour capter le très gros volume. Si un jour ContexFly veut une part
variable, c'est cette forme-là — jamais 5 % dès le premier franc.

### ⚠️ Le risque économique que ni l'un ni l'autre rapport ne pose

Le cœur de marché local est à **9 900 – 20 000 FCFA/mois**. Le seul acteur local qui tarifie
l'agent vendeur à l'unité — Fiitsa — le facture **1 crédit par conversation et par jour, soit 100
FCFA** (vérifié). Son propre simulateur admet qu'à 20 conversations/jour cela donne **60 000
FCFA/mois pour le seul agent IA**, et pousse vers Premium à 49 990.

**Traduction : l'unique acteur qui a mesuré le coût d'un agent IA conversationnel sur ce marché le
tarife à un niveau incompatible avec la bande de prix que le marché accepte.** Un abonnement
ContexFly à 15 000 FCFA/mois avec conversations IA illimitées est un pari contre sa propre
structure de coût.

*(Le coût réel d'inférence par conversation dépend du modèle retenu et du nombre de tours — je ne
l'ai pas calculé ici, ce serait inventer un chiffre. Mais c'est **la** modélisation à faire avant
le skill `tarification`, et elle peut invalider le modèle tarifaire entier.)*
→ À porter dans `Questions-Ouvertes.md`.

---

# PARTIE 4 — Verdict final

## 4.1 Les vrais concurrents, dans l'ordre

1. **L'app WhatsApp Business gratuite + le cahier + la capture d'écran MoMo.** Coût 0 FCFA,
   catalogue de 500 produits et **panier natif confirmé**. C'est contre ça que l'abonnement se
   justifie, pas contre un SaaS. Le mur est net et il est le seul terrain défendable : *elle ne
   vend pas quand le commerçant dort, elle n'encaisse rien, elle ne sait rien de ses clients.*
2. **Ozirus et les agences camerounaises.** Elles vendent aujourd'hui, en français, à Douala et
   Yaoundé, exactement la promesse de ContexFly, avec quelqu'un à appeler et un paiement unique.
   Ce sont elles qui prendront les 50 premiers clients.
3. **Fiitsa.** Le seul produit qui coche les cinq filtres. Attaquable sur trois points concrets : le
   trou entre 0 et 49 990 FCFA, la commission de 5 % qui punit la réussite, et la profondeur
   probable — mais **non vérifiée** — de son agent vendeur.
4. **Ayweu, puis Genuka.** Indirects aujourd'hui, directs le jour où l'un des deux ajoute un agent
   IA. Ils ont ce que ContexFly n'a pas : une base installée camerounaise et une marque locale.
5. **Vendeur.ci**, sur le marché n°2 (Côte d'Ivoire) avant même que ContexFly y arrive.
6. **Flowcart**, à 12–24 mois, et sur le haut du marché seulement.
7. **Tout le reste du panel mondial : non pertinent.** Le traiter comme concurrent fausserait le
   positionnement.

## 4.2 Reste-t-il un espace produit réel ? — réponse sans complaisance

**Oui, mais ce n'est pas l'espace décrit dans `Idee.md`, et il est plus étroit qu'il n'y paraît.**

**Ce qui n'est PAS un espace** — et il faut arrêter de le compter comme tel :
- **Le panier dans WhatsApp.** Meta le donne gratuitement. Confirmé.
- **L'inbox avec bascule IA↔humain.** Waazi la vend seule à 25 000 FCFA/agent au Cameroun.
  Prérequis, pas différenciant.
- **Le mobile money comme fossé technique.** Flowcart intègre déjà Flutterwave, qui collecte MTN
  MoMo et Orange Money au Cameroun en XAF. Le rail existe chez un concurrent.
- **La fidélisation pilotée par la donnée d'achat.** Flowcart l'a déjà (paliers, VIP, winback).
  Neuf localement, banal mondialement.
- **« Un agent IA qui vend sur WhatsApp ».** Des dizaines de produits l'annoncent. `Idee.md` le
  pressentait ; c'est confirmé.

**Ce qui EST un espace, et il est réel** :
1. **Le trou de prix.** Entre 0 et 49 990 FCFA/mois, **aucun produit ne fait la chaîne complète
   catalogue → conversation → panier → encaissement MoMo → commande enregistrée** en français.
   Fiitsa saute par-dessus, Flowcart démarre à 41 000 avec une boutique en prérequis, les acteurs à
   5 000–20 000 FCFA (Ayweu, Genuka, ReplyPro, NéoBot) ne font qu'un morceau de la chaîne. **C'est
   le seul espace franchement documenté par les deux rapports.**
2. **Le commerçant sans site web.** L'angle mort du secteur mondial entier (Shopify en prérequis
   chez 5 acteurs sur 10, y compris Flowcart) et de Flowcart en particulier. C'est la population
   camerounaise majoritaire.
3. **L'exécution sur la brique argent.** Encaisser réellement, réconcilier, gérer le paiement à la
   livraison, remplacer la capture d'écran. Personne localement ne l'a prouvé, et c'est la fonction
   où la fiabilité compte le plus.
4. **Deux vides d'adaptation que personne ne remplit** : le mode dégradé en connexion instable, et
   les notes vocales / le pidgin.

**Les trois vérités inconfortables à retenir :**

- **La différenciation de ContexFly est géographique et tarifaire, pas fonctionnelle.** Aucune de
  ses fonctionnalités n'est inédite au niveau mondial. Ce qui est inédit, c'est l'assemblage à ce
  prix, dans cette langue, sur ce rail de paiement, sans prérequis de boutique. C'est une position
  légitime — Ayweu et Genuka ont bâti dessus — mais elle doit être assumée telle quelle dans
  `positionnement-marketing`, pas maquillée en innovation produit.
- **Aucune de ces barrières n'est technique.** Langue, prix, segment, go-to-market : toutes
  tombent sur décision d'un concurrent mieux financé. La seule barrière durable candidate est
  **opérationnelle** : réussir à onboarder sur l'API officielle Meta et sur un compte de collecte
  MoMo un commerçant qui n'a ni RCCM ni NIU. C'est le vrai actif défendable du projet, et
  `Idee.md` le pressent déjà (Embedded Signup, plafond de 250 destinataires qui n'exige pas la
  vérification d'entreprise). **Ce n'est pas l'agent IA qui protégera ContexFly, c'est
  l'onboarding.**
- **Une question non tranchée peut encore fermer une grande partie de l'espace** : la profondeur
  réelle de l'agent vendeur de Fiitsa.

**Ce n'est pas une partie perdue. C'est une partie qui se joue sur l'exécution, l'onboarding et le
prix — pas sur la nouveauté fonctionnelle. Et il faut le dire à Maxime en ces termes avant le
skill `positionnement-marketing`.**

---

# PARTIE 5 — Ce qui reste non vérifié et qui pèse

Par ordre de conséquence sur les décisions à venir :

1. **La profondeur de l'agent vendeur de Fiitsa** — conversation naturelle ou formulaire WhatsApp
   Flows ? *Décide de la taille de l'espace produit.* → Compte Découverte gratuit + commande de
   bout en bout.
2. **Le coût d'inférence réel d'une conversation IA complète** rapporté à la bande de prix locale
   (9 900–20 000 FCFA/mois). *Peut invalider le modèle tarifaire entier.* → À modéliser avant
   `tarification`.
3. **Les prérequis d'ouverture d'un compte marchand chez un agrégateur MoMo** (CamPay, Notch Pay,
   Lygos, Flutterwave) : RCCM ? NIU ? compte bancaire d'entreprise ? *Décide si l'onboarding
   self-service est possible — donc si la seule barrière défendable du projet existe.* → Contact
   direct. Aucun rapport n'a pu le vérifier.
4. **AgentCraftr** (site 100 % JS) — positionnement affiché exactement dans le segment, avec
   « own catalogue » et « takes orders ». *Seul concurrent mondial potentiel non évalué.*
5. **Ngavix** — module « boutique WhatsApp » revendiqué **à partir de 10 000 FCFA/mois** (source
   secondaire). *Si c'est exact, il est pile dans le trou de prix identifié comme l'espace de
   ContexFly.* → À ouvrir en priorité, avant Flowcart.
6. **Yalo en Afrique** — contradiction non résolue entre sa page d'accueil (« 40+ pays… Afrique »)
   et les sources tierces. Faible impact : segment enterprise.
7. **Le panier WhatsApp Business est-il activé au Cameroun spécifiquement ?** Confirmé comme
   fonctionnalité native ; la disponibilité régionale n'a pas été testée sur un téléphone
   camerounais.
