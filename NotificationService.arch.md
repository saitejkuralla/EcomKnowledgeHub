# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T09:07:33+00:00 |

---

# NotificationService Architecture

## 1. Purpose & Overview

**NotificationService** is a small, demo .NET 8 backend microservice that simulates sending customer notifications when an order is confirmed or cancelled in an external order-management system.  
- It receives HTTP requests representing order-confirmed and order-cancelled events.
- It validates request payloads.
- It "sends" notifications by writing log lines (no real email/SMS provider integrated).
- No data is persisted—responses include a generated notification ID and status.

## 2. Tech Stack

- **Language:** C#
- **Framework:** .NET 8 Minimal API
- **Test Framework:** xUnit (for unit/integration testing)
- **Configuration:** JSON files for environment settings

## 3. API / Entry Points

The service exposes the following HTTP endpoints:

**POST /api/notifications/order-confirmed**  
- Accepts order confirmation event payload.
- Validates fields: `orderId`, `customerName`, `customerEmail` (must be non-empty), `total` (>= 0), `confirmedAtUtc`.
- On success: logs notification, returns `202 Accepted` with `{ notificationId, status }`.
- On validation failure: returns `400 Bad Request` with error message.

**POST /api/notifications/order-cancelled**  
- Accepts order cancellation event payload.
- Validates fields: `orderId`, `customerName`, `customerEmail` (must be non-empty), `cancelledAtUtc`.
- On success: logs notification, returns `202 Accepted` with `{ notificationId, status }`.
- On validation failure: returns `400 Bad Request` with error message.

**GET /api/notifications/health**  
- Returns `{ status: "Healthy" }` for service health checking.

**Swagger UI**  
- Hosted at `/swagger` by default in Development environment.

## 4. Data Layer

- **No persistent storage:** The service does **not** use a database, cache, or external storage.
- **Data Model:** Defined in `NotificationModels.cs` (likely includes DTOs for order-confirmed and order-cancelled events).
- **Configuration:** Uses `appsettings.json` and `appsettings.Development.json` for environment-specific settings.

## 5. Key Modules

- `src/OrderFlow.NotificationService/Program.cs`  
  - Entry point, sets up the Minimal API and routes.

- `src/OrderFlow.NotificationService/Models/NotificationModels.cs`  
  - Defines request/response models (e.g., notification payloads).

- `src/OrderFlow.NotificationService/Validation/NotificationValidator.cs`  
  - Handles server-side input validation for the endpoints.

- `src/OrderFlow.NotificationService/Properties/launchSettings.json`  
  - Contains local development settings (ports, environment, etc.).

- `src/OrderFlow.NotificationService/appsettings*.json`  
  - Configures runtime settings (potentially log levels, environment).

- `tests/OrderFlow.NotificationService.Tests/NotificationEndpointsTests.cs`  
  - xUnit test cases for endpoints and validation.

## 6. Dependencies

- **.NET Framework Libraries:** Minimal API stack, JSON handling, logging.
- **External Services:** None (demo only; does not interface with real email/SMS providers).
- **Test Libraries:** xUnit for automated testing.

## 7. Deployment Notes

- **Build/Run:**  
  - Standard .NET workflow using `dotnet run` from the `src/OrderFlow.NotificationService` directory.
  - Listens on `http://localhost:5100` by default.
  - Development environment includes Swagger UI.

- **Testing:**  
  - Execute tests via `dotnet test`.

- **Deployment Configuration:**  
  - Controlled via `appsettings.json` and `launchSettings.json`; no explicit Docker or cloud configs present.
  - No CI/CD specifics or deployment scripts (e.g., Dockerfile, YAML) evident.

---

**Uncertainties:**
- No evidence of production integrations (e.g., SMTP, Twilio, databases).
- Not clear what logging provider is used, only that log lines are written.
- No persistence mechanism; notification IDs are generated per request and ephemeral.