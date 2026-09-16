# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T08:55:24+00:00 |

---

# NotificationService Architecture

## 1. Purpose & Overview

**OrderFlow.NotificationService** is a standalone .NET 8 microservice designed as a demo for handling customer notifications. Its primary functions are:
- Accepting HTTP events for order confirmations and cancellations from an external order-management system.
- Validating incoming request data.
- Simulating notification delivery by logging (does not connect to email/SMS providers).
- Returning a generated notification ID and delivery status as part of the response.

**Note:** The service is purely for demonstration. It does not persist data nor send real notifications.

---

## 2. Tech Stack

- **Language:** C#
- **Framework:** .NET 8 Minimal API
- **Testing:** xUnit
- **Configuration:** appsettings.json (standard .NET configuration)

---

## 3. API / Entry Points

Exposed HTTP endpoints:

- `POST /api/notifications/order-confirmed`
  - Input: `orderId`, `customerName`, `customerEmail`, `total`, `confirmedAtUtc`
  - Validates input; logs notification; returns generated `notificationId` (202 Accepted).
- `POST /api/notifications/order-cancelled`
  - Input: `orderId`, `customerName`, `customerEmail`, `cancelledAtUtc`
  - Validates input; logs notification; returns generated `notificationId` (202 Accepted).
- `GET /api/notifications/health`
  - Simple health check endpoint. Returns `{"status": "Healthy"}` (200 OK).

**Error Handling:**
- Validation failures (missing/empty fields, negative total, etc.) return `400 Bad Request` with an error message.

**Swagger UI:** Available at `/swagger` when running in the `Development` environment.

---

## 4. Data Layer

- **Persistence:** None. The service does not store any data permanently.
- **Storage/Caching:** None.
- **Schema hints:** Data models defined in `Models/NotificationModels.cs` for request validation (includes fields like `orderId`, `customerName`, `customerEmail`, `total`, `confirmedAtUtc`, `cancelledAtUtc`).

---

## 5. Key Modules

- `Program.cs`
  - Entry point; defines minimal API routes, logging, and response handling.
- `Models/NotificationModels.cs`
  - Contains C# model classes for notification requests and responses.
- `Validation/NotificationValidator.cs`
  - Contains validation logic for incoming API requests.
- `appsettings.json` / `appsettings.Development.json`
  - Configuration files for application settings, likely for logging and environment.
- `Properties/launchSettings.json`
  - Local launch profiles and port settings.
- **Tests:**
    - `tests/OrderFlow.NotificationService.Tests/NotificationEndpointsTests.cs`
      - xUnit tests covering endpoint behaviors and validation.
    - `OrderFlow.NotificationService.Tests.csproj`
      - Test project file.

---

## 6. Dependencies

- **External Services:** None; the service is fully self-contained (no integration with real notification providers).
- **Libraries:** Standard .NET 8 libraries for minimal APIs, logging, and validation.

---

## 7. Deployment Notes

- **Build & Run:**
    - Navigate to `src/OrderFlow.NotificationService` and run `dotnet run`.
    - By default, listens on `http://localhost:5100`.
- **Swagger UI:** Enabled in `Development` environment for API exploration.
- **Testing:** Run `dotnet test` for the xUnit test suite.
- **Project Files:**
    - `.csproj` files define build and dependency metadata.
    - `.slnx` solution grouping.
    - `launchSettings.json` for development (port, profile config).

**No evidence of containerization, CI/CD, or cloud deployment**—deploys as a simple .NET console web application.

---

## Summary

OrderFlow.NotificationService is a minimalist C#/.NET microservice for demoing order notification flows, emphasizing validation and endpoint structure. It is stateless, has no persistent storage or external integrations, and is designed for easy local use and testing.