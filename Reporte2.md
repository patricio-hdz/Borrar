## Reporte del módulo de optimización convexa

El artículo en general toca el tema de "Avances en optimización convexa de algoritmos para Big Data", la idea es de los mismos es reducir las problemáticas computacionales, de almacenamiento y de comunicación.

#### Sección de Convex optimization in the wake of Big Data

Hasta hace algún tiempo, la importancia que tenía el tema de optimización convexa recaía en distintas aplicaciones, sin embargo dos de las más obvias eran; tener algoritmos eficientes que fueran capaces de calcular soluciones optimas globales y la habilidad de usar geometría convexa para revisar propiedades de la solución. Hoy en día, los problemas de poder manejar datasets cada vez más grandes y resolver problemas de dimensiones inimaginables hace algún tiempo, le han dado un nuevo boost a la optimización convexa.

Notamos que para la parte de las bases de optimización convexa, los autores dan una descripción general de:

- **Métodos de primer orden**: Obtienen soluciones de precisión media-baja, estos métodos logran convergencia casi independiente al número de dimensiones con las  que se este trabajando, e normalmente se programan bajo una metodología que los hace excelentes candidatos para implementaciones distribuidas o en paralelo.

- **Randomization**: Estos algoritmos vuelven *escalables* métodos de primer orden, ya que podemos controlar su comportamiento esperado. Mediante la aleatorización muchas veces podemos utilizar una muestra aleatoria para obtener el comportamiento global, con esto obtenemos resultados en tiempos muchos más cortos.

- **Implementaciones en paralelo o distribuidas**: Estas implementaciones sacan jugo a las nuevas capacidades tecnológicas mediante una optimización de muchos de los métodos de primer orden.

En cuanto a los métodos de primer orden, se presenta la ecuación tradicional y el punto relevante desde mi opinión es que se pueden obtener soluciones con operaciones sencillas como multiplicación de matriz-vector. Además tenemos una variante como LASSO para agregar un término de regularización y mejorar el performance del algoritmo. Se da el ejemplo de como el gradiente estocástico se escala de manera más eficiente que un gradiente conjugado, ya que sólo requerimos acceder a una fracción de los datos.

#### Sección de First-Order Methods for Smooth and Non-Smooth Convex Optimization

En esta sección los autores abordan principalmente el *framework* de gradiente proximal y cómo es que problemas *non-smooth* pueden ser resueltos casi tan eficientemente como sus contrapartes *smooth*.




#### Conclusiones

Al tener grandes cantidades de datos, se ha comenzado a bajar un poco el nivel de exigencia en cuanto a precisión en las soluciones de los algoritmos, sin embargo, se ha ganado en cuanto a poder tener estimaciones o resultados dentro de bases inmensas, que de otra manera nos dejarían incompetentes de poder sacar valor de ellas.

























#### Referencia

https://arxiv.org/pdf/1411.0972.pdf

https://www.codecogs.com/eqnedit.php
