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
- **GatewayService**: Acts as the primary point of entry for all client requests, routing them to the appropriate services through **YARP (Yet Another Reverse Proxy)**. This simplifies the architecture, enhances security, and facilitates load balancing by serving as a dynamic reverse proxy.
- **BiddingService**: Manages the auction bidding processes, ensuring smooth and efficient operations.
- **NotificationService**: Handles real-time user notifications and communication using **SignalR** for real-time web functionalities.

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

## GRPC and Protobuf Integration

The project utilizes **gRPC** and **Protobuf** for efficient and high-performance communication between microservices:
- **gRPC**: Provides a robust RPC framework for service-to-service communication.
- **Protobuf**: Used for serializing structured data, ensuring fast and efficient communication between services.

## Real-Time Communication with SignalR

The **NotificationService** leverages **SignalR** to enable real-time communication:
- **SignalR Integration**: Allows server-side code to push content to connected clients instantly.
- **Real-Time Updates**: Ensures that users receive immediate notifications and updates, enhancing the user experience.

## SSL Certificates with mkcert

To ensure secure communication in local development, **mkcert** is used to generate SSL certificates:
- **SSL Configuration**: mkcert allows for easy creation and management of local SSL certificates, enhancing security during development.

## Technologies Used

- **.NET Core**
- **PostgreSQL**
- **MongoDB**
- **RabbitMQ**
- **Docker**
- **YARP**
- **SignalR**
- **gRPC**
- **Protobuf**
- **mkcert**

## Resilience and Secure Connections

Incorporating **Polly**, a library for resilience and handling transient faults, the application:
- **Polly Retry Policies**: Configures transient HTTP error management by retrying connections every 3 seconds, vital for ensuring uninterrupted service in a distributed system.

## Simplified Deployment with Docker

The application has been containerized using Docker, allowing for seamless deployment and management:
- **Dockerized Services**: Each service now has its own Dockerfile, simplifying the build and deployment process.
- **One-Step Deployment**: Launch all services with a single command `docker compose up -d`, which automatically sets up the entire infrastructure.

### Docker Network Configuration

To ensure seamless communication between the backend and frontend services, a custom Docker network is created. This network allows all services to communicate with each other efficiently. Additionally, some services are assigned static IP addresses to simplify their connection and ensure consistent network configurations.

Here is an overview of the steps taken to configure the network:

- **Creating the Network**: A Docker network named `my_microservices_network` is created to connect all services.
- **Assigning Static IPs**: Certain services are given static IP addresses to make it easier to connect and manage them within the network.

This setup ensures that all microservices can communicate with each other seamlessly, providing a robust and reliable infrastructure for the application.

## Installation

To deploy this project, ensure Docker is installed on your machine. Follow these steps to build and start all services:

1. Create a Docker network to facilitate communication between the backend and frontend services:
   ```bash
   docker network create my_microservices_network
2. Build and start all services with the following commands:
 ```bash
docker compose build 
docker compose up -d
