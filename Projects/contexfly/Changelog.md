# Changelog — ContexFly

Historique des changements notables à ce qui existait déjà (pas les ajouts initiaux, qui vivent
dans les fichiers eux-mêmes — ici : ce qui a été modifié, retiré, ou reconsidéré après une
nouvelle boucle d'analyse).

## 2026-08-15 — cadrage / benchmark

- **Changement :** Le volet « démarchage commercial et envoi de messages en masse » du brief
  initial est retiré et remplacé par un volet **fidélisation et réengagement d'une base opt-in**.
- **Raison :** Violation de la politique Meta pour le démarchage à froid, bannissement
  algorithmique du numéro du client, et coût du template marketing sans dégressivité.

- **Changement :** Le **panier éditable** cesse d'être traité comme un argument produit.
- **Raison :** Vérifié — le panier est une fonctionnalité native et gratuite de l'app WhatsApp
  Business. L'argument se déplace sur ce qui vient **après** le panier (total validé, encaissement,
  commande enregistrée, relance), qui reste entièrement manuel aujourd'hui.

## 2026-08-15 — après exploration du produit Fiitsa

- **Changement :** Ajout d'une **cinquième politique de paiement, l'acompte** (versement partiel
  qui confirme la commande, solde à la livraison), aux quatre modes retenus au cadrage.
- **Raison :** Mode observé chez Fiitsa et probablement le plus adapté au terrain camerounais —
  il traite le risque du paiement à la livraison sans imposer le prépaiement.

- **⚠️ Changement majeur :** ContexFly **entre dans le flux d'argent** (encaissement puis
  reversement au commerçant), alors que le benchmark recommandait explicitement de rester en
  dehors.
- **Raison :** Décision de Maxime, motivée par le fait que Notch Pay couvre payin et payout, et
  par le constat que Fiitsa a franchi la barrière d'onboarding exactement par ce moyen.
- **Ce que ça invalide dans les conclusions précédentes :** la recommandation « abonnement fixe,
  0 % de commission » du benchmark reposait en partie sur l'argument *« une commission est
  structurellement incollectable car ContexFly ne voit pas passer l'argent »*. **Cet argument
  tombe.** Les trois autres tiennent toujours (la commission punit le client qui réussit, elle
  impose la gestion des litiges, et le 0 % est un argument commercial immédiat contre les 5 % de
  Fiitsa), mais le modèle tarifaire doit être **rouvert** au skill `tarification` plutôt que
  considéré comme acquis.
- **Ce que ça ajoute comme charge :** KYC des commerçants, trésorerie de tiers, litiges et
  remboursements, calendrier de reversement, exposition réglementaire. À traiter en exigences
  non-fonctionnelles et dans le MVP.

- **Changement :** L'agrégateur de paiement retenu passe de **PawaPay à Notch Pay** (offre
  **Notch Pay Sync**), quelques heures après l'arbitrage initial.
- **Raison :** Felix avait tranché pour PawaPay sur le critère « cadre contractuel sous-marchands
  écrit », tout en signalant que son Schedule 2 exigeait des documents de société pour chaque
  sous-marchand — ce qui réintroduisait la barrière RCCM que l'option B devait supprimer (Q21).
  Maxime a apporté l'élément manquant : **Notch Pay pratique le KYC (personne physique) là où
  PawaPay n'accepte que le KYB (entreprise)**, et dispose d'une offre marketplace dédiée,
  Notch Pay Sync. Vérification faite : Sync propose comptes sous-marchands, split payment et
  reversements de masse automatisés. Le critère qui avait fait pencher pour PawaPay est donc
  également satisfait, et le point de blocage disparaît.
- **Ce que ça débloque :** le commerçant informel sans RCCM redevient onboardable, ce qui était la
  raison d'être de l'option B.

## 2026-08-17 — fonctionnalités

- **Changement :** L'orientation de l'inbox (E1) passe de **« bureau d'abord, mobile plus tard »**
  à **« mobile-first, avec un responsive sérieusement travaillé pour ordinateur et tablette »**,
  quelques minutes après la première position.
- **Raison :** Felix avait signalé le coût du choix « bureau d'abord » — Ayweu, le concurrent local
  qui revendique 3 000+ vendeurs, est mobile-only, et une inbox de bureau risquait de n'être jamais
  ouverte par un commerçant qui gère son commerce depuis son téléphone, rendant la bascule IA↔humain
  (A6) théorique. Maxime a repris la position.
- **Conséquence de conception :** les trois panneaux du modèle Zoko ne tiennent pas sur un écran de
  téléphone. Navigation à niveaux, et deux éléments qui ne doivent jamais être à plus d'un geste :
  l'indicateur de fenêtre 24 h (E2) et l'historique de commandes du client. **Web responsive, pas
  application native** — pour ne pas ajouter les stores à un chemin critique déjà contraint par la
  validation Meta.

- **Changement :** La contrainte du plafond de fréquence marketing de Meta, d'abord traitée comme
  une simple gestion d'erreur, devient une fonctionnalité à part entière — **F7, pédagogie des
  règles WhatsApp**.
- **Raison :** Demande de Maxime (« il faut juste expliquer à l'utilisateur »). Posture opposée à
  celle de Fiitsa, qui revendique « 0 risque de blocage par Meta » — affirmation intenable
  puisque la note de qualité dépend du taux de blocage des destinataires, pas de l'outil d'envoi.
  Expliquer la règle réduit le support et fait attribuer les échecs à Meta plutôt qu'à ContexFly.

## 2026-08-19 — aller-retour `architecture-integrations` → `fonctionnalites`

- **Changement :** ajout du **domaine N — 13 fonctionnalités imposées par les contraintes
  externes**, découvertes en vérifiant la documentation officielle de Meta et de Notch Pay.
- **Raison :** aucune n'a été choisie — chacune est imposée par une contrainte vérifiée. Les plus
  structurantes : l'agrégateur de réponse (N4, dû à la limite d'un message toutes les 6 secondes
  vers le même utilisateur), le second routeur de webhooks indexé sur le WABA ID (N1), et la
  surveillance de santé de connexion (N10, `ACCOUNT_OFFBOARDED` au changement de téléphone).

- **Correction :** l'affirmation « séparation des flux par alternate webhook endpoints (URL propre
  par WABA) » écrite dans `Contraintes-Techniques.md` était **partiellement fausse**. Les
  endpoints alternatifs ne couvrent que le **trafic conversationnel** ; les webhooks de template,
  de qualité et de compte arrivent obligatoirement sur l'URL par défaut, sans `phone_number_id`.
  Corrigé, et `Architecture.md` §1.1 annoté en conséquence.

## 2026-08-19 — modèle de données et périmètre

- **⚠️ Changement majeur :** « le nombre d'agents est plafonné par le palier d'abonnement »
  (décision du 17/08, G1) est **annulé**. Avec l'option A, **chaque activité a son propre
  abonnement** ; il n'y a plus de quota d'activités.
- **Raison :** l'option A fait d'une activité une organisation du socle, et `subscriptions` est
  rattaché à l'organisation. Le geste commercial sur le multi-activités passe désormais par un
  **coupon dégressif**, pas par un entitlement.
- **Ce que ça change pour `tarification` :** la grille se construit **par activité**, pas par
  compte avec quota.

- **Changement :** le mode dégradé, **écarté du MVP** le 19/08 au matin, est **retenu** le même
  jour (Q38 → **K1**, PWA installable et consultation hors ligne).
- **Raison :** décision de Maxime. Septième fonctionnalité en effort L du périmètre.

- **Changement :** l'import d'une base clients passe de « à trancher » à **retenu** (Q37 → **B5**).

- **Changement :** le rôle intermédiaire passe de `admin` à **`manager`**. Le rôle `admin` du
  socle est renommé, pas ajouté.
