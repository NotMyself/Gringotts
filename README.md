# Gringotts Financial

Welcome to the Gringotts Financial application, a comprehensive financial management platform built on ASP.NET MVC.

## Overview

Gringotts Financial is a multi-tenant financial management system designed to help organizations manage accounts, clients, vendors, and financial transactions through a secure and user-friendly interface.

## Key Features

- **Account Management**: Create and manage various types of financial accounts
- **Client Management**: Track client information and relationships
- **Organization Management**: Support for multi-tenant architecture
- **Vendor Management**: Maintain vendor relationships and transactions
- **Financial Dashboard**: Get a quick overview of financial status and key metrics

## Technology Stack

- **Framework**: .NET Framework 4.7.2
- **Architecture**: ASP.NET MVC with CQRS pattern
- **ORM**: Entity Framework 6.4.4
- **Dependency Injection**: Autofac 6.3.0
- **Database**: SQL Server 2019
- **UI**: Bootstrap, jQuery, FontAwesome
- **Diagnostics**: Glimpse, NLog

## Getting Started

1. Clone the repository: `git clone https://github.com/NotMyself/Gringotts.git`
2. Open `Gringotts.sln` in Visual Studio
3. Run `Update-Database` in Package Manager Console
4. Press F5 to start the application

## Project Structure

The application follows a layered architecture with separation of concerns:

- **Gringotts.Web**: User interface, controllers, and view models
- **Gringotts.Core**: Business logic, domain models, commands, queries, and handlers
- **Gringotts.Data**: Data access, repositories, and database context
- **Gringotts.Common**: Shared utilities and helpers

## Documentation

For detailed documentation about the project architecture and implementation patterns, see the following:

- [Project Cheat Sheet](CHEAT_SHEET.md) - Quick reference guide for the project
- [Command/Query Separation](docs/commandqueryseperation.md) - How CQRS is implemented
- [Data Access](docs/dataaccess.md) - Data access patterns and repositories
- [Diagnostics](docs/diagnostics.md) - Monitoring and debugging capabilities
- [Prompts](prompts.md) - Documentation of the conversation that generated these docs

## Architecture

Gringotts implements several architectural patterns:

- **MVC (Model-View-Controller)** - The application follows ASP.NET MVC pattern
- **Command/Query Separation (CQRS)** - Separates read operations from write operations
- **Dependency Injection** - Uses Autofac for service registration
- **Repository Pattern** - For data access abstraction via Entity Framework
- **Mediator Pattern** - Uses MediatR for processing Commands, Queries & Notifications

## Multitenancy

The application supports multiple tenants (organizations) within a single deployment. Each tenant has isolated data while sharing the application infrastructure.

## License

[MIT License](LICENSE)
