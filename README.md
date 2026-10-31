# aiantas-website-deploy

Builds and deploys https://aiantasalethrikou2014.com, the website of Αίαντας
Αλεθρικού.

The site's source is in a private repository. This one holds only the
workflow, [`.github/workflows/website.yml`](.github/workflows/website.yml),
and it is public so that its GitHub Actions minutes are free and no other
project can use them up (ADR 0026 in the source repository).

Every 15 minutes it checks whether the coach has published a result, or
whether the site's source has changed on `main`, and deploys if either has.
Every morning it rebuilds anyway.

## Deploy now

```bash
gh workflow run website.yml -R NikolasNeofytou/aiantas-website-deploy
```

## Secrets

Settings → Secrets and variables → Actions:

| Secret | What it is |
|---|---|
| `SQUAD_SHEET_DEPLOY_KEY` | The private half of a **read-only** deploy key on the source repository |
| `FIREBASE_SERVICE_ACCOUNT_AIANTAS_CLUB` | A JSON key for the Hosting service account of Firebase project `aiantas-club` |

The workflow writes neither to a log. It never runs for pull requests, so
nobody outside can reach them.

## alive.txt

GitHub switches off a public repository's schedule after 60 days without a
commit. The morning run updates `alive.txt` once a month to keep it on.
