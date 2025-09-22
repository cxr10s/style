# Implementación de Apertura Condicional de WhatsApp

## 🎯 Objetivo
Implementar una funcionalidad que detecte automáticamente si WhatsApp está instalado en el dispositivo móvil y abra la app nativa o redirija a WhatsApp Web según corresponda.

## 🔧 Funcionalidades Implementadas

### 1. Función `openWhatsApp(phone, message)`
- **Propósito**: Función principal que maneja la detección condicional
- **Parámetros**:
  - `phone`: Número de teléfono (formato internacional sin +)
  - `message`: Mensaje a enviar
- **Lógica**:
  - Intenta abrir WhatsApp usando el esquema `whatsapp://`
  - Detecta si la app se abre mediante eventos de visibilidad
  - Si no se detecta apertura en 1.5 segundos, redirige a `https://api.whatsapp.com`

### 2. Función `tryOpenWhatsApp(message)`
- **Propósito**: Función de alto nivel que decide qué estrategia usar
- **Lógica**:
  - En dispositivos móviles: Usa `openWhatsApp()` con detección condicional
  - En desktop: Redirige directamente a WhatsApp Web

### 3. Detección de Dispositivos Móviles
- **Función**: `isMobileDevice()`
- **Criterios**: Detecta Android, iOS, Windows Phone, etc.
- **Regex**: `/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini|Mobile|mobile|CriOS/i`

## 🚀 Cómo Funciona

### En Dispositivos Móviles:
1. **Intento de apertura**: Se ejecuta `window.location.href = whatsapp://send?...`
2. **Detección de éxito**: Se escuchan eventos `visibilitychange`, `blur`, y `pagehide`
3. **Timeout de seguridad**: Si no se detecta apertura en 1.5s, redirige a web
4. **Limpieza**: Se limpian todos los event listeners después de 3s

### En Desktop:
- Redirige directamente a `https://api.whatsapp.com/send?...`

## 🧪 Funciones de Prueba

### `testWhatsAppFunctionality()`
- Prueba la funcionalidad básica de WhatsApp
- Mensaje: "Hola, esta es una prueba de la funcionalidad de WhatsApp desde Estilo Activo."

### `testWhatsAppConditional()`
- Prueba específica de la detección condicional
- Incluye logs detallados para debugging
- Mensaje: "🧪 Prueba de detección condicional de WhatsApp - Estilo Activo"

### `debugMobileDetection()`
- Muestra información detallada sobre la detección de dispositivos móviles
- Incluye User Agent, ancho de pantalla, soporte táctil, etc.

## 📱 Compatibilidad

### Navegadores Móviles Soportados:
- ✅ Chrome Mobile (Android/iOS)
- ✅ Safari Mobile (iOS)
- ✅ Firefox Mobile (Android/iOS)
- ✅ Samsung Internet (Android)
- ✅ Edge Mobile (Android/iOS)

### Navegadores Desktop:
- ✅ Chrome
- ✅ Firefox
- ✅ Safari
- ✅ Edge
- ✅ Opera

## 🔍 Cómo Probar

### 1. En la Consola del Navegador:
```javascript
// Prueba básica
testWhatsAppFunctionality();

// Prueba de detección condicional
testWhatsAppConditional();

// Debug de detección móvil
debugMobileDetection();
```

### 2. En el Modal de Reserva:
- Llena el formulario de reserva
- Haz clic en "Reservar por WhatsApp"
- Observa el comportamiento según el dispositivo

### 3. Verificar Logs:
- Abre las herramientas de desarrollador (F12)
- Ve a la pestaña "Console"
- Ejecuta las funciones de prueba
- Observa los logs detallados

## ⚙️ Configuración

### Número de WhatsApp:
- **Actual**: `573116039256` (Colombia)
- **Ubicación**: Variable `whatsappNumber` en `tryOpenWhatsApp()`

### Timeouts:
- **Detección de app**: 1500ms (1.5 segundos)
- **Limpieza de listeners**: 3000ms (3 segundos)

## 🐛 Troubleshooting

### Problemas Comunes:

1. **No se abre la app en móvil**:
   - Verificar que WhatsApp esté instalado
   - Comprobar que el navegador permita esquemas personalizados
   - Revisar logs en la consola

2. **Redirección a web inmediata**:
   - El timeout de 1.5s puede ser muy corto
   - Verificar que los event listeners estén funcionando

3. **No funciona en algunos navegadores**:
   - Algunos navegadores bloquean esquemas personalizados
   - Usar `https://api.whatsapp.com` como fallback

### Logs de Debug:
```javascript
// Verificar detección móvil
console.log('Es móvil:', isMobileDevice());
console.log('User Agent:', navigator.userAgent);

// Probar apertura directa
window.location.href = 'whatsapp://send?phone=573116039256&text=Prueba';
```

## 📋 Notas Técnicas

### Eventos Utilizados:
- `visibilitychange`: Detecta cuando la página pierde visibilidad
- `blur`: Detecta cuando la ventana pierde el foco
- `pagehide`: Detecta cuando la página se oculta

### Esquemas de URL:
- **App nativa**: `whatsapp://send?phone={number}&text={message}`
- **Web**: `https://api.whatsapp.com/send?phone={number}&text={message}`

### Manejo de Errores:
- Try-catch en la apertura de la app
- Timeout de seguridad para evitar bloqueos
- Limpieza automática de recursos

## 🎉 Resultado Final

La implementación proporciona una experiencia fluida:
- **Con WhatsApp instalado**: Abre la app nativa directamente
- **Sin WhatsApp**: Redirige automáticamente a WhatsApp Web
- **En desktop**: Usa WhatsApp Web directamente
- **Fallback robusto**: Siempre funciona, independientemente del estado de la app
