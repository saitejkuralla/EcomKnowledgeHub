# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T12:37:43+00:00 |

---

# NotificationService Architecture

## 1. Purpose & Overview

**OrderFlow.NotificationService** is a lightweight demo microservice built on .NET 8, exposing a minimal HTTP API for customer notifications relating to orders. It is intended to simulate—without actual integration—sending notifications when an order is confirmed or cancelled. The service does not interact with real email/SMS providers or persist any data; instead, it logs notification events and returns a notification status.

**Key Functions:**
- Accepts order-confirmed and order-cancelled events via HTTP.
- Validates incoming request payloads.
- Logs a simulated "notification sent" message.
- Returns a generated notification ID and "Sent" status.

## 2. Tech Stack

- **Language:** C#
- **Framework:** .NET 8 (Minimal API)
- **Testing Framework:** xUnit
- **Configuration:** JSON-based (`appsettings.json`, `appsettings.Development.json`)
- **Tools:** Swagger UI (for API exploration in development)

## 3. API / Entry Points

Exposed HTTP endpoints:

### `POST /api/notifications/order-confirmed`
- Validates: `orderId`, `customerName`, `customerEmail` (non-empty), `total` (>= 0), `confirmedAtUtc`.
- Response: `202 Accepted` with `{ notificationId, status }`.

### `POST /api/notifications/order-cancelled`
- Validates: `orderId`, `customerName`, `customerEmail` (non-empty), `cancelledAtUtc`.
- Response: `202 Accepted` with `{ notificationId, status }`.

### `GET /api/notifications/health`
- Returns `200 OK` with `{ status: "Healthy" }`.

**Validation failures:** Return `400 Bad Request` with a plain-text error message.

**Swagger UI:** Available at [http://localhost:5100/swagger](http://localhost:5100/swagger) in Development environment.

## 4. Data Layer

- **Persistence:** None—no database, cache, or external storage.
- **Data Models:** Defined in `Models/NotificationModels.cs`. Used for request validation and response formatting.
- **Configuration:** Uses `appsettings.json`, `appsettings.Development.json` for settings (unclear details; likely hosting, logging).

## 5. Key Modules

**Project Structure:**

```
src/
  OrderFlow.NotificationService/
    OrderFlow.NotificationService.csproj         # Project file
    Program.cs                                  # Entry point / API route definitions
    Models/
      NotificationModels.cs                     # DTOs for notifications
    Validation/
      NotificationValidator.cs                  # Input validation logic
    Properties/
      launchSettings.json                       # Launch configs (dev env, ports)
    appsettings.json                            # Base config
    appsettings.Development.json                # Development overrides
tests/
  OrderFlow.NotificationService.Tests/
    NotificationEndpointsTests.cs               # xUnit tests for endpoints/validation
    OrderFlow.NotificationService.Tests.csproj  # Test project file
```

**Responsibilities:**
- `Program.cs`: Defines API routes/endpoints and their handlers.
- `Models/NotificationModels.cs`: Contains request/response models.
- `Validation/NotificationValidator.cs`: Handles validation logic for incoming requests.
- `NotificationEndpointsTests.cs`: Tests API endpoint behavior and validation.

## 6. Dependencies

- **External Libraries:** Standard .NET libraries (minimal; specifics not detailed, but JSON model binding, logging, and Swagger likely).
- **External Services:** None—no integration with email/SMS or databases.
- **Dev Tools:** Swagger UI for API testing, xUnit for automated tests.

## 7. Deployment Notes

- **Build/Run:**  
  ```bash
  cd src/OrderFlow.NotificationService
  dotnet run
  ```
  - Listens on `http://localhost:5100` by default.
  - Development environment is set by `launchSettings.json`.
  - Swagger UI is enabled in development for API exploration.

- **Testing:**  
  ```bash
  dotnet test
  ```
  - Test suite covers endpoint responses and validation.

- **Configuration:**  
  - Uses `appsettings.json` and environment-specific `appsettings.Development.json`. Details not provided, but typically for configuring host/port, logging, etc.

---

**Note:**  
- No data is persisted or retrieved; all operations are in-memory and focused on request validation and response generation.
- No integration with real notification delivery services.
- Project is intended for demo/sample purposes—production use would require significant extensions (e.g., real provider integration, storage).