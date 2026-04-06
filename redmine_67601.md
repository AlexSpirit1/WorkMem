---
name: redmine_67601
description: Контекст і тест-план для баг-фіксу A360 test webhook (#67601)
type: project
---

**Тікет:** https://tracker.sendpulse.com/issues/67601
**Статус:** Testing (Assigned: Oleksandr Svyrydenko)
**Проект:** Automations А360

**Що виправлено:**
- Test webhook на наш event URL більше не повертає `"The request did not pass code verification"`
- Перевірку наявності ордера прибрано — тепер дивимось тільки на тариф
- Платний тариф → без обмежень
- Free/expired → обмеження 1 раз на годину; тестовий вебхук → `"Upgrade required to access this feature"`
- Виправлено DTO error (`isFreeSformSubmitAllowed` null → bool)
- Виправлено `Undefined variable $result` при кількох URL

**Test endpoint:** `POST /api/a360-service/v2/automation/blocks/action/test-webhook/`

**Тестові акаунти:**
- preprod es00: `6878122` → https://pre.sendpulse.com/automation/flow/id/334910, action ID: `80620`
- stage es05: `8662602` → https://pre.sendpulse.com/automation/constructor/56127

**Why:** Потрібно покрити тестами після двох послідовних фіксів (19.03 і 03.04)
**How to apply:** Тест-план затверджено. Наступний крок — написати автотести для `test-webhook` ендпоінту.

**Тестування 2026-04-06:**
Тестував вручну через RabbitMQ — публікував `crm.deal.payment.complete` івенти в чергу `Events_Crm_Deal_Payment_stage` з різними `contactId`, `dealId`, `userId`, `pipelineId`, email. UI та автотести не використовувались.
