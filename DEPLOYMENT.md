# 🚀 Guía de Despliegue - Vectoris Global

## 📋 Requisitos Previos

### **Hosting Requerido**
- ✅ Servidor web estático (Apache, Nginx, LiteSpeed)
- ✅ Soporte para HTML5, CSS3, JavaScript ES6+
- ✅ Acceso FTP/FileManager o SSH
- ✅ Dominio personalizado
- ✅ SSL Certificate (HTTPS)

### **Hosting Recomendados**
- **Hostinger** - Premium Web Hosting ($2.99/mes)
- **Bluehost** - Shared Hosting ($2.95/mes)
- **SiteGround** - GoGeek Hosting ($4.99/mes)
- **Vercel** - Frontend Hosting (Gratis para empezar)
- **Netlify** - Static Site Hosting (Gratis para empezar)

## 🔄 Proceso de Despliegue

### **Paso 1: Preparación de Archivos**

1. **Descargar el proyecto completo**
   ```bash
   # Descargar desde el repositorio
   git clone https://github.com/tu-repo/vectoris-global.git
   cd vectoris-global
   ```

2. **Verificar estructura de archivos**
   ```
   vectoris-production-ready/
   ├── index.html              # ✅ Página principal
   ├── dashboard.html           # ✅ Dashboard clientes
   ├── admin.html              # ✅ Panel administrativo  
   ├── registro.html           # ✅ Formulario registro
   ├── tarifas.html           # ✅ Página tarifas
   ├── recursos.html          # ✅ Recursos/ayuda
   ├── css/
   │   ├── styles.css         # ✅ Estilos principales
   │   └── components.css     # ✅ Componentes
   ├── js/
   │   ├── main.js           # ✅ Funcionalidad principal
   │   ├── dashboard.js      # ✅ Dashboard cliente
   │   ├── admin.js          # ✅ Panel admin
   │   └── registro.js       # ✅ Formulario registro
   └── README.md             # ✅ Documentación
   ```

### **Paso 2: Configuración del Dominio**

1. **Apuntar DNS al hosting**
   ```
   # Ejemplo de registros DNS
   A     @        192.168.1.1
   A     www      192.168.1.1
   CNAME mail     mail.tudominio.com
   ```

2. **Configurar SSL Certificate**
   - Usar Let's Encrypt (gratuito)
   - O SSL del proveedor hosting
   - Redirigir HTTP a HTTPS

### **Paso 3: Subida de Archivos**

#### **Opción A: FTP/FileManager**
```bash
# Conectar por FTP
ftp tudominio.com
# Usuario: tu-usuario
# Contraseña: tu-contraseña

# Navegar al directorio raíz
cd public_html/
# O
cd www/
# O
cd httpdocs/

# Subir todos los archivos
mput -r vectoris-production-ready/* .
```

#### **Opción B: SSH/SFTP**
```bash
# Conectar por SSH
ssh usuario@tudominio.com

# Navegar al directorio web
cd /home/usuario/public_html/

# Subir archivos
scp -r vectoris-production-ready/* usuario@tudominio.com:/home/usuario/public_html/
```

#### **Opción C: Git Deploy (si el hosting lo permite)**
```bash
# En el servidor
cd /home/usuario/public_html/
git clone https://github.com/tu-repo/vectoris-global.git .
```

### **Paso 4: Verificación de Despliegue**

1. **Acceder al sitio**
   ```
   https://tudominio.com
   ```

2. **Verificar páginas principales**
   - ✅ `https://tudominio.com` - Página principal
   - ✅ `https://tudominio.com/registro.html` - Registro
   - ✅ `https://tudominio.com/dashboard.html` - Dashboard
   - ✅ `https://tudominio.com/admin.html` - Panel admin

3. **Verificar recursos**
   - ✅ CSS cargando correctamente
   - ✅ JavaScript funcionando
   - ✅ Imágenes y iconos visibles
   - ✅ Formularios operativos

## 🔧 Configuración Específica

### **Apache (.htaccess)**
```apache
# Habilitar compresión
<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/plain
    AddOutputFilterByType DEFLATE text/html
    AddOutputFilterByType DEFLATE text/xml
    AddOutputFilterByType DEFLATE text/css
    AddOutputFilterByType DEFLATE application/xml
    AddOutputFilterByType DEFLATE application/xhtml+xml
    AddOutputFilterByType DEFLATE application/rss+xml
    AddOutputFilterByType DEFLATE application/javascript
    AddOutputFilterByType DEFLATE application/x-javascript
</IfModule>

# Cache de navegador
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
    ExpiresByType image/png "access plus 1 month"
    ExpiresByType image/jpg "access plus 1 month"
    ExpiresByType image/gif "access plus 1 month"
    ExpiresByType image/ico "access plus 1 year"
    ExpiresByType image/svg+xml "access plus 1 year"
</IfModule>

# Forzar HTTPS
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# URLs amigables
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ $1.html [L]
```

### **Nginx (nginx.conf)**
```nginx
server {
    listen 80;
    server_name tudominio.com www.tudominio.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name tudominio.com www.tudominio.com;
    
    root /var/www/tudominio;
    index index.html;
    
    # SSL
    ssl_certificate /path/to/ssl/cert.pem;
    ssl_certificate_key /path/to/ssl/private.key;
    
    # Compresión
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    
    # Cache
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
    
    # URLs amigables
    location / {
        try_files $uri $uri/ $uri.html =404;
    }
    
    # Seguridad
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'" always;
}
```

## 🔒 Configuración de Seguridad

### **Headers de Seguridad**
```html
<!-- Agregar en index.html -->
<meta http-equiv="X-Content-Type-Options" content="nosniff">
<meta http-equiv="X-Frame-Options" content="DENY">
<meta http-equiv="X-XSS-Protection" content="1; mode=block">
<meta http-equiv="Referrer-Policy" content="strict-origin-when-cross-origin">
```

### **robots.txt**
```txt
User-agent: *
Allow: /
Disallow: /admin.html
Disallow: /*.json$

Sitemap: https://tudominio.com/sitemap.xml
```

### **sitemap.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
        <loc>https://tudominio.com/</loc>
        <lastmod>2024-01-01</lastmod>
        <priority>1.0</priority>
    </url>
    <url>
        <loc>https://tudominio.com/registro.html</loc>
        <lastmod>2024-01-01</lastmod>
        <priority>0.8</priority>
    </url>
    <url>
        <loc>https://tudominio.com/tarifas.html</loc>
        <lastmod>2024-01-01</lastmod>
        <priority>0.8</priority>
    </url>
</urlset>
```

## 📊 Monitoreo y Mantenimiento

### **Google Analytics**
```html
<!-- Agregar en todas las páginas -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### **Google Search Console**
1. Verificar propiedad en Google Search Console
2. Enviar sitemap
3. Monitorear errores de rastreo
4. Revisar rendimiento

### **Monitoreo de Rendimiento**
```javascript
// Agregar en main.js
if ('performance' in window) {
    window.addEventListener('load', function() {
        const perfData = performance.getEntriesByType('navigation')[0];
        const pageLoadTime = perfData.loadEventEnd - perfData.loadEventStart;
        console.log('Page load time:', pageLoadTime, 'ms');
        
        // Enviar a analytics si es necesario
        if (typeof gtag !== 'undefined') {
            gtag('event', 'page_load_time', {
                value: Math.round(pageLoadTime),
                custom_parameter: 'page_load_time'
            });
        }
    });
}
```

## 🚨 Solución de Problemas Comunes

### **Problema: Página en blanco**
```bash
# Verificar consola del navegador
# F12 → Console → Buscar errores

# Soluciones comunes:
# 1. Verificar rutas de CSS/JS
# 2. Revisar permisos de archivos
# 3. Comprobar sintaxis HTML/JS
```

### **Problema: LocalStorage no funciona**
```javascript
// Verificar disponibilidad
if (typeof(Storage) !== "undefined") {
    // LocalStorage disponible
} else {
    // Mostrar mensaje de compatibilidad
    showNotification('Tu navegador no es compatible', 'error');
}
```

### **Problema: Redirección HTTPS**
```apache
# Forzar HTTPS en .htaccess
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

### **Problema: CORS (si se usa API externa)**
```javascript
// En el servidor API
header('Access-Control-Allow-Origin: https://tudominio.com');
header('Access-Control-Allow-Methods: GET, POST, OPTIONS');
header('Access-Control-Allow-Headers: Content-Type');
```

## 📈 Optimización de Rendimiento

### **Minificación de CSS/JS**
```bash
# Usar herramientas online o CLI
# CSS Minifier: https://cssminifier.com/
# JS Minifier: https://javascript-minifier.com/
```

### **Optimización de Imágenes**
```bash
# Usar ImageOptim o TinyPNG
# Convertir a WebP si es compatible
```

### **CDN (Opcional)**
```html
<!-- Usar CDN para recursos comunes -->
<link href="https://cdn.jsdelivr.net/npm/normalize.css@8.0.1/normalize.min.css" rel="stylesheet">
```

## 🔄 Actualizaciones y Mantenimiento

### **Backup Automático**
```bash
# Script de backup (backup.sh)
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
tar -czf /backups/vectoris_$DATE.tar.gz /home/usuario/public_html/
find /backups/ -name "vectoris_*.tar.gz" -mtime +7 -delete
```

### **Actualización de Contenido**
1. Modificar archivos HTML/CSS/JS
2. Subir cambios al servidor
3. Limpiar cache del navegador
4. Verificar funcionamiento

### **Monitoreo de Uso**
- Revisar LocalStorage periódicamente
- Limpiar datos antiguos si es necesario
- Monitorear rendimiento del sitio

## ✅ Checklist de Despliegue

### **Antes del Despliegue**
- [ ] Hosting contratado y configurado
- [ ] Dominio apuntando al servidor
- [ ] SSL Certificate configurado
- [ ] Archivos listos y probados localmente
- [ ] Backup del sitio anterior (si existe)

### **Durante el Despliegue**
- [ ] Subir todos los archivos al servidor
- [ ] Verificar permisos de archivos (644 para archivos, 755 para directorios)
- [ ] Configurar .htaccess o nginx.conf
- [ ] Probar todas las páginas principales
- [ ] Verificar que no haya errores en consola

### **Después del Despliegue**
- [ ] Configurar Google Analytics
- [ ] Enviar sitemap a Google Search Console
- [ ] Probar funcionalidad completa
- [ ] Verificar en diferentes navegadores
- [ ] Probar en dispositivos móviles
- [ ] Monitorear rendimiento los primeros días

## 🎞️ Soporte y Contacto

### **Soporte Técnico**
- **Documentación**: README.md completo
- **FAQ**: Sección de recursos
- **Email**: soporte@vectorisglobal.com
- **WhatsApp**: +58-412-123-4567

### **Comunidad**
- **GitHub Issues**: Reportar problemas
- **Foro**: Discusión con otros usuarios
- **Tutoriales**: Videos de configuración

---

## 🚀 ¡Listo para Producir!

Una vez completados estos pasos, tu sistema Vectoris Global estará completamente funcional y listo para recibir usuarios.

**Tiempo estimado de despliegue: 30-60 minutos**
**Nivel de dificultad: Fácil-Medio**
**Requisitos técnicos: Básicos**

¡Felicidades por tu nuevo sistema de casilleros! 🎉
