# n8n-workflows

**ENGLISH** | [ESPAÑOL](README.es.md)

Backup of the n8n workflows that run criptonautas.co and comunidad.criptonautas.co.
`workflows-backup-github` publishes them here every 12 hours, one file per workflow,
named after it.

## Rules

- Only **active** workflows are published. Drafts and paused ones stay in n8n.
- Names are kebab-case `service-object-action` (`ghost-cover-add`), and each workflow has
  one tag for its service: `ghost`, `discourse` or `ops`. A prefix such as
  `[ON-HOLD]` or `[TO-EDIT]` keeps a workflow out of the backup.
- Webhook paths work as passwords, so the backup publishes them as `redacted`.
- The backup never deletes: a workflow that is switched off or renamed leaves its old
  file here until someone removes it.

## Reusing a workflow

Import its JSON in n8n (Workflows → Import from file), create your own credentials with the
names the nodes reference, and give each webhook a random path of your own. Hostnames such as
`criptonautas-featured-cover:8000` are containers on our network: point them at your services.

## Workflows

| Workflow | Trigger | What it does |
|---|---|---|
| **Blog (Ghost)** | | |
| `ghost-cover-add` | Ghost webhook | Gives a post without a featured image a brand cover from [criptonautas-featured-cover](https://github.com/criptonautas/criptonautas-featured-cover) |
| `ghost-featured-image-send` | Ghost webhook, manual backfill | Runs tagged featured images through [criptonautas-featured-ghost-filter](https://github.com/criptonautas/criptonautas-featured-ghost-filter) |
| `ghost-translate-sync` | Ghost webhook | Keeps en.criptonautas.co in step with each change on criptonautas.co |
| `ghost-translate-post` | Called by other workflows | Translates one post with DeepL, writes its English twin and reindexes it |
| `ghost-translate-batch` | Daily 05:30 UTC, manual | Translates what is still missing, within the DeepL quota |
| `ghost-feedback-chatwoot-send` | Blog feedback tab | Sends ideas, errors and support requests from the blog to Chatwoot |
| `ghost-search-index-es` | Manual rebuild, called by other workflows | Keeps the blog's Typesense search index up to date |
| **Community (Discourse)** | | |
| `discourse-community-cover-add` | Discourse webhook, manual backfill | Brand covers for wiki, course and glossary topics without an image |
| `discourse-curso-artifact-publish` | Webhook with a secret header | Creates or updates a course artifact on the forum |
| `discourse-curso-quiz-totals-publish` | Hourly | Publishes anonymous course quiz totals once a quiz has 5 answers |
| `discourse-authentik-groups-sync` | Schedule | Mirrors Discourse group membership into Authentik groups |
| `paper-trading-prices` | Every 5 min | Kraken prices for the paper trading game |
| `paper-trading-ranking` | Hourly | Updates the ranking and adds new players to their group |
| `paper-trading-daily` | Daily 12:05 UTC | Posts the daily summary |
| **Operations** | | |
| `stack-status-check` | Every 5 min, `GET /estado` | Checks our services and serves their status to criptonautas.co/stack |
| `litellm-alerts-ntfy` | LiteLLM webhook | Forwards LiteLLM alerts to ntfy |
| `workflows-errors-ntfy` | Error in any workflow | Sends the error to ntfy |
| `workflows-backup-github` | Every 12 h, manual | This backup |

## License

[GPL-3.0](LICENSE).

Text of this README under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
