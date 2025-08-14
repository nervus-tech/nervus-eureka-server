# Nervus Eureka Server

[![Build Status](https://github.com/nervus-tech/nervus-eureka-server/workflows/CI/badge.svg)](https://github.com/nervus-tech/nervus-eureka-server/actions)
[![Docker Image](https://img.shields.io/badge/docker-ghcr.io%2Fnervus--tech%2Fnervus--eureka--server-blue)](https://ghcr.io/nervus-tech/nervus-eureka-server)

## 📋 Overview

The Nervus Eureka Server is a **Service Discovery** component built with Spring Boot that enables microservices to register themselves and discover other services in the Nervus.tech ecosystem. It's based on Netflix Eureka and provides a robust, scalable service registry.

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Microservice  │    │  Eureka Server   │    │   Microservice  │
│   (Client)      │◄──►│   (Registry)     │◄──►│   (Client)      │
└─────────────────┘    └──────────────────┘    └─────────────────┘
         │                       │                       │
         │              ┌──────────────────┐             │
         └──────────────►│   Load Balancer  │◄────────────┘
                        └──────────────────┘
```

## ✨ Features

- **Service Registration**: Microservices can register themselves automatically
- **Service Discovery**: Clients can discover available service instances
- **Health Monitoring**: Built-in health checks for registered services
- **Load Balancing**: Client-side load balancing with service instances
- **High Availability**: Support for multiple Eureka server instances
- **Docker Ready**: Containerized deployment with Docker support

## 🚀 Quick Start

### Prerequisites

- Java 17 or higher
- Maven 3.6+
- Docker (optional)

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/nervus-tech/nervus-eureka-server.git
   cd nervus-eureka-server/eureka-server
   ```

2. **Run with Maven**
   ```bash
   ./mvnw spring-boot:run
   ```

3. **Access the dashboard**
   - URL: http://localhost:8761
   - Default credentials: None (development mode)

### Docker Deployment

1. **Build the image**
   ```bash
   docker build -t nervus-eureka-server .
   ```

2. **Run the container**
   ```bash
   docker run -p 8761:8761 nervus-eureka-server
   ```

3. **Using Docker Compose**
   ```bash
   docker-compose up -d
   ```

## 🐳 Docker Compose Environments

### Local Development
```bash
docker-compose up -d
```

### Staging Environment
```bash
docker-compose -f docker-compose-staging.yml up -d
```

### Production Environment
```bash
docker-compose -f docker-compose-prod.yml up -d
```

## ⚙️ Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `SERVER_PORT` | `8761` | Eureka server port |
| `EUREKA_CLIENT_SERVICEURL_DEFAULTZONE` | `http://localhost:8761/eureka/` | Default zone URL |
| `EUREKA_INSTANCE_HOSTNAME` | `localhost` | Instance hostname |
| `EUREKA_SERVER_ENABLE_SELF_PRESERVATION` | `false` | Self-preservation mode |

### Application Properties

Key configuration in `src/main/resources/application.properties`:

```properties
# Server Configuration
server.port=8761
eureka.instance.hostname=localhost

# Client Configuration
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka/
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false

# Server Configuration
eureka.server.enable-self-preservation=false
eureka.server.eviction-interval-timer-in-ms=1000
```

## 🔧 Development

### Project Structure
```
eureka-server/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/nervus/eureka_server/
│   │   │       └── EurekaServerApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
│           └── com/nervus/eureka_server/
│               └── EurekaServerApplicationTests.java
├── Dockerfile
├── docker-compose.yml
├── docker-compose-staging.yml
├── docker-compose-prod.yml
└── pom.xml
```

### Building

```bash
# Clean build
./mvnw clean package

# Skip tests
./mvnw clean package -DskipTests

# Run tests only
./mvnw test
```

### Testing

```bash
# Run unit tests
./mvnw test

# Run with coverage
./mvnw jacoco:report
```

## 🌐 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Eureka dashboard |
| `/eureka/apps` | GET | List all registered applications |
| `/eureka/apps/{appName}` | GET | Get specific application info |
| `/actuator/health` | GET | Health check endpoint |
| `/actuator/info` | GET | Application information |

## 🔒 Security

- **Development**: No authentication (for local development)
- **Staging/Production**: Configure authentication as needed
- **Network Security**: Ensure proper firewall rules for port 8761

## 📊 Monitoring & Health Checks

### Health Check Endpoint
```
GET /actuator/health
```

### Metrics
- Service registration count
- Service discovery requests
- Instance health status
- Response times

## 🚨 Troubleshooting

### Common Issues

1. **Service not registering**
   - Check Eureka server is running
   - Verify service configuration
   - Check network connectivity

2. **Dashboard not accessible**
   - Verify port 8761 is open
   - Check firewall settings
   - Ensure no other service is using the port

3. **High memory usage**
   - Monitor heap usage
   - Adjust JVM parameters
   - Check for memory leaks

### Logs

```bash
# View application logs
docker logs <container-id>

# Follow logs
docker logs -f <container-id>

# View specific log levels
docker logs <container-id> | grep ERROR
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is proprietary and confidential. All rights reserved by Nervus.tech.

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/nervus-tech/nervus-eureka-server/issues)
- **Documentation**: [Nervus.tech Docs](https://docs.nervus.tech)
- **Team**: DevOps Team

## 🔄 Version History

- **v1.0.0** - Initial release with basic service discovery
- **v1.1.0** - Added Docker support and environment configurations
- **v1.2.0** - Enhanced monitoring and health checks

---

**Built with ❤️ by the Nervus.tech Team**
