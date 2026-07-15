# Plantilla de handoff

Presenta esta salida en el chat. No la escribas a disco sin aprobación.

````markdown
# Setup agéntico propuesto: [nombre]

## Objetivo
[Resultado de negocio.]

## Rol y validación
- Rol principal:
- Roles secundarios:
- Entregables habituales:
- Evidencia de “listo”:
- Entornos permitidos:
- Validaciones en CI vs manuales:
- Dependencias de otros roles:

## Proceso actual confirmado
Cuando [trigger], [actor] recibe [entrada], hace [pasos], decide [decisiones],
produce [salida] y valida mediante [evidencia del rol].

## Temas que mantiene
| Tema/error | Frecuencia | Riesgo | Owner | Señales | Dónde revisar | Piloto |
|------------|------------|--------|-------|---------|---------------|--------|
| [...] | [...] | [...] | [...] | [...] | [...] | sí/no |

## Evidencia utilizada
- [Evidencia] [fuente y frescura]
- [Decisión del usuario]
- [Inferencia] [razón y confianza]

## Fricciones priorizadas
1. [Fricción ligada a tema, coste y riesgo]

## Setup mínimo
| Pieza | Responsabilidad | Por qué | Entrada | Salida | Término (evidencia del rol) |
|-------|-----------------|---------|---------|--------|-----------------------------|
| [...] | [...] | [...] | [...] | [...] | [...] |

## Flujo
[Pasos o diagrama pequeño.]

## Decisiones humanas y guardrails
- [Acción]: requiere [aprobación/evidencia].
- [Efecto externo]: [dry-run/confirmación/rollback].

## Política aprobada
- Owner:
- Versión:
- Valores permitidos:
- Definiciones y exclusiones:
- Precedencia:
- Fallback:
- Gates:
- Evidencia de aprobación:

## Delegaciones
### [Subagente]
- Objetivo:
- Alcance:
- Fuentes:
- No hacer:
- Salida:
- Término:

## Fuera de alcance
- [...]

## Alternativas
- [Alternativa, cuándo sería mejor, por qué no ahora.]

## Conflictos con reglas
- Fuente y texto:
- Corrección:
- Decisión: mantener / excepción / actualizar
- Alcance:

## Versionamiento
- Convención:
- Artefactos:
- Changelog:
- Cambios que crean versión:
- Evento por ejecución:
- Owner:
- Validación:
- Rollback:

## Riesgos y supuestos
- [...]

## Piloto
1. [Caso.]
2. [Validación.]
3. [Condición para escalar.]

## Siguiente paso
[Una acción.]

## Prompt para implementar
```text
[Prompt autocontenido.]
```
````

## Reglas de calidad

- No listar capacidades no relacionadas.
- Separar hechos, inferencias y decisiones.
- No proponer más piezas de las necesarias.
- No imponer validación de un rol a otro.
- Vincular cada fricción con un tema y evidencia del rol.
- No inventar ownership ni taxonomías.
- No implementar decisiones sin política y fallback.
- Vincular cambios de comportamiento con motivo, aprobación y validación.
