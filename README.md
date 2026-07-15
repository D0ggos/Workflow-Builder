# Agentic Workflow Designer

Skill portable para entrevistar desarrolladores y diseñar workflows agénticos a
medida. No impone una arquitectura: reconstruye el trabajo real, identifica qué
mantiene la persona y propone la combinación mínima de skills, reglas,
subagentes, scripts, hooks, automatizaciones, APIs o MCP.

Compatible con el formato abierto [Agent Skills](https://agentskills.io/).

## Qué hace

La skill guía una entrevista progresiva para:

1. identificar el rol del usuario y cómo valida resultados;
2. reconstruir el proceso actual;
3. inventariar temas, errores y áreas de ownership;
4. identificar fuentes de verdad;
5. priorizar fricciones por frecuencia, coste y riesgo;
6. separar trabajo determinístico de interpretación;
7. definir con el usuario taxonomías, decisiones, fallbacks y gates;
8. elegir los artefactos mínimos;
9. diseñar límites y criterios de término con evidencia del rol;
10. proponer versionamiento e historial auditable;
11. producir un handoff listo para implementar.

Se adapta a backend, frontend, mobile, QA, DevOps/SRE, data y otros perfiles.
No asume que todos validan con SQL, payloads o tests de API.

También detecta correcciones que contradicen reglas persistentes. En ese caso
cita el conflicto y pregunta si debe mantener la regla, aplicar una excepción o
actualizarla.

## Qué no hace

- No implementa el workflow durante la entrevista.
- No inventa categorías, severidades ni decisiones.
- No automatiza por defecto cada tarea repetitiva.
- No asume que una skill o un LLM siempre son la solución.
- No impone validación de un rol a otro.
- No lee código o configuración sin consentimiento.

## Estructura

```text
agentic-workflow-designer/
├── SKILL.md
├── README.md
├── MANUAL.md
├── questions.md
├── roles.md
├── decision-tree.md
├── governance.md
├── handoff-template.md
├── examples.md
├── project-context-protocol.md
├── CHANGELOG.md
└── agents/
    ├── project-context-investigator.md
    └── opencode/
        └── project-context-investigator.md
```

`project-context-investigator` es opcional. Permite explorar código en modo
solo lectura antes de diseñar el workflow. Si no se instala, la skill indica al
agente principal que use un explorador equivalente o aplique el protocolo
incluido.

## Requisitos

- Un cliente que soporte `SKILL.md`/Agent Skills, o que pueda cargar
  instrucciones Markdown.
- No requiere dependencias de runtime.
- El subagente necesita herramientas de lectura y búsqueda del repositorio.

## Preparar el repositorio

Después de publicarlo, reemplaza esta variable por la URL real:

```bash
REPO_URL="https://github.com/D0ggos/Workflow-Builder"
```

Las instrucciones siguientes muestran instalación personal y por proyecto.

## Cursor

Cursor descubre skills en `.cursor/skills/`, `.agents/skills/`,
`~/.cursor/skills/` y `~/.agents/skills/`.

### Personal

```bash
git clone "$REPO_URL" ~/.cursor/skills/agentic-workflow-designer
mkdir -p ~/.cursor/agents
cp ~/.cursor/skills/agentic-workflow-designer/agents/project-context-investigator.md \
  ~/.cursor/agents/project-context-investigator.md
```

### Proyecto

```bash
git submodule add "$REPO_URL" .cursor/skills/agentic-workflow-designer
mkdir -p .cursor/agents
cp .cursor/skills/agentic-workflow-designer/agents/project-context-investigator.md \
  .cursor/agents/project-context-investigator.md
```

También puedes copiar la carpeta en lugar de usar un submódulo.

Invócala explícitamente con:

```text
/agentic-workflow-designer
```

O por intención:

```text
Ayúdame a convertir este proceso manual en un workflow reutilizable.
```

Documentación oficial: [Cursor Agent Skills](https://cursor.com/docs/skills).

## Claude Code

Claude Code usa `.claude/skills/` para proyecto y `~/.claude/skills/` para
instalación personal. Las skills pueden activarse por contexto o mediante
`/agentic-workflow-designer`.

### Personal

```bash
git clone "$REPO_URL" ~/.claude/skills/agentic-workflow-designer
mkdir -p ~/.claude/agents
cp ~/.claude/skills/agentic-workflow-designer/agents/project-context-investigator.md \
  ~/.claude/agents/project-context-investigator.md
```

### Proyecto

```bash
git submodule add "$REPO_URL" .claude/skills/agentic-workflow-designer
mkdir -p .claude/agents
cp .claude/skills/agentic-workflow-designer/agents/project-context-investigator.md \
  .claude/agents/project-context-investigator.md
```

Documentación oficial:

- [Skills de Claude Code](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Subagentes de Claude Code](https://docs.anthropic.com/en/docs/claude-code/sub-agents)

## OpenCode

OpenCode descubre skills en:

- proyecto: `.opencode/skills/`, `.claude/skills/` y `.agents/skills/`;
- personal: `~/.config/opencode/skills/`, `~/.claude/skills/` y
  `~/.agents/skills/`.

### Personal

```bash
git clone "$REPO_URL" ~/.config/opencode/skills/agentic-workflow-designer
mkdir -p ~/.config/opencode/agents
cp ~/.config/opencode/skills/agentic-workflow-designer/agents/opencode/project-context-investigator.md \
  ~/.config/opencode/agents/project-context-investigator.md
```

### Proyecto

```bash
git submodule add "$REPO_URL" .opencode/skills/agentic-workflow-designer
mkdir -p .opencode/agents
cp .opencode/skills/agentic-workflow-designer/agents/opencode/project-context-investigator.md \
  .opencode/agents/project-context-investigator.md
```

El adaptador de OpenCode declara `mode: subagent` y niega edición, shell y web.

Documentación oficial:

- [Skills de OpenCode](https://opencode.ai/docs/skills/)
- [Agentes de OpenCode](https://opencode.ai/docs/agents/)

## Instalación portable con `.agents`

`.agents/skills/` es una convención compartida por varios clientes. Cursor y
OpenCode la descubren directamente:

```bash
git submodule add "$REPO_URL" .agents/skills/agentic-workflow-designer
```

Claude Code no documenta `.agents/skills/` como ruta nativa. Para compartir la
misma copia, crea un enlace:

```bash
mkdir -p .claude/skills
ln -s ../../.agents/skills/agentic-workflow-designer \
  .claude/skills/agentic-workflow-designer
```

En sistemas donde los enlaces simbólicos no sean convenientes, copia la carpeta
a la ruta específica del cliente.

El subagente sigue necesitando instalarse en la ruta propia de cada herramienta.

## Otros IDEs y agentes

Si el cliente soporta Agent Skills:

1. busca su directorio de skills de proyecto o usuario;
2. copia o clona esta carpeta con el nombre
   `agentic-workflow-designer`;
3. confirma que `SKILL.md` quede directamente dentro de esa carpeta;
4. instala el subagente solo si el cliente soporta agentes personalizados;
5. adapta el frontmatter del subagente a los permisos del cliente.

Si el cliente no soporta skills nativas, todavía puedes usarla:

1. agrega `SKILL.md` y sus referencias al repositorio;
2. configura las instrucciones del agente para leer `SKILL.md` cuando el
   usuario pida diseñar o automatizar un workflow;
3. usa `project-context-protocol.md` desde el agente principal en lugar del
   subagente.

No copies el contenido completo de la skill dentro de una regla global: ocupará
contexto en tareas no relacionadas.

## Verificar la instalación

Comprueba:

1. la carpeta se llama `agentic-workflow-designer`;
2. contiene `SKILL.md`;
3. el frontmatter incluye `name` y `description`;
4. el cliente muestra la skill disponible;
5. este prompt activa la entrevista:

```text
Quiero diseñar un workflow para una tarea que repito cada semana.
```

La respuesta debería preguntar por profundidad o rol/validación antes de
implementar. No debería crear archivos inmediatamente.

Para probar el protocolo de gobernanza:

```text
El agente debe clasificar errores, pero todavía no definí las categorías.
```

La skill debe pedir que el usuario defina o apruebe valores, ejemplos,
precedencia y fallback.

## Actualizar

Clon personal:

```bash
git -C ~/.cursor/skills/agentic-workflow-designer pull
```

Adapta la ruta para Claude Code u OpenCode. Si copiaste el subagente, vuelve a
copiarlo después de actualizar.

Submódulo de proyecto:

```bash
git submodule update --remote --merge \
  .cursor/skills/agentic-workflow-designer
```

Adapta la ruta al cliente utilizado.

## Publicar en GitHub

1. Crea un repositorio vacío.
2. Mueve o copia el contenido de esta carpeta a su raíz.
3. Elige una licencia antes de publicarlo.
4. Reemplaza `TU_USUARIO` en este README.
5. Crea el primer commit y conecta el remote.
6. Prueba una instalación limpia en al menos un proyecto temporal.

Este paquete no incluye licencia para no asumir una sin decisión del autor.

## Uso rápido

```text
Soy [rol]. Quiero automatizar [proceso]. Primero entrevista mi forma actual de
trabajar, cómo valido resultados, los temas que mantengo y propón el setup
mínimo. No implementes hasta que apruebe el handoff.
```

Consulta [MANUAL.md](MANUAL.md) para la metodología completa.
