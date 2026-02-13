# Microservices Architecture Project

A Spring Boot microservices architecture featuring service discovery and API gateway pattern.

## 🏗️ Architecture Overview

This project implements a microservices ecosystem with the following components:

- **Eureka Server**: Service discovery and registration
- **API Gateway**: Central entry point for routing and load balancing

## 📦 Services

### Eureka Server
Service registry that enables microservices to discover and communicate with each other.

- **Port**: 8761
- **Location**: `/eureka`
- **Dashboard**: http://localhost:8761

### API Gateway
Routes incoming requests to appropriate microservices with built-in load balancing.

- **Port**: 8093
- **Location**: `/api-gateway`
- **Features**:
  - Dynamic service discovery routing
  - CORS configuration for frontend (localhost:4200)
  - OAuth2 JWT authentication with Keycloak
  - Load balancing with Ribbon

#### Configured Routes
- Customer Service: `/customers/**` → `lb://CUSTOMER-SERVICE`
- Reclamation Service: `/reclamations/**` → `http://localhost:8083`

## 🚀 Getting Started

### Prerequisites

- Java 17 or higher
- Maven 3.6+
- Keycloak server running on port 9098 (for OAuth2)

### Running the Services

1. **Start Eureka Server**
   ```bash
   cd eureka
   mvnw spring-boot:run
   ```
   Wait for Eureka to fully start (check http://localhost:8761)

2. **Start API Gateway**
   ```bash
   cd api-gateway
   mvnw spring-boot:run
   ```

### Verification

- Eureka Dashboard: http://localhost:8761
- Gateway Management Endpoints: http://localhost:8093/actuator/gateway/routes

## 🔧 Configuration

### Eureka Server
```properties
server.port=8761
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

### API Gateway
```properties
server.port=8093
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
spring.cloud.gateway.discovery.locator.enabled=true
```

## 🔐 Security

The API Gateway is configured with:
- **OAuth2 Resource Server** with JWT tokens
- **Keycloak Integration**: `http://localhost:9098/realms/micro-services`
- **CORS**: Configured for Angular frontend on `http://localhost:4200`

## 📋 Service Registration

New microservices automatically register with Eureka by including:
```properties
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
eureka.client.register-with-eureka=true
eureka.client.fetch-registry=true
```

## 🐳 Docker Support

API Gateway includes a Dockerfile for containerization:
```bash
cd api-gateway
docker build -t api-gateway .
```

## 📊 Monitoring

- Gateway routes are exposed via Spring Boot Actuator
- Access endpoint: `/actuator/gateway`
- Debug logging enabled for gateway and reactor netty

## 🛠️ Tech Stack

- Spring Boot
- Spring Cloud Netflix Eureka
- Spring Cloud Gateway
- Spring Security OAuth2
- Keycloak

## 📝 Future Microservices

This architecture is designed to support additional microservices:
- Customer Service (referenced in routes)
- Reclamation Service (configured)
- Additional business services can be added seamlessly

## 🤝 Contributing

When adding new microservices:
1. Configure Eureka client in `application.properties`
2. Add routing rules in API Gateway if needed
3. Register service name in Eureka for discovery

## 📄 License

[Add your license here]
