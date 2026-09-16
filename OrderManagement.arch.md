# OrderManagement

| Field | Value |
|---|---|
| Type | fullstack |
| Commit/Fingerprint | `bcc95601f02b` |
| Analyzed at | 2026-09-16T09:12:56+00:00 |

---

# OrderManagement / OrderFlow Architecture Overview

---

## 1. Purpose & Overview

OrderFlow is an order management application that enables users to manage **customers**, **products**, and **orders**, including support for product discounts. The system offers a web-based UI for creating, viewing, and editing orders, as well as managing customers and products. Business rules such as customer tiers and large order discounts are enforced server-side.

---

## 2. Tech Stack

**Backend**
- **Language:** C#
- **Frameworks:** .NET (likely ASP.NET Core for API)
- **ORM/Database:** Entity Framework Core indicated by usage of `DbContext`
- **Other:** Custom middlewares, validation via custom validators

**Frontend**
- **Language:** TypeScript
- **Framework:** Angular
- **Styling:** SCSS
- **Build tools:** Angular CLI

---

## 3. Backend: API / Entry Points

**Exposed via HTTP API Controllers:**
- `/api/customers`
    - [GET, POST, PUT, DELETE] via `CustomersController.cs`
- `/api/orders`
    - [GET, POST, PUT, DELETE] via `OrdersController.cs`
- `/api/products`
    - [GET, POST, PUT, DELETE] via `ProductsController.cs`

**Other Entry Points:**
- Application startup via `Program.cs`
- No CLI commands indicated

**API contract (requests & responses):**
- Contract DTOs for customer, order, and product management
- Requests and responses defined under `Contracts\Requests` and `Contracts\Responses`

---

## 4. Backend: Data Layer

- **Database:** 
    - Relational database (likely SQL), managed via Entity Framework Core with `OrderFlowDbContext.cs`
- **Schema Hints:**
    - Entities: `Customer`, `Order`, `OrderItem`, `Product`
    - Enums: `CustomerTier`, `OrderStatus`
    - Configurations for EF models (e.g., `CustomerConfiguration.cs`)
    - Discount subdomain with discount rules, calculators, and context
- **No evidence of external caching layer or blob storage**

---

## 5. Frontend: Routing & Pages

- **Routes defined in:** `src/app/app.routes.ts`
- **Main pages/components:**
    - `/dashboard`: Dashboard page
    - `/orders`: Order list, order creation (`order-list`, `order-create`)
    - `/orders/:id`: Order detail (`order-detail`)
    - `/customers`: Customers listing and form dialog
    - `/products`: Products listing and form dialog

- **Shared layout handled by:** `layout/app-shell.component.*`

---

## 6. Frontend: Component Architecture

- **Core domain models/services:**
    - `core/models`: Customer, Product, Order models
    - `core/services`: Service wrappers for API calls (customer, order, product)
- **Feature modules:**
    - `customers`: List view and form dialog
    - `products`: List view and form dialog
    - `orders`: List, detail, and create views
    - `dashboard`: Overview of system
- **Shared components:**
    - `shared/components`: Basic UI elements such as `confirm-dialog`, `empty-state`, and `tier-chip`
- **Layout:**
    - `layout/app-shell.component.*`: Main page layout/shell

---

## 7. Frontend: State Management

- **Data flow:** 
    - Handled using Angular service classes (no evidence of NgRx or any redux-like libraries)
    - Each domain has a corresponding service for API interaction and local state
- **Environment configs:** `src/environments/`

---

## 8. Key Modules

| Module / File                                                                                  | Layer     | Responsibility / Content                                 |
|------------------------------------------------------------------------------------------------|-----------|----------------------------------------------------------|
| `OrderFlow.Api/Controllers/CustomersController.cs`                                             | Backend   | Exposes customer-related API endpoints                   |
| `OrderFlow.Api/Controllers/OrdersController.cs`                                                | Backend   | Order-related API endpoints                              |
| `OrderFlow.Api/Controllers/ProductsController.cs`                                              | Backend   | Product-related API endpoints                            |
| `OrderFlow.Domain/Entities/Customer.cs, Order.cs, Product.cs, OrderItem.cs`                    | Backend   | Domain entities and logic                                |
| `OrderFlow.Domain/Discounts/`                                                                  | Backend   | Discount calculation rules and abstractions              |
| `OrderFlow.Infrastructure/Persistence/OrderFlowDbContext.cs`                                   | Backend   | EF Core DB Context integration                           |
| `OrderFlow.Infrastructure/Repositories/CustomerRepository.cs` (etc.)                           | Backend   | Data persistence implementation                          |
| `OrderFlow.Application/Services/OrderService.cs`, etc.                                         | Backend   | Business logic, service orchestration                    |
| `orderflow-ui/src/app/app.routes.ts`                                                           | Frontend  | Routing configuration                                    |
| `orderflow-ui/src/app/customers/customers.component.ts`                                        | Frontend  | Customers view logic                                     |
| `orderflow-ui/src/app/orders/order-create/order-create.component.ts`                           | Frontend  | Order creation UI                                        |
| `orderflow-ui/src/app/orders/order-list/order-list.component.ts`                               | Frontend  | Order list UI                                            |
| `orderflow-ui/src/app/shared/components/confirm-dialog/confirm-dialog.component.ts`            | Frontend  | Shared confirm dialog component                          |
| `orderflow-ui/src/app/core/services/order.service.ts`                                          | Frontend  | API interaction for Orders                               |

---

## 9. Dependencies

- **Backend**
    - .NET libraries (Entity Framework Core)
    - No direct mention of third-party integrations; likely standard .NET stack
- **Frontend**
    - Angular framework and dependencies via `package.json`
    - No clear evidence of extra major JS libraries for state, UI, or HTTP (e.g., no NgRx, no Material, unless in `package.json`)

---

## 10. Build & Deployment Notes

- **Backend**
    - Built as .NET solution (`.slnx` file, `csproj` files for each project)
    - Config via `appsettings.json`, `launchSettings.json`
    - Executed as typical ASP.NET Core web API

- **Frontend**
    - Built with Angular CLI (`angular.json`, `tsconfig.json`)
    - Standard npm scripts in `package.json`
    - `public/` folder for static assets
    - Environment-based build configurations (`environment.ts`, `environment.prod.ts`)

- **Deployment**
    - No explicit Docker, CI, or cloud config files in the listing
    - Must be deployed as separate backend API (.NET) and frontend SPA (Angular)

---

**Note**:  
Certain aspects (e.g., authentication, external services, deployment automation) are **unclear or not present** in this structure and are not covered.