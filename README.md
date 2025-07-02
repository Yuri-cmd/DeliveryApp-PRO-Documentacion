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

