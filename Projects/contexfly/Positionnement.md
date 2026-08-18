# Positionnement Marketing — ContexFly

(Premier passage par le skill `positionnement-marketing`, avant les fonctionnalités — sera repris
et approfondi par `analyse-approfondie` une fois le produit stabilisé. Ne pas considérer comme
final avant ce second passage.)

Base factuelle : `Benchmark-Concurrents.md` et `_verifications-felix.md` (2026-08-15).

---

## Pourquoi ce produit, maintenant, pour cette cible

### Le pourquoi

**Le canal est déjà acquis — il n'y a rien à évangéliser.** Les commerçants camerounais vendent
déjà sur WhatsApp, tous les jours. ContexFly n'a pas à convaincre qui que ce soit de changer
d'outil ou d'habitude, ce qui élimine le coût d'adoption le plus cher d'un SaaS B2B.

**Ce qui manque n'est ni un canal, ni une vitrine : c'est la fin de la chaîne.** L'app WhatsApp
Business gratuite donne déjà un catalogue de 500 articles et un panier. Mais **le panier est un
message, pas une commande.** Tout ce qui suit reste manuel : recalculer le total, confirmer la
disponibilité, réclamer le paiement, vérifier une capture d'écran de transfert Mobile Money,
noter la commande quelque part, préparer la fiche du livreur, relancer si le client disparaît.

C'est là — et uniquement là — que ContexFly a quelque chose à vendre.

### Pourquoi maintenant

Trois verrous ont sauté récemment. Sans eux, ce produit n'était pas faisable pour un développeur
seul il y a dix-huit mois :

1. **La Coexistence Meta** — un même numéro peut désormais être actif simultanément sur l'app
   WhatsApp Business et sur la Cloud API, avec 6 mois d'historique synchronisé. Le blocage
   d'onboarding numéro un — *« si je passe à l'API je perds mon app et mes conversations »* —
   disparaît. *(Disponibilité au Cameroun à confirmer — Q8.)*
2. **Meta n'exige plus la vérification d'entreprise pour envoyer.** Un nouveau portefeuille
   démarre à 250 destinataires uniques par 24 h, et ce plafond ne compte **pas** les réponses aux
   conversations initiées par le client. Une boutique informelle peut donc démarrer, et sa prise
   de commande n'est jamais plafonnée.
3. **Les agrégateurs Mobile Money proposent des offres marketplace avec KYC de personne
   physique** (Notch Pay Sync). Il devient possible d'encaisser pour le compte d'un commerçant qui
   n'a pas de société.

---

## Problèmes réellement résolus

Inventaire concret. Chacun est observable chez un commerçant qui vend sur WhatsApp aujourd'hui.

**Ventes perdues**
1. Les messages arrivés la nuit, le dimanche ou pendant un pic ne reçoivent pas de réponse.
2. Le plafond humain : on ne peut pas tenir 50 conversations en parallèle sans embaucher.
3. Le panier abandonné : la conversation s'arrête en cours de route et personne ne relance.

**Erreurs et frictions dans la prise de commande**
4. La commande reconstituée de mémoire ou d'une remontée de fil : erreurs de quantité, de
   référence, d'adresse.
5. Le total recalculé à la main à chaque modification du panier.
6. La vente d'un article en rupture, faute de vérifier le stock au moment de la conversation.

**Argent**
7. La capture d'écran de transfert Mobile Money comme preuve de paiement : non vérifiable et
   falsifiable.
8. La réconciliation — savoir qui a payé quoi, et ce qui reste dû.
9. Le risque du paiement à la livraison : client absent ou qui se rétracte, livreur payé pour
   rien. → c'est le problème que règle l'**acompte**.

**Mémoire client**
10. Aucune trace exploitable des clients passés : les étiquettes de l'app WhatsApp Business sont
    manuelles, et il n'existe aucun historique d'achat.
11. Impossible de cibler : la diffusion WhatsApp est plafonnée à 256 contacts par liste et
    **ignore silencieusement** les destinataires qui n'ont pas enregistré le numéro.
12. Impossible de récompenser un bon client au bon moment, faute de savoir qu'il en est à sa
    troisième commande.

**Opérations**
13. La fiche à remettre au livreur, recopiée à la main à chaque commande.
14. La rupture de contexte quand un employé reprend une conversation commencée par un autre.

---

## Différenciation face au benchmark

### Sur le prix

| Repère | Prix observé |
|---|---|
| App WhatsApp Business + cahier | **0 FCFA** |
| Cœur de marché local (Ayweu, Genuka, ReplyPro) | **5 000 – 25 000 FCFA/mois** |
| Waazi (inbox seule) | 25 000 FCFA/agent |
| Agences camerounaises (Ozirus) | 149 000 – 349 000 one-shot + 15 000 – 30 000/mois |
| **Fiitsa** | **49 990 FCFA/mois** (ou gratuit à 5 % de commission) |
| Flowcart | ~42 000 FCFA/mois + Shopify en prérequis |
| Panel mondial | 30 – 250 $/mois |

**Position recommandée : 9 900 – 19 900 FCFA/mois, 0 % de commission.**

⚠️ **Correction du 2026-08-17 — la formulation du trou de prix était trop large.** Vérifié dans le
produit : **Ngavix vend un module « Boutique en ligne » à 10 000 FCFA/mois** avec catalogue,
commandes et statuts, codes promo, encaissement Mobile Money (GeniusPay) et **notifications
WhatsApp automatiques à chaque changement de statut**. À ce prix, un commerçant camerounais a donc
déjà une boutique complète.

Ce que Ngavix **ne fait pas** : la conversation. Pas d'agent, pas de boîte de réception, pas de
panier construit dans le fil WhatsApp — WhatsApp n'y sert que de canal de notification sortante.

→ **La revendication exacte n'est donc pas « la chaîne complète à ce prix », c'est
« la *conversation* à ce prix ».** Ce qui n'existe nulle part entre 0 et 49 990 FCFA, c'est
l'agent qui répond, qualifie, construit le panier et encaisse **dans le fil WhatsApp**. La
boutique, elle, existe déjà à 10 000 FCFA.

Deux arguments de prix opposables immédiatement :
- **« 0 % de commission, quel que soit ton chiffre d'affaires »** — contre les 5 % de Fiitsa, qui
  coûtent 25 000 FCFA/mois à un commerçant faisant 500 000 FCFA de ventes. Le modèle de Fiitsa
  punit exactement le client qui réussit.
- **« Tu paies Meta directement, on ne touche pas un franc sur tes messages »** — vrai par
  construction avec le statut Tech Provider, vérifiable, et opposable à des concurrents qui
  restent muets sur ce point.

⚠️ **Cette position de prix est à la fois le différenciateur principal et le risque principal.**
Fiitsa facture son agent vendeur 100 FCFA par conversation et par jour, et son propre simulateur
donne 60 000 FCFA/mois à 20 conversations/jour. Un abonnement à 15 000 FCFA avec conversations
illimitées est un pari contre sa propre structure de coût tant que le coût d'inférence n'a pas été
modélisé (Q13). **C'est la question qui doit ouvrir le skill `tarification`.**

### Sur les fonctionnalités

**Vraiment différenciant — trois choses, pas plus :**

1. **La chaîne complète sans prérequis de boutique en ligne.** Personne dans la bande de prix
   locale ne va du catalogue à la commande encaissée. Ayweu renvoie vers un lien boutique externe,
   Genuka fait de l'ERP, Waazi du helpdesk, NéoBot et ReplyPro de la qualification de leads.
   Flowcart le fait mais exige Shopify et coûte le double.
2. **La remise de fidélité déclenchée par l'historique d'achat, à l'intérieur de la
   conversation.** Vérifié dans le produit : l'agent de Fiitsa n'a **aucun accès** à l'historique
   de commandes de ses clients — ce n'est pas seulement absent, ce n'est pas branchable sur leur
   architecture. Flowcart le fait, mondialement, mais n'est ni sur ce marché ni dans cette bande
   de prix.
3. **Des automatisations pré-écrites, activables en un clic.** Fiitsa a livré un constructeur de
   règles générique dont l'onglet Templates contient deux entrées factices — dont une nommée
   « Workflow Santé et Business **(copie)** » — à 0 utilisation et 30 minutes de configuration
   estimée. C'est un différenciateur d'**exécution**, pas de fonctionnalité. Mais c'en est un
   réel, et il est peu coûteux à obtenir.

**Alignement sur l'existant — prérequis pour être crédible, à ne JAMAIS vendre comme un atout :**

- **Le panier** — natif et gratuit dans l'app WhatsApp Business. Un commerçant informé répondra
  « je l'ai déjà ».
- **L'inbox avec bascule IA ↔ humain** — Waazi la vend seule à Douala.
- **Le Mobile Money** — tous les acteurs locaux l'ont.
- **« Un agent IA qui vend sur WhatsApp »** — des dizaines de produits l'annoncent.
- **L'API officielle Meta** — Fiitsa et Genuka l'ont déjà.
- **L'acompte** — repris de Fiitsa. C'est un rattrapage, pas une avance.

### Sur la cible

**Le segment négligé, et c'est le terrain le plus défendable : le commerçant sans site web et
sans société formelle.**

- **Angle mort du secteur mondial entier** : Shopify est un prérequis chez 5 acteurs sur 10, dont
  Flowcart. Un commerçant sans site n'est le client de personne.
- **Angle mort tarifaire de Fiitsa** : à 49 990 FCFA/mois pour 20 sections dont il en utilisera
  trois, le commerçant individuel n'est pas leur cible réelle, quoi qu'en dise leur discours.
- **Angle mort administratif** : sans RCCM ni NIU, l'accès à un compte marchand est fermé — sauf
  via un intermédiaire qui encaisse, ce que permet Notch Pay Sync avec son KYC personne physique.

C'est aussi le segment le plus difficile à servir. C'est précisément ce qui le rend défendable.

---

## Honnêteté sur la différenciation

**La différenciation de ContexFly est géographique, tarifaire et d'exécution — pas
fonctionnelle.** Aucune de ses fonctionnalités n'est inédite au niveau mondial. Ce qui est inédit,
c'est l'assemblage : à ce prix, dans cette langue, sur ce rail de paiement, sans prérequis de
boutique. C'est une position légitime — Ayweu et Genuka ont construit dessus — mais elle doit être
assumée telle quelle, jamais maquillée en innovation produit.

**Aucune de ces barrières n'est technique.** Langue, prix, segment, go-to-market : toutes tombent
le jour où un concurrent mieux financé décide de descendre en gamme.

**Ce qui reste défendable dans la durée, par ordre de solidité :**

1. **L'onboarding.** Faire passer un commerçant informel de zéro à première commande encaissée —
   connexion Meta, KYC, catalogue, première vente. C'est opérationnel, ça se gagne à l'usure, et
   ça ne se copie pas par une release. **Ce n'est pas l'agent IA qui protégera ContexFly.**
2. **La donnée de commande accumulée.** Plus le produit tourne, plus la fidélisation devient
   précise, et plus il coûte cher de partir. Effet cumulatif modeste mais réel — et c'est le seul
   avantage qui grandit avec le temps.
3. Rien d'autre.

**Le contre-argument qu'il faut se dire à soi-même :** Fiitsa a déjà franchi la barrière
d'onboarding, en devenant encaisseur. ContexFly ne fera donc pas *mieux* sur ce point — il fera
*pareil*. L'avantage doit venir du **prix et du focus**, pas de l'onboarding seul. Le point 1
ci-dessus protège contre les nouveaux entrants, pas contre Fiitsa.

### Le pari, en une phrase

> Un produit qui fait **une seule chose de bout en bout** — vendre et encaisser sur WhatsApp — à
> un tiers du prix du généraliste local, pour le commerçant que le secteur mondial ignore.

### Les deux façons dont ce positionnement peut s'effondrer

- **Par le haut** : Fiitsa descend à 15 000 FCFA/mois ou lance une offre focalisée. L'avantage
  prix disparaît en une release. Seule parade : que le focus et l'exécution soient visiblement
  supérieurs, pas seulement moins chers.
- **Par le bas** : le coût d'inférence rend l'abonnement à 15 000 FCFA intenable. Le
  positionnement s'effondre sans qu'aucun concurrent n'ait bougé.

Dans les deux cas, **le point de rupture est le prix.** C'est le sujet le plus urgent après les
fonctionnalités.
