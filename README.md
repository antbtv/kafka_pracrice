# Kafka Food Order Microservices

A demo project that shows how to use Apache Kafka with Spring Boot microservices to process food orders.

## Architecture

This project uses a microservices setup with these parts:

- **Producer Service** (Port 8080): REST API that gets food orders and sends them to Kafka
- **Consumer Service** (Port 8081): Listens to Kafka topics and saves orders to H2 database
- **Apache Kafka**: Message broker for async communication
- **Zookeeper**: Helps manage Kafka cluster
- **Kafdrop**: Web UI to manage and watch Kafka
- **H2 Database**: In-memory database to store orders

## Features

- **Async Processing**: Orders are processed without waiting using Kafka messages
- **Microservices Setup**: Services work separately and talk through Kafka
- **Docker Setup**: Complete Docker Compose configuration
- **Data Storage**: Orders are saved in H2 database
- **Monitoring**: Kafdrop web interface to check Kafka topics

## Technology Stack

- **Java 17**
- **Spring Boot 3.5.0**
- **Spring Kafka**
- **Spring Data JPA**
- **H2 Database**
- **Apache Kafka**
- **Docker & Docker Compose**
- **Lombok**
- **Maven**

## Project Structure

```
kafka_practice/
├── docker-compose.yml
├── producer/
│   ├── Dockerfile
│   ├── pom.xml
│   └── src/main/java/com/example/producer/
│       ├── config/Config.java
│       ├── controller/FoodOrderController.java
│       ├── service/FoodOrderService.java
│       ├── model/
│       │   ├── FoodOrder.java
│       │   └── Producer.java
│       └── ProducerApplication.java
└── consumer/
    ├── Dockerfile
    ├── pom.xml
    └── src/main/java/com/example/consumer/
        ├── config/Config.java
        ├── service/FoodOrderService.java
        ├── model/
        │   ├── Consumer.java
        │   └── FoodOrder.java 
        ├── dto/
        |   └── FoodOrderDto.java
        ├── repository/FoodOrderRepository.java
        └── ConsumerApplication.java
```

## Getting Started

### What You Need

- Docker and Docker Compose installed

### Quick Start with Docker

1. **Get the code**
   ```bash
   git clone <repository-url>
   cd kafka_practice/producer
   ```

2. **Start all services**
   ```bash
   docker-compose up -d --build
   ```

3. **Check if services are running**
    - Kafdrop: http://localhost:9000
    - Producer API: http://localhost:8080/actuator/health
    - Consumer API: http://localhost:8081/actuator/health
    - H2 Console: http://localhost:8081/h2-console

## API Usage

### Create Food Order

**Endpoint:** `POST /order`

**Request Body:**
```json
{
  "item": "Pizza",
  "amount": 15.99
}
```

**Response:**
```json
"message sent"
```

## Monitoring & Management

### Kafdrop (Kafka Web UI)
- **URL**: http://localhost:9000
- **What you can do**:
    - See topics and partitions
    - Look at messages
    - Watch consumer groups
    - Manage topics

### H2 Database Console
- **URL**: http://localhost:8081/h2-console
- **Login info**:
    - JDBC URL: `jdbc:h2:mem:testdb`
    - Username: `sa`
    - Password: `password`

### Health Checks
- Producer: http://localhost:8080/actuator/health
- Consumer: http://localhost:8081/actuator/health

## Configuration

### Kafka Topic Settings
- **Topic Name**: `t.food.order`
- **Partitions**: 1
- **Replication Factor**: 1
- **Consumer Group**: `default`

### Service Ports
- **Producer Service**: 8080
- **Consumer Service**: 8081
- **Kafka Broker**: 9092
- **Zookeeper**: 2181
- **Kafdrop**: 9000

## Stopping the Application

```bash
# Stop all services
docker-compose down

# Stop and remove data
docker-compose down -v

# Remove built images
docker-compose down --rmi all
```

## Key Kafka Ideas Shown

- **Topics and Partitions**: How messages are organized and processed in parallel
- **Producers and Consumers**: How to send and receive message patterns
- **Consumer Groups**: How to balance load and handle failures
- **Message Storage**: How Kafka stores messages using logs

## Contacts

If you have questions or need help, contact:

* Email: [antonbut48@gmail.com](mailto:antonbut48@gmail.com)