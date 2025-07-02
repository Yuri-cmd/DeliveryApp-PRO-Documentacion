# 📑 Documento de Requerimientos del Sistema
## DeliveryApp PRO

---

## 1️⃣ Objetivo del sistema

El sistema **DeliveryApp PRO** busca gestionar pedidos de delivery entre clientes y repartidores, permitiendo a los administradores gestionar productos y monitorear pedidos en tiempo real.

---

## 2️⃣ Alcance del proyecto

- Plataforma móvil para clientes (Flutter).
- Plataforma móvil para repartidores (Flutter).
- API REST (NestJS) con base de datos MySQL.
- Panel de administración (puede ser solo API en esta fase).
- Notificaciones push.
- Geolocalización y mapas.

---

## 3️⃣ Roles del sistema

### 3.1 Cliente
- Se registra e inicia sesión.
- Realiza pedidos de productos.
- Visualiza el estado de sus pedidos en tiempo real.
- Rastrea la ubicación del repartidor en el mapa.
- Califica al repartidor tras la entrega.

### 3.2 Repartidor
- Inicia sesión.
- Ve pedidos cercanos a su ubicación y pedidos asignados.
- Actualiza el estado del pedido (recogido, en camino, entregado).
- Usa mapa para ver la dirección del cliente.
- Recibe notificaciones de nuevos pedidos.

### 3.3 Administrador
- Inicia sesión en el sistema.
- Gestiona usuarios (alta, baja, edición).
- Gestiona el catálogo de productos.
- Ve todos los pedidos y su estado.
- Asigna o reasigna pedidos a repartidores.
- Genera reportes de ventas y entregas.

---

## 4️⃣ Historias de usuario

### 📱 Cliente
- Como cliente, quiero registrarme o iniciar sesión para poder acceder a mi cuenta.
- Como cliente, quiero navegar el catálogo de productos para elegir qué pedir.
- Como cliente, quiero agregar productos a un carrito para gestionar mi compra.
- Como cliente, quiero pagar mi pedido para finalizar la compra.
- Como cliente, quiero ver el estado de mi pedido en tiempo real para saber cuándo llegará.
- Como cliente, quiero ver la ubicación del repartidor en el mapa para rastrear la entrega.
- Como cliente, quiero calificar al repartidor después de la entrega para dar retroalimentación.

---

### 🚚 Repartidor
- Como repartidor, quiero iniciar sesión para acceder a mis pedidos.
- Como repartidor, quiero ver los pedidos cercanos a mi ubicación para planificar mis entregas.
- Como repartidor, quiero ver los pedidos asignados para planificar mi ruta.
- Como repartidor, quiero cambiar el estado del pedido (recogido, en camino, entregado) para mantener informado al cliente.
- Como repartidor, quiero ver la dirección del cliente en un mapa para navegar correctamente.
- Como repartidor, quiero recibir notificaciones de nuevos pedidos asignados para no perder entregas.

---

### 🛠️ Administrador
- Como administrador, quiero iniciar sesión para acceder al panel de control.
- Como administrador, quiero gestionar usuarios (alta, baja, edición) para mantener el sistema ordenado.
- Como administrador, quiero gestionar el catálogo de productos para actualizar la oferta.
- Como administrador, quiero ver todos los pedidos y su estado para monitorear operaciones.
- Como administrador, quiero asignar pedidos a repartidores para optimizar entregas.
- Como administrador, quiero generar reportes de ventas y entregas para análisis del negocio.

---

## 5️⃣ Reglas de negocio

- El cliente debe estar registrado para hacer pedidos.
- El repartidor solo puede ver pedidos cercanos a su ubicación y los asignados a él.
- El administrador puede reasignar pedidos entre repartidores.
- Un pedido solo puede estar en un estado a la vez: pendiente, confirmado, en camino, entregado.
- No se puede pagar un pedido que esté vacío.
- Los productos deben tener precio y stock (si aplica).
- El repartidor debe actualizar el estado del pedido en tiempo real.
- El cliente puede calificar solo pedidos entregados.
- Solo el administrador puede crear o eliminar productos.
- El sistema debe enviar notificaciones push para cambios de estado.

---

## 6️⃣ Requisitos técnicos iniciales

- **Backend:** NestJS, MySQL (Prisma o TypeORM), JWT, Websockets
- **Frontend:** Flutter 3+, Riverpod o Bloc, Google Maps o Mapbox
- **Notificaciones:** Firebase Cloud Messaging
- **Hosting:** Railway, Render o similar

---

# 📑 Documento de Diseño del Sistema
## DeliveryApp PRO - FASE 2: Diseño

---

## ✅ 2.1 Diagramas de Casos de Uso (versión texto)

### 📌 Casos de uso por rol

#### 📱 Cliente
- Registrarse / iniciar sesión
- Navegar catálogo
- Agregar productos al carrito
- Pagar pedido
- Ver estado del pedido en tiempo real
- Ver ubicación del repartidor en el mapa
- Calificar al repartidor

---

#### 🚚 Repartidor
- Iniciar sesión
- Ver pedidos cercanos
- Aceptar pedido
- Cambiar estado del pedido (recogido, en camino, entregado)
- Navegar al destino con mapa
- Recibir notificaciones

---

#### 🛠️ Administrador
- Iniciar sesión
- Crear/editar/borrar usuarios
- Crear/editar/borrar productos
- Ver pedidos y estados
- Asignar/reasignar pedidos
- Ver reportes

---

### ✅ ➜ Diagrama conceptual (texto)

Cliente <--> API <--> Pedido <--> Repartidor
Admin <--> API <--> Usuarios, Productos, Pedidos
Repartidor <--> API <--> Pedido, Notificaciones


---

## ✅ 2.2 Modelo Entidad-Relación (ER) preliminar

### 📌 Entidades principales

✅ **User**
- id (PK)
- name
- email
- password
- role (admin, cliente, repartidor)
- phone
- location_lat
- location_lng
- created_at

✅ **Product**
- id (PK)
- name
- description
- price
- image_url
- stock
- created_at

✅ **Order**
- id (PK)
- client_id (FK -> User)
- repartidor_id (FK -> User)
- status (pending, confirmed, en_camino, entregado)
- total_price
- address
- location_lat
- location_lng
- created_at

✅ **OrderItem**
- id (PK)
- order_id (FK -> Order)
- product_id (FK -> Product)
- quantity
- unit_price

✅ **Review**
- id (PK)
- order_id (FK -> Order)
- client_id (FK -> User)
- repartidor_id (FK -> User)
- rating
- comment
- created_at

✅ **Notification**
- id (PK)
- user_id (FK -> User)
- title
- message
- is_read
- created_at

---

### ✅ Relaciones clave

- User (1) ↔ (N) Order (como cliente)
- User (1) ↔ (N) Order (como repartidor)
- Order (1) ↔ (N) OrderItem
- Product (1) ↔ (N) OrderItem
- User (1) ↔ (N) Notification
- Order (1) ↔ (1) Review

---

## ✅ 2.3 Definición de tablas (DDL en texto)

✅ **users**
id INT PK AUTO_INCREMENT
name VARCHAR(100)
email VARCHAR(100) UNIQUE
password VARCHAR(255)
role ENUM('admin','cliente','repartidor')
phone VARCHAR(20)
location_lat DECIMAL(10,8)
location_lng DECIMAL(11,8)
created_at DATETIME

✅ **products**
id INT PK AUTO_INCREMENT
name VARCHAR(100)
description TEXT
price DECIMAL(10,2)
image_url VARCHAR(255)
stock INT
created_at DATETIME

✅ **orders**
id INT PK AUTO_INCREMENT
client_id INT FK
repartidor_id INT FK NULL
status ENUM('pending','confirmed','en_camino','entregado')
total_price DECIMAL(10,2)
address VARCHAR(255)
location_lat DECIMAL(10,8)
location_lng DECIMAL(11,8)
created_at DATETIME

✅ **order_items**
id INT PK AUTO_INCREMENT
order_id INT FK
product_id INT FK
quantity INT
unit_price DECIMAL(10,2)

✅ **reviews**
id INT PK AUTO_INCREMENT
order_id INT FK
client_id INT FK
repartidor_id INT FK
rating INT
comment TEXT
created_at DATETIME

✅ **notifications**
id INT PK AUTO_INCREMENT
user_id INT FK
title VARCHAR(255)
message TEXT
is_read BOOLEAN
created_at DATETIME

---
## ✅ 2.4 Arquitectura Modular NestJS (pensando en microservicios futuros)

src/
  auth/
  users/
  products/
  orders/
  order-items/
  reviews/
  notifications/
  common/
  database/
---
### ✅ Arquitectura técnica
El backend se desarrollará como un **monolito modular en NestJS**, con módulos independientes (Auth, Users, Products, Orders, etc.) conectados a una única base de datos MySQL.  

El diseño modular permite migrar a microservicios en el futuro, donde cada módulo se desplegaría como un servicio independiente con mensajería (RabbitMQ, Kafka) y un API Gateway para unificar la comunicación con los clientes móviles.
---
### ✅ Módulos NestJS

- **auth**: Registro de usuario, login, autenticación JWT, roles y permisos.
- **users**: Perfil de usuario, edición, localización actual.
- **products**: Catálogo de productos, precios, stock, imágenes.
- **orders**: Creación y gestión de pedidos, asignación de repartidores, cambio de estado.
- **order-items**: Productos específicos incluidos en cada pedido.
- **reviews**: Calificación y comentarios de los clientes.
- **notifications**: Envío y consulta de notificaciones push (FCM).
- **common**: Pipes, Guards, DTOs y utilidades compartidas.
- **database**: Configuración de TypeORM/Prisma, entidades y migraciones.


