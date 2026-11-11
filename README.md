# n8n-workflows

**ENGLISH** | [ESPAÑOL](README.es.md)

Backup of the n8n workflows that run criptonautas.co and comunidad.criptonautas.co.
`workflows-publish-github` publishes them here every 12 hours, one file per workflow,
named after it.

## Rules

- Only **active** workflows are published. Drafts and paused ones stay in n8n.
- Names are kebab-case `service-action-object` (`ghost-cover-add`). A prefix such as
  `[ON-HOLD]` or `[TO-EDIT]` keeps a workflow out of the backup.
- The backup never deletes: a workflow that is switched off or renamed leaves its old
  file here until someone removes it.

## Workflows

| Workflow | Trigger | What it does |
|---|---|---|
| **Blog (Ghost)** | | |
| `ghost-cover-add` | Ghost webhook | Gives a post without a featured image a brand cover from [criptonautas-featured-cover](https://github.com/criptonautas/criptonautas-featured-cover) |
| `ghost-featured-image-send` | Ghost webhook, manual backfill | Runs tagged featured images through [criptonautas-featured-ghost-filter](https://github.com/criptonautas/criptonautas-featured-ghost-filter) |
| `ghost-translate-sync` | Ghost webhook | Keeps en.criptonautas.co in step with each change on criptonautas.co |
| `ghost-translate-post` | Called by other workflows | Translates one post with DeepL, writes its English twin and reindexes it |
| `ghost-translate-batch` | Daily 05:30 UTC, manual | Translates what is still missing, within the DeepL quota |
| `ghost-search-index-es` | Manual rebuild, called by other workflows | Keeps the blog's Typesense search index up to date |
| **Community (Discourse)** | | |
| `discourse-community-cover-add` | Discourse webhook, manual backfill | Brand covers for wiki, course and glossary topics without an image |
| `curso-publish-artifact` | Webhook | Creates or updates a course artifact on the forum |
| `curso-publish-quiz-totals` | Hourly | Publishes anonymous course quiz totals once a quiz has 5 answers |
| `paper-trading-prices` | Every 5 min | Kraken prices for the paper trading game |
| `paper-trading-ranking` | Hourly | Updates the ranking and adds new players to their group |
| `paper-trading-daily` | Daily 12:05 UTC | Posts the daily summary |
| **Operations** | | |
| `stack-status-check` | Every 5 min, `GET /estado` | Checks our services and serves their status to criptonautas.co/stack |
| `alerts-litellm-ntfy` | LiteLLM webhook | Forwards LiteLLM alerts to ntfy |
| `workflows-errors-ntfy` | Error in any workflow | Sends the error to ntfy |
| `workflows-publish-github` | Every 12 h, manual | This backup |

## License

[GPL-3.0](LICENSE).

Text of this README under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
