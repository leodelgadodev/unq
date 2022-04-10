# Practica 5

**EXPOSICION**<museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, precioEntrada>

DFs:

1) museo → ciudadMuseo

2) nombreObra → nombreGaleria, museo, añoCreacion

3) nombreGaleria, museo → precioEntrada

Claves candidatas:

nombreObra

nombreObra, museo, nombreGaleria ? si elijo esta, no es una buena clave candidata ya que necesitaria una tabla gigante que ya la dividi en pedazos. La duda es, puedo decir que es una clave candidata posible?

Clave primaria:

nombreObra

1FN:

**EXPOSICION**<museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, precioEntrada>

⇒

**EXPOSICION**<museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, precioEntrada>

2FN:

**EXPOSICION**<museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, precioEntrada>

⇒

MUSEO<museo (FK), ciudadMuseo>

OBRA<nombreObra, nombreGaleria, museo, añoCreacion>

GALERIA<nombreGaleria (FK), museo (FK), precioEntrada>

3FN:

**EXPOSICION**<museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, precioEntrada>

aplico DF1 sobre la relacion original (Exposicion)

MUSEO<museo, ciudadMuseo> (la PK es determinada x la DF)

RESIDUAL 1<nombreGaleria, nombreObra, añoCreacion, precioEntrada, museo>

aplico DF3 sobre RESIDUAL 1

GALERIA<nombreGaleria, museo, precioEntrada>

RESIDUAL 2<nombreObra, añoCreacion, nombreGaleria, museo>

aplico DF2 sobre RESIDUAL 2

OBRA<nombreObra, añoCreacion, nombreGaleria, museo>

RESIDUAL 3<nombreObra, nombreGaleria, museo>