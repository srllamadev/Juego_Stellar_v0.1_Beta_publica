### Revisión requisito por requisito

| Requisito | Tu implementación | Estado |
|---|---|---|
| Fork del repositorio | `srllamadev/rwa-launchpad-bootcamp` | ✅ |
| Trabajar en `dia-3` | Cambios realizados en `dia-3` | ✅ |
| Crear `AmountTooLow` | `AmountTooLow = 7` | ✅ |
| Rechazar `< 500` | `if payment_amount < 500` | ✅ |
| Inversión 100 falla | Test + prueba en testnet | ✅ |
| Inversión 500 funciona | Test + prueba en testnet | ✅ |
| Desplegar en testnet | Contrato desplegado | ✅ |
| Inicializar contrato | Ejecutado correctamente | ✅ |
| Agregar inversionista a whitelist | Ejecutado | ✅ |
| Consultar balance | Resultado `5` | ✅ |
| Link Stellar Expert exitoso | Lo tienes | ✅ |
| Video ≤ 2 min o capturas | Falta preparar/entregar | ⏳ |

En el código público se puede comprobar directamente que agregaste el error:

```rust
AmountTooLow = 7,
```

y que `check_variation_gate` rechaza inversiones menores a 500:

```rust
if payment_amount < 500 {
    return Err(Error::AmountTooLow);
}
```

Además, `invest()` llama a esa validación antes de continuar. :chatgpt-content-reference{index="1"}

También están los dos tests que te pedían: el de `100` espera `Error(Contract, #7)` y el de `500` comprueba que se generan `5` RWA y que el balance queda en `5`. :chatgpt-content-reference{index="2"}

Y en tus pruebas de testnet ya quedó demostrado el flujo: la inversión de `100` produjo `Error(Contract, #7)`, mientras que la de `500` generó una transacción exitosa. :chatgpt-content-reference{index="3"} Luego consultaste el balance y obtuviste `"5"`. :chatgpt-content-reference{index="4"}

## Qué mostraría yo en el video

Como tu consigna actual dice **máximo 2 minutos**, ignora el `DEMO.md` antiguo del repositorio que habla de 3 minutos. :chatgpt-content-reference{index="5"}

Hazlo de unos **1:20–1:40 minutos**. No necesitas explicar absolutamente todo.

**0:00–0:15 — GitHub**

Entra a:

[Tu repositorio de GitHub](https://github.com/srllamadev/rwa-launchpad-bootcamp?utm_source=chatgpt.com)

Di algo como:

> “Este es mi fork del repositorio de RWA Launchpad. Trabajé en la carpeta día 3.”

Entra rápidamente a:

`dia-3/src/lib.rs`

Muestra estas dos cosas:

```rust
AmountTooLow = 7
```

y:

```rust
if payment_amount < 500 {
    return Err(Error::AmountTooLow);
}
```

Di:

> “Agregué la regla que exige una inversión mínima de 500 unidades.”

---

**0:15–0:30 — Tests**

Abre `dia-3/src/test.rs`.

Muestra rápidamente:

```rust
client.invest(&investor, &100);
```

con:

```rust
#[should_panic(expected = "Error(Contract, #7)")]
```

y luego:

```rust
let minted = client.invest(&investor, &500);
assert_eq!(minted, 5);
```

Puedes decir:

> “También agregué los tests: 100 debe fallar con AmountTooLow y 500 debe funcionar.”

Si quieres, ejecuta:

```bash
cd dia-3
cargo test
```

pero si tarda, **no lo hagas durante el video**. Mejor ten la terminal preparada con el resultado.

---

### 0:30–0:55 — La parte MÁS importante: inversión de 100 ❌

Muestra la terminal ejecutando la inversión de 100.

Lo importante es que aparezca:

```text
invest
payment_amount 100
```

y luego:

```text
Error(Contract, #7)
```

Di:

> “Ahora el inversionista intenta invertir 100 unidades. Como es menor al mínimo de 500, la transacción falla con el error número 7, que corresponde a AmountTooLow.”

Este punto es fundamental.

---

### 0:55–1:20 — Inversión de 500 ✅

Después ejecutas/muestras la inversión de 500:

```text
payment_amount 500
```

y que aparezca:

```text
Transaction submitted successfully!
```

Tu transacción fue:

`4ba6098371da7a2d082dd7ece4e1a13616ed564b499ec37ca8d339719d47f643`

La captura que me enviaste es **muy buena evidencia**, porque Stellar Expert muestra:

```text
Status: Successful
```

y además:

```text
invest(..., 500) -> 5
```

También muestra la transferencia de las `500` unidades del token de pago al contrato.

---

### 1:20–1:35 — Balance

En terminal muestra:

```text
=== Check Bob's RWA balance ===
"5"
```

Di:

> “Finalmente consulto el balance del inversionista. Como el precio por unidad es 100 y se invirtieron 500, recibe 5 tokens RWA.”

---

### 1:35–1:50 — Stellar Expert

Termina enseñando justamente la pantalla que me mandaste.

En la parte superior se ve:

**Status: Successful**

y abajo:

**invest(..., 500) → 5**

Di:

> “Finalmente verifico la inversión exitosa directamente en Stellar Expert sobre testnet.”

Fin del video.

---

## Hay dos detalles que sí corregiría antes de entregar

No son fallos del contrato, pero te recomiendo solucionarlos para que el entregable quede más sólido.

El primero está en `user-tool.sh`. Actualmente tu script público solamente hace:

```bash
--payment_amount 500
```

después consulta el balance y posteriormente intenta un `transfer`. :chatgpt-content-reference{index="7"}

**No contiene la prueba de inversión de 100.**

Como la tarea dice explícitamente que el inversionista intenta primero `100` y después `500`, yo modificaría ese script para que demuestre exactamente eso:

```bash
echo "=== Invest 100 - debe fallar ==="
stellar contract invoke \
  --id "$CONTRACT_ID" \
  --source "$USER_KEY" \
  --network "$NETWORK" \
  -- \
  invest \
  --investor "$(stellar keys address "$USER_KEY")" \
  --payment_amount 100 || true

echo "=== Invest 500 - debe funcionar ==="
stellar contract invoke \
  --id "$CONTRACT_ID" \
  --source "$USER_KEY" \
  --network "$NETWORK" \
  -- \
  invest \
  --investor "$(stellar keys address "$USER_KEY")" \
  --payment_amount 500

echo "=== Balance ==="
stellar contract invoke \
  --id "$CONTRACT_ID" \
  --source "$USER_KEY" \
  --network "$NETWORK" \
  -- \
  balance \
  --id "$(stellar keys address "$USER_KEY")"
```

El `|| true` es importante porque tu script tiene:

```bash
set -euo pipefail
```

y sin eso, al fallar correctamente la inversión de `100`, Bash cerraría el script y nunca ejecutaría la de `500`.

El segundo detalle es el **payment token**. Tu solución utiliza tu propio `RWAPAY`, pero el README original del bootcamp dice que se debe usar un token de prueba desplegado por el instructor. :chatgpt-content-reference{index="8"} La consigna que tú me mostraste de Semana 4 **no exige explícitamente que sea el token del instructor**, así que técnicamente tu demostración cumple la regla; aun así, si tu docente les proporcionó un Contract ID específico para el token de pago, conviene confirmar que esperaba ese token.

## Lo que debes entregar finalmente

Puedes pegar algo así en la plataforma:

> **Repositorio:**  
> https://github.com/srllamadev/rwa-launchpad-bootcamp
>
> **Contract ID — Testnet:**  
> `CCJES4U4Y3MDTJOIOOX6DBB77QL7OWS7WAM5V4KPLAZG3L7SJSWFQCY5`
>
> **Transacción de inversión exitosa (500):**  
> `https://stellar.expert/explorer/testnet/tx/4ba6098371da7a2d082dd7ece4e1a13616ed564b499ec37ca8d339719d47f643`
>
> **Resultado:**  
> Inversión de 100 → rechazada con `AmountTooLow`.  
> Inversión de 500 → exitosa.  
> Balance final del inversionista → `5 RWA`.
>
> **Video:**  
> `[aquí colocas tu enlace de YouTube/Drive]`

### Entonces, ¿ya terminaste?

Falta únicamente **grabar/subir el video (o entregar las capturas)**. Y yo haría ese pequeño cambio en `user-tool.sh` para que el repositorio refleje exactamente el flujo `100 ❌ → 500 ✅ → balance 5`, y así no quede ningún punto discutible en la revisión.
