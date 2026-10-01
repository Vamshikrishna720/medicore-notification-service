# medicore-notification-service

Async notifications for the **MediCore** healthcare platform
([monorepo](https://github.com/Vamshikrishna720/medicore)).

## Highlights

- `/internal/notifications` ingest (shared-token guarded) called by appointment-service over Feign
- **@Async** dispatch on a dedicated `ThreadPoolTaskExecutor` (`medicore-mail-*` threads) via a **separate dispatcher bean** — cross-bean call so the `@Async` proxy actually engages
- Status lifecycle QUEUED → SENT / FAILED persisted per notification; simulated SMTP latency (swap in SES/SendGrid for production)
- Users read their own feed via JWT identity

## Endpoints

| Method | Path | Access |
|---|---|---|
| POST | `/internal/notifications` | internal token |
| GET | `/api/notifications?page=&size=` | JWT (any role) |

## Run

```bash
mvn spring-boot:run          # :8085 (needs MySQL + Eureka)
```

Swagger: `http://localhost:8085/swagger-ui/index.html`
