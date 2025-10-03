# Detector de Posición Vertical 📱

Una aplicación web que combina **geolocalización** y **detección de orientación** para mostrar el texto "Hola" solo cuando el dispositivo esté completamente vertical.

## 🎯 Funcionalidades

- **Geolocalización**: Obtiene y muestra las coordenadas GPS del usuario
- **Detección de Orientación**: Usa sensores del dispositivo para detectar la posición
- **Texto Condicional**: Solo muestra "Hola" cuando el teléfono está perfectamente vertical
- **Interfaz Visual**: Indicadores en tiempo real del estado del dispositivo

## 🚀 Cómo usar

### 1. Iniciar el proyecto
```bash
cd orientation-detector
npm run dev
```

### 2. Acceder desde dispositivo móvil
- Abre `http://localhost:4321` en tu teléfono
- O usa `npm run dev -- --host` para acceso en red local

### 3. Conceder permisos
- **Ubicación**: Permite acceso a GPS cuando el navegador lo solicite
- **Sensores**: En iOS 13+, presiona el botón "Activar Sensor de Orientación"

### 4. Probar la funcionalidad
- Mantén el teléfono **completamente vertical** (derecho)
- El texto "Hola" aparecerá solo en esta posición
- Inclina el teléfono y el texto desaparecerá

## 📱 Cómo funciona

### Detección de Orientación Vertical
La aplicación usa `DeviceOrientationEvent` para monitorear:
- **Beta**: Inclinación adelante/atrás (-180° a 180°)
- **Gamma**: Inclinación izquierda/derecha (-90° a 90°)
- **Alpha**: Rotación (0° a 360°)

### Criterio de "Vertical"
El dispositivo se considera vertical cuando:
- `|Beta| < 15°` (tolerancia de ±15 grados)
- `|Gamma| < 15°` (tolerancia de ±15 grados)

### Estados Visuales
- ✅ **Verde**: Dispositivo vertical → "Hola" visible
- ❌ **Rojo**: Dispositivo inclinado → "Hola" oculto

## 🔧 Tecnologías utilizadas

- **Astro**: Framework web moderno
- **JavaScript Vanilla**: Para lógica del navegador
- **CSS3**: Animaciones y gradientes
- **APIs Web**:
  - `Geolocation API`: Para coordenadas GPS
  - `DeviceOrientationEvent`: Para sensores de orientación

## 📊 Datos mostrados

1. **Coordenadas GPS**: Latitud, longitud y precisión
2. **Estado de Orientación**: Vertical vs Inclinado
3. **Datos del Sensor**: Valores Beta, Gamma y Alpha en tiempo real
4. **Mensaje Principal**: "Hola" (solo cuando está vertical)

## 🎨 Características de UX

- **Transiciones suaves**: El texto aparece/desaparece con animaciones
- **Feedback visual**: Colores que indican el estado actual
- **Datos en tiempo real**: Valores de sensores actualizándose constantemente
- **Responsive**: Funciona en diferentes tamaños de pantalla

## 🔒 Consideraciones de Permisos

### iOS 13+ (Safari)
- Requiere interacción del usuario para activar sensores
- Botón especial para solicitar permisos

### Android (Chrome/Firefox)
- Permisos se solicitan automáticamente
- No requiere interacción adicional

### Ubicación
- Ambas plataformas requieren confirmación del usuario
- Funciona mejor con GPS activado

## 🛠 Personalización

### Cambiar tolerancia de orientación
En `src/pages/index.astro`, línea ~191:
```javascript
const tolerance = 15; // Cambiar este valor (en grados)
```

### Modificar el texto mostrado
En `src/pages/index.astro`, línea ~86:
```html
<div id="hello" class="hello-text">Hola</div> <!-- Cambiar "Hola" -->
```

### Ajustar estilos
Modificar las reglas CSS en la sección `<style>` del archivo.

## 🧪 Pruebas

### En escritorio
- Los sensores pueden no estar disponibles
- Se mostrará mensaje de "no disponible"
- La geolocalización sí funcionará

### En móvil
- Funcionalidad completa disponible
- Probar en diferentes orientaciones
- Verificar permisos del navegador

## 📝 Notas técnicas

- La detección funciona mejor en dispositivos móviles reales
- Los emuladores pueden no simular correctamente los sensores
- HTTPS es requerido para geolocalización en producción
- Los valores de orientación pueden variar entre dispositivos