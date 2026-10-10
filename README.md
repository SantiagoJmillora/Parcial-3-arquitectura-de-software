# Arquitectura del software de recaudo del sistema integrado de transporte

**Curso:** Arquitectura de Software, UPB · **Profesor:** César López · **Parcial 3**
**Tema 4:** Recaudo del sistema integrado de transporte de una ciudad mediana (alimentadores, articulados y metro; tarjeta VAMOS y débito/crédito).

**Integrantes:** _Nombre 1 · Nombre 2 · Nombre 3 · Nombre 4_

> Plan de trabajo: [BACKLOG.md](BACKLOG.md) · Guía del proyecto: [CLAUDE.md](CLAUDE.md) · Modelo fuente: [modelo/](modelo/)

---

## Índice
1. [Contexto y entrevista](#1-contexto-y-entrevista)
2. [Motivación](#2-motivación) · [V1](#v1-motivación)
3. [Mapa de capacidades y proceso E2E](#3-mapa-de-capacidades-y-proceso-e2e) · [V2](#v2-mapa-de-capacidades) · [V3](#v3-cadena-de-valor-y-proceso-e2e)
4. [Descomposición de servicios](#4-descomposición-de-servicios) · [V4](#v4-descomposición-de-servicios)
5. [Dominios y lenguaje ubicuo](#5-dominios-y-lenguaje-ubicuo) · [V5](#v5-dominios) · [V7](#v7-lenguaje-ubicuo)
6. [Agregados, comandos y eventos](#6-agregados-comandos-y-eventos) · [V6](#v6-agregados-comandos-y-eventos)
7. [Mapa de contextos e interoperabilidad](#7-mapa-de-contextos-e-interoperabilidad) · [V8](#v8-mapa-de-contextos) · [V9](#v9-interoperabilidad-y-anticorrupción)
8. [Bounded Context Canvas](#8-bounded-context-canvas) · [V11](#v11-bounded-context-canvas)
9. [Decisiones y supuestos](#9-decisiones-y-supuestos) · [V10](#v10-trazabilidad-vertical)
10. [Tabla de aportes](#10-tabla-de-aportes)

---

## 1. Contexto y entrevista
_Solicitud del usuario, alcance y lo que queda fuera. Resumen de la entrevista y enlaces a [entrevista/](entrevista/): instrucción de rol, guion, conversación y análisis de hallazgos._

## 2. Motivación
### V1 Motivación
![V1 Motivación](vistas/V1_motivacion.png)

**Análisis:** _…_
**Decisiones:** _…_

## 3. Mapa de capacidades y proceso E2E
### V2 Mapa de capacidades
![V2 Mapa de capacidades](vistas/V2_mapa_capacidades.png)

**Análisis:** _…_  **Capacidades impactadas:** _…_

### V3 Cadena de valor y proceso E2E
![V3 Cadena de valor y proceso E2E](vistas/V3_cadena_valor_e2e.png)

**Análisis:** _…_

## 4. Descomposición de servicios
### V4 Descomposición de servicios
![V4 Descomposición de servicios](vistas/V4_descomposicion_servicios.png)

**Análisis:** _…_

#### Tabla de inclusión y exclusión
| Capa | Servicio | ¿Se implementa? | Justificación |
|---|---|---|---|
| | | | |

#### Contratos de servicio (contract-first)
| Servicio | Entradas | Salidas | Errores | Requisitos no funcionales |
|---|---|---|---|---|
| | | | | |

#### Servicios externos (capa anticorrupción)
| Externo | Tipo | Información intercambiada | Dirección | Sincronía/frecuencia |
|---|---|---|---|---|
| | | | | |

## 5. Dominios y lenguaje ubicuo
### V5 Dominios
![V5 Dominios](vistas/V5_dominios.png)

| Dominio | Clasificación | Argumento |
|---|---|---|
| | | |

### V7 Lenguaje ubicuo
![V7 Lenguaje ubicuo](vistas/V7_lenguaje_ubicuo.png)

| Término | Definición | Dominio/contexto | Ejemplo |
|---|---|---|---|
| | | | |

## 6. Agregados, comandos y eventos
### V6 Agregados, comandos y eventos
_Un diagrama por dominio._

#### V6a _Dominio…_
![V6a](vistas/V6a_agregados_dominio.png)

| Agregado (raíz) | Entidades / objetos de valor | Invariantes | Comandos | Eventos |
|---|---|---|---|---|
| | | | | |

## 7. Mapa de contextos e interoperabilidad
### V8 Mapa de contextos
![V8 Mapa de contextos](vistas/V8_mapa_contextos.png)

| Contexto A | Contexto B | Patrón | Justificación |
|---|---|---|---|
| | | | |

### V9 Interoperabilidad y anticorrupción
![V9 Interoperabilidad y anticorrupción](vistas/V9_interoperabilidad_acl.png)

**Análisis:** _…_

## 8. Bounded Context Canvas
### V11 Bounded Context Canvas
![V11 Bounded Context Canvas](vistas/V11_bounded_context_canvas.png)

**Cómo lo resolvimos en ArchiMate (componente investigativo):** _…_

## 9. Decisiones y supuestos
### V10 Trazabilidad vertical
![V10 Trazabilidad vertical](vistas/V10_trazabilidad.png)

**Decisiones de diseño:** _…_
**Supuestos:** _…_

## 10. Tabla de aportes
| Integrante | Aportes (tareas del backlog) | Commits |
|---|---|---|
| | | |
