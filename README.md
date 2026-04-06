# Vaitty — Business Developer Agent

**Vaitty** es una plataforma tecnológica que simplifica la vida de las personas a través de servicios coordinados. Este repositorio contiene la documentación, herramientas interactivas y configuración del **Business Developer Agent (Mati Caballero)**.

## 🗂️ Contenido del repositorio

### Documentación
- **`CLAUDE.md`** — Memoria completa del proyecto, reglas de negocio, estructura técnica, partners, modelos de pricing, alcances de servicios.

### Herramientas Interactivas
- **`vaitty-map.html`** — Mapa interactivo del sistema (8 pestañas: Bounded Contexts, Finance, Partner Platform, Supply Domain, Orchestration, Analytics, Channels, Business Model Canvas). 🔐 Contraseña: `vaitty2026`
- **`cotizador_vaitty.html`** — Cotizador interactivo con motor de pricing completo (variables de entrada, cálculos de margen, curva de uso).
- **`product_tree_builder.html`** — Wizard de 6 pasos para diseñar productos Vaitty (tipo de comercialización, modelo de cobertura, verticales, servicios, montos, alcances).

### Documentos de Referencia
- **TYC- SANCOR BANCOR 25112025.docx** — Contrato tipo con estructura estándar de Vaitty.
- **Catálogo de Servicios** — XLSX con definición completa de servicios por vertical (Hogar, Movilidad, Mascotas, Personas).
- **Cotizador.xlsx** — Motor de cotización con variables de entrada y lógica de cálculo.

---

## 🎯 Proceso comercial

El flujo de trabajo de **Mati Caballero** (agente de Business Development):

```
1. RECIBIR REQUERIMIENTO → Identificar partner, cartera, capitas
2. DISEÑAR PRODUCTO → Seleccionar categorías, modelo de cobertura
3. COTIZAR → Variables en motor, obtener precio per cápita
4. REDACTAR T&C → Adaptar contrato base
5. ARMAR PROPUESTA → Análisis, producto, económica, T&C
6. ENVIAR A APROBACIÓN → Slack (Nadir, Lara) → Envío a partner
```

---

## 📊 Verticales y Servicios

| Vertical | Categorías | Ejemplos |
|----------|-----------|----------|
| **Hogar** | Emergencias, Programados, Instalaciones | Plomería, Electricidad, Cerrajería, Mantenimientos |
| **Movilidad** | Emergencias viales, Asistencia sustentable | Remolque, Asistencia en ruta, Bicicleta |
| **Mascotas** | Televeterinaria, Emergencias | Consulta virtual ($25.000), Cirugía, Internación |
| **Personas** | Telemedicina, Salud, Bienestar | Videollamada ($25.000), Psicología, Nutrición |

---

## 💰 Modelos de Cobertura

### Wallet
- Saldo anual con tope máximo por evento
- Ejemplo: $1.000.000 anuales / $100.000 tope por evento

### Tradicional (Límites)
- Cobertura segmentada por categoría
- Cada categoría: monto por evento + límite de eventos (mensual/anual/ilimitado)
- Ejemplo: 1 mantenimiento/mes, 3 emergencias/año

### Escalones
- Precio aumenta según tasa de uso mensual (%)
- Usado en productos con potencial de alta frecuencia

---

## 🏢 Partners Actuales

| Partner | Producto | Año |
|---------|---------|-----|
| Qualia | Hogar + multi-producto | 2021 |
| Galicia | Hogar | 2022 |
| BBVA | Hogar Full/PAS + Mascotas | 2024 |
| Allianz | Electrodomésticos | 2023 |
| RUS | Hogar | 2021 |
| Hipotecario | Claims/electrodomésticos | 2023 |
| Zurich/Santander | Liquidación de siniestros | 2023 |
| AON | Asistencias generales | 2025 |
| Sancor/Bancor | Hogar | 2025 |

---

## 🔧 Cómo usar este repositorio

### 1. Explorar el Mapa del Sistema
Abre `vaitty-map.html` en tu navegador. Contiene 8 vistas navegables de la arquitectura completa.
- **Contraseña**: `vaitty2026`

### 2. Diseñar un Producto
Usa `product_tree_builder.html` para:
- Elegir tipo de comercialización (Bundle/Stand-alone)
- Definir modelo de cobertura (Wallet/Tradicional/Escalones)
- Seleccionar verticales y categorías
- Especificar montos y límites

### 3. Cotizar
Usa `cotizador_vaitty.html` para:
- Ingresar variables de entrada (capitas, tasa de uso, cobertura media, etc.)
- Calcular precio per cápita
- Ver rentabilidad estimada
- Ajustar por curva de uso

### 4. Consultar Reglas de Negocio
Lee `CLAUDE.md` para:
- Estructura del producto (5 niveles jerárquicos)
- Alcances y exclusiones de servicios
- Modelos de precio (per cápita, escalones, TPA, etc.)
- Reglas operativas (SLAs, reintegro, etc.)
- Infraestructura técnica

---

## 📝 Notas Importantes

- **Marca**: La documentación usa **Vaitty**. "Rapihogar" es el nombre anterior (aún en contratos históricos).
- **Acrónimos**:
  - **TPA**: Third Party Administrator (pricing target con riesgo compartido)
  - **GAREX**: Garantía extendida para electrodomésticos
  - **SLA**: Service Level Agreement (estándares operativos)
- **Precio de referencia**: El catálogo tiene 3 capas de datos (baremo real, referencia de mercado, historial de 8 años).

---

## 🔐 Acceso a Herramientas

Todas las herramientas interactivas requieren contraseña para proteger datos comerciales.

**Contraseña**: `vaitty2026`

---

## 📞 Contacto

**CEO**: Nadir Donemberg (nadir@vaitty.com)
**Business Manager**: Lara Tzvir

**Razón social**: FAST HOME SERVICES S.A.S
**CUIT**: 30-71516755-3
**Domicilio**: Boulevard del Bicentenario de la Independencia Nacional N° 35, Oficina 8, Córdoba

---

## 📄 Licencia

Proyecto confidencial de Vaitty. Prohibida la distribución sin autorización.

---

**Última actualización**: 2026-04-06
**Versión**: 1.0
