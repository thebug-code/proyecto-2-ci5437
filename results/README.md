#
### CI5437 - Inteligencia Artificial 1
##### Prof. Carlos Infante
# Proyecto 2: Arboles de Juego
Por Oliver Bueno, Alejandro Meneses

## Representación de Othello
En primer lugar, se completó la implementación de la función outflank, que verifica si existe un movimiento es válido. En particular, se agrego la verificación para los movimientos diagonales. Para ello, se toma la posición en la que se quiere colocar la ficha del jugador actual, y se recorren las cuatro diagonales posibles en ambas direcciones, hasta encontrar una casilla vacía o el borde del tablero. Si en el camino se encuentran una o más fichas del rival seguidas por una ficha del jugador actual, el movimiento es válido.

## Algoritmos para árboles de juego

Se implementarón los siguientes algoritmos para recorrer los respectivos árboles de juego:

- Negamax sin poda alpha-beta: es una variante del algoritmo minimax que se basa en la propiedad de suma cero de un juego de dos jugadores. Este algoritmo simplifica la implementación del minimax al usar la negación del valor de la posición para el jugador contrario. Explora todo el árbol de juego hasta una profundidad determinada y devuelve el valor máximo de los sucesores del nodo actual.
- Negamax con poda alpha-beta: es una mejora del algoritmo anterior que usa dos valores, alfa y beta, para eliminar partes del árbol que no influyen en la decisión final. Esto reduce el número de nodos que se tienen que examinar y acelera la búsqueda.
- Scout es un algoritmo inventado por Judea Pearl en 1980 que fue el primero en superar al algoritmo alpha-beta y en ser probado como óptimo asintóticamente. Este algoritmo usa una ventana nula para todos los nodos, excepto el primero, y solo hace re-búsquedas cuando el valor del nodo está fuera de la ventana. Asume que el primer nodo explorado es el mejor y que tiene el mismo valor que el nodo actual. Esto permite evitar muchas re-búsquedas innecesarias.
- Negascout es un algoritmo muy similar a Scout, pero que usa el marco de negamax y algunas mejoras relacionadas con la poda alfa-beta. Este algoritmo fue introducido por Alexander Reinefeld en 1983 y es prácticamente equivalente a la búsqueda de la variante principal (PVS), que es otra forma de implementar el algoritmo Scout. La diferencia principal entre Negascout y PVS es cómo manejan las re-búsquedas: Negascout pasa el valor devuelto por la búsqueda de ventana nula en lugar de alfa, mientras que PVS pasa alfa y beta. Esto puede afectar al orden de los nodos y al número de re-búsquedas necesarias.

En cada implementación de los cuatro algoritmos anteriores, se tiene que:

En primer lugar, se eliminaron los parámetros  `depth` y `use_tt` de la implementación de cada uno de estos. El parámetro `depth` indica la profundidad máxima a la que se debe explorar el árbol de juego, pero en este caso no se quiso limitar la búsqueda a ninguna profundidad, sino que se exploró todo el árbol hasta que se alcanzara el tiempo límite establecido. El parámetro `use_tt` indica si se debe usar una tabla de transposición, que es una estructura de datos que almacena los valores de los nodos ya visitados para evitar repetir cálculos, pero en este caso no se implementó esta estructura, ya que se consideró que no era necesaria para el tamaño del árbol de juego.

La implementación de cada uno de los algoritmos, se baso en los pseudocódigos vistos en clases. La única adición relevante a estos es que, para este problema, se consideró el caso de que un jugador no pueda colocar ninguna de sus fichas y deba pasar el turno. Para ello, al momento de ejecutar los algoritmos, se verifica que exista algún movimiento válido, y en caso de no haberlo, el turno pasa al otro jugador usando el mismo estado.

Además, es importante resaltar que en la representación del juego obtenida en `othello_cut`, las fichas negras son representadas con el valor booleano true, y las fichas blancas con el valor false; mientras que en nuestra implementación de los algoritmos, el turno del jugador con fichas negras es representado con el entero 1 y el turno del jugador de fichas blancas, con -1. Por esta razón, se utilizó `color == 1` para pasar de la representación de los algoritmos a la del juego.

## Resultados Experimentales
Los algoritmos se ejecutaron en una computadora con las siguientes características:

- Procesador: 11th Gen Intel(R) Core(TM) i7-1165G7 @ 2.80GHz.
- Memoria RAM: 20.0 GB (19.8 GB usable).
- Sistema operativo: Windows 11 Home.

Además, la ejecución de los algoritmos se realizo usando el programa y siguiendo las indicaciones mencionadas en el enunciado del proyecto: evaluandolos en una instancia de la variación principal del problema que se encuentra a una distancia cada vez más lejana de la meta en cada iteración. El tiempo límite establecido para cada ejecución es de 2 horas (7200 segundos). Con esto donde se permitió que los algoritmos se ejecutaran en la mayor cantidad de nodos iniciales posibles pertenecientes a la variación principal hasta haber transcurrido este tiempo. Los resultados se muestran en las siguientes tablas

#### Neganax
| PV | Jugador | Valor | Expandidos  | Generados  | Tiempo (s) | Generados/Segundo |
|------------|---------|-------|-------------|------------|----------|-------------------|
| 34.        | Blanco  | -4    | 0           | 1          | 3.00002e-06 | 333,331        |
| 33.        | Negro   | -4    | 1           | 2          | 6.00005e-06 | 333,331        |
| 32.        | Blanco  | -4    | 3           | 5          | 4.00003e-06 | 1.24999e+06    |
| 31.        | Negro   | -4    | 4           | 6          | 2.00002e-06 | 2.99998e+06    |
| 30.        | Blanco  | -4    | 9           | 13         | 5.00004e-06 | 2.59998e+06    |
| 29.        | Negro   | -4    | 10          | 14         | 5.00004e-06 | 2.79998e+06    |
| 28.        | Blanco  | -4    | 64          | 91         | 3.80001e-05 | 2.39473e+06    |
| 27.        | Negro   | -4    | 125         | 177        | 7.70001e-05 | 2.2987e+06     |
| 26.        | Blanco  | -4    | 744         | 1049       | 0.000472   | 2.22246e+06     |
| 25.        | Negro   | -4    | 3168        | 4498       | 0.002021   | 2.22563e+06     |
| 24.        | Blanco  | -4    | 8597        | 11978      | 0.004796   | 2.4975e+06      |
| 23.        | Negro   | -4    | 55127       | 76826      | 0.03269    | 2.35014e+06     |
| 22.        | Blanco  | -4    | 308479      | 428402     | 0.182118   | 2.35233e+06     |
| 21.        | Negro   | -4    | 2525249     | 3478735    | 1.446      | 2.40577e+06     |
| 20.        | Blanco  | -4    | 9459570     | 13078933   | 6.214      | 2.10475e+06     |
| 19.        | Negro   | -4    | 65121519    | 90647895   | 38.6079    | 2.34791e+06     |
| 18.        | Blanco  | -4    | 625084814   | 876269598  | 373.83     | 2.34403e+06     |
| 17.        | Negro   | -4    | 3999381161  | 1305006091 | 2339.84    | 557733          |

#### Negamax con poda alpha-beta
| PV | Jugador | Valor | Expandidos | Generados | Tiempo (s) | Generados/Segundo |
|------------|---------|-------|-------------|------------|----------|-------------------|
| 34.        | Blanco  | -4    | 0           | 1          | 1.00001e-06 | 999992            |
| 33.        | Negro   | -4    | 1           | 2          | 2.00002e-06 | 999992            |
| 32.        | Blanco  | -4    | 3           | 5          | 3.00002e-06 | 1.66665e+06       |
| 31.        | Negro   | -4    | 4           | 6          | 1.00001e-06 | 5.99995e+06       |
| 30.        | Blanco  | -4    | 9           | 13         | 4.00003e-06 | 3.24998e+06       |
| 29.        | Negro   | -4    | 10          | 14         | 3.00002e-06 | 4.66663e+06       |
| 28.        | Blanco  | -4    | 21          | 27         | 9.00001e-06 | 3e+06             |
| 27.        | Negro   | -4    | 62          | 82         | 2.30001e-05 | 3.56521e+06       |
| 26.        | Blanco  | -4    | 186         | 238        | 7e-05      | 3.4e+06           |
| 25.        | Negro   | -4    | 769         | 1003       | 0.000301   | 3.33223e+06       |
| 24.        | Blanco  | -4    | 1152        | 1502       | 0.000409   | 3.67237e+06       |
| 23.        | Negro   | -4    | 3168        | 4068       | 0.001194   | 3.40704e+06       |
| 22.        | Blanco  | -4    | 7031        | 9130       | 0.002924   | 3.12243e+06       |
| 21.        | Negro   | -4    | 76021       | 98755      | 0.041441   | 2.38303e+06       |
| 20.        | Blanco  | -4    | 98129       | 127644     | 0.061595   | 2.07231e+06       |
| 19.        | Negro   | -4    | 205017      | 267604     | 0.123571   | 2.16559e+06       |
| 18.        | Blanco  | -4    | 960343      | 1259430    | 0.572935   | 2.19821e+06       |
| 17.        | Negro   | -4    | 1549785     | 2031924    | 0.969424   | 2.09601e+06       |
| 16.        | Blanco  | -4    | 22325108    | 29501798   | 12.3624    | 2.3864e+06        |
| 15.        | Negro   | -4    | 32949019    | 43574643   | 18.7108    | 2.32885e+06       |
| 14.        | Blanco  | -4    | 82016158    | 107642871  | 46.7151    | 2.30424e+06       |
| 13.        | Negro   | -4    | 315074162   | 415909956  | 200.79     | 2.07136e+06       |
| 12.        | Blanco  | -4    | 2230058150  | 2931981147 | 1318.7     | 2.22339e+06       |
| 11.        | Negro   | -4    | 512734023   | 2042502265 | 3019.8     | 676369            |

#### Negascout
| PV | Jugador | Valor | Expandidos | Generados | Tiempo (s) | Generados/Segundo |
|------------|---------|-------|-------------|------------|----------|-------------------|
| 34.        | Blanco  | -4    | 0           | 1          | 2.99991e-06 | 333344         |
| 33.        | Negro   | -4    | 1           | 2          | 2.00002e-06 | 999992         |
| 32.        | Blanco  | -4    | 3           | 5          | 3.00002e-06 | 1.66665e+06    |
| 31.        | Negro   | -4    | 4           | 6          | 1.9999e-06  | 3.00015e+06    |
| 30.        | Blanco  | -4    | 14          | 20         | 9.00007e-06 | 2.22221e+06    |
| 29.        | Negro   | -4    | 15          | 21         | 8.00006e-06 | 2.62498e+06    |
| 28.        | Blanco  | -4    | 26          | 34         | 1.4e-05    | 2.42857e+06     |
| 27.        | Negro   | -4    | 64          | 84         | 3.89999e-05 | 2.15385e+06    |
| 26.        | Blanco  | -4    | 312         | 398        | 0.000176   | 2.26136e+06     |
| 25.        | Negro   | -4    | 1275        | 1668       | 0.00074    | 2.25405e+06     |
| 24.        | Blanco  | -4    | 1894        | 2465       | 0.001014   | 2.43097e+06     |
| 23.        | Negro   | -4    | 3051        | 3898       | 0.001854   | 2.10248e+06     |
| 22.        | Blanco  | -4    | 9316        | 12067      | 0.006375   | 1.89286e+06     |
| 21.        | Negro   | -4    | 37959       | 48674      | 0.028764   | 1.69218e+06     |
| 20.        | Blanco  | -4    | 63522       | 81826      | 0.04703    | 1.73987e+06     |
| 19.        | Negro   | -4    | 142545      | 184361     | 0.095357   | 1.93338e+06     |
| 18.        | Blanco  | -4    | 466053      | 606378     | 0.287221   | 2.11119e+06     |
| 17.        | Negro   | -4    | 869928      | 1134797    | 0.504452   | 2.24956e+06     |
| 16.        | Blanco  | -4    | 5517551     | 7223328    | 3.22104    | 2.24255e+06     |
| 15.        | Negro   | -4    | 19704698    | 25833440   | 11.4101    | 2.26409e+06     |
| 14.        | Blanco  | -4    | 47600175    | 62053925   | 28.1821    | 2.20189e+06     |
| 13.        | Negro   | -4    | 185296093   | 242589301  | 108.725    | 2.23121e+06     |
| 12.        | Blanco  | -4    | 477000927   | 623019805  | 271.827    | 2.29197e+06     |
| 11.        | Negro   | -4    | 2569420749  | 3362309726 | 1499.65    | 2.24206e+06     |
| 10.        | Blanco  | -4    | 4286712056  | 1324722117 | 2545.57    | 520403          |

## Comparación de los algoritmos
A continuación se presentan gráficos que comparan el rendimiento de los algoritmos estudiados. Dichos gráficos se muestran en notación logarítmica para mejor apreciación de los resultados.


Gráfico 1: Nodos expandidos en cada nivel

![Expandidos][1]

[1]: Figuras/imaexp.jpg

Gráfico 2: Nodos generados en cada nivel

![Generados][2]

[2]: Figuras/imagene.jpg

Gráfico 3: Tiempo en recorrer cada nivel

![Tiempo][3]

[3]: Figuras/imatiem.jpg

Dados los resultados, se observa que el algoritmo más eficiente para recorrer el arbol de juego es Negascout, siendo ligeramente superior a lo mostrado por el algoritmo Scout.

Observando detalladamente cada algorimos, se observa que Negamax expande y genera una cantidad de nodos muy superior con respecto a los demás algoritmos, llegando a explorar el árbol hasta un PV igual a 17, mientras que el mismo algoritmo expleando poda alfa-beta explora árbol llega hasta un PV igual a 11. Esto muestra que aplicar poda alfa-beta en el algoritmo Negamax genera un aumento de eficiencia significativo.

Por otro lado, comparando los algoritmos Scout y Negascout, estos presentan un comportamiento similar, en las gráficas se muestra como estos se solapan hasta cierto punto, observando que el algoritmo Negascout comienza a tener mejor rendimiento que el algoritmo Scout en los niveles más profundos.

También es importante observar que el algotitmos Negamax con poda alfa-beta se comporta com mejor rendimiento que los demás en los primeros 11 nieveles del árbol de juego.

Comparando los resultados de las corridas de los cuatro algoritmos, se observa que los algoritmos Scout y Negascout recorren a mayor profundidad (tienen los menores pv) el árbol de juego, esto se observa mejor en la siguiente gráfica.


Gráfico 4: Valores mínimos de los pv

![pv][4]

[4]: Figuras/imapv.jpg


