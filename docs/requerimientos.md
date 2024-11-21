# Requerimientos funcionales

## Entity

Movimiento:
- Mover la entidad en dirección y velocidad definidas por direction y speed.
- Normalizar la dirección para garantizar movimientos consistentes.

Colisiones:
- Detectar y manejar colisiones en las direcciones horizontal y vertical.
- Ajustar la posición del objeto al detectar colisiones con otros elementos (obstacle_sprites).

Valor de onda:
Generar un valor basado en una onda sinusoidal para efectos visuales (como parpadeo).

## Player

Control del personaje:
- Permitir el movimiento del personaje en las direcciones básicas (arriba, abajo, izquierda, derecha).
- Detectar acciones específicas como ataque (SPACE) y magia (LCTRL).
- Cambiar entre armas (Q) y hechizos mágicos (E).

Gestión de estado:
- Determinar el estado del personaje (en movimiento, atacando, en reposo, etc.).
- Controlar la invulnerabilidad tras recibir daño.

Gestión de recursos:
- Recuperar energía automáticamente en función de las estadísticas.
- Reducir energía al usar habilidades mágicas.

Daño y ataque:
- Calcular el daño total del arma y las habilidades mágicas combinando estadísticas base y específicas.
- Reproducir efectos de sonido asociados a los ataques.

Actualización del estado:
- Animar el personaje en base al estado actual.
- Aplicar tiempos de enfriamiento para ataques y cambios de armas o magia.
- Manejar colisiones con obstáculos.

## Enemy

Interacción con el jugador:
- Detectar la distancia y dirección entre el enemigo y el jugador.
- Cambiar el estado del enemigo según su proximidad al jugador (idle, move, attack).
- Infligir daño al jugador cuando esté en rango de ataque.

Animación:
- Cargar y gestionar animaciones basadas en el estado del enemigo.
- Ajustar la transparencia de la imagen según el estado de vulnerabilidad.

Movimiento:
- Moverse hacia el jugador si está dentro del rango de detección.
- Reaccionar al impacto siendo empujado en la dirección opuesta.

Enfriamiento:
Implementar un sistema de cooldown para ataques y vulnerabilidad.

Manejo de vida:
- Reducir la salud al recibir daño.
- Detectar la muerte del enemigo y desencadenar partículas de muerte y experiencia para el jugador.

# Requisitos no funcionales

## Entity
Rendimiento:
Optimizar el cálculo de colisiones iterando solo sobre los obstacle_sprites relevantes.

Reutilización:
Diseñar la clase como una super clase para facilitar la herencia por otras clases (como Player).

Modularidad:
Separar la lógica de movimiento, colisión y generación de valores en métodos independientes.

Compatibilidad:
Implementación basada en pygame, asegurando que sea utilizable en otros proyectos con esta biblioteca.

Efectos visuales:
Generar efectos simples, como el parpadeo, usando el método wave_value.

## Player

Rendimiento:
Garantizar una tasa de cuadros consistente para animaciones y cálculos (priorizar eficiencia en bucles de animación y entrada).

Mantenibilidad:
- Uso de métodos y atributos bien definidos para modularidad y fácil expansión.
- Separar datos como weapon_data y magic_data en archivos independientes para facilitar actualizaciones.

Compatibilidad:
Funcionar con la biblioteca pygame y sus componentes de gráficos y sonido.

Reutilización:
Diseñar la clase Player como una subclase de Entity para reutilizar lógica compartida entre personajes u objetos similares.

Accesibilidad:
Diseñar controles simples e intuitivos para interacción con teclado.

## Enemy

Modularidad:
Diseñar la clase para integrarse fácilmente con otros sistemas del juego (gráficos, colisiones, interacciones).

Eficiencia:
- Calcular la distancia y dirección solo cuando sea necesario.
- Minimizar llamadas a métodos externos para mejorar el rendimiento.

Expansibilidad:
Facilitar la creación de nuevos tipos de enemigos al permitir datos dinámicos (e.g., monster_data).

Reutilización:
Utilizar la herencia de la clase Entity para aprovechar las funciones de movimiento y colisiones.

Audio:
Reproducir sonidos adecuados para eventos importantes (ataque, golpe, muerte) con volúmenes configurables.

Feedback visual:
Usar cambios de animación y transparencia para mejorar la percepción del estado del enemigo (vulnerabilidad, ataque, etc.).