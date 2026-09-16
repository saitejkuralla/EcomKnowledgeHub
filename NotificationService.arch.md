# NotificationService

| Field | Value |
|---|---|
| Type | backend |
| Commit/Fingerprint | `708588caea50` |
| Analyzed at | 2026-09-16T11:10:11+00:00 |

---

# OrderFlow.NotificationService Architecture

## 1. Purpose & Overview

OrderFlow.NotificationService is a demo microservice built with .NET 8. Its primary function is to simulate sending customer notifications when an order is **confirmed** or **cancelled** in an external order-management system. The service validates incoming requests, logs notification events (without actually sending emails or SMS), and returns a generated notification ID and status. No real provider integrations or data persistence exist—it is intended for demonstration purposes.

---

## 2. Tech Stack

- **Language**: C#
- **Framework**: .NET 8 Minimal API
- **Testing**: xUnit
- **Configuration**: JSON files (`appsettings.json`, `appsettings.Development.json`)
- **API Documentation**: Swagger UI (enabled by default in development)

---

## 3. API / Entry Points

### HTTP Endpoints

#### `POST /api/notifications/order-confirmed`
- **Input**: `orderId`, `customerName`, `customerEmail`, `total` (must be >= 0), `confirmedAtUtc`
- **Validation**: Required fields & non-negative total
- **Behavior**: Logs a confirmation notification; returns notification ID and status
- **Response**: `202 Accepted` with JSON containing `notificationId` and `status`

#### `POST /api/notifications/order-cancelled`
- **Input**: `orderId`, `customerName`, `customerEmail`, `cancelledAtUtc`
- **Validation**: Required fields
- **Behavior**: Logs a cancellation notification; returns notification ID and status
- **Response**: `202 Accepted` with JSON containing `notificationId` and `status`

#### `GET /api/notifications/health`
- **Behavior**: Returns health status of the service
- **Response**: `200 OK` with `{ "status": "Healthy" }`

### Error Handling
- For missing/invalid fields, returns `400 Bad Request` with a plain-text error message.

### API Documentation
- **Swagger UI**: Available at `/swagger` when running in the Development environment.

---

## 4. Data Layer

- **Persistence**: None—no database, cache, or storage is implemented.
- **Data Handling**: Request payloads are validated but not persisted.
- **Schema**: Models for notification events defined in C# (`NotificationModels.cs`). Responses contain generated UUIDs and status.

---

## 5. Key Modules

### src/OrderFlow.NotificationService
- **Program.cs**: Entry point, sets up minimal API routes and request handling.
- **Models/NotificationModels.cs**: Defines C# classes for order-confirmed and order-cancelled requests/responses.
- **Validation/NotificationValidator.cs**: Implements request payload validation logic.
- **appsettings.json / appsettings.Development.json**: Configuration files for environment-specific settings.
- **Properties/launchSettings.json**: IDE/runtime launch settings.
- **OrderFlow.NotificationService.csproj**: Project file specifying dependencies and build settings.

### tests/OrderFlow.NotificationService.Tests
- **NotificationEndpointsTests.cs**: xUnit tests covering endpoint behavior, including happy paths and validation failures.
- **OrderFlow.NotificationService.Tests.csproj**: Test project configuration.

---

## 6. Dependencies

- **External Libraries**:
  - .NET 8 SDK and runtime
  - xUnit (for testing)
- **External Services**:
  - None—no real notification provider or database integration.

---

## 7. Deployment Notes

- **Build**: Standard .NET build via `dotnet build`.
- **Run**: `dotnet run` from `src/OrderFlow.NotificationService` (listens on `http://localhost:5100` by default).
- **Test**: `dotnet test` (runs xUnit tests).
- **Swagger**: Available in development environment at `/swagger`.
- **Configuration**: Customizable via `appsettings.json` and `launchSettings.json`.
- **Solution File**: `OrderFlow.NotificationService.slnx` for IDE integration.

---

## Additional Notes

- The service is standalone and stateless.
- If any architectural or operational aspect is unclear (such as support for containerization, CI/CD, or logging configuration), it is not evident from the repository structure or README.