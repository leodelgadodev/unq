# MER

## Elementos

- [   ] Entidades - Representación de una cosa o idea del dominio
- < - > Relaciones - (ej. "Compra"). Forma en la que dos entidades interactúan entre sí, por medio de un significado específico. Se representan con un rombo
- (  )  Atributos - Dato individual de una entidad
    - Simples
    - Compuestos (ej. direccion → calle, direccion → numero)
    - Multivaluados - muchos simples en uno solo (ej. una escuela tiene años lectivos)
    
    > **multivaluados se escriben en singular o en plural? Ejercicios resueltos x la profe tienen ambos**
    > 
    - Calculados/derivados - Puede obtenerse a partir de un dato de la instancia por medio de un calculo. Va con ( ) con linea de puntitos
    - Si un atributo es PK, va subrayado

Entidades → Sustantivos

Atributos → Sustantivos

Datos (de atributos) →Sustantivos o adjetivos

Relaciones → Verbos

## Características

- Primera etapa del diseño de una BD.
- NO intentar optimizar cuestiones que me hagan ruido (ej. usar el Multivaluados, no intentar usar la 3FN de una, porque para la primera etapa de MER que es la que vemos no tienen sentido).
- Modelarlo basandonos en que siempre va a tener al menos 1 instancia de la relación. Para que sea un ( 0:X ) me lo tiene que indicar explicitamente el enunciado.
- Modelarlo haciendolo atributo-first y no relaciones-first.
- Cuando hay ambiguedades en el enunciado pedido, puede que haya varias soluciones correctas. Optar por la solución más inclusiva y mejor descriptiva de la realidad. (Ej. una solución de una relacion puede tranquilamente ser 0:N o 1:N)
- Atributo clave == PK
- Los nombres de las relaciones deben ser todos distintos, no pueden haber dos relaciones entre entidades que se denominen con el mismo verbo. Esto es porque al pasarlo a MR se convierten en tablas.

## Cardinalidades

- Medida de en cuántas instancias de un tipo de relación puede aparecer una determinada entidad (instancia) en un determinado rol
- Se ponen en la entidad receptora, en el objetivo de la relación si la relación es 1:1 o N:M. (Ej. '"Compra" lleva la cardinalidad del lado de la entidad que es comprada)
- Se ponen en el lado del muchos en la relación 1:N

[ Profesor ] - - ( N : M ) - - - < Dicta > - - - ( N : M ) - - [ Curso ]

[ Profesor ] - ( 1 : N ) - - - - < Pertenece > - - - - ( 1 : 1 ) - - [ Escuela ] 

[ Estudiante ] - ( 1 : N ) - - - < Pertenece > - - - - ( 1 : 1 ) - - [ Grupo ]

- Una persona podria adoptar o on a una o más mascotas
- A su vez, una mascota puede ser o no adoptada por una persona

[ Persona ]  - ( 0 : 1 ) - - - < Adopta > - - - ( 0 : N ) - - [ Mascota ]

## Entidad débil

- Aquella que depende de otra para identificarse
- No tiene PK por si misma
- Se representa con dos recuadros en la entidad y dos recuadros en el rombo de la relación
- Puede tener una PK compuesta por un atributo de la entidad con la que se relaciona y otro atributo propio de la entidad debil

Ej.

Chat - ( 1 : 1 ) - - - < < Tiene > > - - - - ( 1 : N ) - - [ [ Mensaje ] ]

Cuenta  - ( 1 : 1 ) - - - < < Emite > > - - - - ( 1 : N ) - - [ [ Transacción ] ]

## Entidad recursiva

- Una entidad puede tener relación con otra instancia de su mismo tipo

Ej.

[ Materia ]  - ( 0 : N ) - - - < Correlativa > - - - - ( 0 : N ) - - [  Materia  ]

Es correlativa de                               Es continuada por

[ Profesor ]  - ( 1 : 1 ) - - - < Supervisa > - - - - ( 1 : N ) - - [  Profesor  ]

Es supervisado por                             Supervisa a