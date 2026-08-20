# Pièges à éviter — ContexFly

**Destiné à l'agent de codage.** Erreurs observées en explorant réellement Fiitsa, Wazzap, Zoko et
Ngavix (15-17 août 2026), ou identifiées pendant l'analyse.

---

## 1. Pièges de conception

| Piège | Observé chez | Pourquoi c'en est un | Ce qu'on fait à la place |
|---|---|---|---|
| **Stock coupé par défaut** dans l'accès aux données de l'agent | Fiitsa | L'agent vend un article épuisé. Sur ce marché, la confiance part la première et ne revient pas | **Stock activé par défaut** ; si un point de vente ne le suit pas, réponse prudente plutôt qu'affirmation (R14) |
| **Écran sans état vide** — page blanche, ni liste, ni bouton, ni message | Fiitsa (« Mes agents IA », « Réductions ») | Sur une cible peu technique, **l'état vide *est* l'activation**. Une page blanche est un abandon | Chaque écran a un état vide qui dit quoi faire et propose l'action |
| **Constructeur de règles générique sans automatisations prêtes** | Fiitsa (2 templates factices, 0 utilisation, 30 min de config estimée) | L'écran vide d'un rule builder reste vide. Le commerçant ne créera jamais sa première règle | **5-6 automatisations pré-écrites activables en un clic** avec 2-3 paramètres (F3). Le constructeur générique vient après, ou jamais |
| **Paywall avant toute valeur** — payer avant même de connecter son numéro | Wazzap (étape 3 sur 5) | Le commerçant paie sans avoir rien vu fonctionner | Compte de démo pré-rempli (H3), et **inscription jamais bloquée sur la connexion Meta** |
| **Agent conversationnel qui perd le fil de ce qu'il collecte** | Wazzap — le nom de l'agent enregistré comme une prestation vendue par le commerçant, puis réutilisé comme telle | **Corrompt les données du client, silencieusement** | Confirmation explicite avant écriture, annulation possible (R15) |
| **Configuration d'agent sans accès à l'historique de commandes** | Fiitsa (aucune case pour ça) | L'agent ne peut pas savoir qu'un client en est à sa 3ᵉ commande — la fidélisation devient impossible à brancher | Accès à l'historique dans les données de l'agent (A5, E3) |
| **Formulaire d'adresse postale à l'occidentale** | — | Signale immédiatement que le produit n'a pas été pensé pour le marché | **Ville + quartier en listes définies par le commerçant + repère libre facultatif** (C4) |

## 2. Pièges techniques

- **Faire fuiter une erreur d'infrastructure jusqu'à l'utilisateur.** Observé chez Fiitsa :
  `Failed to send a request to the Edge Function` affiché tel quel dans l'interface du commerçant,
  deux fois, y compris sur un simple « Bonjour ». Toute erreur technique est traduite en message
  compréhensible.
- **Livrer un testeur d'agent qui ne fonctionne pas.** Même source. Si le commerçant ne peut pas
  vérifier ce que son agent dira à ses clients, il ne l'activera pas. **Le test est un chemin
  critique, pas une fonctionnalité annexe.**
- **Passer l'identifiant d'activité en argument d'outil.** C'est le défaut par lequel un agent
  franchit la frontière entre commerçants par simple injection de prompt (R8).
- **Faire confiance à un montant issu du dialogue.** Tout invariant d'argent est recalculé à
  l'écriture (R1, R2).
- **Envoyer une campagne sans limitation de débit.** Brûle le quota Meta d'un coup et dégrade la
  note de qualité du numéro **du commerçant** (R20).
- **Incohérence de devise dans un même produit.** Observé chez Ngavix : tableau de bord en €,
  boutique en FCFA. Une seule devise : **XAF**.
- **Ne pas afficher l'état de la fenêtre de service 24 h.** Sans cet indicateur, un vendeur ne
  comprend jamais pourquoi son message part ou échoue — il conclut que le produit est cassé (E2).

## 3. Pièges de discours

**À ne jamais présenter comme un argument de vente — ce sont des prérequis, pas des
différenciateurs :**

- **Le panier.** L'app WhatsApp Business a un panier natif et gratuit. Un commerçant informé
  répondra « je l'ai déjà ».
- **L'inbox avec bascule IA↔humain.** Waazi la vend seule à 25 000 FCFA/agent à Douala.
- **Le Mobile Money.** Tous les acteurs locaux l'ont.
- **« Un agent IA qui vend sur WhatsApp ».** Des dizaines de produits l'annoncent.
- **L'API officielle Meta.** Fiitsa et Genuka l'ont déjà.
- **L'acompte.** Repris de Fiitsa — c'est un rattrapage, pas une avance.
- **« Une boutique en ligne ».** Ngavix en vend une à 10 000 FCFA/mois avec catalogue, commandes,
  codes promo et notifications WhatsApp.
- **« 0 % de marge sur tes messages ».** Genuka WA l'affiche déjà mot pour mot.

**Promesse à ne jamais faire :** « 0 risque de blocage par Meta » — revendiquée par Fiitsa, et
intenable : la note de qualité dépend du taux de blocage des destinataires, pas de l'outil d'envoi.
Promettre l'impossible prépare une déception ; **expliquer la règle construit la confiance** (F7).

**Ce qui reste défendable, et donc ce qu'on met en avant :** la **conversation** — un agent qui
répond, qualifie, construit le panier et encaisse **dans le fil WhatsApp**, à un prix de commerçant,
sans prérequis de boutique en ligne.
