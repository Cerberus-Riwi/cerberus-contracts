# Changelog

Todos los cambios relevantes de los contratos de `cerberus-contracts`.
El versionado sigue [SemVer](https://semver.org/lang/es/): `MAJOR.MINOR.PATCH`.

- **MINOR**: cambios compatibles hacia atrás (campos nuevos opcionales, relajar `required`).
- **MAJOR**: cambios incompatibles (campos nuevos obligatorios, renombres, borrados).

---

## [v1.1.0] — AAAA-MM-DD

Cambio compatible. Formaliza el ajuste de `scan-result` que ya estaba en `main`
para soportar hallazgos DAST (ZAP).

### Changed
- `scan-result.schema.json`: `filePath` deja de ser obligatorio en cada finding
  (removido de `required`). Los hallazgos que no provienen de un archivo del
  repositorio ya no necesitan un `filePath` ficticio.

### Added
- `scan-result.schema.json`: nuevo campo opcional `locationUrl` (`format: uri`)
  en los findings, para la URL donde una herramienta DAST detecta la vulnerabilidad.
  Documentado en prosa como mutuamente excluyente con `filePath` (la exclusión
  aún no está impuesta por el schema — pendiente de decisión `oneOf`/`anyOf`).
- `examples/scan-result-dast.example.json`: ejemplo de un `scan-result` con
  findings de ZAP que usan `locationUrl` y no tienen `filePath`.

### Fixed
- Renombrado del schema `scan-request.schema (2).json` → `scan-request.schema.json`
  (artefacto de copia de Windows). El README y el `$ref` ya apuntaban al nombre
  canónico, que ahora existe.

---

## [v1.0.0] — AAAA-MM-DD

Versión inicial congelada de los contratos de mensajería sobre RabbitMQ.

### Added
- `scan-request.schema.json`: mensaje SecurityGate → servicios de análisis.
- `scan-result.schema.json`: mensaje servicios de análisis → SecurityGate.
- `scan-verdict.schema.json`: veredicto SecurityGate → Frontend y Servicio ML.
- Ejemplos: `scan-request`, `scan-result`, `scan-result-timeout`, `scan-verdict`.
