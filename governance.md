# Gobernanza de decisiones e historial

## Política definida por el usuario

Un agente no debe inventar en producción categorías, severidades, estados,
prioridades, aprobaciones, routing, acciones ni umbrales.

Puede proponer un borrador. El usuario debe aprobarlo antes de implementar.

```yaml
policy:
  name: error-classification
  owner: platform-team
  version: 1
  allowed_values:
    - id: api_timeout
      label: Timeout de API
      definition: La llamada externa supera el umbral o no responde.
      positive_examples: []
      negative_examples: []
  precedence:
    - exact_rule_before_semantic_inference
  fallback:
    value: pending_review
    requires_human: true
```

La política parte del mapa de temas que mantiene el usuario. Temas ajenos o
fuera del piloto no entran en la taxonomía activa.

## Preguntas obligatorias

1. ¿Qué valores están permitidos?
2. ¿Qué incluye y excluye cada uno?
3. ¿Puede haber varios?
4. ¿Qué precedencia aplica?
5. ¿Qué ocurre sin evidencia suficiente?
6. ¿Qué exige revisión humana?
7. ¿Quién puede cambiar la política?
8. ¿Cómo se versiona y valida?

## Reglas para el agente

- No crear categorías por observar un patrón.
- No forzar un caso al label más cercano.
- Usar el fallback aprobado.
- Conservar evidencia.
- Registrar versión y resultado.
- Separar propuesta y aprobación.
- Activar el protocolo de conflicto ante contradicciones textuales.

## Versionamiento proporcional

| Artefacto | Recomendación |
|-----------|---------------|
| Skill, regla, agente o script | Git + changelog si cambia comportamiento |
| Taxonomía o política | Versión explícita + fixtures |
| Dataset | Fecha, versión de esquema y snapshot/hash |
| Prompt crítico | Versión o hash por ejecución |
| Test/scenario | Git + referencia al bug |
| Integración | Versión de API/config y despliegue |

No agregues metadatos que el cliente no soporte. Guarda la versión en un
archivo de gobernanza o changelog cuando el formato no la admita.

## Entrada de historial

```markdown
## [versión o fecha] — [título]

- Actor/owner:
- Motivo:
- Evidencia o bug:
- Decisión aprobada:
- Antes:
- Después:
- Artefactos afectados:
- Política/dataset/prompt:
- Validación:
- Excepciones:
- Rollback:
```

El changelog explica intención y comportamiento; Git conserva el diff.

## Evento de ejecución

```json
{
  "run_id": "stable-id",
  "workflow_version": "2",
  "policy_version": "4",
  "input_ref": "incident-123",
  "decision": "pending_review",
  "evidence_refs": ["issue:123", "trace:abc"],
  "human_approval": null,
  "effects": [],
  "validation": "passed",
  "timestamp": "ISO-8601"
}
```

No registres secretos ni datos personales innecesarios.

## Cuándo crear versión

Sí:

- categorías o decisiones;
- precedencia o fallback;
- fuentes de verdad;
- efectos externos;
- gates;
- contrato de entrada/salida.

Normalmente no:

- ortografía;
- aclaración sin cambio de regla;
- refactor interno con el mismo contrato.

El usuario/equipo elige semver, entero o fecha.

## Validación

1. Revisar casos representativos, negativos y ambiguos.
2. Comparar versión anterior y nueva.
3. Explicar cambios esperados e inesperados.
4. Obtener aprobación del owner.
5. Registrar validación y rollback.
