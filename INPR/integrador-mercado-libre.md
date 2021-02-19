# Gobstorcado Libre

Nos pidieron implementar comportamiento de un sistema de compra y venta de productos para toda Latinoamérica unida. Para ello contamos con los siguientes registros:

```js
type GobstorcadoLibre is record {
	field usuarios // lista de Usuario
	field productos // lista de Producto
}

type Usuario is record {
// INV. REP: El email es unico por usuario
// INV. REP: El
	field email // string
	field nivel // number
	field saldo // number
	field compras // lista de Producto
}

type Producto is record {
	field precio // number
	field tipoDeProducto // TipoDeProducto
}

type TipoDeProducto is variant {
	case Tecnologia {}
	case Mueble {}
	case Almacen {}
}
```

También contamos con las siguientes funciones y procedimientos auxiliares:

- `esBlackFriday()` denota si Gobstorcado Libre está ofreciendo ofertas de Black Friday para productos de todo tipo.
- `esBlackMonday()` denota si Gobstorcado Libre está ofreciendo ofertas de Black Monday para productos de tecnología.
- `PonerProducto(unProducto)` coloca un producto en la celda actual. Precondición: en la celda actual no hay otro producto.
- `SacarProducto()` saca un producto de la celda actual. Precondición: en la celda actual hay un producto.

Por último contamos con un despacho (el tablero de Gobstones) para guardar los productos de GobstorcadoLibre.

Implementar las siguientes funciones y procedimientos:

- `gobstorcadoLibreTrasDarDeAltaUnUsuario_(unGL, unEmail)` denota el GobstorcadoLibre luego de crear un nuevo usuario y agregarlo a la lista de usuarios. El usuario inicia con nivel 1, sin saldo y sin compras.
- `ActualizarStock(unGL)` que coloca productos en el despacho según como aparecen en el orden de la lista de productos de GobstorcadoLibre. Previo a esto hay que retirar todos los productos del despacho. Nota: los muchachos del despacho prefieren ir acumulando los productos en un recorrido de Este a Norte, según ellos se les hace más fácil.
- `DespacharProducto(unProducto)` saca del despacho un producto del tipo del producto indicado. Nota: los muchachos del despacho prefieren ir sacando el primer producto que encuentren del tipo indicado según un recorrido de Este a Norte, según ellos se les hace más fácil.
- `gobstorcadoLibreTrasUnaCompraDe_(unUsuario, unProducto, unGL)` denota el GobstorcadoLibre tras realizar una compra. Para ello hay que tener en cuenta varias cosas:
    - Si el precio del producto supera el saldo disponible del usuario, denota boom.
    - Registrar la compra en la lista de compras del usuario. Si el numero de la compra es divisible por 10, subir el nivel del usuario.
    - Si es black friday, aplicar un descuento del 10% al producto.
    - Si es black monday y el producto es de tecnología, aplicar un 5% de descuento al producto.
    - Los descuentos son acumulables entre sí.
    - Descontar el saldo del usuario tras la compra.
    - Retirar el producto de la lista de productos disponible en GobstorcadoLibre.
    - Actualizar al usuario en la lista de usuarios de GobstorcadoLibre.
