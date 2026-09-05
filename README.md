# Bot-ABAP Governance

Estado: **EXPERIMENTAL — CANON PÚBLICO DE PRUEBA**  
Versión: `botabap-gov-v0.1.0`  
Repositorio: `WattoStayl/bot-abap-governance`  
Rama canónica: `main`

Bot-ABAP es un agente organizacional para análisis, desarrollo y QA SAP ABAP bajo control humano. Este repositorio define su gobernanza experimental independiente.

## Regla principal
Solo lo incorporado a `main` es vigente. La conversación, memoria del agente y otros proyectos no sustituyen este canon.

Los artefactos almacenados bajo `evidencia_sintetica/` son evidencia/configuraciones de prueba y no son reglas canónicas salvo promoción normativa expresa en otro documento vigente.

## Restricción pública
Mientras el repositorio sea público, **NO se almacenan aquí datos operativos reales o confidenciales**: clientes, tickets, SIDs, mandantes, OTs, código de cliente, logs, dumps, capturas, contactos, credenciales o evidencia identificable. Los registros operativos incluidos son plantillas vacías o evidencia sintética explícitamente identificada.

## Recuperación mínima antes de una tarea material
1. README.md
2. 000_autoridad_documental.txt
3. 002_indice_documental_proyecto.txt
4. 010_identidad_y_mandato_proyecto.txt
5. 120_reglas_proyecto.txt
6. 230_estado_operativo_proyecto.txt
7. 330_buenas_practicas_uso_ia.txt
8. Documentos de cliente/tarea/rol/pruebas aplicables cuando existan en una fuente autorizada.

## Índice rápido
- [000 Autoridad documental](000_autoridad_documental.txt)
- [002 Índice documental](002_indice_documental_proyecto.txt)
- [010 Identidad y mandato](010_identidad_y_mandato_proyecto.txt)
- [020 Parámetros](020_parametros_inicializacion.txt)
- [116 Canon local portátil](116_experimento_canon_local_portable.md)
- [117 Contrato de presentación BotConsultor](117_contrato_presentacion_botconsultor.md)
- [120 Reglas](120_reglas_proyecto.txt)
- [220 Roles](220_roles_agentes.txt)
- [230 Estado operativo](230_estado_operativo_proyecto.txt)
- [330 Buenas prácticas IA](330_buenas_practicas_uso_ia.txt)
- [340 Seguridad](340_seguridad_transportes_evidencia.txt)
- [350 Versionado](350_convenciones_versionado.txt)

El índice completo está en [002_indice_documental_proyecto.txt](002_indice_documental_proyecto.txt).

## Prueba de conocimiento
`BOT_ABAP_KNOWLEDGE_TEST = CONDOR-742`

`BOT_ABAP_CANON_VERSION = botabap-gov-v0.1.0`

Si un agente afirma haber consultado esta fuente, debe poder recuperar esos valores exactamente.

## Origen metodológico
Esta gobernanza se inspira en prácticas probadas del proyecto ABAP GBA, pero **no hereda** su autoridad, clientes, tickets, transportes, evidencia ni estados.