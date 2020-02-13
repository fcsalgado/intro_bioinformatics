# **Regular expressions (expresiones regulares)**

Uno de los grandes problemas a los que se enfrenta un biólogo es organizar un texto. Imaginense tomando datos en campo o en el laboratorio, siempre se debe tener un orden de las cosas, ¿O no? :honeybee: :bookmark_tabs:

Estas notas, ya sean tomadas por nosotros u otro investigador, muchas veces necesitan ser moficadas con base en nuestras necesidades, y gastamos horas haciendo esto. Muchachxs, pues su vida va a cambiar, ya que estas modificaciones las podrán hacer en un segundo con las **expresiones regulares**

¿Cómo funcionan?

1. Deben bajar un editor de texto, yo les recomiendo [Atom](https://atom.io/)
2. Deben tener un texto a editar, obviamente
3. Deben usar algunos carateres especiales (wildcards)

Wildcard: Caracter especial que representa una variedad específica de caracteres

## Primer ejercicio
1. Abran el editor de texto Atom y teclea `crtl + f`. Aparecerá la barra de búsqueda y remplazo:
![barra](https://raw.githubusercontent.com/fcsalgado/bioinformatics_urosario/master/images/barra.png)
y activa el simbolo `.*`

2. Usando la barra de busqueda y remplazo conviertan el siguiente nombre científico `Gasteracantha cancriformis` en `G. cancriformis` ¿Cómo lo hicieron?

3. Ahora usando el mismo método de busqueda/remplazo transformen los siguiente nombres científicos,  `
```
 Gasteracantha cancriformis
 Macracantha arcuata
 Austracantha minax
 ```
 Ahora si fue más difícil, ¿No?

4. Hagamos el último intento con `Ameiva ameiva`. Imposible!

Usarán ahora su primer wildcard: `\w` . este wildcard representa cualquier número (0-9), letra (A-z) y guión bajo ( _ ). Veamos como trabaja

## Segundo ejercicio

Imagina que quieres borrar las letras N,S,E y W de las siguientes coordenadas

```
+42 56'N +018 12'E
-18 12'S -142 42'W
```
¿Cúal es la solución?
- Una opción es buscar cada letra de manera independiente, pero recuerda que si algo se está repitiendo muchas veces es porque algo estamos haciendo mal
- La otra opción es usar el `\w`, recuerda que esta opción tambien remplaza números, ¿Qué hacemos?

## Tercer ejercicio

Vamos ahora a aprender a capturar texto, ¡esto es fundamental! para ello usaremos los `()` y el símbolo `$` seguido de números, ya veremos cómo.

Imagina que tienes esta lista de elementos:

```
5to
4to
2do
1ro
```
y deseamos quedarnos solo con los número y borrar las letras. para ellos debemos resolver ¿Cómo capturas todos los elementos de cada fila?

Estando ya capturados, utilicen los parentesis para separar el elemento que quieren. Ahora en la casilla de remplazo usen el siguiente término: `$1` ¿Funcionó? ¿Qué significará el número?

Ahora pulsen `ctrl + z` para volver al texto original

Para capturar dos partes del texto utilzaremos ahora la siguiente nomenclatura: `(\w)\w(\w\w)` y remplazaremos con los siguiente `$1$2` ¿Cambió en algo?

Ahora quiero que nuestro texto original, quede de la siguiente forma:
`Orden de llegada: <Número>`

¿Cómo lo harían?

## Cuarto ejercicio

Ahora conoceremos un nuevo simbolo que es amigo (parcero) de los wildcards y es el simbolo más (`+`), que simboliza que el mismo tipo de termino de interés debe estar más de una vez consecutiva. por ejemplo `\w+`

Volvamos al primer ejercicio, tomen la lista de especies y piensen en una forma de capturar la primera letra de cada género, luego el resto del género. ¿Cómo lo harían?

Nota: Recuerden usar todo lo que hemos aprendido.

## Quinto ejercicio

Ahora con el input del primer ejercicio obtengan el siguiente resultado:

```
Gasteracantha cancriformis G. cancriformis
Macracantha arcuata M. arcuata
Austracantha minax A. minax
```
¿Qué tal les fue?

## Sexto ejercicio

Ahora hablemos de los caracteres especiales. ¿Qué sucede si me encuentro con cosas como * o () o &. ¿Cómo los capturo?, bueno para eso vamos usar el backslash. Por ejemplo, si quiero capturar una `,` voy a ahacerlo de la siguiente forma `\,`

Ahora usen la siguiente frase:

`“What speaks to the soul, escapes our measurements.” (Alexander von humboldt)`

Y combiertanla en la siguiente:

`“our measurements speaks to the soul” humboldt.`

¿Cómo lo harían?

## Septimo ejercicio

¿ y existen otros wildcards?, ¡Por supuersto que si! una muy buena lista de wildcards los pueden encontrar en este [link](http://practicalcomputing.org/files/PCfB_Appendices.pdf), de un muy buen libro que se los recomiendo, se llama **Practical computing for biologist**

Lo que vamos a hacer ahora es que usando esta lista de referencia, ustedes van a transformar este [archivo fasta](https://www.ncbi.nlm.nih.gov/popset/1497464918), de tal manera que los encabezados que son así

`>MH258555.1 Gasteracantha cancriformis isolate SEQ01 cytochrome oxidase subunit 1 gene, partial cds; mitochondrial`

Queden así:

`>MH258555.1_G.cancriformis_SEQ01_COI_mitochondrial`

¡Esperen!

También quiero que solo queden los primeros 100 pares de bases. Cuando terminen, me muestran cómo lo hicieron.

¡Buena suerte! :neckbeard:
