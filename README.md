# Juego: Gato vs. Ratón con MiniMax 🐭🆚😼

## Descripción del Proyecto

Simulación de persecución entre un gato y un ratón en un tablero bidimensional. 
El objetivo principal fue desarrollar agentes inteligentes para ambos personajes utilizando el algoritmo **MiniMax**. 
La IA del ratón evoluciona de movimientos aleatorios a una huida inteligente; el gato utiliza Minimax estratégicamente desde el inicio para intentar atrapar al ratón. 

Para una descripción detallada de las fases y el flujo del juego, consulta el siguiente documento:

[Ver Diagrama de Flujo Detallado](GAME_FLOW.md)

---

## Características Implementadas y Funcionamiento ✅

* **Algoritmo MiniMax:** Tanto el gato como el ratón (en su fase inteligente) lo utilizan para la toma de decisiones estratégicas, explorando posibles jugadas futuras.
* **Múltiples Condiciones de Finalización:** El juego concluye si el gato atrapa al ratón, si el ratón escapa por una salida, o si se alcanza el límite de turnos (empate).
* **Función de Evaluación Estratégica:** El núcleo de la IA considera la distancia entre jugadores, la proximidad del ratón a las salidas, y la rapidez en la toma de decisiones durante la simulación de Minimax.
* **Comportamiento Evolutivo del Ratón:** Inicia con movimientos aleatorios (`TIMER_SMART`) antes de activar su comportamiento de huida inteligente basado en Minimax.
* **Entorno de Juego Definido:** Tablero bidimensional con paredes, múltiples salidas, posiciones de inicio semi-aleatorias para los jugadores y movimiento en 8 direcciones.

---

## Desafíos y Aprendizajes en el Desarrollo 🛠️

* **Ajuste de la IA:** Fue necesario refinar la función de evaluación para evitar comportamientos subóptimos, como un gato demasiado pasivo ("arquero en las salidas") o bucles de movimientos repetitivos.
* **Balance del Juego:** Se consideraron y descartaron ideas como múltiples turnos para el gato para mantener un juego equilibrado.
* **Refinamiento de Lógica:** Se pulieron detalles como la prevención de superposiciones al inicio y el correcto manejo de las mecánicas de captura.

---

## Momentos Claves del Proyecto ✨

El descubrimiento más significativo y que mejoró notablemente el comportamiento de los agentes fue la implementación del factor `SEARCH_DEPTH - depth` dentro de la función de evaluación de Minimax.

Este simple ajuste incentivó a los agentes a buscar soluciones (victorias o evitar derrotas) en **menos turnos**, eliminando comportamientos "tímidos" y haciendo sus estrategias más decididas.

---

## Cómo Ejecutar el Juego 🚀

1.  Asegúrate de tener Python 3 instalado.
2.  El proyecto es un Jupyter Notebook (`Juegogato_raton.ipynb`).
3.  Abre el notebook en un entorno Jupyter (Jupyter Lab, Google Colab, etc.).
4.  Ejecuta todas las celdas en orden. La última celda inicia la simulación con `jugar_partida()`.

---

## Tecnologías Utilizadas 💻

* **Python 3**
* Librerías estándar de Python:
    * `random` (para aleatoriedad)
    * `copy` (específicamente `deepcopy` para Minimax)
    * `time` (para pausas en la simulación)
