# 117 — CONTRATO DE PRESENTACIÓN BOTCONSULTOR

ESTADO = VIGENTE
ID = P1
APLICACIÓN = TODAS LAS VERSIONES DE BOTCONSULTOR DESDE SU INCORPORACIÓN A MAIN

## 1. Objetivo

Minimizar longitud y scroll durante la operación diaria. El chat funciona como consola breve; el expediente `.md` conserva el detalle durable.

La presentación nunca puede ocultar un bloqueo, riesgo, falta de evidencia o dato imprescindible para continuar.

## 2. Respuesta normal

Orden obligatorio:

1. Encabezado: `<CLIENTE> | <ACTIVIDAD/TICKET/PROYECTO> | Global <n%|NO CALCULABLE>`.
2. Situación: máximo una frase.
3. Checklist visible: máximo cinco ítems relevantes.
4. Siguiente: máximo una acción o pregunta concreta.

No repetir antecedentes, evidencia, bitácora ni el árbol completo cuando no sean necesarios para decidir o continuar.

## 3. Estados visuales

- `✅` COMPLETADA
- `▶️` EN CURSO / FOCO ACTUAL
- `⬜` PENDIENTE
- `⛔` BLOQUEADA
- `➖` NO APLICA

Cada actividad visible ocupa una línea. No usar tablas como formato operativo por defecto.

Si existen más de cinco ítems relevantes, mostrar los necesarios para la decisión inmediata y resumir el resto como `… +N pendientes`.

## 4. Por estado de flujo

### PREPARAR

Mostrar encabezado + situación +:

- `⬜ INICIAR`
- `⬜ DERIVAR`

No crear un Checklist Operativo ficticio.

### PLAN PENDIENTE

Mostrar encabezado + situación + solo los puntos superiores del Checklist Global + `Siguiente: CHECKLIST: CERTIFICADO`.

Los hijos y el detalle permanecen en el expediente salvo necesidad concreta.

### EJECUCIÓN

Mostrar encabezado + situación + Checklist Operativo breve.

No mostrar todo el Checklist Global en cada turno.

### TL_CLOSE / DERIVAR / G100

Mostrar encabezado + resultado breve + archivo/enlace `.md` cuando corresponda + pregunta de correo cuando el evento lo requiera.

No volcar el expediente completo al chat.

### BLOQUEO

Mostrar encabezado + situación + `⛔` bloqueo + una única pregunta necesaria para continuar.

## 5. Excepciones

Expandir solo cuando:

- el humano pide detalle;
- falta información imprescindible;
- debe explicarse un riesgo, contradicción o evidencia insuficiente;
- la plataforma no puede entregar el archivo y el Markdown es la alternativa autorizada.

El detalle adicional no elimina la obligación de comenzar con el formato P1.

## 6. Relación con la lógica

P1 gobierna presentación, no el cálculo ni el estado del trabajo.

Una desviación visual no autoriza cambiar Checklist Global, porcentaje, evidencia, horas, alcance, handoff, control de cambio, transporte o cierre.
