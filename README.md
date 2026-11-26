# ai-api-testing

Автоматична API-регресія для [Swagger Petstore](https://petstore3.swagger.io/) (навчальний проєкт).

## Що всередині

- `collections/petstore-crud.postman_collection.json` — Postman-колекція з CRUD-сценарієм:
  Create → Get → Update → Get → Delete → Verify deletion (6 запитів, 20 assertions).
- `.github/workflows/api-regression.yml` — GitHub Actions workflow з Newman.

## Як запускається

| Тригер | Що відбувається |
|---|---|
| Вручну (Actions → API regression → Run workflow) | Регресія запускається одразу |
| Pull request зі змінами колекції чи workflow | Регресія запускається для перевірки змін (без публікації звіту) |
| Розклад: щопонеділка о 07:00 UTC | Workflow перевіряє Jira і запускає регресію лише тоді, коли є тікети з лейблом `api-testing` у статусі `Ready for QA` |

## HTML-звіт

Звіт кожного прогону публікується на GitHub Pages:

- останній прогін: `https://<owner>.github.io/ai-api-testing/latest/`
- конкретний прогін: `https://<owner>.github.io/ai-api-testing/runs/<номер прогону>/`

## Секрети (Settings → Secrets and variables → Actions)

| Секрет | Значення |
|---|---|
| `JIRA_BASE_URL` | Адреса Jira, наприклад `https://your-site.atlassian.net` |
| `JIRA_EMAIL` | Email акаунта Jira |
| `JIRA_API_TOKEN` | API-токен Jira (https://id.atlassian.com/manage-profile/security/api-tokens) |

## Локальний запуск

```bash
npx newman run collections/petstore-crud.postman_collection.json
```
