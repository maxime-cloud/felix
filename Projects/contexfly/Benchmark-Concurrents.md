# Benchmark Concurrents — ContexFly

**Date de réalisation : 2026-08-15.** À rafraîchir au-delà de 4 semaines (voir skill
`benchmark-concurrents`) — les tarifs et fonctionnalités cités ici se propagent jusqu'à
`tarification` et `La-Verite-Difficile.md`.

## Documents détaillés (annexes)

| Fichier | Contenu |
|---|---|
| `_benchmark-mondial.md` | 10 fiches mondiales + 12 candidats écartés avec raison |
| `_benchmark-local.md` | Fiches Cameroun / Afrique francophone + concurrents non numériques |
| `_verifications-felix.md` | **Fait foi en cas de contradiction** — vérifications faites au navigateur avec JS |
| `_arbitrage-pertinence.md` | Verdicts acteur par acteur, enseignements, verdict final |

## Fiabilité des sources — à lire avant d'utiliser un chiffre

Les deux sous-agents n'avaient pas de navigateur exécutant le JavaScript : plusieurs grilles
tarifaires rendues côté client n'ont pas pu être lues (Wati, Whautomate, Bik, Manychat en 403) et
sont marquées « non lu » dans les annexes. J'ai repassé moi-même sur les trois points décisifs —
Fiitsa, Flowcart, le panier WhatsApp natif. **Pour un benchmark tarifaire exhaustif, installer le
MCP Playwright** : `claude mcp add playwright npx @playwright/mcp@latest`.

Aucun chiffre de ce dossier n'est une estimation. Ce qui n'a pas été vu est noté « non vérifié ».

---

## 1. Panel mondial

**Établis :** Wati, Interakt (Jio Haptik), AiSensy, Zoko, Yalo.
**Émergents :** Flowcart (ex-Sukhiba), Wassist, Zipchat AI, Wizybot, Chatarmin.
Écartés avec raison : Respond.io, SleekFlow, charles, Rasayel, Periskope, DoubleTick, Gupshup,
Manychat, Bik, Whautomate, AgentCraftr, Uptail.

### Ce que le panel mondial établit

- **Le paiement réellement bouclé dans le fil de conversation est le différenciateur le plus rare
  du secteur** — un seul produit sur dix le décrit clairement (Flowcart). Interakt et AiSensy
  s'appuient sur WhatsApp Pay natif, **limité à l'Inde/UPI**. Zoko, Zipchat, Wizybot, Chatarmin
  renvoient vers le checkout de la boutique.
- **Le secteur suppose que le marchand a déjà une boutique en ligne.** Shopify est un prérequis
  chez 5 acteurs sur 10. **Un commerçant sans site web n'est le client de personne.**
- **Zéro sur dix n'inclut le coût des messages Meta dans son abonnement.**
- **Aucun des dix ne mentionne Orange Money, MTN MoMo, le XAF, le Cameroun ou l'Afrique
  francophone** sur une page ouverte. Passerelles citées : Stripe, PayPal, Razorpay, PayU,
  Cashfree, UPI. Aucun agrégateur africain.
- **Prix :** point de gravité **49–80 $/mois** à l'entrée d'un palier commerce complet ; fourchette
  PME 30–250 $/mois. Modèle dominant : abonnement + frais Meta répercutés + **IA en add-on payant**
  (Interakt facture ses agents IA 74,99 $/mois, plus cher que sa plateforme à 55 $). Essai gratuit
  de 7 jours quasi universel.

### Flowcart — le cas le plus proche (vérifié au navigateur)

Fonctionnellement, c'est ContexFly : checkout en un clic dans WhatsApp, agents IA de vente
entraînés, relance de panier, inbox multi-agents, fidélisation avec winback, recherche
conversationnelle du catalogue. Kényan (ex-Sukhiba, 1,55 M$ seed 2024), SOC 2 Type II, Meta
Business Solution Partner, clients L'Oréal et Masoko/Safaricom.

Paliers **69,99 / 139,99 / 199,99 $ par mois**, plus commission **dégressive au-dessus d'un seuil
de gratuité** : 1,5 % au-delà de 3 000 $ de CA WhatsApp mensuel, 1 % au-delà de 5 000 $, 0,5 %
au-delà de 10 000 $.

**Trois faits l'écartent du terrain de ContexFly aujourd'hui :** son sélecteur de devises propose
USD, INR, KES, NGN, ZAR — **pas de XAF** ; le seul chemin d'inscription en libre-service affiché
sur tout le site est **« Install on Shopify »** ; l'entrée à 69,99 $ ≈ **42 000 FCFA** vise des
marques, pas des commerçants. Mobile money **non vérifié** — aucune page ouverte ne nomme de
moyen de paiement.

→ **Verdict : concurrent à 12–24 mois, sur le haut du marché.** Rien ne l'empêche d'ajouter le
XAF. Il prouve surtout que le produit est faisable et viable.

---

## 2. Panel local — Cameroun & Afrique francophone

**Correction de cadrage assumée : aucun acteur du commerce conversationnel WhatsApp en Afrique
francophone n'est « établi ».** Les plus avancés ont 3-4 ans et revendiquent des chiffres
d'adoption auto-déclarés et contradictoires. Le panel est classé par maturité observable.

### Fiitsa — le seul qui coche tous les filtres (vérifié au navigateur)

Français, FCFA, Mobile Money (Orange Money, MTN, Wave, Moov, Airtel, M-Pesa), 13 pays africains,
API officielle Meta, palier gratuit.

**Mais ce n'est pas un produit focalisé sur la vente : c'est une suite généraliste à 8 agents IA**
— facturation et documents, campagnes Facebook/Instagram Ads, community management, création de
site web et de tunnels, templates WhatsApp, calendriers de rendez-vous, formulaires, CRM, et
**Fiitsa Studio**, une prestation de production vidéo faite par des humains. La vente
conversationnelle est **un** de ces 8 agents.

| Formule | Prix | Commission sur les ventes |
|---|---|---|
| Découverte | Gratuit | **5 %** — 3 produits max, 500 contacts |
| Pay As You Go | Gratuit + crédits | **5 %** |
| Premium | **49 990 FCFA/mois** | 0 % |
| Entreprise | **99 990 FCFA/mois** | 0 % |
| Agence | Gratuit | 0 % — White Label, businesses illimités *(incohérent avec le reste de la grille)* |

Crédit PAYG = 100 FCFA. **Agent vendeur facturé 1 crédit par conversation et par jour.**

**Incohérences relevées** (signal de jeunesse, pas de faiblesse fatale) : « +500 entrepreneurs »
sur la page tarifs contre 3 000-4 000 ailleurs ; calculateur de ROI aux gains inventés sans
source ; revendication **« 0 risque de blocage par Meta »** — intenable, le quality rating dépend
du taux de blocage des destinataires, pas de l'outil d'envoi.

**Non vérifié, et c'est LA question qui décide de la taille de l'espace produit :** la profondeur
réelle de son agent vendeur. La ligne « Formulaires WhatsApp — achats, réservations » suggère un
parcours par **formulaire** plutôt que par conversation naturelle. Ce n'est pas une preuve. Se
tranche avec un compte gratuit et une commande de bout en bout.

### Les autres acteurs locaux

Aucun ne couvre la chaîne complète : **Ayweu** (3 000+ vendeurs revendiqués, SN/CI/CM,
5 000–20 000 FCFA, **2 % sur paiement en ligne mais 0 % en paiement à la livraison**) organise
l'après-conversation via un lien boutique externe ; **Genuka** fait de l'ERP + inbox et affiche
les messages « au tarif Meta sans marge » ; **Waazi** vend du helpdesk seul à 25 000 FCFA/agent ;
**NéoBot**, **ReplyPro** et **Sira** font de la qualification de leads, sans catalogue ni panier
ni paiement. **Ozirus** et les agences camerounaises vendent la même promesse en prestation
(149 000–349 000 FCFA one-shot + 15 000–30 000/mois).

### Deux signaux de terrain sur la barrière d'entrée réelle

- **ReplyPro** (Media System SARL, Douala) affiche son canal WhatsApp **« momentanément
  indisponible — validation en cours »**.
- **Vendeur.ci** propose ouvertement une connexion **« QR Code (Baileys) »**, non officielle et
  contraire aux CGU Meta.

→ **La barrière d'entrée de ce marché est l'accès à l'API officielle, pas la concurrence.**
L'onboarding mérite autant d'attention produit que l'agent IA.

### Fourchette de prix locale

**0 à 20 000 FCFA/mois** pour la cible. Cœur de marché **9 900–25 000**. Au-delà de 25 000, on
quitte le commerçant individuel. **Fiitsa à 49 990 est hors de cette bande** — c'est une ouverture.

---

## 3. Concurrents non numériques — la vraie base de comparaison

**L'app WhatsApp Business gratuite a un catalogue de 500 articles ET un panier natif** (vérifié :
le client ajoute, supprime, modifie les quantités, puis **envoie son panier sous forme de
message** ; activation dans Réglages → Outils professionnels → Catalogue). S'y ajoutent le cahier
papier (0 FCFA, fonctionne sans réseau), le tableur, le statut WhatsApp comme vitrine, et le
**paiement MoMo manuel avec capture d'écran** — gratuit et universellement compris.

⚠️ **Conséquence directe : « le client construit un panier » n'est pas un argument de vente.**

**Le mur exact que l'app gratuite atteint, et c'est le seul terrain défendable :**
- elle **ne vend pas quand le commerçant dort** ;
- elle **n'encaisse rien** (WhatsApp Pay n'existe pas en Afrique) ;
- elle **ne sait rien des clients** (étiquettes manuelles → le ciblage par habitude d'achat est
  impossible) ;
- sa diffusion est un piège silencieux (256 par liste, et les non-contacts sont ignorés sans
  message d'erreur).

**Le panier WhatsApp est un message, pas une commande.** Tout ce qui suit reste manuel :
recalculer, confirmer, réclamer le paiement, vérifier la capture d'écran, noter la commande
quelque part. **L'argument de ContexFly, c'est tout ce qui vient après le panier, sans le
commerçant.**

---

## 4. Verdict de pertinence — les vrais concurrents, dans l'ordre

1. **L'app WhatsApp Business gratuite + le cahier + la capture d'écran MoMo.** C'est contre ça que
   l'abonnement se justifie, pas contre un SaaS.
2. **Ozirus et les agences camerounaises.** Elles vendent aujourd'hui, en français, à Douala et
   Yaoundé, avec quelqu'un à appeler. Ce sont elles qui prendront les 50 premiers clients.
3. **Fiitsa.** Attaquable sur trois points : le trou entre 0 et 49 990 FCFA, la commission de 5 %
   qui punit la réussite, et la profondeur non vérifiée de son agent vendeur.
4. **Ayweu, puis Genuka.** Indirects aujourd'hui, directs le jour où l'un ajoute un agent IA. Ils
   ont ce que ContexFly n'a pas : une base installée camerounaise et une marque locale.
5. **Vendeur.ci**, sur le marché n°2 (Côte d'Ivoire).
6. **Flowcart**, à 12–24 mois, haut de marché.
7. **Tout le reste du panel mondial : non pertinent** — le traiter comme concurrent fausserait le
   positionnement.

---

## 5. Reste-t-il un espace produit ? — sans complaisance

**Oui, mais ce n'est pas celui décrit au départ, et il est plus étroit qu'il n'y paraît.**

### Ce qui n'est PAS un espace — à arrêter de compter comme tel
- **Le panier dans WhatsApp** — Meta le donne gratuitement.
- **L'inbox avec bascule IA↔humain** — Waazi la vend seule à 25 000 FCFA/agent au Cameroun.
  Prérequis, pas différenciateur.
- **Le mobile money comme fossé technique** — le rail existe déjà chez un concurrent.
- **La fidélisation pilotée par la donnée d'achat** — Flowcart l'a déjà (paliers, VIP, winback).
  Neuf localement, banal mondialement.
- **« Un agent IA qui vend sur WhatsApp »** — des dizaines de produits l'annoncent.

### Ce qui EST un espace, et il est réel
1. **Le trou de prix.** Entre 0 et 49 990 FCFA/mois, **aucun produit ne fait la chaîne complète**
   catalogue → conversation → panier → encaissement MoMo → commande enregistrée, en français.
   C'est l'espace le plus franchement documenté par les deux volets.
2. **Le commerçant sans site web.** L'angle mort du secteur mondial entier. C'est la population
   camerounaise majoritaire.
3. **L'exécution sur la brique argent.** Encaisser, réconcilier, gérer le paiement à la livraison,
   remplacer la capture d'écran. Personne localement ne l'a prouvé.
4. **Deux vides d'adaptation que personne ne remplit** : le mode dégradé en connexion instable,
   et les notes vocales / le pidgin.

### Les trois vérités inconfortables
- **La différenciation de ContexFly est géographique et tarifaire, pas fonctionnelle.** Aucune
  fonctionnalité n'est inédite mondialement. Ce qui est inédit, c'est l'assemblage à ce prix, dans
  cette langue, sur ce rail de paiement, sans prérequis de boutique. Position légitime — Ayweu et
  Genuka ont bâti dessus — mais à assumer telle quelle, pas à maquiller en innovation produit.
- **Aucune de ces barrières n'est technique.** Toutes tombent sur décision d'un concurrent mieux
  financé. La seule barrière durable candidate est **opérationnelle** : réussir à onboarder sur
  l'API Meta et sur un compte de collecte MoMo un commerçant sans RCCM ni NIU.
  **Ce n'est pas l'agent IA qui protégera ContexFly, c'est l'onboarding.**
- **Une question non tranchée peut encore fermer une grande partie de l'espace** : la profondeur
  réelle de l'agent vendeur de Fiitsa.

---

## 6. Modèle économique — recommandation issue du benchmark

**Sur les frais Meta : la question est déjà tranchée par l'architecture.** Avec Tech Provider +
Embedded Signup, le client possède son WABA et ajoute son propre moyen de paiement — Meta le
facture directement. ContexFly **ne peut pas** appliquer de marge et **n'a pas** de risque de
trésorerie. → **À afficher explicitement sur la page tarifs** : « tu paies Meta directement, nous
ne touchons pas un franc sur tes messages ». Vrai, vérifiable, aligné sur le standard local le
plus crédible (Genuka), immédiatement opposable à des concurrents muets.

**Sur la commission sur les ventes : à écarter.** Quatre raisons factuelles :
1. **Structurellement incollectable ici** — le paiement à la livraison est massivement pratiqué, et
   Ayweu facture 0 % en COD précisément parce qu'il ne voit pas passer l'argent. Une commission
   pousse à contraindre le commerçant vers le paiement en ligne, contre l'habitude de son client.
2. **Elle punit le client qu'on veut garder** — 25 000 FCFA/mois pour un commerçant à 500 000 FCFA
   de ventes chez Fiitsa. Sélection adverse.
3. **Elle impose d'être dans le flux d'argent** — réconciliation, litiges, exposition
   réglementaire. Disproportionné pour un développeur solo.
4. **C'est un argument commercial immédiat** — « 0 % de commission quel que soit ton chiffre
   d'affaires » se comprend en trois secondes.

**L'objection honnête :** le 5 % de Fiitsa est une arme d'acquisition redoutable (le commerçant ne
paie que s'il vend). **La réponse n'est pas la commission, c'est un palier gratuit plafonné en
volume + la recharge prépayée** que ReplyPro et Vendeur.ci ont déjà validée localement — le
commerçant recharge 2 000 FCFA comme du crédit téléphonique.

Si un jour une part variable est voulue, la forme transposable est celle de Flowcart :
**dégressive et au-dessus d'un seuil de gratuité** — jamais 5 % dès le premier franc.

## ⚠️ Le risque économique que le benchmark met au jour

Le cœur de marché local est à **9 900–20 000 FCFA/mois**. Or le seul acteur local qui tarifie
l'agent vendeur à l'unité — Fiitsa — le facture **100 FCFA par conversation et par jour**, et son
propre simulateur admet qu'à 20 conversations/jour cela fait **60 000 FCFA/mois pour l'agent IA
seul**.

**Traduction : l'unique acteur qui a mesuré le coût d'un agent IA conversationnel sur ce marché le
tarife à un niveau incompatible avec la bande de prix que le marché accepte.** Un abonnement
ContexFly à 15 000 FCFA/mois avec conversations illimitées est un pari contre sa propre structure
de coût. **Modélisation du coût d'inférence à faire avant le skill `tarification`** — elle peut
invalider le modèle tarifaire entier.

---

## 7. Ce qui reste non vérifié et qui pèse

Par ordre de conséquence :

1. **La profondeur de l'agent vendeur de Fiitsa** — conversation naturelle ou formulaire ?
   *Décide de la taille de l'espace produit.* → compte gratuit + commande de bout en bout.
2. **Le coût d'inférence réel d'une conversation complète** rapporté à la bande 9 900–20 000 FCFA.
   *Peut invalider le modèle tarifaire.*
3. **Les prérequis d'ouverture d'un compte marchand chez un agrégateur MoMo** (RCCM ? NIU ? compte
   bancaire d'entreprise ?). *Décide si l'onboarding self-service est possible — donc si la seule
   barrière défendable existe.* → contact direct, aucun rapport n'a pu le vérifier.
4. **AgentCraftr** (site 100 % JS) — positionnement affiché exactement dans le segment. Seul
   concurrent mondial potentiel non évalué.
5. **Ngavix** — module « boutique WhatsApp » revendiqué **à partir de 10 000 FCFA/mois** (source
   secondaire). Si c'est exact, il est pile dans le trou de prix identifié comme l'espace de
   ContexFly. **À ouvrir en priorité, avant Flowcart.**
6. **Yalo en Afrique** — contradiction non résolue. Faible impact, segment enterprise.
7. **Disponibilité du panier WhatsApp au Cameroun** — fonctionnalité native confirmée, mais la
   disponibilité régionale n'a pas été testée sur un téléphone camerounais.
