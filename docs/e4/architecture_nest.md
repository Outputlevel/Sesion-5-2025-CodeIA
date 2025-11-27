# Arquitectura NestJS - Sistema de Restaurantes

## Descripción General

Arquitectura modular escalable para sistema de gestión de restaurantes usando NestJS. Implementa patrones de diseño enterprise: módulos, controladores, servicios, DTOs y responsabilidad única.

**Framework**: NestJS 10.x  
**Runtime**: Node.js 22.x  
**Database**: PostgreSQL + Prisma ORM  
**Testing**: Jest + Supertest  
**Autenticación**: JWT  
**Validación**: Class Validator + Class Transformer  
**Documentación**: Swagger/OpenAPI

---

## 1. Estructura de Árbol del Proyecto

```
src/
├── common/
│   ├── decorators/
│   │   ├── auth.decorator.ts
│   │   ├── user.decorator.ts
│   │   ├── roles.decorator.ts
│   │   └── validate-uuid.decorator.ts
│   ├── filters/
│   │   ├── http-exception.filter.ts
│   │   └── validation-exception.filter.ts
│   ├── guards/
│   │   ├── auth.guard.ts
│   │   ├── jwt.guard.ts
│   │   └── roles.guard.ts
│   ├── interceptors/
│   │   ├── response.interceptor.ts
│   │   ├── logging.interceptor.ts
│   │   └── transform.interceptor.ts
│   ├── middleware/
│   │   ├── logger.middleware.ts
│   │   └── request-id.middleware.ts
│   ├── pipes/
│   │   ├── validation.pipe.ts
│   │   └── parse-uuid.pipe.ts
│   ├── utils/
│   │   ├── logger.util.ts
│   │   ├── pagination.util.ts
│   │   └── error-handler.util.ts
│   └── types/
│       ├── request.types.ts
│       └── response.types.ts
│
├── config/
│   ├── database.config.ts
│   ├── jwt.config.ts
│   ├── app.config.ts
│   └── env.validation.ts
│
├── prisma/
│   ├── schema.prisma
│   ├── migrations/
│   │   ├── 20241127120000_init/migration.sql
│   │   └── ...
│   └── seeders/
│       ├── restaurants.seed.ts
│       ├── menus.seed.ts
│       └── index.ts
│
├── modules/
│   ├── auth/
│   │   ├── auth.module.ts
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.service.spec.ts
│   │   ├── jwt.strategy.ts
│   │   ├── dtos/
│   │   │   ├── login.dto.ts
│   │   │   ├── register.dto.ts
│   │   │   ├── refresh-token.dto.ts
│   │   │   └── auth-response.dto.ts
│   │   └── interfaces/
│   │       ├── jwt-payload.interface.ts
│   │       └── auth-response.interface.ts
│   │
│   ├── restaurants/
│   │   ├── restaurants.module.ts
│   │   ├── controllers/
│   │   │   ├── restaurants.controller.ts
│   │   │   └── restaurants.controller.spec.ts
│   │   ├── services/
│   │   │   ├── restaurants.service.ts
│   │   │   └── restaurants.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-restaurant.dto.ts
│   │   │   ├── update-restaurant.dto.ts
│   │   │   ├── restaurant-response.dto.ts
│   │   │   └── pagination.dto.ts
│   │   └── interfaces/
│   │       └── restaurant.interface.ts
│   │
│   ├── locations/
│   │   ├── locations.module.ts
│   │   ├── controllers/
│   │   │   └── locations.controller.ts
│   │   ├── services/
│   │   │   ├── locations.service.ts
│   │   │   └── locations.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-location.dto.ts
│   │   │   └── location-response.dto.ts
│   │   └── interfaces/
│   │       └── location.interface.ts
│   │
│   ├── menus/
│   │   ├── menus.module.ts
│   │   ├── controllers/
│   │   │   └── menus.controller.ts
│   │   ├── services/
│   │   │   ├── menus.service.ts
│   │   │   └── menus.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-menu.dto.ts
│   │   │   ├── update-menu.dto.ts
│   │   │   ├── menu-response.dto.ts
│   │   │   └── menu-item.dto.ts
│   │   └── interfaces/
│   │       └── menu.interface.ts
│   │
│   ├── menu-items/
│   │   ├── menu-items.module.ts
│   │   ├── controllers/
│   │   │   └── menu-items.controller.ts
│   │   ├── services/
│   │   │   ├── menu-items.service.ts
│   │   │   └── menu-items.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-menu-item.dto.ts
│   │   │   ├── update-menu-item.dto.ts
│   │   │   └── menu-item-response.dto.ts
│   │   └── interfaces/
│   │       └── menu-item.interface.ts
│   │
│   ├── ingredients/
│   │   ├── ingredients.module.ts
│   │   ├── controllers/
│   │   │   └── ingredients.controller.ts
│   │   ├── services/
│   │   │   ├── ingredients.service.ts
│   │   │   └── ingredients.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-ingredient.dto.ts
│   │   │   └── ingredient-response.dto.ts
│   │   └── interfaces/
│   │       └── ingredient.interface.ts
│   │
│   ├── employees/
│   │   ├── employees.module.ts
│   │   ├── controllers/
│   │   │   └── employees.controller.ts
│   │   ├── services/
│   │   │   ├── employees.service.ts
│   │   │   └── employees.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-employee.dto.ts
│   │   │   ├── update-employee.dto.ts
│   │   │   └── employee-response.dto.ts
│   │   └── interfaces/
│   │       └── employee.interface.ts
│   │
│   ├── customers/
│   │   ├── customers.module.ts
│   │   ├── controllers/
│   │   │   └── customers.controller.ts
│   │   ├── services/
│   │   │   ├── customers.service.ts
│   │   │   └── customers.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── register-customer.dto.ts
│   │   │   ├── customer-response.dto.ts
│   │   │   └── customer-profile.dto.ts
│   │   └── interfaces/
│   │       └── customer.interface.ts
│   │
│   ├── orders/
│   │   ├── orders.module.ts
│   │   ├── controllers/
│   │   │   └── orders.controller.ts
│   │   ├── services/
│   │   │   ├── orders.service.ts
│   │   │   ├── orders.service.spec.ts
│   │   │   ├── order-status.service.ts
│   │   │   ├── order-validation.service.ts
│   │   │   └── order-validation.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-order.dto.ts
│   │   │   ├── update-order-status.dto.ts
│   │   │   ├── cancel-order.dto.ts
│   │   │   ├── order-item.dto.ts
│   │   │   └── order-response.dto.ts
│   │   └── interfaces/
│   │       ├── order.interface.ts
│   │       └── order-item.interface.ts
│   │
│   ├── reviews/
│   │   ├── reviews.module.ts
│   │   ├── controllers/
│   │   │   └── reviews.controller.ts
│   │   ├── services/
│   │   │   ├── reviews.service.ts
│   │   │   ├── reviews.service.spec.ts
│   │   │   ├── review-analytics.service.ts
│   │   │   └── review-analytics.service.spec.ts
│   │   ├── dtos/
│   │   │   ├── create-review.dto.ts
│   │   │   ├── update-review.dto.ts
│   │   │   ├── review-response.dto.ts
│   │   │   └── review-analytics.dto.ts
│   │   └── interfaces/
│   │       └── review.interface.ts
│   │
│   └── health/
│       ├── health.module.ts
│       ├── health.controller.ts
│       └── health.service.ts
│
├── app.module.ts
└── main.ts
```

---

## 2. Módulos Principales

### 2.1 Módulo de Autenticación (AuthModule)

**Responsabilidades:**
- Autenticación de usuarios (login, logout)
- Generación y validación de JWT
- Refresh de tokens
- Estrategia de JWT

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `AuthController` | Endpoints de login, registro, refresh |
| `AuthService` | Lógica de autenticación, hasheo, tokens |
| `JwtStrategy` | Validación de JWT (Passport) |
| DTOs | Login, Register, RefreshToken, AuthResponse |

**Dependencias:**
- `CustomersModule` (para crear clientes)
- JWT Service (NestJS)
- Bcrypt (hashing)

**Estructura Prisma:**
- `PrismaService` inyectado para acceso a BD
- Operaciones sin repositorio (directo al cliente Prisma)

---

### 2.2 Módulo de Restaurantes (RestaurantsModule)

**Responsabilidades:**
- CRUD de restaurantes
- Gestión de ubicaciones
- Cálculo de ratings
- Búsquedas y filtrados

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `RestaurantsController` | Endpoints de restaurantes |
| `RestaurantsService` | Lógica de CRUD, ratings, búsquedas |
| `LocationsService` | CRUD de ubicaciones |
| DTOs | CreateRestaurant, UpdateRestaurant, RestaurantResponse |

**Dependencias:**
- `OrdersModule` (para cálculos de ratings)
- `ReviewsModule` (para ratings)
- TypeORM

**Patrones:**
- Paginación estándar
- Búsqueda fuzzy (trigram en BD)
- Soft deletes (si aplica)

---

### 2.3 Módulo de Menús (MenusModule)

**Responsabilidades:**
- Gestión de menús y versiones
- CRUD de items de menú
- Validación de disponibilidad
- Gestión de ingredientes

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `MenusController` | Endpoints de menús |
| `MenusService` | Lógica de menús, versionado |
| `MenuItemsController` | Endpoints de items |
| `MenuItemsService` | CRUD de items, validaciones |
| `IngredientsService` | Gestión de ingredientes |
| DTOs | CreateMenu, MenuItem, MenuResponse |

**Dependencias:**
- `RestaurantsModule` (FK a restaurantes)

**Patrones:**
- Versionado de menús (valid_from, valid_to)
- Validación de restricciones dietéticas
- Cálculo de información nutricional

---

### 2.4 Módulo de Empleados (EmployeesModule)

**Responsabilidades:**
- Gestión de empleados por restaurante
- Cambios de rol y estado laboral
- Validación de emails únicos

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `EmployeesController` | Endpoints de empleados |
| `EmployeesService` | CRUD, validaciones, búsquedas por rol |
| DTOs | CreateEmployee, UpdateEmployee, EmployeeResponse |

**Dependencias:**
- `RestaurantsModule` (FK a restaurantes)
- `OrdersModule` (para validar asignaciones)

---

### 2.5 Módulo de Clientes (CustomersModule)

**Responsabilidades:**
- Registro y gestión de clientes
- Perfil de usuario
- Programa de lealtad
- Historial de órdenes

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `CustomersController` | Endpoints de clientes |
| `CustomersService` | CRUD, registro, búsquedas |
| `LoyaltyService` | Gestión del programa de lealtad |
| DTOs | RegisterCustomer, CustomerResponse, CustomerProfile |

**Dependencias:**
- `AuthModule` (para registro integrado)

**Patrones:**
- Generación de loyalty_number automática
- Estadísticas de cliente (total_orders, total_spent)

---

### 2.6 Módulo de Órdenes (OrdersModule)

**Responsabilidades:**
- Creación y gestión de órdenes
- Flujo de estados de la orden
- Cálculo de totales y descuentos
- Asignación de empleados
- Cancelación y reembolsos

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `OrdersController` | Endpoints de órdenes |
| `OrdersService` | CRUD de órdenes |
| `OrderStatusService` | Transiciones de estado |
| `OrderValidationService` | Validaciones (items disponibles, cliente, etc.) |
| `OrderCalculationService` | Cálculo de totales, impuestos, descuentos |
| DTOs | CreateOrder, UpdateOrderStatus, CancelOrder, OrderResponse |

**Dependencias:**
- `RestaurantsModule` (FK a restaurantes)
- `CustomersModule` (FK a clientes)
- `MenuItemsModule` (items del menú)
- `EmployeesModule` (asignaciones)

**Patrones:**
- State Machine para transiciones
- Validación de disponibilidad de items
- Cálculo de delivery time estimado
- Soft deletes en órdenes

---

### 2.7 Módulo de Reseñas (ReviewsModule)

**Responsabilidades:**
- Creación de reseñas
- Cálculo de ratings promedio
- Análisis de sentimiento (opcional)
- Reporte de reseñas

**Componentes:**

| Componente | Responsabilidad |
|------------|-----------------|
| `ReviewsController` | Endpoints de reseñas |
| `ReviewsService` | CRUD de reseñas |
| `ReviewAnalyticsService` | Cálculos de promedio, distribución |
| DTOs | CreateReview, UpdateReview, ReviewResponse, ReviewAnalytics |

**Dependencias:**
- `RestaurantsModule` (FK a restaurantes)
- `CustomersModule` (FK a clientes)

**Patrones:**
- Índice único por customer-restaurant-día
- Caché de ratings (actualizar cada hora)

---

## 3. Detalle de Módulos

### 3.1 AuthModule - Estructura Completa

```typescript
// auth.module.ts
@Module({
  imports: [
    JwtModule.registerAsync({
      useFactory: (configService: ConfigService) => ({
        secret: configService.get<string>('JWT_SECRET'),
        signOptions: { expiresIn: '1h' }
      }),
      inject: [ConfigService]
    }),
    PassportModule,
    CustomersModule
  ],
  controllers: [AuthController],
  providers: [AuthService, JwtStrategy, PrismaService],
  exports: [AuthService, JwtModule]
})
export class AuthModule {}
```

**AuthController:**
- `POST /auth/login` → AuthService.login()
- `POST /auth/register` → AuthService.register()
- `POST /auth/refresh` → AuthService.refreshToken()

**AuthService (con Prisma):**
- `login(email, password)` → validar credenciales con `this.prisma.customer.findUnique()`
- `register(registerDto)` → crear cliente con `this.prisma.customer.create()`
- `refreshToken(refreshToken)` → generar nuevo access token
- `validateToken(token)` → verificar y decodificar JWT
- `hashPassword(password)` → bcrypt hash
- `comparePassword(password, hash)` → bcrypt compare

---

### 3.2 RestaurantsModule - Estructura Completa

```typescript
// restaurants.module.ts
@Module({
  imports: [ReviewsModule],
  controllers: [RestaurantsController],
  providers: [RestaurantsService, LocationsService, PrismaService],
  exports: [RestaurantsService]
})
export class RestaurantsModule {}
```

**RestaurantsController:**
- `GET /restaurants` → listar con paginación y filtros
- `GET /restaurants/:id` → obtener detalle
- `POST /restaurants` → crear (solo admin)
- `PATCH /restaurants/:id` → actualizar (solo admin)
- `DELETE /restaurants/:id` → eliminar (solo admin)

**RestaurantsService (con Prisma):**
- `findAll(filters, pagination)` → `this.prisma.restaurant.findMany()`
- `findById(id)` → `this.prisma.restaurant.findUnique({ include: { locations: true } })`
- `create(createDto)` → `this.prisma.restaurant.create()` + ubicación
- `update(id, updateDto)` → `this.prisma.restaurant.update()`
- `delete(id)` → `this.prisma.restaurant.delete()` con validaciones
- `getAverageRating(restaurantId)` → agregación con Prisma raw query
- `getRestaurantStats(restaurantId)` → estadísticas

**LocationsService (con Prisma):**
- `create(restaurantId, locationDto)` → `this.prisma.location.create()`
- `update(locationId, updateDto)` → `this.prisma.location.update()`
- `delete(locationId)` → `this.prisma.location.delete()`
- `findByRestaurant(restaurantId)` → `this.prisma.location.findMany()`

---

### 3.3 MenusModule - Estructura Completa

```typescript
// menus.module.ts
@Module({
  imports: [RestaurantsModule],
  controllers: [MenusController, MenuItemsController],
  providers: [MenusService, MenuItemsService, IngredientsService, PrismaService],
  exports: [MenusService, MenuItemsService]
})
export class MenusModule {}
```

**MenusController:**
- `GET /restaurants/:restaurantId/menus` → listar menús
- `POST /restaurants/:restaurantId/menus` → crear menú
- `PATCH /restaurants/:restaurantId/menus/:menuId` → actualizar
- `DELETE /restaurants/:restaurantId/menus/:menuId` → eliminar

**MenusService (con Prisma):**
- `findByRestaurant(restaurantId, filters)` → `this.prisma.menu.findMany()` con validez de fechas
- `findById(menuId)` → `this.prisma.menu.findUnique({ include: { items: true } })`
- `create(restaurantId, createDto)` → `this.prisma.menu.create()`
- `update(menuId, updateDto)` → `this.prisma.menu.update()`
- `delete(menuId)` → `this.prisma.menu.delete()`
- `getActiveMenus(restaurantId, date)` → filtro temporal con Prisma

**MenuItemsController:**
- `GET /menus/:menuId/items` → listar items
- `POST /menus/:menuId/items` → crear item
- `PATCH /menus/:menuId/items/:itemId` → actualizar
- `DELETE /menus/:menuId/items/:itemId` → eliminar

**MenuItemsService (con Prisma):**
- `findByMenu(menuId, filters)` → `this.prisma.menuItem.findMany()`
- `findById(itemId)` → `this.prisma.menuItem.findUnique({ include: { ingredients: true } })`
- `create(menuId, createDto)` → `this.prisma.menuItem.create()`
- `update(itemId, updateDto)` → `this.prisma.menuItem.update()`
- `delete(itemId)` → `this.prisma.menuItem.delete()`
- `getAvailable(menuId)` → items con status 'available'

**IngredientsService (con Prisma):**
- `findAll(search)` → `this.prisma.ingredient.findMany()` con búsqueda
- `findById(id)` → `this.prisma.ingredient.findUnique()`
- `create(createDto)` → `this.prisma.ingredient.create()`
- `addToRecipe(menuItemId, ingredients)` → `this.prisma.recipe.createMany()`
- `removeFromRecipe(menuItemId, ingredientId)` → `this.prisma.recipe.delete()`

---

### 3.4 OrdersModule - Estructura Completa

```typescript
// orders.module.ts
@Module({
  imports: [
    RestaurantsModule,
    CustomersModule,
    MenuItemsModule,
    EmployeesModule
  ],
  controllers: [OrdersController],
  providers: [
    OrdersService,
    OrderStatusService,
    OrderValidationService,
    OrderCalculationService,
    PrismaService
  ],
  exports: [OrdersService]
})
export class OrdersModule {}
```

**OrdersController:**
- `POST /orders` → crear orden
- `GET /orders/:id` → obtener orden
- `GET /customers/me/orders` → órdenes del cliente
- `GET /restaurants/:restaurantId/orders` → órdenes del restaurante (admin)
- `PATCH /orders/:id/status` → actualizar estado
- `POST /orders/:id/cancel` → cancelar orden
- `POST /orders/:id/assign` → asignar empleado

**OrdersService (con Prisma + transacciones):**
- `create(customerId, createDto)` → `this.prisma.$transaction()` para ACID
- `findById(id)` → `this.prisma.order.findUnique({ include: { items: true, assignments: true } })`
- `findByCustomer(customerId, filters)` → `this.prisma.order.findMany()`
- `findByRestaurant(restaurantId, filters)` → `this.prisma.order.findMany()`
- `update(id, updateDto)` → `this.prisma.order.update()`

**OrderStatusService (con Prisma):**
- `updateStatus(orderId, newStatus)` → cambiar estado con validación de transición
- `validateTransition(currentStatus, newStatus)` → lógica state machine
- `getValidNextStates(currentStatus)` → estados permitidos
- `notifyStatusChange(order, newStatus)` → notificaciones (webhook/event)

**OrderValidationService (con Prisma):**
- `validateItems(restaurantId, items)` → verificar disponibilidad
- `validateCustomer(customerId)` → cliente activo: `this.prisma.customer.findUnique()`
- `validateRestaurant(restaurantId)` → restaurante activo
- `validateDiscountCode(code)` → descuento válido (si aplica)
- `validateDeliveryType(restaurantId, deliveryType)` → tipo de entrega

**OrderCalculationService:**
- `calculateSubtotal(items)` → suma de precios
- `calculateTax(subtotal, restaurantId)` → cálculo de impuestos
- `calculateDiscount(subtotal, code)` → aplicar descuentos
- `calculateFinalTotal(subtotal, tax, discount)` → total final
- `estimateDeliveryTime(restaurantId, deliveryType)` → tiempo estimado

---

### 3.5 ReviewsModule - Estructura Completa

```typescript
// reviews.module.ts
@Module({
  imports: [
    RestaurantsModule,
    CustomersModule,
    CacheModule.register()
  ],
  controllers: [ReviewsController],
  providers: [ReviewsService, ReviewAnalyticsService, PrismaService],
  exports: [ReviewsService]
})
export class ReviewsModule {}
```

**ReviewsController:**
- `POST /restaurants/:restaurantId/reviews` → crear reseña
- `GET /restaurants/:restaurantId/reviews` → listar reseñas
- `PATCH /restaurants/:restaurantId/reviews/:reviewId` → actualizar
- `DELETE /restaurants/:restaurantId/reviews/:reviewId` → eliminar

**ReviewsService (con Prisma):**
- `create(customerId, restaurantId, createDto)` → `this.prisma.review.create()`
- `findByRestaurant(restaurantId, filters)` → `this.prisma.review.findMany()`
- `update(reviewId, updateDto)` → `this.prisma.review.update()` (solo autor)
- `delete(reviewId)` → `this.prisma.review.delete()` (solo autor/admin)
- `findById(reviewId)` → `this.prisma.review.findUnique()`

**ReviewAnalyticsService (con Prisma aggregation):**
- `getAverageRating(restaurantId)` → `this.prisma.review.aggregate({ _avg: { rating } })`
- `getRatingDistribution(restaurantId)` → agregación por rating
- `getReviewStats(restaurantId)` → estadísticas completas
- `getTrendingReviews(limit)` → reseñas recientes ordenadas
- `updateRatingCache(restaurantId)` → actualizar caché de ratings

---

## 4. DTOs (Data Transfer Objects)

### 4.1 Estructura de DTOs

**Patrón:**
- Un DTO por acción (Create, Update, Response)
- Uso de class-validator decorators
- Class-transformer para mapeos
- Documentación con @ApiProperty

**Ejemplo - CreateRestaurantDto:**

```typescript
export class LocationDto {
  @IsString()
  @MinLength(1)
  @MaxLength(500)
  @ApiProperty()
  address: string;

  @IsString()
  @MinLength(1)
  @MaxLength(100)
  @ApiProperty()
  city: string;

  @IsLatitude()
  @IsOptional()
  @ApiProperty()
  latitude?: number;

  @IsLongitude()
  @IsOptional()
  @ApiProperty()
  longitude?: number;
}

export class CreateRestaurantDto {
  @IsString()
  @MinLength(1)
  @MaxLength(255)
  @IsUnique({ tableName: 'restaurants', column: 'name' })
  @ApiProperty()
  name: string;

  @IsOptional()
  @IsString()
  @ApiProperty()
  description?: string;

  @IsEmail()
  @ApiProperty()
  email: string;

  @IsPhoneNumber()
  @IsOptional()
  @ApiProperty()
  phone?: string;

  @Type(() => LocationDto)
  @ValidateNested()
  @ApiProperty({ type: LocationDto })
  location: LocationDto;
}
```

### 4.2 DTOs por Módulo

| Módulo | DTOs |
|--------|------|
| Auth | LoginDto, RegisterDto, RefreshTokenDto, AuthResponseDto |
| Restaurants | CreateRestaurantDto, UpdateRestaurantDto, RestaurantResponseDto |
| Menus | CreateMenuDto, UpdateMenuDto, MenuResponseDto |
| Menu Items | CreateMenuItemDto, UpdateMenuItemDto, MenuItemResponseDto |
| Employees | CreateEmployeeDto, UpdateEmployeeDto, EmployeeResponseDto |
| Customers | RegisterCustomerDto, CustomerResponseDto, CustomerProfileDto |
| Orders | CreateOrderDto, UpdateOrderStatusDto, CancelOrderDto, OrderResponseDto |
| Reviews | CreateReviewDto, UpdateReviewDto, ReviewResponseDto |

---

## 5. Patrones de Arquitectura

### 5.1 Inyección de Dependencias

```typescript
// restaurants.controller.ts
@Controller('restaurants')
@ApiTags('Restaurants')
export class RestaurantsController {
  constructor(
    private readonly restaurantsService: RestaurantsService,
    private readonly logger: LoggerService
  ) {}
}
```

### 5.2 Inyección de Configuración

```typescript
// auth.service.ts
export class AuthService {
  constructor(
    private readonly jwtService: JwtService,
    @Inject(ConfigService) private configService: ConfigService
  ) {}
}
```

### 5.3 Transacciones

```typescript
// orders.service.ts
@Transactional()
async createOrder(customerId: string, createDto: CreateOrderDto) {
  // Operaciones ACID
}
```

### 5.4 Caché

```typescript
// reviews.service.ts
@Cacheable({ ttl: 3600 })
async getAverageRating(restaurantId: string) {
  // Cálculo costoso
}
```

---

## 6. Guardias y Decoradores

### 6.1 Guards de Autenticación

```typescript
// jwt.guard.ts
@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}

// roles.guard.ts
@Injectable()
export class RolesGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const roles = this.reflector.get<string[]>('roles', context.getHandler());
    const request = context.switchToHttp().getRequest();
    const user = request.user;
    return roles.includes(user.role);
  }
}
```

### 6.2 Decoradores Personalizados

```typescript
// @Auth() - requiere autenticación
// @Roles('admin') - requiere rol específico
// @User() - inyecta usuario actual
// @ValidateUUID() - valida UUID

@UseGuards(JwtAuthGuard, RolesGuard)
@Roles('admin')
@Post()
create(@Body() createDto: CreateRestaurantDto, @User() user) {
  // Lógica
}
```

---

## 7. Validación de Datos

### 7.1 Pipe de Validación Global

```typescript
// main.ts
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,
    forbidNonWhitelisted: true,
    transform: true,
    transformOptions: {
      enableImplicitConversion: true
    }
  })
);
```

### 7.2 Validadores Personalizados

```typescript
// validators/is-unique.validator.ts
@ValidatorConstraint()
export class IsUniqueConstraint implements ValidatorConstraintInterface {
  async validate(value: string, args: ValidationArguments) {
    // Verificar unicidad en BD
  }
}

@registerDecorator({
  name: 'isUnique',
  target: Object.prototype.constructor,
  validator: IsUniqueConstraint
})
export function IsUnique(options: IsUniqueOptions) {
  return function(target: Object, propertyName: string) {
    // Decorador
  };
}
```

---

## 8. Manejo de Excepciones

### 8.1 Filtro Global de Excepciones

```typescript
// http-exception.filter.ts
@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const response = host.switchToHttp().getResponse();
    
    return response.status(exception.getStatus()).json({
      success: false,
      error: {
        code: exception.constructor.name,
        message: exception.getResponse()
      }
    });
  }
}

// main.ts
app.useGlobalFilters(new HttpExceptionFilter());
```

### 8.2 Excepciones Personalizadas

```typescript
// exceptions/restaurant-not-found.exception.ts
export class RestaurantNotFoundException extends NotFoundException {
  constructor(restaurantId: string) {
    super({
      code: 'RESTAURANT_NOT_FOUND',
      message: `Restaurante ${restaurantId} no encontrado`,
      details: { restaurantId }
    });
  }
}
```

---

## 9. Interceptadores

### 9.1 Interceptador de Respuesta

```typescript
// response.interceptor.ts
@Injectable()
export class ResponseInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler) {
    return next.handle().pipe(
      map(data => ({
        success: true,
        data,
        meta: {
          timestamp: new Date().toISOString()
        }
      }))
    );
  }
}
```

### 9.2 Interceptador de Logging

```typescript
// logging.interceptor.ts
@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler) {
    const start = Date.now();
    const request = context.switchToHttp().getRequest();
    
    return next.handle().pipe(
      tap(() => {
        this.logger.log(
          `${request.method} ${request.url} - ${Date.now() - start}ms`
        );
      })
    );
  }
}
```

---

## 10. Responsabilidades por Capa

### 10.1 Controller (Capa de Presentación)

**Responsabilidades:**
- ✓ Recibir requests HTTP
- ✓ Validar datos de entrada (decoradores)
- ✓ Llamar servicios
- ✓ Formatear respuestas HTTP
- ✓ Manejar códigos de estado

**Prohibido:**
- ✗ Lógica de negocio
- ✗ Acceso directo a BD
- ✗ Validaciones complejas

**Ejemplo:**

```typescript
@Post()
@UseGuards(JwtAuthGuard)
async create(
  @Body() createDto: CreateOrderDto,
  @User() user: UserPayload
): Promise<OrderResponseDto> {
  return this.ordersService.create(user.sub, createDto);
}
```

---

### 10.2 Service (Capa de Negocio)

**Responsabilidades:**
- ✓ Lógica de negocio
- ✓ Orquestación de operaciones
- ✓ Validaciones complejas
- ✓ Llamadas a repositorios
- ✓ Transacciones

**Prohibido:**
- ✗ Formato HTTP
- ✗ Acceso directo a request/response
- ✗ Manejo de JWT (auth service solo)

**Ejemplo:**

```typescript
async create(customerId: string, createDto: CreateOrderDto) {
  // Validar
  await this.orderValidationService.validate(createDto);
  
  // Calcular
  const totals = this.orderCalculationService.calculate(createDto);
  
  // Crear
  const order = await this.ordersRepository.create({
    customerId,
    ...createDto,
    ...totals
  });
  
  // Asignar
  await this.assignDefaultEmployee(order);
  
  return order;
}
```

---

### 10.3 Repository (Capa de Datos)

**Responsabilidades:**
- ✓ Operaciones CRUD
- ✓ Queries a BD
- ✓ Mapeo de entidades
- ✓ Transacciones (nivel BD)

**Prohibido:**
- ✗ Lógica de negocio
- ✗ Llamadas a servicios externos

**Ejemplo:**

```typescript
@EntityRepository(Order)
export class OrderRepository extends Repository<Order> {
  async findWithDetails(id: string): Promise<Order> {
    return this.findOne({
      where: { id },
      relations: ['items', 'customer', 'restaurant']
    });
  }
}
```

---

## 11. Flujo de Request

```
HTTP Request
    ↓
Middleware (Logger, RequestId)
    ↓
Route Handler
    ↓
Controller
  ├─ Decoradores (Auth, Roles)
  ├─ Guards (Validación)
  ├─ Pipes (Validación de datos)
  └─ Método
    ↓
Service
  ├─ Validaciones
  ├─ Lógica de negocio
  ├─ Repositorios
  └─ Transacciones
    ↓
Repository (TypeORM)
  ├─ Queries
  └─ BD (PostgreSQL)
    ↓
Response
  ├─ Interceptador (Formateo)
  ├─ Filtro de excepciones (Errores)
  └─ HTTP Response

```

---

## 12. Configuración del Módulo Principal

```typescript
// app.module.ts
@Module({
  imports: [
    ConfigModule.forRoot({
      isGlobal: true,
      envFilePath: '.env',
      validate: envValidation
    }),
    // Módulos de negocio
    AuthModule,
    RestaurantsModule,
    MenusModule,
    EmployeesModule,
    CustomersModule,
    OrdersModule,
    ReviewsModule,
    HealthModule
  ],
  controllers: [AppController],
  providers: [AppService, LoggerService, PrismaService]
})
export class AppModule {}

// PrismaService es global, inyectado donde sea necesario
```

**PrismaService (patrón singleton):**
```typescript
// prisma.service.ts
@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit {
  async onModuleInit() {
    await this.$connect();
  }

  async enableShutdownHooks(app: INestApplication) {
    this.$on('beforeExit', async () => {
      await app.close();
    });
  }
}
```

---

## 13. Matriz de Autenticación y Autorización

| Endpoint | Método | Autenticación | Rol |
|----------|--------|---------------|-----|
| /restaurants | GET | No | Público |
| /restaurants | POST | JWT | admin |
| /restaurants/{id} | PATCH | JWT | admin |
| /restaurants/{id} | DELETE | JWT | admin |
| /restaurants/{id}/orders | GET | JWT | admin/propietario |
| /orders | POST | JWT | customer |
| /orders/{id} | GET | JWT | customer/admin |
| /orders/{id}/cancel | POST | JWT | customer/admin |
| /reviews | POST | JWT | customer |
| /admin/** | * | JWT | admin |

---

## 14. Resumen de Módulos

| Módulo | Responsabilidades | DTOs | Servicios |
|--------|------------------|------|-----------|
| Auth | Login, registro, JWT | 4 | AuthService, JwtStrategy |
| Restaurants | CRUD restaurantes, ratings | 4 | RestaurantsService, LocationsService |
| Menus | CRUD menús e items | 5 | MenusService, MenuItemsService |
| Ingredients | Gestión ingredientes | 2 | IngredientsService |
| Employees | CRUD empleados | 3 | EmployeesService |
| Customers | Registro, perfil, lealtad | 3 | CustomersService, LoyaltyService |
| Orders | CRUD órdenes, estados | 6 | OrdersService, OrderStatusService, OrderValidationService, OrderCalculationService |
| Reviews | CRUD reseñas, analytics | 4 | ReviewsService, ReviewAnalyticsService |

**Total**: 8 módulos | ~35 DTOs | ~15 servicios | ~4 controllers principales

---

## 15. Guía de Implementación

### Orden recomendado:
1. **ConfigModule** - Variables de entorno
2. **PrismaService** - Conexión PostgreSQL
3. **AuthModule** - Autenticación base
4. **RestaurantsModule** - Entidad principal
5. **MenusModule** - Menús y items
6. **EmployeesModule** - Empleados
7. **CustomersModule** - Clientes
8. **OrdersModule** - Órdenes (complejo, depende de muchos)
9. **ReviewsModule** - Reseñas
10. **HealthModule** - Health checks

Esta arquitectura garantiza:
- ✓ Escalabilidad
- ✓ Testabilidad
- ✓ Mantenibilidad
- ✓ Separación de responsabilidades
- ✓ Reutilización de código

---

## 16. Testing con Jest

### 16.1 Configuración Jest

**jest.config.js:**
```javascript
module.exports = {
  moduleFileExtensions: ['js', 'json', 'ts'],
  rootDir: 'src',
  testRegex: '.*\\.spec\\.ts$',
  transform: {
    '^.+\\.(t|j)s$': 'ts-jest',
  },
  collectCoverageFrom: [
    '**/*.(t|j)s',
  ],
  coverageDirectory: '../coverage',
  testEnvironment: 'node',
  moduleNameMapper: {
    '^src/(.*)$': '<rootDir>/$1',
  },
};
```

### 16.2 Testing de Servicios

**Ejemplo: restaurants.service.spec.ts**

```typescript
describe('RestaurantsService', () => {
  let service: RestaurantsService;
  let prisma: PrismaService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [
        RestaurantsService,
        {
          provide: PrismaService,
          useValue: {
            restaurant: {
              findMany: jest.fn(),
              findUnique: jest.fn(),
              create: jest.fn(),
              update: jest.fn(),
              delete: jest.fn(),
            },
          },
        },
      ],
    }).compile();

    service = module.get<RestaurantsService>(RestaurantsService);
    prisma = module.get<PrismaService>(PrismaService);
  });

  describe('findAll', () => {
    it('debería retornar un array de restaurantes', async () => {
      const restaurants = [
        { id: '1', name: 'Test Restaurant', status: 'active' },
      ];
      jest.spyOn(prisma.restaurant, 'findMany').mockResolvedValue(restaurants);

      const result = await service.findAll({}, { page: 1, limit: 10 });

      expect(result).toEqual(restaurants);
      expect(prisma.restaurant.findMany).toHaveBeenCalled();
    });
  });

  describe('findById', () => {
    it('debería retornar un restaurante por ID', async () => {
      const restaurant = { id: '1', name: 'Test Restaurant' };
      jest.spyOn(prisma.restaurant, 'findUnique').mockResolvedValue(restaurant);

      const result = await service.findById('1');

      expect(result).toEqual(restaurant);
      expect(prisma.restaurant.findUnique).toHaveBeenCalledWith({
        where: { id: '1' },
        include: { locations: true },
      });
    });

    it('debería lanzar NotFoundException si no existe', async () => {
      jest.spyOn(prisma.restaurant, 'findUnique').mockResolvedValue(null);

      await expect(service.findById('999')).rejects.toThrow(
        NotFoundException,
      );
    });
  });

  describe('create', () => {
    it('debería crear un nuevo restaurante', async () => {
      const createDto: CreateRestaurantDto = {
        name: 'New Restaurant',
        email: 'test@example.com',
        location: {
          address: '123 Main St',
          city: 'Madrid',
          state: 'Madrid',
          postal_code: '28001',
        },
      };

      const created = { id: '1', ...createDto, status: 'active' };
      jest.spyOn(prisma.restaurant, 'create').mockResolvedValue(created);

      const result = await service.create(createDto);

      expect(result).toEqual(created);
      expect(prisma.restaurant.create).toHaveBeenCalled();
    });

    it('debería lanzar ConflictException si el nombre existe', async () => {
      jest
        .spyOn(prisma.restaurant, 'create')
        .mockRejectedValue(
          new Prisma.PrismaClientKnownRequestError(
            'Unique constraint failed',
            { code: 'P2002' },
          ),
        );

      await expect(service.create({} as any)).rejects.toThrow(
        ConflictException,
      );
    });
  });
});
```

### 16.3 Testing de Controladores

**Ejemplo: restaurants.controller.spec.ts**

```typescript
describe('RestaurantsController', () => {
  let controller: RestaurantsController;
  let service: RestaurantsService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      controllers: [RestaurantsController],
      providers: [
        {
          provide: RestaurantsService,
          useValue: {
            findAll: jest.fn(),
            findById: jest.fn(),
            create: jest.fn(),
            update: jest.fn(),
            delete: jest.fn(),
          },
        },
      ],
    }).compile();

    controller = module.get<RestaurantsController>(RestaurantsController);
    service = module.get<RestaurantsService>(RestaurantsService);
  });

  describe('GET /restaurants', () => {
    it('debería retornar lista de restaurantes', async () => {
      const restaurants = [{ id: '1', name: 'Test' }];
      jest.spyOn(service, 'findAll').mockResolvedValue(restaurants);

      const result = await controller.findAll({}, {}, {});

      expect(result).toEqual(restaurants);
      expect(service.findAll).toHaveBeenCalled();
    });
  });

  describe('POST /restaurants', () => {
    it('debería crear un nuevo restaurante', async () => {
      const createDto: CreateRestaurantDto = {
        name: 'New Restaurant',
        email: 'test@example.com',
        location: {
          address: '123 Main St',
          city: 'Madrid',
          state: 'Madrid',
          postal_code: '28001',
        },
      };
      const created = { id: '1', ...createDto, status: 'active' };
      jest.spyOn(service, 'create').mockResolvedValue(created);

      const result = await controller.create(createDto);

      expect(result).toEqual(created);
      expect(service.create).toHaveBeenCalledWith(createDto);
    });
  });
});
```

### 16.4 Testing E2E con Supertest

**Ejemplo: restaurants.e2e.spec.ts**

```typescript
describe('Restaurants E2E', () => {
  let app: INestApplication;
  let prisma: PrismaService;

  beforeAll(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    prisma = moduleFixture.get<PrismaService>(PrismaService);
    await app.init();
  });

  afterAll(async () => {
    await app.close();
    await prisma.$disconnect();
  });

  describe('GET /restaurants', () => {
    it('debería retornar lista de restaurantes', () => {
      return request(app.getHttpServer())
        .get('/restaurants')
        .expect(200)
        .expect((res) => {
          expect(res.body).toHaveProperty('success', true);
          expect(res.body).toHaveProperty('data');
          expect(Array.isArray(res.body.data)).toBe(true);
        });
    });
  });

  describe('POST /restaurants', () => {
    it('debería crear un nuevo restaurante', async () => {
      const createDto = {
        name: `Test Restaurant ${Date.now()}`,
        email: `test${Date.now()}@example.com`,
        location: {
          address: '123 Main St',
          city: 'Madrid',
          state: 'Madrid',
          postal_code: '28001',
        },
      };

      const response = await request(app.getHttpServer())
        .post('/restaurants')
        .set('Authorization', `Bearer ${authToken}`)
        .send(createDto)
        .expect(201);

      expect(response.body).toHaveProperty('success', true);
      expect(response.body.data).toHaveProperty('id');
      expect(response.body.data.name).toBe(createDto.name);
    });

    it('debería fallar si el nombre existe', async () => {
      const createDto = {
        name: 'Duplicate Name',
        email: 'test@example.com',
        location: {
          address: '123 Main St',
          city: 'Madrid',
          state: 'Madrid',
          postal_code: '28001',
        },
      };

      await request(app.getHttpServer())
        .post('/restaurants')
        .set('Authorization', `Bearer ${authToken}`)
        .send(createDto);

      return request(app.getHttpServer())
        .post('/restaurants')
        .set('Authorization', `Bearer ${authToken}`)
        .send(createDto)
        .expect(409);
    });
  });
});
```

### 16.5 Scripts en package.json

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json"
  }
}
```

---

## 17. Integración con Prisma

### 17.1 Schema.prisma (Ejemplo simplificado)

```prisma
// prisma/schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model Restaurant {
  id            String      @id @default(uuid())
  name          String      @unique
  description   String?
  phone         String?
  email         String
  status        String      @default("active")
  locations     Location[]
  menus         Menu[]
  employees     Employee[]
  orders        Order[]
  reviews       Review[]
  createdAt     DateTime    @default(now())
  updatedAt     DateTime    @updatedAt

  @@index([status])
  @@fulltext([name])
}

model Location {
  id            String      @id @default(uuid())
  restaurantId  String
  restaurant    Restaurant  @relation(fields: [restaurantId], references: [id], onDelete: Cascade)
  address       String
  city          String
  state         String
  postal_code   String
  latitude      Float?
  longitude     Float?
  createdAt     DateTime    @default(now())

  @@index([restaurantId])
  @@index([city, state])
}

model Menu {
  id            String      @id @default(uuid())
  restaurantId  String
  restaurant    Restaurant  @relation(fields: [restaurantId], references: [id], onDelete: Cascade)
  name          String
  description   String?
  validFrom     DateTime
  validTo       DateTime?
  status        String      @default("active")
  items         MenuItem[]
  createdAt     DateTime    @default(now())

  @@unique([restaurantId, name, validFrom])
  @@index([restaurantId])
  @@index([validFrom, validTo])
}

model MenuItem {
  id            String      @id @default(uuid())
  menuId        String
  menu          Menu        @relation(fields: [menuId], references: [id], onDelete: Cascade)
  name          String
  description   String?
  price         Decimal     @db.Decimal(10, 2)
  calories      Int?
  vegetarian    Boolean     @default(false)
  vegan         Boolean     @default(false)
  status        String      @default("available")
  ingredients   Recipe[]
  orderItems    OrderItem[]
  createdAt     DateTime    @default(now())

  @@index([menuId])
  @@index([vegetarian, vegan])
  @@index([status])
}

model Ingredient {
  id            String      @id @default(uuid())
  name          String      @unique
  allergenInfo  String?
  unit          String?
  recipes       Recipe[]
  createdAt     DateTime    @default(now())

  @@fulltext([name])
}

model Recipe {
  id            String      @id @default(uuid())
  menuItemId    String
  menuItem      MenuItem    @relation(fields: [menuItemId], references: [id], onDelete: Cascade)
  ingredientId  String
  ingredient    Ingredient  @relation(fields: [ingredientId], references: [id], onDelete: Restrict)
  quantity      Decimal     @db.Decimal(10, 2)
  createdAt     DateTime    @default(now())

  @@unique([menuItemId, ingredientId])
  @@index([menuItemId])
  @@index([ingredientId])
}

model Employee {
  id                  String      @id @default(uuid())
  restaurantId        String
  restaurant          Restaurant  @relation(fields: [restaurantId], references: [id], onDelete: Cascade)
  email               String      @unique
  firstName           String
  lastName            String
  role                String
  phone               String?
  hireDate            DateTime
  employmentStatus    String      @default("active")
  assignments         OrderAssignment[]
  createdAt           DateTime    @default(now())

  @@index([restaurantId, role])
  @@index([email])
  @@index([employmentStatus])
}

model Customer {
  id                  String      @id @default(uuid())
  email               String      @unique
  firstName           String
  lastName            String
  phone               String?
  loyaltyNumber       String?     @unique
  subscriptionStatus  String      @default("active")
  orders              Order[]
  reviews             Review[]
  createdAt           DateTime    @default(now())

  @@index([email])
  @@index([loyaltyNumber])
  @@index([subscriptionStatus])
}

model Order {
  id              String      @id @default(uuid())
  restaurantId    String
  restaurant      Restaurant  @relation(fields: [restaurantId], references: [id], onDelete: Restrict)
  customerId      String
  customer        Customer    @relation(fields: [customerId], references: [id], onDelete: Restrict)
  orderDate       DateTime    @default(now())
  totalAmount     Decimal     @db.Decimal(10, 2)
  taxAmount       Decimal     @default(0) @db.Decimal(10, 2)
  discountAmount  Decimal     @default(0) @db.Decimal(10, 2)
  paymentMethod   String?
  orderStatus     String      @default("pending")
  deliveryType    String?
  items           OrderItem[]
  assignments     OrderAssignment[]
  createdAt       DateTime    @default(now())
  updatedAt       DateTime    @updatedAt

  @@index([restaurantId])
  @@index([customerId])
  @@index([orderDate])
  @@index([orderStatus])
  @@index([deliveryType])
}

model OrderItem {
  id                    String      @id @default(uuid())
  orderId               String
  order                 Order       @relation(fields: [orderId], references: [id], onDelete: Cascade)
  menuItemId            String
  menuItem              MenuItem    @relation(fields: [menuItemId], references: [id], onDelete: Restrict)
  quantity              Int
  unitPrice             Decimal     @db.Decimal(10, 2)
  specialInstructions   String?
  createdAt             DateTime    @default(now())

  @@index([orderId])
  @@index([menuItemId])
}

model OrderAssignment {
  id            String      @id @default(uuid())
  orderId       String
  order         Order       @relation(fields: [orderId], references: [id], onDelete: Cascade)
  employeeId    String
  employee      Employee    @relation(fields: [employeeId], references: [id], onDelete: Restrict)
  role          String
  assignedAt    DateTime    @default(now())
  completedAt   DateTime?
  createdAt     DateTime    @default(now())

  @@index([orderId])
  @@index([employeeId])
  @@index([role])
}

model Review {
  id            String      @id @default(uuid())
  customerId    String
  customer      Customer    @relation(fields: [customerId], references: [id], onDelete: Cascade)
  restaurantId  String
  restaurant    Restaurant  @relation(fields: [restaurantId], references: [id], onDelete: Cascade)
  rating        Int
  title         String?
  comment       String?
  createdAt     DateTime    @default(now())

  @@unique([customerId, restaurantId, createdAt])
  @@index([restaurantId])
  @@index([customerId])
  @@index([createdAt])
  @@index([rating])
}
```

### 17.2 Migraciones Prisma

```bash
# Crear migración
npx prisma migrate dev --name init

# Aplicar migraciones en producción
npx prisma migrate deploy

# Resetear DB (desarrollo)
npx prisma migrate reset

# Generar Prisma Client
npx prisma generate
```

### 17.3 Seeding con Prisma

**prisma/seed.ts:**
```typescript
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function main() {
  // Crear restaurantes
  const restaurant = await prisma.restaurant.create({
    data: {
      name: 'Pizzería Roma',
      email: 'info@pizzeriaroma.es',
      locations: {
        create: {
          address: 'Calle Principal 10',
          city: 'Madrid',
          state: 'Madrid',
          postal_code: '28001',
        },
      },
    },
  });

  console.log('Seeding completed', restaurant);
}

main()
  .then(async () => {
    await prisma.$disconnect();
  })
  .catch(async (e) => {
    console.error(e);
    await prisma.$disconnect();
    process.exit(1);
  });
```

**package.json:**
```json
{
  "prisma": {
    "seed": "ts-node prisma/seed.ts"
  }
}
```

---

## 18. Node.js 22.x - Características y Compatibilidad

### 18.1 Requisitos del Proyecto

**Node 22.x ofrece:**
- ✓ ES2024 features
- ✓ Mejor rendimiento V8
- ✓ WebStream API built-in
- ✓ Compatibilidad total con TypeScript 5.x+
- ✓ Soporte para `.node` modules

### 18.2 package.json Recomendado

```json
{
  "name": "restaurantes-api",
  "version": "1.0.0",
  "description": "Sistema de gestión de restaurantes con NestJS",
  "author": "Your Name",
  "license": "MIT",
  "engines": {
    "node": ">=22.0.0",
    "npm": ">=10.0.0"
  },
  "scripts": {
    "build": "nest build",
    "start": "node dist/main.js",
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:e2e": "jest --config ./test/jest-e2e.json",
    "prisma:generate": "prisma generate",
    "prisma:migrate": "prisma migrate dev",
    "prisma:seed": "prisma db seed",
    "prisma:studio": "prisma studio"
  },
  "dependencies": {
    "@nestjs/common": "^10.0.0",
    "@nestjs/config": "^3.0.0",
    "@nestjs/core": "^10.0.0",
    "@nestjs/jwt": "^11.0.0",
    "@nestjs/passport": "^10.0.0",
    "@nestjs/platform-express": "^10.0.0",
    "@nestjs/swagger": "^7.0.0",
    "@prisma/client": "^5.0.0",
    "bcrypt": "^5.1.0",
    "class-transformer": "^0.5.1",
    "class-validator": "^0.14.0",
    "passport": "^0.6.0",
    "passport-jwt": "^4.0.1",
    "reflect-metadata": "^0.1.13",
    "rxjs": "^7.8.0"
  },
  "devDependencies": {
    "@nestjs/cli": "^10.0.0",
    "@nestjs/schematics": "^10.0.0",
    "@nestjs/testing": "^10.0.0",
    "@prisma/cli": "^5.0.0",
    "@types/bcrypt": "^5.0.0",
    "@types/express": "^4.17.17",
    "@types/jest": "^29.5.0",
    "@types/node": "^20.0.0",
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "@typescript-eslint/parser": "^6.0.0",
    "eslint": "^8.0.0",
    "jest": "^29.5.0",
    "prettier": "^3.0.0",
    "prisma": "^5.0.0",
    "supertest": "^6.3.0",
    "ts-jest": "^29.1.0",
    "ts-loader": "^9.4.0",
    "ts-node": "^10.9.0",
    "typescript": "^5.0.0"
  }
}
```

---

## Resumen Final

### Stack Tecnológico Completo:
- **Runtime**: Node.js 22.x
- **Framework**: NestJS 10.x
- **Base de Datos**: PostgreSQL + Prisma ORM
- **Testing**: Jest + Supertest
- **Autenticación**: JWT + Passport
- **Validación**: Class Validator
- **Documentación**: Swagger/OpenAPI

### Estructura:
- 8 módulos principales
- ~40 DTOs
- ~20 servicios
- Cobertura de testing en servicios y controladores
- Testing E2E con Supertest
- Prisma Schema completo con migraciones

### Ventajas de esta arquitectura:
✓ **Escalable** - Módulos independientes  
✓ **Testeable** - Jest integrado con mocks  
✓ **Mantenible** - Separación de responsabilidades  
✓ **Type-Safe** - TypeScript + Prisma  
✓ **Performante** - Node 22 + Prisma optimizado
