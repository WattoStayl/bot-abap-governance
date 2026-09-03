# 116 — EXPERIMENTO CANON LOCAL PORTÁTIL

ESTADO = DISEÑO VALIDADO / LISTO PARA PRUEBA OPERATIVA

## 1. Objetivo

Probar un modelo de trabajo Bot-ABAP donde el estado operativo de cada unidad de trabajo viaje en un archivo Markdown administrado por el humano, sin depender de memoria persistente del agente ni de una fuente operacional central para continuar el trabajo cotidiano.

El expediente debe permitir que otro humano, otro chat o una sesión futura pueda reconstruir qué se solicitó, qué se sabe, qué se decidió, dónde quedó el trabajo y qué corresponde hacer después.

## 2. Principios

1. Una unidad de trabajo mantiene un único expediente Markdown vigente.
2. El humano custodia el archivo vigente.
3. El chat no sustituye el expediente.
4. El expediente no sustituye Word, Excel, PDF, capturas, correos u otros artefactos de trabajo; los conecta y preserva los hechos que deben sobrevivir.
5. La estructura es estable y el contenido crece según necesidad y riesgo.
6. No se agregan campos vacíos solo porque podrían ser útiles en el futuro.
7. La ausencia de un dato que todavía no es necesario no bloquea el trabajo.
8. Cuando la ausencia de un dato aumenta el riesgo, el agente advierte al humano.
9. Solo se bloquea el alcance que realmente no puede continuar de forma segura o verificable.
10. Arriba vive la verdad vigente; abajo vive la historia que explica cómo se llegó a ella.
11. No inventar horas, estados, aprobaciones, versiones SAP, objetos, OTs, pruebas, decisiones ni resultados.
12. No mezclar clientes, tareas, transportes, decisiones ni evidencia entre expedientes.
13. Los roles [ABAP] y [ABAP.QA] siguen sujetos a activación y autoridad definidas por la gobernanza general; cargar un expediente no activa un rol.

## 3. Unidad documental

Tipos admitidos:

- `ACTIVIDAD`: trabajo que todavía no posee un identificador formal o que no necesita uno.
- `TICKET`: trabajo asociado a un número de ticket confirmado.
- `PROYECTO`: unidad de trabajo de alcance mayor identificada por un nombre de proyecto.

Nombres recomendados:

- `ACTIVIDAD-<nombre-corto>.md`
- `TICKET-<numero>.md`
- `PROYECTO-<nombre-corto>.md`

No utilizar sufijos como `v2`, `v7`, `FINAL` o equivalentes para expresar vigencia. La revisión documental se registra dentro del expediente.

## 4. Estructura obligatoria del expediente

El expediente usa exactamente seis secciones superiores:

1. `IDENTIDAD`
2. `SOLICITUD Y ALCANCE`
3. `CONTEXTO`
4. `ESTADO ACTUAL`
5. `BITÁCORA`
6. `EVIDENCIA Y REFERENCIAS`

No se crean secciones superiores permanentes independientes para especificación, análisis técnico, plan, transporte, pruebas, QA, feedback, control de cambio, handoff o cierre. Esa información aparece dentro de las seis secciones cuando corresponde.

Regla:

**La estructura es estable; el contenido es progresivo.**

## 5. IDENTIDAD

### 5.1 ACTIVIDAD

Ejemplo sintético:

```md
# ACTIVIDAD — Error en procesamiento automático

## 1. IDENTIDAD

Tipo: ACTIVIDAD
Título: Error en procesamiento automático
Cliente: CLIENTE-SINTETICO
Revisión del expediente: 1
Última actualización: <fecha/hora confirmada o autorizada>
```

No inventar un identificador temporal solo para completar el expediente.

### 5.2 TICKET

```md
# TICKET-8001

## 1. IDENTIDAD

Tipo: TICKET
ID: 8001
Título: Error en procesamiento automático
Cliente: CLIENTE-SINTETICO
Revisión del expediente: 4
Última actualización: <fecha/hora confirmada o autorizada>
```

### 5.3 PROYECTO

```md
# PROYECTO — Mejora proceso de pagos

## 1. IDENTIDAD

Tipo: PROYECTO
Título: Mejora proceso de pagos
Cliente: CLIENTE-SINTETICO
Revisión del expediente: 3
Última actualización: <fecha/hora confirmada o autorizada>
```

`En manos de` no pertenece a IDENTIDAD. Es estado operativo y vive en `ESTADO ACTUAL`.

Abrir o cargar un archivo no equivale por sí solo a recibir formalmente el trabajo.

## 6. Transición ACTIVIDAD → TICKET

Una actividad puede comenzar sin número de ticket.

Cuando el humano confirma posteriormente un ticket:

1. el mismo expediente cambia `Tipo: ACTIVIDAD` a `Tipo: TICKET`;
2. incorpora el `ID` confirmado;
3. conserva solicitud, alcance, contexto, checklist, avance, bitácora, horas y evidencia;
4. registra el hecho material en BITÁCORA;
5. en la siguiente consolidación adopta el nombre `TICKET-<numero>.md`;
6. el nuevo nombre sustituye al anterior como archivo vigente bajo custodia humana.

La asignación de ticket no reinicia el trabajo ni cambia por sí sola alcance, avance o estado.

## 7. Revisión del expediente

`Revisión del expediente` identifica consolidaciones materiales del Markdown.

Aumenta cuando se consolida y se devuelve un `.md` actualizado, no por cada mensaje de chat ni por cada pequeño cambio durante una sesión.

La revisión documental no equivale a:

- versión SAP;
- versión de perfil de cliente;
- número de ticket;
- versión de tarea;
- identificador de transporte.

### 7.1 Varias copias aparentes de una misma unidad

La mera carga de varios `.md` no implica conflicto. Primero se interpreta la instrucción humana.

Si el humano solicita comparación, reporte, resumen o análisis transversal, los archivos se usan conforme a esa instrucción y en solo lectura por defecto.

Solo cuando una contradicción o ambigüedad impide ejecutar de forma fiable la instrucción, el agente solicita aclaración.

Si la instrucción exige determinar cuál copia debe modificarse y existen versiones incompatibles, no se elige silenciosamente una.

## 8. SOLICITUD Y ALCANCE

La entrada original se conserva literalmente:

```md
## 2. SOLICITUD Y ALCANCE

### Solicitud original
"<entrada original literal>"
```

La definición vigente se normaliza progresivamente:

```md
### Definición vigente

Necesidad:
<qué debe resolverse>

Resultado esperado:
<qué se necesita conseguir>
```

Agregar alcance, exclusiones, requisitos y criterios de aceptación cuando sean necesarios para gobernar o verificar el trabajo.

Si no existe definición verificable suficiente para continuar con seguridad, aplicar `SPEC_REQUIRED`.

Si falta un dato imprescindible para una decisión concreta, aplicar `ERR_INSUFFICIENT_CONTEXT` solo al alcance afectado.

Una especificación Word u otro artefacto puede seguir siendo la fuente detallada. El expediente no necesita copiarla completa, pero debe preservar los hechos, decisiones y referencias imprescindibles para continuar.

## 9. CONTEXTO

`CONTEXTO` conserva únicamente los antecedentes que el siguiente humano necesita para comprender o continuar correctamente el trabajo.

Puede incluir, cuando sea relevante:

- módulo SAP;
- proceso;
- sistema/mandante;
- versión SAP o componentes;
- objetos relevantes;
- interfaces;
- restricciones técnicas;
- transportes;
- otros antecedentes operativos.

No incluir por defecto campos vacíos como:

- `SAP_BASIS:`
- `Objetos:`
- `OT:`
- `Pruebas:`
- `Riesgos:`

Un dato aparece cuando se vuelve útil o necesario.

Las decisiones dependientes de versión siguen requiriendo el perfil/contexto confirmado definido por la gobernanza general.

## 10. ESTADO ACTUAL

Objetivo: responder rápidamente:

- ¿Dónde quedó esto?
- ¿Quién tiene el trabajo?
- ¿Qué está bloqueado?
- ¿Qué corresponde hacer ahora?

Base:

```md
## 4. ESTADO ACTUAL

Estado: EN_ANALISIS
En manos de: <humano actual>

Resumen:
<estado vigente resumido>

Siguiente acción:
<una acción concreta>
```

Mientras la tarea permanezca abierta debe existir una siguiente acción concreta, salvo que el estado mismo determine otra condición.

Los estados de tarea son los definidos por la gobernanza general. Después de la entrega funcional se usa exactamente:

`DESARROLLO ENTREGADO - EN PRUEBAS DE USUARIO`

La falta de respuesta durante pruebas de usuario no equivale a aprobación ni cierre.

## 11. Relevamiento inicial

Cuando no se carga un `.md` y existe una actividad concreta, realizar un relevamiento breve y proporcional.

Solicitar únicamente lo necesario para comenzar, por ejemplo:

- tema o descripción breve;
- tipo: ticket, proyecto u otra actividad;
- cliente;
- módulo SAP si aplica;
- número de ticket si existe;
- fecha y hora de inicio si el humano efectivamente comenzará a trabajar y la bitácora se gestionará.

El número de ticket no es obligatorio para iniciar.

Si todavía no existe, crear `Tipo: ACTIVIDAD`.

No solicitar OT, objetos, versión técnica u otros datos futuros salvo que ya sean necesarios.

Después del relevamiento:

`SIN CONTEXTO → RELEVAMIENTO BREVE → .md BASE → INICIAR o DERIVAR`

Una pregunta genérica o consulta aislada no obliga a crear expediente.

## 12. Expediente mínimo inicial

Ejemplo sintético con ticket:

```md
# TICKET-8001

## 1. IDENTIDAD

Tipo: TICKET
ID: 8001
Título: <descripción breve>
Cliente: CLIENTE-SINTETICO
Revisión del expediente: 1
Última actualización: <fecha/hora confirmada o autorizada>

## 2. SOLICITUD Y ALCANCE

### Solicitud original
"<entrada literal del humano>"

### Definición vigente

Necesidad:
<descripción inicial breve>

## 3. CONTEXTO

Módulo SAP: <solo si aplica y está disponible>

## 4. ESTADO ACTUAL

Estado: EN_ANALISIS
En manos de: <humano actual>

Resumen:
Expediente creado a partir del relevamiento inicial.

Siguiente acción:
Completar entendimiento de la actividad.

## 5. BITÁCORA

Sin eventos materiales registrados.

## 6. EVIDENCIA Y REFERENCIAS

Sin artefactos registrados.
```

No abrir un tramo horario solo por crear el archivo.

## 13. INICIAR y DERIVAR

### 13.1 INICIAR

`INICIAR` significa comenzar efectivamente el trabajo.

Solo en ese momento se abre un tramo horario si se gestiona tiempo.

Si la hora de inicio no está confirmada, solicitarla en esa frontera operacional.

### 13.2 DERIVAR

`DERIVAR` prepara la continuidad por otro humano.

No supone que el análisis o ejecución haya comenzado.

El handoff:

1. cierra el tramo activo del humano que entrega, si existe;
2. conserva pendientes y bloqueos;
3. consolida el expediente;
4. registra el handoff en BITÁCORA;
5. entrega el `.md` actualizado;
6. cambia `En manos de` únicamente cuando la transferencia al siguiente humano está confirmada.

Preparar una derivación no equivale a confirmar que el destinatario ya recibió el trabajo.

El nuevo humano inicia su propio tramo únicamente cuando efectivamente comienza a trabajar.

## 14. ENTENDIMIENTO

Objetivo: comprender suficientemente qué ocurre y qué resultado necesita el humano.

Pregunta base:

**Cuéntame con tus palabras qué ocurre y qué necesitas resolver.**

Preguntar de forma adaptativa solo por vacíos que impidan entender razonablemente el problema.

ENTENDIMIENTO termina cuando:

1. se comprende qué está ocurriendo;
2. se comprende qué resultado necesita el humano;
3. no existe una ambigüedad que haga imposible diseñar razonablemente el trabajo.

Un dato que pueda descubrirse durante la ejecución no bloquea el entendimiento; se transforma en actividad del Checklist Global.

Ejemplo:

```md
- [ ] Identificar objeto y lógica responsable.
```

Regla:

**ENTENDIMIENTO determina qué debemos resolver. DISEÑO DE TRABAJO determina cómo llegar a resolverlo.**

## 15. DISEÑO DE TRABAJO y Checklist Global

El Checklist Global representa el 100 % del trabajo actualmente planificado.

Debe ser proporcional al riesgo y suficientemente completo para orientar la ejecución sin exigir información que todavía no existe.

### 15.1 Cobertura semántica obligatoria

Todo Checklist Global debe cubrir, explícitamente o mediante justificación, los cinco dominios:

- ANÁLISIS
- DISEÑO
- DESARROLLO
- PRUEBAS
- HITOS DE CIERRE

Estos dominios son cobertura semántica, no fases obligatorias.

El humano puede diseñar menos o más fases globales si colectivamente cubren los cinco dominios.

Ejemplo sin desarrollo ABAP:

```md
#### 1. Diagnóstico
Cobertura: ANÁLISIS + DISEÑO

#### 2. Resolución funcional
Cobertura: DESARROLLO + PRUEBAS

Justificación:
La resolución es funcional y no requiere desarrollo ABAP.

#### 3. Cierre
Cobertura: HITOS DE CIERRE
```

### 15.2 Estados del Checklist Global

- `BORRADOR`
- `LISTO PARA VALIDACIÓN`
- `CERTIFICADO`

El agente puede proponer `LISTO PARA VALIDACIÓN` cuando:

1. el trabajo conocido está suficientemente dividido;
2. las actividades relevantes están representadas;
3. los cinco dominios están cubiertos o justificados;
4. cada punto global tiene significado de término;
5. existe una prioridad inicial razonable;
6. no existe una omisión conocida que vuelva engañoso el mapa.

Solo el humano certifica:

`CHECKLIST: CERTIFICADO`

La certificación significa:

**Este árbol representa el 100 % del trabajo planificado actualmente.**

No autoriza por sí sola desarrollo, transporte, producción, QA, control de cambio ni cierre.

### 15.3 Criterio de término

Cada punto global debe indicar cuándo se considera completo.

Ejemplo:

```md
#### 1. Diseño

Termina cuando:
Existe una solución definida y suficiente para ejecutar.

- [ ] Confirmar escenarios relevantes.
- [ ] Determinar causa.
- [ ] Definir solución.
```

## 16. Estados de nodos del checklist

Los estados operativos persistentes de actividades son:

- `PENDIENTE`
- `EN CURSO`
- `BLOQUEADA`
- `COMPLETADA`
- `NO APLICA`

`DISPONIBLE` no se persiste; es una condición calculada.

Una actividad está disponible cuando:

- está `PENDIENTE`;
- no tiene bloqueo;
- sus dependencias están satisfechas.

Normalmente existe un solo foco `EN CURSO` por expediente.

Si el humano cambia de foco y la actividad anterior no terminó ni quedó bloqueada, vuelve a `PENDIENTE`.

Los estados del checklist no sustituyen los estados de tarea definidos por la gobernanza general.

## 17. Estado derivado de padres

Para un nodo padre:

- todos los hijos aplicables `COMPLETADA` → `COMPLETADA`;
- todos los hijos `NO APLICA` → `NO APLICA`;
- existe trabajo iniciado/completado y queda trabajo pendiente → `EN CURSO`;
- nada comenzó y existe trabajo ejecutable → `PENDIENTE`;
- todo el trabajo restante está bloqueado y no existe alternativa ejecutable → `BLOQUEADA`.

Un padre no se bloquea solo porque uno de sus hijos esté bloqueado.

## 18. Cálculo de avance

El avance se calcula de abajo hacia arriba.

### 18.1 Hojas

- `COMPLETADA` = 100 %
- `PENDIENTE` = 0 %
- `EN CURSO` = 0 %
- `BLOQUEADA` = 0 %
- `NO APLICA` = excluida del denominador cuando está justificada

### 18.2 Padres

Cada padre es el promedio de sus hijos directos aplicables.

El Global es el promedio de los puntos superiores certificados del Checklist Global.

Los hermanos tienen igual peso por defecto.

La prioridad no modifica el porcentaje.

Mantener decimales internamente y mostrar el entero más cercano.

Si una actividad es demasiado grande para que 0/100 represente razonablemente el avance, dividirla en actividades hijas. No asignar porcentajes subjetivos como “60 % realizado”.

Un bloqueo permanece en el denominador con 0 % y por tanto no infla artificialmente el avance.

Si todos los hijos son justificadamente `NO APLICA`, el padre se considera `NO APLICA` y se excluye del nivel superior.

Editar el checklist puede aumentar o disminuir el avance calculado.

## 19. Prioridades

La prioridad se aplica a actividades ejecutables.

En flujos lineales simples, el orden del checklist representa el orden preferente y no es necesario agregar metadatos.

Cuando existen alternativas paralelas o el orden no es evidente:

```md
- [ ] Validar escenario especial.
  Prioridad: 1

- [ ] Preparar datos de prueba.
  Prioridad: 2
```

Menor número = mayor prioridad.

Primero se calcula disponibilidad; después se aplica prioridad.

Una actividad bloqueada conserva su prioridad, pero no se propone como ejecutable.

Cuando se desbloquea, recupera su prioridad diseñada.

El humano puede cambiar el foco sin necesariamente cambiar la prioridad diseñada, o puede repriorizar expresamente el plan.

Cambiar prioridad no cambia el porcentaje de avance.

Regla:

**El diseño establece el orden preferente; la disponibilidad determina qué puede hacerse; el humano decide qué se hace realmente.**

## 20. Checklist Operativo

El Checklist Global es el mapa maestro.

El Checklist Operativo es el subconjunto que el humano decide trabajar ahora.

Existe un solo Checklist Operativo vigente por expediente.

No crear silenciosamente uno nuevo si el anterior conserva pendientes. Antes debe retomarse, replanificarse o postergarse explícitamente.

Ejemplo:

```md
### Checklist Operativo — <fecha>

- [x] Identificar lógica responsable.

- [ ] Revisar determinación.
  Estado: EN CURSO

- [ ] Preparar caso de prueba.
```

El cumplimiento de una jornada no redefine el denominador Global.

Al terminar un tramo, no dejar una actividad artificialmente `EN CURSO` si nadie está trabajando en ella. Si no terminó ni está bloqueada, vuelve a `PENDIENTE`.

Los pendientes se conservan y se presentan al retomar antes de crear trabajo nuevo.

## 21. Encabezado operativo durante REALIZACIÓN

Durante la ejecución, las respuestas deben ubicar al humano rápidamente en el árbol.

Ticket sintético:

```text
🎫 CLIENTE-SINTETICO | Ticket 8001 (Descripción breve) | Global 42% | Fase 2/3 Desarrollo (60%) | Subfase 2/4 Ajuste (50%)
▶️ Prioridad: Ejecutar prueba integrada | 🟢 Disponibles: 2 | 🔴 Bloqueadas: 1
```

Proyecto sintético:

```text
🛠️ CLIENTE-SINTETICO | Proyecto "Mejora proceso" | Global 42% | Fase 2/3 Diseño (60%)
▶️ Prioridad: Definir solución | 🟢 Disponibles: 2 | 🔴 Bloqueadas: 0
```

El nombre del cliente debe provenir del expediente. No usar literalmente la palabra `CLIENTE` como sustituto del nombre.

Si el cliente está ausente o no confirmado, mostrar `NO DEFINIDO`; no inventarlo.

Si el humano trabaja excepcionalmente en una actividad distinta de la prioridad diseñada, distinguir:

- `En curso`
- `Prioridad diseñada`

No inventar un número de ticket para una ACTIVIDAD.

## 22. Bloqueos y dependencias

Al bloquear una actividad:

```md
- [ ] Ejecutar prueba integrada.
  Estado: BLOQUEADA
  Motivo: falta antecedente requerido.
  Desbloquea cuando: se disponga del antecedente.
```

Las dependencias se registran solo cuando aportan valor:

```md
- [ ] Ejecutar regresión.
  Depende de: Ejecutar prueba integrada.
```

El bloqueo se propaga únicamente a dependientes reales.

Las actividades independientes permanecen disponibles.

Una tarea completa pasa a `BLOQUEADA` solo cuando no queda trabajo aplicable ejecutable.

### 22.1 Desbloqueo

Cuando desaparece la causa:

`BLOQUEADA → PENDIENTE → DISPONIBLE (calculado)`

Reevaluar recursivamente dependencias.

El desbloqueo no cambia silenciosamente el foco actual.

Si se desbloquea una actividad de mayor prioridad, informar y dejar al humano decidir si cambia el foco.

## 23. Cierre de fase o subfase

Llegar al final de una fase dispara una revisión de cierre.

Una fase/subfase se considera completada únicamente cuando:

1. todos sus hijos aplicables están `COMPLETADA` o justificadamente `NO APLICA`; y
2. se cumple su criterio `Termina cuando`.

Si existe cualquier trabajo aplicable pendiente, `EN CURSO` o bloqueado, no se declara cierre.

Si todo lo restante está bloqueado y no existe alternativa, la fase queda `BLOQUEADA`, no completada.

En la revisión de fin de fase mostrar únicamente el checklist de ese contexto, los pendientes, bloqueos, impacto y alternativas ejecutables.

Si el humano determina que una actividad ya no corresponde, debe resolverla explícitamente como completada, no aplica justificado, replanificada o mediante el tratamiento de alcance aplicable. No ocultarla para cerrar.

## 24. Edición humana del plan

El humano puede editar:

- estructura;
- actividades;
- prioridades;
- dependencias;
- estados;
- puntos cerrados;
- Checklist Global;
- Checklist Operativo.

El agente no bloquea una edición humana por ser tardía, pero advierte impactos relevantes, por ejemplo:

- trazabilidad;
- pruebas anteriores;
- dependencias;
- entregables;
- cierre;
- retrabajo;
- avance calculado.

Después de una edición confirmada:

1. actualizar el árbol vigente;
2. recalcular porcentajes;
3. recalcular disponibilidad;
4. propagar bloqueos/dependencias;
5. actualizar prioridad visible;
6. registrar en BITÁCORA si el cambio es material.

No crear `Checklist v1`, `Checklist v2` ni copias históricas del plan.

Existe un único checklist vigente. La historia material se conserva en BITÁCORA.

Editar el checklist no autoriza por sí solo una ampliación/reducción de alcance, transporte, producción, cierre u otro gate.

## 25. Tiempo y bitácora

Las horas solo se consideran confirmadas cuando:

- el humano las informa expresamente; o
- existe una fuente autorizada inequívoca.

Nunca inferir trabajo por distancia temporal entre mensajes.

Mantener máximo un tramo activo por usuario cuando se gestiona bitácora.

Solo los tramos cerrados participan en totales.

Si falta hora de inicio o fin, la duración es `NO DEFINIDA`.

Solicitar hora en fronteras operacionales relevantes:

- inicio o reanudación;
- pausa;
- cambio de ticket/proyecto;
- handoff;
- fin de jornada/tramo;
- antes de una consolidación que dejaría accidentalmente un tramo abierto.

No abrir un tramo por crear o cargar un expediente.

No entregar como consolidado un expediente con un tramo accidentalmente abierto sin advertir al humano.

BITÁCORA registra acontecimientos materiales, no la conversación.

Registrar, según corresponda:

- análisis/diagnóstico material;
- decisiones;
- estimaciones y aprobaciones;
- implementación;
- pruebas y resultados;
- feedback;
- FALLO / CONTROL DE CAMBIO;
- transportes;
- bloqueos relevantes;
- handoff;
- identificación posterior de ticket;
- cierres de puntos globales;
- correcciones documentales materiales.

Las correcciones históricas se realizan mediante nueva entrada que corrige o sustituye; no se borra silenciosamente historia material.

## 26. Handoff

Un handoff vive en BITÁCORA, no como sección superior.

Ejemplo:

```md
### HANDOFF — <fecha>

De: <humano A>
A: <humano B>

Situación:
<dónde quedó>

Continuar con:
<siguiente acción>

Expediente entregado:
SÍ
```

`En manos de` cambia solo cuando la transferencia está confirmada.

El estado de la tarea no cambia necesariamente por el handoff.

El nuevo humano no hereda automáticamente el tramo horario del anterior.

## 27. Cargar y retomar un expediente

Al cargar un `.md`, el agente reconstruye silenciosamente:

1. identidad;
2. solicitud y definición vigente;
3. contexto relevante;
4. estado actual;
5. Checklist Global y Operativo;
6. avance;
7. bloqueos/dependencias;
8. último handoff;
9. eventos recientes necesarios;
10. evidencia/referencias aplicables.

No volver a interrogar al humano por datos ya disponibles en el expediente.

Cargar el archivo no significa iniciar trabajo ni abrir horas.

Si el humano indica que continuará, abrir el nuevo tramo solo con hora confirmada.

Si existe una discrepancia material entre `En manos de` y lo que informa el humano, aclararla antes de alterar esa verdad vigente.

## 28. Varios expedientes y operaciones transversales

La carga de varios `.md` normalmente puede responder a:

- comparación;
- reportes;
- backlog;
- horas;
- riesgos;
- búsqueda;
- resúmenes;
- análisis transversal.

La instrucción específica del humano define la operación.

Por defecto, estas operaciones son de SOLO LECTURA sobre los expedientes.

No modificar archivos fuente salvo solicitud expresa.

No declarar conflicto solo porque existan varias revisiones o archivos similares.

Si durante la operación aparecen contradicciones o ambigüedades que afectan el resultado solicitado, pedir aclaración únicamente sobre el punto afectado.

## 29. Artefactos, evidencia y referencias

El `.md` no reemplaza artefactos de trabajo.

Los conecta:

```md
## 6. EVIDENCIA Y REFERENCIAS

- Especificacion_demo.docx
  Tipo: especificación funcional
  Estado: vigente
  Relevancia: define el comportamiento solicitado.
```

No exigir hash, MIME, ruta u otra metadata de bajo valor por defecto.

Un nombre de archivo sin contexto es evidencia débil; registrar qué es, por qué importa o qué demuestra.

Si un artefacto estaba registrado en el expediente pero no fue cargado en la sesión actual:

- existencia del artefacto: `CONFIRMADO POR EXPEDIENTE`;
- contenido: `NO DISPONIBLE EN ESTA SESIÓN`.

Los hechos importantes viven en el cuerpo del expediente; la evidencia demuestra esos hechos.

## 30. Microsoft 365 u otro contexto de plataforma

El contexto automático de plataforma puede ayudar a identificar nombres, relaciones o antecedentes, pero:

`CONTEXTO DE PLATAFORMA ≠ CANON ≠ AUTORIDAD`

No persistir metadata de conveniencia que no necesite sobrevivir.

Cuando una decisión o hecho deba sobrevivir, registrarlo explícitamente en el expediente con su procedencia cuando el riesgo lo justifique.

Procedencias útiles:

- `CONFIRMADO POR HUMANO`
- `CONFIRMADO POR EXPEDIENTE`
- `CONFIRMADO POR CONTEXTO DE PLATAFORMA`
- `INFERIDO`
- `NO DISPONIBLE`

Las inferencias controladas se presentan al humano como:

**Observación a validar:**

y no se tratan como confirmadas hasta validación humana.

## 31. FALLO y CONTROL DE CAMBIO

Antes de modificar código por feedback:

- `FALLO`: incumplimiento del alcance, requisito o criterio vigente;
- `CONTROL DE CAMBIO`: modificación o ampliación del alcance, requisitos, comportamiento, objetos, interfaces, datos, versión o criterios.

Un fallo puede volver a desarrollo dentro de la especificación vigente.

Un control de cambio sigue el gate definido por la gobernanza general:

`registrar → analizar impacto → estimar → informar → obtener autorización → actualizar definición/especificación → implementar`

Editar el checklist no sustituye este gate.

## 32. Pruebas

Las pruebas se derivan de:

- definición/especificación;
- criterios de aceptación;
- riesgo;
- versión/contexto SAP aplicable.

Un resultado `PASS` requiere resultado observado y evidencia suficiente.

Ausencia de error, activación correcta, timeout o respuesta parcial no bastan por sí solos.

Los resultados materiales pueden registrarse en BITÁCORA y la evidencia correspondiente en `EVIDENCIA Y REFERENCIAS`, sin necesidad de crear una sección superior de pruebas.

## 33. Transportes

Una OT aparece solo cuando aplica.

No mostrar `OT: NO APLICA` durante todo el expediente como relleno.

Si la resolución final no requirió modificación SAP y dejar constancia tiene valor:

```md
Transporte: NO APLICA
Motivo: resolución sin modificación SAP.
```

Las órdenes reales se rigen por la fuente privada y reglas de transporte definidas por la gobernanza general.

`LIBERADA` requiere evidencia positiva.

Liberación no equivale a importación en producción.

## 34. Consolidación y entrega del `.md`

El humano gobierna el ciclo de trabajo. El agente mantiene la consistencia documental.

El humano puede solicitar un `.md` actualizado en cualquier momento.

### 34.1 Disparador automático principal

Cada cierre de un punto superior del Checklist Global dispara automáticamente:

1. revisar/cerrar el contexto operativo correspondiente;
2. recalcular avance;
3. actualizar Checklist Global;
4. consolidar estado, bitácora, bloqueos, decisiones y evidencia;
5. aumentar `Revisión del expediente`;
6. generar y entregar el `.md` actualizado;
7. preguntar si el humano desea enviarlo por correo y, en ese caso, a quién.

El cierre del último punto Global, con 100 %, sigue el mismo proceso.

100 % de checklist no equivale por sí solo a cierre de tarea.

### 34.2 DERIVAR

DERIVAR también exige consolidar y entregar el `.md`, porque el expediente es el mecanismo de continuidad entre humanos.

### 34.3 Pausa, cambio de trabajo y fin de jornada

Estas fronteras obligan a mantener coherencia temporal y a conservar pendientes.

No generan automáticamente un nuevo `.md` salvo que:

- el humano lo solicite;
- coincidan con el cierre de un punto Global; o
- formen parte de un DERIVAR.

## 35. Correo y otros efectos externos

Generar el expediente no autoriza enviarlo.

Antes de correo u otro efecto externo:

- confirmar que el humano desea el envío;
- confirmar destinatarios;
- respetar permisos y reglas aplicables.

Nunca enviar automáticamente solo por cerrar un punto Global.

## 36. Cierre de la tarea

Checklist Global en 100 % significa que el trabajo planificado está completado según el árbol vigente.

No significa automáticamente:

- aceptación funcional;
- producción;
- importación de transporte;
- cierre formal.

La tarea se cierra únicamente conforme a los gates de cierre definidos por la gobernanza general.

## 37. Flujo de referencia

```text
SIN CONTEXTO
   ↓
RELEVAMIENTO BREVE
   ↓
.md BASE
   ↓
INICIAR ───────────── DERIVAR
   ↓                      ↓
ENTENDIMIENTO           HANDOFF
   ↓
DISEÑO DE TRABAJO
   ↓
CHECKLIST GLOBAL
   ↓
COBERTURA:
ANÁLISIS · DISEÑO · DESARROLLO · PRUEBAS · HITOS DE CIERRE
   ↓
CERTIFICACIÓN HUMANA
   ↓
REALIZACIÓN
   ↓
CHECKLIST OPERATIVO
   ↓
EJECUCIÓN
   ├─ COMPLETADA
   ├─ BLOQUEADA → propagar dependencias reales
   └─ DISPONIBLE → proponer según prioridad
   ↓
REVISIÓN / CIERRE DE PUNTO GLOBAL
   ↓
.md AUTOMÁTICO + CONSULTA DE ENVÍO
   ↓
SIGUIENTE PUNTO GLOBAL
   ↓
...
   ↓
CHECKLIST GLOBAL 100 %
   ↓
.md FINAL AUTOMÁTICO
   ↓
GATES DE CIERRE
   ↓
CIERRE HUMANO
```

## 38. Plantilla estructural

```md
# <IDENTIFICACIÓN VISIBLE>

## 1. IDENTIDAD

Tipo: <ACTIVIDAD | TICKET | PROYECTO>
<campos disponibles y relevantes>
Revisión del expediente: <n>
Última actualización: <fecha/hora confirmada o autorizada>

## 2. SOLICITUD Y ALCANCE

### Solicitud original
"<entrada original literal>"

### Definición vigente

Necesidad:
<qué debe resolverse>

Resultado esperado:
<cuando ya esté definido>

<alcance, exclusiones, requisitos y criterios solo cuando sean necesarios>

## 3. CONTEXTO

<solo antecedentes necesarios para comprender o continuar>

## 4. ESTADO ACTUAL

Estado: <estado vigente>
En manos de: <humano actual>

Resumen:
<dónde quedó>

Siguiente acción:
<una acción concreta>

<bloqueos si existen>

<avance, Checklist Global y Checklist Operativo cuando existan>

## 5. BITÁCORA

<eventos materiales>

## 6. EVIDENCIA Y REFERENCIAS

<artefactos y fuentes relevantes>
```

## 39. Pruebas sintéticas del diseño

El diseño fue recorrido conceptualmente con tres escenarios sintéticos:

1. cambio ABAP con pruebas y transporte;
2. resolución funcional sin desarrollo ABAP ni OT;
3. actividad iniciada sin ticket que posteriormente recibe un número de ticket.

Resultado de diseño: los tres escenarios pueden representarse con la misma estructura de seis secciones, sin migración de plantilla y sin campos permanentes innecesarios.

Este resultado valida la coherencia del diseño documental, no constituye evidencia de una prueba operativa real del agente.

## 40. Controles de seguridad

Mientras el repositorio canónico sea público:

- no persistir clientes reales;
- no persistir tickets reales;
- no persistir SIDs/mandantes reales;
- no persistir OTs reales;
- no persistir código de cliente;
- no persistir logs, dumps, capturas o evidencia identificable;
- no persistir contactos reales;
- no persistir credenciales o secretos;
- usar únicamente ejemplos sintéticos.

Los expedientes reales deberán vivir en la fuente privada/local autorizada y bajo custodia humana.

## 41. Siguiente gate

Con el diseño documental ya validado e incorporado al canon experimental, el siguiente gate es probar su comportamiento operativo antes de utilizar el modelo con operación real.

1. preparar el prompt/comportamiento del agente experimental;
2. ejecutar una prueba operativa sintética end-to-end con generación, carga, handoff, consolidación y análisis transversal;
3. evaluar fricción de uso y ajustar el diseño únicamente mediante el control documental aplicable.

NEXT_GATE = PREPARAR AGENTE EXPERIMENTAL Y EJECUTAR PRUEBA OPERATIVA SINTÉTICA END-TO-END.
