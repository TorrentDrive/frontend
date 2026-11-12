<picture>
  <source media="(prefers-color-scheme: dark)" srcset=".github/banner-dark.svg">
  <img alt="frontend — torrentdrive by gitnasr" src=".github/banner-light.svg" width="100%">
</picture>

[Documentation](https://tc.gitnasr.com/docs) · [Website](https://tc.gitnasr.com) · [MIT License](LICENSE)

The modern, responsive web application for [TorrentDrive](https://tc.gitnasr.com) — an open-source, self-hosted torrent-to-Google Drive and S3 cloud downloader.

Built with **Next.js 16 App Router**, **Tailwind CSS**, and **Radix UI**, this frontend provides the initial first-run setup wizard, real-time BitTorrent swarm monitoring, selective batch file download pickers, and cloud storage profile management.

> **Just want to run it?** You do not need this repo.
>
> <!-- snippet:install-linux -->
> ```bash
> curl -fsSL https://raw.githubusercontent.com/TorrentDrive/backend/main/install.sh | bash
> ```
> <!-- /snippet -->
>
> Full documentation: **[tc.gitnasr.com/docs](https://tc.gitnasr.com/docs)**

---

## What lives in this repo

```
app/
├── (auth)/          Login and OAuth callback
├── (setup)/         First-run wizard — creates the one admin account
├── (dashboard)/     Torrents, jobs, storage profiles
├── dashboard/       Dashboard shell, files, settings
└── api/auth/        NextAuth route handler
components/  ·  hooks/  ·  lib/  ·  stores/  ·  types/
```

Two architectural principles in this codebase:

- **There are no `NEXT_PUBLIC_*` variables, deliberately.** The browser calls the relative path `/proxy/api`, and the server resolves it to the backend. The API address is never baked into client bundles, so one build works against any backend.
- **Auth is credentials-only.** `auth.config.ts` registers a single `Credentials` provider that posts to the backend. Google is a *storage* provider, connected per-user inside the app — it is not a sign-in method.

---

## Developing

```bash
git clone https://github.com/TorrentDrive/frontend.git
cd frontend
npm ci
cp .env.example .env.local   # optional — see the file, everything has a default
npm run dev
```

The dev server listens on `http://localhost:3000` and expects the API on `http://localhost:47200`. Start the backend first — see [TorrentDrive/backend](https://github.com/TorrentDrive/backend).

Sign-in needs `NEXTAUTH_SECRET`; it is the only value without a fallback. Every configuration key is documented at [tc.gitnasr.com/docs/configuration](https://tc.gitnasr.com/docs/configuration).

```bash
npm run build        # production build (output: standalone)
npx tsc --noEmit     # type check, same gate CI runs
```

---

## Repositories

| Repository | Contents |
|------------|----------|
| [backend](https://github.com/TorrentDrive/backend) | .NET 9 API, workers, all-in-one image, installer, and PaaS blueprints |
| [frontend](https://github.com/TorrentDrive/frontend) | Next.js web app |
| [website](https://github.com/TorrentDrive/website) | Documentation site — the canonical docs live here |

---

## License

MIT — see [LICENSE](https://github.com/TorrentDrive/frontend/blob/main/LICENSE).
