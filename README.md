# Aforo Backend API

**Status:** 🚧 En desarrollo  
**Versión:** 1.0.0 (Pendiente)

---

## 📋 Descripción

Backend API REST para la plataforma de gestión de eventos **Aforo**. Proporciona los servicios necesarios para soportar todas las funcionalidades del frontend público.

---

## 🎯 Estado del Proyecto

El **frontend público (MVP) está 100% completado** con datos mock. Este repositorio contendrá la implementación del backend real con las siguientes integraciones:

---

## 🔧 Integraciones Pendientes

### **1. Autenticación & Autorización**
- [ ] JWT tokens con refresh tokens
- [ ] OAuth 2.0 (Google, Facebook, LinkedIn)
- [ ] 2FA con TOTP
- [ ] Password reset flow
- [ ] Email verification

### **2. Payments & Billing**
- [ ] Stripe integration
- [ ] MercadoPago SDK
- [ ] Webhook handlers para confirmaciones
- [ ] Refund processing
- [ ] Invoice generation

### **3. Live Features**
- [ ] WebSocket server (Socket.io o similar)
- [ ] HLS streaming server o integración con servicios (Mux, Cloudflare Stream)
- [ ] Real-time sync para Q&A, polls, quiz, chat
- [ ] Message queue (Redis/RabbitMQ)

### **4. Cashless System**
- [ ] Digital wallet management
- [ ] QR code generation y validation
- [ ] Transaction processing
- [ ] Balance tracking
- [ ] Settlement con vendors

### **5. Ticketing**
- [ ] Ticket generation con QR dinámico
- [ ] Inventory management
- [ ] Pricing rules y promociones
- [ ] Check-in validation
- [ ] Access control

### **6. Certificados**
- [ ] PDF generation (puppeteer o similar)
- [ ] Email delivery (SendGrid, AWS SES)
- [ ] Verification API
- [ ] Certificate templates

### **7. Storage & Assets**
- [ ] S3/CloudFlare R2 para imágenes
- [ ] CDN configuration
- [ ] Image optimization
- [ ] File upload handling

### **8. Notificaciones**
- [ ] Email service
- [ ] Push notifications (FCM)
- [ ] SMS service (Twilio)
- [ ] In-app notifications

### **9. Analytics & Reporting**
- [ ] Event tracking
- [ ] Revenue reports
- [ ] Attendance analytics
- [ ] Dashboard metrics

---

## 🏗️ Stack Tecnológico Propuesto

### **Backend Framework:**
- **Python:** FastAPI (async, high-performance)
- **Node.js:** NestJS (TypeScript, enterprise-ready)
- **Go:** Gin/Fiber (ultra performance)

### **Database:**
- **PostgreSQL** - Relacional (eventos, users, tickets, orders)
- **Redis** - Cache y sessions
- **MongoDB** - NoSQL para logs y analytics (opcional)

### **Message Queue:**
- **Redis** o **RabbitMQ** - Para jobs async

### **Storage:**
- **AWS S3** o **CloudFlare R2** - Object storage
- **CloudFlare CDN** - Asset delivery

### **Real-time:**
- **Socket.io** - WebSocket management
- **Redis Pub/Sub** - Message broadcasting

### **Monitoring:**
- **Sentry** - Error tracking
- **DataDog** o **New Relic** - APM
- **Grafana + Prometheus** - Metrics

---

## 📊 Modelos de Datos (Pendientes)

### **Principales Entidades:**

```typescript
// Users
User {
  id, email, password_hash, name, phone,
  role, tenant_id, created_at, updated_at
}

// Events
Event {
  id, title, description, category,
  start_date, end_date, location,
  cover_image, organizer_id, status,
  settings (json)
}

// Tickets
Ticket {
  id, event_id, type_id, order_id,
  attendee_name, attendee_email,
  qr_code, status, check_in_date
}

// Orders
Order {
  id, event_id, user_id, total_amount,
  payment_method, payment_status,
  items (json), billing_info (json)
}

// Wallet
Wallet {
  id, user_id, balance, currency,
  status, created_at, updated_at
}

// Transactions
Transaction {
  id, wallet_id, type, amount,
  vendor_id, status, reference,
  timestamp
}

// Certificates
Certificate {
  id, user_id, event_id,
  certificate_number, verification_code,
  issue_date, pdf_url
}
```

---

## 🚀 Endpoints API (Propuestos)

### **Auth**
```
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/refresh
POST   /api/auth/logout
POST   /api/auth/forgot-password
POST   /api/auth/reset-password
```

### **Events**
```
GET    /api/events
GET    /api/events/:id
POST   /api/events
PUT    /api/events/:id
DELETE /api/events/:id
GET    /api/events/:id/tickets
```

### **Tickets**
```
GET    /api/tickets
GET    /api/tickets/:id
POST   /api/tickets/purchase
GET    /api/tickets/:id/qr
POST   /api/tickets/:id/check-in
```

### **Cashless**
```
GET    /api/wallet
POST   /api/wallet/recharge
POST   /api/wallet/pay
GET    /api/wallet/transactions
GET    /api/vendors
```

### **Live**
```
WS     /api/live/:eventId/stream
POST   /api/live/:eventId/questions
POST   /api/live/:eventId/polls/:pollId/vote
POST   /api/live/:eventId/quiz/answer
WS     /api/live/:eventId/chat
```

### **Certificates**
```
GET    /api/certificates
GET    /api/certificates/:id
GET    /api/certificates/:id/download
GET    /api/certificates/verify/:code
```

---

## 🔒 Seguridad

- [ ] Rate limiting
- [ ] CORS configuration
- [ ] JWT expiration y rotation
- [ ] SQL injection prevention
- [ ] XSS protection
- [ ] HTTPS only
- [ ] API key management
- [ ] Webhook signature verification

---

## 📝 Documentación Pendiente

- [ ] OpenAPI/Swagger spec
- [ ] API documentation
- [ ] Database schema diagram
- [ ] Architecture diagram
- [ ] Deployment guide
- [ ] Environment variables guide

---

## 🎯 Roadmap de Desarrollo

### **Sprint 1 (2 semanas):**
- [ ] Setup básico del proyecto
- [ ] Auth system (JWT + OAuth)
- [ ] User management
- [ ] Events CRUD
- [ ] Database setup

### **Sprint 2 (2 semanas):**
- [ ] Ticketing system
- [ ] Payment integration (Stripe)
- [ ] Order management
- [ ] Email notifications

### **Sprint 3 (2 semanas):**
- [ ] Cashless/Wallet system
- [ ] Transaction processing
- [ ] QR generation

### **Sprint 4 (2 semanas):**
- [ ] Live features (WebSocket)
- [ ] Real-time sync
- [ ] Certificate generation

---

## 🔗 Relacionado

- **Frontend Público:** https://github.com/carlosamesar/valor-plus-aforo-frontend
- **Documentación del MVP:** Ver `ENTREGA-FINAL-MVP-AFORO.md` en el repo de frontend

---

## 📞 Contacto

Para consultas sobre el desarrollo del backend, contactar al equipo de desarrollo.

---

**Última actualización:** 2026-10-27  
**Status:** 🚧 Pendiente de desarrollo  
**Frontend MVP:** ✅ 100% Completo
