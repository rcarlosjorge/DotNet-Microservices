# Build a Microservices App with .NET and NextJS

This project is a comprehensive microservices application constructed from scratch using .NET for the backend, incorporating modern architecture patterns and advanced data handling techniques.

## Current Services

- **AuctionService**: Manages all CRUD operations for auctions, connected to PostgreSQL with support for migrations, DTOs, and seed data for proper database initialization.
- **SearchService**: Filters and searches data, using MongoDB to handle complex queries efficiently.

## Message Handling with RabbitMQ

To ensure robust inter-service communication, the system utilizes RabbitMQ for messaging:
- **Message Queueing**: RabbitMQ handles message delivery between services, ensuring that messages are queued and persistently stored until processed.
- **Resilience**: Implements retry mechanisms where messages are retried every 5 seconds in case of service downtime.
- **Error Handling**: `AuctionCreatedFaultConsumer` handles exceptions like `System.ArgumentException`, correcting and reissuing the message to ensure reliability.

## Data Model Validation

To enhance data integrity, the following entities have been introduced:
- `modelBuilder.AddInboxStateEntity();`
- `modelBuilder.AddOutboxMessageEntity();`
- `modelBuilder.AddOutboxStateEntity();`

These additions ensure that messages are correctly managed in scenarios of temporary service unavailability, utilizing inbox and outbox patterns to handle incoming and outgoing communications securely.

## Planned Services

- **BiddingService**: To manage auction bidding processes.
- **NotificationService**: To handle real-time user notifications and communication.

## Technologies Used

- **.NET Core**
- **PostgreSQL**
- **MongoDB**
- **RabbitMQ**
- **Docker**

## Resilience and Secure Connections

The application employs **Polly**, a resilience and transient-fault-handling library, to implement retry policies for HTTP connections between services:
- **Polly Retry Policies**: Configured to manage transient HTTP errors by retrying every 3 seconds until the service is available again, essential for maintaining continuous operation in a distributed environment.

## Installation

To deploy this project, ensure Docker is installed on your machine. Follow these steps to get started:

```bash
# Clone the repository
git clone https://github.com/rcarlosjorge/DotNet-NextJS-Microservices.git
# Navigate to each service directory and perform necessary configurations or initialization tasks.
dotnet watch
# Return to the root directory
cd ..
# Start the Docker containers from the root directory.
docker compose up -d
