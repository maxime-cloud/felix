# Checklist SaaS-Essentiels — Les Angles Morts Classiques

Objectif : dérouler cette liste pour CHAQUE projet, catégorie par catégorie. Pour chaque item,
trois issues possibles, à consigner dans `Exigences-Non-Fonctionnelles.md` :
- **Applicable, détaillé** — on précise comment ça s'applique à ce projet précis.
- **Écarté, justifié** — explicitement hors scope avec une raison ("pas de paiement en ligne
  dans le MVP, facturation gérée manuellement par le salon").
- **À trancher** — part dans `Questions-Ouvertes.md`.

Ne jamais cocher un item sans une des trois issues ci-dessus. "On verra plus tard" n'est pas une
issue valable pour un item Must-adjacent (sécurité, rôles, paiement).

## 1. Identité, comptes et rôles
- Qui peut créer un compte ? Auto-inscription, ou uniquement invité par un admin ?
- Combien de niveaux de rôles (propriétaire, admin, employé, client final...) ?
- Un utilisateur peut-il appartenir à plusieurs organisations/boutiques à la fois ?
- Récupération de mot de passe, changement d'email, suppression de compte.

## 2. Multi-tenant / structure des données par organisation
- Chaque client du SaaS (entreprise/boutique) est-il totalement cloisonné des autres ?
- Un même utilisateur peut-il gérer plusieurs établissements (ex: chaîne de salons) ?
- Limites par plan (nombre d'utilisateurs, de boutiques, de transactions...).

## 3. Facturation et modèle de revenus
- Le SaaS lui-même est-il payant (abonnement à Maxime) ou gratuit pour l'instant ?
- Si payant : paliers, essai gratuit, mode de paiement adapté au marché (mobile money type
  Orange Money / MTN MoMo plus pertinent que carte bancaire selon la cible).
- Le SaaS gère-t-il lui-même de l'argent pour son utilisateur final (ex: encaissement client) ?
  Si oui, c'est un sujet Must — sécurité et traçabilité renforcées.

## 4. Notifications et communications
- Quels événements déclenchent une notification (rappel de rendez-vous, stock bas, facture
  échue...) ? Par quel canal — SMS, email, WhatsApp, notification in-app ? (Le SMS/WhatsApp est
  souvent plus fiable qu'un email pour une PME locale.)
- L'utilisateur peut-il configurer ce qu'il reçoit ?

## 5. Onboarding et prise en main
- Que voit un nouvel utilisateur à la toute première connexion (écran vide, données de démo,
  assistant guidé) ?
- Y a-t-il un import de données existantes (ex: liste clients déjà tenue sur Excel/cahier) ?

## 6. Recherche, filtres et volumétrie
- Dès que le nombre d'enregistrements dépasse quelques dizaines, comment on cherche/filtre/trie ?
- Pagination, exports (CSV/Excel/PDF) des listes et rapports.

## 7. Historique, audit et traçabilité
- Pour les actions sensibles (suppression, modification de prix, encaissement), garde-t-on un
  historique de qui a fait quoi et quand ?
- Peut-on annuler/restaurer une suppression accidentelle ?

## 8. Sécurité et confidentialité des données
- Authentification : mot de passe simple suffit-il, ou faut-il envisager un 2FA pour les comptes
  admin ?
- Chiffrement des données sensibles (paiement, informations clients).
- Conformité aux règles locales de protection des données si applicable.
- Qui peut voir quoi selon son rôle (cf. section 1) — vérifier qu'aucune donnée sensible n'est
  visible par un rôle qui n'en a pas besoin.

## 9. Disponibilité, performance et connectivité
- Le produit doit-il fonctionner en mode dégradé si la connexion internet coupe (fréquent selon
  le contexte camerounais) ? Sauvegarde locale temporaire, synchronisation différée ?
- Volumétrie attendue réaliste (nombre d'utilisateurs simultanés, de transactions/jour) — pas
  besoin de sur-architecturer un MVP pour un usage qui n'existera pas avant longtemps.

## 10. Interface admin / back-office
- Au-delà de l'usage client final, Maxime (ou l'opérateur du SaaS) a-t-il besoin d'un espace pour
  gérer les comptes, voir l'usage global, intervenir en support ?

## 11. Intégrations externes
- Le produit doit-il se connecter à un outil existant chez le client (comptabilité, WhatsApp
  Business, un ERP, un service de paiement) ? Lister les intégrations Must vs Could.
- Le produit doit-il exposer une API pour d'autres usages futurs ?

## 12. Internationalisation / langue
- Une seule langue (français) suffit-elle, ou faut-il prévoir l'anglais dès le départ (marché
  camerounais bilingue, extension régionale possible) ?
- Formats locaux : devise (FCFA), format de date, fuseau horaire.

## 13. États d'interface à ne pas oublier
- Écran vide (aucune donnée encore) — que voit-on, que propose-t-on de faire ?
- Écran de chargement, écran d'erreur (perte de connexion, action refusée).
- Confirmation avant action destructive (suppression, annulation).

## 14. Support et aide
- Comment un utilisateur bloqué obtient-il de l'aide (FAQ intégrée, contact direct, chat) ?

## 15. Légal et conformité
- CGU/CGV, politique de confidentialité — même minimales, à prévoir si le SaaS collecte des
  données clients de tiers (ex: un salon qui stocke les coordonnées de ses clients).

## 16. Sauvegarde et continuité
- À quelle fréquence les données sont-elles sauvegardées ? Qui peut restaurer en cas de
  problème ? (Sujet souvent oublié dans un MVP mais critique dès qu'un client réel dépend du
  produit pour gérer son activité quotidienne.)

## 17. Cycle de vie et suppression de données
- Que se passe-t-il quand un client de Maxime arrête son abonnement — export de ses données,
  suppression après délai, conservation légale minimale ?
