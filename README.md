# 📦 ENTREGA FINAL — Sistema de Gestión de Inventario

Proyecto desarrollado como **Entrega Final** para la materia **Plataforma de Desarrollo - Web / Backend**.  
La aplicación implementa un sistema **full stack** de gestión de inventario con autenticación, control de roles y base de datos relacional.

---

## 🚀 Tecnologías utilizadas

### Backend
- **Node.js**
- **Express**
- **SQLite** (Base de datos relacional)
- **JWT (JSON Web Tokens)** para autenticación
- **bcryptjs** para hash de contraseñas

### Frontend
- **React**
- **React Router**
- **Fetch API**
- **CSS personalizado** (interfaz tipo panel administrativo)

---

## 🗄️ Base de Datos (SQLite)

El sistema utiliza una **base de datos relacional SQLite**, creada automáticamente al iniciar el servidor.

### Tablas implementadas

#### 📁 `categorias`
- `id` (PK)
- `nombre` (único)

#### 📦 `productos`
- `id` (PK)
- `nombre`
- `precio`
- `stock`
- `categoria_id` (FK → categorias.id)

Relación **uno a muchos** entre categorías y productos.

#### 👤 `usuarios`
- `id` (PK)
- `username` (único)
- `password_hash` (contraseña encriptada)
- `role` (`admin` | `usuario`)

---

## 👤 Usuario administrador por defecto

Si la base de datos no contiene usuarios, el sistema crea automáticamente:

- **Usuario:** `admin`
- **Contraseña:** `1234`
- **Rol:** `admin`

Las contraseñas se almacenan **hasheadas con bcrypt**, no en texto plano.

---

## 🔐 Autenticación y control de acceso

- Login mediante **JWT**
- El token debe enviarse en cada request protegida:


### Roles
- **admin**
- Gestión completa de productos
- Gestión completa de usuarios
- **usuario**
- Gestión de productos
- Sin acceso a la gestión de usuarios

---

## 📡 Endpoints principales

### Autenticación
- `POST /api/login`

### Productos
- `GET /api/productos`
- `GET /api/productos/:id`
- `POST /api/productos` *(requiere login)*
- `PUT /api/productos/:id` *(requiere login)*
- `DELETE /api/productos/:id` *(requiere login)*

### Usuarios (solo administradores)
- `GET /api/usuarios`
- `POST /api/usuarios`
- `DELETE /api/usuarios/:id`

---

## 🖥️ Frontend

- Login obligatorio
- Panel de inventario con:
- Listado de productos
- Alta, edición y eliminación
- Vista de detalle de producto
- Panel de **Gestión de Usuarios** visible solo para administradores
- Manejo de errores (401 / 403)
- Interfaz tipo **panel administrativo**

---

## ▶️ Cómo ejecutar el proyecto

### Backend
```bash
cd server
npm install
npm run dev

## 🗄 Persistencia de datos (SQLite)

La aplicación utiliza **SQLite** como base de datos relacional local.

- Los datos se almacenan en el archivo:

- Este archivo **no se versiona en Git** (está incluido en `.gitignore`) por buenas prácticas.
- Mientras el archivo `database.db` exista, **los usuarios y productos creados se mantienen entre reinicios del servidor**.
- Si el archivo se elimina, el sistema:
- recrea automáticamente las tablas
- inserta categorías por defecto
- crea un usuario administrador inicial

### Usuario administrador por defecto
- **Usuario:** `admin`
- **Contraseña:** `1234`

Este comportamiento es intencional y permite levantar el proyecto desde cero sin configuración adicional.



