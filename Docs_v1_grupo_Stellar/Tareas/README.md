Revisando **todo el Brief de diseño v0.4**. Estas son las responsabilidades donde apareces explícitamente:

1. **Probar la v0.01 integrada y registrar qué funciona y qué falla.**  
   Es tu tarea principal de QA. Además, en el documento figura que tu invitación al repositorio todavía estaba pendiente de aceptar al 25 de septiembre. :chatgpt-content-reference{index="0"}

2. **Mantener el cuadro de QA desde la v0.01 hasta la demo.**  
   Uno de los criterios de aceptación exige que ningún flujo quede bloqueado y específicamente dice que **XYZ registra en un cuadro qué funciona y qué falla desde la v0.01**. :chatgpt-content-reference{index="1"}

3. **Participar con Diego en la decisión D03 de balance/captura.**  
   Tienes asignado, junto con Diego, revisar/decidir:
   - captura,
   - empate,
   - ingreso mínimo,
   - energía,
   - tope de flota.  
   La fecha indicada era **28 de septiembre**. :chatgpt-content-reference{index="2"}

4. **Trabajar con Ismael en aspectos técnicos de Phaser — D04.**  
   La decisión dice: **motor de render Phaser**, y todavía había que fijar:
   - tick,
   - rutas,
   - portátil/equipo de referencia.  
   Los responsables que aparecen son **XYZ e Ismael**. :chatgpt-content-reference{index="3"}

5. **Decidir con Diego si usar escuadrones o naves individuales — D08.**  
   Esta es importante para el prototipo del mapa gris. El documento dice que la decisión debe hacerse con el prototipo y, si el microcontrol no entra en plazo, se usarían escuadrones. :chatgpt-content-reference{index="4"} :chatgpt-content-reference{index="5"}

6. **Evaluar si el microcontrol entra en el plazo.**  
   En riesgos aparece específicamente: si el microcontrol no entra, **XYZ y Diego** deben usar escuadrones como respaldo y decidirlo el lunes 28. :chatgpt-content-reference{index="6"}

7. **Ayudar con la migración/integración de Phaser sin romper simulación ni estado.**  
   El documento identifica como riesgo el cambio desde el cliente Canvas hacia Phaser. La responsabilidad de **XYZ e Ismael** es que Phaser consuma la misma `viewFor`, sin tocar `sim` ni `state`. :chatgpt-content-reference{index="7"}

8. **Ayudar a asegurar el 1v1 si para el 2 de octubre no funcionan dos clientes.**  
   El plan de contingencia dice que, si para esa fecha no existen dos clientes funcionando, **Orlando y XYZ** deben frenar contenido nuevo y concentrarse en resolver el **1v1**. :chatgpt-content-reference{index="8"}

9. **Participar con Diego en pruebas de bola de nieve y captura estancada.**  
   Si aparece ese problema, ustedes deben revisar:
   - reset,
   - reroll limitado,
   - captura después del PvE,
   - que el Explorador no bloquee la captura. :chatgpt-content-reference{index="9"}

10. **QA de órdenes del servidor.**  
    En la sección R3 aparece la tarjeta **Y01**, vinculada a la validación de órdenes. Para la demo faltaban validaciones como `protocolVersion`, visibilidad del objetivo, rutas, recursos, fases y órdenes de atacar/mantener/capturar/producir/tecnología. :chatgpt-content-reference{index="10"}  
    Esto encaja directamente con tu papel de pruebas integrales, aunque el documento no desarrolla en estas páginas el detalle completo de la tarjeta Y01.

11. **Probar específicamente la reconexión/desconexión.**  
    Aunque R4 es principalmente de Orlando/backend, el documento ya establece casos que deben entrar en tu cuadro:
    - cortar red 5 s;
    - recargar página durante el sector;
    - hacer clic mientras está desconectado y comprobar que esas órdenes no se ejecuten;
    - no volver en 60 s → abandono;
    - tercera desconexión → no pausa y unidades en “mantener”. :chatgpt-content-reference{index="11"}

### Entonces

La responsabilidad queda:

**XYZ = QA integral + integración cliente/servidor + apoyo técnico en Phaser/movimiento + pruebas y decisiones jugables con Diego.**

Para **ahora mismo**, yo separaría tus tareas en este orden:

| Prioridad | Tu tarea |
|---|---|
| 🔴 Ahora | Aceptar invitación del repo |
| 🔴 Ahora | Crear cuadro de pruebas v0.01 |
| 🔴 Domingo/Lunes | Probar mapa gris + movimiento de naves |
| 🔴 Domingo/Lunes | Probar Phaser + `viewFor` sin romper `sim/state` |
| 🔴 Lunes 28 | Decidir con Diego: naves individuales vs escuadrones |
| 🟠 Lunes 28 | Revisar D03: captura, empate, energía y límites |
| 🟠 Después | Probar dos clientes / 1v1 |
| 🟠 Después | Probar órdenes válidas e inválidas |
| 🟡 Después | Reconexión, abandono y órdenes durante desconexión |
| 🟡 Playtest | Detectar bola de nieve/captura estancada |
| 🟢 Hasta 7/10 | Mantener actualizado el cuadro QA hasta la demo |

Y el **hito inmediato** del equipo es claro: para el lunes deben existir **unidades moviéndose en el mapa gris**, además de tomar la decisión entre escuadrones y naves individuales. :