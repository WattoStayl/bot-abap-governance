# BotConsultor V9 CRL4 — Retoma

ESTADO = PROBADA EN CU3 Y CU7 / NO PROMOVIDA / DECISIÓN POST-CU7 PENDIENTE
CONFIGURACIÓN = Description V9 candidata + Instructions CRL4
GATE INSTRUCTIONS = 7810 / 8000 caracteres; reserva 190; CUMPLE
P1 = VIGENTE

## Resultado CRL4 / CU3

V9-CRL4-CU3 terminó con **8 correcciones**:
- 4 ALTA
- 4 MEDIA
- 0 BAJA
- 0 CRÍTICA

Comparación CU3:
- V8 = 24
- CRL1 = 13
- CRL2 = 11
- CRL3 = 11
- CRL4 = 8

Reducción CRL4 vs V8 = 66.7%.
Reducción CRL4 vs CRL3 = 27.3%.

### Correcciones CU3

- `V9-CRL4-CU3-C01 — ALTA` — El Checklist Global no cubrió explícitamente los cinco dominios semánticos obligatorios del alcance; debía representar ANÁLISIS, DISEÑO, EJECUCIÓN/DESARROLLO, PRUEBAS e HITOS DE CIERRE como aplicables o NO APLICA justificados.
- `V9-CRL4-CU3-C02 — ALTA` — El Global 20% no fue trazable con el Checklist Global certificado visible; el árbol/hierarquía gobernante y el porcentaje quedaron inconsistentes.
- `V9-CRL4-CU3-C03 — ALTA` — La actualización documental durante el análisis no fue coherente con la matriz cerrada de eventos: si no hubo TL_CLOSE no correspondía archivo, y si hubo TL_CLOSE faltó completar FILE + MAIL?.
- `V9-CRL4-CU3-C04 — MEDIA` — El handoff se expresó como ya realizado antes de confirmarse la recepción del receptor; debía mantenerse destinataria propuesta / recepción pendiente.
- `V9-CRL4-CU3-C05 — MEDIA` — Tras LOAD reconstruyó Global y estado pero mostró checklist PREP `INICIAR/DERIVAR` en vez de los pendientes reales del expediente.
- `V9-CRL4-CU3-C06 — MEDIA` — Una consulta puntual de auditoría horaria omitió P1-STRICT completo.
- `V9-CRL4-CU3-C07 — MEDIA` — En S2, `INICIAR` sin leaf específico activó automáticamente un foco; el foco debía quedar bajo control humano.
- `V9-CRL4-CU3-C08 — ALTA` — Modificó silenciosamente el Global certificado al introducir nuevos pendientes y convertir una restricción en tarea completada.

### Fortalezas CU3

- PREP generó BASE automático, Global NO CALCULABLE y exactamente INICIAR/DERIVAR.
- START desde PREP entró a PLAN y CERT no activó trabajo.
- handoff conservó estado y cerró el tramo del emisor.
- receptor no heredó horas.
- G100 cerró correctamente el tramo cuando la hora final estaba confirmada.
- P1 fue sustancialmente más consistente que versiones anteriores.

## Resultado CRL4 / CU7

V9-CRL4-CU7 terminó con **7 correcciones**:
- 6 ALTA
- 1 MEDIA
- 0 BAJA
- 0 CRÍTICA

Comparación CU7:
- V8 = 21
- CRL4 = 7

Reducción CRL4 vs V8 = 66.7%.

### Correcciones CU7

- `V9-CRL4-CU7-C01 — ALTA` — El Checklist Global inicial no cubrió explícitamente ANÁLISIS, DISEÑO, EJECUCIÓN/DESARROLLO, PRUEBAS e HITOS DE CIERRE; omitió implementación y pruebas como trabajo real del alcance.
- `V9-CRL4-CU7-C02 — ALTA` — Al completar tres puntos superiores y pasar Global 0→60% omitió el evento TL_CLOSE obligatorio: consolidación, .md automático y MAIL?.
- `V9-CRL4-CU7-C03 — MEDIA` — Un CONTROL DE CAMBIO aún no autorizado apareció como nodo del checklist operativo vigente; debía permanecer fuera del árbol certificado hasta autorización.
- `V9-CRL4-CU7-C04 — ALTA` — Tras aprobar el CONTROL DE CAMBIO, la replanificación marcó como COMPLETADA la corrección de Nombre aunque solo análisis/diseño estaban demostrados; confundió diseño con ejecución.
- `V9-CRL4-CU7-C05 — ALTA` — Al volver a cerrar trabajo afectado por un FALLO, actualizó Global y entregó .md pero omitió MAIL? del TL_CLOSE.
- `V9-CRL4-CU7-C06 — ALTA` — Al completar el diseño de Segmento y pasar Global 40→60% omitió TL_CLOSE → CONS/FILE + MAIL?.
- `V9-CRL4-CU7-C07 — ALTA` — Al completar criterios de validación y pasar Global 60→80% volvió a omitir TL_CLOSE → CONS/FILE + MAIL?.

### Fortalezas CU7

- La ampliación Segmento fue clasificada explícitamente como CONTROL DE CAMBIO antes de modificar alcance o ejecutar.
- Se registraron impacto y estimación manteniendo el alcance original mientras no existía aprobación.
- Tras autorización volvió a PLAN y exigió nueva certificación.
- El feedback posterior se clasificó correctamente como FALLO, reabriendo trabajo dentro del alcance vigente sin pedir nueva autorización de cambio.
- Diseño se mantuvo separado de implementación en los turnos explícitos.
- G100 generó .md, preguntó MAIL?, cerró el tramo 09:00→11:15 y no implicó cierre formal.
- Ante la pregunta de cierre definitivo rechazó cerrar porque Segmento no estaba implementado ni probado.

## Raíces residuales a analizar

1. **Construcción semántica del Global**: cobertura explícita de los cinco dominios, jerarquía y trazabilidad del porcentaje.
2. **Diseño ≠ ejecución en el árbol**: no marcar como completa una corrección si solo se demostró análisis/diseño.
3. **TL_CLOSE determinista**: varios cierres de TL siguen sin completar CONS/FILE + MAIL?.
4. **Trabajo no autorizado fuera del árbol vigente**: CONTROL DE CAMBIO pendiente no debe aparecer como nodo operativo.
5. **LOAD**: reconstruir y mostrar estado de trabajo, no volver visualmente a PREP.
6. **Control humano del foco**: START genérico en S2 no debe activar leaf.
7. **P1 transversal**: también debe aplicarse a consultas puntuales de auditoría.

## Mejora UX pendiente

PROPUESTA, no aplicada durante los casos: para una persona nueva, `CHECKLIST: CERTIFICADO` no explica qué ocurrirá. Evaluar una interfaz como:

`Si apruebas este plan, responde: CHECKLIST: CERTIFICADO`

El comando estable puede mantenerse; la mejora es de presentación/entendimiento humano.

## Lectura estratégica para la siguiente sesión

CRL4 redujo aproximadamente dos tercios de las correcciones históricas en ambos stress tests y no produjo correcciones CRÍTICAS. La mejora ya no parece dispersa: los defectos remanentes están concentrados principalmente en **Global + TL_CLOSE**, con algunas regresiones menores de LOAD/foco/P1.

## Decisión pendiente

NO DECIDIDA. No inferir la siguiente rama.

Opciones a evaluar en la próxima sesión:

1. **CRL5**: iterar el motor focalizando Global, separación diseño/ejecución, TL_CLOSE y los regresores menores observados.
2. **Mantener CRL4 y avanzar CU12–CU15**: probar flujos GBA más realistas antes de otra iteración del motor.

## Protocolo de retoma

1. refrescar `main` y registrar SHA;
2. leer README/000/002/010/120/230/330;
3. leer `117_contrato_presentacion_botconsultor.md`, `320_plan_pruebas_proyecto.txt`, `321_registro_resultados_pruebas.txt`, este resume, Description V9 y Instructions CRL4;
4. confirmar que CRL4 sigue en 7810/8000 caracteres;
5. revisar CU3=8 y CU7=7 en conjunto;
6. esperar decisión humana expresa: CRL5 o CU12-CU15;
7. no editar configuración ni iniciar un nuevo caso antes de esa decisión.

## Siguiente acción

Analizar los resultados completos de CRL4 y decidir expresamente entre **CRL5** y **CU12–CU15**.
