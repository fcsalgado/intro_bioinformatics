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
![barra](/home/fabian/Documents/bioinformatics_urosario/images/barra.png)
y activa los simbolos `.*` y `Aa`

2. Usando la barra de busqueda y remplazo conviertan el siguiente nombre científico `Gasteracantha cancriformis` en `G. cancriformis` ¿Cómo lo hicieron?

3. Ahora usando el mismo método de busqueda/remplazo transformen los siguiente nombres científicos,  `Gasteracantha cancriformis Macracantha arcuata Austracantha minax` Ahora si fue más difícil, ¿No?

4. Hagamos el último intento con `XXXX`. Imposible!

Usarán ahora su primer wildcard: `\w` . este wildcard representa cualquier número (0-9), letra (A-z) y guión bajo ( _ )
