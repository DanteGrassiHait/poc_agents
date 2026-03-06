# AGENTS.md - API Integration MercadoLibre Service

## Project Overview

API Integration MercadoLibre Service - Microservicio Spring Boot para integración con la API de MercadoLibre. Maneja productos, pedidos, envíos y facturación.

- **Language:** Java 21
- **Build Tool:** Gradle (Kotlin DSL)
- **Framework:** Spring Boot 3.5.7
- **Database:** PostgreSQL with Liquibase

## Setup Commands

```bash
# Install dependencies
./gradlew dependencies

# Build project
./gradlew build

# Run tests
./gradlew test

# Run tests with coverage
./gradlew jacocoTestReport

# Run specific test class
./gradlew test --tests "com.infosisglobal.apiintegrationmercadolibreservice.service.ClassNameTest"

# Run application locally
./gradlew bootRun
```

## Code Style

- **Java Version:** 21
- **Formatting:** Use IDE code style (IntelliJ/Eclipse)
- **Validation:** Use Jakarta Validation annotations (@NotNull, @NotBlank, etc.)
- **Logging:** Use Lombok @Slf4j, avoid System.out/err

### Naming Conventions

| Type        | Pattern           | Example                    |
|-------------|-------------------|----------------------------|
| Service     | {Name}Service     | MercadoLibreProductService |
| Controller  | {Name}Controller  | ProductoController         |
| Repository  | {Name}Repository  | PedidoRepository           |
| Client      | {Name}Client      | MercadoLibreClient         |
| Entity      | {Name}            | Producto                   |
| DTO         | {Name}DTO         | ProductoDTO                |
| Exception   | {Name}Exception   | ProductoNotFoundException  |
| DAO         | {name}JPADAO      | ProductoJPADAO             |
| Interceptor | {name}Interceptor | MercadoLibreInterceptor    |
| Config      | {Name}Config      | MercadoLibreConfig         |


> **Nota:** El sufijo indica el tipo de clase. Para buscar una clase, primero buscar por su sufijo en la carpeta correspondiente. Las clases que no sigan este patrón se buscan normalmente en el proyecto.

## Project Structure

```
src/main/java/com/infosisglobal/apiintegrationmercadolibreservice/
├── config/          # Configuration classes
├── controller/      # REST controllers
├── service/         # Business logic
├── data/            # Entities and DTOs
    ├── dao/         # Data access object
    ├── datatype/    # Datatype enums
    ├── domain/      # Entity
    ├── dto/         # Data transfer object
    ├── mapper/      # Entity/DTO mapper
    └── repository/  # Data access
├── client/          # External API clients (MercadoLibre, etc.)
├── interceptor/     # Intercept request
└── exception/       # Custom exceptions

src/test/java/       # Unit tests
```

## Testing

- **Framework:** JUnit 5 + Mockito
- **Test Coverage:** JaCoCo (minimum 70%)
- **Object Creation:** Use Instancio for DTOs

### Testing Guidelines

Para tareas de tests unitarios, el agente lee automáticamente `unit-testing/AGENTS.md` que contiene:

- Patrones de configuración de tests
- Soluciones a problemas comunes (NullPointerException, ReflectionTestUtils, etc.)
- Ejemplos de uso de Instancio
- Lista de tests creados y su coverage

## Common Patterns

### REST Controllers
- Return ResponseEntity<?>
- Use @Valid for request validation
- Handle exceptions with @ControllerAdvice

### Services
- Extend MercadoLibreEntityService for entity operations
- Use integrationClient for external API calls
- Protected fields require ReflectionTestUtils in tests

### External Clients
- MercadoLibreClient for MercadoLibre API
- RestTemplate for HTTP calls
- Token-based authentication

## Important Notes

- Configuration loaded from Spring Cloud Config
- Secrets stored in environment variables / vault
- Use @Transactional for database operations
- Liquibase for database migrations (src/main/resources/db/changelog/)
