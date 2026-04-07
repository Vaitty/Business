# Lógica de Cotización

**Estado**: [VIGENTE]

## Variables de Entrada (Motor de Cotización)

| Variable | Descripción | Default |
|----------|-------------|---------|
| **Capitas** | Número de beneficiarios | — |
| **Tasa de uso base** | % mensual de uso esperado del servicio | 0.3% |
| **Cobertura media** | Ticket/cobertura promedio por evento ($) | — |
| **Markup comercial** | Multiplicador sobre costo cápita | 5x |
| **Impuestos directos** | % sobre precio | 9% |
| **Comisión comercial canal** | Revenue share del canal | 55% máx |
| **Costo IT por servicio** | Costo tecnológico variable por uso ($) | Variable |
| **Costo unitario operación** | Costo mensual por FTE operativo ($) | Variable |
| **Productividad operación** | Servicios por FTE por mes | Variable |

---

## Fórmula de Cálculo (Simplificada)

```
1. Servicios por mes = Capitas × Tasa de uso base
2. Costo directo = Servicios × Cobertura media
3. Subtotal costo cápita = (Costo directo + Costo operación + Costo IT + Costo admin) / Capitas
4. Precio per cápita = (Subtotal costo × Markup + Impuestos)
5. Rentabilidad neta = (Facturación - Comisión canal - Costos) / Facturación
```

---

## Ajuste por Curva de Uso

El precio sube proporcionalmente si la tasa de uso real supera la base.

**Lógica**: Si asumimos 0.3% y el cliente usa 0.5%, el precio se ajusta hacia arriba.

---

## Rangos de Precio Observados (Contratos Reales)

### Por Vertical

| Vertical | Mínimo | Típico | Premium |
|----------|--------|--------|---------|
| **Hogar** | $15-30 | $50-150 | $200-600+ |
| **Mascotas** | — | $577-1.000 | $2.785+ |
| **Vida/Financiero** | $15 | $53 | $152 |
| **Movilidad** | — | Ref baja | — |

---

## Modelos de Precio en Mercado

| Modelo | Unidad | Riesgo | Partners |
|--------|--------|--------|----------|
| **Per Cápita Flat** | Beneficiario/mes fijo | Alto | Qualia, Galicia, RUS, AON |
| **Per Cápita Escalones** | Variable por tramos | Nulo | BBVA |
| **Por Evento/Siniestro** | Servicio ejecutado | Nulo | Allianz, Zurich, Hipotecario |
| **Combinado** | Base + por evento | Bajo | — |
| **TPA Standard** | Target + 50/50 profit | Compartido | SAI, Qualia Servicios |
| **GAREX** | 4-6% del valor del bien | Acotado | Hipotecario |
| **Stand-alone Markup** | Precio base × markup partner | Bajo | Retail/Financieras |

---

## IMPORTANTE — Confidencialidad

**NUNCA mostrar al partner**:
- Rentabilidad interna de Vaitty
- Costos de operación
- Márgenes o markups internos
- Estructura de costos

**Mostrar solo**:
- Precio per cápita
- Facturación total estimada
- (Stand-alone) Precio final al cliente (si es modelo Comisión)

---

**Última actualización**: 2026-04-06
**Archivo de cálculo**: `/docs/Cotizador.xlsx`
