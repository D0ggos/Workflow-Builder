# Protocolo de investigación contextual

Usa este protocolo desde el agente principal o mediante el subagente opcional
`project-context-investigator`.

## Regla

Nunca describas comportamiento basándote solo en nombres. Contrasta:

1. implementación;
2. consumidores/call sites;
3. tests;
4. documentación;
5. tipos y configuración;
6. evidencia de runtime.

## Entrada

```text
Objetivo del workflow:
Área inicial:
Pregunta a responder:
Fuentes autorizadas:
Restricciones:
```

## Qué investigar

- entrypoint, entrada y salida;
- callers y dependencias;
- estado leído o escrito;
- efectos externos;
- guards y errores;
- tests;
- reglas textuales;
- contradicciones e incertidumbres.

Prioriza orquestadores, interfaces públicas, routing, persistencia, permisos,
side effects y reglas de negocio. No leas exhaustivamente helpers irrelevantes.

## Ambigüedad material

Pausa si la respuesta cambia límites, permisos, fuente de verdad, estrategia de
validación, efectos, ownership o batch vs conversación.

Devuelve:

```text
Pregunta:
Por qué importa:
Evidencia:
Opciones observables:
Recomendación:
```

## Confianza

- Confirmado: implementación y consumidor/test coinciden.
- Probable: implementación clara sin suficiente contraste.
- Ambiguo: fuentes contradictorias.
- Desconocido: evidencia insuficiente.

## Salida

```markdown
# Contexto del proyecto

## Resumen verificable
## Mapa de piezas y evidencia
## Convenciones textuales
## Hipótesis descartadas
## Incertidumbres
## Solicitudes de aclaración
## Implicaciones para el workflow
## Fuera de alcance
```

Termina cuando el flujo relevante está respaldado, las piezas críticas tienen
consumidores/dependencias identificados o incertidumbre explícita, y el
diseñador puede continuar sin asumir comportamiento.
