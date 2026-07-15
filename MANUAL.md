# Manual para diseñar workflows agénticos

Este manual explica cómo convertir trabajo repetitivo de desarrollo en un
workflow asistido por agentes. Parte del proceso humano, no de una herramienta.

## 1. Contexto antes que solución

Describe:

1. rol y cómo valida;
2. actor y disparador;
3. entradas y fuentes;
4. pasos actuales;
5. temas o errores que mantiene la persona;
6. decisiones humanas;
7. resultado;
8. evidencia de término;
9. fricciones;
10. evidencia necesaria para auditoría.

Prompt inicial:

```text
Soy [rol: backend/frontend/QA/DevOps/data/...].
Trabajo en [equipo/producto] y hacemos este proceso:
1. [Actor] recibe [entrada].
2. Revisa [señales].
3. Decide [criterio].
4. Ejecuta [acción].
5. Verifica mediante [evidencia típica de mi rol].

Los temas o errores que mantengo son:
- [tema, frecuencia, riesgo, owner, dónde revisar]

Quiero diseñar un workflow para [objetivo].
No implementes todavía. Adapta el diseño a mi rol, reconstruye el proceso,
inventaria mis temas, separa hechos de inferencias, propone el esqueleto mínimo
y pregúntame las decisiones que cambien el diseño.
```

## 2. Construir contexto por capas

### Rol

Antes del proceso, fija el perfil: entregables, evidencia de “listo”, entornos
y validaciones que dependen de otros. Un workflow de frontend no se valida como
uno de backend. Consulta `roles.md`.

### Proceso

Mapea actores, entradas, salidas y validación propia del rol.

### Ownership

Inventaría un mapa —confirmado por el usuario— de temas, frecuencia, riesgo, owner,
señales y lugares donde investigar. No confundas problemas del proceso con los
temas que la persona mantiene.

### Conocimiento

Registra síntomas, vocabulario, hipótesis y reglas. Una hipótesis no es hecho
hasta ser validada.

### Fuentes

Clasifica cada fuente como verdad, snapshot, catálogo, evidencia, derivado o
ruido. Registra frescura e identificadores.

### Esqueleto

Separa ingestión, normalización, interfaz canónica, análisis, reproducción,
cambio y verificación solo cuando sean necesarias.

### Política

Antes de automatizar decisiones, el usuario define categorías, ejemplos,
precedencia, fallback, gates y owner.

### Auditoría

Define versiones, IDs, evidencia, aprobaciones, validación y rollback.

## 3. Elegir el artefacto

| Necesidad | Artefacto |
|-----------|-----------|
| Convención breve y persistente | Regla/instruction |
| Workflow temático | Skill |
| Investigación aislada | Subagente |
| Operación determinística | Script/query |
| Política ante evento | Hook |
| Tarea periódica | Automatización |
| Sistema externo | MCP/API |

Una skill es atómica por tema, no por instrucción. Un subagente recibe una tarea
acotada; el agente principal conserva decisiones y síntesis.

## 4. Investigación sin alucinaciones

Nunca describas una función por su nombre. Contrasta implementación, callers,
tests, documentación, tipos, configuración y runtime.

Todo hallazgo distingue:

- evidencia;
- inferencia;
- decisión humana;
- pendiente.

Admite “no verificable”. Pausa si la incertidumbre cambia permisos, límites,
fuente de verdad, efectos o validación.

## 5. Decisiones gobernadas

Clasificar no es inferencia libre. Los valores deben estar aprobados.

```yaml
policy:
  owner: team-owner
  version: 1
  allowed_values: []
  precedence: []
  fallback:
    value: pending_review
    requires_human: true
```

Un patrón nuevo no crea una categoría. Se usa el fallback y se presenta la
propuesta al owner.

## 6. Correcciones que contradicen reglas

Cuando una corrección choque con texto persistente:

1. cita archivo y regla;
2. explica el impacto;
3. ofrece mantener, exceptuar o actualizar;
4. muestra el cambio antes de escribir;
5. registra alcance, versión y validación.

## 7. Historial

Git conserva diffs. El changelog explica intención:

```text
Versión/fecha:
Owner:
Motivo:
Decisión:
Antes/después:
Artefactos:
Validación:
Rollback:
```

Cada ejecución relevante registra versión de workflow/política, input,
decisión, evidencia, intervención humana, efectos, validación y timestamp.

## 8. Criterios de término

Evita “analiza y arregla”. Usa resultados observables del rol:

- backend: test, contrato, log/trace, dry-run, migración reversible;
- frontend/mobile: preview, visual diff, a11y, device matrix, E2E;
- QA: caso reproducible, retest fail→pass, matriz de entornos;
- DevOps: plan/diff, pipeline, smoke, rollback;
- data: schema, conteos, query reproducible, métrica en rango;
- comunes: reporte con fuentes, fallback aplicado, versiones registradas.

## 9. Activación contextual

Una buena descripción permite activar la skill por intención. No debe ser
agresiva:

- activa ante una petición inequívoca;
- pregunta si puede ser puntual o persistente;
- prioriza una skill más específica;
- no ofrece automatización ante cada tarea trivial.

## 10. Principios

1. Contexto antes que código.
2. Proceso antes que herramienta.
3. El rol define cómo se valida.
4. Skills por tema.
5. Subagentes con alcance.
6. Scripts/tests para lo determinístico.
7. Evidencia antes que inferencia.
8. Decisiones definidas por el usuario.
9. Fallback ante ambigüedad.
10. Cambios auditables.
11. El setup se adapta a la persona, no al revés.
