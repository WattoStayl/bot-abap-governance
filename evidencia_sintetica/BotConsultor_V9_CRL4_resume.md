# BotConsultor V9 CRL4 — Retoma

ESTADO = PROPUESTA / NO VIGENTE / NO PROBADA
BASE DE COMPARACIÓN = CU3

## Resultado anterior

V9 CRL3 / CU3 terminó con 11 correcciones:
- 5 ALTA
- 5 MEDIA
- 1 BAJA
- 0 CRÍTICA

Comparación: V8=24; CRL1=13; CRL2=11; CRL3=11.

Mejoras cualitativas confirmadas de CRL3:
- P1-STRICT produjo checklist vertical consistente en la mayor parte del flujo;
- BASE automático y nombre estable del expediente mejoraron;
- el Global respetó NO APLICA para ejecución/pruebas fuera del alcance;
- handoff preservó Global y tiempo del emisor;
- receptor no heredó horas;
- foco siguió bajo control humano.

Pendientes observados en CRL3:
1. antes de certificación llegó a mostrar Global 0% en vez de NO CALCULABLE;
2. PREP incluyó metadatos del expediente como ítems de checklist;
3. START entró inicialmente en ejecución antes de construir/certificar G;
4. datos descubribles fueron tratados como bloqueantes;
5. PLAN y START generaron archivo/revisión sin evento aplicable;
6. checklist incluyó metadatos como “Checklist certificado” o “Expediente actualizado”;
7. TL_CLOSE no completó siempre FILE + MAIL?;
8. G100 no completó MAIL?;
9. G100 dejó activo el tramo de Daniela pese a hora 11:45 confirmada.

## Diseño CRL4

CRL4 introduce:
- máquina cerrada S0 PREP → S1 PLAN → S2 EXEC;
- START desde PREP solo mueve a PLAN y nunca ejecuta análisis;
- Global NO_CALCULABLE obligatorio antes de CHECKLIST: CERTIFICADO;
- matriz cerrada de auto-write: solo BASE, TL_CLOSE, DERIVAR, G100 y USER_E;
- START/PLAN/CERT/LOAD no consolidan ni generan revisión/archivo;
- checklist operativo solo contiene estados de trabajo, nunca metadatos documentales;
- TL_CLOSE/G100 obligan FILE + MAIL? antes de responder;
- si TL_CLOSE causa G100 se ejecuta una sola cadena combinada;
- G100 usa una hora confirmada en el mismo turno para cerrar el tramo activo antes de CONS;
- P1-STRICT se mantiene como contrato visual.

## Gate de tamaño

Instructions CRL4 = 7810 caracteres.
Máximo canónico = 8000.
Reserva = 190.
Resultado = CUMPLE.

## Secuencia de prueba confirmada

1. Probar primero CU3 completo con CRL4 y contador de correcciones desde cero para comparar avance contra:
   - V8/CU3 = 24 correcciones;
   - CRL1/CU3 = 13;
   - CRL2/CU3 = 11;
   - CRL3/CU3 = 11.
2. Después probar CU7 completo con CRL4.
   - referencia histórica V8/CU7 = 21 correcciones;
   - foco: cambio de alcance, feedback, FALLO vs CONTROL DE CAMBIO, autorización y replanificación sin perder P1-STRICT ni los gates de verdad/evidencia.
3. Solo después de disponer de los resultados de CU3 y CU7, el humano decidirá expresamente entre:
   - construir/probar CRL5 si todavía conviene iterar el motor;
   - mantener CRL4 y continuar con CU12, CU13, CU14 y CU15.
4. La decisión CRL5 vs CU12–CU15 está PENDIENTE y no debe inferirse antes de terminar CU3 y CU7.
5. No modificar Instructions durante un caso activo.

## Protocolo de prueba

Usar Description V9 candidata + Instructions CRL4 en Copilot, chat nuevo, correcciones por caso desde cero y sin editar configuración durante el caso.

Primer caso = CU3.

Primer prompt CU3:
`Tengo una actividad para ACME-DEMO, módulo FI. Necesitamos revisar por qué en algunos registros de una salida Z la columna Nombre queda vacía. Todavía no existe número de ticket.`

Primer gate esperado CU3:
- encabezado P1;
- Global NO CALCULABLE;
- BASE .md automático;
- checklist exactamente INICIAR / DERIVAR;
- ningún análisis ni Global antes de INICIAR.

Después de cerrar y evaluar CU3, iniciar CU7 con contador de correcciones en cero. No decidir CRL5 ni CU12–CU15 hasta finalizar CU7.
