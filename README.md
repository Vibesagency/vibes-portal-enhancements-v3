# vibes-portal-enhancements-v3

This is the "Vibes Quotation Cycles" plugin, live at
`team.vibesagency.co/wp-content/plugins/vibes-portal-enhancements-v3`. It
handles long-term (monthly/annual) quotation contracts, Google Drive
quotation reference links, and the admin-only visibility rules for sales
records in the Vibes Team Portal.

**`vibes-portal-enhancements.php`** is the active plugin file. It intercepts
`POST /vibes/v1/quotations` (via a `rest_pre_dispatch` filter, ahead of
`vibes-team-portal`'s own handler for the same route) and is the file that
actually creates quotations on this site.

**`vibes-quotation-cycles.php`** is a retired, intentionally-empty stub —
an older duplicate of the same logic, kept only so WordPress doesn't show a
"file missing" error and so nothing can accidentally reactivate it.

## Why this is a separate repo

`team.vibesagency.co`'s Hostinger hosting only supports one native Git
auto-deploy connection per site, and that one is already used by the
`vibes-team-portal` plugin. This repo deploys itself independently via a
GitHub Actions workflow over SFTP instead (see
`.github/workflows/deploy.yml`) — push to `main` and it ships automatically,
the same as `vibes-team-portal`'s native Hostinger deploy.

## Setup (one-time)

Add these repository secrets (Settings → Secrets and variables → Actions):

| Secret | Value |
|---|---|
| `SFTP_HOST` | `92.113.18.157` (hPanel → Advanced → SSH Access, or FTP Accounts) |
| `SFTP_PORT` | `22` for SSH/SFTP, or `21` if deploying over plain FTP instead |
| `SFTP_USERNAME` | the FTP/SSH account username |
| `SFTP_PASSWORD` | its password |

The deploy step only uploads the files in this repo to this plugin's own
folder — it never deletes anything and never touches any other folder on
the server.
