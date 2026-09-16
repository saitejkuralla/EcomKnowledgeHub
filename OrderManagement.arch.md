# OrderManagement

| Field | Value |
|---|---|
| Type | fullstack |
| Commit/Fingerprint | `bcc95601f02b` |
| Analyzed at | 2026-09-16T09:06:01+00:00 |

---

## Language Breakdown

- .cs: 65 file(s)
- .ts: 26 file(s)
- .json: 12 file(s)
- .html: 11 file(s)
- .scss: 11 file(s)
- .csproj: 6 file(s)
- .md: 4 file(s)
- (no ext): 3 file(s)
- .slnx: 1 file(s)
- .http: 1 file(s)
- .ico: 1 file(s)

## Project Structure

```
.gitignore
HANDOFF.md
OrderFlow\OrderFlow.slnx
OrderFlow\README.md
OrderFlow\backend\OrderFlow.Api\OrderFlow.Api.csproj
OrderFlow\backend\OrderFlow.Api\OrderFlow.Api.http
OrderFlow\backend\OrderFlow.Api\Program.cs
OrderFlow\backend\OrderFlow.Api\appsettings.Development.json
OrderFlow\backend\OrderFlow.Api\appsettings.json
OrderFlow\backend\OrderFlow.Api\Contracts\Requests\CreateCustomerRequest.cs
OrderFlow\backend\OrderFlow.Api\Contracts\Requests\CreateOrderRequest.cs
OrderFlow\backend\OrderFlow.Api\Contracts\Requests\CreateProductRequest.cs
OrderFlow\backend\OrderFlow.Api\Contracts\Responses\CustomerResponse.cs
OrderFlow\backend\OrderFlow.Api\Contracts\Responses\OrderResponse.cs
OrderFlow\backend\OrderFlow.Api\Contracts\Responses\ProductResponse.cs
OrderFlow\backend\OrderFlow.Api\Controllers\CustomersController.cs
OrderFlow\backend\OrderFlow.Api\Controllers\OrdersController.cs
OrderFlow\backend\OrderFlow.Api\Controllers\ProductsController.cs
OrderFlow\backend\OrderFlow.Api\Middleware\ExceptionHandlingMiddleware.cs
OrderFlow\backend\OrderFlow.Api\Properties\launchSettings.json
OrderFlow\backend\OrderFlow.Api\Validation\CreateCustomerRequestValidator.cs
OrderFlow\backend\OrderFlow.Api\Validation\CreateOrderRequestValidator.cs
OrderFlow\backend\OrderFlow.Api\Validation\CreateProductRequestValidator.cs
OrderFlow\backend\OrderFlow.Application\ApplicationServiceCollectionExtensions.cs
OrderFlow\backend\OrderFlow.Application\OrderFlow.Application.csproj
OrderFlow\backend\OrderFlow.Application\Contracts\Commands\CreateCustomerCommand.cs
OrderFlow\backend\OrderFlow.Application\Contracts\Commands\CreateOrderCommand.cs
OrderFlow\backend\OrderFlow.Application\Contracts\Commands\CreateProductCommand.cs
OrderFlow\backend\OrderFlow.Application\Contracts\Results\CustomerResult.cs
OrderFlow\backend\OrderFlow.Application\Contracts\Results\OrderResult.cs
OrderFlow\backend\OrderFlow.Application\Contracts\Results\ProductResult.cs
OrderFlow\backend\OrderFlow.Application\Exceptions\BusinessRuleViolationException.cs
OrderFlow\backend\OrderFlow.Application\Exceptions\NotFoundException.cs
OrderFlow\backend\OrderFlow.Application\Interfaces\ICustomerRepository.cs
OrderFlow\backend\OrderFlow.Application\Interfaces\ICustomerService.cs
OrderFlow\backend\OrderFlow.Application\Interfaces\IOrderRepository.cs
OrderFlow\backend\OrderFlow.Application\Interfaces\IOrderService.cs
OrderFlow\backend\OrderFlow.Application\Interfaces\IProductRepository.cs
OrderFlow\backend\OrderFlow.Application\Interfaces\IProductService.cs
OrderFlow\backend\OrderFlow.Application\Services\CustomerService.cs
OrderFlow\backend\OrderFlow.Application\Services\OrderService.cs
OrderFlow\backend\OrderFlow.Application\Services\ProductService.cs
OrderFlow\backend\OrderFlow.Domain\OrderFlow.Domain.csproj
OrderFlow\backend\OrderFlow.Domain\Discounts\AppliedDiscount.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\DiscountContext.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\DiscountResult.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\IDiscountCalculator.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\IDiscountRule.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\Rules\CustomerTierDiscountRule.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\Rules\DiscountCalculator.cs
OrderFlow\backend\OrderFlow.Domain\Discounts\Rules\LargeOrderDiscountRule.cs
OrderFlow\backend\OrderFlow.Domain\Entities\Customer.cs
OrderFlow\backend\OrderFlow.Domain\Entities\Order.cs
OrderFlow\backend\OrderFlow.Domain\Entities\OrderItem.cs
OrderFlow\backend\OrderFlow.Domain\Entities\Product.cs
OrderFlow\backend\OrderFlow.Domain\Enums\CustomerTier.cs
OrderFlow\backend\OrderFlow.Domain\Enums\OrderStatus.cs
OrderFlow\backend\OrderFlow.Domain\Exceptions\DomainException.cs
OrderFlow\backend\OrderFlow.Infrastructure\InfrastructureServiceCollectionExtensions.cs
OrderFlow\backend\OrderFlow.Infrastructure\OrderFlow.Infrastructure.csproj
OrderFlow\backend\OrderFlow.Infrastructure\Persistence\OrderFlowDbContext.cs
OrderFlow\backend\OrderFlow.Infrastructure\Persistence\Configurations\CustomerConfiguration.cs
OrderFlow\backend\OrderFlow.Infrastructure\Persistence\Configurations\OrderConfiguration.cs
OrderFlow\backend\OrderFlow.Infrastructure\Persistence\Configurations\OrderItemConfiguration.cs
OrderFlow\backend\OrderFlow.Infrastructure\Persistence\Configurations\ProductConfiguration.cs
OrderFlow\backend\OrderFlow.Infrastructure\Persistence\Configurations\SeedIds.cs
OrderFlow\backend\OrderFlow.Infrastructure\Repositories\CustomerRepository.cs
OrderFlow\backend\OrderFlow.Infrastructure\Repositories\OrderRepository.cs
OrderFlow\backend\OrderFlow.Infrastructure\Repositories\ProductRepository.cs
OrderFlow\frontend\orderflow-ui\.editorconfig
OrderFlow\frontend\orderflow-ui\.gitignore
OrderFlow\frontend\orderflow-ui\README.md
OrderFlow\frontend\orderflow-ui\angular.json
OrderFlow\frontend\orderflow-ui\package-lock.json
OrderFlow\frontend\orderflow-ui\package.json
OrderFlow\frontend\orderflow-ui\tsconfig.app.json
OrderFlow\frontend\orderflow-ui\tsconfig.json
OrderFlow\frontend\orderflow-ui\tsconfig.spec.json
OrderFlow\frontend\orderflow-ui\.vscode\extensions.json
OrderFlow\frontend\orderflow-ui\.vscode\launch.json
OrderFlow\frontend\orderflow-ui\.vscode\tasks.json
OrderFlow\frontend\orderflow-ui\public\favicon.ico
OrderFlow\frontend\orderflow-ui\src\index.html
OrderFlow\frontend\orderflow-ui\src\main.ts
OrderFlow\frontend\orderflow-ui\src\styles.scss
OrderFlow\frontend\orderflow-ui\src\app\app.component.html
OrderFlow\frontend\orderflow-ui\src\app\app.component.scss
OrderFlow\frontend\orderflow-ui\src\app\app.component.spec.ts
OrderFlow\frontend\orderflow-ui\src\app\app.component.ts
OrderFlow\frontend\orderflow-ui\src\app\app.config.ts
OrderFlow\frontend\orderflow-ui\src\app\app.routes.ts
OrderFlow\frontend\orderflow-ui\src\app\core\models\customer.model.ts
OrderFlow\frontend\orderflow-ui\src\app\core\models\order.model.ts
OrderFlow\frontend\orderflow-ui\src\app\core\models\product.model.ts
OrderFlow\frontend\orderflow-ui\src\app\core\services\customer.service.ts
OrderFlow\frontend\orderflow-ui\src\app\core\services\discount-preview.util.ts
OrderFlow\frontend\orderflow-ui\src\app\core\services\order.service.ts
OrderFlow\frontend\orderflow-ui\src\app\core\services\product.service.ts
OrderFlow\frontend\orderflow-ui\src\app\customers\customer-form-dialog.component.html
OrderFlow\frontend\orderflow-ui\src\app\customers\customer-form-dialog.component.scss
OrderFlow\frontend\orderflow-ui\src\app\customers\customer-form-dialog.component.ts
OrderFlow\frontend\orderflow-ui\src\app\customers\customers.component.html
OrderFlow\frontend\orderflow-ui\src\app\customers\customers.component.scss
OrderFlow\frontend\orderflow-ui\src\app\customers\customers.component.ts
OrderFlow\frontend\orderflow-ui\src\app\dashboard\dashboard.component.html
OrderFlow\frontend\orderflow-ui\src\app\dashboard\dashboard.component.scss
OrderFlow\frontend\orderflow-ui\src\app\dashboard\dashboard.component.ts
OrderFlow\frontend\orderflow-ui\src\app\layout\app-shell.component.html
OrderFlow\frontend\orderflow-ui\src\app\layout\app-shell.component.scss
OrderFlow\frontend\orderflow-ui\src\app\layout\app-shell.component.ts
OrderFlow\frontend\orderflow-ui\src\app\orders\order-create\order-create.component.html
OrderFlow\frontend\orderflow-ui\src\app\orders\order-create\order-create.component.scss
OrderFlow\frontend\orderflow-ui\src\app\orders\order-create\order-create.component.ts
OrderFlow\frontend\orderflow-ui\src\app\orders\order-detail\order-detail.component.html
OrderFlow\frontend\orderflow-ui\src\app\orders\order-detail\order-detail.component.scss
OrderFlow\frontend\orderflow-ui\src\app\orders\order-detail\order-detail.component.ts
OrderFlow\frontend\orderflow-ui\src\app\orders\order-list\order-list.component.html
OrderFlow\frontend\orderflow-ui\src\app\orders\order-list\order-list.component.scss
OrderFlow\frontend\orderflow-ui\src\app\orders\order-list\order-list.component.ts
OrderFlow\frontend\orderflow-ui\src\app\products\product-form-dialog.component.html
OrderFlow\frontend\orderflow-ui\src\app\products\product-form-dialog.component.scss
OrderFlow\frontend\orderflow-ui\src\app\products\product-form-dialog.component.ts
OrderFlow\frontend\orderflow-ui\src\app\products\products.component.html
OrderFlow\frontend\orderflow-ui\src\app\products\products.component.scss
OrderFlow\frontend\orderflow-ui\src\app\products\products.component.ts
OrderFlow\frontend\orderflow-ui\src\app\shared\components\confirm-dialog\confirm-dialog.component.ts
OrderFlow\frontend\orderflow-ui\src\app\shared\components\empty-state\empty-state.component.ts
OrderFlow\frontend\orderflow-ui\src\app\shared\components\tier-chip\tier-chip.component.ts
OrderFlow\frontend\orderflow-ui\src\environments\environment.prod.ts
OrderFlow\frontend\orderflow-ui\src\environments\environment.ts
OrderFlow\specs\001-order-discount\spec.md
OrderFlow\tests\OrderFlow.IntegrationTests\OrderFlow.IntegrationTests.csproj
OrderFlow\tests\OrderFlow.IntegrationTests\OrderFlowWebApplicationFactory.cs
OrderFlow\tests\OrderFlow.IntegrationTests\Api\CustomersApiTests.cs
OrderFlow\tests\OrderFlow.IntegrationTests\Api\OrdersApiTests.cs
OrderFlow\tests\OrderFlow.IntegrationTests\Api\ProductsApiTests.cs
OrderFlow\tests\OrderFlow.UnitTests\OrderFlow.UnitTests.csproj
OrderFlow\tests\OrderFlow.UnitTests\Application\Services\OrderServiceTests.cs
OrderFlow\tests\OrderFlow.UnitTests\Domain\Discounts\CustomerTierDiscountRuleTests.cs
OrderFlow\tests\OrderFlow.UnitTests\Domain\Discounts\DiscountCalculatorTests.cs
OrderFlow\tests\OrderFlow.UnitTests\Domain\Discounts\LargeOrderDiscountRuleTests.cs
```

> Generated in **basic mode** (no LLM configured). Set `LLM_PROVIDER` and the matching API key in `.env` for AI-generated analysis.