# CI/CD Demo - Spring Boot Security Hardened Application

[![Java CI with Maven](https://github.com/Kinley-pal8/cicd-demo/workflows/Java%20CI%20with%20Maven/badge.svg)](https://github.com/Kinley-pal8/cicd-demo/actions)
[![Security Scan](https://github.com/Kinley-pal8/cicd-demo/workflows/Enhanced%20Security%20Scan/badge.svg)](https://github.com/Kinley-pal8/cicd-demo/actions)

A comprehensive CI/CD demonstration project built with Spring Boot, showcasing modern security practices, automated testing, and continuous integration with GitHub Actions and Snyk security scanning.

## 🚀 Features

- **Spring Boot 3.4.10** - Latest stable version with security patches
- **Java 17 LTS** - Long-term support with modern language features
- **RESTful API** - Clean endpoints for health checks and data generation
- **Security Hardened** - Zero known vulnerabilities through comprehensive dependency management
- **Containerized** - Alpine-based Docker image for minimal attack surface
- **Automated Testing** - Unit tests with JaCoCo code coverage
- **CI/CD Pipeline** - GitHub Actions with security scanning integration

## 📋 Table of Contents

- [Quick Start](#quick-start)
- [API Endpoints](#api-endpoints)
- [Development](#development)
- [Security](#security)
- [Docker](#docker)
- [CI/CD Pipeline](#cicd-pipeline)
- [Testing](#testing)
- [Contributing](#contributing)

## 🏃‍♂️ Quick Start

### Prerequisites

- Java 17 or later
- Maven 3.8+
- Docker (optional)

### Local Development

1. **Clone the repository**

   ```bash
   git clone https://github.com/Kinley-pal8/cicd-demo.git
   cd cicd-demo
   ```

2. **Run the application**

   ```bash
   ./mvnw spring-boot:run
   ```

3. **Access the application**
   - Health Check: http://localhost:8080/
   - Version Info: http://localhost:8080/version
   - Sample Data: http://localhost:8080/nations

## 🔌 API Endpoints

| Endpoint      | Method | Description           | Response              |
| ------------- | ------ | --------------------- | --------------------- |
| `/`           | GET    | Health check endpoint | Plain text status     |
| `/version`    | GET    | Application version   | Version string        |
| `/nations`    | GET    | Random nation data    | JSON array (10 items) |
| `/currencies` | GET    | Random currency data  | JSON array (20 items) |

### Example Responses

**GET /nations**

```json
[
  {
    "nationality": "American",
    "capitalCity": "Washington D.C.",
    "flag": "🇺🇸",
    "language": "English"
  }
]
```

**GET /currencies**

```json
[
  {
    "name": "US Dollar",
    "code": "USD"
  }
]
```

## 🛠 Development

### Project Structure

```
src/
├── main/java/sg/edu/nus/iss/cicddemo/
│   ├── CicdDemoApplication.java          # Main application class
│   └── Controller/
│       └── DataController.java           # REST API controller
├── main/resources/
│   └── application.properties            # App configuration
└── test/java/                           # Unit tests
```

### Key Dependencies

- **Spring Boot Starter Web** - RESTful web services
- **DataFaker 2.4.0** - Secure test data generation (replaced JavaFaker)
- **Jackson** - JSON processing
- **JUnit 5** - Testing framework

### Building

```bash
# Clean and compile
./mvnw clean compile

# Run tests
./mvnw test

# Package application
./mvnw package

# Run with specific profile
./mvnw spring-boot:run -Dspring-boot.run.profiles=dev
```

## 🔒 Security

This project implements comprehensive security measures:

### Vulnerability Management

- **Zero Known CVEs** - All dependencies updated to secure versions
- **Automated Scanning** - Snyk integration in CI/CD pipeline
- **Alpine Base Image** - Minimal container with reduced attack surface
- **Non-root User** - Container runs with limited privileges

### Recent Security Fixes

| CVE            | Component    | Fix                                | Status   |
| -------------- | ------------ | ---------------------------------- | -------- |
| CVE-2025-41249 | spring-core  | Upgrade to 6.2.11                  | ✅ Fixed |
| Multiple CVEs  | JavaFaker    | Replaced with DataFaker 2.4.0      | ✅ Fixed |
| Container CVEs | OpenJDK base | Switched to Eclipse Temurin Alpine | ✅ Fixed |

### Security Policy

The project maintains a `.snyk` policy file tracking all vulnerability remediations with expiration dates for continuous monitoring.

## 🐳 Docker

### Building the Image

```bash
# Build image
docker build -t cicd-demo:latest .

# Run container
docker run -p 8080:8080 cicd-demo:latest
```

### Image Details

- **Base Image**: `eclipse-temurin:17-jdk-alpine`
- **Size**: Optimized for minimal footprint
- **Security**: Non-root user, dumb-init process manager
- **Port**: Exposes 8080

### Docker Compose (Optional)

```yaml
version: "3.8"
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=docker
```

## 🔄 CI/CD Pipeline

### GitHub Actions Workflows

1. **Maven Build & Test** (`.github/workflows/maven.yml`)

   - Runs on push/PR to master
   - Java 17 with Eclipse Temurin
   - Maven test execution
   - Artifact caching

2. **Enhanced Security Scan** (`.github/workflows/enhanced-security.yml`)
   - Snyk vulnerability scanning
   - CodeQL analysis
   - SARIF report generation
   - Security artifact upload

### Pipeline Features

- **Automated Testing** - Unit tests run on every commit
- **Security Scanning** - Snyk checks for vulnerabilities
- **Code Analysis** - CodeQL for security issues
- **Dependency Caching** - Maven dependencies cached for faster builds
- **Multi-stage Validation** - Test → Security → Deploy flow

## 🧪 Testing

### Running Tests

```bash
# Run all tests
./mvnw test

# Run with coverage
./mvnw test jacoco:report

# Run specific test
./mvnw test -Dtest=DataControllerTest
```

### Test Coverage

- **Unit Tests**: Controller and application tests
- **Integration Tests**: Full Spring context testing
- **Coverage Tool**: JaCoCo for comprehensive reporting
- **Coverage Report**: `target/site/jacoco/index.html`

### Test Structure

```
src/test/java/
├── CicdDemoApplicationTests.java        # Application context tests
└── DataControllerTest.java              # Controller endpoint tests
```

## 🤝 Contributing

### Development Workflow

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** changes (`git commit -m 'Add amazing feature'`)
4. **Push** to branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Code Standards

- **Java 17** language features encouraged
- **Spring Boot** best practices
- **Security First** - All dependencies must be vulnerability-free
- **Test Coverage** - Maintain high test coverage
- **Documentation** - Update README for significant changes

### Security Requirements

- Run `mvn dependency:tree` to check for vulnerable dependencies
- Ensure Snyk scans pass
- Update `.snyk` policy for any new vulnerabilities
- Use secure coding practices

## 📚 Additional Resources

- **Spring Boot Documentation**: https://spring.io/projects/spring-boot
- **DataFaker Documentation**: https://www.datafaker.net/
- **Snyk Security**: https://snyk.io/
- **GitHub Actions**: https://docs.github.com/en/actions

## 📄 License

This project is part of an educational CI/CD workshop demonstrating modern DevSecOps practices.

## 🏫 Academic Context

**Workshop**: CI/CD SAST/DAST Integration  
**Institution**: National University of Singapore (NUS)  
**Focus**: Practical integration of security scanning tools in CI/CD pipelines

---

**Version**: 1.0.0  
**Last Updated**: September 2025  
**Security Status**: ✅ All known vulnerabilities resolved
# swe302_practical_4
