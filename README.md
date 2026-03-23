_Este proyecto ha sido creado como parte del currículo de 42 por gortiz-j y evaflete._

**Descripción**
- **Proyecto**: Generador y visualizador de laberintos (A-Maze-ing).
- **Qué hace**: genera laberintos (opcionalmente "perfectos"), guarda la representación en un fichero hexadecimal y ofrece una visualización gráfica con MiniLibX.
**Algoritmo**: Resumen del algoritmo y comportamiento de la semilla:

        - Algoritmo de generación:
            Se utiliza una búsqueda en profundidad (DFS) con retroceso (backtracking)
            para crear un laberinto "perfecto" (si se solicita):
                1. Partimos de la celda de entrada y la marcamos como visitada.
                2. Seleccionamos aleatoriamente un vecino no visitado, rompemos el
                     muro entre la celda actual y el vecino, marcamos el vecino y lo
                     añadimos a la pila.
                3. Si no hay vecinos no visitados, retrocedemos (pop de la pila) y
                     repetimos hasta vaciar la pila.

            Esta técnica garantiza que el laberinto (fuera de zonas protegidas como
            el patrón "42") tenga conectividad total y, en el caso "perfecto",
            exactamente un único camino entre dos celdas cualesquiera.

        - Patrón "42":
            Antes de la generación se pueden reservar celdas como bloqueadas para
            dibujar el logo '42'. Si el tamaño del laberinto es menor que 10x10 el
            patrón se omite (por falta de espacio) y se imprime un warning.

        - Semilla (seed):
            El constructor acepta un entero `seed`. Si `seed` no es `None`, se pasa
            a `random.seed(self.seed)`. Esto fija la secuencia de números pseudo-
            aleatorios del módulo `random` y hace que las decisiones aleatorias
            (por ejemplo `random.choice`) sean deterministas mientras se use la
            misma semilla y los mismos parámetros de entrada (WIDTH, HEIGHT, ENTRY,
            EXIT, algoritmo, etc.). En otras palabras, usar la misma semilla y los
            mismos parámetros producirá el mismo laberinto, de forma análoga a las
            semillas de mundos en juegos como Minecraft.

**Uso**
- **Ejecutar**: `python3 a_maze_ing.py config.txt`
- **Archivo de configuración**: `config.txt` (claves: `WIDTH`, `HEIGHT`, `ENTRY`, `EXIT`, `OUTPUT_FILE`, `PERFECT`, `SEED`, `ALGORITHM`).

**Semilla y reproducibilidad**
- **Formato**: `SEED` debe ser un entero (por ejemplo `SEED=12346`).
- **Comportamiento**: si se proporciona la misma semilla y los mismos parámetros (`WIDTH`, `HEIGHT`, `ENTRY`, `EXIT`, `PERFECT`, algoritmo) el laberinto generado será el mismo (determinismo de Python `random`). Si no se proporciona `SEED`, el generador elige una semilla aleatoria internamente.
- **Dónde se maneja**: ver [a_maze_ing.py](a_maze_ing.py) y [maze_generator.py](maze_generator.py).

**Patrón "42"**
- El logo `42` se dibuja como celdas cerradas cuando el tamaño lo permite. Si el laberinto es menor que 10x10, el patrón se omite y se imprime una advertencia a stderr. (Ver [maze_generator.py](maze_generator.py)).

**Archivos principales**
- [a_maze_ing.py](a_maze_ing.py): lectura de configuración y arranque.
- [maze_generator.py](maze_generator.py): clase `MazeGenerator`, generación, resolución y guardado.
- [draw.py](draw.py): visualizador con MiniLibX.
- `config.txt`: ejemplo de configuración por defecto.
- `maze.txt`: salida de ejemplo generada por el programa.

**Makefile**
-habituales: `make`, `clean`, `fclean`, `re`.

**Ejemplo rápido**
- Contenido mínimo `config.txt`:

```
WIDTH=25
HEIGHT=25
ENTRY=0,0
EXIT=4,6
OUTPUT_FILE=maze.txt
PERFECT=False
SEED=12346
```

- Ejecutar:

```
python3 a_maze_ing.py config.txt
```

**Recursos**
- MiniLibX: documentación incluida en `mlx/`.

**Uso de IA**
- testing y tareas repetitivas y monotonas

# A-maze-ing
