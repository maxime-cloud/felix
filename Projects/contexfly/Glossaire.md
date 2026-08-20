# Glossaire — ContexFly

**Destiné à l'agent de codage.** Un concept = un nom, partout : schéma, routes, code, interface.

---

## Entités

| Terme retenu | Nom technique | Définition | À ne PAS utiliser |
|---|---|---|---|
| **Activité** | `organization` | Un commerce. **= une organisation du socle** (décision option A). Porte son agent, son catalogue, son numéro WhatsApp, son WABA, son sous-compte Notch Pay, son abonnement et son KYC. **Unité d'isolation des données.** | business, boutique, entreprise, shop, tenant |
| **Compte utilisateur** | `user` (Better Auth) | Une personne. Peut être membre de plusieurs activités. **N'est pas un conteneur d'activités.** | compte, workspace |
| **Point de vente** | `outlet` | Emplacement physique d'une activité. Porte du stock et des horaires. | boutique, magasin, store, succursale |
| **Propriétaire** | `owner` | **Un seul par activité.** Personne physique vérifiée au KYC, titulaire du WABA et de l'abonnement. | gérant, patron |
| **Gérant** | `manager` | Tout sauf facturation, archivage et transfert de propriété. ⚠️ Le socle nomme ce rôle `admin` — ContexFly le renomme. | owner, admin, patron |
| **Vendeur** | `member` | Employé rattaché à **une activité**. Inbox et commandes, pas les revenus. | agent (réservé à l'IA), opérateur |
| **Agent** | `agent` | **L'agent IA.** Un par activité. Jamais un humain. | bot, assistant, chatbot |
| **Client** | `customer` | Le client final du commerçant. N'est **jamais** utilisateur du SaaS. | contact, acheteur, prospect, lead |
| **Conversation** | `conversation` | Fil WhatsApp avec un client. Statut `active` / `completed`. | thread, chat, discussion |
| **Panier** | `cart` | Construit dans la conversation. Devient une commande à la validation. | basket |
| **Commande** | `order` | Entité distincte, survit à la conversation. | vente, transaction |
| **Produit** | `product` | Article du catalogue. | article, item |
| **Variante** | `variant` | Déclinaison (pointure, couleur…). **Porte le stock.** | option, déclinaison, SKU |
| **Zone** | `deliveryZone` | Ville + quartier desservi, avec ses frais. | secteur, région |
| **Acompte** | `deposit` | Versement partiel qui confirme la commande. ⚠️ **Le libellé affiché au client est personnalisable par le commerçant** — ne jamais figer le mot « acompte » dans l'interface client. | avance, arrhes |
| **Automatisation** | `automation` | Règle de fidélisation pré-écrite, activable. | workflow, scénario |
| **Segment** | `segment` | Groupe de clients calculé sur l'historique d'achat. | liste, audience |
| **Parrain** | `referrer` | Apporteur d'affaires ContexFly. Extérieur au produit. | affilié, ambassadeur |
| **Abonnement** | `subscription` | L'abonnement du commerçant à ContexFly. | plan, forfait |

## Ne jamais confondre

- **Activité ≠ Point de vente.** Une activité peut avoir plusieurs points de vente. L'isolation des
  données se fait à l'**activité**, jamais au point de vente.
- **Agent ≠ Vendeur.** `agent` désigne toujours l'IA, `staff` toujours un humain. Ne jamais parler
  d'« agent » pour un employé, y compris dans l'interface.
- **Client ≠ Utilisateur.** Le `customer` est le client du commerçant, il n'a **jamais** de compte
  ContexFly. L'`owner` et le `staff` sont les seuls utilisateurs.
- **Commande ≠ Conversation.** Une conversation peut ne produire aucune commande ; une commande
  survit à sa conversation.
- **Réduction plateforme ≠ remise commerçant.** `L3` est une réduction sur l'**abonnement
  ContexFly** ; `F2` est une remise accordée par le commerçant à **son** client. Deux entités
  distinctes, à ne jamais fusionner.

## Conventions

- **Identifiants de code, tables, champs, routes : anglais.**
- **Interface : français d'abord**, anglais prévu (bilinguisme FR/EN, cible camerounaise).
- **Commentaires de code : anglais.**
- Casse : `camelCase` pour les champs, `PascalCase` pour les composants — conventions de
  `ai-builder-saas`, à confirmer à `integration-base`.
- Devise : **XAF (FCFA)**. Montants stockés en **entiers** — le franc CFA n'a pas de subdivision
  en usage.
