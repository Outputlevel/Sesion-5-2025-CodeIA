# 📋 PROTOCOLOS OPERACIONALES DE AGENTES

## Sistema de Operaciones para Equipo Multi-Agente

**Versión**: 1.0  
**Última actualización**: Noviembre 2025  
**Propósito**: Definir flujos, protocolos y procedimientos operacionales para coordinación de agentes

---

## 1. INICIALIZACIÓN DE SPRINT

### 1.1 Reunión de Planificación (Meta Agente + Todos)

```
DURACIÓN: 2-4 horas
FRECUENCIA: Cada 2 semanas
PARTICIPANTES: Meta Agente, 6 Subagentes

AGENDA:
├─ Revisión de objetivos del sprint
├─ Análisis de requisitos nuevos
├─ Estimación de complejidad (Architecture)
├─ Identificación de dependencias (Meta Agente)
├─ Asignación de tareas por agente
├─ Establecimiento de hitos (milestones)
└─ Identificación de riesgos

OUTPUT:
├─ Sprint backlog con tasks por agente
├─ Matriz de dependencias
├─ Riesgos identificados
└─ Hitos clave con fechas
```

### 1.2 Estructura de Tareas del Sprint

```json
{
  "sprint": {
    "id": "SPRINT-001",
    "fecha_inicio": "2025-11-27",
    "fecha_fin": "2025-12-10",
    "meta": "Implementar módulo Reviews con 80% cobertura",
    "tasks": [
      {
        "id": "ARCH-001",
        "agente": "Architecture Agent",
        "descripcion": "Diseñar entidad Review y relaciones",
        "prioridad": "P0",
        "fecha_deadline": "2025-11-28",
        "dependencias": [],
        "criterios_aceptacion": [
          "Entity diagram creado",
          "Relaciones documentadas",
          "ADR creado"
        ]
      },
      {
        "id": "DB-001",
        "agente": "Database Agent",
        "descripcion": "Implementar modelo Review en Prisma",
        "prioridad": "P0",
        "fecha_deadline": "2025-11-29",
        "dependencias": ["ARCH-001"],
        "criterios_aceptacion": [
          "Schema Prisma actualizado",
          "Migraciones creadas",
          "Índices optimizados"
        ]
      },
      {
        "id": "API-001",
        "agente": "API Agent",
        "descripcion": "Crear endpoints para Reviews",
        "prioridad": "P0",
        "fecha_deadline": "2025-11-30",
        "dependencias": ["DB-001"],
        "criterios_aceptacion": [
          "Controllers implementados",
          "DTOs validados",
          "Swagger documentado"
        ]
      },
      {
        "id": "SEC-001",
        "agente": "Security Agent",
        "descripcion": "Agregar autenticación a Reviews",
        "prioridad": "P1",
        "fecha_deadline": "2025-12-01",
        "dependencias": ["API-001"],
        "criterios_aceptacion": [
          "Guards configurados",
          "Permisos definidos",
          "Validaciones de entrada"
        ]
      },
      {
        "id": "TEST-001",
        "agente": "Testing Agent",
        "descripcion": "Cobertura de tests para Reviews",
        "prioridad": "P0",
        "fecha_deadline": "2025-12-03",
        "dependencias": ["SEC-001"],
        "criterios_aceptacion": [
          "Coverage > 80%",
          "Tests E2E ejecutados",
          "0 tests flaky"
        ]
      },
      {
        "id": "DEVOPS-001",
        "agente": "DevOps Agent",
        "descripcion": "Configurar CI/CD para Review",
        "prioridad": "P1",
        "fecha_deadline": "2025-12-05",
        "dependencias": ["TEST-001"],
        "criterios_aceptacion": [
          "GitHub Actions workflow",
          "Staging deployment",
          "Rollback strategy"
        ]
      },
      {
        "id": "META-001",
        "agente": "Meta Agente",
        "descripcion": "Code review y validación final",
        "prioridad": "P0",
        "fecha_deadline": "2025-12-08",
        "dependencias": ["DEVOPS-001"],
        "criterios_aceptacion": [
          "PRs aprobados",
          "QA checks pasados",
          "Documentación completa",
          "Mergeable a main"
        ]
      }
    ]
  }
}
```

---

## 2. PROTOCOLO DE CÓDIGO Y PULL REQUESTS

### 2.1 Ciclo de Vida de un PR

```
PASO 1: Developer crea feature branch
        └─→ Formato: feature/{agente}/{descripcion}
        └─→ Ejemplo: feature/database/add-review-model

PASO 2: Developer implementa cambios en su dominio
        └─→ Sigue patrones definidos por su agente
        └─→ Crea tests según Testing Agent specs
        └─→ Documenta cambios (si aplica)

PASO 3: Pre-commit checks locales
        ├─→ ESLint (code style)
        ├─→ TypeScript strict (types)
        ├─→ Jest --coverage (tests)
        └─→ git-secrets (no secrets expuestos)

PASO 4: Push a GitHub
        └─→ Trigger automated checks:
            ├─→ GitHub Actions (build, test, coverage)
            ├─→ SonarQube (code quality)
            ├─→ Snyk (security scan)
            └─→ Dependency check

PASO 5: Crear Pull Request (GitHub)
        ├─→ Título: [AGENTE] Descripción corta
        ├─→ Descripción: ¿Qué? ¿Por qué? ¿Cómo?
        ├─→ Screenshots/videos si es UI
        ├─→ Link a task/issue
        └─→ Checklist de PR completado

PASO 6: Code Review por especialista relacionado
        ├─→ Architecture Agent revisa diseño
        ├─→ Database Agent revisa queries/schema
        ├─→ API Agent revisa controllers/DTOs
        ├─→ Security Agent revisa autenticación/autorización
        ├─→ Testing Agent revisa tests/coverage
        ├─→ DevOps Agent revisa deployment/scripts
        └─→ Feedback en comentarios específicos

PASO 7: Ajustes por developer
        ├─→ Responde comentarios
        ├─→ Realiza cambios solicitados
        ├─→ Pushes a mismo branch
        └─→ Re-solicita review

PASO 8: Aprobación Final (Meta Agente)
        ├─→ Valida que todos los reviews estén OK
        ├─→ Revisa integración con resto del codebase
        ├─→ Aprueba PR con LGTM comment
        └─→ Merges a main branch

PASO 9: Post-merge
        ├─→ Delete feature branch
        ├─→ Actualizar task en backlog
        ├─→ Trigger deployment a staging
        └─→ Notificar equipo en Slack
```

### 2.2 Template de PR

```markdown
## 🎯 Descripción

¿Qué cambios introduce este PR?
- [ ] Bug fix
- [ ] Nueva feature
- [ ] Refactor
- [ ] Documentación

## 📋 Detalle de Cambios

- Cambio 1
- Cambio 2
- Cambio 3

## 🧪 Testing

- [ ] Tests unitarios agregados
- [ ] Tests de integración ejecutados
- [ ] Coverage >= 80%
- [ ] Tests E2E pasando

## ✅ Checklist Pre-Merge

- [ ] Código sigue patrones definidos
- [ ] TypeScript strict mode OK
- [ ] ESLint pasa sin errores
- [ ] No hay secretos expuestos
- [ ] Documentación actualizada
- [ ] CHANGELOG actualizado
- [ ] Dependencias auditadas

## 🔗 Links

- Issue: #123
- Task: SPRINT-001
- Relacionado: PR #456

## 👥 Reviewers Necesarios

- @architecture-agent
- @database-agent
- @testing-agent

## 📸 Screenshots / Videos

[Si aplica]
```

---

## 3. COMUNICACIÓN INTER-AGENTES

### 3.1 Canales de Comunicación

```
SÍNCRONO:
├─→ Slack #agentes-dev (diario standup)
├─→ Jira issues comments (coordinación)
├─→ GitHub PR discussions (code review)
└─→ Video calls (bloqueantes críticos)

ASÍNCRONO:
├─→ Architecture Decisions Records (ADRs)
├─→ Documentación en /docs
├─→ Mermaid diagrams en repos
└─→ Wiki de proyecto
```

### 3.2 Daily Standup (9:00 AM)

```
FORMATO: Async en Slack #agentes-standup

CADA AGENTE REPORTA:
✅ Qué completé ayer
⏳ En qué estoy hoy
🚧 Blockers o problemas
👀 Dependencias esperadas

EJEMPLO:

@architecture-agent:
✅ Diseñé módulo Reviews con todas las relaciones
⏳ Hoy validaré schema con Database Agent
🚧 Ninguno
👀 Espero que Database Agent finalice schema.prisma hoy

@database-agent:
✅ Implementé 10 modelos de Prisma
⏳ Creo migraciones para Reviews hoy
🚧 Prisma version tiene issue con JSON fields - need Security Agent advice
👀 Esperando diseño final de Architecture Agent ✓ Recibido

@api-agent:
✅ Nada (día de descanso)
⏳ Creo endpoints para Restaurants
🚧 Necesito validación de DTOs con Security Agent
👀 Esperando schema finalizado
```

### 3.3 Protocolo de Bloqueos

```
CUANDO UN AGENTE ESTÁ BLOQUEADO:

1. Intenta resolverlo primero (30 min)
2. Si no puede, escala a agente relacionado
3. Si afecta múltiples agentes, escala a Meta Agente
4. Meta Agente toma decisión en < 2 horas

EJEMPLO DE BLOQUEO:

Database Agent en Slack:
"🚨 BLOCKED: Prisma no soporta X feature nativa. 
Alternativas:
A) Migrar a TypeORM (Architecture decision)
B) Usar raw queries (Security risk)
C) Workaround en aplicación (Performance impact)
@meta-agent solicitamos decisión"

Meta Agente:
"Análisis:
- A) 3 días de refactor, no vale la pena
- B) Risk muy alto, no se puede
- C) Impacto mínimo si se usa con cuidado
Decisión: Vamos con C) - implementar workaround
@database-agent crea ADR-004 documentando decisión"
```

---

## 4. QUALITY ASSURANCE GATES

### 4.1 Checks Automatizados en CI/CD

```yaml
name: Agent Quality Gates

on: [pull_request]

jobs:
  qa-gates:
    runs-on: ubuntu-latest
    steps:
      # Linting
      - name: ESLint Check
        run: npm run lint
        if_fails: FAIL
        
      # Type Safety
      - name: TypeScript Check
        run: npm run type-check
        if_fails: FAIL
        
      # Testing
      - name: Unit Tests
        run: npm run test:unit
        if_fails: FAIL
        
      # Coverage
      - name: Coverage Check
        run: npm run test:coverage
        threshold: 80%
        if_below: WARN
        
      # Security
      - name: npm audit
        run: npm audit --audit-level=moderate
        if_fails: FAIL
        
      - name: Snyk Security Scan
        run: snyk test --severity-threshold=high
        if_fails: FAIL
        
      # Code Quality
      - name: SonarQube Analysis
        uses: SonarSource/sonarcloud-github-action
        if_degradation: WARN
        
      # Performance
      - name: Bundle Size Check
        run: npm run bundle-size
        if_increases: 5%
        action: WARN
```

### 4.2 Manual Review Checklist

```
ARCHITECTURE AGENT REVIEW:
├─ [ ] ¿Sigue patrones SOLID?
├─ [ ] ¿Está bien desacoplado?
├─ [ ] ¿Las dependencias son claras?
├─ [ ] ¿Escalable?
└─ [ ] ¿Documentado (ADR si es decisión)?

DATABASE AGENT REVIEW:
├─ [ ] ¿Queries optimizadas?
├─ [ ] ¿Índices apropiados?
├─ [ ] ¿Constraints definidos?
├─ [ ] ¿Migraciones reversibles?
└─ [ ] ¿Sin N+1 queries?

API AGENT REVIEW:
├─ [ ] ¿REST design correcto?
├─ [ ] ¿Status codes apropiados?
├─ [ ] ¿DTOs validados?
├─ [ ] ¿Error handling consistente?
└─ [ ] ¿Documentado en Swagger?

SECURITY AGENT REVIEW:
├─ [ ] ¿JWT/Auth implementado?
├─ [ ] ¿RBAC en place?
├─ [ ] ¿Input validation?
├─ [ ] ¿No hay secrets expuestos?
└─ [ ] ¿Cumple OWASP?

TESTING AGENT REVIEW:
├─ [ ] ¿Coverage >= 80%?
├─ [ ] ¿Tests significativos?
├─ [ ] ¿No tests flaky?
├─ [ ] ¿E2E críticos cubiertos?
└─ [ ] ¿AAA pattern seguido?

DEVOPS AGENT REVIEW:
├─ [ ] ¿Deployment script OK?
├─ [ ] ¿Environment vars seguros?
├─ [ ] ¿Health checks?
├─ [ ] ¿Rollback strategy?
└─ [ ] ¿Logs y monitoring?
```

---

## 5. RESOLUCIÓN DE CONFLICTOS

### 5.1 Matriz de Escalamiento

```
NIVEL 1: Agent-to-Agent
└─→ Dos agentes involucrados resuelven entre ellos
    Ejemplo: Architecture vs Database sobre índices

NIVEL 2: Multi-Agent
└─→ 3+ agentes involucrados, Meta Agente modera
    Ejemplo: Architecture + Database + API sobre performance

NIVEL 3: Architecture Board
└─→ Meta Agente + Arquitectura Principal
    Ejemplo: Cambio significativo de stack

NIVEL 4: Stakeholder
└─→ Requiere input de Product Owner
    Ejemplo: Cambio de requisitos que afecta timeline
```

### 5.2 Proceso de Arbitraje

```
1. Cada parte presenta su posición (5 min cada una)
2. Meta Agente hace preguntas clarificatorias (5 min)
3. Análisis de impacto:
   - Timeline
   - Código
   - Performance
   - Mantenibilidad
4. Decisión: Razones y next steps
5. Documentar en ADR si es significativo
```

---

## 6. MONITOREO Y MÉTRICAS

### 6.1 Dashboard de Agentes (Actualizado Diariamente)

```
┌────────────────────────────────────────────────────┐
│           AGENT PERFORMANCE DASHBOARD               │
├────────────────────────────────────────────────────┤
│                                                    │
│ Architecture Agent          │ 92% Productivity     │
│ ├─ Tasks completadas: 8/10   (80%)                 │
│ ├─ Code review time: 4.2h (Target: 4h)            │
│ ├─ Quality score: 95/100                           │
│ └─ Blocker resolution: 1.5h                        │
│                                                    │
│ Database Agent              │ 85% Productivity     │
│ ├─ Tasks completadas: 6/7    (86%)                 │
│ ├─ Migration tests: 10/10 ✓                        │
│ ├─ Query performance: 98ms (Target: 100ms)        │
│ └─ Index efficiency: 94%                           │
│                                                    │
│ API Agent                   │ 88% Productivity     │
│ ├─ Endpoints implementados: 18/22 (82%)            │
│ ├─ Swagger coverage: 100%                          │
│ ├─ API response time: 156ms (Target: 200ms)       │
│ └─ Validation errors: 0 in staging                │
│                                                    │
│ Testing Agent               │ 90% Productivity     │
│ ├─ Coverage: 82% (Target: 80%) ✓                   │
│ ├─ Test execution: 3.2min (Target: 5min) ✓        │
│ ├─ Flaky test rate: 0.5% (Target: 0%) ⚠          │
│ └─ E2E critical: 100% covered                      │
│                                                    │
│ Security Agent              │ 89% Productivity     │
│ ├─ Security reviews: 7/7 ✓                         │
│ ├─ Vulnerabilities found: 0 ✓                      │
│ ├─ Auth implementation: 100% ✓                     │
│ └─ Compliance checks: ✓                            │
│                                                    │
│ DevOps Agent                │ 87% Productivity     │
│ ├─ Deployments: 4/4 successful ✓                   │
│ ├─ Uptime: 99.95%                                  │
│ ├─ Deployment time: 3.5min                         │
│ └─ Rollback availability: ✓                        │
│                                                    │
│ Meta Agente                 │ 91% Coordination     │
│ ├─ Merged PRs: 12/12 ✓                             │
│ ├─ Avg review time: 8h (Target: 12h)              │
│ ├─ Escalated issues: 2 (both resolved)            │
│ └─ Team satisfaction: 4.5/5                        │
│                                                    │
└────────────────────────────────────────────────────┘
```

### 6.2 Weekly Review Metrics

```
SEMANA ACTUAL: 2025-11-27 to 2025-12-03

Velocity:
├─ Sprint commitments: 45 story points
├─ Completados: 42 (93%)
├─ En progreso: 3
└─ Blocked: 0

Calidad:
├─ Bugs en staging: 0
├─ Code coverage: 82% (↑2%)
├─ Vulnerabilidades: 0 críticas (✓)
├─ Performance regresión: 0 (✓)

Colaboración:
├─ PRs promedio review time: 8h
├─ Escalamientos: 1 (resuelto)
├─ Comunicación lag: < 1h
└─ Knowledge sharing: 2 pairing sessions

Riesgos detectados:
├─ Testing Agent tiene 1 flaky test (ACTION)
├─ Database Agent solicita refactor de indices (PENDING)
└─ DevOps Agent necesita update Docker base image (TODO)
```

---

## 7. GESTIÓN DE RIESGOS EN TIEMPO REAL

### 7.1 Risk Register Dinámico

```json
{
  "riesgos_activos": [
    {
      "id": "RISK-001",
      "titulo": "Migraciones Prisma fallidas en producción",
      "agente_responsable": "Database Agent",
      "probabilidad": "BAJA",
      "impacto": "CRÍTICO",
      "mitigacion": [
        "Todas las migraciones testadas en staging idéntico",
        "Rollback script validado",
        "Backup antes de deploy"
      ],
      "status": "MONITORED",
      "ultimo_review": "2025-11-27"
    },
    {
      "id": "RISK-002",
      "titulo": "N+1 queries en endpoints complejos",
      "agente_responsable": "API Agent + Database Agent",
      "probabilidad": "MEDIA",
      "impacto": "ALTO",
      "mitigacion": [
        "Testing Agent crea tests de performance",
        "Database Agent audita todas las queries",
        "Monitoring en staging"
      ],
      "status": "IN_PROGRESS",
      "ultimo_review": "2025-11-26"
    },
    {
      "id": "RISK-003",
      "titulo": "Secretos expostos en GitHub",
      "agente_responsable": "Security Agent + DevOps Agent",
      "probabilidad": "BAJA",
      "impacto": "CRÍTICO",
      "mitigacion": [
        "git-secrets en pre-commit",
        "GitHub secret scanning habilitado",
        "Auditoría de commits",
        "Educación del equipo"
      ],
      "status": "MONITORED",
      "ultimo_review": "2025-11-25"
    }
  ]
}
```

### 7.2 Incident Response Plan

```
CUANDO SUCEDE UN INCIDENTE EN PRODUCCIÓN:

1. DETECCIÓN (< 2 min)
   └─→ Alert en Datadog/New Relic
       └─→ Slack notification #incidents

2. TRIAGE (< 5 min)
   ├─→ Severity: P1 (Crítico) / P2 (Alto) / P3 (Medio)
   ├─→ Agente responsible investigates
   └─→ Meta Agente convoca guerra room si P1

3. MITIGACIÓN (P1: < 30 min, P2: < 2h)
   ├─→ Rollback si es necesario
   ├─→ Feature flag para disable problema
   └─→ Hotfix en rama dedicada

4. ROOT CAUSE ANALYSIS (< 4h)
   ├─→ Agente especialista identifica causa
   ├─→ Testing Agent crea test para reproduzca
   └─→ Documenta en blameless post-mortem

5. FIX & PREVENTION (< 24h)
   ├─→ Implementar fix permanente
   ├─→ Validar en staging
   ├─→ Deploy a producción
   └─→ Agregar test para prevenir recurrencia

6. POST-MORTEM (< 48h)
   ├─→ Equipo completo analiza
   ├─→ Lecciones aprendidas
   ├─→ Action items para evitar
   └─→ Publicar post-mortem interno
```

---

## 8. DOCUMENTACIÓN Y CONOCIMIENTO

### 8.1 Estructura de Documentación

```
/docs
├── /e4
│   ├── db_model.md                (Database Agent)
│   ├── api_contracts.md           (API Agent)
│   ├── architecture_nest.md       (Architecture Agent)
│   ├── agents_framework.md        (Meta Agente)
│   ├── agents_operations.md       (Este archivo)
│   ├── security_guidelines.md     (Security Agent)
│   └── deployment_guide.md        (DevOps Agent)
│
├── /architecture
│   ├── decisions/
│   │   ├── ADR-001-orm-choice.md
│   │   ├── ADR-002-module-structure.md
│   │   └── ADR-NNN-...md
│   │
│   └── diagrams/
│       ├── entity-relationship.md
│       ├── module-dependencies.md
│       └── deployment-architecture.md
│
├── /guides
│   ├── setup.md
│   ├── contributing.md
│   ├── testing-guide.md
│   └── deployment-guide.md
│
└── /runbooks
    ├── incident-response.md
    ├── database-recovery.md
    └── deployment-rollback.md
```

### 8.2 Convención de ADR (Architectural Decision Records)

```markdown
# ADR-NNN: [Título de la Decisión]

**Fecha**: 2025-11-27
**Agente Responsable**: Architecture Agent
**Status**: Accepted | Pending | Superseded

## Contexto

¿Cuál era el problema?

## Decisión

¿Qué decidimos hacer?

## Razones

1. Razón 1
2. Razón 2
3. Razón 3

## Consecuencias

### Positivas
- Beneficio 1
- Beneficio 2

### Negativas
- Trade-off 1
- Trade-off 2

## Alternativas Consideradas

- Alternativa A: [Ventajas/Desventajas]
- Alternativa B: [Ventajas/Desventajas]

## Follow-up

- Task 1
- Task 2
```

---

## 9. VELOCIDAD DE ENTREGA

### 9.1 Objetivos de Tiempo

```
TAREA TÍPICA POR AGENTE:

Pequeña (< 4h):
├─→ 1-2 cambios, 1 archivo
├─→ Design review: 30 min
├─→ Code review: 1h
├─→ Testing: 1h
└─→ Total: 3-4h ✓

Mediana (4-12h):
├─→ 3-5 cambios, 3-5 archivos
├─→ Design review: 1h
├─→ Implementation: 4-6h
├─→ Code review: 2h
├─→ Testing: 2-3h
└─→ Total: 9-12h ✓

Grande (12-32h):
├─→ 5+ cambios, 10+ archivos
├─→ Design review: 2h
├─→ Implementation: 12h
├─→ Code review: 4h
├─→ Testing: 6-8h
└─→ Integration: 2-4h
└─→ Total: 26-32h (2-3 días) ✓
```

### 9.2 Throughput Mensual

```
Meta: 45 story points / sprint (80 horas de trabajo)
Equipo: 6 agentes especializados
Sprints: 2 sprints / mes

DISTRIBUCIÓN TÍPICA:
├─ Architecture: 12 story points (20%)
├─ Database: 10 story points (22%)
├─ API: 12 story points (27%)
├─ Security: 4 story points (9%)
├─ Testing: 5 story points (11%)
└─ DevOps: 2 story points (4%)

MÉTRICAS HISTÓRICAS (últimas 3 sprints):
Sprint 1: 42 points (93% completion)
Sprint 2: 45 points (100% completion)
Sprint 3: 43 points (96% completion)
Promedio: 43.3 points/sprint
```

---

## 10. HERRAMIENTAS Y TECNOLOGÍA

### 10.1 Stack de Herramientas Compartidas

```
COMUNICACIÓN:
├─ Slack (síncrono)
├─ GitHub Issues (tracking)
└─ GitHub Discussions (async)

CONTROL DE CÓDIGO:
├─ Git (versionamiento)
├─ GitHub (repository)
├─ GitHub Actions (CI/CD)
└─ pre-commit (local validation)

MONITOREO DE CALIDAD:
├─ SonarQube (code quality)
├─ Snyk (security scanning)
├─ Dependabot (dependency updates)
└─ CodeQL (static analysis)

TESTING:
├─ Jest (unitario)
├─ Supertest (E2E)
├─ Artillery (performance)
└─ OWASP ZAP (security)

DEPLOYMENT:
├─ Docker (containerización)
├─ Docker Compose (local)
├─ Kubernetes (orchestration)
└─ ArgoCD (GitOps)

MONITOREO:
├─ Datadog (logs, metrics, traces)
├─ Grafana (dashboards)
├─ Prometheus (metrics)
└─ AlertManager (alertas)
```

### 10.2 Integración GitHub

```yaml
# .github/workflows/agent-quality-gates.yml

name: Agent Quality Gates

on:
  pull_request:
    branches: [main, develop]
  push:
    branches: [main]

permissions:
  pull-requests: write
  contents: read
  checks: write

jobs:
  architecture-agent:
    name: Architecture Validation
    runs-on: ubuntu-latest
    # ...

  database-agent:
    name: Database Validation
    runs-on: ubuntu-latest
    # ...

  api-agent:
    name: API Validation
    runs-on: ubuntu-latest
    # ...

  security-agent:
    name: Security Scan
    runs-on: ubuntu-latest
    # ...

  testing-agent:
    name: Test Coverage
    runs-on: ubuntu-latest
    # ...

  devops-agent:
    name: Deployment Check
    runs-on: ubuntu-latest
    # ...

  meta-agent:
    name: Final Approval
    needs: [architecture-agent, database-agent, api-agent, security-agent, testing-agent, devops-agent]
    runs-on: ubuntu-latest
    # Merge automático si todos pasan
```

---

## 11. ENTRENAMIENTO Y CONOCIMIENTO

### 11.1 Pairing Sessions

```
FORMATO: 2x por semana, 1h cada una

Objetivo: Transferencia de conocimiento entre agentes

SESIONES TÍPICAS:
├─ Architecture + Database: Schema discussions
├─ API + Security: Endpoint security
├─ Testing + DevOps: Test automation
└─ Meta Agente + Todos: Complex decisions
```

### 11.2 Learning Resources

Cada agente tiene acceso a:
- Documentación oficial de su stack
- Libros especializados
- Cursos online (Pluralsight, Udemy)
- Comunidades especializadas
- Código abierto ejemplos

---

## 12. CONCLUSIÓN

Este documento de **operaciones de agentes** proporciona:

✅ **Estructura clara** de cómo trabajan juntos  
✅ **Procesos definidos** para evitar caos  
✅ **Automatización máxima** mediante CI/CD  
✅ **Transparencia total** con dashboards  
✅ **Escalamiento eficiente** de problemas  
✅ **Velocidad sin sacrificar calidad**  

El equipo de agentes está listo para **desarrollar a alta velocidad** manteniendo **estándares de excelencia**.

---

**Documento**: agents_operations.md  
**Versión**: 1.0  
**Próximas mejoras**: Templates específicos por agente, scripts de automatización
