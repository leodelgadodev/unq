# Normalización

- Llevar el esquema de la base de datos a alguna de las formas normales, entendiendo las formas normales y dependencias funcionales.
- Cada paso de las FN tienen los pasos previos (ej. para hacer la 2da FN tengo que hacer la 1ra FN antes).

## Anomalías

Surgen de una mala descomposición con el proceso de aplicar mal normalización

- **De inserción**: Cada vez que inserto un dato, es necesario repetir los datos (ej. cuando descompongo un multivaluado de un profesor con muchos emails, voy a repetir la tupla del profe entera por cada email?)
- **De modificación**: Cada vez que se actualiza un dato es necesario actualizarlo en todos lados de las tuplas donde se usa (ej. en el anterior, si el profe cambia de sexo, se lo tengo que cambiar en todas las tuplas)
- **De borrado**: Si borro un dato asociado a muchas tuplas, se pierde la información (ej. si tengo codigo de depto y nombre depto en el dato del profesor, solo 1 profe lo tiene asignado, y lo borro, perdi el codigo y nombre del depto para siempre, porque no lo tenia en otra tabla)

---

## Dependencias Funcionales (DF)

- En una tabla común y corriente, todos los elementos de la misma en ppio son dependientes de la clave primaria (ej. el id 1 tiene una combinacion de valores especifica). Sin embargo, pueden haber otras dependencias no tan visibles entre los datos de la misma tabla (ej. una marca especifica significa que habra un color especifico), en otras palabras una dependencia funcional.
- X depende funcionalmente de Y si para cada caso de X **siempre** tiene asociado el mismo valor Y en una Relación<X, Y>.

![Untitled](Normalizac%20dc79c/Untitled.png)

- Proveedores tenia dependencias funcionales adentro, y que no eran solo con la PK:
    - CodProv → NomProv
    - CodProv → CodInsumo
    - ***CodInsumo → Precio***
- De no encargarnos de resolver estas DFs vamos a tener datos repetidos a lo largo de la tabla (ej. en la de arriba aparecen tuplas con NomProv repetido)

> **Hacer un Join Natural entre las dos tablas nuevas me deberia dar como resultado la tabla original?**  No necesariamente, ya que al hacer el join entre las tablas puedo obtener datos que originalmente no tenía o perder otros, generando anomalías en los datos. Para que pueda hacer el join tengo que separar las tablas de tal forma que tengan una **Descomposición sin pérdida**.
> 

- **Dependencia Total**: X → Y lo es si eliminar cualquier atributo de X hace que la dependencia deje de ser válida. (Ej. dni →persona, si borro el dni pierdo la dependencia)
- **Dependencia Parcial**: X→ Y si saco cualquier atributo acá, la dependencia sigue siendo válida. (Ej. id ^ warehouse → warehouse address. Si saco id, puedo obtener igual warehouse adress)

> **Que haya 1 caso de un atributo que no cumpla la dependencia, la anula totalmente? SI.**
> 

> **Las dependencias son siempre conmutativas?** NO, ya que si bien (marca →modelo) === (modelo → marca), (dni → nombre) =/= (nombre → dni). Solo son conmutativas si los dos atributos son únicos.
> 

### Clave Candidata

- Subconjuntos de atributos que podrían ser una clave primaria (ej. combinaciones de atributos, que podrian ser un conjunto con un solo elemento).
- Si le saco un atributo, deja de ser clave.
- Compuesto por **Atributos primos**

### Dependencia Funcional Transitiva

---

## Primera FN

- Todos los multivaluados pasan a ser su propia relación, en el cual deja de ser atributo de la relación original y se lleva la PK de donde proviene como PK y FK.
- No existen atributos multivaluados ni compuestos, solo existen atributos atómicos.
- Para justificar que está en 1ra FN, "está xq todos los valores son atómicos".
- Compuestos se descompone en "prefijo_caracteristica". Ej. Persona<nyAp(nombre, apellido)> ⇒ Persona<nyAp_nombre, nyAp_apellido>

*Sin 1FN*: 

- PERSONA<Cuit, NyAp, puesto, {email}>

*Con 1FN:*

- PERSONA<Cuit, NyAp, puesto>
- EMAIL<Cuit, email>

*Sin 1FN*: 

- DEUDA<Cuit, {(deuda_monto, deuda_fechaVencimiento)}>

*Con 1FN:*

- DEUDA<Cuit, monto, fechaVencimiento>

---

## Segunda FN

- Se eliminan todas las DFs parciales y se llevan a otras tablas, dejar sólo las DFs totales.
- Pista: analizar DFs que salgan a partir de las PK. Especialmente importante si tengo varios atributos como PK.
- Pista: anotar primero todas las DFs que haya.
- Justificacion: una relación o tabla está en 2da FN si está en 1ra FN y no tiene dependencias funcionales parciales.

*Sin 2FN:*

- LOTE<Id, Warehouse_id, Quantity, Warehouse_adress>
- ***Quantity*** depende de ***Id*** y ***Warehouse_id***. Si saco uno de los dos no puedo obtener ***Quantity***.
- ***Warehouse_adress*** depende de ***Warehouse_id***. Puedo eliminar ***id*** que todavia lo voy a poder conseguir.
    - En resumen, las DFs son:
    - Id ^ warehouse_id → quantity (Total)
    - id ^ warehouse_id → warehouse_adress (Parcial)
    - warehouse_id → warehouse_adress (Total)

*Con 2FN:*

- LOTE<Id, Warehouse_id, Quantity>
- WAREHOUSE<*Warehouse_id*, Warehouse_adress>
    - Las nuevas DFs son:
    - Id ^ warehouse_id → quantity (Total)
    - warehouse_id → warehouse_adress (Total)

## Tercera FN

- Se eliminan todas las DFs transitivas y se llevan a otras tablas.
- Justificacion: Está en 3FN porque no hay DFs transitivas (o no lo está, por la presencia de alguna, y poner cual)

## Algoritmo de Normalización

- Para pasar una relación de 1ra FN a 3ra FN sin mucho quilombo

**(1)** Determinar las DFs

**(2)** Determinar la PK

**(3)** En base a la clave primaria, identificar en qué FN está la relación

**(4)** Para llevar a 2da FN, eliminar dependencias parciales

**(5)** Para llevar a 3ra FN, eliminar dependencias transitivas

**(6)** Para llevar a 4ta FN, eliminar dependencias multivaluadas

- **Atributo determinante**: el que está a la izq. de la DF
- **Atributo determinado**: el que está a la der. de la DF (solo relevantes los que tambien son determinantes)
- **Atributos resto**: cuando no son ninguno de los dos casos

1. A veces me las da el enunciado, a veces los tengo que encontrar yo.

1. 

**PK** = **Determinantes** - **Determinados** + **Resto**

Ej.

R<A, B, C, D, E>

- DF1: A → C (Parcial)
- DF2: B → D, E (Parcial)
- DF3: D → E (Transitiva)

**PK** = {A, B, D} - {C, D, E} + {}

PK = {A, B}

La relación está en 1ra FN

4.

Uso las DFs parciales para ir restandole a la relación original sin descomponer:

DFx: X → Y

Construyo Rx: Rx<X, Y> 

Calculo residual = R. original - {Determinados de DFx} = Residualx<...> 

Repetir estos pasos con todas las DFs parciales, y usando el residual anterior para calcular el proximo.

Ej.

1er. paso

DF1: A → C

R<A,B,C,D,E>

R1<A, C>

Construyo residual =

R - {C} = Residual1<A, B, D, E>

2do paso, ya eliminamos una dependencia parcial en el paso anterior

DF2: B → D, E

R2<B,D,E>

Construyo Residual =

Residual1 - {D,E} = Residual2<A,B>

R1, R2, Residual2 ya no tiene DFs parciales

 :. estamos en 2da FN 

3er paso, para pasar a 3ra FN

Partiendo de R1, R2 y Residual2, si las cruzo con join natural obtengo la tabla original

R2 no está en 3ra FN porque hay transitividad entre D → E, R1 y Residual ya estan en 3ra FN xq no tienen transitivas.

Entonces, con R2 construyo:

DF1: B → D

DF2: D → E

R2<B, D, E>

Las DFs se convirtieron c/u en su propia tabla

R2.1<B, D>, R2.2<D, E>

Resultado final:

R1, R2, R2.1, R2.2, Residual2 están en 3FN

[Practica 5](Normalizac%20dc79c/Practica%205%2038e11.md)

Como voy a guardar los datos vs

Como estoy representando los datos

Ej. estudiante tiene num. legajo y DNI. Desde la implementacion da lo mismo, pero segun lo que quiero representar mi dominio que es estudiantes de la UNQ, tiene mas sentido que use el num. legajo