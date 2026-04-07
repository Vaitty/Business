# Vaitty — Índice de Documentación Modular

**Última actualización**: 2026-04-06
**Estado**: [VIGENTE] — Este índice refleja la realidad operativa

---

## 📋 Navegación Rápida

### Información Corporativa
- **[01_IDENTIDAD.md](01_IDENTIDAD.md)** — Razón social, CEO, datos bancarios, nota sobre marca (Rapihogar → Vaitty)

### Productos y Servicios
- **[02_VERTICALES.md](02_VERTICALES.md)** — Estructura de 4 verticales (Hogar, Mascotas, Movilidad, Personas), servicios, alcances
- **[03_PRODUCTOS.md](03_PRODUCTOS.md)** — Árbol de diseño (5 pasos), modelos de cobertura (Wallet/Tradicional/Escalones), paquetes (Bundle/Stand-alone)
- **[04_COTIZADOR.md](04_COTIZADOR.md)** — Lógica de cotización, variables, fórmulas, rangos de precio, modelos de pricing

### Operativo
- **[05_OPERATIVO.md](05_OPERATIVO.md)** — SLAs, exclusiones, flujos (directa/reintegro), obligaciones beneficiario, flujo financiero
- **SERVICIOS_DETALLE.md** *(próximo)* — Alcances completos por servicio (Gas, Plomería, Cerrajería, etc.)

### Comercial y Partners
- **[06_PARTNERS.md](06_PARTNERS.md)** — Lista de partners actuales (15 documentados), patrones por tipo, oportunidades
- **[07_CONTRATOS.md](07_CONTRATOS.md)** — Datos legales, estructura T&Cs, Anexos, checklist, organización de archivos

### Técnico
- **TECNOLOGIA.md** *(próximo)* — Infraestructura, agentes (Mati Caballero), servicios webhook, bases de datos
- **ARQUITECTURA.md** *(próximo)* — Bounded contexts, modelo financiero, flujo de transacciones

### Histórico y Cambios
- **[REFACTORING_HISTORY.md](REFACTORING_HISTORY.md)** — Hitos de refactorización y cambios arquitectónicos
- **BITACORA_SESIONES.md** *(próximo)* — Registr cronológico de cambios, decisiones, evolución del proyecto

---

## 🗂️ Estructura de Carpetas

```
docs/
├── _REFERENCE/
│   ├── INDEX.md                    ← AQUÍ ESTÁS
│   ├── 01_IDENTIDAD.md
│   ├── 02_VERTICALES.md
│   ├── 03_PRODUCTOS.md
│   ├── 04_COTIZADOR.md
│   ├── REFACTORING_HISTORY.md
│   ├── product_system_core_v3.docx (documento de arquitectura)
│   └── ...
├── _CATALOGO/
│   ├── catalogo_servicios.md       (fuente de verdad)
│   └── Vaitty - Catalogo de Servicios.xlsx
├── _MAPAS/
│   ├── vaitty_map_v3.html         (actual)
│   ├── vaitty_map.html
│   └── vaitty_map_secured.html
└── ...
```

---

## 🔍 Cómo Usar Este Índice

**Si buscas...**

- **"¿Cómo cotizo un producto?"** → [04_COTIZADOR.md](04_COTIZADOR.md)
- **"¿Cuáles son los verticales?"** → [02_VERTICALES.md](02_VERTICALES.md)
- **"¿Cómo diseño un producto?"** → [03_PRODUCTOS.md](03_PRODUCTOS.md)
- **"¿Cuál es el CUIT de Vaitty?"** → [01_IDENTIDAD.md](01_IDENTIDAD.md)
- **"¿Qué cambió recientemente?"** → [REFACTORING_HISTORY.md](REFACTORING_HISTORY.md)
- **"¿Qué SLAs tenemos?"** → OPERATIVO.md *(próximo)*
- **"¿Quiénes son nuestros partners?"** → PARTNERS.md *(próximo)*

---

## 📝 Convención de Marcado

- **[VIGENTE]** — Información actual y operativa
- **[HISTÓRICO]** — Información antigua, conservada por referencia
- **[DEPRECADO]** — Información que fue reemplazada, NO usar

---

## 🔄 Cambios Recientes

**2026-04-06** — REFACTORING #3
- Modularización de CLAUDE.md en 9 archivos temáticos
- Creación de INDEX.md para navegación centralizada
- Marques [VIGENTE] vs [HISTÓRICO]
- Ver [REFACTORING_HISTORY.md](REFACTORING_HISTORY.md) para detalles

---

**Próxima revisión**: 2026-04-13
