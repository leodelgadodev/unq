# Base de Datos

La Universidad Nacional de Quilmes nos pidió crear un motor de base de datos basado en el tablero de gobstones...  for science...

Para ello contamos con los siguientes registros:

```tsx
type Database is record {
// INV. REP: hay tantas filas como la cantidad de filas del tablero
// INV. REP: la primer fila del tablero es la primer fila de la lista de Sur a Norte
// INV. REP: indexFila es un numero mayor a 0 que representa la fila en donde se
// encuentra la proxima fila con la proxima key vacia en un recorrido
// INV. REP: indexKey es un numero mayos a 0 que representa la key en donde se
// encuentra la proxima key vacía dentro de la fila
	field fila // lista de Fila 
	field indexFila // numero 
	field indexKey // numero
}

type Fila is record {
// INV. REP: hay tantas keys como la cantidad de celdas de la fila
// INV. REP: la primer key de la fila es la primera celda de la lista de Oeste a Este
	field keys // lista de Key
}

type Key is record {
	field value // string
}
```

Y contamos con las siguientes funciones:

- `codificar()` denota un string que resulta de leer las bolitas de la celda actual. Si la celda actual está vacía, denota el string 'NULL'.
- `traducir(unaKey)` denota una lista de bolitas que resulta de leer el valor de una Key. Si el string de una key es 'NULL' denota una lista vacía.

Además de contar con todas las funciones y procedimientos implementados en cualquier práctica.

Implementar las siguientes funciones y procedimientos:

- `hayEspacioDisponible(unDatabase)` denota si hay Keys vacías en un Database.
- `databaseLuegoDeCreate_(unDatabase, unValue)` denota una database con un nuevo valor en la primera Key disponible en un recorrido a partir de la primera fila de la database disponible y los valores del indexFila y indexKey actualizados. Si no hay keys vacías denota boom.
- `databaseLuegoDeUpdate(unDatabase, unaFila, unaKey, unValue)` denota un database con el valor actualizado con el value provisto en la fila y key indicados.
- `codificarBaseDeDatos()` denota un nuevo database que resulta de codificar todas las celdas del tablero.
- `TraducirBaseDeDatos(unDatabase)` Genera cambios en el tablero de acuerdo a los valores de una database.
