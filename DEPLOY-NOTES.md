# Deploy notes (polarbearlin fork)

- Cloudflare Worker: `folia-major` (account id `652443a2dd213c9a637144902b50a5ee`), custom domain `music.topsiai.com`, `preview_urls: false`.
- Durable Object: binding `QQ_QR_CHANNEL` -> class `QqQrChannel` (migration v1, sqlite).
- Secrets: `QQ_SESSION_SECRET` is a Worker secret only (`npx wrangler secret put QQ_SESSION_SECRET`). Never commit it.
- Frontend env (`.env.production`, public values):
  - `VITE_QQ_API_BASE=/api/qq` (served by the Worker)
  - `VITE_NETEASE_API_BASE=https://folia-netease-api-lppppoi.vercel.app` (Vercel project, ENABLE_RANDOM_CN_IP on)
  - `VITE_KUGOU_API_BASE=https://folia-kugou-api-lppppoi.vercel.app` (Vercel project, needs QR login)
  - `VITE_SKIP_STARTUP_EXPERIENCE=true` (fork-only: skip the first-launch onboarding sequence for public visitors)
  - `VITE_DEFAULT_LANGUAGE=zh-CN` (fork-only: visitors who never picked a language see Chinese instead of following the browser)
  - `VITE_LIBRARY_INITIAL_SUITE=grid` (home starts on the classic grid with a search box, not the empty Bravais wall)
  - `VITE_DEFAULT_VISUALIZER_MODE=lumiere`, `VITE_DEFAULT_VISUALIZER_BACKGROUND_MODE=common` (fork-only: default lyric style 绘光 + 通用 background)
- Deploy: `npm run build && CLOUDFLARE_ACCOUNT_ID=652443a2dd213c9a637144902b50a5ee npx wrangler deploy`
