# After-Sales Service System — WeChat Mini Program

Real-time after-sales service system, built with a Devin Bot.

Customers scan the QR code on their product to submit a repair request, upload photos and videos, and track service progress in real time:

Received → Triaged → Assigned → Dispatched → En Route → On Site → Repairing → Quality Check → Completed → Rated → Closed

## Features

- Real-time ticket tracking over WebSocket
- Smart dispatch: nearest available technician by skill and location
- SLA countdown with auto-escalation when a ticket is overdue
- Spare-parts inventory with 2-hour TTL reservations
- Offline-first for field technicians: local cache + outbox queue + idempotency keys
- Admin dashboard and customer ratings

## Tech stack

- Frontend: WeChat Mini Program with Taro + TypeScript
- Backend: NestJS
- Database: PostgreSQL + Prisma
- Cache / queue: Redis
- Realtime: WebSocket (Socket.io)
- CI/CD: GitHub Actions, dev → staging → canary 5% → prod, deploy freeze 8am–6pm

## Day-one plan

PR #1 scaffolds the Turborepo monorepo, the Ticket model with the 12-state machine, POST /auth/wechat (wx.login → code2session → JWT), and the WebSocket gateway. Verified by a Socket.io smoke test in CI: create a ticket, change status to Assigned, assert the Mini Program receives ticket.status_changed within 2 seconds.

## Business

- ~200 existing customers, 3 field technicians, 1 dispatcher
- 25–40 tickets/day, ~800/month, $25k+/month flowing through the system
- Currently manual in WeChat groups + spreadsheets, ~15% tickets lost or delayed
