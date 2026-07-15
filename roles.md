# Roles y formas de validar

El workflow debe adaptarse al rol del usuario. No asumas backend, APIs, SQL o
payloads dry-run. Pregunta el rol y cómo comprueba hoy que algo quedó bien.

## Cómo descubrir el rol

Pregunta en este orden:

1. ¿Cuál es tu rol principal?
2. ¿Qué entregables produces habitualmente?
3. ¿Qué evidencia usas para decir “está listo”?
4. ¿Qué entornos puedes tocar: local, preview, staging, producción?
5. ¿Qué partes del ciclo las hace otro rol?

Opciones comunes — permite múltiples o “Otro”:

- backend / API / servicios;
- frontend / UI;
- fullstack;
- mobile;
- QA / testing;
- DevOps / platform / SRE;
- data / analytics / ML;
- seguridad;
- tech lead / arquitectura;
- product engineering / discovery técnico;
- otro.

No reduzcas a un solo estereotipo. Una persona puede ser backend con ownership
de observabilidad, o frontend que también mantiene contratos de API.

## Matriz de validación por rol

Usa esta matriz como menú, no como checklist obligatorio. Pregunta cuáles aplica
el usuario y cuáles son gates duros vs opcionales.

| Rol | Entregables típicos | Validaciones habituales | Evidencia de término |
|-----|---------------------|-------------------------|----------------------|
| Backend | API, jobs, migraciones, contratos | unit/integration, contract tests, query/conteo, logs, traces, dry-run de side effects | test verde, payload esperado, métrica/log, migración reversible |
| Frontend | UI, estados, accesibilidad, client state | unit/component, visual/regression, Storybook/preview, a11y, Lighthouse, E2E de flujo | preview aprobado, screenshot/diff, checklist UX, E2E del camino crítico |
| Mobile | builds, stores, device matrix | unit, UI tests, device/emulator, snapshot, smoke en build | build instalable, smoke en dispositivo objetivo, checklist de release |
| QA | planes, casos, reportes, regresiones | exploratory, regression suite, reproducciones, matrices de entorno | caso reproducible, evidencia fail→pass, cobertura del riesgo |
| DevOps/SRE | infra, CI/CD, alertas, runbooks | plan/apply dry-run, pipeline verde, canary/rollback, dashboards, chaos/smoke post-deploy | plan sin drift inesperado, deploy con rollback, alerta validada |
| Data/Analytics/ML | queries, pipelines, modelos, dashboards | schema checks, row counts, data quality, backfill dry-run, notebook/repro, métricas offline/online | dataset validado, query reproducible, métrica dentro de rango |
| Seguridad | findings, controles, reviews | threat model, SAST/DAST, secrets scan, review de permisos, exploit PoC controlado si aplica | finding citado, severidad acordada, remediación verificada |
| Tech lead | decisiones, ADRs, reviews | checklist de arquitectura, trade-offs documentados, pruebas de riesgo alto | decisión registrada, riesgos y rollback definidos |

## Señales de validación — menú ampliado

Cuando preguntes cómo verifica, ofrece opciones del rol y deja “Otro”:

**Comunes**

- test automatizado (unit, integration, contract, E2E);
- diff de código o configuración;
- revisión humana con checklist;
- métrica o dashboard posterior;
- reproducción fail → pass.

**Backend / datos**

- query o conteo;
- contrato OpenAPI/Protobuf/schema;
- payload dry-run o sandbox;
- logs/traces;
- migración con rollback.

**Frontend / mobile**

- preview/Storybook;
- screenshot o visual diff;
- checklist de accesibilidad o UX;
- matriz de navegadores/dispositivos;
- build instalable / TestFlight / internal track.

**QA**

- caso exploratorio documentado;
- suite de regresión;
- evidencia multimedia o pasos exactos;
- matriz de entornos/datos;
- definición de severidad y retest.

**DevOps / platform**

- `plan`/`diff` de infra;
- pipeline CI/CD;
- canary, blue/green o feature flag;
- smoke post-deploy;
- runbook de rollback.

**Data / ML**

- validación de esquema y nulos;
- comparación de snapshots o hashes;
- backfill controlado;
- evaluación offline;
- monitoreo de drift.

## Anti-patrones por sesgo de rol

No hagas esto:

- proponer SQL/payload dry-run a quien valida con preview visual;
- proponer Storybook/screenshot a un backend sin UI;
- asumir que “test” significa solo unit tests;
- omitir rollback en DevOps o migraciones;
- tratar accesibilidad o device matrix como opcionales si el rol las usa como gate;
- imponer clasificaciones de errores de backend a un rol de diseño/producto;
- pedir secretos, tokens de tiendas o credenciales cloud en el chat.

## Cómo adaptar el diseño

1. Fija el rol y las validaciones confirmadas antes de elegir artefactos.
2. Los criterios de término de cada skill deben usar la evidencia de ese rol.
3. Si el usuario es fullstack o híbrido, separa gates por tipo de cambio.
4. Si parte de la validación la hace otro rol, márcalo como dependencia o fuera
   de alcance.
5. Cuando propongas automatizar tests, pregunta qué ya corre en CI y qué queda
   manual a propósito.

## Preguntas mínimas de verificación

1. ¿Qué demuestra que el cambio está bien?
2. ¿Eso es automatizable, semi-automatizable o solo humano?
3. ¿En qué entorno se valida?
4. ¿Qué no debe tocarse en la validación?
5. ¿Qué evidencia hay que guardar para auditoría o retest?
6. ¿Quién aprueba si la evidencia es ambigua?
