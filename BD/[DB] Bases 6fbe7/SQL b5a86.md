# SQL

## Joins

- Inner Join → Join entre A y B, donde si una tupla de A no logra matchear con B se descarta (hay data asimétrica entre las dos tablas y no es un 1 a 1 con cada tupla)
- Outer Joins → Joins que no descartan tuplas en caso de no matchear. En algunas docs o algunos flavors de SQL la consulta se escribe con la palabra "Outer" pero en el SQL común no.
    - Left Join → no descarta las de A pero descarta si no matchea en B
    - Right Join → No descarta las de B pero descarta si no matchea con A
    - Full Join → No descarta ninguna
    - Natural Join → ojo con este xq cuando lo tire en el tuto interactivo me dio cualquier cosa
    - Cross Join → Producto cartesiano

[joins.webp](SQL%20b5a86/joins.webp)

```sql
SELECT * FROM pepito AS tablaA JOIN tablaB ON tablaA.id = tablaB.tablaA_id
```

### Aggregate Functions

- COUNT(*) → me cuenta las rows
- COUNT(column) → me cuenta las rows, sin contar los que tengan null para esa column
- SUM(column) → suma todos los valores de ese column

### Group By

- Basicamente un Reduce pero de SQL y aplicado a una tabla. Se reduce segun la columna que le indique (todos los que tengan x valor en la column especificada se colapsan a una sola tupla).
- El cómo se colapsan las tuplas viene dado por lo que lo acompañes, que puede ser con un where, con un aggregate u otra cosa.
- Siempre siempre se ejecuta despues de un where, nunca antes porque se rompe todo. Para poder filtrar en un group by por una condicion se usa `having`
- En principio si estoy usando aggregate functions es por acá, si no estoy usando ninguna hay otra solucion disponible sin usar esto
- NO puedo usar aggregate functions en un WHERE, si o si en el SELECT

```sql
SELECT role, COUNT(*) nro_employees FROM employees GROUP BY role;
```

![Untitled](SQL%20b5a86/Untitled.png)

### Operadores artiméticos/de Conjuntos

- x `BETWEEN` y, z → recibe dos valores numericos y dice si lo que recibio antes está entre esos dos
- a `IN/NOT IN` C(x)  → recibe una columna o elemento y un conjunto y dice si ese elemento está en ese conjunto

> **Podria recibir dos conjuntos? NO xq la comparacion IN opera a nivel datos**
> 
- C(x) `EXCEPT` C(y) → Resta
- C(x) `UNION` C(y) → Suma
- C(x) `INTERCEPT` C(y) → Intercepcion
- 

### Todo junto

```sql
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;
```

### Operaciones CRUD

### Insert

```sql
-- puedo ponerlo sin el val del id para que lo genere solo
INSERT INTO a_table (val1, val2, val3, ..., valN) VALUES
(a1, a2, a3, a4, aN),
(b1, b2, b3, b4, bN),
(..etc..);
```

### Update

```sql
-- en el set solo defino las columnas que quiero actualizar
-- pro tip intentar arrancar haciendo el WHERE con un id si es posible
-- pro tip 2 primero hacer el select con un where para ver que estemos 
-- los datos correctos
UPDATE mytable
SET column1 = value_or_expr, 
    column2 = another_value_or_expr, 
    …
WHERE condition;
```

### Delete

```sql
DELETE FROM movies
WHERE condition;
```

### Operaciones a nivel Tabla

```sql
ALTER TABLE t1 ADD COLUMN columnA datatype;
ALTER TABLE t1 RENAME COLUMN columnA TO columnB;
ALTER TABLE t1 DROP COLUMN columnA;
ALTER TABLE t1 ADD CONSTRAINT constraint_name <type, etc>;
-- strings van con comillas simples
-- SIEMPRE pensar si necesito clavar un DISTINCT (pista, si no estoy seleccionando
-- la pk entera muy probablemente necesite un distinct)
-- SIEMPRE todas las palabras reservadas van con mayuscula
```

### Constraints

```sql
CONSTRAINT <nombre del constrein> FOREIGN KEY(tabla) REFERENCES tabla(id);
-- El nombre del constraint tiene que ser unico. Ej. tabla1_fk, tabla2_fk

-- Si hago referencia a la PK de otra tabla OJO de traerme la PK entera:
CONSTRAINT local_fk FOREIGN KEY(local_id, shopping_id) 
	REFERENCES local(id, shopping_id);

-- si necesito que una FK sea PK:
CONSTRAINT shopping_fk FOREIGN KEY(shopping_id) REFERENCES shopping(id),

-- si necesito una PK compuesta por mas de una columna:
CONSTRAINT local_pk PRIMARY KEY(id, shopping_id);

-- si necesito validar que futuros inserts cumpla de que sea uno de
-- entre varios valores especificos posibles:
CONSTRAINT colores_posibles CHECK (
	color IN ('Rojo', 'Verde', 'Azul', 'Violeta', 'Marrón')
);
```

- LIKE '%a%' → todos los que tengan a

### Like

- LIKE 'a%' → todos los que empiecen con a
- LIKE '%a' → todos los que terminen con a

### ilike

- lo mismo pero no es case sensitive

### Indicaciones según el Enunciado

- Seleccionar * en los que "solo" me quedo con...
    - EXCEPT (Resta)
    
- Listar por X columna..
    - GROUP BY
    
- Ordenar de la A a la Z o de menor a mayor
    - ORDER BY ... ASC;
- Ordenar de la Z a la A o de mayor a menor
    - ORDER BY ... DESC;
    

> **Claves foraneas son siempre NOT NULL a menos que yo lo especifique como NULL?**
> 
- Si

> **Como se declara un autoincremental?**
> 
- Con SERIAL y sin definir el type INT

> **Como declarar una PRIMARY KEY que está compuesta por varios atributos?**
> 
- No declarandola de una y declarandola con un CONSTRAINT

> **Como definir un atributo que por defecto tiene un valor cuando creo la tabla si es que no le defino nada?**
> 
- `origen varchar(3) NOT NULL default 'ARG'`
- attr type default 'valor',