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

### Tablero de juego inicial

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

El wko _arena_ nos permitirá parametrizar algunas cuestiones (más abajo las desarrollaremos).

El tablero inicial debe visualizarse de la siguiente manera:

![image](images/tableroOriginalChico.png)

En él aparece

- elDiego, nuestro personaje principal (lo que en Wollok Game se denomina _visual character_)
- un ícono que representan 10 monedas de oro
- una serie de artefactos: espadas, armaduras y máscaras
- nuestro primer rival del Diego, el enigmático dt _sampaoli_

Todas las imágenes pueden obtenerse en el [directorio assets de este repositorio](assets/), cada grupo es libre de modificar las imágenes por otras según lo considere conveniente.

A continuación describiremos el comportamiento esperado dentro del juego.

### Configuración del juego

- el fondo del juego se define por el [archivo soccerWallPaper.jpg](assets/soccerWallPaper.jpg). 
- el título debe decir "Hechiceria" o algo similar
- el tamaño de la pantalla debe ser de 25 x 15 según lo configura el wko _arena_

### Personaje principal: elDiego

![image](assets/maradona.png)

El Diego es el personaje principal del juego y como tal tiene caracter visual, pero además se asocia con un personaje (el modelo que construiste en las tres entregas anteriores). Ese modelo comienza con 20 monedas de oro en su haber, no tiene artefactos y la información sobre el hechizo preferido es irrelevante para el juego.

Los movimientos del Diego no necesitan ser programados ya que Wollok Game los provee por ser el personaje principal, pero sí debemos tener en cuenta el siguiente comportamiento:

- la imagen por defecto se obtiene del [archivo maradona.png en assets](assets/maradona.png) si la habilidad de lucha es menor o igual a 5, cuando la sobrepasa obtiene el efecto _wakanda forever_ [representado por el archivo maradona2.png](assets/maradona2.png)

- Cada vez que se presione la tecla I, debe decirnos la cantidad de monedas que tiene, la cantidad de artefactos que posee y su habilidad de lucha

![images](images/infoDiego.gif)


### Adquiriendo monedas

![image](assets/bitcoin.png)

