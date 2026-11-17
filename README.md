# Medidor de polling rate

Página web que mide a cuántos Hz (polling rate) reportan un ratón y un teclado, directamente en el navegador. No usa servidor ni dependencias: es un solo `index.html` estático.

## Cómo funciona

- **Ratón:** cada movimiento llega con su propia marca de tiempo (`pointerrawupdate` o `getCoalescedEvents`). La página cuenta cuántos reportes llegan por segundo mientras el ratón se mueve (en ventanas de 250 ms) y guarda el pico más alto registrado, sin redondearlo a un valor estándar.
- **Teclado:** un teclado no envía datos de forma continua, así que el valor se estima. Al presionar varias teclas casi a la vez, el tiempo entre eventos cae en múltiplos del intervalo de sondeo (8 ms a 125 Hz, 1 ms a 1000 Hz). La página busca el intervalo estándar más grande que encaja con esos tiempos.

## Límites

- A 4000 y 8000 Hz el navegador puede perder eventos y mostrar menos de lo real. Chrome o Edge dan mejor resultado.
- La precisión del teclado depende del reloj del navegador; por encima de unos 2000 Hz solo se puede dar un mínimo («más de X Hz»).

## Despliegue

Sitio estático en Vercel conectado a este repositorio: cada push a `main` despliega.
