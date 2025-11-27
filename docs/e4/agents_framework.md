# 🤖 Framework de Agentes y Subagentes
## Sistema de Agentes Especializados para Desarrollo del Proyecto NestJS

**Fecha**: Noviembre 2025  
**Versión**: 1.0  
**Objetivo**: Definir un sistema multi-agente especializado con responsabilidades claras, herramientas específicas, habilidades comprobadas y mapeo de riesgos/limitaciones

---

## 1. ARQUITECTURA GENERAL DE AGENTES

```
┌─────────────────────────────────────────────────────────────┐
│                   META AGENTE (Orquestador)                 │
│         Project Director & Quality Assurance Lead             │
│                  Responsable: Coordinación                    │
└────────────────────┬────────────────────────────────────────┘
                     │
     ┌───────────────┼───────────────┬────────────────┬──────────────┐
     │               │               │                │              │
     ▼               ▼               ▼                ▼              ▼
┌─────────────┐ ┌──────────────┐ ┌──────────────┐ ┌─────────────┐ ┌──────────┐
│ Architecture│ │   Database   │ │   API REST   │ │   Testing   │ │ Security │
│   Agent     │ │    Agent     │ │    Agent     │ │    Agent    │ │  Agent   │
│ (Módulos)   │ │ (Prisma/SQL) │ │ (Endpoints)  │ │ (Jest/E2E)  │ │(JWT/Auth)│
└─────────────┘ └──────────────┘ └──────────────┘ └─────────────┘ └──────────┘
     │               │               │                │              │
     └───────────────┼───────────────┴────────────────┴──────────────┘
                     │
     ┌───────────────┴───────────────┐
     │                               │
     ▼                               ▼
┌─────────────────┐          ┌───────────────┐
│  DevOps Agent   │          │  CI/CD Agent  │
│ (Deployment)    │          │  (Pipelines)  │
└─────────────────┘          └───────────────┘
```

---

## 2. META AGENTE: Project Orchestrator & Quality Lead

### 📋 Perfil
- **ID**: `meta-agent-001`
- **Nombre**: Project Director
- **Tipo**: Orquestador Central
- **Responsabilidad Principal**: Coordinación, validación de calidad, escalamiento de problemas
- **Ubicación en Workflow**: Punto de entrada y coordinador de todos los subagentes

### 🎯 Responsabilidades Principales

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Coordinación de Subagentes** | Distribuir tareas, sincronizar entregas, validar dependencias |
| 2 | **Control de Calidad** | Verificar código, arquitectura, testing, documentación |
| 3 | **Gestión de Riesgos** | Monitorear riesgos técnicos, escalar problemas críticos |
| 4 | **Planificación de Sprints** | Definir iteraciones, prioridades, hitos |
| 5 | **Validación de Entregas** | Aprobar código antes de merge, verificar completitud |
| 6 | **Comunicación** | Reportes de progreso, escalamiento a stakeholders |
| 7 | **Gestión de Configuración** | Mantener consistencia en estándares y convenciones |

### 🛠️ Herramientas Disponibles

```json
{
  "herramientas_core": [
    "VS Code API",
    "Git & GitHub",
    "Workspace Analyzer",
    "Code Quality Scanner",
    "Dependency Checker"
  ],
  "herramientas_colaboracion": [
    "Task Orchestration Engine",
    "Agent Communication Protocol",
    "Knowledge Base Manager",
    "Issue Tracker Integration"
  ],
  "herramientas_validacion": [
    "Linters (ESLint, Prettier)",
    "Type Checker (TypeScript)",
    "Security Scanner (SonarQube)",
    "Performance Analyzer"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| Arquitectura de Software | Experto | ✅ Decisiones arquitectónicas documentadas |
| Gestión de Proyectos | Senior | ✅ Planificación ágil |
| Code Review | Experto | ✅ Patrones SOLID, arquitectura limpia |
| TypeScript/JavaScript | Experto | ✅ Definición de estándares |
| NestJS | Experto | ✅ Arquitectura modular |
| PostgreSQL | Senior | ✅ Diseño de datos |
| Metodología Ágil | Senior | ✅ Sprints y entregas |
| Comunicación Técnica | Senior | ✅ Documentación clara |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Cuello de botella de aprobación** | ALTA | CRÍTICO | Delegación de autoridad en revisiones menores |
| **Falta de sincronización entre agentes** | MEDIA | ALTO | Protocolo de comunicación estricto |
| **Decisiones que afectan múltiples módulos** | MEDIA | ALTO | Arquitectura desacoplada, interfaces claras |
| **Sobrecarga de tareas** | ALTA | MEDIO | Automatización de validaciones |
| **Cambios de requisitos tardíos** | MEDIA | CRÍTICO | Control de cambios riguroso |
| **Integración fallida entre módulos** | MEDIA | CRÍTICO | Testing de integración completo |

### 📊 Métricas de Éxito

- ✅ 95%+ de entregas a tiempo
- ✅ 0 defectos críticos en producción
- ✅ 100% cobertura de tests > 80%
- ✅ Documentación actualizada siempre
- ✅ Tiempos de review < 24 horas
- ✅ 0 deuda técnica acumulada

---

## 3. ARCHITECTURE AGENT: Especialista en Diseño

### 📋 Perfil
- **ID**: `agent-arch-001`
- **Nombre**: Architecture Specialist
- **Responsabilidad**: Diseño modular, patrones, decisiones de stack
- **Reporta a**: Meta Agente

### 🎯 Responsabilidades

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Diseño de Arquitectura** | Definir módulos, capas, patrones |
| 2 | **Evaluación de Stack Tecnológico** | Seleccionar herramientas, librerías, frameworks |
| 3 | **Patrones de Diseño** | Implementar SOLID, Clean Architecture, DDD |
| 4 | **Documentación de Arquitectura** | Mantener diagramas, ADRs (Architectural Decision Records) |
| 5 | **Revisión Técnica** | Validar que el código sigue arquitectura |
| 6 | **Escalabilidad** | Asegurar que sistemas pueden crecer |
| 7 | **Performance** | Optimizar críticas de cuello de botella |

### 🛠️ Herramientas

```json
{
  "desarrollo": [
    "NestJS 10.x",
    "TypeScript 5.x",
    "Node.js 22.x",
    "Express (integrado en NestJS)"
  ],
  "validacion": [
    "ESLint con reglas NestJS",
    "TypeScript Compiler (strict mode)",
    "SonarQube para code quality",
    "Dependency-Check para vulnerabilidades"
  ],
  "documentacion": [
    "Mermaid para diagramas",
    "OpenAPI/Swagger",
    "Architecture Decision Records (ADR)",
    "PlantUML"
  ],
  "herramientas_ia": [
    "Code analyzer",
    "Pattern detector",
    "Dependency visualizer"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| Arquitectura NestJS | Experto | ✅ 8+ módulos diseñados |
| Principios SOLID | Experto | ✅ Bajo acoplamiento, alto cohesión |
| Design Patterns | Experto | ✅ Factory, Singleton, Strategy, etc. |
| TypeScript Avanzado | Experto | ✅ Tipos complejos, genéricos |
| Performance Optimization | Senior | ✅ Análisis de cuellos de botella |
| Escalabilidad | Senior | ✅ Diseño horizontal y vertical |
| Documentation | Senior | ✅ ADRs claros y mantenidos |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Over-engineering inicial** | MEDIA | MEDIO | Iteración temprana, YAGNI |
| **Cambios arquitectónicos tardíos** | MEDIA | CRÍTICO | Prototipo temprano de decisiones críticas |
| **Complejidad acumulada** | ALTA | ALTO | Refactorización periódica |
| **Inconsistencia en módulos** | MEDIA | MEDIO | Code review exhaustiva |
| **Falta de flexibilidad** | BAJA | ALTO | Arquitectura basada en interfaces |
| **Desconocimiento de limitaciones del stack** | MEDIA | ALTO | Research y POCs |

### 📊 Métricas de Éxito

- ✅ Arquitectura documentada completamente
- ✅ 0 violaciones de principios SOLID
- ✅ Módulos con <300 LOC por servicio
- ✅ Desacoplamiento entre módulos
- ✅ 0 dependencias cíclicas

---

## 4. DATABASE AGENT: Especialista en Datos

### 📋 Perfil
- **ID**: `agent-db-001`
- **Nombre**: Database Specialist
- **Responsabilidad**: Esquema, migraciones, optimización, integridad
- **Reporta a**: Meta Agente

### 🎯 Responsabilidades

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Diseño de Esquema** | Modelo relacional, normalización, constraints |
| 2 | **Migraciones** | Crear y ejecutar migraciones Prisma |
| 3 | **Optimización** | Índices, queries, performance tuning |
| 4 | **Integridad de Datos** | Constraints, triggers, validaciones |
| 5 | **Backups y Recovery** | Estrategia de recuperación ante desastres |
| 6 | **Seeding** | Datos de prueba y producción |
| 7 | **Documentación** | ER diagrams, DDL, guías |

### 🛠️ Herramientas

```json
{
  "orm_y_migraciones": [
    "Prisma 5.x",
    "prisma/client",
    "prisma/migration"
  ],
  "database": [
    "PostgreSQL 13+",
    "pgAdmin para administración",
    "DBeaver para análisis"
  ],
  "validacion": [
    "Prisma schema validator",
    "SQL formatter (pgFormatter)",
    "Query analyzer (EXPLAIN ANALYZE)",
    "Performance monitor (pg_stat)"
  ],
  "datos": [
    "Prisma seed script",
    "Faker.js para datos ficticios",
    "Knex.js (si necesita queries complejas)"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| Diseño Relacional | Experto | ✅ FNBC normalizado |
| Prisma ORM | Experto | ✅ Schema completo con relaciones |
| PostgreSQL | Experto | ✅ Índices, constraints, triggers |
| Normalización | Experto | ✅ 3NF - FNBC |
| Query Optimization | Senior | ✅ EXPLAIN ANALYZE |
| Data Modeling | Experto | ✅ ER diagrams |
| Migraciones | Senior | ✅ Versionadas y reversibles |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Migraciones fallidas en producción** | BAJA | CRÍTICO | Testing exhaustivo en staging |
| **N+1 queries en Prisma** | MEDIA | ALTO | Uso correcto de `include`/`select` |
| **Deadlocks** | BAJA | ALTO | Transacciones bien diseñadas |
| **Crecimiento de datos no previsto** | MEDIA | ALTO | Particionamiento y archivado |
| **Cambios de esquema durante desarrollo** | ALTA | MEDIO | Control estricto de migraciones |
| **Performance de índices** | MEDIA | MEDIO | Monitoreo constante |

### 📊 Métricas de Éxito

- ✅ Esquema normalizado FNBC
- ✅ Todas las queries < 100ms (p95)
- ✅ 0 deadlocks en testing
- ✅ Cobertura de constraints 100%
- ✅ Migraciones versionadas y reversibles

---

## 5. API AGENT: Especialista en Endpoints REST

### 📋 Perfil
- **ID**: `agent-api-001`
- **Nombre**: API Specialist
- **Responsabilidad**: Diseño de endpoints, validación, documentación
- **Reporta a**: Meta Agente

### 🎯 Responsabilidades

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Diseño de Endpoints** | RESTful design, HTTP methods, status codes |
| 2 | **DTOs y Validación** | Request/response validation, class-validator |
| 3 | **Documentación OpenAPI** | Swagger, ejemplos, esquemas |
| 4 | **Rate Limiting** | Throttling, quotas |
| 5 | **Error Handling** | Respuestas consistentes, códigos de error |
| 6 | **Versionamiento** | Estrategia de versiones de API |
| 7 | **Ejemplos y Testing** | Postman, ejemplos funcionales |

### 🛠️ Herramientas

```json
{
  "framework": [
    "NestJS Controllers",
    "Express (base)",
    "Class Validator",
    "Class Transformer"
  ],
  "documentacion": [
    "@nestjs/swagger",
    "OpenAPI 3.0",
    "Swagger UI",
    "Postman"
  ],
  "validacion": [
    "HTTP status code validator",
    "JSON schema validator",
    "REST contract tester",
    "API blueprint tools"
  ],
  "herramientas_pruebas": [
    "Postman Collections",
    "Insomnia",
    "Thunder Client",
    "REST Client VS Code extension"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| REST API Design | Experto | ✅ 22 endpoints diseñados |
| NestJS Controllers | Experto | ✅ Uso de decoradores y middleware |
| HTTP & Status Codes | Experto | ✅ Semántica correcta |
| Validación de Datos | Experto | ✅ class-validator implementado |
| OpenAPI/Swagger | Senior | ✅ Documentación automática |
| Error Handling | Senior | ✅ Respuestas consistentes |
| API Versioning | Senior | ✅ Estrategia de compatibilidad |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Breaking changes en API** | MEDIA | CRÍTICO | Versionamiento estricto |
| **Falta de validación de entrada** | MEDIA | CRÍTICO | class-validator en todos los DTOs |
| **Performance de endpoints** | MEDIA | ALTO | Profiling y optimización |
| **Documentación desactualizada** | ALTA | MEDIO | Swagger automático desde código |
| **Inconsistencia en respuestas** | MEDIA | MEDIO | Interceptores estandarizados |
| **SQL Injection en queries** | BAJA | CRÍTICO | Siempre usar Prisma |

### 📊 Métricas de Éxito

- ✅ 22 endpoints implementados
- ✅ 100% validación en DTOs
- ✅ OpenAPI documentado completamente
- ✅ Response times < 200ms (p95)
- ✅ 0 breaking changes en versión

---

## 6. TESTING AGENT: Especialista en Calidad

### 📋 Perfil
- **ID**: `agent-test-001`
- **Nombre**: Quality Assurance Specialist
- **Responsabilidad**: Testing unitario, integración, E2E, cobertura
- **Reporta a**: Meta Agente

### 🎯 Responsabilidades

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Testing Unitario** | Services, utilities, lógica pura |
| 2 | **Testing de Integración** | Controllers, Prisma, base de datos |
| 3 | **Testing E2E** | Flujos completos de usuario |
| 4 | **Cobertura de Código** | Mantener > 80% cobertura |
| 5 | **Performance Testing** | Load tests, stress tests |
| 6 | **Security Testing** | Pruebas de autenticación, autorización |
| 7 | **Documentación de Casos** | Especificaciones de pruebas |

### 🛠️ Herramientas

```json
{
  "framework_testing": [
    "Jest 29.x",
    "Supertest 6.x",
    "@nestjs/testing"
  ],
  "coverage": [
    "Istanbul (integrado en Jest)",
    "Coverage reports",
    "SonarQube integration"
  ],
  "herramientas_adicionales": [
    "Faker.js para datos",
    "jest-mock-extended para mocks",
    "@types/jest para tipos"
  ],
  "performance_testing": [
    "Artillery para load tests",
    "K6 para stress tests",
    "Autocannon para benchmarks"
  ],
  "security_testing": [
    "OWASP ZAP",
    "Snyk para vulnerabilidades",
    "SonarQube security rules"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| Jest Framework | Experto | ✅ Tests unitarios y E2E |
| Supertest | Senior | ✅ Testing de controllers |
| Test Design | Experto | ✅ AAA pattern, mocking |
| Code Coverage | Senior | ✅ > 80% objetivo |
| Performance Testing | Senior | ✅ Load y stress tests |
| Security Testing | Senior | ✅ OWASP conocido |
| TDD Methodology | Senior | ✅ Test-first approach |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Tests frágiles y flaky** | MEDIA | MEDIO | Datos determinísticos, no mock timing |
| **Cobertura falsa (tests que no validan)** | MEDIA | ALTO | Code review de tests |
| **Falta de E2E tests** | MEDIA | CRÍTICO | Flujos críticos cubiertos |
| **Performance tests ausentes** | MEDIA | MEDIO | Baseline de performance |
| **Mocks excesivos** | MEDIA | ALTO | Balance mock/integration |
| **Tests lentos** | ALTA | MEDIO | Tests paralelos, fixtures rápidos |

### 📊 Métricas de Éxito

- ✅ Cobertura > 80% global
- ✅ 0 tests flaky
- ✅ Ejecución de suite < 5 minutos
- ✅ 100% de flujos críticos cubiertos (E2E)
- ✅ Performance baseline definido

---

## 7. SECURITY AGENT: Especialista en Seguridad

### 📋 Perfil
- **ID**: `agent-sec-001`
- **Nombre**: Security Specialist
- **Responsabilidad**: Autenticación, autorización, validación, vulnerabilidades
- **Reporta a**: Meta Agente

### 🎯 Responsabilidades

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Autenticación** | JWT, Passport strategies, login/logout |
| 2 | **Autorización** | RBAC, guards, permisos |
| 3 | **Validación de Entrada** | Prevención de inyección SQL, XSS, etc. |
| 4 | **Gestión de Secretos** | Environment variables, key rotation |
| 5 | **Auditoría** | Logging de acciones críticas |
| 6 | **Encriptación** | Datos sensibles en reposo y en tránsito |
| 7 | **Compliance** | GDPR, regulaciones aplicables |

### 🛠️ Herramientas

```json
{
  "autenticacion_autorizacion": [
    "@nestjs/jwt",
    "@nestjs/passport",
    "passport-jwt",
    "bcrypt para hashing",
    "crypto para encriptación"
  ],
  "validacion": [
    "class-validator",
    "class-transformer",
    "joi para schemas",
    "helmet.js para headers"
  ],
  "gestion_secretos": [
    ".env files (dotenv)",
    "Environment variable validator",
    "Secrets manager (AWS Secrets Manager o Azure Key Vault)"
  ],
  "auditoria_logging": [
    "Winston para logging",
    "Morgan para request logging",
    "Elasticsearch para análisis (opcional)"
  ],
  "seguridad_escaneo": [
    "npm audit",
    "Snyk",
    "SonarQube",
    "OWASP ZAP"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| JWT & OAuth2 | Experto | ✅ Tokens implementados |
| RBAC (Role-Based Access Control) | Experto | ✅ Guards y permisos |
| Password Security | Experto | ✅ Hashing con bcrypt |
| Input Validation | Experto | ✅ class-validator |
| OWASP Top 10 | Senior | ✅ Conocimiento de vulnerabilidades |
| Encryption | Senior | ✅ Data encryption in transit |
| Compliance (GDPR) | Senior | ✅ Privacy-first design |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Tokens comprometidos** | BAJA | CRÍTICO | Short expiry, refresh tokens |
| **SQL Injection** | BAJA | CRÍTICO | Siempre usar Prisma |
| **XSS attacks** | MEDIA | ALTO | Helmet.js, CSP headers |
| **Brute force attacks** | MEDIA | ALTO | Rate limiting, account lockout |
| **Vulnerabilidades en dependencias** | MEDIA | ALTO | npm audit regular, Snyk |
| **Exposición de secretos** | MEDIA | CRÍTICO | .gitignore, secretos manager |
| **Falta de auditoría** | ALTA | MEDIO | Logging exhaustivo |

### 📊 Métricas de Éxito

- ✅ 0 vulnerabilidades críticas en dependencias
- ✅ 100% validación de entrada
- ✅ JWT tokens con expiry < 1 hora
- ✅ Logs de auditoría para todas las acciones sensibles
- ✅ 0 secretos en repositorio (git-secrets OK)

---

## 8. DEVOPS AGENT: Especialista en Infraestructura

### 📋 Perfil
- **ID**: `agent-devops-001`
- **Nombre**: DevOps Specialist
- **Responsabilidad**: Deployment, CI/CD, configuración, monitoreo
- **Reporta a**: Meta Agente

### 🎯 Responsabilidades

| # | Responsabilidad | Descripción |
|---|---|---|
| 1 | **Configuración de Entornos** | Dev, staging, production |
| 2 | **CI/CD Pipeline** | GitHub Actions, automatización |
| 3 | **Containerización** | Docker, imagen base |
| 4 | **Orquestación** | Kubernetes (si aplica) |
| 5 | **Deployment** | Estrategias blue-green, canary |
| 6 | **Monitoreo** | Logs, métricas, alertas |
| 7 | **Disaster Recovery** | Backup, failover, RTO/RPO |

### 🛠️ Herramientas

```json
{
  "containerizacion": [
    "Docker",
    "Docker Compose",
    "Dockerfile multistage"
  ],
  "ci_cd": [
    "GitHub Actions",
    "GitHub Workflows",
    "Secrets management en GitHub",
    "Artifacts"
  ],
  "orchestracion": [
    "Docker Compose (dev)",
    "Kubernetes (si aplica)",
    "Helm para charts"
  ],
  "cloud_platforms": [
    "AWS (EC2, RDS, S3)",
    "Azure (App Service, SQL Database)",
    "DigitalOcean (opciones simples)"
  ],
  "monitoreo_y_logging": [
    "Datadog o New Relic",
    "ELK Stack (Elasticsearch, Logstash, Kibana)",
    "CloudWatch (si AWS)",
    "Application Insights (si Azure)"
  ],
  "infraestructura_como_codigo": [
    "Terraform",
    "CloudFormation",
    "Pulumi"
  ]
}
```

### 💡 Habilidades Clave

| Habilidad | Nivel | Validación |
|-----------|-------|-----------|
| Docker & Containerización | Senior | ✅ Dockerfile optimizado |
| GitHub Actions | Senior | ✅ Workflows automatizados |
| Kubernetes | Senior | ✅ Deployments, services (si aplica) |
| Infrastructure as Code | Senior | ✅ Terraform o CloudFormation |
| Linux/Bash | Senior | ✅ Scripts de administración |
| Cloud Platforms | Senior | ✅ AWS/Azure conocimiento |
| Monitoring & Logging | Senior | ✅ Alertas configuradas |

### ⚠️ Riesgos y Limitaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|--------|-----------|
| **Despliegue fallido en producción** | MEDIA | CRÍTICO | Staging idéntico a prod |
| **Secrets expuestos en logs** | MEDIA | CRÍTICO | Log filtering automático |
| **Downtime durante deployment** | BAJA | ALTO | Blue-green deployment |
| **Base de datos corrupta** | BAJA | CRÍTICO | Backups automatizados y testados |
| **Insuficiente capacity** | MEDIA | ALTO | Auto-scaling configurado |
| **Falta de monitoreo** | MEDIA | CRÍTICO | Alertas para métricas clave |

### 📊 Métricas de Éxito

- ✅ Deployment < 5 minutos
- ✅ RTO < 1 hora
- ✅ RPO < 15 minutos
- ✅ 99.9% uptime
- ✅ 0 secrets en logs

---

## 9. FLUJO DE COORDINACIÓN Y COMUNICACIÓN

### 9.1 Estructura de Comunicación

```
Developer Input (User Request)
    │
    ▼
Meta Agente (Analysis & Planning)
    │
    ├─→ Architecture Agent (Design)
    │    ├─→ Database Agent (Schema)
    │    ├─→ API Agent (Endpoints)
    │    └─→ Security Agent (Auth)
    │
    ├─→ Testing Agent (Coverage)
    │    └─→ Validation
    │
    └─→ DevOps Agent (Deployment)
         └─→ CI/CD Pipeline
    │
    ▼
Merge to Main Branch
    │
    ▼
Production Deployment
```

### 9.2 Protocolo de Comunicación Entre Agentes

| Fase | Agente | Acción | Output |
|------|--------|--------|--------|
| **1. Análisis** | Meta Agente | Recibe requisito, analiza, planifica | Task backlog para subagentes |
| **2. Arquitectura** | Architecture Agent | Diseña módulos, estructura | Architecture diagram, ADRs |
| **3. Datos** | Database Agent | Define esquema, migraciones | schema.prisma, migration files |
| **4. API** | API Agent | Diseña endpoints, validaciones | Controllers, DTOs, Swagger |
| **5. Seguridad** | Security Agent | Implementa auth, encryption | Guards, decorators, middleware |
| **6. Testing** | Testing Agent | Cubre con tests | Test suites, coverage report |
| **7. DevOps** | DevOps Agent | Configura deployment | Dockerfile, GitHub Actions |
| **8. Validación** | Meta Agente | Verifica calidad, aprueba | Merge approval, release notes |

### 9.3 Escalamiento de Problemas

```
Level 1: Subagente (problema en su dominio)
    ↓
Level 2: Dos subagentes (requiere coordinación)
    ↓
Level 3: Meta Agente (toma decisión final)
    ↓
Level 4: Stakeholder (si requiere cambio de requisitos)
```

---

## 10. MATRIZ DE DEPENDENCIAS

```
┌──────────────────────────────────────────────────────────────────┐
│ Agente              │ Depende de        │ Requerido por          │
├──────────────────────────────────────────────────────────────────┤
│ Architecture        │ Meta Agente       │ Todos                  │
│ Database            │ Architecture      │ API, Testing, DevOps   │
│ API                 │ Architecture,DB   │ Testing, Security      │
│ Security            │ Architecture, API │ Testing, DevOps        │
│ Testing             │ Todo lo anterior  │ Meta Agente (Q/A)      │
│ DevOps              │ Todo lo anterior  │ Production             │
└──────────────────────────────────────────────────────────────────┘
```

---

## 11. CASOS DE USO: EJECUCIÓN DE AGENTES

### 11.1 Caso: Implementar Nuevo Módulo (Ej: Reviews)

```
Meta Agente
├─→ "Implementar módulo Reviews"
    │
    ├─→ Architecture Agent
    │   └─→ "Diseña entidad Review, relaciones, controllers"
    │       Output: review.module.ts, entities diagram
    │
    ├─→ Database Agent
    │   └─→ "Crea modelo Review en Prisma"
    │       Input: arquitectura de Architecture Agent
    │       Output: schema.prisma actualizado
    │
    ├─→ API Agent
    │   └─→ "Crea endpoints para Reviews: GET, POST, PATCH"
    │       Input: Database schema, Security requirements
    │       Output: Controllers, DTOs, Swagger docs
    │
    ├─→ Security Agent
    │   └─→ "Agrega autenticación y autorización para Reviews"
    │       Output: Guards, decorators
    │
    ├─→ Testing Agent
    │   └─→ "Cubre Review con tests unitarios, integración, E2E"
    │       Output: *.spec.ts files, coverage report
    │
    └─→ Meta Agente
        └─→ "Revisa todos los PRs, aprueba y mergea"
            Output: Merged to main branch
```

### 11.2 Caso: Bug Fix en Producción

```
Issue Report (P1 Crítico)
    │
    ▼
Meta Agente (Análisis de urgencia)
    │
    ├─→ Identificar módulo afectado
    │   └─→ Asignar a subagente especialista
    │
    ├─→ Subagente especialista
    │   ├─→ Reproduzca el bug
    │   ├─→ Identifique la causa raíz
    │   └─→ Implemente fix
    │
    ├─→ Security Agent (si es crítico de seguridad)
    │   └─→ Valide que no introduce nuevas vulnerabilidades
    │
    ├─→ Testing Agent
    │   └─→ Cree test que reproduzca bug y valide fix
    │
    ├─→ DevOps Agent
    │   └─→ Deploy en hotfix branch a staging
    │
    └─→ Meta Agente
        └─→ Aprueba y mergea a main, deployed a prod
```

---

## 12. TABLA DE AUTORIDAD Y TOMA DE DECISIONES

| Decisión | Autoridad | Escalamiento |
|----------|-----------|--------------|
| Patrón de código | Architecture Agent | Meta Agente |
| Cambio de schema | Database Agent | Architecture Agent → Meta Agente |
| Nuevo endpoint | API Agent | Architecture Agent → Meta Agente |
| Requerimiento de seguridad | Security Agent | Meta Agente |
| Cobertura de testing | Testing Agent | Meta Agente |
| Estrategia de deployment | DevOps Agent | Meta Agente |
| Cambio de requisitos | Meta Agente | Stakeholder |
| Deuda técnica significativa | Meta Agente | Stakeholder |

---

## 13. MÉTRICAS GLOBALES DEL EQUIPO DE AGENTES

### 13.1 Productividad

| Métrica | Target | Verificación |
|---------|--------|--------------|
| Velocity (story points/sprint) | 40-50 | Burndown chart |
| Defectos encontrados/día | < 1 | Bug tracker |
| Cambios rechazados en QA | < 5% | PRs aprobados |
| Tiempo de implementación | -20% vs baseline | Sprint timing |

### 13.2 Calidad

| Métrica | Target | Verificación |
|---------|--------|--------------|
| Code coverage | > 80% | SonarQube |
| Vulnerabilidades | 0 críticas | Snyk |
| Test pass rate | 100% | CI/CD pipeline |
| Performance | p95 < 200ms | Performance tests |

### 13.3 Mantenibilidad

| Métrica | Target | Verificación |
|---------|--------|--------------|
| Cyclomatic complexity | < 10 | SonarQube |
| Deuda técnica | < 10 días | SonarQube |
| Documentación | 100% | Code review |
| Conocimiento distribuido | 2+ expertos por módulo | Team interviews |

---

## 14. TABLA DE HABILIDADES Y ESPECIALIZACIÓN

```
┌─────────────────────┬────────────────┬────────────┬─────────────┬────────────┐
│ Habilidad           │ Architecture   │ Database   │ API         │ Security   │
├─────────────────────┼────────────────┼────────────┼─────────────┼────────────┤
│ NestJS              │ ⭐⭐⭐⭐⭐      │ ⭐⭐⭐     │ ⭐⭐⭐⭐⭐    │ ⭐⭐⭐⭐   │
│ TypeScript          │ ⭐⭐⭐⭐⭐      │ ⭐⭐⭐⭐   │ ⭐⭐⭐⭐⭐    │ ⭐⭐⭐⭐   │
│ PostgreSQL          │ ⭐⭐⭐         │ ⭐⭐⭐⭐⭐  │ ⭐⭐⭐     │ ⭐⭐⭐     │
│ Prisma ORM          │ ⭐⭐⭐         │ ⭐⭐⭐⭐⭐  │ ⭐⭐⭐⭐   │ ⭐⭐      │
│ REST API Design     │ ⭐⭐⭐⭐       │ ⭐⭐      │ ⭐⭐⭐⭐⭐    │ ⭐⭐⭐⭐   │
│ Testing (Jest)      │ ⭐⭐⭐         │ ⭐⭐⭐⭐   │ ⭐⭐⭐⭐   │ ⭐⭐⭐     │
│ Security/JWT        │ ⭐⭐⭐         │ ⭐⭐      │ ⭐⭐⭐⭐   │ ⭐⭐⭐⭐⭐  │
│ Docker/DevOps       │ ⭐⭐           │ ⭐⭐      │ ⭐⭐        │ ⭐⭐⭐     │
│ Performance Tuning  │ ⭐⭐⭐⭐       │ ⭐⭐⭐⭐⭐  │ ⭐⭐⭐     │ ⭐⭐      │
│ SOLID Principles    │ ⭐⭐⭐⭐⭐      │ ⭐⭐⭐     │ ⭐⭐⭐     │ ⭐⭐⭐     │
└─────────────────────┴────────────────┴────────────┴─────────────┴────────────┘

Testing Agent: ⭐⭐⭐⭐⭐ en Jest, ⭐⭐⭐⭐⭐ en Supertest, ⭐⭐⭐⭐ en Performance
DevOps Agent: ⭐⭐⭐⭐⭐ en Docker, ⭐⭐⭐⭐ en GitHub Actions, ⭐⭐⭐⭐ en Kubernetes
```

---

## 15. PLAN DE ONBOARDING PARA NUEVOS SUBAGENTES

Si en el futuro se necesitan agentes adicionales (ej: Analytics, Documentation, etc.):

1. **Fase 1: Análisis de Necesidad** (Meta Agente)
   - ¿Por qué se necesita este agente?
   - ¿Qué responsabilidades tiene?
   - ¿Cuáles son sus dependencias?

2. **Fase 2: Definición de Especialización** (Meta Agente + Arquitectura)
   - Stack tecnológico
   - Herramientas específicas
   - Habilidades requeridas

3. **Fase 3: Integración** (Todos los agentes)
   - Aclaración de interfaces de comunicación
   - Definición de deliverables
   - Escalamiento de problemas

4. **Fase 4: Ramp-Up** (Nuevo agente + Meta Agente)
   - Pares de problemas pequeños
   - Mentorship de agentes relacionados
   - Validación de cumplimiento de estándares

---

## 16. CONCLUSIÓN

Este **framework de agentes especializados** proporciona:

✅ **Claridad**: Cada agente sabe exactamente qué hacer  
✅ **Especialización**: Expertos en su dominio  
✅ **Escalabilidad**: Pueden trabajar en paralelo  
✅ **Calidad**: Múltiples capas de validación  
✅ **Rapidez**: Coordinación eficiente  
✅ **Riesgos Mitigados**: Identificación explícita de limitaciones  

El **Meta Agente** actúa como director de orquesta, asegurando que todos los subagentes trabajan de forma coordinada hacia el objetivo común: un **sistema backend NestJS de clase mundial**.

---

**Documento**: agents_framework.md  
**Versión**: 1.0  
**Última actualización**: Noviembre 2025  
**Próximas mejoras**: Plantilla de onboarding, scripts de automatización
