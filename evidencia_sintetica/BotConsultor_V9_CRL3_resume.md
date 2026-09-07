# BotConsultor V9 CRL3 — estado de retoma

ESTADO = ARTEFACTO DE PRUEBA / PROPUESTA / NO VIGENTE
BASE_CANONICA_LEIDA = main @ 5d512b0d80f927942c50f0e79ec8d23f8a9ca94c

## Configuración
- Description: `evidencia_sintetica/BotConsultor_V9_description_candidate.txt`
- Instructions: `evidencia_sintetica/BotConsultor_V9_instructions_CRL3_candidate.txt`
- Instructions medido: 7917 caracteres.
- Máximo canónico: 8000.
- Reserva: 83.
- SHA-256: `4d72ee4ce3a7600fea76d679c1178ec91715e6e4b5b71e1e76b0c98adce892b9`.

## Prioridad CRL3
La prioridad máxima es mantener coherencia visual P1 en TODA respuesta normal: checklist vertical Markdown, un ítem por línea física, máximo cinco ítems y verificación FORMAT_CHECK antes de enviar.

`117_contrato_presentacion_botconsultor.md` fue endurecido para exigir `- <emoji> <actividad>` por ítem y prohibir concatenación horizontal.

## Resultado CRL2/CU3
- V8: 24 correcciones / 1 CRÍTICA.
- CRL1: 13 / 0 CRÍTICAS.
- CRL2: 11 / 6 ALTA / 5 MEDIA / 0 CRÍTICA.
- CRL2 preservó correctamente el tramo del emisor a través del handoff, el receptor retomó sin heredar horas y mantuvo el Global certificado.
- Persistieron fallos en BASE, alcance/NO APLICA, TL_CLOSE automático, nombre físico/handoff y consistencia visual.

## Cambios CRL3
1. P1-STRICT con gramática Markdown vertical y FORMAT_CHECK obligatorio.
2. BASE inmediato si tipo/cliente/módulo/tema ya están disponibles; datos descubribles no bloquean.
3. Global limitado al alcance actual; dominios futuros fuera de alcance se justifican NO APLICA en vez de ampliar el plan.
4. TL_CLOSE definido como transición no-D→D con cadena de evento obligatoria antes de respuesta normal.
5. Nombre físico estable sin rev/state/handoff/final.
6. Destinatario de handoff permanece propuesto hasta confirmación explícita de recepción.
7. Conserva las mejoras CRL2 de tiempos, continuidad y control humano del foco.

## Protocolo de próxima prueba
1. Refrescar `main` y leer canon mínimo.
2. Releer P1, 320/321, este archivo, Description y CRL3.
3. Verificar de nuevo Instructions <=8000.
4. Cargar Description V9 + CRL3 en Copilot.
5. Abrir chat nuevo.
6. Repetir CU3 con correcciones en cero.
7. No editar configuración durante el caso.

Primer prompt:
```text
Tengo una actividad para ACME-DEMO, módulo FI. Necesitamos revisar por qué en algunos registros de una salida Z la columna Nombre queda vacía. Todavía no existe número de ticket.
```

En la primera respuesta verificar prioritariamente:
- encabezado P1;
- checklist en bullets Markdown realmente verticales;
- solo INICIAR/DERIVAR en PREP;
- Global NO CALCULABLE;
- BASE `.md` automático real.
