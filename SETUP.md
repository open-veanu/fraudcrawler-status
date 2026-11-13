# status.fraudcrawler.veanu.ch setup

## One-time setup

1. **Create the repo from the template.** Open https://github.com/upptime/upptime, click
   "Use this template", set owner `open-veanu` and name `fraudcrawler-status`, make it
   **Public**, and check "Include all branches".
2. **Replace `.upptimerc.yml`** with the one in this folder and commit it to `master`.
3. **Create a PAT for Upptime.** Use a fine-grained token scoped to `open-veanu/fraudcrawler-status`
   with read/write access to Actions, Contents, Issues and Workflows.
4. **Add the repo secrets** under Settings > Secrets and variables > Actions:
   | Secret | Value |
   |---|---|
   | `GH_PAT` | the token from step 3 |
   | `SUPABASE_PROD_ANON_KEY` | prod anon key (from `src/utils/serverConfig.ts`) |
   | `SUPABASE_TEST_ANON_KEY` | dev/test anon key (from `src/utils/serverConfig.ts`) |
5. **Run the workflows.** In the Actions tab, enable workflows, then run "Setup CI" and,
   once it finishes, "Static Site CI".
6. **Turn on GitHub Pages.** Under Settings > Pages, set the source to the `gh-pages` branch
   and the custom domain to `status.fraudcrawler.veanu.ch`. Tick "Enforce HTTPS" once the
   certificate is ready.
7. **Add the DNS record** at the veanu.ch DNS provider (it's managed outside Vercel):
   `status.fraudcrawler  CNAME  open-veanu.github.io.`

## Day-to-day

- **Outages** are detected automatically. Upptime opens an issue with the `status` label
  and closes it when the service recovers. Comment on that issue to post updates; the
  comments appear on the status page.
- **Manual incident** (e.g. degraded crawl quality, which uptime checks can't see): open an
  issue, add the `status` label plus the slug label of the affected service (e.g.
  `prod-backend`), and write updates as comments. Close it to resolve.
- **Planned maintenance**: open an issue with the `maintenance` label and this body:

  ```
  <!--
  start: 2026-11-20T18:00:00.000Z
  end: 2026-11-20T19:00:00.000Z
  expectedDown: prod-backend, prod-web
  -->
  Short description shown on the status page.
  ```

  During that window, the services listed under `expectedDown` won't trigger downtime issues.

## Service slugs

`prod-web`, `prod-backend`, `prod-supabase`, `test-web`, `test-backend`, `test-supabase`,
`upstream-vercel`, `upstream-supabase`, `upstream-flyio`
