# Contratos — Datos Legales y T&Cs

**Estado**: [VIGENTE]

---

## 🏢 Datos Legales de Vaitty

| Campo | Valor |
|-------|-------|
| **Razón social** | FAST HOME SERVICES S.A.S |
| **CUIT** | 30-71516755-3 |
| **Domicilio** | Boulevard del Bicentenario de la Independencia Nacional N° 35, Oficina 8, Córdoba |
| **Matrícula** | 14973-A |
| **Cuenta Corriente** | CC Pesos N° 0020850-3 138-5 |
| **CBU** | 0070138520000020850353 |
| **Banco** | Galicia |

---

## 📄 Estructura de Contrato Tipo

El contrato base (TYC- SANCOR BANCOR 25112025.docx) tiene esta estructura:

### Carta Oferta
- Firmada por Nadir Donemberg (CEO)
- Fecha y datos del partner
- Resumen ejecutivo del producto

### Anexo A — Cláusulas del Acuerdo
- **Objeto**: Qué es el servicio
- **Actuación**: Cómo Vaitty actúa
- **Plataforma**: Canales tecnológicos disponibles
- **Precio**: Modelo de cotización
- **Vigencia**: Duración del acuerdo
- **Resolución**: Cómo se termina

### Anexo I — Términos y Condiciones Específicos
- Servicios incluidos por vertical
- Coberturas (montos, límites, exclusiones)
- Forma de prestación (directa/reintegro)
- SLAs
- Condiciones operativas

### Anexo II — Módulos y Condiciones de Plataforma
- Canales tecnológicos habilitados (WhatsApp, Portal, API)
- Integración con sistemas del partner
- Soporte y mantenimiento
- Seguridad y confidencialidad

### Anexo III — Precio y Liquidación
- Precio per cápita (si Bundle) o precio por unidad (Stand-alone)
- Modelo de facturación (mensual, anual, por evento)
- Forma de pago
- Períodos de gracia (si aplica)
- Comisión del canal (si stand-alone)

---

## 🔄 Proceso de Contratación

### 1. Diseño del Producto (Con Mati Caballero)
- Partner y Vaitty definen juntos el paquete
- Se documenta en "Propuesta Comercial"

### 2. Cotización Interna
- Nadir + Lara aprueban el precio
- Se genera "Análisis Económico"

### 3. Redacción de T&Cs
- Se adapta el contrato base (TYC- SANCOR BANCOR)
- Se personaliza para el partner específico
- Se incluyen Anexos I, II, III con datos del producto

### 4. Aprobación Legal
- Revisión interna de T&Cs
- Validación de exclusiones y cláusulas
- Firma de Nadir

### 5. Firma del Partner
- Partner revisa y firma
- Se archiva en `/docs/_CONTRATOS/ACTIVOS/[PARTNER]/`

### 6. Inicio de Operaciones
- Partner comienza a ofertar el producto
- Vaitty habilita canales y prestadores

---

## 📚 Tipos de Modificaciones (Addendas)

Cuando se agregan productos nuevos a un partner existente:

1. **Addenda**: Documento adicional que modifica/extiende el contrato original
2. **Mantiene estructura**: Usa mismos Anexos A, II
3. **Producto específico**: Nuevo Anexo I + Anexo III (precio)
4. **Ejemplo**: BBVA firma Hogar (2024) → Addenda Mascotas (2024-Q2)

---

## 🗂️ Organización de Contratos

### En Disco Local
```
docs/_CONTRATOS/
├── ACTIVOS/
│   ├── Qualia/
│   ├── BBVA/
│   ├── Galicia/
│   └── ...
├── HISTORICO/
│   ├── Contratos_Viejos/
│   └── Versiones_Previas/
└── MODELOS/
    ├── TYC- SANCOR BANCOR 25112025.docx
    ├── Anexo I - Hogar.docx
    ├── Anexo I - Mascotas.docx
    └── ...
```

### En GitHub
```
Business/ (repo público)
├── CONTRATOS/ (referencia)
│   └── Enlace a documentos legales
└── (No subir documentos originales — confidencial)
```

---

## ⚠️ Confidencialidad

**Datos que NO se publican** en GitHub:
- Contratos originales firmados
- T&Cs con datos específicos de partner
- Precios y comisiones
- Información financiera sensible
- Datos de beneficiarios

**Referencia pública permitida**:
- Estructura tipo de contrato
- Anexos genéricos sin datos
- Procesos (no archivos)

---

## 📋 Checklist de Contrato Nuevo

- [ ] ¿Producto bien definido (Anexo I)?
- [ ] ¿Precio aprobado por Nadir/Lara?
- [ ] ¿Canales tecnológicos habilitados?
- [ ] ¿Prestadores asignados?
- [ ] ¿T&Cs personalizadas?
- [ ] ¿Exclusiones documentadas?
- [ ] ¿SLAs confirmados?
- [ ] ¿Firma de ambas partes?
- [ ] ¿Archivado en /ACTIVOS/[PARTNER]/?
- [ ] ¿Notificado a operaciones?

---

**Última actualización**: 2026-04-06
**Archivo base**: `docs/_CONTRATOS/MODELOS/TYC- SANCOR BANCOR 25112025.docx`
**Ver también**: OPERATIVO.md (exclusiones), PRODUCTOS.md (coberturas)
