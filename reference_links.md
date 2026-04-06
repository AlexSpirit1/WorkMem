---
name: reference_links
description: Ключові посилання по проекту A360 Deal Payment (#67169)
type: reference
---

## RabbitMQ черги
- Stage: http://162.55.164.90:15682/#/queues/%2F/Events_Crm_Deal_Payment_stage
- Stage (альт): http://159.69.138.120:15672/#/queues/%2F/Events_Crm_Deal_Payment_stage1

## Redmine
- Основна таска: https://tracker.sendpulse.com/issues/67169
- Ручна оплата: https://tracker.sendpulse.com/issues/69147

## Препрод ланцюжки
- https://pre.sendpulse.com/automation/flow/id/211450
- https://pre.sendpulse.com/automation/flow/id/340552
- https://pre.sendpulse.com/automation/flow/id/56436
- https://pre.sendpulse.com/automation/flow/id/56437
- https://pre.sendpulse.com/automation/flow/id/56459

## Скрипт
- `C:/Users/svyry/sendpulse-qa-automation/publish_rabbit.js` — відправка подій в RabbitMQ
- Черга зараз: `Events_Crm_Deal_Payment_stage` на `162.55.164.90:15682`
- Redmine API key: в `.env.stage`
