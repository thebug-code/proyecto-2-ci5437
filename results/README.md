# Proyecto 2: Arboles de Juego

## Representación de Othello
En primer lugar, se completó la implementación de la función outflank, que verifica si existe un movimiento es válido. En particular, se agrego la verificación para los movimientos diagonales. Para ello, se toma la posición en la que se quiere colocar la ficha del jugador actual, y se recorren las cuatro diagonales posibles en ambas direcciones, hasta encontrar una casilla vacía o el borde del tablero. Si en el camino se encuentran una o más fichas del rival seguidas por una ficha del jugador actual, el movimiento es válido.

## Algoritmos para árboles de juego

Se implementarón los siguientes algoritmos para recorrer los respectivos árboles de juego:

    - Negamax sin poda alpha-beta: es una variante del algoritmo minimax que se basa en la propiedad de suma cero de un juego de dos jugadores. Este algoritmo simplifica la implementación del minimax al usar la negación del valor de la posición para el jugador contrario. Explora todo el árbol de juego hasta una profundidad determinada y devuelve el valor máximo de los sucesores del nodo actual.
    - Negamax con poda alpha-beta: es una mejora del algoritmo anterior que usa dos valores, alfa y beta, para eliminar partes del árbol que no influyen en la decisión final. Esto reduce el número de nodos que se tienen que examinar y acelera la búsqueda.
    - Scout es un algoritmo inventado por Judea Pearl en 1980 que fue el primero en superar al algoritmo alpha-beta y en ser probado como óptimo asintóticamente. Este algoritmo usa una ventana nula para todos los nodos, excepto el primero, y solo hace re-búsquedas cuando el valor del nodo está fuera de la ventana. Asume que el primer nodo explorado es el mejor y que tiene el mismo valor que el nodo actual. Esto permite evitar muchas re-búsquedas innecesarias.
    - Negascout es un algoritmo muy similar a Scout, pero que usa el marco de negamax y algunas mejoras relacionadas con la poda alfa-beta. Este algoritmo fue introducido por Alexander Reinefeld en 1983 y es prácticamente equivalente a la búsqueda de la variante principal (PVS), que es otra forma de implementar el algoritmo Scout. La diferencia principal entre Negascout y PVS es cómo manejan las re-búsquedas: Negascout pasa el valor devuelto por la búsqueda de ventana nula en lugar de alfa, mientras que PVS pasa alfa y beta. Esto puede afectar al orden de los nodos y al número de re-búsquedas necesarias.

En cada implementación de los cuatro algoritmos anteriores, se tiene que:

En primer lugar, se eliminaron los parámetros  `depth` y `use_tt` de la implementación de cada uno de los algoritmos. El parámetro `depth` indica la profundidad máxima a la que se debe explorar el árbol de juego, pero en este caso no se quiso limitar la búsqueda a ninguna profundidad, sino que se exploró todo el árbol hasta llegar a los nodos terminales o hasta que se alcanzara el tiempo máximo establecido. El parámetro `use_tt` indica si se debe usar una tabla de transposición, que es una estructura de datos que almacena los valores de los nodos ya visitados para evitar repetir cálculos, pero en este caso no se implementó esta estructura, ya que se consideró que no era necesaria para el tamaño del árbol de juego.

La implementación de cada uno de los algoritmos, se baso en los pseudocódigos vistos en clases. La única adición relevante a estos es que, para este problema, se consideró el caso de que un jugador no pueda colocar ninguna de sus fichas y deba pasar el turno. Para ello, al momento de ejecutar los algoritmos, se verifica que exista algún movimiento válido, y en caso de no haberlo, el turno pasa al otro jugador usando el mismo estado.

Además, es importante resaltar que en la representación del juego obtenida en `othello_cut`, las fichas negras son representadas con el valor booleano true, y las fichas blancas con el valor false; mientras que en nuestra implementación de los algoritmos, el turno del jugador con fichas negras es representado con el entero 1 y el turno del jugador de fichas blancas, con -1. Por esta razón, se utilizó `color == 1` para pasar de la representación de los algoritmos a la del juego.
