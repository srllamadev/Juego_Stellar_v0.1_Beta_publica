> **PROMPT PARA EL AGENTE — TAREA / QA Y PRUEBAS INTEGRALES**
>
> Estoy trabajando en el proyecto **Impulso Stellar**, un RTS roguelite competitivo PvPvE para navegador.
>
> La responsabilidad dentro del equipo es **desarrollo y pruebas integrales**.
>
> En la reunión del 25/09 se acordó:
>
> - Cámara estilo MOBA: cada jugador debe ver su propia base en la parte inferior.
> - Para la demo se utilizará un mapa fijo.
> - Las unidades tendrán vida, velocidad y daño.
> - Estos valores y el resultado de las acciones deben ser calculados/validados por el servidor.
> - El objetivo inmediato para domingo/lunes es tener **naves moviéndose correctamente sobre un mapa gris**.
> - Ismael trabaja Phaser + mapa gris y aspecto de las naves.
> - Orlando trabaja sala de campaña R1 y revisión del contrato.
> - Diego + Hans trabajan balance v0.1: vida, daño, velocidad y costos.
> - Debo realizar el **cuadro de pruebas** y revisar la integración.
> - Funciones como partidas personalizadas, teclas configurables, idiomas y mapas aleatorios son posteriores a la demo y NO deben distraernos ahora.
>
> ## TU OBJETIVO
>
> Ayúdame a ejecutar mi responsabilidad de **QA / pruebas integrales** del proyecto.
>
> Antes de modificar cualquier archivo:
>
> 1. Analiza completamente el repositorio.
> 2. Identifica su estructura, ramas disponibles, scripts, README, package.json, workspace, aplicaciones cliente/servidor, tests existentes y estado actual.
> 3. No supongas nombres de archivos ni arquitecturas que no existan.
> 4. No elimines ni reestructures código existente.
> 5. No hagas `merge`, `push`, `rebase` ni cambios destructivos sin indicármelo primero.
> 6. Si tienes acceso a GitHub y existe una invitación pendiente al repositorio, indícame exactamente qué invitación encontraste y ayúdame a aceptarla. Si no puedes aceptarla directamente por permisos/autenticación, explícame el paso exacto que debo realizar manualmente y continúa con el análisis local.
>
> ---
>
> # FASE 1 — DIAGNÓSTICO DEL REPOSITORIO
>
> Primero quiero un reporte corto indicando:
>
> - Rama actual.
> - Estado de `git status`.
> - Último commit.
> - Estructura principal del proyecto.
> - Cómo se ejecuta frontend.
> - Cómo se ejecuta backend.
> - Cómo se ejecutan tests.
> - Qué partes ya funcionan.
> - Qué partes todavía están incompletas.
> - Si existe ya una versión identificable como `v0.01`, prototipo, training room, demo o equivalente.
>
> No modifiques código todavía.
>
> ---
>
> # FASE 2 — CREAR EL CUADRO DE PRUEBAS
>
> Crea dentro del repositorio una documentación de QA, preferentemente:
>
> `docs/qa/cuadro-pruebas-v0.01.md`
>
> Si ya existe una estructura equivalente de documentación, utiliza la existente en lugar de crear carpetas innecesarias.
>
> El cuadro debe tener como mínimo estas columnas:
>
> | ID | Módulo | Prueba | Precondición | Pasos | Resultado esperado | Resultado obtenido | Estado | Severidad | Evidencia | Responsable | Observaciones |
>
> Usa estos estados:
>
> - ✅ PASA
> - ❌ FALLA
> - ⚠️ PARCIAL
> - ⏳ BLOQUEADO
> - 🔲 PENDIENTE
>
> Severidades:
>
> - CRÍTICA
> - ALTA
> - MEDIA
> - BAJA
>
> ---
>
> # FASE 3 — PRUEBAS PRIORITARIAS PARA DOMINGO/LUNES
>
> Para el avance inmediato, céntrate primero en el prototipo de **mapa gris + movimiento de naves**.
>
> Crea y, cuando sea posible, ejecuta pruebas para:
>
> ### QA-MAP-001 — El mapa carga
> - Abrir el cliente.
> - Entrar a la escena jugable.
> - Verificar que el mapa fijo/gris aparece sin errores.
>
> ### QA-MAP-002 — Posición inicial de las bases
> - Verificar que existen dos bases.
> - Cada jugador debe visualizar su propia base en la parte inferior de su cámara.
> - La orientación debe sentirse tipo MOBA.
>
> ### QA-MAP-003 — Movimiento de una nave
> - Seleccionar una unidad.
> - Dar una orden de movimiento.
> - Confirmar que se desplaza hasta el destino válido.
>
> ### QA-MAP-004 — Varias unidades
> - Crear/utilizar varias naves.
> - Ordenar movimientos diferentes.
> - Comprobar que no desaparecen, duplican o quedan corruptas.
>
> ### QA-MAP-005 — Límites del mapa
> - Intentar mover una nave fuera del área jugable.
> - El servidor debe impedir destinos inválidos.
>
> ### QA-MAP-006 — Sincronización cliente-servidor
> - Comprobar que la posición autorizada por el servidor coincide con lo dibujado por Phaser.
> - El cliente no debe ser la autoridad de la simulación.
>
> ### QA-MAP-007 — Dos jugadores
> - Si el multiplayer ya está disponible, abrir dos clientes.
> - Comprobar que los movimientos de uno son visibles correctamente en el otro cuando corresponde.
>
> ### QA-MAP-008 — Cámara
> - Verificar desplazamiento de cámara.
> - Verificar zoom si ya está implementado.
> - Verificar perspectiva/orientación de ambos jugadores.
>
> ### QA-UNIT-001 — Vida
> - Confirmar que una unidad tiene atributo de vida.
>
> ### QA-UNIT-002 — Velocidad
> - Confirmar que diferentes valores de velocidad producen el comportamiento esperado.
>
> ### QA-UNIT-003 — Daño
> - Si el combate ya está implementado, comprobar que el daño lo calcula el servidor.
>
> ### QA-UNIT-004 — Autoridad del servidor
> - Intentar, mediante cliente o DevTools si corresponde, alterar posición, vida, velocidad o daño.
> - Verificar que el servidor no acepte estados arbitrarios enviados por el cliente.
>
> ---
>
> # FASE 4 — MATRIZ GENERAL HACIA LA DEMO DEL 7/10
>
> Además del prototipo inmediato, deja preparadas como PENDIENTES las pruebas de aceptación generales:
>
> ### Multijugador
> - Crear sala.
> - Unirse mediante código.
> - Dos jugadores listos.
> - Inicio de campaña.
> - Sincronización entre dos navegadores.
>
> ### Órdenes
> - Movimiento válido.
> - Movimiento inválido.
> - Orden sobre unidad ajena.
> - Orden duplicada.
> - Secuencia incorrecta.
> - Rate limit.
>
> ### Información por jugador
> - Información propia completa.
> - Información pública.
> - Rival visible.
> - Rival fuera de visión NO enviado al navegador.
>
> ### Reconexión
> - Cortar conexión durante aproximadamente 5 segundos.
> - La partida debe pausarse si esa funcionalidad ya está integrada.
> - Reconectar conservando asiento y unidades.
> - Recargar página y recuperar sesión.
> - Confirmar que órdenes generadas durante la desconexión no se ejecutan después.
> - No regresar durante 60 segundos → abandono.
> - Tercera desconexión → verificar comportamiento definido cuando sea implementado.
>
> ### Sectores
> - Sector 1.
> - Transición.
> - Sector 2.
> - Transición.
> - Sector 3.
> - Resultado final.
>
> ### Captura
> - Núcleo cerrado.
> - Núcleo habilitado.
> - Un jugador capturando.
> - Dos jugadores disputando.
> - Retirada y pérdida/decaimiento del progreso.
> - Captura completa.
>
> ### Economía
> - Metal.
> - Energía.
> - Costos.
> - Recursos insuficientes.
> - Producción de unidades.
>
> ### Cosméticos
> - Inventario sin alterar estadísticas.
> - Compra en testnet.
> - Propiedad.
> - Equipamiento.
> - Visualización del cosmético por el rival.
> - Mismo estado lógico de la partida con y sin cosméticos.
>
> ---
>
> # FASE 5 — EJECUCIÓN
>
> Para cada prueba que actualmente pueda realizarse:
>
> 1. Ejecuta el proyecto siguiendo los scripts reales del repositorio.
> 2. No inventes resultados.
> 3. Ejecuta los tests automáticos existentes.
> 4. Registra errores de consola/servidor relevantes.
> 5. Marca cada prueba como PASA, FALLA, PARCIAL, BLOQUEADO o PENDIENTE.
> 6. En `Resultado obtenido`, describe exactamente lo observado.
> 7. En `Evidencia`, coloca comandos, logs, test ejecutado, archivo relacionado o captura que yo deba tomar.
>
> Si una función todavía no existe, NO la marques como fallo. Utiliza:
>
> `🔲 PENDIENTE — funcionalidad todavía no integrada`
>
> o
>
> `⏳ BLOQUEADO — depende de trabajo de otro integrante`.
>
> ---
>
> # FASE 6 — REPORTE DE AVANCE PARA EL GRUPO
>
> Al terminar genera también:
>
> `docs/qa/avance_pruebas.md`
>
> Con esta estructura:
>
> ## Avance — QA
>
> **Fecha:** [fecha actual]
>
> **Versión / commit probado:** `[hash]`
>
> **Pruebas realizadas:** X  
> **Pasaron:** X  
> **Fallaron:** X  
> **Parciales:** X  
> **Bloqueadas:** X  
> **Pendientes:** X
>
> ### Funciona
> - ...
>
> ### Falla
> - ...
>
> ### Bloqueado por integración
> - ...
>
> ### Riesgos para el lunes
> - ...
>
> ### Siguiente prueba recomendada
> - ...
>
> Finalmente dame un mensaje corto listo para enviar al grupo por WhatsApp/Discord, por ejemplo:
>
> `Avance: probé la integración actual en [commit]. Mapa: [...]. Movimiento: [...]. Cliente/servidor: [...]. Tengo X pruebas OK, X fallos y X pendientes. Los bloqueos actuales son [...]. Cuadro actualizado en docs/qa/cuadro-pruebas-v0.01.md.`
>
> ---
>
> # IMPORTANTE
>
> No quiero que intentes desarrollar todas las funciones faltantes del juego.
>
> **Mi responsabilidad principal en esta tarea es QA, pruebas integrales y documentación de qué funciona y qué falla.**
>
> Si encuentras un error:
>
> 1. Reprodúcelo.
> 2. Documenta cómo reproducirlo.
> 3. Identifica la causa probable.
> 4. Señala qué módulo/equipo parece involucrado.
> 5. No cambies código del compañero automáticamente.
> 6. Solo propón o implementa una corrección si yo te autorizo después.
>
> Empieza ahora por **FASE 1: diagnóstico del repositorio** y después avanza con el cuadro de pruebas.

Se priorizaría que el agente te deje listo el diagnóstico + el archivo `cuadro-pruebas-v0.01.md`, aunque todavía muchas filas estén como `PENDIENTE` o `BLOQUEADO`. Eso ya demuestra que tu parte de QA está organizada y preparada para probar cada integración que suban Ismael, Orlando, Diego y Hans.