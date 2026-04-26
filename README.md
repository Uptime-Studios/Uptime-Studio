┌─────────────────┐     HTTP      ┌──────────────────────┐
│   Browser /     │ ────────────► │   Express API Server  │
│   Frontend      │               │   (src/index.js)      │
└─────────────────┘               └──────────┬───────────┘
                                             │ enqueue job
                                             ▼
                                   ┌──────────────────┐
                                   │   BullMQ Queue   │
                                   │   (Redis)        │
                                   └────────┬─────────┘
                                            │ dequeue job
                                            ▼
                                   ┌──────────────────────┐
                                   │   Monitor Worker     │
                                   │   (monitorWorker.js) │
                                   │   1. SSRF check      │
                                   │   2. Axios GET       │
                                   │   3. Write Heartbeat │
                                   │   4. Notify Discord  │
                                   └──────────┬───────────┘
                                              │
                                   ┌──────────▼───────────┐
                                   │   PostgreSQL (Prisma) │
                                   └──────────────────────┘
