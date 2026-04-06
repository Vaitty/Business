# Vaitty — Agente Business Developer

## Identidad de la empresa
- **Razón social**: FAST HOME SERVICES S.A.S (marca comercial: **Vaitty**)
- **CEO**: Nadir Donemberg (DNI 33.699.113)
- **Business Manager**: Lara Tzvir
- **Misión**: Simplificar la vida de las personas a través de servicios coordinados tecnológicamente.

---

## Verticales y categorías de servicios

### Hogar
- **Emergencias**: Plomería, Electricidad, Cerrajería, Gas, Vidrios, Aire Acondicionado
- **Programados/Preventivos**: Mantenimientos y reparaciones, Instalaciones

### Movilidad
- Movilidad sustentable, Vial

### Mascotas
- Veterinaria, servicios de bienestar animal

### Personas
- Salud, servicios de bienestar personal

Cada servicio tiene:
- **Tipo**: Emergencia o Programado
- **Descripción**: qué resuelve
- **Incluye**: alcance específico
- **No incluye**: exclusiones explícitas
- **Bien/Artefacto**: objeto sobre el que aplica

Ver catálogo completo en `docs/Listado de servicios.xlsx`

---

## Modelo de negocio

### Tipos de cliente (partners)
- Aseguradoras, bancos, financieras

### Tipos de paquetes
| Tipo | Descripción | Público objetivo |
|------|-------------|-----------------|
| **Bundle** | Embebido en una cartera ya consolidada | Carteras ballena/mayoristas, añaden valor a productos intangibles |
| **Stand-alone** | Se comercializa individualmente | Upsale en productos en mostrador |

### Modelos de cobertura
- **Wallet**: saldo anual con tope por evento (ej: $540.000 anuales / $45.000 por evento)
- **Por uso con límites**: cantidad de usos por categoría (ej: 1 mantenimiento/mes, 3 emergencias/año)
- **Combinado**: mezcla de ambos modelos

### Coberturas configurables
- Monto de wallet anual
- Tope por evento
- Límite de usos por mes/año por categoría
- Qué categorías están incluidas (Hogar, Movilidad, Mascotas, Personas)
- Servicios específicos dentro de cada categoría
- Modalidad de reintegro vs. prestación directa

---

## Lógica del cotizador

**Archivo**: `docs/Cotizador.xlsx`

### Variables de entrada (Hoja: Inputs)
| Variable | Descripción |
|----------|-------------|
| Capitas | Número de beneficiarios |
| Tasa de uso base | % mensual de uso esperado del servicio |
| Cobertura media | Ticket/cobertura promedio por evento ($) |
| Markup comercial | Multiplicador sobre costo cápita (default: 5x) |
| Impuestos directos | % sobre precio (default: 9%) |
| Comisión comercial canal | Revenue share del canal (default: 55%) |
| Costo IT por servicio | Costo tecnológico variable por uso ($) |
| Costo unitario operación | Costo mensual por FTE operativo ($) |
| Productividad operación | Servicios por FTE por mes |

### Lógica de cálculo (simplificada)
1. **Servicios por mes** = Capitas × Tasa de uso base
2. **Costo directo** = Servicios × Cobertura media
3. **Subtotal costo cápita** = (Costo directo + Costo operación + Costo IT + Costo admin) / Capitas
4. **Precio per cápita** = (Subtotal costo × Markup + Impuestos) → ajustado por curva de uso
5. **Rentabilidad neta** = (Facturación - Comisión canal - Costos) / Facturación

### Ajuste por curva de uso
El precio sube proporcionalmente si la tasa de uso real supera la base. Ver hoja `Curva_Uso`.

### Salida comercial
- Producto | Modo (Bundle/Stand-alone) | Capitas | Cobertura media | Tasa de uso | **Precio per cápita sugerido**

---

## Jerarquía de producto

Todo producto Vaitty se construye sobre cinco niveles jerárquicos. Cada nivel tiene responsabilidades propias.

```
Esquema          → define el proceso y flow de prestación
  └── Producto / Póliza  → conjunto de beneficios
        └── Beneficio    → conjunto de servicios + tipo de cobertura
              └── Servicio → con incluye / no incluye / alcance
                    └── Bien / Asset → objeto físico sobre el que aplica
```

### Esquemas de prestación
| Esquema | Descripción | Ejemplos |
|---------|-------------|---------|
| **Asistencia** | Prestación directa por prestador designado por Vaitty. Modalidad estándar. | Plomería, electricidad, cerrajería |
| **Reintegro** | El beneficiario gestiona y paga; Vaitty reembolsa. Tres subtipos (ver abajo). | Servicios sin red de prestadores |
| **Siniestro** | Reclamación y liquidación por daño o evento. Requiere documentación. | GAREX, electrodomésticos |
| **Movilidad** | Asistencia en ruta. El prestador va al lugar del beneficiario móvil. | Remolque, asistencia vial, bicicleta |

### Tipos de reintegro
| Tipo | Definición | Impacto |
|------|-----------|---------|
| **Por defecto** | Solo puede prestarse por reintegro. No existe prestación directa. | Predecible, acotado al tope de cobertura |
| **Por elección** | El beneficiario prefiere gestionarlo por su cuenta. | Moderado. Menor costo operativo para Vaitty. |
| **Por falta de prestador** | No hay prestador disponible. Vaitty habilita el reintegro para no bloquear. | **ALTO**: consume casi siempre el 100% del tope por evento. Indicador de gap en red. Debe generar alerta operativa. |

### Reglas operativas del reintegro
- El beneficiario notifica a Vaitty dentro de las **72 horas** del evento
- Presenta comprobantes dentro de los **7 días corridos**
- Vaitty reintegra dentro de las **72 horas hábiles** de aprobado
- Validaciones antifraude obligatorias: ARCA + detector de duplicados

---

## Árbol de diseño de producto

El orden para diseñar cualquier producto es siempre este:

**1. Tipo de comercialización**
- Bundle: embebido en cartera existente del partner
- Stand-alone: se vende individualmente en mostrador (arranca desde 0 cápitas)

**2. Tipo de producto (modelo de cobertura)**

### WALLET
- El beneficiario tiene un **saldo anual** para gastar en cualquier servicio
- Tiene un **tope máximo por evento**
- Sin límite de cantidad de eventos por servicio o categoría
- Ejemplo: $1.000.000 anuales / $100.000 tope por evento
- Preguntar al partner: ¿cuánto quieren de saldo anual? ¿cuánto de tope por evento?

### TRADICIONAL
- La cobertura se segmenta **por categoría de servicio**
- Cada categoría tiene su propio monto por evento y su propio límite de eventos
- Las categorías pueden tener coberturas distintas entre sí
- Ejemplo Emergencias: hasta $34.000 por evento / máximo 3 eventos al año / 1 por mes
- Ejemplo Mantenimientos: hasta $50.000 por evento / máximo 1 por mes
- El límite de eventos puede ser: mensual fijo, anual fijo, o ilimitado
- Preguntar por cada categoría: monto por evento + límite de eventos (mensual/anual/ilimitado)

**3. Verticales**
Hogar / Movilidad / Mascotas / Personas

**4. Categorías dentro de cada vertical**
- Hogar: Emergencias, Mantenimientos, Instalaciones, Experiencias
- Movilidad: Emergencias viales, Asistencia bicicleta
- Mascotas: Televeterinaria (**precio fijo $25.000**), Emergencias veterinarias
- Personas: Telemedicina (**precio fijo $25.000**), Salud, Bienestar

**5. Montos y alcance de eventos**
- Si es Wallet: saldo anual total + tope por evento
- Si es Tradicional: por cada categoría → monto por evento + límite (mensual / anual / ilimitado)

### Servicios con precio fijo (no preguntar cobertura pretendida)
Algunos servicios tienen costo fijo por proveedor de Vaitty. Para estos NO se pregunta la cobertura pretendida al partner:
- **Telemedicina**: $25.000 por evento
- **Televeterinaria**: $25.000 por evento

### Tipos de cobertura por beneficio (Grow Center)
| Tipo | Parámetros | Uso |
|------|-----------|-----|
| **wallet** | annualAmount + eventAmount | Saldo anual con tope por evento |
| **events** | eventCount + eventLimit | Cantidad de eventos con monto límite |
| **km_events** | kmEventCount + kmRange | Eventos dentro de rango km — para Movilidad |
| **one_time** | oneTimeAmount | Precio fijo — Telemedicina, Televeterinaria |

### Modelos de cotización para Stand-alone

**Markup**: Vaitty calcula un precio base. El partner lo revende agregando su margen deseado.

**Comisión**: El partner informa su % de comisión (máximo 55%). Vaitty calcula el precio final al cliente que ya incluye esa comisión.
- Precio final = Precio base Vaitty / (1 - % comisión)
- Siempre verificar que la comisión no supere el 55%

---

## Proceso comercial (flujo del agente)

```
1. RECIBIR REQUERIMIENTO (chat con el partner)
   → Identificar: nombre del partner, tipo de cartera, capitas estimadas,
     productos actuales, objetivo (bundle/stand-alone), verticales de interés

2. DISEÑAR EL PRODUCTO
   → Seleccionar categorías y servicios del catálogo
   → Definir modelo de cobertura (wallet / límites / combinado)
   → Establecer incluye/excluye por servicio

3. COTIZAR
   → Cargar variables en el motor de cotización
   → Obtener precio per cápita, facturación total, rentabilidad

4. REDACTAR T&C
   → Adaptar el contrato base (TYC- SANCOR BANCOR) al nuevo partner
   → Incluir Anexo I (servicios y coberturas), Anexo II (plataforma), Anexo III (precio)

5. ARMAR PROPUESTA COMPLETA
   → Análisis del contexto del partner
   → Propuesta de producto (nombre, descripción, modelo de cobertura)
   → Servicios incluidos con alcances
   → Propuesta económica (precio per cápita, facturación estimada)
   → T&C

6. ENVIAR A SLACK PARA APROBACIÓN
   → Notificar a Nadir y Lara con el resumen de la propuesta
   → Esperar aprobación antes de enviar al partner

7. ENVIAR AL PARTNER (previa aprobación)
```

---

## Formato de propuesta (basado en La Caja 2024)

### Estructura del documento
1. **Análisis**: contexto del partner, oportunidades identificadas, puntos de dolor
2. **Propuesta de producto**: nombre del producto, concepto, diferenciadores
3. **Modelo de cobertura**: wallet/límites, montos, categorías incluidas
4. **Servicios incluidos**: listado con alcances por categoría
5. **Propuesta económica**: precio per cápita por segmento, condiciones
6. **Canales**: WhatsApp oficial, portal autogestión, API, Contact Center
7. **T&C**: referencia al contrato

---

## Contrato tipo

**Archivo**: `docs/TYC- SANCOR BANCOR 25112025.docx`

Estructura:
- **Carta oferta** firmada por Nadir Donemberg
- **Anexo A**: Cláusulas del Acuerdo (Objeto, Actuación, Plataforma, Precio, etc.)
- **Anexo I**: Términos y Condiciones específicos de servicios y coberturas
- **Anexo II**: Módulos y condiciones de uso de plataforma
- **Anexo III**: Precio y liquidación

Datos de Vaitty en contratos:
- Razón social: FAST HOME SERVICES S.A.S
- CUIT: 30-71516755-3
- Domicilio: Boulevard del Bicentenario de la Independencia Nacional N° 35, Oficina 8, Córdoba
- Matrícula: 14973-A
- Cuenta bancaria: CC Pesos N° 0020850-3 138-5 | CBU: 0070138520000020850353 | Banco Galicia

---

## Canales tecnológicos de Vaitty
- WhatsApp oficial certificado (automatizado)
- Portal de autogestión para usuarios
- APIs para integración en app/web del partner (full white label)
- Portal de seguimiento en tiempo real para la compañía
- IVR y canal telefónico exclusivo
- Portal partners: https://partners.vaitty.com.ar _(URL anterior: partners.rapihogar.com.ar)_

---

## SLAs y estándares operativos

- Servicio disponible **24 horas / 365 días** del año
- **80% de las llamadas** atendidas en menos de **20 segundos**
- **Emergencias**: atención con la mayor celeridad posible tras la solicitud
- **Tareas programadas** (mantenimiento, reparación, instalación): dentro de los **10 días corridos** desde la solicitud
- **Reintegro**: el beneficiario informa dentro de las **72 horas** del evento y presenta comprobantes dentro de los **7 días corridos**. Vaitty reintegra dentro de las **72 horas hábiles**.

## Exclusiones generales (aplican a todos los servicios)

- Mala fe o dolo del beneficiario
- Fallas o daños preexistentes antes del inicio del servicio
- Servicios contratados directamente sin autorización de Vaitty (salvo reintegro habilitado)
- Daños por fenómenos extraordinarios de la naturaleza (inundaciones, terremotos, huracanes, etc.)
- Daños intencionales, terrorismo, guerra, vandalismo, disturbios civiles
- Intervención de autoridad competente con orden judicial
- Cuando el beneficiario no se identifique como tal o no brinde información veraz
- Emergencias solo se prestan en el domicilio declarado al momento del alta
- Reparaciones de bienes muebles dañados como consecuencia de fallas eléctricas/hidráulicas

## Alcances por servicio (Hogar — referencia rápida)

| Servicio | Incluye | No incluye |
|----------|---------|-----------|
| Gas (pérdida) | Detección y reparación de fugas en cañerías externas; gasista matriculado | Cañerías empotradas, albañilería, medidores |
| Plomería (rotura) | Fugas en caños expuestos; sustitución del tramo dañado | Cañerías embutidas, rotura de pisos/paredes |
| Cerrajería | Apertura y ajuste en puertas externas | Cerraduras nuevas; electrónicas, digitales, blindadas |
| Electricidad (cortocircuito) | Reparación provisoria desde tablero interno | Electrodomésticos; redes externas; altura >2.4m |
| Destapaciones | Baños, cocinas y lavaderos hasta 7 metros | Presión de agua; cámaras sépticas, pozos, veredas |
| Vidrios | Verticales de cerramiento; medición y colocación | Blindados, curvos, horizontales, espejos; altura >2.4m |
| Calefones/termotanques | Revisión, limpieza, recambio de termocupla/flexible | Repuestos, parte eléctrica, albañilería |
| Cocinas/hornos a gas | Limpieza, regulación de quemadores e inyectores | Repuestos, parte eléctrica |
| Aire acondicionado | Limpieza de filtros, revisión conductos y termostatos | Bomba condensadora, trabajos en altura >2.4m |
| Telemedicina | Videollamada 24/7: medicina general, pediatría, ginecología | Medicamentos, atención presencial, enfermedades crónicas |
| Asistencia legal | Consulta con profesional, revisión de documentación | Actuaciones judiciales; solo 1 consulta por evento |
| Televeterinaria | Videollamada con veterinario para perros y gatos | Animales no de compañía; menores de 3 meses o mayores de 12 años |

---

## Nota importante — Marca
**Rapihogar** es el nombre anterior de Vaitty. Algunos documentos y contratos aún usan "Rapihogar" o "rapihogar.com.ar". Al generar nuevas propuestas y contratos, usar siempre **Vaitty**.

---

## Reglas de negocio (extraídas de contratos reales)

### Modelos de precio usados en el mercado

| Modelo | Unidad de cobro | Riesgo Vaitty | Partners |
|--------|----------------|---------------|---------|
| **Per cápita flat** | Beneficiario/mes fijo | Alto | Qualia, Galicia, RUS, AON |
| **Per cápita escalones** | Beneficiario/mes variable por tramos | **Nulo** (modelo propio) | BBVA |
| **Por evento/siniestro** | Servicio ejecutado | Nulo | Allianz, Hipotecario, Zurich |
| **Combinado cápita + evento** | Base fija/mes + cargo por ejecución | Bajo | — |
| **TPA Standard** | Precio target con 4 pilares + profit 50/50 neto | Compartido | SAI, Qualia Servicios |
| **TPA GAREX** | Fee admin % + markup 15% en reparaciones | Nulo | — |
| **GAREX Directo con seguro** | 4-6% del valor del bien (seguro 2.5-3%) | Acotado | — |
| **GAREX Directo sin seguro** | % del valor del bien, sin respaldo | Total | — |

**Notas clave:**
- Per cápita escalones: es capitado, no por evento. A mayor uso, mayor cobro. Riesgo cero para Vaitty.
- TPA Standard: precio target = costo admin (20-25%) + costo comercial (20-25%) + costo servicios + profit 50/50 neto. Riesgo compartido.
- GAREX Directo con seguro: Vaitty arbitra el spread entre precio al retail y costo del seguro.
- GAREX Directo sin seguro: Vaitty asume riesgo total, sin respaldo de terceros.

### Lógica de Wallet vs. Escalones
- **Wallet**: Modelo de cobertura con saldo anual fijo y tope por evento. Ideal para partners con uso predecible o bajo riesgo de alta frecuencia. Precio fijo per cápita, sin ajustes por uso real.
- **Escalones**: Precio que aumenta linealmente según la tasa de uso mensual (% de eventos sobre beneficiarios). Usado para gestionar riesgo en verticales con potencial de alta frecuencia (ej. Mascotas). El precio sube por tramos, incentivando control de uso.
- **Cuándo usar cada uno**: Wallet para stand-alone o bundles con bajo volumen; Escalones para productos embebidos en carteras grandes donde el uso puede escalar.

### Rangos de precio per cápita observados en contratos reales
| Tipo de producto | Mínimo | Típico | Premium |
|-----------------|--------|--------|---------|
| Hogar | $15-30 | $50-150 | $200-600+ |
| Mascotas | - | $577-1.000 | $2.785+ |
| Vida/Financiero | $15 | $53 | $152 |
| Movilidad (bici) | - | referencia baja | - |

### Límites de uso frecuencia por vertical
| Vertical | Techo mensual recomendado | Eventos/año estimados |
|----------|--------------------------|----------------------|
| Hogar | 1.3% | 15-18 cada 1.000 beneficiarios |
| Mascotas | 2.0-5.0% | mayor frecuencia esperada |
| Movilidad | 0.5-1.0% | menor frecuencia |
| Electrodomésticos | 1.0-2.0% | moderado |

### Patrones de productos por tipo de partner

**Aseguradoras** (Qualia, Allianz, RUS, AON):
- Producto principal: Hogar (emergencias + programados)
- Add-on típico: Mascotas, Movilidad
- Modelo: per cápita flat o escalones

**Bancos** (Galicia, BBVA, Hipotecario, Supervielle):
- Producto embebido en cartera de seguros
- Combinan múltiples líneas (Hogar + Vida + Financiero)
- Ejemplo Cencosud (via Qualia): 5 productos simultáneos con precios diferenciados

**Financieras/Retail** (Cencosud, Compre Directo):
- Productos tipo "Bolso Protegido", "Compra Protegida"
- Precio bajo ($53/cápita) por volumen alto
- Stand-alone, upsale en punto de venta

### Modelo financiero del ciclo de servicio

#### Proceso de transacción (nombrado operativo)
El evento financiero generado al completar un servicio se llama **Proceso de transacción** (no "factura generada"). Representa el registro interno en Vaitty del costo del servicio para posterior settlement con el prestador.

#### Facturación del prestador a Vaitty
- El prestador **NO factura por servicio individual**. Acumula múltiples servicios y emite una **factura acumulada periódica** a Vaitty (frecuencia a definir por contrato con cada prestador: semanal, quincenal, mensual).
- El importe que factura el prestador a Vaitty corresponde al **baremo pactado** por los servicios ejecutados dentro del tope de cobertura.
- El sistema debe soportar: múltiples ítems de servicio por factura de prestador, conciliación contra los Procesos de transacción generados, y aprobación antes del pago.

#### Recaudación del excedente por el prestador
- Cuando el costo total del servicio supera el tope de cobertura, el **excedente lo cobra el prestador directamente al beneficiario en el momento de finalizar el servicio**.
- Vaitty NO intermedia en el cobro del excedente.
- El sistema debe informar al prestador, antes de ejecutar el servicio, los dos montos: (a) lo que cubre Vaitty (baremo/cobertura), y (b) lo que puede cobrarle al beneficiario (excedente máximo). Esta información viaja en la **ServiceAuthorization**.
- El beneficiario debe conocer ambos montos antes de autorizar la prestación.

#### Flujo financiero completo (asistencia directa)
```
Servicio completado
  → Proceso de transacción generado (registro Vaitty)
  → Prestador cobra excedente al beneficiario (en el momento, directo)
  → Cobertura consumida (deducción wallet o events en el sistema)
  → Prestador acumula servicios en su período de facturación
  → Prestador emite factura acumulada a Vaitty
  → Vaitty concilia contra Procesos de transacción
  → Vaitty aprueba y paga al prestador
  → Sistema calcula comisiones del período
  → Liquidación al árbol de distribución
```

### Reglas para incorporar nuevos productos (Addendas)
1. Los productos nuevos (Mascotas, Movilidad) se agregan como **Addenda** al contrato original
2. Mantienen estructura de precio independiente (no se mezclan con Hogar)
3. Cada vertical tiene su propia grilla de precios
4. Se pueden combinar libremente (Hogar + Mascotas + Movilidad)

### Partners actuales documentados
| N° | Partner | Producto | Año inicio |
|----|---------|---------|-----------|
| 1 | Qualia | Hogar + multi-producto | 2021 |
| 2 | Galicia | Hogar | 2022 |
| 3 | BBVA | Hogar Full/PAS + Mascotas | 2024 |
| 4 | Allianz | Electrodomésticos | 2023 |
| 5 | RUS | Hogar | 2021 |
| 6 | Hipotecario Seguros | Claims/electrodomésticos | 2023 |
| 7 | Fedpat | Movilidad sustentable (bicicletas) | 2024 |
| 8 | Zurich/Santander | Liquidación de siniestros | 2023 |
| 9 | AON | Asistencias generales | 2025 |
| 10 | Meridional | - | - |
| 11 | La Caja | Hogar | - |
| 14 | Supervielle | - | - |
| 15 | Allianz (2° contrato) | - | - |
| 16 | Opción Seguros | - | - |
| 20 | Sancor/Bancor | - | 2025 |

---

## Portales de Partner — 3 stakeholders distintos

Existen tres portales partner, cada uno responde a un equipo diferente:

> **Decisión arquitectónica (2026-04-02)**: Los tres portales son UNA SOLA plataforma con módulos activados por tipo de usuario. Los presets de acceso los crea y modifica Vaitty a pedido del partner — el partner no puede auto-configurarse el acceso.

| Portal | Stakeholder | Función |
|--------|------------|---------|
| **Partner Grow Center** | Sales team del partner + equipo interno Vaitty | Configuración de coberturas y productos. Selecciona servicios del catálogo publicado por el Supply Domain. NO define servicios ni baremos. |
| **Partner Service Tracking** | Área de calidad/operaciones del partner | Seguimiento de servicios en curso, SLAs, calidad de prestadores, solicitar servicios. |
| **Partner Sales Manager** | Comercializadores, sucursales, vendedores | Alta de beneficiarios, gestión de ventas, comisiones devengadas de la red. |

### Partner Grow Center — Detalle técnico
- **Stack**: React 18 + TypeScript + Vite + Tailwind + TanStack Query (construido con Lovable)
- **Backend de producto**: API Gateway REST (`dev.rapihogar.com.ar` → migrar a `vaitty`)
- **Entidades que CONSUME (del Supply Domain / Provider & Service Mgmt)**: Servicios, Bienes (Assets), Especialidades — solo lectura para el Grow Center
- **Entidades propias en localStorage (migrar a BD)**: Beneficios, Coberturas, Productos, Listas de Precios, Partners
- **BusinessModels soportados**: `bundle`, `standalone`, `cashback`, `garantia_extendida`
- **Verticales**: `hogar`, `movilidad`, `mascotas`, `personas`, `dispositivos`
- **Tipos de partner**: asegurado, banco, retail, broker, real_estate, organizador, productor, asesor, prepaga, art
- **Rutas bloqueadas** (BlockedRouteProtector): dashboard, benefits, products, coverages, price-lists, clients — habilitables por configuración
- **Autenticación**: JWT via `POST /v1/backend/login/` — token en localStorage con clave `rapihogar_auth-token`

---

## Supply Domain — Provider & Service Management

### Decisión arquitectónica
**Fecha**: 2026-04-02

El catálogo de servicios (definición, baremos, bienes, especialidades) vive en el **Supply Domain**, no en el Product Configuration (Grow Center). El Grow Center consume el catálogo pero no lo define ni lo edita.

**Razón**: El baremo (precio al prestador) es el resultado de una negociación de Vaitty con el prestador. El partner nunca interviene en esa negociación — solo elige qué servicios cubre y hasta cuánto. Mezclar la definición del servicio con la configuración del producto crea acoplamiento innecesario y expone datos de costos al partner.

### Dos capas internas del mismo bounded context

**Service Catalog** (qué existe, definido por Vaitty ops):
- Definición de servicios: nombre, descripción, incluye, no incluye, exclusiones
- Bienes / Assets sobre los que aplica cada servicio
- Especialidades requeridas por servicio
- Precio de referencia orientativo (3 capas: baremo real, referencia de mercado, historial de 8 años)

**Provider Registry** (quién ejecuta, negociado con prestadores):
- Padrón de prestadores con perfil de servicios y zonas de cobertura
- Baremos por prestador, especialidad y zona geográfica
- Performance histórica y métricas de calidad
- Algoritmo de posicionamiento: prestadores en rango del precio de referencia ganan prioridad
- Gap de red: sin prestador → habilita reintegro + alerta operativa automática

### Flujo de consumo
```
Provider & Service Mgmt publica catálogo
  → Product Configuration (Grow Center) consume y selecciona servicios
  → Product Engine arma coberturas y precios sobre esa selección
  → Service Orchestration consulta Provider Registry para asignar prestador
  → Finance consulta baremo para liquidar al prestador
```

### Regla clave de separación
| Concepto | Dueño | Visible al partner |
|----------|-------|-------------------|
| Definición del servicio (qué incluye) | Supply Domain | Sí (read-only) |
| Baremo (precio al prestador) | Supply Domain | **No** |
| Precio de referencia orientativo | Supply Domain | Sí |
| Monto de cobertura al beneficiario | Product Configuration | Sí |
| Límites de eventos | Product Configuration | Sí |

---

## Infraestructura técnica del proyecto

### Agente conversacional — "Mati Caballero"
El agente principal del proyecto se llama **Mati Caballero** (Business Developer de Vaitty). Es un agente conversacional construido con la API de Anthropic que acompaña el proceso comercial con partners de punta a punta.

- **Modelo**: claude-opus-4-6 con `thinking: adaptive`
- **Entry point**: `agent/main.py` — loop de chat por terminal
- **Prompt del sistema**: `agent/system_prompt.py` — define personalidad, flujo de trabajo (6 pasos), reglas de cotización, alcances de servicios por T&C

Flujo de trabajo de Mati (6 pasos):
1. Intake — toma de requerimientos del partner (una pregunta por turno)
2. Co-diseño del producto — verticales, categorías, coberturas
3. Confirmación del cliente — el partner aprueba el "qué" antes de ver precios
4. Pedir email y registrar cotización — llama a herramienta `registrar_cotizacion`
5. Cotización interna — Nadir y Lara aprueban el precio
6. Envío de propuesta al partner

**Regla clave**: Mati NUNCA muestra precios al partner directamente. Solo el equipo interno (Nadir/Lara) los ve y aprueba antes de enviarlos.

### Agentes especializados (módulos Python)
| Archivo | Función |
|---------|---------|
| `agent/baremo_agent.py` | Consulta y análisis de baremos (tablas de precios de prestadores) |
| `agent/catalogo_agent.py` | Acceso y consulta del catálogo de servicios |
| `agent/market_researcher.py` | Investigación de mercado y competencia |
| `agent/partner_pricing_agent.py` | Cotización y pricing por partner |
| `agent/service_pricing_agent.py` | Pricing a nivel de servicio individual |
| `agent/sheet_catalogo.py` | Integración con Google Sheets del catálogo |

### Base de datos
- **Archivo**: `data/mati.db` (SQLite)
- Almacena cotizaciones registradas por Mati, datos de partners, eventos

### Servidor webhook
- **`webhook/server.py`**: servidor HTTP (FastAPI/Flask) que recibe eventos externos
- **`webhook/db.py`**: capa de acceso a base de datos del webhook
- **`service_manager.py`**: gestor de servicios del servidor
- **`start_server.sh`**: script de arranque del servidor

### Integración con Google
- `google_credentials.json` — credenciales de servicio de Google
- `google_oauth_client.json` — configuración OAuth
- `google_token.pickle` — token de acceso activo
- Uso probable: Google Sheets (catálogo, cotizador) y/o Google Drive

### Base de conocimiento T&C (extraída)
Documentos de Términos y Condiciones procesados y disponibles en texto plano para el agente:

| Archivo | Contenido |
|---------|-----------|
| `data/tyc_docs/tyc_sancor_bancor.txt` | T&C contrato Sancor/Bancor |
| `data/tyc_docs/tyc_bancor_hogar_v2.txt` | T&C Hogar v2 Bancor |
| `data/tyc_docs/tyc_qualia_hogar.txt` | T&C Qualia Hogar |
| `data/tyc_docs/acuerdo_qualia_2025.txt` | Acuerdo Qualia 2025 |
| `data/tyc_docs/allianz_tc_hogar_oct24.txt` | T&C Allianz Hogar Oct 2024 |
| `data/tyc_docs/tyc_hogar_modelo.txt` | T&C Hogar modelo genérico |
| `data/tyc_docs/tyc_mascotas_modelo.txt` | T&C Mascotas modelo |
| `data/tyc_docs/tyc_movilidad_modelo.txt` | T&C Movilidad modelo |
| `data/tyc_docs/tyc_personas_modelo.txt` | T&C Personas modelo |
| `data/tyc_docs/tyc_salud_modelo.txt` | T&C Salud modelo |
| `data/tyc_docs/tyc_tecnologia_modelo.txt` | T&C Tecnología modelo |
| `data/tyc_docs/tyc_rus_mascotas_*.txt` | T&C RUS Mascotas (Esencial, Simple, Integral) |
| `data/tyc_docs/tyc_life_sai_hogar_premium.txt` | T&C Life SAI Hogar Premium |
| `data/tyc_docs/tyc_generico_rapihogar.txt` | T&C genérico histórico (marca anterior) |
| `data/tyc_docs/_extracted_*.md` | Resúmenes procesados por vertical |
| `agent/knowledge/tyc_rules.md` | Reglas de negocio extraídas de contratos |

### Logs del servidor
- `logs/server.log` — log general de operaciones
- `logs/server_error.log` — log de errores

---

## Mapa de archivos del proyecto

```
vaitty/
├── CLAUDE.md                          ← Este archivo. Memoria persistente del proyecto.
├── agent/
│   ├── main.py                        ← Entry point del agente Mati (terminal)
│   ├── system_prompt.py               ← Personalidad y flujo completo de Mati
│   ├── baremo_agent.py                ← Agente de baremos de prestadores
│   ├── catalogo_agent.py              ← Agente de catálogo de servicios
│   ├── market_researcher.py           ← Agente de investigación de mercado
│   ├── partner_pricing_agent.py       ← Agente de pricing por partner
│   ├── service_pricing_agent.py       ← Agente de pricing por servicio
│   ├── sheet_catalogo.py              ← Integración Google Sheets catálogo
│   └── knowledge/
│       └── tyc_rules.md               ← Reglas de negocio extraídas de contratos
├── data/
│   ├── mati.db                        ← Base de datos SQLite (cotizaciones, partners)
│   └── tyc_docs/                      ← T&C extraídos en texto plano (14 archivos)
├── webhook/
│   ├── server.py                      ← Servidor webhook HTTP
│   └── db.py                          ← Acceso a BD del webhook
├── docs/
│   ├── Cotizador.xlsx                 ← Motor de cotización (variables e inputs)
│   ├── Listado de servicios.xlsx      ← Catálogo de servicios (formato original)
│   ├── Vaitty - Catalogo de Servicios.xlsx  ← Catálogo actualizado Vaitty
│   ├── Vaitty - Nuevos Servicios Propuestos.xlsx ← Servicios en evaluación
│   ├── catalogo_servicios.md          ← Catálogo completo en Markdown (generado por agente)
│   ├── baremo_cache.json              ← Cache de baremos procesados
│   ├── TYC- SANCOR BANCOR 25112025.docx ← Contrato tipo (base para nuevos contratos)
│   ├── Propuesta Asistencias La caja Hogar (Sep 2024) REV.docx ← Propuesta referencia
│   ├── Contratos con clientes/        ← PDFs firmados de todos los partners (9+)
│   └── competencia/                   ← Baremos y materiales de competidores
│       ├── AXA Partners/              ← AXA Partners 2023, IPAS 2022
│       ├── Allianz Partners/          ← Baremo AZ 2023
│       ├── Asitur/                    ← Baremo por provincia
│       ├── Cuidacasa/                 ← Siniestros graves
│       ├── Home serve/                ← Baremo profesionales
│       ├── Multiasistencia/           ← Baremo 2022
│       ├── Mutua Madrileña/           ← Baremo Hogar 2022
│       ├── On red (funciona)/         ← Baremo multigremio
│       ├── Servihogar (Zurich/Liberty)/ ← Baremos A/B/C
│       ├── Comparativa Baremos Venta.xlsx ← Comparativa consolidada
│       └── Rapihogar Baremo.xlsx      ← Baremo propio (nombre histórico)
├── service_manager.py                 ← Gestor del servidor
├── start_server.sh                    ← Script de arranque
├── google_credentials.json            ← Credenciales Google (no subir a git)
├── google_oauth_client.json           ← OAuth client config (no subir a git)
├── google_token.pickle                ← Token activo Google (no subir a git)
└── logs/
    ├── server.log                     ← Log operacional
    └── server_error.log               ← Log de errores
```

---

## Estado del proyecto y bitácora de sesiones

> **Convención**: Al terminar una sesión de trabajo relevante, actualizar esta sección con fecha, qué se hizo y qué queda pendiente. Así la próxima sesión arranca con contexto.

### Última sesión — 2026-04-02 (sesión 4)
**Qué se hizo:**
- Rediseño del mapa interactivo del sistema (vaitty_map_v3.html): se agregaron 8 sistemas fuera del Event Bus con cards expandibles, descripción del Event Bus, distinción por tipo (channel adapter / comercial / analytics / redefinir)
- Canales conversacionales incorporados: WhatsApp Bot (beneficiario, estructurado → redefinir), Voice Bot (monolito → redefinir), Bot WhatsApp Prestador (activo, gaps en métricas), Agente Mati actualizado (opera vía WhatsApp, dual-role: comercial + BI)
- Decisión arquitectónica clave: **Supply Domain** — el catálogo de servicios y los baremos se mueven de Product Configuration (Grow Center) a Provider & Service Management. El Grow Center consume el catálogo pero no lo define.
- Artefactos creados: Cotizador interactivo (HTML con React, motor de pricing completo), Product Tree Builder (wizard 6 pasos)
- Skills creados y empacados: `cotizar`, `propuesta-comercial`, `generar-tyc`
- Clarificaciones incorporadas: Partner Platform es UNA plataforma con 3 vistas por módulo; presets controlados por Vaitty

**Descubrimientos / Reglas confirmadas en esta sesión:**
- La Partner Platform (Grow Center + Service Tracking + Sales Manager) es una sola plataforma — los módulos visibles los define Vaitty a pedido del partner
- WhatsApp tiene 3 bots para 3 personas distintas: beneficiario (estructurado, redefinir), prestador (activo), partner/Mati (comercial + BI)
- Mati también corre por WhatsApp y tiene rol de BI para partners activos (datos de clientes, servicios, tasas de uso, indicadores)
- **Supply Domain**: baremo y definición de servicio pertenecen a Provider & Service Management, no al Grow Center. Separación crítica para no exponer costos al partner.
- Voice Bot: monolito sin skills → redefinir como orquestador de voz + skills intercambiables deployables independientemente

**Próximos pasos sugeridos:**
- [ ] Instalar skills creados: `cotizar`, `propuesta-comercial`, `generar-tyc`
- [ ] Validar cotizador y product tree builder abriendo los HTML
- [ ] Diseñar la arquitectura de la capa de mensajería WhatsApp (3 números/cuentas separadas para 3 personas)
- [ ] Iniciar diseño de la arquitectura del Voice Bot modular (STT → intent → routing → skills)
- [ ] Migrar entidades localStorage del Grow Center a base de datos real (PRIORIDAD)
- [ ] Incorporar Supply Domain al `vaitty_product_system_core_v3.docx`
- [ ] Configurar integración con Slack para notificaciones de aprobación

---

### Última sesión — 2026-04-02 (sesión 3)
**Qué se hizo:**
- Análisis arquitectónico profundo como AI Architect: 7 bounded contexts, commission engine, service lifecycle con event sourcing
- Correcciones y clarificaciones de reglas de negocio:
  - Comisiones: one-shot vs. recurring, pueden coexistir, campo `trigger`
  - Identidad del beneficiario: 4 flujos de activación según quién recauda
  - Períodos de gracia stand-alone: ciclo de recaudación del 1 al 10
  - Modelo financiero completo: "Proceso de transacción" (no "factura generada"), prestador factura acumulada a Vaitty, excedente cobrado por prestador directo al beneficiario en el momento
  - Precio de referencia de catálogo vs. baremo: 3 capas de datos (baremo, referencia, historial real)
  - Posicionamiento de prestadores por precio de referencia
- Creación de mapa interactivo del sistema: `docs/vaitty_system_map.jsx` (React + Tailwind, 7 vistas navegables)
- Incorporación de todas las reglas financieras a CLAUDE.md (sección "Modelo financiero del ciclo de servicio")
- Incorporación de reglas al mapa del sistema y al panel de detalle de Finance

**Descubrimientos / Reglas confirmadas en esta sesión:**
- El evento al completar un servicio se llama **Proceso de transacción** (nomenclatura operativa)
- El prestador **NO factura por servicio**: emite factura acumulada periódica a Vaitty
- El excedente lo recauda el prestador **directo al beneficiario al momento de finalizar**
- Hay 8 años de data histórica que deben cruzarse con el nuevo modelo de datos
- La configuración por partner es el gap más importante — dos interfaces: Portal + Mati

**Próximos pasos sugeridos:**
- [x] Actualizar URL en `agent/system_prompt.py` (rapihogar → vaitty) — corregido 2026-04-02
- [x] Sincronizar lógica del árbol de diseño de producto entre `system_prompt.py` y `CLAUDE.md` — completado 2026-04-02
- [x] Mapa interactivo del sistema — completado 2026-04-02
- [ ] Incorporar reglas de esta sesión al `vaitty_product_system_core_v2.docx`
- [ ] Configurar integración con Slack para notificaciones de aprobación
- [ ] Definir canal de entrada del agente (WhatsApp — pendiente setup)
- [ ] Migrar entidades localStorage del Grow Center a base de datos real (PRIORIDAD)
- [ ] Conectar Mati al Product Engine vía API
- [ ] Cross-reference del modelo de datos histórico (8 años) con el nuevo diseño

---

### Última sesión — 2026-04-02
**Qué se hizo:**
- Correcciones en CLAUDE.md: tabla de precios duplicada eliminada, URL portal partners actualizada (rapihogar → vaitty), nota de migración de marca marcada como completada
- Exploración completa de la estructura del proyecto
- Incorporación al CLAUDE.md de: infraestructura técnica, mapa de archivos completo, sección de bitácora

**Descubrimientos importantes:**
- El agente tiene nombre propio: **Mati Caballero**
- El `system_prompt.py` tiene lógica más detallada que el CLAUDE.md en algunas áreas (árbol de diseño de producto, servicios con precio fijo, etc.) — considerar sincronizar
- El `system_prompt.py` todavía referenciaba `partners.rapihogar.com.ar` — **corregido en esta sesión**
- Existe una base de datos SQLite (`data/mati.db`) y un servidor webhook funcional
- La carpeta `competencia/` tiene baremos de 8 competidores — útil para benchmarking de precios

**Próximos pasos sugeridos:**
- [x] Actualizar URL en `agent/system_prompt.py` (rapihogar → vaitty) — corregido 2026-04-02
- [x] Sincronizar lógica del árbol de diseño de producto entre `system_prompt.py` y `CLAUDE.md` — completado 2026-04-02
- [ ] Configurar integración con Slack para notificaciones de aprobación
- [ ] Definir canal de entrada del agente (WhatsApp — pendiente setup)

---

## Notas pendientes
- [x] Profundizar reglas de negocio con Lara (confirmar lógica de wallet vs. escalones) — Documentado en sección Reglas de negocio
- [ ] Configurar integración con Slack para notificaciones de aprobación
- [ ] Definir canal de entrada del agente (WhatsApp — pendiente setup)
- [x] Actualizar nombre de plataforma en contratos (rapihogar → vaitty) — URL corregida en CLAUDE.md; contratos históricos mantienen Rapihogar como registro
