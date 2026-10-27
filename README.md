<div align="center">

# ⚙️ Aforo Backend API

**API REST para la plataforma de gestión de eventos Aforo**

[![Status](https://img.shields.io/badge/Status-In%20Development-yellow)](https://github.com/carlosamesar/valor-plus-aforo-backend)
[![Python](https://img.shields.io/badge/Python-3.11+-blue?logo=python)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688?logo=fastapi)](https://fastapi.tiangolo.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16+-336791?logo=postgresql)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)

[Frontend](https://github.com/carlosamesar/valor-plus-aforo-frontend) · [Documentación](#-documentación) · [Roadmap](#-roadmap)

</div>

---

## 📋 Tabla de Contenidos

- [Estado del Proyecto](#-estado-del-proyecto)
- [Descripción](#-descripción)
- [Stack Tecnológico](#-stack-tecnológico)
- [Arquitectura](#-arquitectura)
- [Integraciones](#-integraciones)
- [Endpoints API](#-endpoints-api)
- [Modelos de Datos](#-modelos-de-datos)
- [Instalación](#-instalación)
- [Roadmap](#-roadmap)
- [Seguridad](#-seguridad)
- [Licencia](#-licencia)

---

## 📊 Estado del Proyecto

> **🚧 EN DESARROLLO**  
> El **frontend público (MVP) está 100% completado** con datos mock.  
> Este repositorio contendrá la implementación del backend real.

**Progreso:**
- ✅ Arquitectura planificada
- ✅ Stack tecnológico definido
- ✅ Endpoints documentados
- ✅ Modelos de datos diseñados
- ⏳ Implementación en progreso
- ⏳ Integraciones pendientes

---

## 🎯 Descripción

**Aforo Backend** es la API REST que proporciona todos los servicios necesarios para soportar la plataforma de gestión de eventos:

- 🎫 **Ticketing:** Gestión de eventos, tickets y reservas
- 💳 **Payments:** Procesamiento de pagos (Stripe, MercadoPago)
- 📺 **Live Features:** WebSocket para Q&A, polls, quiz, chat en tiempo real
- 💰 **Cashless:** Sistema de billetera digital y transacciones
- 👥 **Networking:** Chat privado, meetings, business cards
- 📱 **Social:** Muro social con posts, likes, comentarios
- 🎓 **Certificates:** Generación de certificados PDF
- 🔐 **Auth:** Autenticación JWT + OAuth 2.0

---

## 🚀 Stack Tecnológico

### **Backend Framework**
- **[FastAPI](https://fastapi.tiangolo.com/)** - Async Python framework de alto rendimiento
- **[Python 3.11+](https://www.python.org/)** - Lenguaje principal
- **[Uvicorn](https://www.uvicorn.org/)** - ASGI server

### **Base de Datos**
- **[PostgreSQL 16+](https://www.postgresql.org/)** - Base de datos relacional (eventos, users, tickets, orders)
- **[SQLAlchemy 2.0](https://www.sqlalchemy.org/)** - ORM async
- **[Alembic](https://alembic.sqlalchemy.org/)** - Migraciones de BD

### **Cache & Sessions**
- **[Redis 7+](https://redis.io/)** - Cache, sessions, rate limiting
- **Redis Pub/Sub** - Message broadcasting para WebSocket

### **Message Queue**
- **[Redis Queue (RQ)](https://python-rq.org/)** o **[Celery](https://docs.celeryq.dev/)** - Jobs async
- **Background tasks:** Envío de emails, generación de PDFs, procesamiento de pagos

### **Storage & CDN**
- **[AWS S3](https://aws.amazon.com/s3/)** o **[CloudFlare R2](https://www.cloudflare.com/products/r2/)** - Object storage
- **CloudFlare CDN** - Asset delivery

### **Real-time**
- **[WebSocket](https://fastapi.tiangolo.com/advanced/websockets/)** - Comunicación bidireccional (FastAPI nativo)
- **Redis Pub/Sub** - Broadcasting entre workers

### **Payments**
- **[Stripe SDK](https://stripe.com/docs/api)** - Procesamiento de pagos internacionales
- **[MercadoPago SDK](https://www.mercadopago.com.co/developers/es/docs)** - Pagos LATAM

### **PDF Generation**
- **[WeasyPrint](https://weasyprint.org/)** o **[ReportLab](https://www.reportlab.com/)** - Generación de certificados

### **Email**
- **[SendGrid](https://sendgrid.com/)** o **[AWS SES](https://aws.amazon.com/ses/)** - Envío de emails transaccionales

### **Monitoring & Logging**
- **[Sentry](https://sentry.io/)** - Error tracking
- **[DataDog](https://www.datadoghq.com/)** o **[New Relic](https://newrelic.com/)** - APM
- **[Prometheus](https://prometheus.io/)** + **[Grafana](https://grafana.com/)** - Metrics

### **Testing**
- **[pytest](https://pytest.org/)** - Testing framework
- **[pytest-asyncio](https://pytest-asyncio.readthedocs.io/)** - Async tests
- **[httpx](https://www.python-httpx.org/)** - HTTP client para testing
- **[Faker](https://faker.readthedocs.io/)** - Mock data generation

---

## 🏗️ Arquitectura

### **Patrón: Clean Architecture**
```
app/
├── api/                    # API Layer (FastAPI routes)
│   ├── v1/
│   │   ├── auth.py        # Autenticación
│   │   ├── events.py      # Eventos
│   │   ├── tickets.py     # Tickets
│   │   ├── cashless.py    # Cashless
│   │   ├── live.py        # Live features
│   │   └── certificates.py
│   └── dependencies.py    # Dependencies injection
│
├── core/                  # Core Layer (config, security)
│   ├── config.py
│   ├── security.py        # JWT, OAuth, encryption
│   └── exceptions.py
│
├── domain/                # Domain Layer (business logic)
│   ├── events/
│   │   ├── models.py      # SQLAlchemy models
│   │   ├── schemas.py     # Pydantic schemas
│   │   ├── service.py     # Business logic
│   │   └── repository.py  # Data access
│   ├── tickets/
│   ├── cashless/
│   └── ...
│
├── infrastructure/        # Infrastructure Layer
│   ├── database.py        # DB connection
│   ├── redis.py           # Redis client
│   ├── s3.py              # S3 client
│   └── email.py           # Email service
│
└── main.py               # Application entry point
```

### **Principios:**
- ✅ **Clean Architecture** - Separación de capas
- ✅ **SOLID** - Principios de diseño
- ✅ **DDD** - Domain-Driven Design
- ✅ **Repository Pattern** - Abstracción de datos
- ✅ **Dependency Injection** - FastAPI dependencies
- ✅ **Async/Await** - Non-blocking I/O

---

## 🔧 Integraciones

### **1. Autenticación & Autorización**
- [ ] JWT tokens con refresh tokens
- [ ] OAuth 2.0 (Google, Facebook, LinkedIn)
- [ ] 2FA con TOTP (Time-based One-Time Password)
- [ ] Password reset flow (email con token temporal)
- [ ] Email verification (confirmación de cuenta)

### **2. Payments & Billing**
- [ ] **Stripe integration** - Pagos internacionales
  - Checkout sessions
  - Webhooks para confirmaciones
  - Refund processing
- [ ] **MercadoPago SDK** - Pagos LATAM
  - Pagos con tarjeta
  - PSE (Colombia)
  - Efectivo (Efecty, Baloto)
- [ ] Invoice generation (PDF + email)

### **3. Live Features**
- [ ] **WebSocket server** (FastAPI nativo)
- [ ] **HLS streaming** - Integración con Mux o Cloudflare Stream
- [ ] **Real-time sync** para Q&A, polls, quiz, chat
- [ ] **Redis Pub/Sub** - Broadcasting de mensajes

### **4. Cashless System**
- [ ] Digital wallet management
- [ ] QR code generation (QRCode library) y validation
- [ ] Transaction processing (atomic operations)
- [ ] Balance tracking en tiempo real
- [ ] Settlement con vendors (liquidaciones)

### **5. Ticketing**
- [ ] Ticket generation con QR dinámico
- [ ] Inventory management (control de cupos)
- [ ] Pricing rules y promociones (descuentos, cupones)
- [ ] Check-in validation (escaneo de QR)
- [ ] Access control (zonas restringidas)

### **6. Certificados**
- [ ] **PDF generation** (WeasyPrint o ReportLab)
- [ ] **Email delivery** (SendGrid, AWS SES)
- [ ] Verification API (código único)
- [ ] Certificate templates (plantillas HTML)

### **7. Storage & Assets**
- [ ] **S3/CloudFlare R2** para imágenes de eventos
- [ ] CDN configuration (CloudFlare)
- [ ] Image optimization (PIL/Pillow)
- [ ] File upload handling (multipart/form-data)

### **8. Notificaciones**
- [ ] **Email service** (transaccionales, confirmaciones)
- [ ] **Push notifications** (FCM - Firebase Cloud Messaging)
- [ ] **SMS service** (Twilio) - OTPs, confirmaciones
- [ ] In-app notifications (WebSocket)

### **9. Analytics & Reporting**
- [ ] Event tracking (GA4, Mixpanel)
- [ ] Revenue reports (dashboard)
- [ ] Attendance analytics (check-ins, asistencia)
- [ ] Dashboard metrics (KPIs en tiempo real)

---

## 📡 Endpoints API

### **Auth**
```http
POST   /api/v1/auth/register           # Registro de usuario
POST   /api/v1/auth/login              # Login (JWT)
POST   /api/v1/auth/refresh            # Refresh token
POST   /api/v1/auth/logout             # Logout
POST   /api/v1/auth/forgot-password    # Recuperar contraseña
POST   /api/v1/auth/reset-password     # Restablecer contraseña
GET    /api/v1/auth/verify-email       # Verificar email
```

### **Events**
```http
GET    /api/v1/events                  # Listar eventos
GET    /api/v1/events/:id              # Detalle de evento
POST   /api/v1/events                  # Crear evento (admin)
PUT    /api/v1/events/:id              # Actualizar evento (admin)
DELETE /api/v1/events/:id              # Eliminar evento (admin)
GET    /api/v1/events/:id/tickets      # Tipos de tickets disponibles
GET    /api/v1/events/search           # Búsqueda con filtros
```

### **Tickets**
```http
GET    /api/v1/tickets                 # Mis tickets
GET    /api/v1/tickets/:id             # Detalle de ticket
POST   /api/v1/tickets/purchase        # Comprar tickets
GET    /api/v1/tickets/:id/qr          # QR del ticket
POST   /api/v1/tickets/:id/check-in    # Check-in (admin/staff)
POST   /api/v1/tickets/:id/transfer    # Transferir ticket
```

### **Orders**
```http
GET    /api/v1/orders                  # Mis órdenes
GET    /api/v1/orders/:id              # Detalle de orden
POST   /api/v1/orders                  # Crear orden
POST   /api/v1/orders/:id/pay          # Procesar pago
POST   /api/v1/orders/:id/cancel       # Cancelar orden
```

### **Cashless**
```http
GET    /api/v1/wallet                  # Mi billetera
POST   /api/v1/wallet/recharge         # Recargar saldo
POST   /api/v1/wallet/pay              # Pagar a vendor
GET    /api/v1/wallet/transactions     # Historial de transacciones
GET    /api/v1/wallet/balance          # Saldo actual
POST   /api/v1/wallet/transfer         # Transferir a otro usuario
GET    /api/v1/vendors                 # Listar vendors
GET    /api/v1/vendors/:id             # Detalle de vendor
```

### **Live**
```http
WS     /api/v1/live/:eventId/stream    # WebSocket streaming
POST   /api/v1/live/:eventId/questions # Enviar pregunta (Q&A)
POST   /api/v1/live/:eventId/questions/:id/vote  # Votar pregunta
POST   /api/v1/live/:eventId/polls/:pollId/vote  # Votar en encuesta
GET    /api/v1/live/:eventId/polls/:pollId/results  # Resultados de encuesta
POST   /api/v1/live/:eventId/quiz/answer          # Responder quiz
GET    /api/v1/live/:eventId/quiz/leaderboard     # Leaderboard del quiz
WS     /api/v1/live/:eventId/chat      # WebSocket chat
```

### **Social**
```http
GET    /api/v1/social/:eventId/posts   # Posts del evento
POST   /api/v1/social/:eventId/posts   # Crear post
POST   /api/v1/social/posts/:id/like   # Like a post
POST   /api/v1/social/posts/:id/comment # Comentar post
GET    /api/v1/social/:eventId/trending # Hashtags trending
```

### **Networking**
```http
GET    /api/v1/networking/:eventId/attendees      # Asistentes
POST   /api/v1/networking/connections/request     # Solicitar conexión
POST   /api/v1/networking/connections/:id/accept  # Aceptar conexión
GET    /api/v1/networking/connections             # Mis conexiones
GET    /api/v1/networking/messages                # Mis conversaciones
POST   /api/v1/networking/messages                # Enviar mensaje
GET    /api/v1/networking/meetings                # Mis meetings
POST   /api/v1/networking/meetings                # Agendar meeting
GET    /api/v1/networking/business-card           # Mi business card
PUT    /api/v1/networking/business-card           # Actualizar business card
```

### **Certificates**
```http
GET    /api/v1/certificates                       # Mis certificados
GET    /api/v1/certificates/:id                   # Detalle de certificado
GET    /api/v1/certificates/:id/download          # Descargar PDF
GET    /api/v1/certificates/verify/:code          # Verificar certificado
POST   /api/v1/certificates/:id/share             # Compartir en LinkedIn
```

### **Admin**
```http
GET    /api/v1/admin/events                       # Dashboard de eventos
GET    /api/v1/admin/events/:id/stats             # Estadísticas del evento
GET    /api/v1/admin/events/:id/attendees         # Asistentes registrados
GET    /api/v1/admin/events/:id/revenue           # Revenue del evento
POST   /api/v1/admin/events/:id/send-email        # Enviar email masivo
```

---

## 💾 Modelos de Datos

### **Principales Entidades (PostgreSQL)**

```python
# Users
User:
  id: UUID (PK)
  email: str (unique, indexed)
  password_hash: str
  name: str
  phone: str
  role: Enum (user, admin, organizer, staff)
  tenant_id: UUID (multi-tenant)
  is_active: bool
  is_verified: bool
  created_at: datetime
  updated_at: datetime

# Events
Event:
  id: UUID (PK)
  title: str (indexed)
  slug: str (unique, indexed)
  description: text
  category: Enum (conference, concert, festival, workshop)
  start_date: datetime (indexed)
  end_date: datetime
  location: str
  venue: str
  cover_image_url: str
  organizer_id: UUID (FK -> User)
  status: Enum (draft, published, ongoing, finished, cancelled)
  settings: JSONB (capacidad, timezone, etc.)
  created_at: datetime
  updated_at: datetime

# Ticket Types
TicketType:
  id: UUID (PK)
  event_id: UUID (FK -> Event)
  name: str (ej: "General", "VIP")
  description: text
  price: Decimal
  quantity_available: int
  quantity_sold: int
  sales_start: datetime
  sales_end: datetime
  is_active: bool

# Tickets
Ticket:
  id: UUID (PK)
  event_id: UUID (FK -> Event)
  ticket_type_id: UUID (FK -> TicketType)
  order_id: UUID (FK -> Order)
  attendee_name: str
  attendee_email: str
  qr_code: str (unique, encrypted)
  status: Enum (active, used, cancelled, transferred)
  check_in_date: datetime (nullable)
  created_at: datetime

# Orders
Order:
  id: UUID (PK)
  event_id: UUID (FK -> Event)
  user_id: UUID (FK -> User)
  total_amount: Decimal
  payment_method: Enum (card, transfer, cash, wallet)
  payment_status: Enum (pending, completed, failed, refunded)
  payment_id: str (Stripe/MercadoPago ID)
  items: JSONB (lista de tickets)
  billing_info: JSONB (nombre, email, documento)
  created_at: datetime
  updated_at: datetime

# Wallet
Wallet:
  id: UUID (PK)
  user_id: UUID (FK -> User, unique)
  balance: Decimal (default 0)
  currency: str (default "COP")
  status: Enum (active, suspended, frozen)
  created_at: datetime
  updated_at: datetime

# Transactions
Transaction:
  id: UUID (PK)
  wallet_id: UUID (FK -> Wallet)
  type: Enum (recharge, payment, refund, transfer)
  amount: Decimal
  vendor_id: UUID (FK -> Vendor, nullable)
  description: str
  status: Enum (pending, completed, failed)
  reference: str (external reference)
  metadata: JSONB
  created_at: datetime

# Certificates
Certificate:
  id: UUID (PK)
  user_id: UUID (FK -> User)
  event_id: UUID (FK -> Event)
  certificate_number: str (unique, indexed)
  verification_code: str (unique, indexed)
  hours_attended: int
  activities: JSONB (lista de actividades completadas)
  issue_date: datetime
  pdf_url: str
  status: Enum (available, downloaded, shared, verified)
  created_at: datetime
```

---

## 📦 Instalación

> **⚠️ Nota:** El backend está en desarrollo. Los siguientes pasos son provisionales.

### **Prerrequisitos**
- Python 3.11+ ([Download](https://www.python.org/))
- PostgreSQL 16+ ([Download](https://www.postgresql.org/))
- Redis 7+ ([Download](https://redis.io/))
- Git ([Download](https://git-scm.com/))

### **Clonar el repositorio**
```bash
git clone https://github.com/carlosamesar/valor-plus-aforo-backend.git
cd valor-plus-aforo-backend
```

### **Crear entorno virtual**
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# o
venv\Scripts\activate     # Windows
```

### **Instalar dependencias**
```bash
pip install -r requirements.txt
```

### **Configurar variables de entorno**
```bash
cp .env.example .env
```

Editar `.env`:
```env
DATABASE_URL=postgresql+asyncpg://user:password@localhost:5432/aforo
REDIS_URL=redis://localhost:6379/0
SECRET_KEY=your-secret-key-here
STRIPE_SECRET_KEY=sk_test_...
MERCADOPAGO_ACCESS_TOKEN=APP_USR-...
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
SENDGRID_API_KEY=...
```

### **Crear base de datos**
```bash
createdb aforo
```

### **Ejecutar migraciones**
```bash
alembic upgrade head
```

### **Ejecutar servidor de desarrollo**
```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

API disponible en: [http://localhost:8000](http://localhost:8000)  
Docs interactiva: [http://localhost:8000/docs](http://localhost:8000/docs)

---

## 🗺️ Roadmap

### **Sprint 1 (2 semanas) - Core Infrastructure**
- [ ] Setup básico del proyecto (FastAPI + PostgreSQL + Redis)
- [ ] Auth system (JWT + OAuth 2.0)
- [ ] User management (CRUD, roles, permisos)
- [ ] Events CRUD (crear, listar, actualizar, eliminar)
- [ ] Database setup + Alembic migrations
- [ ] Testing setup (pytest + fixtures)
- [ ] CI/CD pipeline (GitHub Actions)

### **Sprint 2 (2 semanas) - Ticketing & Payments**
- [ ] Ticketing system (tipos de tickets, inventory)
- [ ] Payment integration (Stripe)
- [ ] Order management (crear, procesar, cancelar)
- [ ] Email notifications (confirmación de compra)
- [ ] Webhook handlers (Stripe)
- [ ] QR code generation (tickets)

### **Sprint 3 (2 semanas) - Cashless & Networking**
- [ ] Cashless/Wallet system (balance, recargas)
- [ ] Transaction processing (atomic operations)
- [ ] Networking API (conexiones, chat, meetings)
- [ ] Business cards (CRUD)
- [ ] Redis Pub/Sub setup

### **Sprint 4 (2 semanas) - Live Features & Certificates**
- [ ] WebSocket server (Q&A, polls, quiz, chat)
- [ ] Real-time sync (Redis broadcasting)
- [ ] Social wall API (posts, likes, comentarios)
- [ ] Certificate generation (PDF)
- [ ] Certificate verification API

### **Sprint 5 (2 semanas) - Admin & Analytics**
- [ ] Admin dashboard endpoints
- [ ] Analytics y reportes
- [ ] MercadoPago integration
- [ ] Push notifications (FCM)
- [ ] Load testing (Locust)

### **Sprint 6 (1 semana) - Deploy & Monitoring**
- [ ] Production deployment (AWS/GCP/Heroku)
- [ ] Monitoring setup (Sentry, DataDog)
- [ ] Performance optimization
- [ ] Security audit
- [ ] Documentation final

---

## 🔒 Seguridad

### **Medidas de Seguridad Implementadas**
- [ ] **Rate limiting** (FastAPI Limiter + Redis)
- [ ] **CORS configuration** (orígenes permitidos)
- [ ] **JWT expiration** (access token 15min, refresh token 7 días)
- [ ] **Password hashing** (bcrypt con salt)
- [ ] **SQL injection prevention** (SQLAlchemy ORM)
- [ ] **XSS protection** (sanitización de inputs)
- [ ] **HTTPS only** (redirect HTTP → HTTPS)
- [ ] **API key management** (rotación automática)
- [ ] **Webhook signature verification** (Stripe, MercadoPago)
- [ ] **Input validation** (Pydantic schemas)
- [ ] **Secrets management** (AWS Secrets Manager)

### **Compliance**
- [ ] GDPR compliance (protección de datos)
- [ ] PCI-DSS (pagos con tarjeta - delegado a Stripe/MercadoPago)
- [ ] OWASP Top 10 (mitigación de vulnerabilidades)

---

## 📚 Documentación

- **[OpenAPI/Swagger](http://localhost:8000/docs)** - Documentación interactiva
- **[ReDoc](http://localhost:8000/redoc)** - Documentación alternativa
- **[Architecture Guide](docs/ARCHITECTURE.md)** - Guía de arquitectura
- **[Database Schema](docs/DATABASE.md)** - Esquema de base de datos
- **[API Reference](docs/API.md)** - Referencia completa de API
- **[Deployment Guide](docs/DEPLOYMENT.md)** - Guía de deployment

---

## 🧪 Testing

```bash
# Ejecutar todos los tests
pytest

# Ejecutar con coverage
pytest --cov=app --cov-report=html

# Ejecutar tests específicos
pytest tests/api/test_events.py

# Ejecutar tests E2E
pytest tests/e2e/
```

**Test Coverage Target:** ≥85%

---

## 🔗 Relacionado

- **[Frontend Público](https://github.com/carlosamesar/valor-plus-aforo-frontend)** - MVP 100% completo
- **[Admin Dashboard](https://github.com/carlosamesar/valor-plus-aforo-admin)** - Panel de administración (Angular)

---

## 🤝 Contributing

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea tu feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la branch (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

Ver [CONTRIBUTING.md](CONTRIBUTING.md) para más detalles.

---

## 📄 Licencia

**Proprietary License** - © 2026 Valor Plus. Todos los derechos reservados.

Este código es propiedad de Valor Plus y no puede ser usado, copiado, modificado o distribuido sin autorización explícita.

---

## 📞 Contacto

**Equipo de Desarrollo Valor Plus**

- 🌐 Website: [valorplus.com](https://valorplus.com)
- 📧 Email: dev@valorplus.com
- 💼 LinkedIn: [Valor Plus](https://linkedin.com/company/valor-plus)

---

## 🙏 Agradecimientos

- **[FastAPI](https://fastapi.tiangolo.com/)** - Amazing Python framework
- **[SQLAlchemy](https://www.sqlalchemy.org/)** - ORM poderoso
- **[Stripe](https://stripe.com/)** - Payment processing
- **[MercadoPago](https://www.mercadopago.com.co/)** - Pagos LATAM

---

<div align="center">

**Hecho con ❤️ por el equipo de Valor Plus**

[⬆ Volver arriba](#️-aforo-backend-api)

</div>
