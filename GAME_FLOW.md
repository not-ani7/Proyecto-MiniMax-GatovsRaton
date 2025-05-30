## Diagrama de flujo del Juego: Gato vs. Ratón con MiniMax
### Fase 1: Configuracion inicial
- **Librerías:** Se importa *copy* para duplicar tableros en simulaciones, *random* para movimientos aleatorios, y *time* para pausas. 

- **Constantes:** Se crean todas las variables que no cambiarán: 

    - **AVATAR_P1, AVATAR_P2:** Los emojis para el gato y el ratón.

    - **FILAS, COLUMNAS:** Las dimensiones del tablero.

    - **MAX_TURNOS:** El límite de turnos para evitar empates infinitos. 

    - **SEARCH_DEPTH:** El nivel de "inteligencia". Le dice al algoritmo MiniMax cuantos turnos en el futuro debe analizar, cuantos movimientos debe simular para tomar una decisión.

    - **TIMER_SMART:** Define cuantos turnos iniciales el ratón se moverá al azar antes de activar su propia inteligencia. 

    - **DIRECCIONES:** Una lista con las 8 tuplas (coordenadas) que representan los posibles movimientos (arriba, abajo, diagonales, etc.)

### Fase 2: Creación del Mundo (El Tablero)
1. Función **crear_partida_aleatoria ( ):**
    - **Propósito:** Generar un nuevo tablero para cada partida

    - **Acciones:** 
        1. Se crea una matriz (lista de listas) llena de casillas vacías (CASILLA)
        2. Coloca las paredes (PARED) y las salidas (CASILLA_SALIDA) en sus lugares.
        3. Asigna posiciones iniciales aleatorias para el gato (en la parte superior) y el ratón (en la parte inferior), asegurándose de que no empiecen en el mismo lugar.

2. Función **imprimir_tablero():**
    - **Proposito:** Mostrar el estado actual del juego de forma visual.
    - **Acciones:** Recorre la matriz del tablero y la imprime en la consola, fila por fila.

### Fase 3: Mecánicas basicas (¿que se puede hacer?)
- **find_pos_jugadores( ):** Escanea el tablero y devuelve las coordenadas (fila, columna) actuales del gato y el ratón. Es el "GPS" del juego. 

- **movimientos_ok( ):** A partir de la posición de un jugador, calcula y devuelve una lista de todos los movimientos válidos. 

- **moverse ( ):** Recibe el tablero actual y un movimiento, y devuelve un *nuevo tablero* con la posición del jugador actualizado. Usa *copy.deepcopy()* para no alterar el tablero original. 

- **verificar_estado_juego( ):** Es el árbitro. Revisa si el ratón fue atrapado, si escapó por una salida o si se acabarón los turnos, y devuelve el resultado de la partida. ("Ganador: 🐈", "Ganador: 🐀", "Empate" o "Partida en curso").

### Fase 4: La inteligencia artificial. 
1. Función **evaluar_partida ( ):** 
    - **Proposito:** Asignar una puntuación numérica a cada estado específico del tablero, en este caso desde la perspectiva del Gato (jugador maximizador). Esta puntuación le dice a la IA que tan favorable es este tablero para el gato. 
    - **Flujo interno y Lógica de puntuación:**
        - Victoria del gato: Puntuación muy alta. 
        - Victoria del ratón: Puntuación muy baja. 
        - Partida en curso: La puntuación se basa en:
            - La distancia entre el gato y el ratón (menos distancia, mejor para el gato)
            - La distancia entre el ratón a la salida (mas distancia, mejor para el gato)

2. Función **minimax( ):** 
    - **Propósito:** Explorar todas las posibles secuencias de jugadas hasta la profundidad (SEARCH_DEPTH) definida. 
    - **Funcionamiento:**
        - Es una funcion *recursiva*: se llama a sí misma para simular los turnos directos.
        - **Turno del gato (Maximizador):** busca el movimiento que le dé la máxima puntuación posible. 
        - **Turno del Ratón (Minimizador):** anticipa la jugada del gato y elige el movimiento que lleve a la mínima puntuación posible (el escenario menos favorable para el gato). 

3. Función **find_best_move ( ):**
    - **Propósito:** Decidir el mejor movimiento para el turno actual.
    - **Acciones:**          
        1. Obtiene la lista de movimientos válidos con *movimientos_ok()*. 
        2. Para cada movimiento posible, crea un tablero hipotético con *moverse ()*. 
        3. Utiliza *minimax()* para evaluar la puntuación de ese tablero hipotético a largo plazo.
        4. Elige el movimiento que, según minimax, conduce al mejor resultado. 
        5. Devuelve la coordenada de ese movimiento óptimo. 

### Fase 5: Ejecución del Juego 
1. Función *jugar_partida():*
    - Flujo de **jugar partida ():**
        1. Crea el tablero inicial.
        2. Entra en un bucle que se repite en cada turno. 
        3. Verifica el estado del juego: Llama a **verificar_estado_juego()**. Si la partida termino, muestra el resultado y se detiene. 
        4. **Turno del Gato:** llama a **find_best_move()** para obtener la jugada del gato, actualiza el tablero y lo imprime. 
        5. **Turno del Ratón:** 
            - Si **turno_numero** es bajo (menor o igual a *TIMER_SMART*), elige un movimiento al azar. 
            - Si no, también usa **find_best_move()** para escapar de forma inteligente. 
            - Actualiza el tablero y lo imprime. 
        6. Incrementa el contador de turnos y cambia al siguiente jugador. El bucle continua. 
    
2. Finalmente, se llama a la función **jugar_partida()**, para iniciar todo el proceso. 