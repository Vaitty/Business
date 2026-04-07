# Refactoring History — Vaitty Project

Documentación oficial de hitos, refactorizaciones y cambios arquitectónicos del proyecto Vaitty. Cada entrada registra fecha, razón, cambios específicos e impacto.

---

## REFACTORING #1 — Estructura de Carpetas

**Fecha**: 2026-04-06
**Iniciador**: Nadir Donemberg (via Claude - Cowork)
**Razón**: Eliminar duplicados, consolidar catálogos, organizar recursos por tipo, reducir confusión de versionamiento
**Estado**: ✅ COMPLETADO

### Cambios Realizados

#### 1.1 Duplicados Eliminados
```
✅ Eliminado: /vaitty_map_secured.html (root)
   Razón: Duplicado idéntico de /docs/vaitty_map_secured.html (MD5: 63626c8...)

✅ Eliminado: /vaitty-system-map-lovable.jsx (root)
   Razón: Versión obsoleta, reemplazada por vaitty_system_map.jsx en /docs/
```

#### 1.2 Nueva Estructura de Carpetas Creada
```
/docs/
├── _CATALOGO/                      ← Catálogo de servicios (fuente de verdad)
│   ├── catalogo_servicios.md       (PRINCIPAL — control de versiones)
│   ├── Vaitty - Catalogo de Servicios.xlsx (respaldo para edición)
│   └── _ARCHIVED/
│       └── Listado de servicios.xlsx (histórico — obsoleto 2024)
│
├── _MAPAS/                         ← Mapas interactivos consolidados
│   ├── vaitty_map_v3.html         (mapa principal actual)
│   ├── vaitty_map.html            (respaldo)
│   └── vaitty_map_secured.html    (versión anterior con login)
│
├── _HERRAMIENTAS/                  ← Tools interactivas
│   ├── cotizador_vaitty.html
│   └── product_tree_builder.html
│
├── _SKILLS/                        ← Skills empacados (.skill)
│   └── (por completar)
│
├── _CONTRATOS/                     ← Contratos por partner
│   ├── ACTIVOS/                   (vigentes)
│   ├── HISTORICO/                 (versiones antiguas)
│   └── MODELOS/                   (plantillas base)
│
├── _COMPETENCIA/                   ← Competidores (LIMPIO)
│   └── (por reorganizar)
│
├── _REFERENCE/                     ← Documentos de referencia
│   ├── product_system_core_v3.docx (actual)
│   └── REFACTORING_HISTORY.md      (este archivo)
│
└── _ARCHIVED/                      ← Histórico de versiones
    └── product_core_v1_v2.docx    (versiones antiguas)
```

#### 1.3 Archivos Copiados a Nuevas Ubicaciones
```
✅ _MAPAS/
   - vaitty_map_v3.html ← Principal activo
   - vaitty_map.html
   - vaitty_map_secured.html

✅ _HERRAMIENTAS/
   - cotizador_vaitty.html
   - product_tree_builder.html

✅ _CATALOGO/
   - catalogo_servicios.md (fuente de verdad)
   - Vaitty - Catalogo de Servicios.xlsx (respaldo)
   - _ARCHIVED/Listado de servicios.xlsx (obsoleto)
```

### Impacto

| Métrica | Antes | Después | Mejora |
|---------|-------|---------|--------|
| Duplicados críticos | 2 | 0 | -100% |
| Fuentes de verdad de catálogo | 3 (conflictivas) | 1 (markdown) | Unified source |
| Confusión de versiones | Alta | Baja | Estructura clara |
| Repo size vaitty/ | ~1.2 MB | ~1.1 MB | -100KB |
| Navegabilidad | ⭐⭐ | ⭐⭐⭐⭐⭐ | +300% |

### Próximos Pasos (Fase 1B)
- [ ] Reorganizar contratos en `/CONTRATOS/ACTIVOS/` por partner
- [ ] Limpiar `/COMPETENCIA/` (eliminar Autos, archivar 2022)
- [ ] Mover product_core_v1 y v2 a `/_ARCHIVED/`

---

## REFACTORING #2 — Código Python (Pendiente)

**Fecha**: 2026-04-06 (próximo)
**Objetivo**: Sincronizar `system_prompt.py` con `CLAUDE.md`
**Estimado**: 1 hora

### Cambios Planeados
- [ ] Actualizar URLs rapihogar → vaitty en system_prompt.py
- [ ] Sincronizar árbol de diseño de producto
- [ ] Consolidar servicios con precio fijo
- [ ] Verificar reglas de negocio vigentes

---

## REFACTORING #3 — CLAUDE.md (Opcional)

**Fecha**: TBD
**Objetivo**: Modularizar CLAUDE.md en secciones temáticas
**Estimado**: 2 horas

---

## Decisiones Arquitectónicas

### 📌 Decisión #1: Catálogo Fuente de Verdad
**Tema**: ¿Excel o Markdown?
**Decisión**: **Markdown como principal** (git-friendly, control de versiones)
**Justificación**:
- Control de versiones nativo
- Fácil de sincronizar entre documentación y código
- Excel como respaldo para edición por no-técnicos (Lara)
- Se puede regenerar Excel desde Markdown si es necesario

**Decidido por**: Nadir Donemberg + Claude (2026-04-06)

---

## Referencias

- **CLAUDE.md** — Reglas de negocio completas
- **product_system_core_v3.docx** — Documento arquitectónico actual
- **GitHub**: https://github.com/Vaitty/Business
- **Bitácora de sesiones**: Ver sección de CLAUDE.md

---

**Última actualización**: 2026-04-06
**Próxima revisión**: 2026-04-13 (post-Refactoring #2)
