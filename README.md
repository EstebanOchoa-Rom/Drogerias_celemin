# 💊 Droguerías Celemin  
## Plataforma Web Profesional para Gestión y Venta de Productos Farmacéuticos

---

# 1. Introducción

Droguerías Celemin es una plataforma web desarrollada para digitalizar y optimizar la operación integral de una droguería, permitiendo la venta en línea de productos farmacéuticos y la gestión administrativa mediante una arquitectura moderna basada en microservicios.

El sistema busca reemplazar procesos manuales y desorganizados por una solución tecnológica segura, escalable y preparada para crecimiento empresarial.

---

# 2. Objetivo General

Diseñar e implementar un sistema web que permita:

- Comercializar productos farmacéuticos en línea.
- Gestionar inventario por lotes con control de fechas de vencimiento.
- Reducir pérdidas por productos vencidos.
- Administrar pedidos y pagos.
- Controlar accesos mediante roles y permisos.
- Mantener trazabilidad de acciones administrativas.
- Escalar a múltiples sedes si el negocio lo requiere.

---

# 3. Alcance del Proyecto (MVP)

El sistema actualmente permite:

- Catálogo público de productos.
- Carrito de compras persistente.
- Checkout con generación de pedidos.
- Control FEFO (First Expire, First Out) en inventario.
- Gestión de productos y categorías.
- Registro de lotes con fecha de vencimiento.
- Dashboard de productos vencidos y próximos a vencer.
- Confirmación manual de pagos.
- Control de acceso basado en roles (RBAC).
- Auditoría de acciones administrativas críticas.

No incluye en esta fase:

- Integración automática con API oficial de Nequi.
- Infraestructura autoescalable en Kubernetes.
- CDN externo para imágenes.
- Notificaciones automáticas por WhatsApp o email.

---

# 4. Arquitectura del Sistema

El sistema implementa una arquitectura basada en microservicios desacoplados.

## Flujo General

Frontend (Next.js)  
↓  
Gateway API (FastAPI)  
↓  
Microservicios independientes  

## Microservicios

- auth-service → Autenticación y RBAC
- catalog-service → Productos, categorías e imágenes
- inventory-service → Lotes y control de vencimientos
- orders-service → Gestión de pedidos
- payments-service → Registro y confirmación de pagos
- stores-service (opcional) → Gestión multi-sede

Cada microservicio posee:

- Base de datos independiente (PostgreSQL).
- Migraciones propias (Alembic).
- Logging estructurado.
- Manejo estandarizado de errores.
- Documentación OpenAPI (Swagger).
- Healthchecks y readiness endpoints.

---

# 5. Estructura del Repositorio
/apps
/frontend
/services
/gateway-api
/auth-service
/catalog-service
/inventory-service
/orders-service
/payments-service
/stores-service
/infra
/docker
/observability
/docs


---

# 6. Tecnologías Utilizadas

## Backend

- Python 3.13
- FastAPI
- SQLAlchemy 2.x
- PostgreSQL
- Alembic
- Docker
- GitHub Actions (CI)

## Frontend

- Next.js (App Router)
- TypeScript
- React
- Arquitectura por features

## Observabilidad

- Prometheus
- Grafana

---

# 7. Modelo Funcional del Sistema

## 7.1 Flujo de Compra

1. Usuario navega el catálogo.
2. Agrega productos al carrito.
3. Completa el checkout.
4. Se genera un pedido.
5. inventory-service descuenta stock por FEFO.
6. payments-service registra el pago.
7. Admin confirma pago si aplica.

---

## 7.2 Flujo de Inventario

1. Admin registra un lote con fecha de vencimiento.
2. El sistema clasifica automáticamente:
   - Vencido
   - Crítico
   - Próximo
   - Normal
3. Dashboard muestra productos ordenados por fecha de vencimiento.
4. Las ventas descuentan primero el lote más próximo a vencer.

---

## 7.3 Flujo Administrativo

1. Usuario administrativo inicia sesión.
2. Se validan roles y permisos.
3. Accede solo a módulos autorizados.
4. Toda acción crítica genera un registro en audit_logs.

---

# 8. Seguridad Implementada

- Autenticación JWT con expiración configurable.
- RBAC basado en permisos granulares.
- Auditoría de acciones administrativas.
- Validación estricta de inputs.
- Manejo seguro de archivos.
- Separación de bases de datos por microservicio.
- No exposición de datos sensibles en logs.

---

# 9. Requisitos del Sistema

## Requisitos de Software

- Docker 24+
- Docker Compose
- Node.js 18+
- pnpm
- Python 3.13

## Requisitos de Hardware (Mínimo Recomendado)

- 8 GB RAM
- 4 CPU
- 20 GB espacio en disco

---

# 10. Instalación y Ejecución

## 1. Clonar el repositorio

```bash
git clone <repository-url>
cd droguerias-celemin
```
2. Configurar variables de entorno

Copiar los archivos .env.example en cada servicio y configurar valores locales.

3. Levantar backend
docker compose up -d
4. Levantar frontend
cd apps/frontend
pnpm install
pnpm dev
11. Estado Actual del Proyecto

Arquitectura completamente definida.

Microservicios desacoplados.

MVP funcional.

Sistema preparado para escalar.

Observabilidad integrada.

SEO técnico implementado en frontend.

12. Principios de Ingeniería Aplicados

Principios SOLID.

Clean Architecture.

Separación de responsabilidades.

Diseño desacoplado.

Preparación para despliegue en nube.

Buenas prácticas DevOps.

13. Roadmap Estratégico

Consolidación del MVP.

Integración de pagos automáticos.

Escalabilidad multi-sede completa.

Optimización avanzada de rendimiento.

Preparación para despliegue enterprise.

14. Conclusión

Droguerías Celemin es una solución tecnológica diseñada para modernizar la operación de una droguería mediante una arquitectura robusta, segura y escalable.

El sistema está preparado para operar como plataforma real de ventas y gestión administrativa, con bases técnicas sólidas que permiten su evolución futura.

15. Autor

Proyecto desarrollado como solución profesional para la digitalización de una droguería real.
