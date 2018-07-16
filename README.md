# TP Objetos 2018 PDP - Rol de Lucha y Hechicería

## Entrega 4 - Wollok Game

### Cambios al modelo

Se requiere que todos los personajes no controlados sepan pelear contra cualquier otro personaje, lo que implica "medir fuerzas" en base a su habilidad de lucha. Esto se resuelve de la siguiente manera:

```javascript
	method pelearContra(personaje) {
		const propio = self.habilidadLucha()
		const ajeno = personaje.habilidadLucha()
		const numeroPropio = (100 / (propio + ajeno)) * propio * 1.5
		const numeroAzar = 1.randomUpTo(100)
		return numeroAzar > numeroPropio
	}
```

### Tablero de juego

Tendremos un tablero del juego de 25 x 15 celdas, pero el tamaño podría variar. Aconsejamos para ello definir el siguiente objeto visual:

```javascript
import hechiceria.*
import wollok.game.*

object arena {
	method ancho() = 25
	method alto() = 15
	method posicionPersonaje() = game.at(1, 1)
	method posicionRival() = game.at(7, 0)
	method comprar(cosa) = {
		personaje => personaje.comprarArtefacto(cosa)
	}
	method comerciante() = new Comerciante(tipoCobro = new Independiente(10))
}
```

