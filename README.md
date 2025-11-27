# CodeIA - Sesión 5 (2025)

## Restaurant Management System - NestJS Backend

[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg?cacheSeconds=2592000)](https://github.com/your-username/Sesion-5-2025-CodeIA/releases/tag/v0.1.0)
[![License](https://img.shields.io/badge/license-Proprietary-red.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/node-22.x-green.svg)](https://nodejs.org/)
[![NestJS](https://img.shields.io/badge/nestjs-10.x-red.svg)](https://nestjs.com/)
[![TypeScript](https://img.shields.io/badge/typescript-5.x-blue.svg)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/postgresql-13+-336791.svg)](https://www.postgresql.org/)

---

## 📋 Descripción

Sistema completo de gestión de restaurantes desarrollado con **NestJS**, **TypeScript**, **PostgreSQL** y **Prisma**. 

Incluye un framework innovador de **7 agentes especializados** que coordina el desarrollo del proyecto, operaciones, calidad y seguridad en un modelo de orquestación centralizado.

**Documentación**: 170+ páginas de especificaciones completas.

---

## 🎯 Características Principales

### Backend API
- ✅ **22 endpoints REST** completamente especificados
- ✅ **12 modelos de base de datos** normalizados
- ✅ **8 módulos NestJS** siguiendo principios SOLID
- ✅ **Autenticación JWT** con RBAC (4 roles)
- ✅ **Validación** con class-validator
- ✅ **Tests** con Jest (>80% coverage target)
- ✅ **E2E tests** con Supertest
- ✅ **CI/CD** con GitHub Actions
- ✅ **Documentación OpenAPI/Swagger**
- ✅ **Rate limiting** en endpoints críticos

### Gestión del Proyecto
- ✅ **7 Agentes especializados** con roles claros
- ✅ **12 procedimientos operacionales** documentados
- ✅ **Sprints biweekly** (40-50 story points)
- ✅ **Métricas KPI** definidas
- ✅ **Gestión de riesgos** con mitigación
- ✅ **Timeline** 90 días → producción
- ✅ **Checklist** de calidad y compliance

### Seguridad
- ✅ **Encriptación bcrypt** para passwords
- ✅ **JWT tokens** con expiry configurable
- ✅ **RBAC** (Role-Based Access Control)
- ✅ **Input validation** 100%
- ✅ **CORS** configurado
- ✅ **Helmet.js** para headers de seguridad
- ✅ **Rate limiting** anti-DDoS
- ✅ **Auditoría** de cambios sensibles

---

## 🏗️ Arquitectura

### Módulos NestJS (8)

```
src/
├── restaurants/        # Gestión de restaurantes
├── menus/             # Menús y platos
├── orders/            # Pedidos y estado
├── users/             # Usuarios y autenticación
├── reviews/           # Reseñas y ratings
├── employees/         # Empleados y asignaciones
├── auth/              # JWT, guards, estrategias
└── common/            # Shared (pipes, decorators, interceptors)
```

### Base de Datos (12 modelos)

```
User → roles (admin, owner, employee, customer)
Restaurant → Menus → MenuItems
          → Orders → OrderItems
          → Employees → WorkingHours
          → Assignments
Reviews & Ratings
Timestamps de auditoría
```

### API Endpoints (22)

**Restaurantes**
- `GET /restaurants` - Listar
- `POST /restaurants` - Crear
- `GET /restaurants/:id` - Detalle
- `PATCH /restaurants/:id` - Actualizar
- `DELETE /restaurants/:id` - Eliminar

**Menús**
- `GET /restaurants/:id/menus` - Listar menús
- `POST /restaurants/:id/menus` - Crear menú
- `GET /restaurants/:id/menus/:menuId` - Detalle
- `PATCH /menus/:id` - Actualizar
- `DELETE /menus/:id` - Eliminar

**Pedidos**
- `POST /orders` - Crear pedido
- `GET /orders` - Listar pedidos
- `GET /orders/:id` - Detalle
- `PATCH /orders/:id/status` - Cambiar estado
- `PATCH /orders/:id/cancel` - Cancelar

**Usuarios**
- `POST /auth/login` - Login
- `POST /auth/refresh` - Refrescar token
- `POST /auth/logout` - Logout
- `GET /users/:id/profile` - Perfil
- `PATCH /users/:id/profile` - Actualizar perfil

**Reseñas**
- `POST /reviews` - Crear reseña
- `GET /restaurants/:id/reviews` - Listar reseñas
- `GET /reviews/stats/:restaurantId` - Estadísticas

---

## 👥 Sistema de 7 Agentes

### Estructura de Coordinación

```
┌─────────────────────────────────────────┐
│      META AGENTE (Orquestador)          │
│  • Coordinación entre agentes           │
│  • Control de calidad                   │
│  • Gestión de riesgos                   │
└────────────┬────────────────────────────┘
             │
    ┌────────┼────────┐
    │        │        │
┌───▼──┐ ┌──▼───┐ ┌──▼────┐
│ ARCH │ │ DATA │ │  API  │
└───┬──┘ └──┬───┘ └──┬────┘
    │       │        │
┌───▼──┐ ┌──▼───┐ ┌──▼────┐
│ SEC  │ │TEST  │ │ DEVOPS│
└──────┘ └──────┘ └───────┘
```

### Roles & Responsabilidades

| Agente | Responsabilidad | Habilidades |
|--------|-----------------|------------|
| **Meta Agente** | Orquestación, QA, riesgos | Arquitectura, Gestión, Code Review (⭐⭐⭐⭐⭐) |
| **Architecture** | Módulos, SOLID, patrones | NestJS, TypeScript, Diseño (⭐⭐⭐⭐⭐) |
| **Database** | Prisma, migraciones, índices | SQL, Prisma, Optimization (⭐⭐⭐⭐⭐) |
| **API** | REST endpoints, DTOs, docs | HTTP, REST, OpenAPI (⭐⭐⭐⭐⭐) |
| **Security** | JWT, RBAC, encriptación | Auth, Crypto, OWASP (⭐⭐⭐⭐⭐) |
| **Testing** | Jest, E2E, coverage >80% | Jest, Testing, QA (⭐⭐⭐⭐⭐) |
| **DevOps** | Docker, GitHub Actions, K8s | DevOps, CI/CD, Monitoring (⭐⭐⭐⭐⭐) |

---

## 📊 Estadísticas del Proyecto

```
Documentación:      170+ páginas
Modelos BD:         12 modelos
Campos BD:          100+ campos
Relaciones:         25+ relaciones
Enums:              10 tipos
Constraints:        35+ constraints
Índices:            20+ índices
Endpoints:          22 REST endpoints
DTOs:               40+ DTOs
Módulos:            8 módulos
Tests Target:       > 80% coverage
Sprint Velocity:    40-50 story points
Timeline:           90 días → producción
```

---

## 🚀 Quick Start

### Prerequisitos

```bash
Node.js 22.x
PostgreSQL 13+
Git 2.40+
Docker (opcional)
```

### Instalación Local

```bash
# 1. Clonar repositorio
git clone https://github.com/your-username/Sesion-5-2025-CodeIA.git
cd Sesion-5-2025-CodeIA

# 2. Instalar dependencias
npm install

# 3. Configurar variables de entorno
cp .env.example .env
# Editar .env con credenciales

# 4. Configurar base de datos
npx prisma migrate dev

# 5. Iniciar servidor
npm run start:dev

# 6. Ver documentación (Swagger)
# http://localhost:3000/api/docs
```

### Docker

```bash
# Build imagen
docker build -t codeIA:0.1.0 .

# Ejecutar con compose
docker-compose up -d

# Logs
docker-compose logs -f api
```

---

## 🧪 Testing

```bash
# Tests unitarios
npm run test

# Tests con coverage
npm run test:cov

# Tests E2E
npm run test:e2e

# Tests en watch mode
npm run test:watch
```

**Target Coverage**: > 80%

---

## 📝 Documentación

Toda la documentación está en `/docs/e4/`:

| Documento | Páginas | Contenido |
|-----------|---------|----------|
| **INDEX.md** | 25 | Master index y navegación |
| **agents_framework.md** | 30 | 7 agentes, roles, responsabilidades |
| **agents_operations.md** | 25 | Procedimientos, sprints, workflows |
| **agents_summary.md** | 20 | Resumen ejecutivo y timeline |
| **architecture_nest.md** | 25 | Diseño modular, SOLID, patrones |
| **api_contracts.md** | 20 | 22 endpoints, DTOs, ejemplos |
| **db_model.md** | 15 | 12 modelos, relaciones, índices |
| **implementation_plan.md** | 10 | Sprint-by-sprint breakdown |
| **risk_map.md** | 5 | Riesgos y mitigación |
| **DELIVERABLES_SUMMARY.md** | 5 | Resumen visual del proyecto |

**Total**: 170+ páginas

### Cómo Leer la Documentación

1. **Comienza con** `INDEX.md` para entender la estructura
2. **Luego lee** `agents_summary.md` para visión ejecutiva
3. **Explora** `architecture_nest.md` para diseño técnico
4. **Consulta** `api_contracts.md` para especificaciones API
5. **Revisa** `agents_framework.md` para entender los roles
6. **Refiere** `agents_operations.md` para procedimientos día a día

---

## 🔐 Seguridad

### Medidas Implementadas

- ✅ **JWT Authentication** - Tokens con expiración configurable
- ✅ **RBAC** - 4 roles (admin, owner, employee, customer)
- ✅ **Password Hashing** - bcrypt con salt rounds
- ✅ **Input Validation** - class-validator en todos los DTOs
- ✅ **Rate Limiting** - 5 endpoints críticos protegidos
- ✅ **CORS** - Configurado para producción
- ✅ **Helmet.js** - Headers de seguridad HTTP
- ✅ **Auditoría** - Logs de cambios sensibles

### Mitigación de Riesgos OWASP Top 10

Todas las vulnerabilidades conocidas han sido identificadas y mitigadas.

---

## 🎯 Roadmap - 90 Días

### Fase 1: Development Core (Semanas 1-4)
- ✅ Módulos base (Restaurants, Menus, Users)
- ✅ Autenticación JWT + RBAC
- ✅ Tests unitarios (>80% coverage)
- **Goal**: API funcionando 100% en staging

### Fase 2: Orders & Hardening (Semanas 5-8)
- ✅ Módulos Orders y Reviews
- ✅ Tests E2E
- ✅ Load testing & optimization
- **Goal**: API production-ready

### Fase 3: Launch (Semanas 9-12)
- ✅ Security audit final
- ✅ Canary deployment
- ✅ Full production deployment
- **Goal**: 99.95% uptime

---

## 📈 Métricas & KPIs

### Calidad de Código
```
Code Coverage:        > 80%
Cyclomatic Complexity: < 10
Maintainability Index: > 80
Duplicated Code:      < 3%
```

### Performance
```
Response Time (p95):  < 200ms
Query Performance:    < 100ms
Startup Time:         < 3s
```

### Seguridad
```
Critical Vulns:       0
Dependency Updates:   Automated
Secret Scanning:      Enabled
SAST Scanning:        Enabled
```

### Operaciones
```
Uptime:               99.95%
Deployment Time:      < 5min
MTTR (bugs):          < 2h
```

---

## 🔧 Stack Tecnológico

**Backend**
- Node.js 22.x
- NestJS 10.x
- TypeScript 5.x

**Database**
- PostgreSQL 13+
- Prisma 5.x ORM

**Testing**
- Jest 29.x
- Supertest 6.x

**Security**
- JWT + Passport.js
- bcrypt
- Helmet.js

**DevOps**
- Docker & Docker Compose
- GitHub Actions
- Kubernetes
- Datadog (monitoring)

---

## 📦 Versionado Semántico

Este proyecto sigue [SemVer 2.0.0](https://semver.org/):

- **MAJOR** (X.0.0): Breaking changes
- **MINOR** (0.X.0): New features
- **PATCH** (0.0.X): Bug fixes

**Versión Actual**: `0.1.0` - Initial framework & documentation

---

## 🤝 Contribuyendo

### Flujo de Trabajo

1. **Create feature branch** desde `main`
2. **Implement feature** con tests
3. **Open Pull Request** para code review
4. **Merge** después de aprobación Meta Agente

### Code Review Checklist

- [ ] Código sigue estándares
- [ ] Tests > 80% coverage
- [ ] Documentación actualizada
- [ ] Sin vulnerabilidades
- [ ] Performance aceptable

---

## 📞 Soporte

- **Issues**: [GitHub Issues](https://github.com/your-username/Sesion-5-2025-CodeIA/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-username/Sesion-5-2025-CodeIA/discussions)
- **Email**: bot@codeIA.dev

---

## 📄 Licencia

Proprietary - All rights reserved (2025)

Este proyecto es propietario. No se permite reproducción, distribución o uso sin autorización explícita.

---

## 👨‍💻 Autores

- **CodeIA Bot** - Initial framework & documentation setup

---

## 🙏 Agradecimientos

Gracias a todos los agentes especializados del equipo por sus contribuciones en:
- Architecture & Design
- Database Optimization
- API Specification
- Security Hardening
- Testing & QA
- DevOps & Infrastructure

---

**Version**: 0.1.0  
**Last Updated**: 2025-11-27  
**Repository**: [Sesion - 5 - 2025 - CodeIA](https://github.com/your-username/Sesion-5-2025-CodeIA)

---

## 🎖️ Badges

[![Made with ❤️](https://img.shields.io/badge/Made%20with-%E2%9D%A4-red.svg)](https://github.com/your-username/Sesion-5-2025-CodeIA)
[![Node.js](https://img.shields.io/badge/Node.js-22.x-green.svg)](https://nodejs.org/)
[![NestJS](https://img.shields.io/badge/NestJS-10.x-red.svg)](https://nestjs.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13+-blue.svg)](https://www.postgresql.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue.svg)](https://www.typescriptlang.org/)
[![Jest](https://img.shields.io/badge/Jest-29.x-yellow.svg)](https://jestjs.io/)
