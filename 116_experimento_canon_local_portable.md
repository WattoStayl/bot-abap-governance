# 116 — EXPERIMENTO CANON LOCAL PORTÁTIL

ESTADO = PROPUESTA REGISTRADA / PENDIENTE DE DISEÑO

## Objetivo
Probar un agente Bot-ABAP sin dependencia de GitHub, Bing, SharePoint, conectores ni una memoria persistente del agente. El humano conserva y administra localmente la documentación canónica de trabajo.

## Principio de simplicidad
La unidad operativa debe ser fácil de entender y manipular por consultores funcionales y ABAP, con mínima fricción:

- 1 ticket = 1 archivo Markdown canónico.
- 1 proyecto = 1 archivo Markdown canónico.
- El humano es custodio del archivo vigente.
- El agente no debe exigir una estructura documental distribuida para el trabajo cotidiano.

## Ciclo operativo propuesto
1. El humano carga el `.md` del ticket o proyecto al iniciar o retomar trabajo.
2. El agente recupera exclusivamente de ese archivo el estado persistente aplicable.
3. Humano y agente trabajan durante la sesión.
4. Al pausar, cambiar de ticket/proyecto o terminar la jornada, el agente consolida los cambios y entrega el `.md` actualizado.
5. El humano guarda localmente ese archivo como versión canónica vigente.
6. Para continuar posteriormente, el humano vuelve a cargar el archivo vigente.

## Regla de memoria
Si no se carga el archivo canónico vigente de la unidad de trabajo, el agente no debe afirmar conocer su estado anterior basándose en memoria conversacional.

## Cambio de contexto
Antes de pasar de un ticket/proyecto a otro, el flujo deseado es:

`ARCHIVO ACTUAL → TRABAJO → PAUSA/CIERRE DE TRAMO → ARCHIVO ACTUALIZADO → NUEVO ARCHIVO`

El objetivo es evitar mezcla accidental de clientes, tickets, proyectos, decisiones y evidencia.

## Operaciones transversales
Para informes semanales, backlog, horas, riesgos u otros análisis cross, el humano puede cargar varios archivos canónicos.

Por defecto, una operación transversal es de SOLO LECTURA sobre los expedientes cargados y produce un artefacto derivado en el formato solicitado por el humano, por ejemplo Markdown, PDF, Word o Excel.

Los archivos fuente solo se modifican si el humano lo solicita expresamente.

## Controles propuestos
- Detectar archivos duplicados o varias versiones aparentes de una misma unidad y solicitar resolución antes de asumir cuál es vigente.
- No mezclar información entre expedientes.
- No inventar horas, estados, aprobaciones, OTs, pruebas ni decisiones faltantes.
- La persistencia se considera completada solo cuando el agente entrega el archivo actualizado y el humano asume su custodia; el chat por sí solo no sustituye el archivo.

## Criterio de diseño pendiente
La estructura final del archivo debe ser suficientemente completa para reconstruir el trabajo, pero deliberadamente simple para que un consultor humano pueda usarla sin fricción.

NEXT_GATE = Diseñar y probar una plantilla mínima autocontenida para `TICKET-XXXX.md` / `PROYECTO-XXXX.md` antes de crear el nuevo agente experimental.
