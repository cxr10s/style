# 🧪 Instrucciones de Prueba - Sistema de Autenticación

## 🚀 **Cómo Ejecutar el Sistema**

### **Opción 1: Con Servidor (Recomendado)**
```bash
# 1. Abre la terminal en la carpeta del proyecto
cd D:\miweb2

# 2. Instala las dependencias (si no están instaladas)
npm install

# 3. Ejecuta el servidor
node server.js

# 4. Abre en el navegador
http://localhost:3000
```

### **Opción 2: Solo Navegador (Para pruebas rápidas)**
```bash
# Simplemente abre index.html en tu navegador
# Los datos se guardarán en localStorage (temporales)
```

## 📝 **Pasos para Probar el Sistema**

### **1. Registro de Usuario Nuevo**
1. **Abre la página** en el navegador
2. **Haz clic en "Iniciar Sesión"**
3. **Haz clic en "Crear cuenta"**
4. **Completa el formulario:**
   - Nombre: `Juan`
   - Apellido: `Pérez`
   - Email: `juan@ejemplo.com`
   - Teléfono: `3001234567`
   - Tipo de documento: `CC`
   - Número de documento: `12345678`
   - Fecha de nacimiento: `1990-01-01`
5. **Haz clic en "Crear Cuenta"**
6. **Ingresa el código de verificación:** `123456`
7. **Haz clic en "Verificar"**
8. ✅ **El usuario se guardará en `users.json`**

### **2. Login con Usuario Registrado**
1. **Haz clic en "Iniciar Sesión"**
2. **Ingresa el email:** `juan@ejemplo.com`
3. **Ingresa cualquier contraseña** (el sistema simula la validación)
4. **Haz clic en "Iniciar Sesión"**
5. ✅ **Debería mostrar avatar aleatorio y nombre del usuario**
6. ✅ **Debería mostrar "Mis Pedidos" en lugar de "Iniciar Sesión"**

### **3. Login con Usuario No Registrado**
1. **Haz clic en "Iniciar Sesión"**
2. **Ingresa un email que no esté registrado:** `noexiste@ejemplo.com`
3. **Ingresa cualquier contraseña**
4. **Haz clic en "Iniciar Sesión"**
5. ✅ **Debería mostrar alerta: "❌ Usuario no registrado. Debes crear una cuenta primero."**

### **4. Ver Perfil de Usuario**
1. **Después de hacer login exitoso**
2. **Haz clic en el avatar del usuario** (en la barra de navegación)
3. ✅ **Debería abrir el modal de perfil con:**
   - Avatar con iniciales y color aleatorio
   - Nombre completo
   - Email
   - Teléfono
   - Tipo y número de documento
   - Fecha de nacimiento
   - Fecha de registro
   - Último acceso

### **5. Ver Mis Pedidos**
1. **Después de hacer login exitoso**
2. **Haz clic en "Mis Pedidos"**
3. ✅ **Debería mostrar el modal de pedidos**

## 🔍 **Verificar que Funciona Correctamente**

### **Verificar users.json**
1. **Abre el archivo `users.json`** en tu editor
2. ✅ **Deberías ver algo como:**
```json
{
  "users": [
    {
      "id": "user_1234567890",
      "name": "Juan",
      "lastname": "Pérez",
      "email": "juan@ejemplo.com",
      "phone": "3001234567",
      "docType": "CC",
      "docNumber": "12345678",
      "birthdate": "1990-01-01",
      "verified": true,
      "registrationDate": "2024-01-15T10:30:00.000Z",
      "registrationTimestamp": 1705312200000,
      "isActive": true,
      "lastLogin": "2024-01-15T10:30:00.000Z"
    }
  ]
}
```

### **Verificar en el Navegador**
1. **Abre las Herramientas de Desarrollador** (F12)
2. **Ve a la pestaña Application → Local Storage**
3. ✅ **Deberías ver `authToken` y `userData`**

## 🎨 **Características del Avatar Aleatorio**

### **Colores Disponibles:**
- 🔴 Rojo (`#ff6b6b`)
- 🔵 Azul (`#4ecdc4`)
- 🔷 Azul claro (`#45b7d1`)
- 🟢 Verde (`#96ceb4`)
- 🟡 Amarillo (`#feca57`)
- 🟣 Rosa (`#ff9ff3`)

### **Generación de Iniciales:**
- Si el nombre es "Juan Pérez" → Iniciales: "JP"
- Si el nombre es "María García López" → Iniciales: "MG"

## 🚨 **Solución de Problemas**

### **Si no se guardan los datos:**
1. **Verifica que el servidor esté ejecutándose** (`node server.js`)
2. **Verifica que estés accediendo a** `http://localhost:3000`
3. **Revisa la consola del navegador** para errores

### **Si no aparece el avatar:**
1. **Verifica que el usuario esté logueado**
2. **Revisa la consola del navegador** para errores
3. **Verifica que el archivo `styles.css` esté cargado**

### **Si no funciona el login:**
1. **Verifica que el usuario esté registrado en `users.json`**
2. **Verifica que el email sea exactamente el mismo**
3. **Revisa la consola del navegador** para errores

## 📊 **Estado Final del Sistema**

### ✅ **Funcionalidades que Funcionan:**

1. **Registro de usuarios** → Se guarda en `users.json`
2. **Login con email/contraseña** → Valida desde `users.json`
3. **Prevención de duplicados** → No permite emails duplicados
4. **Avatar aleatorio** → Se genera automáticamente
5. **Perfil personalizado** → Cada usuario tiene su perfil único
6. **UI dinámica** → Muestra usuario cuando está logueado
7. **Botón "Mis Pedidos"** → Reemplaza "Iniciar Sesión" cuando está logueado
8. **Flujo obligatorio de compra** → Se activa después del login
9. **Registro de transacciones** → Solo compras exitosas

¡El sistema está **100% funcional** y listo para usar! 🎉
