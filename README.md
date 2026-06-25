# cerberus-contracts

Repositorio de contratos de mensajería del sistema Cerberus.

Contiene los JSON Schemas que definen la estructura exacta de todos los mensajes
que viajan entre microservicios por RabbitMQ. Ningún servicio puede definir
sus propios formatos — todos deben adherirse a los contratos aquí versionados.

---

## Estructura

```
schemas/
  v1/
    scan-request.schema.json    ← SecurityGate → servicios de análisis
    scan-result.schema.json     ← Servicios de análisis → SecurityGate
    scan-verdict.schema.json    ← SecurityGate → Frontend y ML
examples/
    scan-request.example.json
    scan-result.example.json
    scan-result-timeout.example.json
    scan-verdict.example.json
```

---

## Flujo de mensajes

```
GitHub webhook
      │
      ▼
SecurityGate ──[scan-request]──► VulnerabilityService
             ──[scan-request]──► CodeQualityService

VulnerabilityService ──[scan-result]──► SecurityGate
CodeQualityService   ──[scan-result]──► SecurityGate

SecurityGate (consolida)
      │
      ├──[scan-verdict]──► Frontend
      └──[scan-verdict]──► Servicio ML
```

---

## Reglas del veredicto final

| Condición | Veredicto |
|---|---|
| `critical > 0` ó `high > 0` | `fail` |
| `critical == 0` y `high == 0` y (`medium > 0` ó `low > 0`) | `warning` |
| Todos en 0 (solo puede haber `info`) | `pass` |

El rollback en Kubernetes solo se activa cuando `verdict == "fail"`.

---

## Versiones

| Tag | Estado | Fecha |
|---|---|---|
| v1.0.0 | Activo | [completar al hacer merge] |

---

## Convenciones de filePath por herramienta

Cuando el hallazgo no proviene de un archivo del repositorio, usar estas convenciones
de string para el campo `filePath`:

| Herramienta | Formato | Ejemplo |
|---|---|---|
| Gitleaks | ruta real del archivo | `src/Services/StorageService.cs` |
| Trivy filesystem | ruta real del archivo | `package.json` |
| Trivy contenedor | `container:{imagen}/{paquete}` | `container:ubuntu:22.04/libssl` |

---

## Regla de modificación

Los schemas bajo `schemas/v1/` son **INAMOVIBLES** tras el congelamiento del día 2.

Cualquier cambio posterior requiere:
1. Aprobación de Ximena Jaramillo Cárdenas (líder técnico)
2. Nuevo tag semántico (`v1.1.0` para cambios compatibles, `v2.0.0` para breaking changes)
3. Comunicación al equipo completo antes de hacer merge

---

## Quién usa qué

| Desarrollador | Servicio | Lee |
|---|---|---|
| Ximena / Camilo | SecurityGate | scan-request (envía), scan-result (recibe), scan-verdict (envía) |
| Luis Miguel | VulnerabilityService | scan-request (recibe), scan-result (envía) |
| Juan José | CodeQualityService | scan-request (recibe), scan-result (envía) |
| Faiber | Frontend | scan-verdict (recibe) |
| Miguel Ángel | Servicio ML | scan-verdict (recibe) |
