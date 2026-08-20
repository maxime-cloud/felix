# Règles métier — ContexFly

**Destiné à l'agent de codage.** Chaque règle est un **invariant testable** : elle doit pouvoir
devenir un test sans reformulation. Se remplit au fil de l'eau.

---

## 1. Argent

**R1 — Le plafond de remise est recalculé côté serveur au moment de l'écriture.**
La valeur proposée par l'agent IA n'est jamais retenue telle quelle : le serveur recalcule le
plafond depuis l'historique réel du client et son palier de fidélité, et **rejette** toute valeur
supérieure.
*Pourquoi :* sinon un client négocie -80 % en conversation. · *Où :* `proposerRemise` ·
*Source :* D5, Q9.

**R2 — Aucun montant issu du dialogue n'est écrit tel quel.**
Total du panier, frais de livraison, montant d'acompte, reste dû : tous recalculés à l'écriture
depuis le catalogue, les zones et la politique de paiement en vigueur.
*Pourquoi :* le dialogue est une intention, pas une source de vérité. · *Source :* D1, C5.

**R3 — ContexFly ne détient jamais les fonds.**
⚠️ **HYPOTHÈSE DE TRAVAIL, PAS UN FAIT VÉRIFIÉ.** La garde des fonds chez Notch Pay n'est
documentée nulle part — vérifié trois fois. Trois indices vont même dans le sens contraire (Q29).
Cette règle est **supposée favorable** et doit être **confirmée par écrit avant mise en
production**. Si elle est fausse, un agrément BEAC devient nécessaire et l'architecture
d'encaissement change de nature.
Les encaissements restent chez l'agrégateur ; ContexFly orchestre et lit. Aucun solde n'est un
portefeuille interne — c'est un miroir.
*Pourquoi :* la détention imposerait un agrément EME / établissement de paiement (BEAC, BCEAO,
CBN). · *Source :* Q23, contrainte §4.3 du document de recherche.

**R4 — Une commande en paiement à la livraison ou avec acompte ne se solde que sur le statut
`livrée`.**
*Pourquoi :* sans cette transition, le reste dû demeure faux indéfiniment. · *Source :* C2, D1.

**R5 — L'encaissement en espèces par le vendeur doit être enregistrable manuellement.**
Sans quoi R4 ne peut jamais se produire pour les commandes non payées en ligne.
*Source :* D1, piste d'approfondissement.

**R6 — Une commission de parrainage se déclenche sur la première commande encaissée du filleul, pas
sur son inscription** ; et elle est reprise (*clawback*) en cas de remboursement ou de résiliation
dans les N premiers mois.
*Pourquoi :* l'inscription ne prouve rien, et la commission récurrente est la cible de fraude
principale des programmes d'affiliation SaaS. · *Source :* L1, L4.

**R7 — Cumul parrainage + code de réduction interdit ou plafonné.**
*Pourquoi :* le total consenti peut dépasser la marge. · *Source :* L3.

**R7bis — Les frais de l'agrégateur sont affichés au commerçant, jamais absorbés silencieusement.**
2 % à l'encaissement + 1 % au reversement = **3 %**. Le montant net attendu est affiché à la
commande et au reversement, et l'origine des 3 % est expliquée dans la documentation de la
plateforme.
*Pourquoi :* sans cet affichage, le commerçant constate un écart entre ce que son client a payé et
ce qu'il reçoit, et l'attribue à ContexFly. · *Source :* décision Maxime du 2026-08-19.

## 2. Isolation et permissions

**R8 — 🔴 L'identifiant d'activité provient du contexte serveur, jamais des arguments d'un outil.**
Aucun outil d'agent n'accepte `activiteId`, `commercantId` ou `clientId` en entrée.
*Pourquoi :* l'interlocuteur est un client final inconnu sur WhatsApp ; une injection de prompt
franchirait sinon la frontière entre commerçants. · *Source :* G1, §3.1 de
`Contraintes-Techniques.md`.

**R9 — Les fonctions appelées par les outils de l'agent sont internes, jamais publiques.**
*Pourquoi :* une fonction publique est appelable depuis le client. · *Source :* idem.

**R10 — Un vendeur est rattaché à une activité, pas au compte**, et n'accède ni aux revenus, ni à
l'abonnement, ni à la configuration de l'agent.
*Source :* G1, G3.

**R26 — Une activité a exactement un `owner`, à tout instant.**
Ni zéro, ni deux. Deux chemins seulement : **transfert** (l'ancien `owner` devient `manager` dans la
même transaction) ou **suppression de l'activité** si l'`owner` part sans successeur. Aucun état
« en attente de reprise ».

**R28 — La suppression d'une activité est refusée tant qu'un mouvement d'argent est en cours.**
Paiement en vol, reste dû, reversement non exécuté, litige ouvert : la suppression est bloquée et
la liste de ce qui bloque est affichée.
*Pourquoi :* supprimer une activité qui doit de l'argent crée un passif sans titulaire.
*Source :* Felix, à la suite de la décision Maxime du 2026-08-19.

**R29 — 🔴 Aucune suppression réelle. Jamais.**
Toute « suppression » demandée par un utilisateur est un **changement de statut** (`deleted`,
`archived`) : la donnée disparaît **pour lui**, reste **visible et réactivable par l'administrateur
ContexFly**, et n'est jamais effacée de la base.
S'applique à : activité, produit, commande, client, conversation, membre, point de vente, zone de
livraison, automatisation, campagne — **et à toute entité future**.
*Pourquoi :* une suppression réelle est irréversible et fait perdre des pièces comptables, la trace
d'un litige, et la possibilité de rattraper une erreur d'un utilisateur. La seule transformation
destructive autorisée est l'**anonymisation** des données personnelles au terme du délai de
rétention (loi camerounaise n°2024/017).
*Source :* décision Maxime du 2026-08-19.

**R30 — Le transfert de propriété d'une activité impose un nouveau KYC.**
Le sous-compte d'encaissement est au nom de l'ancien `owner`. L'encaissement est **suspendu** tant
que le KYC du nouveau `owner` n'est pas validé.
*Pourquoi :* un transfert de propriété est un changement de marchand, pas un changement de rôle.
*Source :* confirmé par Maxime, 2026-08-19.

**R31 — Une perte d'accès subie est notifiée dans l'application ET par e-mail.**
S'applique quand un membre perd son accès du fait d'une décision qui n'est pas la sienne :
archivage d'une activité, retrait d'un membre, changement de rôle vers le bas.
*Source :* décision Maxime du 2026-08-19.
*Source :* décision Maxime du 2026-08-19.

**R14 — Un point de vente peut être déclaré « stock non suivi ».**
L'agent se rabat alors sur une réponse prudente au lieu d'affirmer une disponibilité.
*Pourquoi :* un stock mal tenu rend l'agent moins fiable qu'un agent sans stock. · *Source :* G2.

**R15 — Toute écriture en base issue d'une saisie conversationnelle est confirmée explicitement
avant d'être appliquée, et annulable.**
*Pourquoi :* observé chez Wazzap — le nom de l'agent enregistré comme une prestation vendue par le
commerçant, puis réutilisé comme telle. · *Source :* B0, réserve 4.

**R16 — Chaque appel d'outil est journalisé** (arguments, résultat, durée, coût).
*Pourquoi :* c'est la matière d'I2 (taux d'autonomie), de P2 (apprentissage), et la piste d'audit
en cas de litige. · *Source :* §3.5 de `Contraintes-Techniques.md`.

## 4. Messagerie WhatsApp

**R17 — Aucun message sortant hors fenêtre de service sans template pré-approuvé.**
*Source :* contrainte Meta.

**R18 — Aucune campagne sans preuve d'opt-in conservée (date, source) et sans lien de
désabonnement.**
*Pourquoi :* obligation Meta ; le taux de blocage dégrade la note de qualité jusqu'au bannissement
du numéro **du commerçant**. · *Source :* F5, F5 avant F4.

**R19 — L'échec `131049` n'est pas une erreur du commerçant.**
Il est expliqué en clair, et l'envoi est reprogrammé. *Source :* F7, Q25.

**R20 — Tout envoi sortant passe par la limitation de débit centralisée.**
*Pourquoi :* trois plafonds Meta simultanés ; une campagne non limitée brûle le quota et dégrade la
note de qualité. · *Source :* `@convex-dev/workpool`, §3 de `Contraintes-Techniques.md`.

## 5. Commandes et livraison

**R21 — Une commande est une entité distincte de la conversation** et lui survit.
*Source :* C1.

**R22 — Un quartier absent des zones déclarées par le commerçant rend la commande non livrable**,
et l'agent le dit au lieu d'accepter.
*Source :* C4, C5.

**R23 — Les états d'une commande et leurs transitions sont exactement ceux du diagramme
`Architecture.md` §9.2 — sept états, pas cinq.**
`panier → en attente → confirmée → expédiée → livrée` · `annulée` depuis `en attente`, `confirmée`
ou `expédiée` · `remboursée` depuis `livrée` ou `annulée` si déjà payée.
Aucune autre transition n'est permise.
*Correction du 2026-08-19 :* la version initiale ne listait que cinq états et interdisait donc
`panier` et `remboursée` — elle rendait D7 (remboursement) inapplicable. *Source :* C2, D7.

**R24 — Le stock est indexé par `(produit, variante, point de vente)`.**
*Source :* B2, G2.

**R25 — L'adresse appartient au client, pas à la commande.**
Plusieurs adresses possibles, une par défaut, proposée à la commande suivante. *Source :* C4.


## 6. Rétention

**R32 — Les conversations complétées et leurs messages sont conservés 24 mois**, les médias
ré-hébergés 6 mois, les commandes et le registre d'écritures sans limite (pièces comptables).
Les données personnelles d'un client final sont **anonymisées après 24 mois sans activité**.
*Pourquoi :* loi camerounaise n°2024/017 pour l'anonymisation, coût de stockage pour les médias.
*Source :* tranché par Felix, 2026-08-19.

**R33 — Le contexte lu par l'agent n'est pas la durée de rétention.** L'agent ne reçoit que les
3 à 5 dernières conversations complétées d'un client, jamais 24 mois d'historique.
*Pourquoi :* chaque token d'historique est facturé à chaque tour ; c'est un réglage de coût.
*Source :* idem.
