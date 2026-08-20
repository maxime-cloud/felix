# Email à Notch Pay — brouillon à relire, modifier et envoyer

**Rédigé le 2026-08-19.** Fondé sur la vérification documentaire consignée dans
`_contraintes-notchpay.md`. Les questions 1 à 6 sont bloquantes : sans réponse écrite,
l'architecture d'encaissement ne peut pas être figée.

---

**De :** contact@stack-trace.site
*(à vérifier avant envoi : l'alias doit être configuré comme adresse d'envoi dans Gmail →
Paramètres → Comptes → « Envoyer des e-mails en tant que ». Sinon l'envoi partira de l'adresse
principale.)*

**À :** hello@notchpay.co
**Copie :** compliance@notchpay.co

**Objet :** Intégration Notch Pay Sync — questions réglementaires et techniques avant développement

---

Bonjour,

Je développe **ContexFly**, un SaaS camerounais qui permet à des commerçants de vendre sur WhatsApp
via un agent conversationnel. La plateforme encaisserait les paiements des clients finaux **pour le
compte de ses commerçants** puis les leur reverserait — c'est le cas d'usage de votre offre **Sync**.

J'ai lu votre documentation développeur, vos pages Sync, votre contrat marchand et votre contrat
partenaire. Plusieurs points déterminants pour mon architecture n'y figurent pas, et je préfère les
clarifier **avant** d'écrire du code plutôt qu'après.

## A. Questions réglementaires — les plus importantes pour moi

1. Lorsqu'un client final paie via une charge de destination (`application_fee` + `destination`),
   **sur quel compte les fonds atterrissent-ils** ? Sur le compte connecté du commerçant, ou sur le
   solde de la plateforme avant transfert ?
2. **Qui est le titulaire juridique du solde** entre l'encaissement et le reversement ?
3. ContexFly peut-il être **strictement intermédiaire technique, sans jamais détenir les fonds**,
   afin de ne pas relever d'un agrément d'établissement de paiement ou de monnaie électronique
   auprès de la BEAC ? Pouvez-vous me le confirmer par écrit ?
4. Les fonds des comptes connectés sont-ils **cantonnés** sur un compte de règlement dédié ?
5. En cas de défaillance de ContexFly, les commerçants récupèrent-ils leur solde **directement
   auprès de Notch Pay** ?
6. Notch Pay dispose-t-il d'un **agrément en zone CEMAC**, et sous quel régime les comptes connectés
   sont-ils opérés ?

## B. Comptes connectés et onboarding

7. Quelles sont les **pièces exactes** exigées pour un compte connecté **personne physique** — un
   commerçant camerounais sans registre de commerce ? Le **justificatif de domicile** est-il
   obligatoire ?
8. Existe-t-il un **plafond de volume** associé au régime personne physique, et que se passe-t-il au
   dépassement ?
9. Les plafonds indiqués pour le Cameroun (500 000 XAF/jour, 5 000 000 XAF/mois) s'appliquent-ils au
   **portefeuille du client final**, au **commerçant**, ou au **compte plateforme** ?
10. Entre les types **Standard, Express et Custom**, lequel recommandez-vous pour une plateforme qui
    gère l'expérience de bout en bout ? Le type Custom déplace-t-il des obligations KYC vers la
    plateforme ?

## C. Points techniques qui conditionnent l'implémentation

11. Quel est le **délai d'expiration exact** d'un paiement mobile money en attente de confirmation
    du client, et à quel moment le statut `expired` est-il émis ?
12. Quelle est votre **politique de réessai des webhooks** — nombre de tentatives, intervalles,
    durée totale ?
13. La signature webhook inclut-elle un **horodatage** ou une protection anti-rejeu ? Existe-t-il un
    **identifiant d'événement unique** exploitable pour la déduplication ?
14. L'événement de succès en mode Sync est-il `payment.complete` ou `payment.succeeded` ? Vos pages
    indiquent l'un et l'autre.
15. Existe-t-il un mécanisme d'**idempotence** sur `POST /payments` ? Un `reference` déjà utilisé
    renvoie-t-il une erreur plutôt que de créer un second débit ?
16. Le **remboursement mobile money** (MTN MoMo, Orange Money) est-il possible par API au Cameroun,
    en total et en partiel ?
17. Quels sont les **montants minimum et maximum** d'un transfert de reversement ?
18. Les **payouts programmés** Sync (quotidien, hebdomadaire, mensuel) se configurent-ils par API ?
    Quels endpoints ?
19. Le canal `cm.orange` est-il bien en **XAF** ? Votre table de canaux indique XOF pour le Cameroun.
20. Les endpoints `/accounts`, `/sync/*` et `/refunds` sont-ils **stables et supportés** ? Ils sont
    absents de votre spécification OpenAPI.
21. Le **bac à sable couvre-t-il Sync** — création de comptes connectés, splits, payouts ?

## D. Commercial

22. Quelle est la **tarification de Sync** ? Y a-t-il un coût par compte connecté ou par split, en
    plus des 1 % payin et 1 % payout ?
23. Le 1 % est-il **déduit du montant encaissé** ou facturé au compte ?
24. Quelles sont les étapes pour **activer Sync** sur mon compte, et quel délai prévoir ?

Je peux vous présenter le projet en visio si c'est plus simple. Les questions 1 à 6 sont bloquantes
pour moi : tant que je n'ai pas de réponse écrite, je ne peux pas figer l'architecture
d'encaissement.

Merci d'avance,

**Maxime Dongne** — ContexFly

---

## ⚠️ Recommandation de Felix avant envoi

**Envisage de couper en deux envois.** 24 questions dans un premier contact, c'est beaucoup, et le
risque réel est une réponse partielle ou un « on revient vers vous ».

- **Envoi 1** — la section A seule (6 questions réglementaires). C'est la question 1 qui conditionne
  tout le reste, et un email court obtient une réponse précise.
- **Envoi 2** — sections B, C et D, après leur réponse ou en même temps que la prise de contact
  commerciale sur l'activation de Sync.

Si tu gardes l'email complet, garde au moins la phrase finale qui hiérarchise : elle indique où
répondre en priorité.

## Version courte, si tu préfères l'envoi 1 seul

> Bonjour,
>
> Je développe ContexFly, un SaaS camerounais permettant à des commerçants de vendre sur WhatsApp.
> La plateforme encaisserait les paiements des clients finaux pour le compte de ses commerçants puis
> les leur reverserait — le cas d'usage de votre offre Sync.
>
> Avant d'engager le développement, j'ai besoin de clarifier six points que je n'ai pas trouvés dans
> votre documentation, vos pages Sync ni vos contrats :
>
> 1. Sur une charge de destination (`application_fee` + `destination`), sur quel compte les fonds
>    atterrissent-ils — le compte connecté du commerçant, ou le solde de la plateforme ?
> 2. Qui est le titulaire juridique du solde entre l'encaissement et le reversement ?
> 3. ContexFly peut-il être strictement intermédiaire technique, sans jamais détenir les fonds, afin
>    de ne pas relever d'un agrément d'établissement de paiement ou de monnaie électronique auprès
>    de la BEAC ? Pouvez-vous me le confirmer par écrit ?
> 4. Les fonds des comptes connectés sont-ils cantonnés sur un compte de règlement dédié ?
> 5. En cas de défaillance de ContexFly, les commerçants récupèrent-ils leur solde directement
>    auprès de Notch Pay ?
> 6. Notch Pay dispose-t-il d'un agrément en zone CEMAC, et sous quel régime les comptes connectés
>    sont-ils opérés ?
>
> J'ai une vingtaine de questions techniques et commerciales par ailleurs (idempotence, webhooks,
> remboursement mobile money, tarification Sync), que je vous enverrai séparément pour ne pas
> alourdir celle-ci. Je peux aussi vous présenter le projet en visio.
>
> Merci d'avance,
> Maxime Dongne — ContexFly
