# Medidor de polling rate

Página web que mide a cuántos Hz (polling rate) reportan un ratón y un teclado, directamente en el navegador. No usa servidor ni dependencias: es un solo `index.html` estático.

## Cómo funciona

- **Ratón:** cada movimiento llega con su propia marca de tiempo (`pointerrawupdate` o `getCoalescedEvents`). La página cuenta cuántos reportes llegan por segundo mientras el ratón se mueve (en ventanas de 250 ms) y guarda el pico más alto registrado. El ratón se marca compatible con la frecuencia estándar más alta (125, 250, 500, 1000, 2000, 4000 u 8000 Hz) a la que el pico llega al menos al 80 %; por ejemplo, un pico de 850 Hz es compatible con 1000 Hz.
- **DPI del ratón:** el navegador no sabe cuánto se movió el ratón sobre la mesa, así que el DPI no se detecta solo. Con el puntero bloqueado (movimiento crudo cuando el navegador lo permite), el usuario desliza el ratón una distancia conocida sobre una regla y la página calcula DPI = puntos ÷ pulgadas. Promedia varias mediciones y muestra el valor común más cercano.
- **Teclado:** un teclado no envía datos de forma continua, así que el valor se estima. Al presionar varias teclas casi a la vez, el tiempo entre eventos cae en múltiplos del intervalo de sondeo (8 ms a 125 Hz, 1 ms a 1000 Hz). La página busca el intervalo estándar más grande que encaja con esos tiempos.

## Límites

- A 4000 y 8000 Hz el navegador puede perder eventos y mostrar menos de lo real. Chrome o Edge dan mejor resultado.
- La precisión del teclado depende del reloj del navegador; por encima de unos 2000 Hz solo se puede dar un mínimo («más de X Hz»).

## Despliegue

Sitio estático en Vercel conectado a este repositorio: cada push a `main` despliega.
