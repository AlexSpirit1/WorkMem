---
name: rabbitmq_events
description: RabbitMQ підключення і шаблони подій для CRM payment черги
type: project
---

**Connection:** http://162.55.164.90:15682 (Management HTTP API)
**Credentials:** admin/admin (stage only)
**Queue:** `Events_Crm_Deal_Payment_stage`
**Publish endpoint:** `POST /api/exchanges/%2F/amq.default/publish`

**Why:** Використовується для ручного тригеру CRM payment подій при тестуванні automation flows.
**How to apply:** Використовувати curl або `shared/helpers/rabbitmq.helper.ts`. Завжди встановлювати `routing_key` = ім'я черги, `payload_encoding` = `"string"`.

---

## CRM Deal Payment Complete — базовий шаблон

Поля що змінюються між тестами:
- `data.id` — dealId
- `data.userId / user_id / responsibleId` — accountId
- `data.pipeline.id` — pipelineId
- `contacts[0].id` — contactId
- `contacts[0].userId / user_id / responsibleId` — accountId
- `contacts[0].emails[0].email` — contact email
- `payments[0].contactId` — contactId
- `payments[0].dealId` — dealId

Поля можна повністю опускати (не null) — наприклад `data.id`, `payments[0].dealId`, `data.pipeline`.

```json
{
  "scope": "crm-service-events",
  "event": "crm.deal.payment.complete",
  "__id": "002cec16-7c99-ea44-3fe2-0f806bed85f8",
  "data": {
    "id": "<dealId>",
    "userId": "<userId>",
    "user_id": "<userId>",
    "name": "test_payment",
    "pipeline": { "id": "<pipelineId>", "name": "Основная воронка" },
    "step": { "id": 38, "name": "default_step_in_progress" },
    "status": "active",
    "responsibleId": "<userId>",
    "source": "manually",
    "price": { "amount": 12, "currency": "UAH" },
    "attributes": [], "attachments": [],
    "contacts": [{
      "id": "<contactId>",
      "userId": "<userId>", "user_id": "<userId>",
      "firstName": "testpayment", "lastName": "",
      "responsibleId": "<userId>",
      "sources": [{ "source": "manually", "externalContactId": null }],
      "phones": [],
      "emails": [{ "email": "<email>", "isMain": true }],
      "messengers": [], "tags": [], "attachments": [], "attributes": [],
      "createdAt": "2026-04-03T19:31:24Z",
      "updatedAt": "2026-04-03T19:31:24Z"
    }],
    "products": [],
    "payments": [{
      "orderId": "77c0ce6a-d5b1-4911-bbf9-f85cec7f8768",
      "contactId": "<contactId>",
      "dealId": "<dealId>",
      "status": "complete",
      "orderOriginalService": "crm",
      "merchantUuid": "6a8b6468-08ae-4ea6-a1da-e64f6e87b3b5",
      "merchantName": "LiqPay",
      "paymentMethod": "LiqPay",
      "price": { "amount": 12, "currency": "UAH" },
      "promocode": { "promoCode": null, "promoCodeDiscount": null, "promoCodeType": null },
      "description": "test_payment"
    }],
    "createdAt": "2026-04-06T15:13:37Z",
    "updatedAt": "2026-04-06T15:14:04Z"
  }
}
```

## Тестові акаунти

| env | userId | note |
|-----|--------|------|
| stage | 7046460 | основний тестовий акк |
| stage | 8662602 | es05, preprod тести #67601 |
