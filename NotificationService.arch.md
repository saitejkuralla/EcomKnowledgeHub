# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T13:24:18+00:00 |

---

# NotificationService Architecture

---

## 1. Purpose & Overview

**OrderFlow.NotificationService** is a standalone .NET 8 minimal-API microservice designed to simulate sending customer notifications when an order is confirmed or cancelled in an external order-management system. It is intended as a demo, with no real integration to email/SMS providers and no persistent storage.

- Accepts HTTP requests for order event notifications.
- Validates important fields in incoming requests.
- "Sends" notifications by writing a log entry.
- Returns a generated notification ID and status to the caller.

---

## 2. Tech Stack

- **Language:** C# (.cs)
- **Framework:** .NET 8 Minimal API
- **Testing:** xUnit
- **Key Libraries:**  
  - ASP.NET Core (inferred from minimal API usage and Program.cs)
  - Swagger/OpenAPI UI (enabled in development)

---

## 3. API / Entry Points

**HTTP REST Endpoints (exposed on `http://localhost:5100`):**

| Endpoint                          | Method | Description                                         |
|------------------------------------|--------|-----------------------------------------------------|
| `/api/notifications/order-confirmed`   | POST   | Send order confirmation notification                |
| `/api/notifications/order-cancelled`   | POST   | Send order cancellation notification                |
| `/api/notifications/health`            | GET    | Health check endpoint                               |

- **Swagger UI:** Accessible at `/swagger` in development mode.
- **Validation:** All endpoints perform payload validation and return `400 Bad Request` on failure.

---

## 4. Data Layer

- **Persistence:** None. No database, cache, or file storage is used.
    - All notifications are simulated and logged; nothing is saved or retrieved.
- **Configuration:** Settings are provided via `appsettings.json` and `appsettings.Development.json`.

---

## 5. Key Modules

| Path                                        | Responsibility                                                          |
|----------------------------------------------|--------------------------------------------------------------------------|
| `src/OrderFlow.NotificationService/Program.cs`            | Entry point; configures endpoints, validation, and logging               |
| `src/OrderFlow.NotificationService/Models/NotificationModels.cs` | Defines request/response models for notifications                        |
| `src/OrderFlow.NotificationService/Validation/NotificationValidator.cs` | Contains validation logic for notification requests                      |
| `src/OrderFlow.NotificationService/appsettings*.json`     | Provides app configuration (e.g., port, env settings)                    |
| `src/OrderFlow.NotificationService/Properties/launchSettings.json`  | Local development launch profiles                                        |
| `tests/OrderFlow.NotificationService.Tests/NotificationEndpointsTests.cs` | Unit/integration tests of API endpoints and validation                   |
| `tests/OrderFlow.NotificationService.Tests/OrderFlow.NotificationService.Tests.csproj` | Test project configuration                                               |

---

## 6. Dependencies

- **External Services:**  
    - None. No email/SMS provider or database is integrated; all notifications are simulated.
- **External Libraries:**  
    - .NET 8 (ASP.NET Core)
    - xUnit (for tests)
    - Swagger/OpenAPI UI (for API docs in development)

---

## 7. Deployment Notes

- **Build & Run:**
    - Build and run with:
      ```bash
      cd src/OrderFlow.NotificationService
      dotnet run
      ```
    - Listens on `http://localhost:5100` by default.
    - Swagger UI is enabled in Development environment.

- **Testing:**
    - Run tests with:
      ```bash
      dotnet test
      ```

- **Configuration:**
    - JSON config files (`appsettings.json`, `appsettings.Development.json`) for settings.
    - `launchSettings.json` for local development profiles.
- **Project Structure:**
    - Main API and models under `src/OrderFlow.NotificationService/`.
    - Test suite under `tests/OrderFlow.NotificationService.Tests/`.

---

> **Note:**  
> No real integrations, storage, or advanced messaging features are present. The service is purely for demonstration and validation of notification mechanics.