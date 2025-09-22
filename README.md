# Estilo Activo - Sistema de Base de Datos

Sistema completo de base de datos para la tienda deportiva Estilo Activo, que permite almacenar usuarios registrados con Google/Facebook y sus órdenes de compra.

## 🚀 Características

- **Base de datos JSON**: Almacenamiento local en archivos JSON
- **Base de datos MySQL**: Integración opcional con MySQL
- **Autenticación social**: Google y Facebook
- **Gestión de usuarios**: Registro, login, actualización de datos
- **Gestión de órdenes**: Historial de compras por usuario
- **API REST**: Endpoints para todas las operaciones
- **Fallback**: Sistema de respaldo automático

## 📋 Requisitos

- Node.js 14.0.0 o superior
- NPM o Yarn
- MySQL 5.7+ (opcional)

## 🛠️ Instalación

### 1. Instalar dependencias

```bash
npm install
```

### 2. Configurar base de datos (Opcional - MySQL)

Si quieres usar MySQL, edita el archivo `mysql-config.js`:

```javascript
const dbConfig = {
    host: 'localhost',
    user: 'tu_usuario',
    password: 'tu_password',
    database: 'estilo_activo_db',
    port: 3306
};
```

### 3. Iniciar el servidor

```bash
# Desarrollo
npm run dev

# Producción
npm start
```

El servidor se ejecutará en `http://localhost:3000`

## 🗄️ Estructura de Base de Datos

### Archivos JSON (Por defecto)
- `users.json` - Datos de usuarios
- `orders.json` - Órdenes de compra
- `products.json` - Catálogo de productos

### MySQL (Opcional)
- Tabla `users` - Información de usuarios
- Tabla `orders` - Órdenes de compra
- Tabla `order_items` - Items de cada orden
- Tabla `products` - Catálogo de productos
- Tabla `user_sessions` - Sesiones de usuarios

## 📊 API Endpoints

### Usuarios
- `GET /api/users` - Obtener todos los usuarios
- `GET /api/users/email/:email` - Buscar usuario por email
- `POST /api/users` - Crear nuevo usuario
- `PUT /api/users/:userId` - Actualizar usuario

### Órdenes
- `POST /api/orders` - Crear nueva orden
- `GET /api/users/:userId/orders` - Órdenes de un usuario

### Estadísticas
- `GET /api/stats` - Estadísticas generales
- `GET /api/export` - Exportar datos

## 🔧 Configuración

### Variables de entorno

Crea un archivo `.env`:

```env
PORT=3000
DB_HOST=localhost
DB_USER=estilo_activo_user
DB_PASSWORD=tu_password_seguro
DB_NAME=estilo_activo_db
NODE_ENV=development
```

### Configuración de MySQL

1. Crear base de datos:
```sql
CREATE DATABASE estilo_activo_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

2. Crear usuario:
```sql
CREATE USER 'estilo_activo_user'@'localhost' IDENTIFIED BY 'tu_password_seguro';
GRANT ALL PRIVILEGES ON estilo_activo_db.* TO 'estilo_activo_user'@'localhost';
FLUSH PRIVILEGES;
```

3. Ejecutar script de configuración:
```bash
npm run setup-mysql
```

## 📱 Uso del Sistema

### Registro de Usuarios
1. Usuario hace clic en "Iniciar Sesión"
2. Selecciona Google o Facebook
3. Se autentica con su cuenta
4. Los datos se almacenan automáticamente en la base de datos

### Datos Almacenados
- **Información personal**: Nombre, email, teléfono
- **Datos de autenticación**: Proveedor (Google/Facebook), foto
- **Información adicional**: Dirección, ciudad, país
- **Historial**: Fechas de registro y último login

### Órdenes de Compra
1. Usuario agrega productos al carrito
2. Procede al pago
3. Se autentica si es necesario
4. La orden se guarda automáticamente en la base de datos

## 🔒 Seguridad

- **Validación de datos**: Todos los inputs se validan
- **Sanitización**: Datos se limpian antes de almacenar
- **CORS**: Configurado para seguridad
- **Rate limiting**: Protección contra spam
- **Validación de sesiones**: Verificación de autenticación

## 📈 Monitoreo

### Estadísticas disponibles
- Total de usuarios registrados
- Total de órdenes procesadas
- Ingresos generados
- Usuarios por proveedor (Google/Facebook)
- Órdenes por mes

### Logs
- Registro de usuarios nuevos
- Actualizaciones de perfil
- Órdenes procesadas
- Errores del sistema

## 🚨 Resolución de Problemas

### Error de conexión a MySQL
```bash
# Verificar que MySQL esté ejecutándose
sudo systemctl status mysql

# Verificar credenciales en mysql-config.js
```

### Error de permisos
```bash
# Dar permisos al usuario de la base de datos
sudo mysql -u root -p
GRANT ALL PRIVILEGES ON estilo_activo_db.* TO 'estilo_activo_user'@'localhost';
FLUSH PRIVILEGES;
```

### Error de puerto ocupado
```bash
# Cambiar puerto en server.js o .env
PORT=3001
```

## 📞 Soporte

Para soporte técnico o reportar bugs:
- Email: soporte@estiloactivo.com
- GitHub Issues: [Crear issue](https://github.com/estilo-activo/database/issues)

## 📄 Licencia

MIT License - Ver archivo LICENSE para más detalles.

---

**Estilo Activo** - Tu destino para productos deportivos de primera calidad.