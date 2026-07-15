# Guía de entrevista

No es un cuestionario obligatorio. Haz una decisión por turno y pregunta solo
lo que pueda cambiar el diseño.

## 1. Profundidad

- Diagnóstico rápido.
- Diseño completo.
- Evaluar una idea concreta.

## 2. Rol y forma de validar

Explainer: el setup cambia según el rol. No asumas backend ni un único tipo de
test. Lee [roles.md](roles.md).

Pregunta el rol principal — admite varios:

- backend / API / servicios;
- frontend / UI;
- fullstack;
- mobile;
- QA / testing;
- DevOps / platform / SRE;
- data / analytics / ML;
- seguridad;
- tech lead / arquitectura;
- otro.

Luego completa solo lo que falte:

1. ¿Qué entregables produces habitualmente?
2. ¿Qué evidencia usas para decir que algo está listo?
3. ¿Qué entornos puedes tocar?
4. ¿Qué parte de la validación hace otro rol?

Resume:

```text
Rol: [rol]. Entregables: [...]. Valida con: [...]. Entornos: [...].
Dependencias de otros roles: [...].
```

## 3. Permiso de lectura

Explica que leer el setup evita preguntas redundantes y no autoriza cambios.

- Leer configuración y documentación relacionadas.
- Leer solo archivos indicados.
- No leer el proyecto.

Si autoriza, inspecciona antes de preguntar. Resume evidencia y huecos sin
juzgar el setup.

## 4. Proceso actual

Pregunta primero por el disparador, con opciones adaptadas al rol:

- incidente o bug;
- nueva funcionalidad;
- preparación/revisión de PR o MR;
- datos, reporte o dashboard;
- deploy, pipeline o incidente de infra;
- caso de prueba o regresión;
- evento periódico;
- otro.

Completa solo lo que falte:

1. ¿Qué entrada recibes?
2. ¿Qué pasos haces?
3. ¿Qué decisiones requieren criterio?
4. ¿Qué resultado produces?
5. ¿Cómo compruebas que quedó bien con la evidencia de tu rol?

Resume:

```text
Cuando [disparador], recibes [entrada], haces [pasos], decides [decisiones],
produces [salida] y validas con [evidencia del rol].
```

## 5. Temas y errores que mantiene

Este mapa es distinto del proceso: registra las áreas o fallas en las que la
persona trabaja habitualmente. Adapta ejemplos al rol; no sugieras solo APIs o
jobs.

Pregunta:

1. ¿Qué temas, fallas o entregables mantienes?
2. ¿Cuáles aparecen más?
3. ¿Cuáles son raros pero caros o riesgosos?
4. ¿Cuáles son tuyos y cuáles de otro equipo?
5. ¿Qué vocabulario, IDs o síntomas los identifican?
6. ¿Dónde suele estar la evidencia o causa?

Resume:

```text
| Tema | Frecuencia | Coste/riesgo | Owner | Señales | Dónde revisar | Piloto |
|------|------------|--------------|-------|---------|---------------|--------|
| ...  | ...        | ...          | ...   | ...     | ...           | sí/no  |
```

Usa el vocabulario del usuario. No inventes categorías. Si el trabajo no gira
en torno a bugs, pregunta por temas de mantenimiento equivalentes.

## 6. Prioridad

Combina frecuencia y coste:

- frecuente y costosa;
- frecuente pero corta;
- infrecuente y riesgosa;
- infrecuente y barata.

Pide elegir 1–3 temas para el piloto.

## 7. Fuente de verdad

Ofrece opciones según el rol; no listes solo SQL/API:

- base de datos o SQL;
- API o contrato;
- issue tracker;
- diseño/Figma/spec de producto;
- hoja de cálculo;
- archivos del repo;
- CI/CD, infra o observabilidad;
- dataset, warehouse o notebook;
- documentación;
- conocimiento humano;
- varias fuentes.

Si hay varias, pregunta cuál prevalece y registra frescura, ID estable y
permisos.

## 8. Estructura y variabilidad

- estructurada y estable;
- estructurada con variantes conocidas;
- texto libre con patrones;
- variable o exploratoria;
- visual/interactiva.

No asumas que una hoja de cálculo o una UI exige LLM. Evalúa primero una
transformación o checklist determinística.

## 9. Tipo de interacción

- batch o programada;
- conversacional;
- pipeline más skill de consulta;
- aún no está claro.

## 10. Decisiones definidas por el usuario

Para clasificar, priorizar, enrutar, aprobar, rechazar o actuar, el usuario debe
definir:

1. valores permitidos;
2. definiciones y exclusiones;
3. ejemplos positivos, negativos y ambiguos;
4. cardinalidad y precedencia;
5. fallback;
6. gates humanos;
7. owner.

El agente puede proponer una taxonomía, pero no establecerla sin aprobación.

## 11. Verificación adaptada al rol

No ofrezcas solo tests de backend. Pregunta qué evidencia demuestra éxito y
muestra opciones del menú de [roles.md](roles.md):

- unit / integration / contract / E2E;
- query, conteo o schema check;
- diff de código, config o infra;
- payload dry-run, sandbox o `plan`;
- preview, Storybook, screenshot o visual diff;
- checklist de UX, a11y o device matrix;
- pipeline CI/CD, canary, smoke post-deploy o rollback;
- reproducción fail→pass / regresión;
- métrica, dashboard o evaluación offline;
- revisión humana con checklist;
- otro.

Pregunta también:

1. ¿Qué ya corre en CI?
2. ¿Qué queda manual a propósito?
3. ¿En qué entorno se valida?
4. ¿Quién aprueba evidencia ambigua?

Si no existe verificación, recomienda crearla antes de automatizar.

## 12. Integraciones y autenticación

Pregunta solo cuando aplique:

- ¿Existe API, MCP, CI o sistema externo?
- ¿Auth personal o de servicio?
- ¿Lectura o escritura?
- ¿Hay datos sensibles?
- ¿Qué entorno puede tocarse?

Nunca pidas secretos en el chat.

## 13. Alcance y propiedad

- personal y reutilizable;
- proyecto;
- equipo;
- piloto personal.

Pregunta quién mantiene reglas, scripts, tests y credenciales.

## 14. Versionamiento e historial

Pregunta qué necesita reconstruir una auditoría:

- versión del workflow;
- política, prompt, dataset, fixture o configuración;
- aprobación y motivo;
- evidencia del rol;
- validación;
- rollback.

Respeta la convención existente. Si no existe, recomienda la mínima que permita
reproducir el fallo o el resultado.

## 15. Profundidad de automatización

- documentación o prompt;
- regla persistente;
- skill coordinadora;
- script, consulta o test harness;
- skill más script;
- workflow con integración externa.

No muestres todas las opciones si una ya es claramente adecuada.

## 16. Convenciones del equipo

Busca estándares, severidades, naming, criterios de review, límites de
seguridad, source of truth, definición de done y gates de calidad del rol.

Si una instrucción posterior contradice una convención textual, activa el
protocolo de conflicto de `SKILL.md`.

## Criterio de término

Detente cuando puedas responder:

1. qué rol y validaciones guiaron el diseño;
2. qué proceso se mejora;
3. qué temas mantiene el usuario;
4. cuál es la fuente de verdad;
5. qué parte es determinística;
6. qué decisiones siguen siendo humanas;
7. qué política limita al sistema;
8. qué piezas mínimas se recomiendan;
9. cómo se verifican con evidencia del rol;
10. cómo se versionan;
11. qué queda fuera de alcance.
