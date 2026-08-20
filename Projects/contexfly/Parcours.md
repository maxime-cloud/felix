# Parcours utilisateurs — ContexFly

Établi le **2026-08-19**. **Mobile-first**, responsive travaillé pour ordinateur et tablette
(décision E1). Niveau écrans et états — jamais de maquette ni de choix visuel.

Chaque parcours porte ses **états** : chargement, vide, erreur, succès. Sur cette cible, **l'état
vide est le principal levier d'activation** — c'est le constat le plus net de l'exploration
concurrentielle (`Reference-Conception-Agent.md` §1).

---

## 1. ⭐ Onboarding du commerçant — le parcours qui décide de tout

C'est le seul avantage durable du produit. Un commerçant perdu ici ne revient pas.

**Principe directeur, repris de Fiitsa et validé : ne jamais bloquer l'inscription sur la connexion
Meta.** Le commerçant doit pouvoir créer son activité, remplir son catalogue et voir le produit
fonctionner **avant** de brancher son numéro.

### Séquence

| # | Écran | Contenu | États |
|---|---|---|---|
| 1 | **Profil** | Type de commerce, secteur, taille d'équipe, objectif n°1. Chaque question justifie sa présence en une ligne | — |
| 2 | ⭐ **Miroir de valeur** | *« Tu réponds à ~N messages par jour. À M minutes chacun, ça fait X heures par semaine — et Y conversations sans réponse. »* Trois compteurs, aucun prix, aucune demande | — |
| 3 | **Création de l'activité** | Nom, description, secteur → instancie les **modèles de champs B0** | — |
| 4 | **Catalogue** | Premiers produits via B0 (§3) **ou** compte de démonstration pré-rempli | 🔴 **vide = mortalité n°1** |
| 5 | **Politique de paiement** | Les 5 modes, expliqués par leur conséquence pour le client | — |
| 6 | **Zones de livraison** | Villes puis quartiers, frais par zone | vide → « tu n'es livrable nulle part » |
| 7 | **Connexion WhatsApp** | Embedded Signup v4 | voir ci-dessous |
| 8 | **Compte d'encaissement** | KYC Notch Pay hébergé | voir ci-dessous |

### 🔴 Les deux étapes qui échouent vraiment

**Connexion WhatsApp (7).** Le code d'échange Meta a une durée de vie de **30 secondes** :
l'écran doit rester ouvert, afficher une progression, et proposer **« recommencer »** en un geste
— pas renvoyer au début du parcours.
États : *en cours de vérification chez Meta* · *file d'attente* (plafond de 10 nouveaux commerçants
par 7 jours avant App Review — annoncer une **date estimée**, jamais un échec) · *rejeté, avec le
motif Meta traduit* · *moyen de paiement Meta manquant* → **bloquant pour les campagnes, pas pour
la vente**, et il faut le dire ainsi.

**Compte d'encaissement (8).** Pièce d'identité, **selfie**, **justificatif de domicile**. Le
justificatif est la friction réelle sur mobile.
États : *à compléter* · *en cours de vérification* · *rejeté avec motif* · *vérifié mais capacité
`payments` non active* — **cas piège : le compte est « vérifié » sans pouvoir encaisser.** L'agent
ne doit pas proposer de lien de paiement dans cet état.

### Fil conducteur permanent
Une **liste d'avancement visible partout** (H6) : numéro connecté · catalogue rempli · politique de
paiement · compte de collecte · première commande. Chaque case non cochée est un point de fuite.
Fiitsa laisse utiliser son produit sans jamais connecter Meta — c'est exactement le trou à éviter.

---

## 2. ⭐ Le client final commande — le flux cœur

**Le client n'a aucun compte, ne télécharge rien, ne retient aucun mot de passe.** Il vit dans
WhatsApp et ne voit qu'**une** page web.

| # | Étape | Où | Points d'attention |
|---|---|---|---|
| 1 | Il écrit | WhatsApp | — |
| 2 | L'agent répond | WhatsApp | **Un seul message par tour** (N4). Réponses courtes |
| 3 | Il demande une variante | WhatsApp | *« vous l'avez en 42 ? »* — **la question canonique** ; l'agent répond grâce à B0, et dit **dans quel point de vente** si le stock est suivi |
| 4 | Le panier se construit | WhatsApp | Récapitulatif à chaque changement |
| 5 | Adresse | WhatsApp | Ville → quartier (listes du commerçant) → repère libre. **Adresse mémorisée proposée par défaut** au prochain achat |
| 6 | Frais annoncés | WhatsApp | Dès le quartier connu, avant validation |
| 7 | Lien de paiement | WhatsApp | **Bouton CTA**, jamais une URL brute. Libellé ≤ 20 caractères |
| 8 | **Page panier** | Web | Ajuster les quantités, supprimer, voir le total. **Sans inscription** |
| 9 | Paiement | Web + téléphone | Il saisit son numéro, **confirme sur son téléphone** (USSD) |
| 10 | Confirmation | WhatsApp | Automatique à réception du webhook. Template `utility`, gratuit |

### États de la page panier (8) — la page la plus fragile du produit
Elle s'ouvre souvent dans le **navigateur intégré de WhatsApp**, en connexion instable.
- **Chargement** — squelette, jamais une page blanche
- **Panier vide** (tout supprimé) — proposer de revenir à la conversation
- **Lien expiré ou déjà payé** — message clair, pas une erreur technique
- **Produit devenu indisponible entre-temps** — le dire **avant** le paiement, pas après
- **Hors ligne** — conserver la saisie, réessayer, ne jamais perdre le panier
- **Paiement en attente de confirmation** — *« compose le code sur ton téléphone »*, minuterie
  visible, **rafraîchissement automatique**. ⚠️ Le délai d'expiration Notch Pay n'étant pas
  documenté, ne pas coder de temps mort arbitraire
- **Paiement échoué / expiré / annulé** — trois messages **distincts**, et un nouveau lien proposé
  dans la conversation plutôt qu'un échec sec

---

## 3. Enregistrer un produit (B0)

| # | Étape | Détail |
|---|---|---|
| 1 | **Champs génériques** | Nom, prix, photo, catégorie, stock |
| 2 | **Photo → pré-remplissage** | L'agent propose description et prix (MVP) |
| 3 | **« Suivant » → conversation** | L'agent demande les attributs **propres au type de produit** : pointure et couleurs pour une chaussure, contenance pour un cosmétique |
| 4 | **« Autre chose à ajouter ? »** | Le commerçant ajoute librement |
| 5 | **La mémoire apprend** | L'attribut ajouté entre dans le modèle de la catégorie → demandé d'office au produit suivant |
| 6 | **Libellé court** | Proposé par l'agent, corrigeable, ≤ 24 caractères |

**États :** *analyse de la photo* · *l'agent réfléchit* · **confirmation avant écriture** —
🔴 obligatoire (R15) : c'est le bug observé chez Wazzap, où le nom de l'agent a été enregistré comme
un produit · *annuler la dernière réponse* · *reprendre plus tard* (un catalogue se remplit en
plusieurs fois) · **hors ligne** — la saisie ne doit jamais être perdue.

---

## 4. Reprise humaine d'une conversation

Trois régimes : **IA** · **brouillon** (l'agent propose, on valide) · **humain**.

- **Bascule en un geste**, depuis la conversation, sans quitter l'écran.
- **Retour à l'IA automatique** après un délai configurable, avec un rappel visible : *« l'agent
  reprend dans 12 minutes »*.
- ⭐ **L'état de la fenêtre 24 h est affiché en permanence** : *« tu peux répondre librement encore
  6 h »* vs *« hors fenêtre — seul un message pré-approuvé peut partir, et il sera facturé »*.
  Sur mobile, **il ne doit jamais être à plus d'un geste**.
- **Mode brouillon (P1)** : la réponse proposée apparaît en attente ; **valider · corriger ·
  rejeter**, en un tap. C'est la rampe de confiance des premières semaines.
- **Après coup (P2)** : *« tu as répondu toi-même 3 fois sur les délais à Kribi — j'ajoute cette
  réponse à ce que sait ton agent ? »*

**Contrainte mobile assumée :** les trois panneaux du modèle Zoko (liste · fil · fiche client) ne
tiennent pas sur un téléphone. Navigation à niveaux, et deux éléments toujours accessibles en un
geste : **l'état de la fenêtre 24 h** et **l'historique de commandes du client**.

---

## 5. Le commerçant suit son argent

- **Tableau de bord** : encaissé, reste dû, prochain reversement, **net après les 3 % de frais** —
  affiché, jamais absorbé silencieusement (R7bis).
- **Fiche commande** : lignes, statut, **bouton « marquer livrée »** — 🔴 le geste qui solde un
  acompte et clôt un paiement à la livraison, et **le maillon le plus fragile de la chaîne**.
  → **Relance automatique** sur les commandes expédiées depuis trop longtemps.
- **Encaissement en espèces** : bouton « payé en espèces » sur la fiche, sinon le reste dû reste
  faux indéfiniment (R5).
- **Fiche livreur** : partageable **directement sur WhatsApp**, pas un fichier à télécharger.

**États :** *paiement en cours de vérification* (P5w) — visible, pas silencieux · *litige ouvert* ·
*reversement en cours* · *reversement revenu en arrière* (statut `reversed` — le registre doit
pouvoir re-créditer).

---

## 6. Campagne de réengagement

Segment → aperçu du nombre de destinataires → template → envoi.

**États indispensables, et ils sont trois, pas deux :** *envoyé* · **« en cours d'évaluation par
Meta »** (portfolio pacing, latence non spécifiée) · *échec*.
Et le cas `131049` : *« ce client a déjà reçu 2 messages promotionnels aujourd'hui, tous commerces
confondus — on réessaie demain »* — **jamais présenté comme une faute du commerçant** (F7).

⚠️ **Vérifier le statut du template au moment de l'envoi**, pas seulement à sa création : Meta peut
l'avoir mis en pause entre-temps.

---

## 7. Ce qui vaut pour tous les écrans

- **États vides utiles** : dire quoi faire et proposer l'action. Un écran blanc est un abandon —
  c'est le défaut le plus visible chez Fiitsa.
- **Jamais d'erreur technique brute.** `Failed to send a request to the Edge Function` affiché à un
  commerçant, c'est ce qu'il ne faut pas faire.
- **Tolérance à la coupure** : ne jamais perdre une saisie.
- **Français d'abord**, anglais prévu.
- **Montants en FCFA entiers**, jamais de décimales.
