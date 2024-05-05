# Build a Microservices App with .NET and NextJS

This project is a microservices application built from scratch using .NET for the backend. The backend is initially designed around two main services: `AuctionService` and `SearchService`, implementing modern microservices architecture patterns and advanced data handling techniques. Additional services are planned and will be integrated into the architecture to extend the application's functionality.

## Current Services

- **AuctionService**: Handles all CRUD operations for auctions. It is connected to PostgreSQL, featuring migrations, DTOs, and seed data to ensure the database is properly initialized.
- **SearchService**: Responsible for filtering and searching data, leveraging MongoDB to handle complex queries efficiently.

## Planned Services

- **PaymentService**: Will handle all transactional operations.
- **NotificationService**: To manage real-time user notifications and communications.

## Resilience and Secure Connections

The system uses **Polly**, a resiliency and transcendence library, to manage retry policies on HTTP connections between services. This ensures that temporary failures in one service do not affect the availability of the other:

- **Polly Retry Policies:** Configured to handle transient HTTP errors and continue trying every 3 seconds until the service is available again, which is critical for continuous operation in a microservices environment.

## Technologies Used

- **.NET Core**
- **PostgreSQL**
- **MongoDB**
- **Docker**

## Installation

To run this project, you will need Docker installed on your machine. Follow these steps to start the services:

```bash
# Clone the repository
git clone https://github.com/rcarlosjorge/DotNet-NextJS-Microservices.git
# Before starting the Docker containers, you must access each service and perform the necessary configuration or initialization tasks.
dotnet watch
# Returns to the root folder
cd .. 
# Once each service is configured, start the Docker containers from the root folder.
docker compose up -d
