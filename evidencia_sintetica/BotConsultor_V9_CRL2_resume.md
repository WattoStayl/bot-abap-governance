# BotConsultor V9 CRL2 — estado de retoma

ESTADO = ARTEFACTO DE PRUEBA / PROPUESTA / NO VIGENTE
FECHA = 2026-09-07
BASE_CANONICA_LEIDA = main @ 54409929b85ce791be1c8c5f62dd551627080c7e

## 1. Artefactos de configuración

- Description candidata: `evidencia_sintetica/BotConsultor_V9_description_candidate.txt`
  - longitud medida: 526 caracteres.
  - máximo canónico: NO DEFINIDO.
- Instructions CRL2 candidata: `evidencia_sintetica/BotConsultor_V9_instructions_CRL2_candidate.txt`
  - longitud medida: 7425 caracteres.
  - SHA-256 del contenido medido localmente antes de persistir: `ac887eefad22ddc427e2dc9d5af05a859ffc97547960ae0829b0135ea2697082`.

## 2. Gate de tamaño

El canon vigente en `020_parametros_inicializacion.txt` establece:

`BOTCONSULTOR_INSTRUCTIONS_MAX_CHARACTERS = 8000`

`BOTCONSULTOR_INSTRUCTIONS_SIZE_GATE = OBLIGATORIO_ANTES_DE_ENTREGAR_O_PROBAR_CANDIDATA`

CRL2 cumple el gate:

- usado: 7425 caracteres;
- máximo: 8000;
- reserva: 575 caracteres.

No declarar lista para prueba una futura variante de Instructions que exceda 8000 caracteres; debe compactarse antes sin perder invariantes, gates ni comportamiento requerido.

El canon actual no define un máximo para Description. Si la plataforma impone un límite, debe confirmarse y persistirse antes de tratarlo como requisito canónico; no inferirlo.

## 3. Antecedente CRL1 / CU3

Stress test sintético V9 CRL1 / CU3:

- V8 CU3: 24 correcciones, incluida 1 CRÍTICA.
- V9 CRL1 CU3: 13 correcciones = 7 ALTA / 6 MEDIA / 0 CRÍTICA.
- reducción: 11 correcciones = 45,8 %.
- hallazgo principal: no se reprodujo la pérdida crítica del Checklist Global certificado durante handoff.

Comportamientos que CRL2 debe conservar:

- preservar árbol certificado y porcentaje entre handoff y chat nuevo;
- receptor no hereda automáticamente horas del emisor;
- carga de `.md` no reconstruye otro Global ni inicia tiempo;
- avance jerárquico coherente;
- diseño no equivale a implementación;
- 100 % de Global no equivale a cierre formal;
- evidencia y pendientes sobreviven al handoff.

## 4. Objetivos lógicos CRL2

CRL2 concentra cambios en cuatro raíces pendientes:

1. Persistencia automática obligatoria: `BASE`, `TL_CLOSE`, `DERIVAR` y `G100` deben ejecutar eventos atómicos de consolidación y entrega real del `.md`; `TL_CLOSE/G100` además preguntan por correo sin enviar automáticamente.
2. Tiempo/handoff: toda consolidación conserva todos los tramos; `DERIVAR` cierra y persiste el tramo del emisor cuando hay inicio/fin confirmados; el receptor abre su propio tramo únicamente al iniciar.
3. Integridad Global: antes de validación deben cubrirse o justificarse ANÁLISIS, DISEÑO, EJECUCIÓN/DESARROLLO, PRUEBAS e HITOS DE CIERRE; ningún hijo puede marcarse COMPLETADO por inferencia o solo para cerrar el padre.
4. Control humano del foco: certificación, cierre de TL, carga, desbloqueo o disponibilidad no pueden marcar automáticamente el siguiente nodo EN CURSO; solo una instrucción inequívoca del humano activa foco.

## 5. Presentación transversal

`117_contrato_presentacion_botconsultor.md` / P1 está VIGENTE y aplica a CRL2 y versiones futuras.

Objetivo: minimizar scroll. Salida normal:

- encabezado `<CLIENTE> | <ACTIVIDAD/TICKET/PROYECTO> | Global ...`;
- situación en máximo una frase;
- checklist visible máximo cinco ítems con `✅ ▶️ ⬜ ⛔ ➖`;
- una sola siguiente acción/pregunta;
- detalle durable en el `.md`, no repetido rutinariamente en chat.

Las desviaciones visuales de CU3 quedan gobernadas por P1 y no son el foco principal del motor lógico CRL2.

## 6. Estado epistemológico / promoción

- `BOTCONSULTOR_CONFIG_BASE`: continúa V8_PRUEBAS hasta promoción expresa posterior.
- CRL2: PROPUESTA / NO VIGENTE / NO PROBADA aún.
- La persistencia de CRL2 bajo `evidencia_sintetica/` no la convierte en norma canónica.
- `CORE/AUX/OUT`, `TICKET→PROYECTO` y `FB@BOT` siguen siendo propuestas V9 y no adquieren vigencia por aparecer dentro del artefacto de prueba.
- `ACTIVE_AGENT_ROLE = NO ACTIVADO`.

## 7. Protocolo de retoma en otro chat

Antes de actuar, refrescar `main`, registrar SHA y leer el conjunto canónico mínimo indicado por README.

Luego:

1. leer este archivo;
2. leer `evidencia_sintetica/BotConsultor_V9_description_candidate.txt`;
3. leer `evidencia_sintetica/BotConsultor_V9_instructions_CRL2_candidate.txt`;
4. verificar nuevamente que Instructions tiene `<= 8000` caracteres;
5. usar Description V9 + CRL2 en Copilot;
6. abrir chat nuevo;
7. ejecutar smoke test CU3 con correcciones acumuladas en cero;
8. no modificar la configuración durante el caso; solo registrar desviaciones;
9. comparar resultado contra CRL1 y preservar no-regresiones.

Primer prompt copiable del smoke test:

```text
Tengo una actividad para ACME-DEMO, módulo FI. Necesitamos revisar por qué en algunos registros de una salida Z la columna Nombre queda vacía. Todavía no existe número de ticket.
```

Al recibir respuesta, evaluar especialmente en el primer paso:

- P1;
- `Global: NO CALCULABLE`;
- creación BASE sin iniciar análisis/tiempo;
- entrega automática de archivo `.md` real;
- `INICIAR / DERIVAR` como acciones de flujo.

## 8. Única siguiente acción

Cargar Description V9 + Instructions CRL2 en Copilot y comenzar el smoke test V9-CRL2/CU3 desde un chat nuevo con el prompt anterior.
