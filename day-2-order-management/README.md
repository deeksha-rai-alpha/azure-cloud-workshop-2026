# Day 2 - Order management (shopping cart, admin, blob function)

See the [root README](../README.md) for the architecture diagram, local setup, configuration and known limitations.

| Project | Type | Role |
|---|---|---|
| `MyShoppingCart` | ASP.NET Core MVC, .NET 10 | Customer storefront; saves confirmed orders to `dbo.Orders` |
| `MyCartAdmin` | ASP.NET Core MVC, .NET 10 | Admin order list and details; sends orders to Blob Storage as JSON; tracks status in `dbo.OrderDispatchState` |
| `OrderBlobLogger` | Azure Functions v4, .NET isolated | Blob trigger that logs blob names (see the limitations in the root README) |

Entry points: `Program.cs` in each project.
SQL scripts: `MyShoppingCart/Database/CreateOrders.sql`, then `MyCartAdmin/Database/CreateOrderDispatchState.sql`.
Settings shape: `appsettings.sample.json` (web apps) and `local.settings.sample.json` (function).
