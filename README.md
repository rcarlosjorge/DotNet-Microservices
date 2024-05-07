# Build a Microservices App with .NET and NextJS

This project is a comprehensive guide to constructing a microservices application from scratch, utilizing .NET for the backend. This setup integrates modern architectural patterns and advanced data management techniques to create a robust and scalable application.

## Integrating Duende IdentityServer

The application leverages **Duende IdentityServer** for robust authentication and authorization capabilities:
- **Adding Duende IdentityServer**: Integrated into the ASP.NET Core application to manage identity services.
- **Configuring IdentityServer**: Setup to issue tokens for various clients and secure web applications and APIs.
- **EntityFramework & ASP.NET Identity**: Enhanced with support for configurations based on EntityFramework and integration with ASP.NET Identity for comprehensive user management and authentication.

## Current Services

- **AuctionService**: Manages CRUD operations for auctions, connected to PostgreSQL. It includes features like migrations, DTOs, and seed data for proper database initialization.
- **SearchService**: Utilizes MongoDB to efficiently handle complex queries for filtering and searching data.
- **IdentityService**: Dedicated to managing user identities and access controls. This service interfaces with Duende IdentityServer and ASP.NET Identity to offer a seamless and secure user experience.

## Message Handling with RabbitMQ

The system uses RabbitMQ to facilitate robust inter-service communication:
- **Message Queueing**: Ensures reliable delivery and storage of messages until they are processed.
- **Resilience**: Features retry mechanisms where messages are retried every 5 seconds in case of service downtime.
- **Error Handling**: Includes an `AuctionCreatedFaultConsumer` to manage exceptions such as `System.ArgumentException`, ensuring message reliability and correctness.

## Data Model Validation

The following entities enhance data integrity and manage communications securely:
- `modelBuilder.AddInboxStateEntity();`
- `modelBuilder.AddOutboxMessageEntity();`
- `modelBuilder.AddOutboxStateEntity();`

These entities help handle scenarios of temporary service unavailability by managing incoming and outgoing messages through inbox and outbox patterns.

## Planned Services

- **BiddingService**: Will manage the auction bidding processes.
- **NotificationService**: Aimed at handling real-time user notifications and communication.

## Technologies Used

- **.NET Core**
- **PostgreSQL**
- **MongoDB**
- **RabbitMQ**
- **Docker**
- - **DUENDE**

## Resilience and Secure Connections

Incorporating **Polly**, a library for resilience and handling transient faults, the application:
- **Polly Retry Policies**: Configures transient HTTP error management by retrying connections every 3 seconds, vital for ensuring uninterrupted service in a distributed system.

## Installation

Follow these steps to deploy the project using Docker:
```bash
# Clone the repository
git clone https://github.com/rcarlosjorge/DotNet-NextJS-Microservices.git
# Navigate to each service directory for necessary configurations or initialization tasks.
dotnet watch
# Return to the root directory
cd ..
# Start the Docker containers from the root directory.
docker compose up -d
