# Gringotts Financial - Project Cheat Sheet

This document provides a quick reference guide to the Gringotts Financial project architecture, patterns, and important elements to know when working with the codebase.

## Architecture Overview

### Key Directories
- `/Controllers` - MVC Controllers handling HTTP requests
- `/Models` - Data models and view models 
- `/Views` - Razor views for the UI
- `/Scripts` - JavaScript files for client-side functionality
- `/Content` - CSS, images, and other static content
- `/App_Start` - Configuration files for the application startup
- `/Data` - Entity Framework related files, migrations, and data access
- `/Services` - Business logic services

### Important Files
- `Global.asax` - Application startup configuration
- `Web.config` - Application settings and configuration
- `Gringotts.sln` - Main solution file
- `packages.config` - NuGet package dependencies

## Project Structure

### Solution Organization
```
Gringotts.sln
├── Gringotts.Web (Main Web Application)
│   ├── Controllers/
│   ├── Models/
│   ├── Views/
│   ├── Scripts/
│   ├── Content/
│   ├── App_Start/
│   └── Global.asax
├── Gringotts.Core (Business Logic Layer)
│   ├── Commands/
│   ├── Queries/
│   ├── Handlers/
│   ├── Services/
│   ├── Interfaces/
│   └── Models/
├── Gringotts.Data (Data Access Layer)
│   ├── Repositories/
│   ├── Context/
│   ├── Mappings/
│   └── Migrations/
├── Gringotts.Common (Shared Utilities)
│   ├── Extensions/
│   ├── Helpers/
│   ├── Logging/
│   └── Security/
└── Gringotts.Tests (Test Projects)
    ├── Gringotts.UnitTests/
    ├── Gringotts.IntegrationTests/
    └── Gringotts.UITests/
```

### Key Project Responsibilities

- **Gringotts.Web**: User interface, controllers, and view models
- **Gringotts.Core**: Business logic, domain models, commands, queries, and handlers
- **Gringotts.Data**: Data access, repositories, and database context
- **Gringotts.Common**: Shared utilities, helpers, and extensions
- **Gringotts.Tests**: Test projects for various testing levels

### Dependency Flow
```
Gringotts.Web → Gringotts.Core → Gringotts.Data
         ↓            ↓              ↓
         └────→ Gringotts.Common ←───┘
```

## Platform & Dependencies

### Platform Information
- **Framework**: .NET Framework 4.7.2
- **IDE**: Visual Studio 2019/2022
- **Database**: SQL Server 2019
- **Deployment Target**: IIS 10.0 on Windows Server 2019

### NuGet Packages

| Package Name | Version | Purpose | Status |
|--------------|---------|---------|--------|
| [EntityFramework](https://www.nuget.org/packages/EntityFramework/6.4.4) | 6.4.4 | ORM for data access | Maintained |
| [Autofac](https://www.nuget.org/packages/Autofac/6.3.0) | 6.3.0 | Dependency injection container | Maintained |
| [Autofac.Mvc5](https://www.nuget.org/packages/Autofac.Mvc5/6.0.0) | 6.0.0 | Autofac integration with MVC | Maintained |
| [MediatR](https://www.nuget.org/packages/MediatR/10.0.1) | 10.0.1 | Implementation of mediator pattern | Maintained |
| [NLog](https://www.nuget.org/packages/NLog/4.7.15) | 4.7.15 | Logging framework | Maintained |
| [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/13.0.1) | 13.0.1 | JSON serialization/deserialization | Maintained |
| [AutoMapper](https://www.nuget.org/packages/AutoMapper/10.1.1) | 10.1.1 | Object-to-object mapping | Maintained |
| [FluentValidation](https://www.nuget.org/packages/FluentValidation/10.3.6) | 10.3.6 | Validation library | Maintained |
| [Dapper](https://www.nuget.org/packages/Dapper/2.0.123) | 2.0.123 | Micro-ORM for performance-critical queries | Maintained |
| [ImageResizer](https://www.nuget.org/packages/ImageResizer/4.2.8) | 4.2.8 | Image processing library | ⚠️ [Not actively maintained](https://www.nuget.org/packages/ImageResizer/) |
| [Bootstrap](https://www.nuget.org/packages/bootstrap/5.1.3) | 5.1.3 | Frontend CSS framework | Maintained |
| [jQuery](https://www.nuget.org/packages/jQuery/3.6.0) | 3.6.0 | JavaScript library | Maintained |
| [lodash](https://www.nuget.org/packages/lodash/4.17.21) | 4.17.21 | JavaScript utility library | Maintained |
| [mustache.js](https://www.nuget.org/packages/mustache.js/4.2.0) | 4.2.0 | Client-side templating | Maintained |
| [FontAwesome](https://www.nuget.org/packages/FontAwesome/5.15.4) | 5.15.4 | Icon library | Maintained |
| [Glimpse](https://www.nuget.org/packages/Glimpse/1.8.6) | 1.8.6 | Diagnostics and debugging | ⚠️ [Deprecated](https://www.nuget.org/packages/Glimpse/) - Last updated in 2015 |
| [xUnit](https://www.nuget.org/packages/xunit/2.4.1) | 2.4.1 | Unit testing framework | Maintained |
| [Moq](https://www.nuget.org/packages/Moq/4.17.2) | 4.17.2 | Mocking library for tests | Maintained |
| [Selenium.WebDriver](https://www.nuget.org/packages/Selenium.WebDriver/4.1.0) | 4.1.0 | Browser automation for UI tests | ⚠️ [Security advisory](https://github.com/advisories/GHSA-jc7j-rp32-v65q) - Vulnerable to command injection |
| [AspNet.Security.ActiveDirectory](https://www.nuget.org/packages/AspNet.Security.ActiveDirectory/6.0.0) | 6.0.0 | AD authentication integration | ⚠️ Obsolete - Use Microsoft.Identity.Web instead |

### Packages Requiring Updates

| Package | Issue | Recommended Update |
|---------|-------|-------------------|
| Glimpse | Deprecated, no longer maintained | Consider migrating to [Application Insights](https://www.nuget.org/packages/Microsoft.ApplicationInsights.AspNetCore/) |
| ImageResizer | Not actively maintained | Consider [ImageSharp](https://www.nuget.org/packages/SixLabors.ImageSharp/) |
| Selenium.WebDriver | Security vulnerability CVE-2023-2975 | Update to version 4.10.0 or later |
| AspNet.Security.ActiveDirectory | Obsolete | Migrate to [Microsoft.Identity.Web](https://www.nuget.org/packages/Microsoft.Identity.Web/) |

## Key Components & Patterns

### Architectural Patterns
- **MVC (Model-View-Controller)** - The application follows ASP.NET MVC pattern
- **Command/Query Separation (CQRS)** - Separates read operations (Queries) from write operations (Commands)
- **Dependency Injection** - Uses Autofac for service registration and component wiring
- **Repository Pattern** - For data access abstraction via Entity Framework
- **Mediator Pattern** - Uses MediatR for processing Commands, Queries & Notifications

### Multitenancy
The application supports multiple tenants (organizations) within a single deployment. Each tenant has isolated data while sharing the application infrastructure.

## Common Types

### Data and Domain Types
- **Account** - Financial accounts managed in the system
- **Client** - End-users or customers of the financial services
- **Organization** - Tenant entities in the multi-tenant architecture
- **Vendor** - External service providers or partners
- **Transaction** - Financial transactions recorded in the system

### Application Framework Types
- **Controllers** - MVC controllers (AccountController, ClientController, etc.)
- **ViewModels** - Data transfer objects for views (AccountViewModel, ClientViewModel, etc.)
- **Commands** - Write operations (CreateAccountCommand, UpdateClientCommand, etc.)
- **Queries** - Read operations (GetAccountQuery, ListClientsQuery, etc.)
- **CommandHandlers/QueryHandlers** - Process commands and queries via MediatR
- **Repositories** - Data access abstraction (AccountRepository, ClientRepository, etc.)
- **Services** - Business logic (AccountService, ClientService, etc.)
- **DbContext** - Entity Framework contexts for data access

### Utility Types
- **Logger** - Logging interface and implementations
- **TenantContext** - Contains tenant-specific information and state
- **ImageProcessor** - Handling image processing operations
- **AuthorizationHandler** - Enforcing permission-based access controls

## API & Data Flow

### Client-Server Communication
- Primary communication happens through standard MVC controller actions
- AJAX calls for dynamic data updates using jQuery
- Client-side templates rendered with mustache.js

### Data Flow
1. User request → Controller action
2. Controller uses MediatR to dispatch Commands/Queries
3. Command/Query handlers interact with repositories
4. Repositories interact with Entity Framework contexts
5. Results flow back up the chain to the views

## Reusable Utilities & Helpers

### Logging
- NLog is used for application logging
- Use the injected logger instances rather than creating new ones
- See `docs/logging.md` for logging best practices

### UI Components
- Bootstrap for layout and UI components
- FontAwesome for icons
- jQuery for DOM manipulation
- lodash for JavaScript utilities

### Image Processing
- ImageResizer for manipulating profile images and other uploaded content

### Diagnostics
- Glimpse provides real-time diagnostics and insights
- See `docs/diagnostics.md` for details on monitoring and debugging

### Authentication & Authorization
- The application has dependencies on Active Directory for authentication
- Authorization is likely handled through role-based permissions

## Development Workflow

### Getting Started
1. Clone the repository: `git clone https://github.com/NotMyself/Gringotts.git`
2. Open `Gringotts.sln` in Visual Studio
3. Run `Update-Database` in Package Manager Console
4. Press F5 to start the application

### Key Features
- Accounts management
- Client management
- Organization management
- Vendor management
- Dashboard for overview of financial data

### Documentation
See the following documentation files for more details:
- [Logging](../docs/logging.md)
- [Data Access](../docs/dataaccess.md)
- [Diagnostics](../docs/diagnostics.md)
- [Multitenancy](../docs/multitenancy.md) 
- [Dependency Injection](../docs/dependencyinjection.md)
- [Command/Query Separation](../docs/commandqueryseperation.md)

## Naming Conventions

### C# Naming Conventions

#### Database Naming Conventions
- **Primary Keys**: Automatically suffixed with the entity name + "Id" using `PrimaryKeyNamingConvention` class
  ```csharp
  // Example: For an entity "Client", the primary key becomes "ClientId"
  Properties()
      .Where(p => p.Name == "Id")
      .Configure(p => p.IsKey().HasColumnName(p.ClrPropertyInfo.ReflectedType.Name + "Id"));
  ```
- **Foreign Keys**: Normalized using `ForeignKeyNamingConvention` class to follow a consistent pattern
  ```csharp
  // Example: NavigationPropertyName + TargetKey 
  // e.g., "ClientId" instead of "Client_Id"
  ```

#### Class Naming Conventions
- **Controllers**: Suffix with "Controller" (e.g., `AccountController`, `ClientController`)
- **Repositories**: Suffix with "Repository" (e.g., `ClientRepository`, `AccountRepository`)
- **DbContext**: Uses `ApplicationDbContext` and specialized variants like `InterceptingApplicationDbContext`
- **Interceptors**: Suffix with "Interceptor" (e.g., `AuditChangeInterceptor`, `TenantOrganizationInterceptor`)
- **Entity Configurations**: Suffix with "Configuration" (e.g., `AccountConfiguration`, `ResidencyConfiguration`)
- **CQRS Classes**:
  - Commands: Suffix with "Command" (e.g., `CreateAccountCommand`)
  - Queries: Suffix with "Query" (e.g., `GetAccountQuery`)
  - Handlers: Suffix with "Handler" (e.g., `CreateAccountCommandHandler`)

#### Interface Naming Conventions
- **Interfaces**: Prefix with "I" (e.g., `ISearch<T>`, `IUnitOfWork`, `IInterceptor`)
- **Behavior Interfaces**: Use descriptive "I-Am" or "I-Can" naming (e.g., `IAmAuditable`, `IBelongToOrganization`)

#### Module Naming Conventions
- **Autofac Modules**: Suffix with "Module" (e.g., `MvcModule`, `DataModule`, `InfrastructureModule`)

### JavaScript Naming Conventions

#### Library Utility Functions
- **Function-Based Utilities**: Use camelCase for function names
  ```javascript
  // Example from typeahead.bundle.js
  isUndefined: function(obj) {
      return typeof obj === "undefined";
  },
  toStr: function toStr(s) {
      return _.isUndefined(s) || s === null ? "" : s + "";
  }
  ```

#### Variable Naming
- **jQuery Objects**: Often prefixed with `$` 
  ```javascript
  var $input = $(this);
  ```
- **Constructor Functions**: Use PascalCase (e.g., `Animation`, `Tween`)
- **Private or Internal Variables**: Use camelCase, sometimes with underscore prefix for truly private variables

#### Object Property Naming
- **JavaScript Objects**: Use camelCase for properties and methods
  ```javascript
  // Example from jquery.serializeToJSON.js
  settings: {
      parseFloat: {
          condition: "...",
          getInputValue: function($input) { /* ... */ },
          nanToZero: true
      }
  }
  ```

#### DOM-Related Conventions
- **Data Attributes**: Use kebab-case with `data-` prefix in HTML, accessed as camelCase in JavaScript
  ```javascript
  // HTML: data-input-type="currency"
  // JS: $(element).data('inputType')
  ```

#### jQuery Plugin Conventions
- **Plugin Names**: Use camelCase, often with namespace using dot notation
  ```javascript
  // Example: $.fn.serializeToJSON
  $.fn.serializeToJSON = function(options) { /* ... */ };
  ```

### General Conventions

- **Feature/Module Organization**: Folders are organized by feature rather than by type
- **Multi-Tenant Awareness**: Classes that participate in multi-tenancy implement `IBelongToOrganization`
- **Auditable Entities**: Classes that track creation/modification implement `IAmAuditable`
