# Deploy notes (polarbearlin fork)

- Cloudflare Worker: `folia-major` (account id `652443a2dd213c9a637144902b50a5ee`), custom domain `music.topsiai.com`, `preview_urls: false`.
- Durable Object: binding `QQ_QR_CHANNEL` -> class `QqQrChannel` (migration v1, sqlite).
- Secrets: `QQ_SESSION_SECRET` is a Worker secret only (`npx wrangler secret put QQ_SESSION_SECRET`). Never commit it.
- Frontend env (`.env.production`, public values):
  - `VITE_QQ_API_BASE=/api/qq` (served by the Worker)
  - `VITE_NETEASE_API_BASE=https://folia-netease-api-lppppoi.vercel.app` (Vercel project, ENABLE_RANDOM_CN_IP on)
  - `VITE_KUGOU_API_BASE=https://folia-kugou-api-lppppoi.vercel.app` (Vercel project, needs QR login)
  - `VITE_SKIP_STARTUP_EXPERIENCE=true` (fork-only: skip the first-launch onboarding sequence for public visitors)
- Deploy: `npm run build && CLOUDFLARE_ACCOUNT_ID=652443a2dd213c9a637144902b50a5ee npx wrangler deploy`
