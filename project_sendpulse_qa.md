---
name: project_sendpulse_qa
description: Контекст Playwright-проекту sendpulse-qa-automation
type: project
---

Playwright-based тест-сюїт для сервісів SendPulse (CRM, EDU, Messengers, Automation, etc.).

**Why:** Покриття автотестами різних модулів SendPulse.
**How to apply:** При роботі в проекті дотримуватись CLAUDE.md конвенцій — POM патерни, fixture imports, структура тестів, tagging, cleanup з `afterEach`.

**Шляхи:**
- Цей ПК (svyry): `C:/Users/svyry/sendpulse-qa-automation`
- Інший ПК (Admin): `C:\Users\Admin\sendpulse-qa-automation`

**Ключові доповнення:**
- `shared/helpers/rabbitmq.helper.ts` — публікація повідомлень в RabbitMQ черги через HTTP Management API (без amqplib)
- RabbitMQ stage: http://162.55.164.90:15682, черга `Events_Crm_Deal_Payment_stage`
- `RABBITMQ_URL`, `RABBITMQ_USER`, `RABBITMQ_PASSWORD` додані в усі `.env.*.example` файли
