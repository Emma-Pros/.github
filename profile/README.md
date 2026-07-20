# Emma Pros Engineering

Internal tooling for Emma Transit & Emma Logistics operations.

## Tech Stack

Keep new projects on the shared stack below. Similar projects should look
similar, so code, patterns, and people move between repos with little friction.

**Shared foundation (every repo):**

- **Language:** TypeScript. Strict mode on. No plain JavaScript for new code.
- **Runtime & package manager:** Node (LTS) with npm.
- **Database & Auth:** Supabase (Postgres + Auth). Row Level Security on, with
  no public policies. Access via `@supabase/supabase-js`.
- **Browser automation:** Playwright (Chromium) for any scraping or bot work.
- **Secrets:** Environment variables only. Commit a `.env.example`, never a real `.env`.

**Web apps:**

- **Framework:** Next.js (App Router) with React and TypeScript.
- **Styling:** Tailwind CSS.
- **Icons:** `lucide-react`.
- **Testing:** Vitest.

**Bots, scrapers, and workers:**

- Node + `tsx` for TypeScript execution.
- Schedule with `node-cron` (or the host's scheduler) for recurring jobs.
- Long-running queue work belongs in a dedicated always-on worker, not the web app.

## Deployment

Pick the host by project type, and keep projects of the same type on the same
host. Matching setups mean one runbook, one mental model, and repos that can
talk to each other later.

| Project type | Deploy target | Notes |
|---|---|---|
| **Web app** (Next.js) | Netlify or Vercel | Managed builds and previews. Use `@netlify/plugin-nextjs` on Netlify. |
| **Always-on bot / worker / scraper** | Fly.io | Docker image per app. Best for Playwright and long-running jobs. |
| **Scheduled one-off script** | Fly.io (cron) or GitHub Actions | Use the lightest option that fits. |

**Rules of thumb:**

1. Containerize deployable services with a `Dockerfile`; keep a `docker-compose.yml` for local parity.
2. Every repo documents its own deploy steps in a `DEPLOY.md` or the README.
3. New projects copy the closest existing repo's setup rather than inventing a new one.
4. Store all secrets in the host's environment settings, never in the repo.

## Coding & Committing Best Practices

1. **Small, focused commits.** One logical change per commit; don't mix refactors with features.
2. **Write clear commit messages.** Imperative mood, present tense ("Add tracking export", not "Added"). Explain *why* in the body when it isn't obvious.
3. **Branch off `main`.** Never commit directly to `main`; open a PR for review.
4. **Keep secrets out of git.** No API keys, tokens, or credentials in code. Use environment variables and `.env` (git-ignored).
5. **Pull before you push.** Rebase or merge latest `main` to avoid conflicts.
6. **Review your own diff first.** Run `git diff` before every commit to catch debug logs, stray files, and accidental changes.
7. **Test before you push.** Run the app/tests locally; don't push code you haven't run.
8. **Descriptive names.** Clear variable, function, and file names beat comments explaining unclear ones.
9. **Match the existing style.** Follow the conventions already in each repo (formatting, structure, naming).
10. **Open a PR early.** Draft PRs invite feedback sooner and keep work visible.
