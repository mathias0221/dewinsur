# Vectoris Global - Sistema de Casilleros

## 📦 Descripción del Sistema

Sistema completo de gestión de casilleros internacionales con tecnología web moderna, diseñado para empresas de logística y envíos. Ofrece gestión integral de paquetes, tarifas personalizadas por ciudad, seguimiento en tiempo real y control administrativo completo.

## 🚀 Características Principales

### ✨ **Para Clientes**
- **Dashboard Personal** - Gestión completa de paquetes
- **Selección de Envíos** - Aéreo/Marítimo con costos en tiempo real
- **Tarifas por Ciudad** - Precios personalizados según ubicación
- **Seguimiento en Vivo** - Estado actualizado de cada paquete
- **Confirmación de Envíos** - Proceso simple y seguro

### 🎯 **Para Administradores**
- **Panel de Control Completo** - Gestión integral del sistema
- **Gestión de Clientes** - Aprobación y administración
- **Configuración de Tarifas** - Por ciudad y rangos de peso
- **Análisis de Ganancias** - Optimización de rentabilidad
- **Gestión de Contenedores** - Agrupamiento inteligente
- **Reportes y Exportación** - Datos detallados

### 💰 **Sistema de Tarifas**
- **Tarifas por Ciudad** - Caracas, Valencia, Maracaibo, etc.
- **Rangos de Peso** - Precios escalonados por peso/volumen
- **Peso Dimensional** - Cálculo automático (divisor 166)
- **Métodos de Envío** - Aéreo y Marítimo
- **Costos Dinámicos** - Actualización en tiempo real

## 🛠️ **Tecnología Utilizada**

### **Frontend Puro**
- **HTML5** - Estructura semántica moderna
- **CSS3** - Variables, Grid, Flexbox, Animaciones
- **JavaScript ES6+** - Sin frameworks externos
- **LocalStorage** - Base de datos nativa del navegador

### **Sin Dependencias**
- ❌ No requiere Node.js
- ❌ No requiere PHP/MySQL
- ❌ No requiere frameworks
- ✅ 100% JavaScript Vanilla
- ✅ Compatible con todos los navegadores modernos

## 📁 **Estructura del Proyecto**

```
vectoris-production-ready/
├── index.html              # Página principal
├── dashboard.html           # Dashboard de clientes
├── admin.html              # Panel administrativo
├── registro.html           # Formulario de registro
├── tarifas.html           # Página de tarifas públicas
├── recursos.html          # Recursos y ayuda
├── css/
│   ├── styles.css         # Estilos principales
│   └── components.css     # Estilos de componentes
├── js/
│   ├── main.js           # Funcionalidades principales
│   ├── dashboard.js      # Dashboard cliente
│   └── admin.js          # Panel administrativo
├── assets/
│   ├── images/           # Imágenes y recursos
│   └── icons/            # Iconos del sistema
└── README.md             # Este archivo
```

## 🚀 **Instalación y Configuración**

### **Requisitos Mínimos**
- Servidor web estático (Apache, Nginx)
- Dominio personalizado
- SSL Certificate (recomendado)

### **Pasos de Instalación**

1. **Subir Archivos**
   ```bash
   # Subir todos los archivos al directorio raíz del hosting
   scp -r vectoris-production-ready/* user@hosting.com:/public_html/
   ```

2. **Configurar Dominio**
   - Apuntar DNS al servidor
   - Configurar SSL (Let's Encrypt)
   - Verificar acceso

3. **Listo para Usar**
   - Acceder a `https://tudominio.com`
   - El sistema está operativo inmediatamente

## 🎮 **Uso del Sistema**

### **Flujo de Cliente**
1. **Registro** - Crear cuenta en el sistema
2. **Aprobación** - Admin aprueba la cuenta
3. **Login** - Acceso al dashboard personal
4. **Paquetes** - Ver guías asignadas
5. **Selección** - Elegir método de envío
6. **Confirmación** - Confirmar envío

### **Flujo de Administrador**
1. **Login Admin** - Acceso al panel
2. **Clientes** - Gestionar usuarios
3. **Paquetes** - Asignar guías
4. **Tarifas** - Configurar precios
5. **Análisis** - Optimizar ganancias
6. **Reportes** - Exportar datos

## 💡 **Funcionalidades Detalladas**

### **📊 Dashboard de Clientes**
- Estadísticas en tiempo real
- Lista de paquetes con detalles
- Costos calculados automáticamente
- Estados de envío actualizados
- Interfaz responsive y moderna

### **🎛️ Panel Administrativo**
- Sidebar navegación intuitiva
- Múltiples secciones organizadas
- Búsqueda y filtrado avanzado
- Modales para acciones específicas
- Exportación de datos en CSV

### **💰 Sistema de Pagos**
- Cálculo automático por ciudad
- Considera peso dimensional
- Diferencia aéreo/marítimo
- Generación de facturas
- Estados de pago

### **📦 Gestión de Contenedores**
- Creación de contenedores personalizados
- Cálculo de volumen y capacidad
- Agrupamiento inteligente de paquetes
- Optimización de espacio
- Análisis de rentabilidad

## 🔧 **Configuración de Tarifas**

### **Tarifas por Ciudad**
```javascript
// Ejemplo de configuración
const cityTariffs = [
  {
    city: "Caracas",
    aereoRate: 5.50,    // $ por libra
    maritimoRate: 8.50  // $ por pie cúbico
  },
  {
    city: "Valencia", 
    aereoRate: 4.80,
    maritimoRate: 7.80
  }
];
```

### **Cálculo de Costos**
```javascript
// Peso dimensional (divisor 166)
const dimensionalWeight = (L * W * H) / 166;

// Peso cobrable (el mayor)
const chargeableWeight = Math.max(realWeight, dimensionalWeight);

// Costo final
const cost = chargeableWeight * cityTariff.aereoRate;
```

## 🎨 **Diseño y UX**

### **Diseño Moderno**
- Interfaz limpia y profesional
- Colores corporativos consistentes
- Iconos intuitivos y claros
- Animaciones suaves y naturales
- Diseño 100% responsive

### **Experiencia de Usuario**
- Navegación intuitiva
- Feedback visual inmediato
- Formularios validados en tiempo real
- Notificaciones contextuales
- Accesibilidad mejorada

## 📱 **Compatibilidad y Responsive**

### **Dispositivos Soportados**
- ✅ Desktop (1920px+)
- ✅ Laptop (1366px+)
- ✅ Tablet (768px+)
- ✅ Mobile (320px+)

### **Navegadores Compatibles**
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## 🔒 **Seguridad**

### **Seguridad Implementada**
- Validación de datos en frontend
- Sanitización de entradas
- Almacenamiento local cifrado
- Sin exposición de datos sensibles
- Protección contra XSS básica

### **Mejoras Recomendadas**
- Implementar backend con Node.js/PHP
- Agregar autenticación con JWT
- Configurar HTTPS obligatorio
- Implementar CORS
- Agregar rate limiting

## 📈 **Escalabilidad**

### **Capacidad Actual**
- **Usuarios**: 1-100 simultáneos (ideal)
- **Datos**: 5-10MB por usuario (LocalStorage)
- **Rendimiento**: Excelente para PYMES

### **Para Crecimiento**
- Migrar a base de datos SQL/NoSQL
- Implementar backend RESTful
- Agregar sistema de caché
- Configurar CDN
- Implementar microservicios

## 🚨 **Limitaciones Conocidas**

### **LocalStorage**
- ✅ Almacenamiento persistente
- ✅ Sin necesidad de servidor
- ⚠️ 5-10MB por dominio
- ⚠️ Por dispositivo (no sincronizado)
- ⚠️ Se puede borrar manualmente

### **Soluciones**
- Exportación automática de datos
- Sincronización manual
- Backup programado
- Migración a backend cuando crezca

## 🎯 **Casos de Uso**

### **Ideal Para**
- Empresas de casilleros pequeños/medianos
- Startups de logística internacional
- Operadores de envíos regionales
- Empresas con 50-500 clientes

### **No Recomendado Para**
- Empresas grandes (+1000 clientes)
- Sistemas con alta concurrencia
- Aplicaciones críticas de misión
- Requerimientos de alta seguridad

## 🔄 **Mantenimiento**

### **Mantenimiento Básico**
- Backup regular de datos
- Actualización de contenido
- Monitoreo de rendimiento
- Limpieza de datos antiguos

### **Actualizaciones**
- Mejoras de UI/UX
- Nuevas funcionalidades
- Parches de seguridad
- Optimización de rendimiento

## 📞 **Soporte**

### **Documentación**
- Guía de instalación completa
- Manual de usuario detallado
- Referencia de API
- Preguntas frecuentes

### **Recursos Adicionales**
- Video tutoriales
- Webinars de capacitación
- Comunidad de usuarios
- Soporte técnico prioritario

## 🚀 **Futuro del Sistema**

### **Próximas Versiones**
- [ ] Backend con Node.js
- [ ] Base de datos PostgreSQL
- [ ] API RESTful
- [ ] Aplicación móvil
- [ ] Integración de pagos
- [ ] Sistema de notificaciones
- [ ] Reportes avanzados
- [ ] Inteligencia artificial

### **Roadmap 2024**
- Q1: Backend y API
- Q2: App móvil React Native
- Q3: Sistema de pagos Stripe
- Q4: IA y analytics

---

## 📄 **Licencia**

Este proyecto es propiedad de Vectoris Global. Todos los derechos reservados.

## 🤝 **Contacto**

- **Email**: info@vectorisglobal.com
- **Teléfono**: +1-305-123-4567
- **WhatsApp**: +58-412-123-4567
- **Web**: https://vectorisglobal.com

---

**Vectoris Global** - Tu socio confiable para envíos internacionales 🌍✈️📦
