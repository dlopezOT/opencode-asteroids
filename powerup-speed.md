# Plan: Implementación de Power-up "Velocidad"

## Objetivo
Agregar un power-up que duplique la velocidad de la nave durante 5 segundos al recogerlo.

## Pasos

### 1. Actualizar la clase `Ship` (`game.js`)
- **Estado:** Añadir `this.speedMultiplier = 1` y `this.speedTimer = 0` al `constructor` o `reset`.
- **Lógica:** En el método `update(dt)`:
    - Decrementar `speedTimer` si es mayor a 0.
    - Si `speedTimer` llega a 0, resetear `speedMultiplier` a 1.
- **Movimiento:** Aplicar `this.speedMultiplier` a la constante `THRUST` durante el cálculo de movimiento: `const THRUST = 260 * this.speedMultiplier;`.

### 2. Crear clase `PowerUp` (`game.js`)
- Definir clase `PowerUp` similar a otras entidades.
- Debe tener: posición (x, y), tipo ('speed'), y un método `draw()` (ej. un círculo de color azul/verde).
- Debe tener una propiedad `dead` para cuando sea recogido.

### 3. Integración en `update(dt)` (`game.js`)
- **Spawn:** Añadir lógica en el bucle principal para generar un `PowerUp` cada cierto tiempo o al destruir asteroides.
- **Colisión:** Añadir comprobación: si `dist(ship, powerUp) < threshold`, activar `ship.speedTimer = 5` y `ship.speedMultiplier = 2`, luego marcar el power-up como `dead`.
- **Render:** Asegurarse de que los power-ups activos sean dibujados en la función `draw()`.

### 4. Verificación
- Abrir `index.html` y comprobar que la nave se mueve normalmente.
- Recoger el power-up y verificar que la aceleración aumenta durante 5 segundos.
- Verificar que vuelve a la velocidad normal tras el tiempo transcurrido.
