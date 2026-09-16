# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T09:12:43+00:00 |

---

# NotificationService Architecture

## 1. Purpose & Overview

**OrderFlow.NotificationService** is a standalone .NET 8 minimal-API microservice designed as a demo for handling customer notifications triggered by order confirmation or cancellation events in an external order-management system.

- **Accepts HTTP events**: Receives requests when orders are confirmed or cancelled.
- **Validates input**: Ensures required fields are provided and valid.
- **Simulates notification sending**: Instead of integrating with real email/SMS providers, it logs a message to indicate a notification was "sent."
- **Stateless**: Does not store any notification records—no persistence layer.
- **Returns status**: Provides a notification ID and status in the response.
- **Demo-only**: Not intended for production; no external integrations.

---

## 2. Tech Stack

- **Language**: C# (.NET 8)
- **API Framework**: Minimal-API (ASP.NET Core)
- **Testing**: xUnit
- **Configuration**: JSON files (`appsettings.json`)
- **Swagger/OpenAPI**: Enabled in Development environment

---

## 3. API / Entry Points

The service exposes the following HTTP endpoints:

| Method | Route                                   | Description                                                     |
|--------|-----------------------------------------|-----------------------------------------------------------------|
| POST   | `/api/notifications/order-confirmed`    | Accepts order confirmation payload, validates, logs, returns notification status. |
| POST   | `/api/notifications/order-cancelled`    | Accepts order cancellation payload, validates, logs, returns notification status. |
| GET    | `/api/notifications/health`             | Simple health check endpoint.                                   |

- **Validation failures**: Returns `400 Bad Request` with plain-text error message.
- **Swagger UI**: Exposed at `/swagger` during development.

---

## 4. Data Layer

- **Persistence**: None. The service does NOT persist data to any database, cache, or external storage.
- **Storage**: All "sent" notifications are only written as log lines.
- **Configuration**: Uses JSON files for configuration (`appsettings.json`, `appsettings.Development.json`).
- **Schema Hints**: Models found in `Models/NotificationModels.cs` define the expected payloads for each endpoint.

---

## 5. Key Modules

### Source Directory: `src/OrderFlow.NotificationService/`

- **Program.cs**: Main entry point; configures endpoints, DI, logging, and API setup.
- **Models/NotificationModels.cs**: Data models for notification payloads (order confirmation/cancellation).
- **Validation/NotificationValidator.cs**: Request validation logic (required fields, data integrity).
- **appsettings.json / appsettings.Development.json**: Configuration files (ports, environment setting, etc).
- **Properties/launchSettings.json**: Development environment launch configuration.

### Test Directory: `tests/OrderFlow.NotificationService.Tests/`

- **NotificationEndpointsTests.cs**: xUnit tests for endpoint behavior—both successful requests and validation failures.
- **OrderFlow.NotificationService.Tests.csproj**: Test project definition.

---

## 6. Dependencies

- **External Libraries**:
  - **ASP.NET Core Minimal-API**: For HTTP routing and handling.
  - **xUnit**: Unit testing framework.
  - **Swagger (Swashbuckle?)**: For API documentation in development.

- **External Services**: **None.**
  - No integration with real notification providers (email/SMS).
  - Self-contained and stateless.

---

## 7. Deployment Notes

- **Build & Run**:
  - Start with:  
    ```bash
    cd src/OrderFlow.NotificationService
    dotnet run
    ```
  - Default listening address: `http://localhost:5100`
  - Development environment enabled by default.

- **Testing**:
  - Run tests with:
    ```bash
    dotnet test
    ```

- **Development Features**:
  - Swagger UI is accessible during development at `/swagger`.
  - Launch settings are defined in `Properties/launchSettings.json`.

- **Production Considerations**:
  - Designed only for demo purposes; lacks real provider integration and data persistence.

---

> **Notes:**  
> - The service is strictly stateless and demo-focused; no data is stored or external notifications sent.  
> - No database, caching, message queue, or external API keys are referenced in available files.  
> - All configurations are local and via JSON.  
> - Directory structure and code organization are clear; no ambiguity regarding purpose or operation.