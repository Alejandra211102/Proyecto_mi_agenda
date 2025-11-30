# 📅 Agenda Personal - Sistema Completo

Sistema de gestión de agenda personal con arquitectura de microservicios, dockerizado y desplegable en AWS.

## 📋 Descripción

Aplicación web completa para gestionar eventos personales con:
- Calendario interactivo visual
- Categorización por prioridades (Urgente, Importante, Normal, Leve)
- Notificaciones automáticas
- Integración con ESP32 para visualización en displays físicos
- API RESTful completa

## 🏗️ Arquitectura del Sistema

```
┌─────────────────────────────────────────┐
│  FRONTEND (React + Vite + Tailwind)     │
│  EC2 Instance - Puerto 80               │
│  Calendario interactivo y gestión UI    │
└─────────────────────────────────────────┘
                    ↓ HTTP
┌─────────────────────────────────────────┐
│  BACKEND (Node.js + Express)            │
│  EC2 Instance - Puerto 3000             │
│  API REST + Cron Jobs                   │
└─────────────────────────────────────────┘
                    ↓ MySQL Protocol
┌─────────────────────────────────────────┐
│  BASE DE DATOS (MySQL 8.0)              │
│  AWS RDS                                │
│  Almacenamiento persistente             │
└─────────────────────────────────────────┘
```

## 🚀 Stack Tecnológico

### Frontend
- **React 18** - Librería de UI
- **Vite** - Build tool y dev server
- **Tailwind CSS** - Framework de estilos
- **Lucide React** - Iconos
- **Nginx** - Servidor web de producción
- **Docker** - Containerización

### Backend
- **Node.js 18** - Runtime de JavaScript
- **Express** - Framework web
- **MySQL2** - Cliente de base de datos
- **node-cron** - Jobs programados
- **CORS** - Control de acceso
- **Docker** - Containerización

### Base de Datos
- **MySQL 8.0** - Sistema de gestión de base de datos
- **AWS RDS** - Servicio administrado

### Infraestructura
- **AWS EC2** - Servidores virtuales (2 instancias)
- **AWS RDS** - Base de datos administrada
- **Docker** - Containerización
- **Git/GitHub** - Control de versiones

## 📁 Estructura del Proyecto

```
agenda-personal/
├── agenda-frontend/          # Aplicación React
│   ├── src/
│   │   ├── App.jsx          # Componente principal
│   │   ├── main.jsx         # Punto de entrada
│   │   └── index.css        # Estilos globales
│   ├── Dockerfile           # Imagen Docker multi-stage
│   ├── nginx.conf           # Configuración de Nginx
│   ├── package.json         # Dependencias
│   └── README.md            # Documentación del frontend
│
├── agenda-backend/           # API REST
│   ├── server.js            # Servidor Express
│   ├── Dockerfile           # Imagen Docker
│   ├── package.json         # Dependencias
│   └── README.md            # Documentación del backend
│
├── database/                 # Scripts de base de datos
│   ├── init.sql             # Script inicial
│   ├── schema.sql           # Esquema de tablas
│   └── README.md            # Documentación de la BD
│
├── docker-compose.full.yml   # Orquestación local
├── .gitignore               # Archivos ignorados por Git
└── README.md                # Este archivo
```

## ⚙️ Características Principales

### 🎨 Frontend
- ✅ Calendario mensual interactivo
- ✅ Vista de eventos por día
- ✅ Creación y edición de eventos con modal
- ✅ Código de colores por prioridad
- ✅ Estadísticas en tiempo real
- ✅ Responsive design (móvil, tablet, desktop)
- ✅ Actualización automática cada 30 segundos

### 🔧 Backend
- ✅ API RESTful completa (CRUD)
- ✅ Endpoints optimizados para ESP32
- ✅ Sistema de notificaciones con cron jobs
- ✅ Validación de datos
- ✅ Manejo de errores robusto
- ✅ Logs detallados
- ✅ Reconexión automática a base de datos

### 🗄️ Base de Datos
- ✅ Esquema optimizado con índices
- ✅ Soporte completo UTF-8 (emojis y caracteres especiales)
- ✅ Timestamps automáticos
- ✅ Relaciones bien definidas
- ✅ Backups automáticos (AWS RDS)

## 🚀 Despliegue Rápido

### Desarrollo Local

```bash
# Clonar repositorio
git clone https://github.com/TU_USUARIO/agenda-personal.git
cd agenda-personal

# Levantar todo con Docker Compose
docker-compose -f docker-compose.full.yml up -d

# Acceder
# Frontend: http://localhost
# Backend: http://localhost:3000
# MySQL: localhost:3306
```

### Producción en AWS

Ver documentación detallada en cada README:
- [Base de Datos en RDS](./database/README.md)
- [Backend en EC2](./agenda-backend/README.md)
- [Frontend en EC2](./agenda-frontend/README.md)

## 📡 API Endpoints

### Eventos

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/api/eventos` | Obtener todos los eventos |
| GET | `/api/eventos/:id` | Obtener un evento específico |
| GET | `/api/eventos/dia/hoy` | Eventos del día actual |
| GET | `/api/eventos/pendientes` | Eventos no completados |
| GET | `/api/eventos/esp32` | Formato optimizado para ESP32 |
| POST | `/api/eventos` | Crear nuevo evento |
| PUT | `/api/eventos/:id` | Actualizar evento |
| POST | `/api/eventos/:id/completar` | Marcar como completado |
| DELETE | `/api/eventos/:id` | Eliminar evento |

### Ejemplo de Petición

```bash
# Crear evento
curl -X POST http://[BACKEND_IP]:3000/api/eventos \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Reunión importante",
    "descripcion": "Presentación de proyecto",
    "fecha_hora": "2025-11-23 14:00:00",
    "prioridad": "urgente"
  }'
```

## 🔐 Variables de Entorno

### Backend

```env
NODE_ENV=production
PORT=3000
DB_HOST=tu-rds-endpoint.amazonaws.com
DB_USER=admin
DB_PASSWORD=tu_password_seguro
DB_NAME=agenda_db
DB_PORT=3306
FRONTEND_URL=http://tu-frontend-ip
```

### Frontend

```env
VITE_API_URL=http://tu-backend-ip:3000/api
```

## 🛠️ Requisitos del Sistema

### Desarrollo Local
- Node.js 18 o superior
- Docker Desktop
- Git
- 8GB RAM mínimo
- 10GB espacio en disco

### Producción AWS
- Cuenta de AWS activa
- AWS CLI configurado (opcional)
- 2 instancias EC2 t2.micro (Free Tier)
- 1 instancia RDS db.t3.micro (Free Tier)
- Conocimientos básicos de SSH

## 📊 Costos Estimados AWS

### Free Tier (12 meses)
- **EC2:** 2 instancias t2.micro (750 horas/mes cada una) - **GRATIS**
- **RDS:** db.t3.micro (750 horas/mes) - **GRATIS**
- **Almacenamiento:** 30GB SSD - **GRATIS**
- **Transferencia:** 15GB salida - **GRATIS**

### Post Free Tier (Estimado mensual)
- **EC2:** ~$18/mes (2 instancias)
- **RDS:** ~$15/mes
- **Almacenamiento:** ~$3/mes
- **Total:** ~$36/mes

## 🧪 Testing

```bash
# Backend - Tests unitarios
cd agenda-backend
npm test

# Frontend - Build de producción
cd agenda-frontend
npm run build

# Docker - Verificar imágenes
docker images

# Docker - Ver logs
docker logs agenda-backend
docker logs agenda-frontend
```

## 🔄 Actualización del Sistema

### Actualizar Frontend

```bash
# En tu computadora local
cd agenda-frontend
git pull
docker build -t TU_USUARIO/agenda-frontend:latest .
docker push TU_USUARIO/agenda-frontend:latest

# En EC2 Frontend
docker pull TU_USUARIO/agenda-frontend:latest
docker stop agenda-frontend
docker rm agenda-frontend
docker run -d --name agenda-frontend --restart always -p 80:80 TU_USUARIO/agenda-frontend:latest
```

### Actualizar Backend

```bash
# Similar al frontend
cd agenda-backend
git pull
# Reconstruir y redesplegar
```

## 📈 Monitoreo

### Logs en Tiempo Real

```bash
# Backend
docker logs -f agenda-backend

# Frontend
docker logs -f agenda-frontend

# Ver recursos
docker stats
```

### Métricas AWS

- CloudWatch para monitoreo de EC2 y RDS
- Alertas de CPU, memoria y disco
- Logs de aplicación centralizados

## 🐛 Troubleshooting

### Frontend no se conecta al Backend

```bash
# Verificar que el backend esté corriendo
curl http://BACKEND_IP:3000/api/eventos

# Verificar variables de entorno
docker exec agenda-frontend cat /etc/nginx/conf.d/default.conf

# Revisar logs
docker logs agenda-frontend
```

### Backend no conecta a RDS

```bash
# Verificar conectividad
telnet RDS_ENDPOINT 3306

# Verificar security groups en AWS
# Asegurar que el RDS permite conexiones desde el EC2 del backend

# Revisar logs
docker logs agenda-backend
```

### Problemas de caracteres especiales

```bash
# Verificar charset en MySQL
docker exec -it agenda-backend mysql -h RDS_ENDPOINT -u admin -p
> SHOW VARIABLES LIKE 'character%';

# Debe mostrar utf8mb4
```

## 🤝 Contribuir

1. Fork el proyecto
2. Crea tu rama de features (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add: nueva característica'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📝 Roadmap

- [ ] Autenticación de usuarios con JWT
- [ ] Notificaciones push en el navegador
- [ ] Sincronización con Google Calendar
- [ ] App móvil nativa (React Native)
- [ ] Recordatorios por email
- [ ] Temas personalizables (dark mode)
- [ ] Exportar eventos a PDF/ICS
- [ ] Compartir eventos entre usuarios
- [ ] Integración con Alexa/Google Assistant



---

**⭐ Si este proyecto te fue útil, dale una estrella en GitHub!**
