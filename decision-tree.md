# Árbol de decisión de artefactos

Empieza por la necesidad, no por una feature del cliente.

## ¿Hace falta automatizar?

No automatices todavía si la tarea es infrecuente y barata, el proceso cambia
constantemente, no existe fuente de verdad, no puede verificarse o el riesgo
supera el beneficio.

## ¿Cuál es el rol y cómo valida?

Confirma rol, entregables y evidencia de “listo” antes de elegir artefactos.
Lee [roles.md](roles.md). No uses validación de un rol para diseñar el de otro.

## ¿Qué mantiene el usuario?

Confirma primero temas, frecuencia, riesgo, owner y señales. Sin ese mapa no
priorices ni propongas taxonomías.

## ¿El sistema elegirá o clasificará?

El usuario debe aprobar valores, acciones, definiciones, exclusiones,
precedencia, fallback y gates. Un LLM puede proponer la política, no
establecerla.

## ¿El trabajo es determinístico?

Si la misma entrada debe producir la misma salida:

- SQL/API para consultar datos estructurados;
- script o test harness para transformar, validar o comparar;
- hook para aplicar una política ante un evento;
- pipeline/plan de infra o checks de schema cuando el rol los use.

Usa LLM para interpretación o excepciones ambiguas dentro de la política.

## ¿Necesita conversación?

Usa skill si el usuario investiga casos, aporta contexto o decide durante el
proceso. Si hay procesamiento masivo y consulta ad hoc, separa pipeline y skill.

## Matriz

| Necesidad | Artefacto |
|-----------|-----------|
| Convención persistente | Rule/instruction |
| Workflow temático | Skill |
| Investigación especializada | Subagente |
| Operación repetible | Script |
| Política por evento | Hook |
| Tarea recurrente | Automation/scheduled job |
| Sistema externo | MCP/API |
| Datos estructurados | SQL/query service |
| Preferencia del editor | Settings |

## Skill vs subagente

La skill coordina. El subagente ejecuta una tarea acotada.

```text
Skill: trigger → contexto → rama → delegación → validación → handoff
Subagente: objetivo + alcance + fuentes + restricciones + salida
```

Usa subagente si requiere exploración amplia, especialización, paralelismo o
aislamiento de contexto. No lo uses para una búsqueda puntual ni para delegar el
problema completo.

## Script/test vs LLM

| Trabajo | Preferencia |
|---------|------------|
| Contar, validar esquema o comparar snapshots | Script/query |
| Correr suite, visual diff o plan de infra | Harness/script/CI |
| Aplicar regla exacta | Script |
| Clasificar texto ambiguo | LLM + política + fallback |
| Explicar causa probable | LLM citando evidencia |
| Juzgar UX o accesibilidad ambigua | Humano + checklist; LLM solo apoyo |
| Proponer taxonomía | LLM + decisión humana |

## Hook vs automatización

Hook: evento local, rápido y determinístico.

Automatización: horario o evento externo, workflow más largo, owner, permisos y
canal de entrega.

## MCP/API

Úsalo cuando la fuente viva en otro sistema y las copias locales generen
desactualización. Define lectura/escritura, auth, secretos, rate limits,
sandbox, confirmación y fallback.

## Preguntas de control

1. ¿El diseño respeta el rol y su forma de validar?
2. ¿Una consulta, test o checklist resuelve esto sin LLM?
3. ¿Una regla breve evita crear una skill?
4. ¿El subagente tiene una tarea aislable?
5. ¿La automatización tiene trigger y owner?
6. ¿El sistema externo necesita escritura?
7. ¿Cada pieza tiene criterio de término con evidencia del rol?
8. ¿Puede empezar con un piloto menor?
9. ¿El mapa de temas fue confirmado?
10. ¿Las decisiones fueron aprobadas?
11. ¿El historial permite reproducir versiones anteriores?
