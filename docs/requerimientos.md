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

## Level y YSortCameraGroup

Creación del mapa:
- Leer y procesar datos desde archivos CSV para generar diferentes tipos de objetos en el mapa, como límites, hierba, objetos y entidades (jugador y enemigos).
- Asignar gráficos específicos a cada tipo de elemento según su categoría.

Control de sprites:
- Manejar grupos de sprites visibles, de obstáculos, de ataques y de entidades atacables.
- Gestionar colisiones entre ataques y sprites atacables.

Interacciones del jugador:
- Crear armas o magia cuando el jugador realiza un ataque.
- Reducir la salud del jugador al recibir daño.
- Pausar y reanudar el juego mediante el menú.

Animaciones y partículas:
- Generar partículas visuales para eventos como ataques, muerte de enemigos o interacción con objetos.
- Reproducir animaciones para la hierba o efectos mágicos.

Control de enemigos:
- Actualizar el comportamiento de los enemigos en función de su proximidad al jugador.
- Reducir la salud de los enemigos al recibir daño.

Experiencia y progreso:
- Incrementar la experiencia del jugador al derrotar enemigos.
- Mostrar la interfaz de usuario para gestionar habilidades y estadísticas.

Cámara dinámica:
- Ajustar la posición de la cámara según la posición del jugador.
- Ordenar los sprites por su posición vertical para simular profundidad.

## MagicPlayer

Uso de magia de curación (heal):
- Incrementar la salud del jugador en función del parámetro strength, sin exceder el límite máximo de salud.
- Reducir la energía del jugador según el costo de la magia (cost).
- Generar partículas visuales específicas para representar el efecto de curación (aura y heal).

Uso de magia de ataque (flame):
- Determinar la dirección del ataque en función del estado actual del jugador (up, down, left, right).
- Crear partículas de llamas a lo largo de una línea en la dirección seleccionada.
- Reducir la energía del jugador según el costo de la magia (cost).

Interacción con animaciones:
- Reproducir sonidos específicos para cada tipo de magia (curación y llamas).
- Integrarse con AnimationPlayer para generar efectos visuales dinámicos basados en la posición y contexto.

## Game

Configuración inicial del juego:
- Inicializar Pygame y configurar la pantalla con dimensiones especificadas (WIDTH y HEIGTH).
- Crear un título para la ventana del juego (Zelda).
- Instanciar la clase Level para gestionar el nivel del juego.

Gestión del bucle principal:
- Ejecutar un bucle infinito para procesar eventos, actualizar el estado del juego y renderizar la pantalla.
- Detectar eventos de teclado, como presionar la tecla M para activar o desactivar el menú del nivel.
- Manejar eventos de salida para cerrar el juego correctamente (QUIT).

Reproducción de música:
- Cargar y reproducir música de fondo (./audio/main.ogg) en un bucle infinito.
- Ajustar el volumen de la música según las necesidades del juego.

Integración con la clase Level:
Llamar al método run() de la clase Level en cada iteración del bucle principal para gestionar la lógica y el renderizado del nivel.

Gestión de fotogramas:
Controlar la velocidad de actualización del juego utilizando un valor constante de FPS (clock.tick(FPS)).

## AnimationPlayer y ParticleEffect

Gestión de Animaciones:
- AnimationPlayer:
    - Cargar y organizar diferentes tipos de animaciones (magia, ataques, muertes de monstruos, efectos visuales).
    - Proveer funciones para reflejar imágenes horizontalmente (reflect_images).
    - Crear partículas de césped y otros efectos según el tipo de animación.
- ParticleEffect:
    - Animar las partículas mediante un índice de fotogramas controlado por animation_speed.
    - Eliminar automáticamente las partículas cuando la animación finaliza.

Creación de Partículas:
- Generar partículas según la posición y el grupo asociado.
- Soportar múltiples categorías de efectos, como ataques (slash, sparkle), magia (heal, flame) y muertes de enemigos (squid, raccoon).

Gestión de Grupos:
Asociar partículas a grupos de sprites (groups) para su integración en el sistema de Pygame.

Modularidad:
Manejar animaciones específicas (create_grass_particles y create_particles) separadamente para diferentes contextos del juego.

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

## Level y YSortCameraGroup

Modularidad:
- Utilizar clases separadas para entidades como Player, Enemy, Weapon, UI y MagicPlayer.
- Separar lógica de nivel y cámara en diferentes clases.

Escalabilidad:
Permitir añadir nuevos elementos al mapa (enemigos, armas, objetos) modificando los datos de entrada.

Eficiencia:
- Optimizar el dibujo de sprites visibles, ordenándolos por la posición vertical para reducir cálculos innecesarios.
- Utilizar estructuras de datos eficientes para manejar grupos grandes de sprites.

Extensibilidad:
Facilitar la creación de nuevos tipos de armas, magias y enemigos al permitir configuraciones externas (archivos de datos o gráficos).

Interfaz visual:
- Proveer retroalimentación visual para interacciones (partículas, daño, eventos especiales).
- Mostrar información clara y organizada sobre estadísticas del jugador.

Robustez:
Manejar colisiones y límites del mapa de forma segura para evitar errores en el movimiento o la interacción.

Rendimiento:
Minimizar llamadas innecesarias a funciones de dibujo y cálculos de posición, especialmente en grupos grandes de sprites.

## MagicPlayer

Modularidad:
Centralizar la lógica de las magias en una clase dedicada, permitiendo una fácil extensión o mantenimiento.

Eficiencia:
- Minimizar cálculos redundantes al determinar direcciones y posiciones de partículas.
- Usar recursos compartidos como sonidos y animaciones para evitar duplicación.

Extensibilidad:
- Permitir la fácil incorporación de nuevos tipos de magia mediante la adición de métodos similares a heal y flame.
- Diseñar los efectos de partículas y sonidos como configurables o reutilizables.

Interfaz visual:
Garantizar que los efectos visuales de la magia sean claros y estén alineados con la posición y estado del jugador.

Rendimiento:
- Optimizar el manejo de partículas para evitar sobrecarga en juegos con múltiples eventos simultáneos.
- Controlar el uso de energía y salud para evitar cálculos innecesarios si el jugador no tiene suficiente energía.

Experiencia de usuario:
- Proveer retroalimentación inmediata al usar magia, como sonido y efectos visuales.
- Respetar límites de energía y salud para mantener balance en el juego.

## Game

Modularidad:
Centralizar la configuración general y el bucle principal en una clase (Game) para facilitar la gestión del flujo del juego.

Rendimiento:
Optimizar el manejo de eventos y la actualización de la pantalla para mantener una experiencia de juego fluida a la velocidad de fotogramas establecida.

Experiencia de usuario:
- Proveer una experiencia auditiva continua mediante música de fondo que mejore la inmersión.
- Usar colores específicos (como WATER_COLOR) para proporcionar coherencia visual en el fondo de la pantalla.

Escalabilidad:
Permitir la incorporación de nuevos niveles u otras funcionalidades mediante la integración con la clase Level.

Manejo de errores:
Garantizar que el juego se cierre correctamente al recibir un evento de salida (pygame.quit() y sys.exit()).

Accesibilidad:
Permitir que los usuarios activen o desactiven menús con una tecla (M) de manera intuitiva.

## AnimationPlayer y ParticleEffect

Rendimiento:
- Optimizar el manejo de listas de fotogramas para asegurar que las animaciones sean fluidas.
- Reflejar imágenes previamente para evitar cálculos redundantes durante la ejecución.

Escalabilidad:
- Estructura flexible que permite agregar nuevas animaciones simplemente extendiendo el diccionario frames.
- Compatibilidad con efectos personalizados según las necesidades del juego.

Reutilización:
Modularidad suficiente para reutilizar las clases en otros sistemas de efectos visuales.

Compatibilidad:
Integración con el sistema de grupos de Pygame para permitir una fácil actualización y renderizado de partículas en el juego.

Experiencia de Usuario:
Proveer efectos visuales coherentes y atractivos que realcen la experiencia de juego.