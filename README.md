# AutoSentry – Vehicle Compliance Monitoring Platform

AutoSentry is a vehicle compliance monitoring platform designed to help vehicle owners stay ahead of critical document expiration deadlines. The system tracks compliance-related vehicle documents, continuously monitors upcoming expirations, and proactively notifies users before deadlines are reached.

Built using a microservices architecture, AutoSentry combines Spring Boot, Apache Kafka, PostgreSQL, Angular, Docker, Prometheus, and Grafana to provide a scalable, observable, and event-driven compliance tracking solution.

---

## Problem Statement

Vehicle owners are often required to keep multiple compliance-related documents valid throughout a vehicle's lifecycle. Missing an expiry date can lead to penalties, operational disruptions, and legal issues.

Managing these deadlines manually becomes increasingly difficult as the number of vehicles grows.

AutoSentry addresses this challenge by:

* Tracking vehicle compliance information
* Monitoring approaching expiry dates
* Automatically generating reminder events
* Delivering proactive notifications before deadlines are reached

---

## Key Features

### Authentication & User Management

* User Registration
* User Login
* JWT-based Authentication
* Secure Password Hashing
* User Profile Management
* Notification Preference Management

### Vehicle Management

* Vehicle Registration
* Vehicle Ownership Tracking
* Vehicle Lookup and Retrieval
* Compliance Metadata Storage

### Compliance Monitoring

* Insurance Expiry Tracking
* Pollution Certificate Expiry Tracking
* Automated Expiry Detection
* Scheduled Compliance Monitoring

### Notification System

* Event-Driven Notification Pipeline
* Kafka-Based Messaging
* Automated Email Notifications
* User Notification Preferences

### Infrastructure & Operations

* API Gateway Routing
* Service Discovery with Eureka
* Containerized Deployment
* Docker Compose Orchestration

### Observability

* Spring Boot Actuator
* Prometheus Metrics Collection
* Grafana Dashboards
* Health Monitoring

---

## System Architecture

The platform follows a distributed microservices architecture.

```text
                        +--------------------+
                        |  Angular Frontend  |
                        +---------+----------+
                                  |
                                  v
                        +--------------------+
                        |    API Gateway     |
                        +---------+----------+
                                  |
           +----------------------+----------------------+
           |                                             |
           v                                             v
+--------------------+                         +--------------------+
|    User Service    |                         |  Vehicle Service   |
+---------+----------+                         +---------+----------+
          |                                              |
          |                                              | Kafka Producer
          v                                              v
   +--------------+                          +------------------------+
   |  PostgreSQL  |                          |  vehicle-expiry-topic  |
   +--------------+                          +-----------+------------+
                                                         |
                                                         | Kafka Consumer
                                                         v
                                             +------------------------+
                                             |  Notification Service  |
                                             +-----------+------------+
                                                         |
                                                         v
                                                  [Email Alerts]

=============================================================================
                          INFRASTRUCTURE SERVICES
=============================================================================
+---------------+    +--------------+    +--------------+    +--------------+
| Eureka Server |    | Apache Kafka |    |  Prometheus  |    |   Grafana    |
+---------------+    +--------------+    +--------------+    +--------------+

---

## Event-Driven Workflow

The notification pipeline is built using Apache Kafka to decouple business logic from notification delivery.

1. **Vehicle Registration**: A user registers a vehicle through the platform.
2. **Compliance Monitoring**: The Vehicle Service continuously evaluates document expiry dates.
3. **Event Generation**: When a monitored document approaches expiry, the Vehicle Service publishes a compliance event to Kafka.
4. **Event Consumption**: The Notification Service consumes the event asynchronously.
5. **Notification Delivery**: An email notification is generated and delivered to the vehicle owner.

This architecture enables services to evolve independently while maintaining loose coupling.

---

## Technology Stack

### Frontend

* Angular
* Angular Signals
* RxJS
* Tailwind CSS
* Angular HttpClient
* Route Guards
* HTTP Interceptors

### Backend

* Java 21
* Spring Boot
* Spring MVC
* Spring Security
* Spring Data JPA
* Spring Cloud

### Authentication

* JWT Authentication
* Password Encryption

### Database

* PostgreSQL

### Messaging

* Apache Kafka
* Spring Kafka

### Service Discovery

* Netflix Eureka

### Infrastructure

* Docker
* Docker Compose

### Monitoring

* Prometheus
* Grafana
* Spring Boot Actuator

### Email

* Spring Mail
* MailHog (Development Environment)

---

## Repository Structure

AutoSentry is organized as a collection of focused repositories.

| Component | Repository | Description |
|------------|------------|------------|
| Frontend | [autosentry-client](https://github.com/SujithKumar-Codes/autosentry-client) | Angular Frontend |
| API Gateway | [autosentry-api-gateway](https://github.com/SujithKumar-Codes/autosentry-api-gateway) | Gateway Layer |
| Eureka Server | [autosentry-eureka-server](https://github.com/SujithKumar-Codes/autosentry-eureka-server) | Service Discovery |
| User Service | [autosentry-user-service](https://github.com/SujithKumar-Codes/autosentry-user-service) | Authentication & User Management |
| Vehicle Service | [autosentry-vehicle](https://github.com/ShawnSaldanha/autosentry-vehicle) | Compliance Monitoring & Kafka Producer |
| Notification Service | [autosentry-notification-service](https://github.com/SujithKumar-Codes/autosentry-notification-service) | Notification Processing |
| Infrastructure | [autosentry-infrastructure](https://github.com/ShawnSaldanha/autosentry-infrastructure) | Docker, Kafka, Monitoring & Infrastructure |

---

## Service Responsibilities

### User Service

Responsible for:

* Registration
* Authentication
* JWT Generation
* User Profile Management
* Notification Preferences

### Vehicle Service

Responsible for:

* Vehicle Registration
* Compliance Tracking
* Expiry Monitoring
* Kafka Event Publishing

### Notification Service

Responsible for:

* Kafka Event Consumption
* Notification Processing
* Email Delivery

### API Gateway

Responsible for:

* Centralized Request Routing
* Service Access Abstraction

### Eureka Server

Responsible for:

* Service Registration
* Service Discovery

---

## Monitoring & Observability

Every core service exposes operational metrics using Spring Boot Actuator.
Prometheus continuously collects metrics from:

* API Gateway
* User Service
* Vehicle Service
* Notification Service
* Eureka Server

Grafana provides centralized dashboards for:

* Application Health
* JVM Metrics
* Request Monitoring
* Resource Utilization
* Service Availability

---

## Development Infrastructure

The platform can be executed locally using Docker Compose.
Infrastructure components include:

* PostgreSQL
* Apache Kafka
* Kafka UI
* MailHog
* Prometheus
* Grafana
* Eureka Server
* API Gateway
* User Service
* Vehicle Service
* Notification Service

---

## Current Compliance Modules

Currently supported:

* Insurance Expiry Monitoring
* Pollution Certificate Expiry Monitoring

---

## Product Roadmap

Planned future enhancements include:

* Fitness Certificate Monitoring
* Road Tax Expiry Monitoring
* SMS Notifications
* WhatsApp Notifications
* Mobile Application
* Fleet Management Support
* Role-Based Access Control
* Centralized Logging
* CI/CD Pipelines
* Kubernetes Deployment
* Distributed Tracing
* Production Email Providers

---

## Team

AutoSentry was developed collaboratively using a Git-based branching workflow.
Contributors participated in the design, implementation, integration, testing, and debugging of the microservices ecosystem, including backend services, frontend development, infrastructure configuration, and system integration.

---

## Project Status

**Active Development**
AutoSentry is a fully functional vehicle compliance monitoring platform with all core features implemented and tested.
The project remains under active development as additional compliance modules, notification channels, infrastructure improvements, and SaaS-oriented capabilities are introduced.

---

## License

This project is currently intended for educational, portfolio, and demonstration purposes.