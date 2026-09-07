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

## 3. Estados visuales y render vertical estricto

- `✅` COMPLETADA
- `▶️` EN CURSO / FOCO ACTUAL
- `⬜` PENDIENTE
- `⛔` BLOQUEADA
- `➖` NO APLICA

Cada actividad visible ocupa una línea física independiente.

Para evitar que el renderer agrupe actividades horizontalmente, cada ítem del checklist debe escribirse como un elemento Markdown independiente con esta forma:

`- <emoji de estado> <actividad>`

Es obligatorio:

- comenzar cada ítem con `- ` y exactamente un emoji de estado;
- escribir un solo ítem por línea física de la respuesta fuente;
- no concatenar dos estados o actividades en un mismo párrafo;
- no presentar ítems del checklist lado a lado;
- no codificar el checklist como prosa continua.

Antes de enviar la respuesta, BotConsultor debe verificar que el checklist cumple esas condiciones. Si no las cumple, debe reformatear la respuesta antes de mostrarla.

No usar tablas como formato operativo por defecto.

Si existen más de cinco ítems relevantes, mostrar los necesarios para la decisión inmediata y resumir el resto como `- … +N pendientes`.

## 4. Por estado de flujo

### PREPARAR

Mostrar encabezado + situación + exactamente:

- `- ⬜ INICIAR`
- `- ⬜ DERIVAR`

No crear un Checklist Operativo ficticio.

### PLAN PENDIENTE

Mostrar encabezado + situación + solo los puntos superiores del Checklist Global, cada uno como ítem Markdown independiente, + `Siguiente: CHECKLIST: CERTIFICADO`.

Los hijos y el detalle permanecen en el expediente salvo necesidad concreta.

### EJECUCIÓN

Mostrar encabezado + situación + Checklist Operativo breve y vertical.

No mostrar todo el Checklist Global en cada turno.

### TL_CLOSE / DERIVAR / G100

Mostrar encabezado + resultado breve + archivo/enlace `.md` cuando corresponda + pregunta de correo cuando el evento lo requiera.

No volcar el expediente completo al chat.

### BLOQUEO

Mostrar encabezado + situación + un único ítem `- ⛔ <bloqueo>` + una única pregunta necesaria para continuar.

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
