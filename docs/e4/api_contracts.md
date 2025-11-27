# Contratos REST API - Sistema de Restaurantes

## Descripción General

Especificación de API REST completa para sistema de gestión de restaurantes. Sigue estándares RESTful, versionamiento y manejo de errores según convenciones HTTP.

**Base URL**: `https://api.restaurantes.com/v1`  
**Autenticación**: Bearer Token (JWT)  
**Content-Type**: `application/json`  
**Formato de Fechas**: ISO 8601 (UTC)

---

## 1. Contratos - Restaurantes

### 1.1 Listar Restaurantes

```http
GET /restaurants?page=1&limit=20&city=Madrid&status=active
```

**Parámetros Query:**

| Parámetro | Tipo | Opcional | Descripción |
|-----------|------|----------|-------------|
| `page` | integer | Sí | Número de página (default: 1) |
| `limit` | integer | Sí | Registros por página (default: 20, máx: 100) |
| `city` | string | Sí | Filtrar por ciudad |
| `state` | string | Sí | Filtrar por provincia |
| `status` | string | Sí | Filtrar por estado (active, inactive, suspended) |
| `search` | string | Sí | Búsqueda por nombre (fuzzy matching) |
| `sort` | string | Sí | Orden: name, rating, created_at (con -, descending) |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "name": "Pizzería Roma",
      "description": "Auténtica pizzería italiana",
      "phone": "+34-91-123-4567",
      "email": "info@pizzeriaroma.es",
      "status": "active",
      "location": {
        "address": "Calle Principal 10",
        "city": "Madrid",
        "state": "Madrid",
        "postal_code": "28001",
        "latitude": 40.4168,
        "longitude": -3.7038
      },
      "avgRating": 4.5,
      "reviewCount": 128,
      "createdAt": "2024-01-15T10:30:00Z",
      "updatedAt": "2024-11-27T15:45:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 245,
    "totalPages": 13
  }
}
```

**Respuesta 400 Bad Request:**

```json
{
  "success": false,
  "error": {
    "code": "INVALID_PAGINATION",
    "message": "El límite no puede exceder 100",
    "details": {
      "field": "limit",
      "value": 150
    }
  }
}
```

---

### 1.2 Obtener Restaurante por ID

```http
GET /restaurants/{restaurantId}
```

**Parámetros Path:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `restaurantId` | UUID | ID del restaurante |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Pizzería Roma",
    "description": "Auténtica pizzería italiana con horno de leña",
    "phone": "+34-91-123-4567",
    "email": "info@pizzeriaroma.es",
    "status": "active",
    "locations": [
      {
        "id": "660e8400-e29b-41d4-a716-446655440001",
        "address": "Calle Principal 10",
        "city": "Madrid",
        "state": "Madrid",
        "postal_code": "28001",
        "latitude": 40.4168,
        "longitude": -3.7038
      }
    ],
    "avgRating": 4.5,
    "reviewCount": 128,
    "totalOrders": 1250,
    "createdAt": "2024-01-15T10:30:00Z",
    "updatedAt": "2024-11-27T15:45:00Z"
  }
}
```

**Respuesta 404 Not Found:**

```json
{
  "success": false,
  "error": {
    "code": "RESTAURANT_NOT_FOUND",
    "message": "El restaurante con ID especificado no existe",
    "details": {
      "restaurantId": "550e8400-e29b-41d4-a716-446655440000"
    }
  }
}
```

---

### 1.3 Crear Restaurante

```http
POST /restaurants
```

**Body (application/json):**

```json
{
  "name": "Pizzería Roma",
  "description": "Auténtica pizzería italiana con horno de leña",
  "phone": "+34-91-123-4567",
  "email": "info@pizzeriaroma.es",
  "location": {
    "address": "Calle Principal 10",
    "city": "Madrid",
    "state": "Madrid",
    "postal_code": "28001",
    "latitude": 40.4168,
    "longitude": -3.7038
  }
}
```

**Validaciones:**

| Campo | Regla |
|-------|-------|
| `name` | Requerido, único, 1-255 caracteres |
| `email` | Requerido, formato email válido |
| `phone` | Opcional, formato internacional |
| `location.address` | Requerido, 1-500 caracteres |
| `location.latitude` | Coordenada válida o null |
| `location.longitude` | Coordenada válida o null |

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Pizzería Roma",
    "description": "Auténtica pizzería italiana con horno de leña",
    "phone": "+34-91-123-4567",
    "email": "info@pizzeriaroma.es",
    "status": "active",
    "location": {
      "id": "660e8400-e29b-41d4-a716-446655440001",
      "address": "Calle Principal 10",
      "city": "Madrid",
      "state": "Madrid",
      "postal_code": "28001",
      "latitude": 40.4168,
      "longitude": -3.7038
    },
    "createdAt": "2024-11-27T16:00:00Z"
  }
}
```

**Respuesta 400 Bad Request:**

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Error de validación en la solicitud",
    "details": {
      "errors": [
        {
          "field": "name",
          "message": "El nombre ya existe",
          "code": "UNIQUE_CONSTRAINT_VIOLATION"
        },
        {
          "field": "email",
          "message": "Email inválido",
          "code": "INVALID_FORMAT"
        }
      ]
    }
  }
}
```

**Respuesta 409 Conflict:**

```json
{
  "success": false,
  "error": {
    "code": "DUPLICATE_RESTAURANT",
    "message": "Un restaurante con este nombre ya existe",
    "details": {
      "field": "name",
      "value": "Pizzería Roma"
    }
  }
}
```

---

### 1.4 Actualizar Restaurante

```http
PATCH /restaurants/{restaurantId}
```

**Body (actualización parcial):**

```json
{
  "name": "Pizzería Roma Premium",
  "status": "inactive",
  "description": "Auténtica pizzería italiana con horno de leña - Ahora cerrado por reformas"
}
```

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Pizzería Roma Premium",
    "status": "inactive",
    "description": "Auténtica pizzería italiana con horno de leña - Ahora cerrado por reformas",
    "updatedAt": "2024-11-27T16:15:00Z"
  }
}
```

---

### 1.5 Eliminar Restaurante

```http
DELETE /restaurants/{restaurantId}
```

**Respuesta 204 No Content:** (Sin body)

**Respuesta 400 Bad Request (si hay órdenes pendientes):**

```json
{
  "success": false,
  "error": {
    "code": "RESTAURANT_HAS_ACTIVE_ORDERS",
    "message": "No se puede eliminar un restaurante con órdenes pendientes",
    "details": {
      "activeOrderCount": 5
    }
  }
}
```

---

## 2. Contratos - Menús

### 2.1 Listar Menús de un Restaurante

```http
GET /restaurants/{restaurantId}/menus?status=active&includeItems=true
```

**Parámetros Query:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `status` | string | Filtro: active, draft, archived |
| `includeItems` | boolean | Incluir items del menú (default: false) |
| `validAt` | ISO-8601 | Menús válidos en fecha (default: hoy) |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "770e8400-e29b-41d4-a716-446655440002",
      "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
      "name": "Menú Desayuno",
      "description": "Desayunos especiales de 7 a 11 AM",
      "status": "active",
      "validFrom": "2024-11-01T00:00:00Z",
      "validTo": "2024-12-31T23:59:59Z",
      "itemCount": 12,
      "items": [
        {
          "id": "880e8400-e29b-41d4-a716-446655440003",
          "name": "Huevos Rancheros",
          "price": 8.50,
          "vegetarian": false,
          "vegan": false
        }
      ],
      "createdAt": "2024-10-20T09:00:00Z"
    }
  ]
}
```

---

### 2.2 Crear Menú

```http
POST /restaurants/{restaurantId}/menus
```

**Body:**

```json
{
  "name": "Menú Desayuno",
  "description": "Desayunos especiales de 7 a 11 AM",
  "validFrom": "2024-11-01T00:00:00Z",
  "validTo": "2024-12-31T23:59:59Z",
  "items": [
    {
      "name": "Huevos Rancheros",
      "description": "Huevos fritos con frijoles",
      "price": 8.50,
      "calories": 450,
      "vegetarian": false,
      "vegan": false
    }
  ]
}
```

**Validaciones:**

| Campo | Regla |
|-------|-------|
| `name` | Requerido, 1-255 caracteres, único por restaurante |
| `validFrom` | Requerido, ISO-8601 |
| `validTo` | Opcional, debe ser > validFrom |
| `items[].price` | Positivo, máximo 2 decimales |
| `items[].calories` | Opcional, positivo |

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "770e8400-e29b-41d4-a716-446655440002",
    "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
    "name": "Menú Desayuno",
    "status": "active",
    "validFrom": "2024-11-01T00:00:00Z",
    "validTo": "2024-12-31T23:59:59Z",
    "itemCount": 1,
    "createdAt": "2024-11-27T16:30:00Z"
  }
}
```

---

### 2.3 Actualizar Menú

```http
PATCH /restaurants/{restaurantId}/menus/{menuId}
```

**Body:**

```json
{
  "name": "Menú Desayuno Premium",
  "status": "archived",
  "validTo": "2024-11-30T23:59:59Z"
}
```

**Respuesta 200 OK:** (Similar a creación)

---

## 3. Contratos - Items de Menú

### 3.1 Listar Items de un Menú

```http
GET /menus/{menuId}/items?dietary=vegetarian&sort=price&order=asc
```

**Parámetros Query:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `dietary` | string | Filtro: vegetarian, vegan |
| `sort` | string | Campo: name, price, calories |
| `order` | string | asc, desc (default: asc) |
| `minPrice` | number | Precio mínimo |
| `maxPrice` | number | Precio máximo |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "880e8400-e29b-41d4-a716-446655440003",
      "menuId": "770e8400-e29b-41d4-a716-446655440002",
      "name": "Huevos Rancheros",
      "description": "Huevos fritos con frijoles",
      "price": 8.50,
      "calories": 450,
      "vegetarian": false,
      "vegan": false,
      "status": "available",
      "ingredients": [
        {
          "id": "990e8400-e29b-41d4-a716-446655440004",
          "name": "Huevo",
          "allergenInfo": "Sin alérgenos comunes"
        }
      ]
    }
  ]
}
```

---

### 3.2 Crear Item de Menú

```http
POST /menus/{menuId}/items
```

**Body:**

```json
{
  "name": "Huevos Rancheros",
  "description": "Huevos fritos con frijoles y salsa",
  "price": 8.50,
  "calories": 450,
  "vegetarian": false,
  "vegan": false,
  "ingredients": [
    {
      "id": "990e8400-e29b-41d4-a716-446655440004",
      "quantity": 2,
      "unit": "piezas"
    }
  ]
}
```

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "880e8400-e29b-41d4-a716-446655440003",
    "menuId": "770e8400-e29b-41d4-a716-446655440002",
    "name": "Huevos Rancheros",
    "price": 8.50,
    "status": "available",
    "createdAt": "2024-11-27T16:45:00Z"
  }
}
```

---

## 4. Contratos - Empleados

### 4.1 Listar Empleados

```http
GET /restaurants/{restaurantId}/employees?role=chef&status=active&page=1&limit=20
```

**Parámetros Query:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `role` | string | Filtro: admin, chef, mesero, cajero, delivery |
| `status` | string | Filtro: active, on_leave, terminated |
| `page` | integer | Número de página |
| `limit` | integer | Registros por página |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "bb0e8400-e29b-41d4-a716-446655440005",
      "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
      "email": "juan.garcia@pizzeriaroma.es",
      "firstName": "Juan",
      "lastName": "García",
      "role": "chef",
      "phone": "+34-91-987-6543",
      "hireDate": "2023-06-15T00:00:00Z",
      "employmentStatus": "active",
      "createdAt": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 5,
    "totalPages": 1
  }
}
```

---

### 4.2 Crear Empleado

```http
POST /restaurants/{restaurantId}/employees
```

**Body:**

```json
{
  "email": "juan.garcia@pizzeriaroma.es",
  "firstName": "Juan",
  "lastName": "García",
  "role": "chef",
  "phone": "+34-91-987-6543",
  "hireDate": "2024-11-27T00:00:00Z"
}
```

**Validaciones:**

| Campo | Regla |
|-------|-------|
| `email` | Requerido, único globalmente, formato válido |
| `firstName`, `lastName` | Requeridos, 1-100 caracteres |
| `role` | Requerido, enum: admin, chef, mesero, cajero, delivery |
| `hireDate` | Requerido, ISO-8601, no puede ser futura |

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "bb0e8400-e29b-41d4-a716-446655440005",
    "email": "juan.garcia@pizzeriaroma.es",
    "firstName": "Juan",
    "lastName": "García",
    "role": "chef",
    "employmentStatus": "active",
    "createdAt": "2024-11-27T17:00:00Z"
  }
}
```

**Respuesta 409 Conflict:**

```json
{
  "success": false,
  "error": {
    "code": "EMPLOYEE_EMAIL_EXISTS",
    "message": "El email ya está registrado",
    "details": {
      "email": "juan.garcia@pizzeriaroma.es"
    }
  }
}
```

---

### 4.3 Actualizar Empleado

```http
PATCH /restaurants/{restaurantId}/employees/{employeeId}
```

**Body:**

```json
{
  "role": "admin",
  "employmentStatus": "on_leave"
}
```

**Respuesta 200 OK:** (Similar a creación)

---

### 4.4 Eliminar Empleado

```http
DELETE /restaurants/{restaurantId}/employees/{employeeId}
```

**Respuesta 204 No Content**

**Respuesta 400 Bad Request:**

```json
{
  "success": false,
  "error": {
    "code": "EMPLOYEE_HAS_ACTIVE_ASSIGNMENTS",
    "message": "No se puede eliminar empleado con órdenes asignadas",
    "details": {
      "activeAssignmentCount": 3
    }
  }
}
```

---

## 5. Contratos - Clientes

### 5.1 Listar Clientes

```http
GET /customers?status=active&sortBy=created_at&order=desc&page=1&limit=20
```

**Parámetros Query:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `status` | string | Filtro: active, inactive, suspended |
| `loyaltyMember` | boolean | Solo miembros de lealtad |
| `search` | string | Búsqueda por nombre o email |
| `sortBy` | string | Campo: created_at, name, orders_count |
| `page`, `limit` | integer | Paginación |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "cc0e8400-e29b-41d4-a716-446655440006",
      "email": "maria.lopez@email.com",
      "firstName": "María",
      "lastName": "López",
      "phone": "+34-91-555-6666",
      "loyaltyNumber": "LOYALTY-001234",
      "subscriptionStatus": "active",
      "totalOrders": 15,
      "totalSpent": 450.75,
      "createdAt": "2024-03-10T12:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 542,
    "totalPages": 28
  }
}
```

---

### 5.2 Registrar Cliente

```http
POST /customers/register
```

**Body:**

```json
{
  "email": "maria.lopez@email.com",
  "firstName": "María",
  "lastName": "López",
  "phone": "+34-91-555-6666"
}
```

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "cc0e8400-e29b-41d4-a716-446655440006",
    "email": "maria.lopez@email.com",
    "firstName": "María",
    "lastName": "López",
    "loyaltyNumber": "LOYALTY-001234",
    "subscriptionStatus": "active",
    "createdAt": "2024-11-27T17:15:00Z"
  }
}
```

---

### 5.3 Obtener Perfil del Cliente (Autenticado)

```http
GET /customers/me
Authorization: Bearer <JWT_TOKEN>
```

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "cc0e8400-e29b-41d4-a716-446655440006",
    "email": "maria.lopez@email.com",
    "firstName": "María",
    "lastName": "López",
    "phone": "+34-91-555-6666",
    "loyaltyNumber": "LOYALTY-001234",
    "subscriptionStatus": "active",
    "totalOrders": 15,
    "totalSpent": 450.75,
    "preferences": {
      "dietary": ["vegetarian"],
      "cuisines": ["Italian", "Spanish"]
    }
  }
}
```

---

## 6. Contratos - Órdenes

### 6.1 Crear Orden

```http
POST /orders
Authorization: Bearer <JWT_TOKEN>
```

**Body:**

```json
{
  "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
  "deliveryType": "delivery",
  "items": [
    {
      "menuItemId": "880e8400-e29b-41d4-a716-446655440003",
      "quantity": 2,
      "specialInstructions": "Sin cebolla"
    }
  ],
  "paymentMethod": "credit_card",
  "discountCode": "PROMO10"
}
```

**Validaciones:**

| Campo | Regla |
|-------|-------|
| `restaurantId` | Requerido, UUID válido, restaurante activo |
| `items` | Mínimo 1 item, máximo 50 |
| `items[].quantity` | Positivo, máximo 99 |
| `paymentMethod` | Enum: credit_card, debit_card, cash, digital_wallet |
| `deliveryType` | Enum: dine_in, takeout, delivery |

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "dd0e8400-e29b-41d4-a716-446655440007",
    "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
    "customerId": "cc0e8400-e29b-41d4-a716-446655440006",
    "orderDate": "2024-11-27T17:30:00Z",
    "totalAmount": 17.00,
    "taxAmount": 3.57,
    "discountAmount": 1.70,
    "finalAmount": 18.87,
    "paymentMethod": "credit_card",
    "orderStatus": "pending",
    "deliveryType": "delivery",
    "items": [
      {
        "id": "ee0e8400-e29b-41d4-a716-446655440008",
        "menuItemId": "880e8400-e29b-41d4-a716-446655440003",
        "name": "Huevos Rancheros",
        "quantity": 2,
        "unitPrice": 8.50,
        "subtotal": 17.00,
        "specialInstructions": "Sin cebolla"
      }
    ],
    "estimatedDelivery": "2024-11-27T18:30:00Z"
  }
}
```

**Respuesta 400 Bad Request:**

```json
{
  "success": false,
  "error": {
    "code": "INVALID_ORDER",
    "message": "Error al crear la orden",
    "details": {
      "errors": [
        {
          "field": "items",
          "message": "Un item está fuera de stock",
          "code": "ITEM_UNAVAILABLE"
        }
      ]
    }
  }
}
```

---

### 6.2 Obtener Orden

```http
GET /orders/{orderId}
Authorization: Bearer <JWT_TOKEN>
```

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "dd0e8400-e29b-41d4-a716-446655440007",
    "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
    "customerId": "cc0e8400-e29b-41d4-a716-446655440006",
    "orderDate": "2024-11-27T17:30:00Z",
    "totalAmount": 17.00,
    "taxAmount": 3.57,
    "discountAmount": 1.70,
    "finalAmount": 18.87,
    "orderStatus": "confirmed",
    "deliveryType": "delivery",
    "items": [
      {
        "id": "ee0e8400-e29b-41d4-a716-446655440008",
        "name": "Huevos Rancheros",
        "quantity": 2,
        "unitPrice": 8.50,
        "subtotal": 17.00,
        "specialInstructions": "Sin cebolla"
      }
    ],
    "estimatedDelivery": "2024-11-27T18:30:00Z",
    "assignments": [
      {
        "id": "ff0e8400-e29b-41d4-a716-446655440009",
        "employeeId": "bb0e8400-e29b-41d4-a716-446655440005",
        "employeeName": "Juan García",
        "role": "chef",
        "assignedAt": "2024-11-27T17:32:00Z",
        "completedAt": null
      }
    ]
  }
}
```

---

### 6.3 Listar Órdenes del Cliente

```http
GET /customers/me/orders?status=pending&page=1&limit=10
Authorization: Bearer <JWT_TOKEN>
```

**Parámetros Query:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `status` | string | Filtro: pending, confirmed, preparing, ready, delivered, cancelled |
| `restaurantId` | UUID | Filtro por restaurante |
| `startDate` | ISO-8601 | Rango de fechas desde |
| `endDate` | ISO-8601 | Rango de fechas hasta |
| `sortBy` | string | Campo: order_date, total_amount |
| `page`, `limit` | integer | Paginación |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "dd0e8400-e29b-41d4-a716-446655440007",
      "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
      "restaurantName": "Pizzería Roma",
      "orderDate": "2024-11-27T17:30:00Z",
      "totalAmount": 17.00,
      "finalAmount": 18.87,
      "orderStatus": "confirmed",
      "deliveryType": "delivery",
      "itemCount": 2
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 15,
    "totalPages": 2
  }
}
```

---

### 6.4 Actualizar Estado de Orden

```http
PATCH /orders/{orderId}/status
Authorization: Bearer <JWT_TOKEN> (solo admin/restaurante)
```

**Body:**

```json
{
  "status": "preparing",
  "estimatedCompletionTime": "2024-11-27T18:15:00Z"
}
```

**Estados permitidos:**

| De | A | Quién | Descripción |
|----|---|-------|-------------|
| pending | confirmed | Restaurante | Confirmación de pedido |
| confirmed | preparing | Restaurante | Iniciando preparación |
| preparing | ready | Restaurante | Listo para entregar |
| ready | delivered | Delivery | Entregado |
| * | cancelled | Cliente/Admin | Cancelación |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "dd0e8400-e29b-41d4-a716-446655440007",
    "orderStatus": "preparing",
    "estimatedCompletionTime": "2024-11-27T18:15:00Z",
    "updatedAt": "2024-11-27T17:35:00Z"
  }
}
```

---

### 6.5 Cancelar Orden

```http
POST /orders/{orderId}/cancel
Authorization: Bearer <JWT_TOKEN>
```

**Body:**

```json
{
  "reason": "Cambié de opinión",
  "refundMethod": "original_payment"
}
```

**Condiciones:**

- Solo si status es `pending` o `confirmed`
- No permitido en `preparing` o `ready`
- Cliente: siempre puede cancelar en primeras 2 minutos
- Admin: puede cancelar en cualquier momento

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "dd0e8400-e29b-41d4-a716-446655440007",
    "orderStatus": "cancelled",
    "refundAmount": 18.87,
    "refundStatus": "processed",
    "cancelledAt": "2024-11-27T17:35:00Z"
  }
}
```

**Respuesta 409 Conflict:**

```json
{
  "success": false,
  "error": {
    "code": "INVALID_ORDER_STATE_FOR_CANCELLATION",
    "message": "No se puede cancelar una orden en estado preparing",
    "details": {
      "currentStatus": "preparing"
    }
  }
}
```

---

## 7. Contratos - Reseñas

### 7.1 Crear Reseña

```http
POST /restaurants/{restaurantId}/reviews
Authorization: Bearer <JWT_TOKEN>
```

**Body:**

```json
{
  "rating": 5,
  "title": "Excelente comida",
  "comment": "La pizzería es increíble. Pizzas deliciosas y servicio rápido."
}
```

**Validaciones:**

| Campo | Regla |
|-------|-------|
| `rating` | Requerido, integer 1-5 |
| `title` | Opcional, 1-255 caracteres |
| `comment` | Opcional, máximo 2000 caracteres |
| Unicidad | Un cliente solo puede reviewar por día |

**Respuesta 201 Created:**

```json
{
  "success": true,
  "data": {
    "id": "gg0e8400-e29b-41d4-a716-446655440010",
    "restaurantId": "550e8400-e29b-41d4-a716-446655440000",
    "customerId": "cc0e8400-e29b-41d4-a716-446655440006",
    "rating": 5,
    "title": "Excelente comida",
    "comment": "La pizzería es increíble. Pizzas deliciosas y servicio rápido.",
    "createdAt": "2024-11-27T18:00:00Z"
  }
}
```

---

### 7.2 Listar Reseñas de Restaurante

```http
GET /restaurants/{restaurantId}/reviews?rating=5&sortBy=created_at&page=1&limit=20
```

**Parámetros Query:**

| Parámetro | Tipo | Descripción |
|-----------|------|-------------|
| `rating` | integer | Filtro por puntuación |
| `sortBy` | string | Campo: created_at, rating |
| `order` | string | asc, desc |
| `page`, `limit` | integer | Paginación |

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": [
    {
      "id": "gg0e8400-e29b-41d4-a716-446655440010",
      "customerId": "cc0e8400-e29b-41d4-a716-446655440006",
      "customerName": "María López",
      "rating": 5,
      "title": "Excelente comida",
      "comment": "La pizzería es increíble. Pizzas deliciosas y servicio rápido.",
      "createdAt": "2024-11-27T18:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 128,
    "totalPages": 7
  },
  "analytics": {
    "averageRating": 4.5,
    "totalReviews": 128,
    "ratingDistribution": {
      "5": 75,
      "4": 35,
      "3": 12,
      "2": 4,
      "1": 2
    }
  }
}
```

---

### 7.3 Actualizar Reseña

```http
PATCH /restaurants/{restaurantId}/reviews/{reviewId}
Authorization: Bearer <JWT_TOKEN> (solo autor)
```

**Body:**

```json
{
  "rating": 4,
  "comment": "Actualización: La segunda vez fue igual de bueno"
}
```

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "id": "gg0e8400-e29b-41d4-a716-446655440010",
    "rating": 4,
    "comment": "Actualización: La segunda vez fue igual de bueno",
    "updatedAt": "2024-11-27T18:05:00Z"
  }
}
```

---

## 8. Errores Comunes y Respuestas Estándar

### 8.1 Errores de Autenticación

**401 Unauthorized:**

```json
{
  "success": false,
  "error": {
    "code": "UNAUTHORIZED",
    "message": "Token inválido o expirado",
    "details": {
      "hint": "Incluya header Authorization: Bearer <token>"
    }
  }
}
```

---

### 8.2 Errores de Autorización

**403 Forbidden:**

```json
{
  "success": false,
  "error": {
    "code": "FORBIDDEN",
    "message": "No tiene permiso para acceder a este recurso",
    "details": {
      "requiredRole": "admin",
      "userRole": "customer"
    }
  }
}
```

---

### 8.3 Errores de Validación

**422 Unprocessable Entity:**

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Los datos enviados no son válidos",
    "details": {
      "errors": [
        {
          "field": "price",
          "message": "El precio debe ser mayor a 0",
          "code": "INVALID_VALUE"
        },
        {
          "field": "email",
          "message": "Email inválido",
          "code": "INVALID_FORMAT"
        }
      ]
    }
  }
}
```

---

### 8.4 Errores de Conflicto

**409 Conflict:**

```json
{
  "success": false,
  "error": {
    "code": "CONFLICT",
    "message": "El recurso ya existe",
    "details": {
      "field": "name",
      "value": "Pizzería Roma"
    }
  }
}
```

---

### 8.5 Errores de Servidor

**500 Internal Server Error:**

```json
{
  "success": false,
  "error": {
    "code": "INTERNAL_SERVER_ERROR",
    "message": "Error interno del servidor",
    "details": {
      "requestId": "req-2024-11-27-12345",
      "timestamp": "2024-11-27T18:10:00Z"
    }
  }
}
```

---

## 9. Patrones de Respuesta

### Estructura General

```json
{
  "success": boolean,
  "data": T | null,
  "error": {
    "code": "ERROR_CODE",
    "message": "Descripción en español",
    "details": {}
  },
  "pagination": {
    "page": number,
    "limit": number,
    "total": number,
    "totalPages": number
  },
  "meta": {
    "requestId": "string",
    "timestamp": "ISO-8601"
  }
}
```

### Headers de Respuesta

```http
Content-Type: application/json
X-Request-Id: req-2024-11-27-12345
X-Rate-Limit-Limit: 1000
X-Rate-Limit-Remaining: 999
X-Rate-Limit-Reset: 1732716600
Cache-Control: no-cache, no-store, must-revalidate
```

---

## 10. Autenticación

### 10.1 Login

```http
POST /auth/login
```

**Body:**

```json
{
  "email": "maria.lopez@email.com",
  "password": "SecurePassword123!"
}
```

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 3600,
    "user": {
      "id": "cc0e8400-e29b-41d4-a716-446655440006",
      "email": "maria.lopez@email.com",
      "role": "customer"
    }
  }
}
```

---

### 10.2 Refresh Token

```http
POST /auth/refresh
```

**Body:**

```json
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Respuesta 200 OK:**

```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 3600
  }
}
```

---

## Resumen de Endpoints

| Método | Ruta | Descripción | Auth |
|--------|------|-------------|------|
| GET | `/restaurants` | Listar restaurantes | No |
| GET | `/restaurants/{id}` | Obtener restaurante | No |
| POST | `/restaurants` | Crear restaurante | Admin |
| PATCH | `/restaurants/{id}` | Actualizar restaurante | Admin |
| DELETE | `/restaurants/{id}` | Eliminar restaurante | Admin |
| GET | `/restaurants/{id}/menus` | Listar menús | No |
| POST | `/restaurants/{id}/menus` | Crear menú | Admin |
| GET | `/menus/{id}/items` | Listar items | No |
| POST | `/menus/{id}/items` | Crear item | Admin |
| GET | `/restaurants/{id}/employees` | Listar empleados | Admin |
| POST | `/restaurants/{id}/employees` | Crear empleado | Admin |
| GET | `/customers` | Listar clientes | Admin |
| POST | `/customers/register` | Registrar cliente | No |
| GET | `/customers/me` | Perfil del cliente | User |
| POST | `/orders` | Crear orden | User |
| GET | `/orders/{id}` | Obtener orden | User/Admin |
| GET | `/customers/me/orders` | Órdenes del cliente | User |
| PATCH | `/orders/{id}/status` | Actualizar estado | Admin |
| POST | `/orders/{id}/cancel` | Cancelar orden | User/Admin |
| POST | `/restaurants/{id}/reviews` | Crear reseña | User |
| GET | `/restaurants/{id}/reviews` | Listar reseñas | No |
| PATCH | `/restaurants/{id}/reviews/{id}` | Actualizar reseña | User |
| POST | `/auth/login` | Login | No |
| POST | `/auth/refresh` | Refresh token | No |

---

## Convenciones

✓ **Versionamiento**: URL prefix `/v1`  
✓ **Formato de Fecha**: ISO 8601 (UTC)  
✓ **IDs**: UUIDs (v4)  
✓ **Moneda**: 2 decimales  
✓ **Rate Limiting**: 1000 req/hora por cliente  
✓ **Timeouts**: 30 segundos para requests, 300 segundos para operaciones batch  
✓ **Idioma**: Español para mensajes de error  
