# n8n-workflows

[ENGLISH](README.md) | **ESPAÑOL**

Backup de los workflows de n8n que hacen funcionar criptonautas.co y
comunidad.criptonautas.co. `workflows-publish-github` los publica acá cada 12 horas,
un archivo por workflow, con su nombre.

## Reglas

- Solo se publican los workflows **activos**. Los borradores y los pausados quedan en n8n.
- Los nombres van en kebab-case `servicio-acción-objeto` (`ghost-cover-add`). Un prefijo
  como `[ON-HOLD]` o `[TO-EDIT]` deja un workflow fuera del backup.
- El backup nunca borra: si un workflow se apaga o se renombra, su archivo viejo queda
  acá hasta que alguien lo quite.

## Workflows

| Workflow | Disparador | Qué hace |
|---|---|---|
| **Blog (Ghost)** | | |
| `ghost-cover-add` | Webhook de Ghost | Pone una portada de la marca a los posts sin imagen destacada, con [criptonautas-featured-cover](https://github.com/criptonautas/criptonautas-featured-cover) |
| `ghost-featured-image-send` | Webhook de Ghost, carga manual | Pasa las imágenes destacadas etiquetadas por [criptonautas-featured-ghost-filter](https://github.com/criptonautas/criptonautas-featured-ghost-filter) |
| `ghost-translate-sync` | Webhook de Ghost | Mantiene en.criptonautas.co al día con cada cambio en criptonautas.co |
| `ghost-translate-post` | Lo llaman otros workflows | Traduce un post con DeepL, escribe su gemelo en inglés y lo reindexa |
| `ghost-translate-batch` | Diario 05:30 UTC, manual | Traduce lo que falta, dentro de la cuota de DeepL |
| `ghost-search-index-es` | Reconstrucción manual, lo llaman otros workflows | Mantiene al día el índice de búsqueda Typesense del blog |
| **Comunidad (Discourse)** | | |
| `discourse-community-cover-add` | Webhook de Discourse, carga manual | Portadas de la marca para temas de wiki, curso y glosario sin imagen |
| `curso-publish-artifact` | Webhook | Crea o actualiza un artifact del curso en el foro |
| `curso-publish-quiz-totals` | Cada hora | Publica los totales anónimos de los quizzes del curso cuando un quiz tiene 5 respuestas |
| `paper-trading-prices` | Cada 5 min | Precios de Kraken para el juego de paper trading |
| `paper-trading-ranking` | Cada hora | Actualiza el ranking y suma a los jugadores nuevos a su grupo |
| `paper-trading-daily` | Diario 12:05 UTC | Publica el resumen del día |
| **Operación** | | |
| `stack-status-check` | Cada 5 min, `GET /estado` | Revisa nuestros servicios y entrega su estado a criptonautas.co/stack |
| `alerts-litellm-ntfy` | Webhook de LiteLLM | Reenvía las alertas de LiteLLM a ntfy |
| `workflows-errors-ntfy` | Error en cualquier workflow | Manda el error a ntfy |
| `workflows-publish-github` | Cada 12 h, manual | Este backup |

## Licencia

[GPL-3.0](LICENSE).

Texto de este README bajo [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
