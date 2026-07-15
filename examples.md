# Ejemplos de adaptación

## 1. Backend: triage de incidentes

Rol: backend. Valida con tests de integración, logs/traces y dry-run de
efectos.

Mapa:

| Tema | Frecuencia | Owner | Piloto |
|------|------------|-------|--------|
| Timeouts de API | alta | usuario | sí |
| Fallas de auth | alta | usuario | sí |
| Race conditions | media | usuario | sí |
| Observabilidad | baja | otro equipo | no |

Setup: pipeline de normalización, taxonomía aprobada, skill de análisis, skill de
fix, harness de reproducción y changelog.

No crear una única skill que relea todas las fuentes en cada consulta.

## 2. Frontend: regresiones de UI

Rol: frontend. Valida con preview, visual diff, checklist a11y y E2E del flujo
crítico.

Mapa: estados de formulario, layout responsive, accesibilidad de modales.

Setup: skill de reproducción del síntoma, script/harness de Storybook o preview,
checklist a11y versionada y criterio de término con screenshot/diff.

No proponer SQL ni payload dry-run como evidencia principal.

## 3. QA: suite de regresión

Rol: QA. Valida con casos reproducibles, matriz de entornos y retest
fail→pass.

Setup: skill para convertir un reporte en caso, plantilla de evidencia,
taxonomía de severidad aprobada y registro de versión del build bajo prueba.

No implementar fixes; el término es evidencia de retest, no merge de código.

## 4. DevOps: cambios de infra

Rol: DevOps/SRE. Valida con `plan`/diff, pipeline, smoke post-deploy y
rollback.

Setup: skill de review de cambios, hook o script de plan dry-run, runbook de
rollback y evento de auditoría con versión de config.

No recomendar Storybook ni contract tests de API como gate principal.

## 5. Data: pipeline semanal

Rol: data/analytics. Valida con schema checks, conteos, rangos y query
reproducible.

Setup: SQL/query versionada, script de calidad de datos y job programado.

No crear skill conversacional ni subagente si el trabajo es determinístico.

## 6. Revisión de PR/MR

Contexto: pocos cambios por semana, criterios escritos y CI existente. El rol
define qué evidencia exige el review.

Setup: skill coordinadora, subagente de estándares y subagente de spec.

No duplicar CI, editar durante la revisión ni mezclar limpieza de ramas con
arquitectura.

## 7. Corrección que contradice una regla

Regla:

```text
No aprobar un release si faltan pruebas de integración.
```

El usuario pide aprobarlo sin pruebas. La respuesta:

1. cita archivo y regla;
2. explica el impacto;
3. pregunta mantener, exceptuar o actualizar;
4. no modifica antes de la elección;
5. registra alcance e historial.

## 8. Activación contextual ambigua

Usuario:

```text
Otra vez tuve que revisar manualmente todos estos reportes.
```

Respuesta:

```text
Puedo ayudarte con esta revisión puntual o analizar si conviene convertirla en
un workflow reutilizable. ¿Qué prefieres?
```

No iniciar la entrevista hasta que el usuario elija.

## 9. Nueva clasificación descubierta

El agente detecta un patrón no cubierto.

Comportamiento esperado:

1. usar el fallback aprobado;
2. mostrar evidencia;
3. proponer la categoría como borrador;
4. pedir decisión al owner;
5. definir precedencia si se aprueba;
6. incrementar versión;
7. validar casos anteriores y nuevos.

Nunca crear el label automáticamente.

## 10. Sesgo de rol incorrecto

Usuario: frontend.

Comportamiento incorrecto: proponer queries SQL y dry-run de payload como
criterio de término.

Comportamiento esperado: preguntar rol y evidencia; usar preview, visual diff,
a11y o E2E según lo que el usuario confirme.

## 11. Investigación de código ambigua

Tests y documentación describen comportamientos distintos. El subagente
devuelve:

```text
Pregunta:
Por qué importa:
Evidencia contradictoria:
Opciones observables:
Recomendación:
```

El agente principal pregunta al usuario y luego reanuda la investigación.

## Señales de un diseño impuesto

- recomienda tecnologías no mencionadas;
- impone validación de backend a otros roles;
- propone siempre skill más subagente;
- enumera features en lugar de resolver fricciones;
- omite el mapa de ownership;
- inventa categorías;
- crea archivos antes de aprobar;
- descarta scripts, tests visuales o “no automatizar” sin evaluarlos;
- convierte un caso particular en convención general.
