# Arquitectura de Solución — Banca por Internet BP

Prueba técnica de Arquitectura de Soluciones. Diseño de una plataforma de banca
por internet para la entidad BP: histórico de cuentas, transferencias y pagos
propios e interbancarios, vinculación digital con reconocimiento facial,
notificación obligatoria de movimientos y auditoría de todas las acciones.

**Entregable:** [Arquitectura_Banca_Digital_BP.pdf](Arquitectura_Banca_Digital_BP.pdf)

## Contenido

El documento se organiza en dos partes:

- **Parte I — El problema.** Enunciado, 16 requisitos numerados, restricciones y supuestos.
- **Parte II — La solución.** Las cuatro vistas del modelo C4, el registro de decisiones
  con doble justificación, y las vistas de despliegue, seguridad, continuidad,
  observabilidad, normativa y costos.

## Modelo C4

| Nivel | Qué muestra | Diagramas |
|---|---|---|
| 1. Contexto | Actores, sistemas internos y terceros | 1 |
| 2. Contenedores | Unidades desplegables, datos y mensajería sobre AWS | 1 |
| 3. Componentes | Piezas internas de cada contenedor construido | 13 |
| 4. Código | Clases de los dos componentes críticos | 2 |

Más tres diagramas de secuencia, despliegue, seguridad y observabilidad: **23 figuras**.

## Decisiones principales

| # | Decisión | Alternativas evaluadas |
|---|---|---|
| AD-01 | Nube: AWS | Azure, Google Cloud, nube privada |
| AD-02 | Móvil: Flutter | React Native, .NET MAUI, nativo |
| AD-03 | Web: Angular | React, Vue, Next.js |
| AD-04 | OAuth 2.0: Authorization Code + PKCE | Implicit, ROPC, Client Credentials, Device Code |
| AD-05 | API Gateway + un BFF por canal | Gateway único, BFF compartido, GraphQL |
| AD-12 | Transferencias: saga con compensación, outbox e idempotencia | Two-phase commit |
| AD-10 | Auditoría: solo anexo, hash encadenado y Object Lock | Tabla con disparadores, log centralizado |
| AD-11 | Clientes frecuentes: cache-aside con invalidación por evento | Read-through, TTL, sesión pegajosa |

El documento recoge **23 decisiones con registro formal**, cada una con sus opciones
evaluadas y **tres justificaciones teóricas**. Sumando las elecciones de tecnología
(31 servicios de AWS con dos razones y su alternativa), los frameworks de canal, los
patrones y los protocolos por tramo, son **93 decisiones justificadas**, ninguna con
menos de dos razones. La sección 22.1 del documento trae el inventario completo.

## Patrones aplicados

**Arquitectura:** API Gateway, Backend for Frontend, capa anticorrupción, arquitectura
orientada a eventos, saga con compensación, outbox transaccional, idempotencia, CQRS,
cache-aside, base de datos por servicio, corte de circuito y mamparo, despliegue canario.

**Diseño** (mecanismo para clientes frecuentes): fachada, cache-aside, observador,
vista materializada, estrategia, decorador, repositorio y constructor.

## Diagramas

Todas las figuras están en [`diagramas/`](diagramas/) en PNG.

| Archivo | Figura |
|---|---|
| `n1_contexto.png` | Nivel 1 — Contexto |
| `n2_contenedores.png` | Nivel 2 — Contenedores |
| `n3_*.png` | Nivel 3 — Componentes (13) |
| `n4_*.png` | Nivel 4 — Código (2) |
| `seq_*.png` | Secuencias: OAuth 2.0, onboarding, transferencia |
| `despliegue_aws.png` | Despliegue, alta disponibilidad y recuperación |
| `seguridad_zonas.png` | Zonas de confianza y controles |
| `monitoreo.png` | Observabilidad y auto-reparación |

## Autor

David Palma — Arquitecto de Soluciones
