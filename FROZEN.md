# CONTRATOS CONGELADOS — v1.1.0

> Este archivo registra el congelamiento y la gobernanza de cada versión de los contratos.

Versión activa: v1.1.0
Tag: v1.1.0

## Regla de oro

Estos schemas son INAMOVIBLES. Cualquier modificación requiere aprobación del
líder técnico, nuevo tag semántico y comunicación al equipo completo antes del merge.

---

## v1.1.0 (activa)

Fecha de congelamiento: 2026-06-30
Tag: v1.1.0
Tipo de cambio: compatible (minor)

Aprobación de la líder técnica: [x] Ximena Jaramillo Cárdenas — fecha: 2026-06-30

### Cambios respecto de v1.0.0

- `scan-result`: el campo `filePath` de cada finding pasa a ser **opcional**
  (ya no está en `required`), para admitir hallazgos que no provienen de un
  archivo del repositorio.
- `scan-result`: se agrega el campo `locationUrl` (`format: uri`) en los findings,
  para registrar la URL donde herramientas DAST (ZAP) detectan la vulnerabilidad.
  En prosa se documenta como mutuamente excluyente con `filePath` (aún no impuesto
  por el schema — ver decisión pendiente en CHANGELOG / issue de gobernanza).
- Nuevo ejemplo `examples/scan-result-dast.example.json`.

### Confirmación del equipo — v1.1.0

Cada integrante confirma que la v1.1.0 sigue cubriendo los campos que su servicio necesita:

- [ ] Ximena Jaramillo Cárdenas — SecurityGate
- [ ] Camilo Florez Moreno — Infraestructura / SecurityGate   ← PENDIENTE
- [ ] Luis Miguel González — VulnerabilityService
- [ ] Juan José Cadena — CodeQualityService
- [ ] Faiber Camacho — Frontend                                ← PENDIENTE
- [ ] Miguel Ángel — Servicio ML                               ← PENDIENTE

> Confirmaciones que faltan explícitamente antes de dar por cerrada la v1.1.0:
> **Camilo Florez, Faiber Camacho y Miguel Ángel.**
> No marcar en nombre de otra persona: cada integrante marca su propia casilla.

---

## v1.0.0 (reemplazada por v1.1.0)

Fecha de congelamiento: _______________
Tag: v1.0.0
Aprobado por: Ximena Jaramillo Cárdenas

### Confirmación del equipo — v1.0.0

- [x] Ximena Jaramillo Cárdenas — SecurityGate
- [ ] Camilo Florez Moreno — Infraestructura / SecurityGate
- [x] Luis Miguel González — VulnerabilityService
- [x] Juan José Cadena — CodeQualityService
- [ ] Faiber Camacho — Frontend
- [ ] Miguel Ángel — Servicio ML
