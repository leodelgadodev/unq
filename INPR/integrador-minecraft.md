# Gobstonecraft

Gobstonecraft es un juego de construcción, exploración, creación, combate, y sobre todo, minería. En este examen vamos a intentar replicar algunas de estas funcionalidades. Para ello, contamos con los siguientes registros:

```js

type Personaje is record {
	field inventario // Inventario
	field armadura // Armadura
}

type Inventario is record {
/* 
	INV. REP: 
	- barraDeAccion no puede almacenar mas de 9 items
	- espacioInterno no puede almacenar mas de 18 items
*/
	field barraDeAccion // lista de Item
	field espacioInterno // lista de Item
}

type Armadura is record {
	field casco // Item
	field chaleco // Item
	field pantalon // Item
	field botas // Item
}

type Item is variant {
	case CascoHierro {}
	case ChalecoHierro {}
	case PantalonHierro {}
	case BotasHierro {}
	case MineralDeHierro {}
	case PicoDeHierro {}
}
```

Además, contamos con las siguientes funciones y procedimientos: 

- `hayZombi()` indica si hay un zombi en la celda actual.
- `hayMineral()` indica si hay un mineral de hierro en la celda actual.
- `QuitarZombi()` retira el zombi de la celda actual. Precondicion: hay un zombi en la celda actual.
- `QuitarMineral()` retira el mineral de la celda actual. Precondicion: hay un mineral en la celda actual.

Implementar las siguientes funciones y procedimientos:

- `Atacar()` - Si hay un zombi en la celda actual, lo quita.
- `hayEspacioEnInventario(unPersonaje)` - denota si un personaje tiene espacio en su inventario interno o en su barra de acción.
- `personajeConNuevoItemEnInventario(unPersonaje, unItem)` - dado un personale y un item, denota el personaje con el item guardado en su inventario. Si hay espacio en el espacio interno, lo guarda ahí, sino en la barra de acción. Precondición: hay espacio en el inventario disponible.
- `personajeConNuevaPiezaDeArmaduraPuesta(unPersonaje, unItem)` - dado un personaje y un item de variante de algún tipo de armadura (casco, chaleco, pantalón o botas) denota el personaje con el item de armadura puesta en el lugar que corresponda. Precondición: el slot de armadura del variante que recibe está libre.
- `personajeConItemMovidoABarraDeAccion(unPersonaje, unItem)` - denota el personaje con el item (que debe encontrarse en el inventario interno) en su barra de accion, simulando un movimiento del item. Si el personaje tiene más de un item del indicado, mover cualquiera de ellos. Precondicion: El personaje tiene el item indicado en su inventario interno y tiene espacio disponible en su barra de accion.
- `Minar(unPersonaje)` - Si hay un mineral en la celda actual, y unPersonaje tiene un PicoDeHierro en su barra de acción, quita el mineral.
- `personajeConNuevoCrafteo(unPersonaje, unItem)` - Denota al personaje con un nuevo item creado en su inventario interno, segun el item que le pasemos para craftear. Para ello, el personaje debe contar con una determinada cantidad de minerales de hierro segun la siguiente tabla:

    3 minerales → Pico de hierro

    4 minerales → Botas de hierro

    5 minerales → Casco de hierro

    7 minerales → Pantalon de hierro

    8 minerales → Chaleco de hierro

- Si no es posible craftear el item, hacer `boom` . El personaje debe usar primero minerales en su inventario interno y luego en su barra de acción. Precondición: El personaje tiene espacio en su inventario interno para el item crafteado.
- `personajeTrasExpedicionDeMineria(unPersonaje, unPicoDeHierro)` - Dado un personale y un item de variante PicoDeHierro, denotar el personaje tras un recorrido por un tablero lleno de minerales y zombis, en el cual el personaje mine y ataque a los mismos a medida que los vaya encontrando. Cada mineral de hierro que consiga minar, se lo guardará en el inventario hasta que se quede sin espacio en el inventario interno y luego en la barra de acción. Nota: Aunque se quede sin espacio en el inventario, debe completar la expedición.
- `personajeTrasExpedicionDeMineriaConMiedo(unPersonaje, unPicoDeHierro)` - Dado un personale y un item de variante PicoDeHierro, denotar el personaje tras un recorrido por un tablero lleno de minerales y zombis, en el cual el personaje mine todo lo posible y se detenga cuando se encuentre con un zombi. Cada mineral de hierro que consiga minar, se lo guardará en el inventario hasta que se quede sin espacio en el inventario interno y luego en la barra de acción. Nota: Aunque se quede sin espacio en el inventario, debe completar la expedición.
