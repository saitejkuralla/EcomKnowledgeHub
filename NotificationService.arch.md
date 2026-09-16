# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T09:05:20+00:00 |

---

## Language Breakdown

- .cs: 4 file(s)
- .json: 3 file(s)
- .csproj: 2 file(s)
- (no ext): 1 file(s)
- .slnx: 1 file(s)
- .md: 1 file(s)

## README Excerpt

# OrderFlow.NotificationService

A small standalone .NET 8 minimal-API microservice that simulates sending customer
notifications when an order is confirmed or cancelled in an external order-management
system. This is a demo service — it does not integrate with a real email/SMS provider
and does not persist any data.

## What it does

- Accepts HTTP requests describing order-confirmed and order-cancelled events.
- Validates the request payload.
- "Sends" the notification by writing a log line (no real provider involved).
- Returns a generated notification id and status.

## Project structure

```
src/OrderFlow.NotificationService/   Minimal API project (Program.cs, models, validation)
tests/OrderFlow.NotificationService.Tests/  xUnit tests (happy paths + validation failure)
```

## How to run

```bash
cd src/OrderFlow.NotificationService
dotnet run
```

The service listens on **http://localhost:5100** by default.

Swagger UI is available at [http://localhost:5100/swagger](http://localhost:5100/swagger)
when running in the `Development` environment (the default for `dotnet run`).

## How to run the tests

```bash
dotnet test
```

## Endpoints

### POST /api/notifications/order-confirmed

Validates `orderId`, `customerName`, `customerEmail` (non-empty) and `total` (>= 0),
logs a confirmation notification, and returns `202 Accepted`.

```bash
curl -X POST http://localhost:5100/api/notifications/order-confirmed \
  -H "Content-Type: application/json" \
  -d '{
    "orderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "customerName": "Jane Doe",
    "customerEmail": "jane.doe@example.com",
    "total": 149.99,
    "confirmedAtUtc": "2026-09-16T10:00:00Z"
  }'
```

Response (`202 Accepted`):

```json
{
  "notificationId": "b3c1a2e4-1234-4a5b-9c6d-7e8f9a0b1c2d",
  "status": "Sent"
}
```

### POST /api/notifications/order-cancelled

Validates `orderId`, `customerName`, `customerEmail` (non-empty), logs a cancellation
notification, and returns `202 Accepted`.

```bash
curl -X POST http://localhost:5100/api/notifications/order-cancelled \
  -H "Content-Type: application/json" \
  -d '{
    "orderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "customerName": "Jane Doe",
    "customerEmail": "jane.doe@example.com",
    "cancelledAtUtc": "2026-09-16T11:30:00Z"
  }'
```

Response (`202 Accepted`):

```json
{
  "notificationId": "b3c1a2e4-1234-4a5b-9c6d-7e8f9a0b1c2d",
  "status": "Sent"
}
```

### GET /api/notifications/health

```bash
curl http://localhost:5100/api/notifications/health
```

Response (`200 OK`):

```json
{
  "status": "Healthy"
}
```

## Validation failures

Missing/empty `orderId`, `customerName`, `customerEmail`, or a negative `total` returns
`400 Bad Request` with a plain-text error message, e.g.:

```bash
curl -i -X POST http://localhost:5100/api/notifications/order-confirmed \
  -H "Content-Type: application/json" \
  -d '{
    "orderId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "customerName": "Jane Doe",
    "customerEmail": "",
  
... (truncated)

## Project Structure

```
.gitignore
OrderFlow.NotificationService.slnx
README.md
src\OrderFlow.NotificationService\OrderFlow.NotificationService.csproj
src\OrderFlow.NotificationService\Program.cs
src\OrderFlow.NotificationService\appsettings.Development.json
src\OrderFlow.NotificationService\appsettings.json
src\OrderFlow.NotificationService\Models\NotificationModels.cs
src\OrderFlow.NotificationService\Properties\launchSettings.json
src\OrderFlow.NotificationService\Validation\NotificationValidator.cs
tests\OrderFlow.NotificationService.Tests\NotificationEndpointsTests.cs
tests\OrderFlow.NotificationService.Tests\OrderFlow.NotificationService.Tests.csproj
```

> Generated in **basic mode** (no LLM configured). Set `LLM_PROVIDER` and the matching API key in `.env` for AI-generated analysis.