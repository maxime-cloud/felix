# Référence — ai-builder-saas (le projet de base)

Résumé du socle SaaS réutilisable de Maxime (anciennement nommé SOCLE-SAAS), pour que
`integration-base` sache ce qui existe déjà avant de recommander quoi que ce soit — jamais
recommander un outil ou une fonctionnalité déjà couverte ici sans le signaler comme doublon.

**Si ce résumé date d'avant une évolution du projet de base**, dis-le à Maxime plutôt que de
supposer qu'il est encore à jour — demande-lui de confirmer ou de corriger ce fichier.

## Stack

TanStack Start (Vite, SSR) · Convex (backend, temps réel, cron, stockage) · Better Auth via
`@convex-dev/better-auth` (+ plugin `twoFactor`) · Zod · shadcn/ui (thème préconfiguré) ·
Tailwind CSS · Paraglide JS (i18n FR/EN, FR en langue de référence)

## Déjà couvert par le socle — ne pas re-proposer sans le signaler

- **Multi-tenant strict** : 3 rôles fixes (owner/admin/member), table de permissions centrale
- **2FA** obligatoire owner/admin (plugin Better Auth `twoFactor`)
- **Facturation** : NotchPay exclusivement (carte, Orange Money, MTN MoMo), interface de
  facturation abstraite, toggles global + par abonné, modèle de renouvellement unifié
- **Notifications** : email (Resend via `@convex-dev/resend`), SMS (Africa's Talking), WhatsApp
  avec validation OTP
- **Stockage de fichiers** : natif Convex (`ctx.storage`), pas de service tiers
- **Rate limiting** : `@convex-dev/rate-limiter`
- **Analytics** : PostHog
- **Sécurité automatisée** : Semgrep, `npm audit`, scan OWASP ZAP baseline, audit log
- **Tests** : Vitest + `convex-test`, React Testing Library, Playwright (+ MCP officiel)
- **i18n** : Paraglide JS, FR référence, build qui échoue sur clé manquante

## Ce qui N'EST PAS dans le socle (candidats légitimes pour `Tools.md`)

- Observabilité applicative fine (stack traces, profiling) — PostHog couvre l'essentiel mais pas
  au niveau de Sentry
- Tout outil spécifique au métier d'un projet précis (ex: génération de PDF avancée, OCR,
  reconnaissance d'image) — à évaluer projet par projet
- Tout ce qui dépasse le périmètre générique B2B (fonctionnalités métier spécifiques à un secteur)

## Fichiers clés du projet ai-builder-saas

- `CLAUDE.md` — règles non négociables (stack, sécurité, i18n, tests, discipline de phase)
- `PROMPT.md` — le prompt de génération initial (9 phases)
- `.mcp.json` — MCP shadcn et Playwright préconfigurés

## Mise à jour de ce fichier

Si Maxime fait évoluer ai-builder-saas (nouvel outil ajouté au socle, changement de stack), ce
fichier doit être mis à jour en conséquence — demande-le-lui explicitement si tu soupçonnes qu'il
a changé depuis la dernière fois.
