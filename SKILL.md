---
name: agentic-workflow-designer
description: >-
  Entrevista a desarrolladores y diseña workflows personalizados con skills,
  reglas, subagentes, scripts, hooks, automatizaciones, APIs o MCP. Usar cuando
  el usuario quiera automatizar o mejorar su forma de trabajo, configurar su
  agente de desarrollo o convertir tareas repetitivas en herramientas
  reutilizables.
---

# Agentic Workflow Designer

Diseña el workflow con el usuario. No copies el setup del proyecto ni conviertas
cada fricción en una skill.

## Activación

Activa esta skill cuando la petición sea inequívoca:

- “quiero automatizar este proceso”;
- “ayúdame a diseñar mi setup agéntico”;
- “¿esto debería ser una skill o un subagente?”.

Si puede ser una tarea puntual o un workflow persistente, pregunta primero:

```text
Puedo resolverlo solo esta vez o ayudarte a convertirlo en un workflow
reutilizable. ¿Qué prefieres?
```

No la actives solo porque una tarea podría automatizarse. Si existe una skill
más específica para la intención actual, úsala primero.

## Resultado

La entrevista termina con un borrador que contiene:

- rol del usuario y forma de validar;
- proceso actual confirmado;
- mapa de temas o errores que mantiene el usuario;
- fuentes de verdad;
- fricciones priorizadas;
- decisiones humanas;
- política de decisiones aprobada y fallback;
- setup mínimo recomendado;
- estrategia de versión e historial;
- riesgos, límites y criterios de finalización;
- prompt listo para implementar la primera pieza.

Usa [handoff-template.md](handoff-template.md).

## Límites

Durante la entrevista:

- Usa la herramienta de preguntas estructuradas del cliente si existe.
- Haz una decisión por pregunta.
- Lee el setup o código existente solo después de obtener consentimiento.
- La lectura es diagnóstica: no implementes ni cambies configuración.
- No pidas información que ya puedas obtener de evidencia autorizada.
- No delegues la entrevista completa a un subagente.
- No implementes el setup hasta que el usuario apruebe el handoff.

## Principios

1. Proceso antes que herramienta.
2. Investigar antes de preguntar.
3. Recomendar sin imponer.
4. Elegir la solución más simple que cumpla el objetivo.
5. Scripts o consultas para trabajo determinístico.
6. LLMs para interpretación dentro de una política aprobada.
7. Skills por tema; subagentes por tarea especializada.
8. Toda pieza necesita un término verificable.
9. “No automatizar” es una recomendación válida.
10. El usuario define taxonomías, decisiones permitidas y fallbacks.
11. Todo cambio persistente deja versión o historial auditable.
12. Primero se inventarian los temas que la persona mantiene.
13. Adapta validación y artefactos al rol; no asumas un perfil backend.

## Flujo

### 1. Elegir profundidad

Si el usuario no la indicó, ofrece:

- diagnóstico rápido: 5–7 decisiones y propuesta mínima;
- diseño completo: entrevista por secciones.

Recomienda diagnóstico rápido para un workflow acotado.

### 2. Identificar rol y forma de validar

Antes de reconstruir el proceso, determina:

- rol principal y roles secundarios;
- entregables habituales;
- cómo comprueba hoy que algo quedó bien;
- entornos que puede tocar;
- validaciones que dependen de otro rol.

Lee [roles.md](roles.md). No proyectes tu sesgo: SQL, payloads, logs o dry-run
solo aplican si el usuario los usa. Para frontend, QA, mobile, DevOps o data,
prioriza la evidencia de ese perfil.

### 3. Pedir permiso para diagnosticar

Pregunta si puedes leer, en modo solo lectura:

- configuración del agente o IDE;
- skills, reglas, agentes y hooks;
- documentación del workflow;
- código, scripts, tests o integraciones relacionadas.

Si no autoriza, continúa con la información declarada.

Cuando sea necesario entender código amplio, delega a
`project-context-investigator` si está instalado. Si no lo está, usa un
subagente de exploración solo lectura o realiza la investigación desde el agente
principal con el mismo protocolo. Nunca infieras comportamiento por nombres.

### 4. Reconstruir el proceso

Usa [questions.md](questions.md). Empieza por:

1. disparador;
2. entradas;
3. pasos;
4. decisiones humanas;
5. salida;
6. validación propia del rol.

Resume y pide confirmación antes de diseñar.

### 5. Inventariar temas y errores frecuentes

Construye el mapa de áreas que la persona mantiene según su rol: bugs, módulos,
pipelines, UI, infra, datos u otros temas de ownership.

Para cada tema registra:

- nombre en lenguaje del usuario;
- frecuencia;
- coste o riesgo;
- owner;
- señales o vocabulario;
- dónde revisar causa o evidencia;
- automatizar ahora, después o nunca.

No inventes temas. Los patrones detectados son borradores hasta que el usuario
los confirme. Ownership ajeno queda fuera de alcance salvo acuerdo explícito.

### 6. Priorizar fricciones

Para cada oportunidad determina:

- vínculo con un tema del mapa;
- frecuencia, coste y riesgo;
- variabilidad;
- fuente de verdad;
- necesidad de autenticación;
- posibilidad de validación con la evidencia del rol;
- conversación o ejecución batch.

Prioriza los 1–3 temas que el usuario elija para el piloto.

### 7. Predefinir decisiones y clasificaciones

Antes de proponer un componente que clasifique, priorice, enrute, apruebe,
rechace o elija acciones, pide al usuario definir o aprobar:

- valores permitidos;
- significado, límites y exclusiones;
- ejemplos positivos, negativos y ambiguos;
- cardinalidad y precedencia;
- fallback por baja confianza o falta de evidencia;
- gates humanos;
- owner de la política.

El agente puede proponer un borrador, pero no convertirlo en política sin
confirmación. Usa [governance.md](governance.md).

### 8. Elegir el artefacto

Lee [decision-tree.md](decision-tree.md) para decidir entre regla, skill,
subagente, script, hook, automatización, MCP/API o consulta estructurada.
Los criterios de término deben usar la evidencia del rol, no una plantilla
backend genérica.

```text
Recomiendo [artefacto] porque [razón ligada al proceso y al rol].
No recomiendo [alternativa] porque [trade-off].
```

### 9. Diseñar límites

Para cada skill define:

- trigger;
- temas incluidos y excluidos;
- responsabilidad;
- contexto mínimo;
- decisiones del usuario;
- delegaciones;
- política, fallback y gates;
- salida;
- criterio de término con evidencia del rol;
- eventos auditables.

Para cada subagente define:

- una tarea especializada;
- fuentes autorizadas;
- modo lectura/escritura;
- formato de retorno;
- condición “no verificable”;
- criterio de término.

### 10. Diseñar versionamiento

Recomienda una estrategia proporcional:

- Git para autoría y diffs;
- changelog para cambios de comportamiento;
- versión de política, dataset, prompt o configuración cuando afecte la
  reproducción;
- ID que conecte ejecución, decisión, cambio y validación.

El historial explica qué cambió, por qué, quién lo aprobó, cómo se validó y cómo
revertirlo. No duplica el diff.

### 11. Presentar el borrador

Genera el handoff sin escribirlo a disco. Permite aprobar, editar decisiones,
comparar alternativas o descartar piezas. No implementes hasta recibir
aprobación.

## Conflictos con reglas persistentes

Si una corrección contradice texto verificable en una skill, regla u otra
definición:

1. Lee la fuente actual.
2. Cita ruta y texto exacto.
3. Explica choque e impacto.
4. Pregunta si quiere mantener, exceptuar esta tarea o actualizar.
5. Si actualiza, confirma alcance, muestra el cambio y define historial.
6. No escribas antes de la aprobación.
7. Registra la decisión en el handoff.

No inventes conflictos desde preferencias implícitas.

## Investigación contextual

Para investigación amplia usa el subagente incluido cuando el cliente lo
soporte. Debe contrastar implementación, consumidores, tests, documentación,
tipos, configuración y evidencia de runtime.

Si devuelve preguntas materiales, pausa esa rama, pregunta al usuario y reanuda
con la respuesta. Consulta [project-context-protocol.md](project-context-protocol.md).

## Cierre

Antes de terminar, valida:

- rol y forma de validar confirmados;
- proceso y mapa de ownership confirmados;
- cada pieza resuelve una fricción concreta;
- fuentes de verdad identificadas;
- decisiones automáticas aprobadas por el usuario;
- fallback para casos desconocidos;
- guardrails para efectos externos;
- criterios de término coherentes con el rol;
- estrategia de versión e historial;
- conflictos registrados;
- siguiente paso único y claro.

Consulta [examples.md](examples.md) para comprobar que el diseño no impone
siempre la misma arquitectura.
