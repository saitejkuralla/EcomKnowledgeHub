# OrderManagement

| Field | Value |
|---|---|
| Type | fullstack |
| Commit/Fingerprint | `bcc95601f02b` |
| Analyzed at | 2026-09-16T08:39:20+00:00 |

---

```markdown
# OrderManagement Architecture Overview

## 1. Purpose & Overview

OrderManagement (OrderFlow) is a full-stack application for managing orders, products, and customers. It enables users to create, view, and manage customers and products, generate orders with product line items, and apply discount logic (such as customer tiers and large order discounts). The system includes both a backend API and an Angular-based frontend.

---

## 2. Tech Stack

### Backend

- **Language:** C#
- **Framework:** ASP.NET Core (Web API)
- **ORM/DB Layer:** Entity Framework Core
- **Testing:** xUnit (evident from test naming)

### Frontend

- **Language:** TypeScript
- **Framework:** Angular
- **Styling:** SCSS
- **Testing:** Jasmine/Karma (by Angular convention)

---

## 3. Backend: API / Entry Points

The main API exposes RESTful endpoints grouped by entity:

- **/api/customers**
    - GET, POST (managed by `CustomersController.cs`)
- **/api/orders**
    - GET, POST (managed by `OrdersController.cs`)
- **/api/products**
    - GET, POST (managed by `ProductsController.cs`)

API contracts are defined in `Contracts/Requests` and `Contracts/Responses`.

> *Note: Exact route patterns and supported verbs are inferred from filename conventions; for supported requests/responses, see the corresponding contracts.*

---

## 4. Backend: Data Layer

- **Database:** Entity Framework Core (EF Core) DbContext (`OrderFlowDbContext.cs`)
- **Entities:**
    - Customer (`Entities/Customer.cs`)
    - Order (`Entities/Order.cs`)
    - Product (`Entities/Product.cs`)
    - OrderItem (`Entities/OrderItem.cs`)
- **Entity Configuration:** Provided in `Persistence/Configurations/*`
- **Seeding/IDs:** Managed in `SeedIds.cs`
- **Discount Model:** Implemented via strategy/policy patterns (`Discounts/` and `Discounts/Rules/`)

---

## 5. Frontend: Routing & Pages

Routing is configured in `src/app/app.routes.ts`, with page components as follows:

- **Dashboard:** `dashboard/dashboard.component.ts` (likely home/overview)
- **Customers:** `customers/customers.component.ts`
- **Products:** `products/products.component.ts`
- **Orders:** 
    - List: `orders/order-list/order-list.component.ts`
    - Create: `orders/order-create/order-create.component.ts`
    - Detail: `orders/order-detail/order-detail.component.ts`

Page navigation is typical for a CRUD business app, routed under their respective resources.

---

## 6. Frontend: Component Architecture

Components are grouped by domain feature:

- **Feature Components:** In feature folders (`customers/`, `products/`, `orders/`, `dashboard/`)
- **Dialogs/Forms:** `customer-form-dialog.component.*`, `product-form-dialog.component.*`
- **Shared Components:** 
    - `shared/components/confirm-dialog/`
    - `shared/components/empty-state/`
    - `shared/components/tier-chip/`
- **Layout/Shell:** App-level frame in `layout/app-shell.component.*`

Composition appears to follow Angular best practices: feature components use shared/util components, forms are presented in dialog components, and state/services are injected.

---

## 7. Frontend: State Management

- **Angular Services:** State/data flow managed via services in `core/services/`:
    - `customer.service.ts`
    - `order.service.ts`
    - `product.service.ts`
- **Models:** Defined in `core/models/`
- **Discount Logic:** Some calculation/preview logic present in `discount-preview.util.ts`
- **No explicit use of NgRx or other state libraries** is evident from the file structure; likely uses service-based state with Observables.

---

## 8. Key Modules

| Path                                                        | Front/Back | Responsibility                                                        |
|-------------------------------------------------------------|------------|-----------------------------------------------------------------------|
| backend/OrderFlow.Api/Controllers/                          | Backend    | API endpoint implementations for Customers, Orders, Products          |
| backend/OrderFlow.Application/Services/                     | Backend    | Domain/application business logic services                            |
| backend/OrderFlow.Infrastructure/Persistence/               | Backend    | Database context and entity configurations                            |
| backend/OrderFlow.Domain/Discounts/                         | Backend    | Discount rules, calculators, and strategy implementations             |
| backend/OrderFlow.Api/Middleware/ExceptionHandlingMiddleware.cs | Backend | Centralized API exception handling                                    |
| frontend/orderflow-ui/src/app/dashboard/                    | Frontend   | Dashboard/overview page                                               |
| frontend/orderflow-ui/src/app/customers/                    | Frontend   | Customers list and form dialog components                             |
| frontend/orderflow-ui/src/app/orders/                       | Frontend   | Orders CRUD: lists, details, and creator components                   |
| frontend/orderflow-ui/src/app/products/                     | Frontend   | Products list and form dialog components                              |
| frontend/orderflow-ui/src/app/layout/                       | Frontend   | App shell/layout components                                           |
| frontend/orderflow-ui/src/app/core/services/                | Frontend   | Angular services for backend API integration per entity               |
| frontend/orderflow-ui/src/app/shared/components/            | Frontend   | Reusable UI components (confirm dialog, empty state, etc.)            |

---

## 9. Dependencies

- **Backend:**
    - ASP.NET Core
    - Entity Framework Core
    - (Possibly) FluentValidation or similar for request validation (suggested by `Validator` classes)
- **Frontend:**
    - Angular and Angular CLI
    - UI component dependencies (not explicitly listed; details in package.json)
    - [No explicit reference to Material or Bootstrap, but could be present; check package.json]

- **External Services:** None clearly evident.

---

## 10. Build & Deployment Notes

- **Backend:**
    - Built via .NET tooling (`.csproj` projects, `OrderFlow.slnx` solution)
    - Configuration via `appsettings.json` and `appsettings.Development.json`
    - `launchSettings.json` for local Dev config

- **Frontend:**
    - Built via Angular CLI (configured by `angular.json`, `tsconfig.*.json`)
    - Standard `ng build`, `ng serve` workflow
    - Environment files present for prod/dev (`environment.ts`, `environment.prod.ts`)

- **Testing:**
    - Backend: Unit and integration tests in `/tests/`
    - Frontend: Not explicitly listed; presumed via Angular's testing conventions

- **Deployment:** No explicit containerization or cloud deployment configuration files are present in the provided structure.

---
```