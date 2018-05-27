## Reporte del módulo de cómputo matricial

#### Motivación
En mi caso dicidí leer el paper "A singular value decomposition on GPU using CUDA", ya que me parece que lo relacionado con procesamiento en la GPU es un tema que hoy en día esta teniendo un gran auge en el campo de la ciencia de datos.

Los autores del paper comienzan explicando que los algoritmos que implementan *SVD* son sumamente valiosos no sólo porque es un resultado de gran poder, ya que las operaciones de matrices utilizando *SVD* son más robustas antes errores numéricos; sino que también porque a lo largo del tiempo se han venido desarrollando más y más aplicaciones donde *SVD* es parte fundamental de su éxito, algunas de ellas son:

- Cálculo de la pseudoinversa de una matriz
- Análisis de componentes principales
- Procesamiento de señales
- Reconocimiento de patrones

No entraré tan a detalle en cuanto al desarrollo de cada uno de los algoritmos que toca el paper, sin embargo sí me parece relevante recordar en qué consiste *SVD*. La *SVD* de una matriz <a href="https://www.codecogs.com/eqnedit.php?latex=A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A" title="A" /></a> de <a href="https://www.codecogs.com/eqnedit.php?latex=m\times&space;n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m\times&space;n" title="m\times n" /></a>, es cualquier factorización  de la forma

<p align="center">
<a href="https://www.codecogs.com/eqnedit.php?latex=A&space;=&space;U\Sigma&space;V^{T}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A&space;=&space;U\Sigma&space;V^{T}" title="A = U\Sigma V^{T}" /></a>
</p>

donde <a href="https://www.codecogs.com/eqnedit.php?latex=U" target="_blank"><img src="https://latex.codecogs.com/gif.latex?U" title="U" /></a> es una matriz ortogonal de <a href="https://www.codecogs.com/eqnedit.php?latex=m&space;\times&space;m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m&space;\times&space;m" title="m \times m" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=V" target="_blank"><img src="https://latex.codecogs.com/gif.latex?V" title="V" /></a> es una matriz ortogonal de <a href="https://www.codecogs.com/eqnedit.php?latex=n&space;\times&space;n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n&space;\times&space;n" title="n \times n" /></a> y <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> es una matriz diagonal de <a href="https://www.codecogs.com/eqnedit.php?latex=m&space;\times&space;n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m&space;\times&space;n" title="m \times n" /></a>.

La rapidez con la que ha aumentado el performance del hardware de gráficos ha convertido a la GPU en una excelente herramienta a explotar para tareas que requieren un trabajo de cómputo intensivo.

Los autores presentan una implementación de *SVD* para matrices densas en la GPU usando CUDA, utilizan la librera de NVIDIA, CUBLAS y CUDAkernels. Su propuesta de implementación logra calcular la *SVD* de matrices muy grandes, la cual en CPU es imposible de calcular por cuestiones de memoria. Los autores destacan que gracias a las librerías de CUDA creadas para el proceso de operaciones matemáticamente complejas, es sencillo programar su algoritmo.

#### Algoritmo

Con base a lo que aborda el texto respecto a distintos *"approaches"* que recientemente se han tenido para implementaciones en la GPU, podemos confirmar una vez más que es un tema que está y ha estado tomando mucha relevancia.

Para la implementación propuesta por los autores ellos utilizan el método de Golub-Reinsch ya que este es simple y compacto, además de que se adapta bien a la arquitectura SIMD GPU. Este método es usado en la paquetería de LAPACK y es un algoritmo de dos pasos, primero la matriz original es reducida a una matriz bidiagonal mediante una serie de transformaciones "householder" (es una transformación lineal del espacio que consiste en una reflexión pura con respecto a un plano, fuente:Wikipedia); posteriormente la matriz bidiagonal resultante es diagonalizada utilizando iteraciones de factorización QR.

#### Sección de bidiagonalización

A continuación el paper presenta una explicación del algoritmo para transformar una matriz en otra bidiagonal, con algunas mejoras, creo que los puntos más importantes de esta explicación son: la idea de romper en bloques las operaciones y por otro lado la explicación de la comunicación entre la GPU y CPU, ya que de ahí se observa el área de oportunidad para mejorar las implementaciones que ya existían.

En lo que se refiere ya a la parte de bidiagonalizar en la GPU, los autores explican que con CUBLAS y matrices cuyas dimensiones son múltiplos de 32 se obtiene el mejor performance, por lo que justamente en su implementación llenan de ceros conforme sea necesario para llevar las matrices y vectores a la dimensión superior ms cercana que sea múltiplo de 32. Mencione anteriormente que los comentarios acerca de la interacción en cuestión de memoria entre la GPU y CPU me parece muy interesante y los autores justamente explotan esto al evitar transferencias pesadas que alentarían los procesos.

#### Sección de diagonalización de una matriz bidiagonal

La matriz bidiagonal que en teoría ya tenemos, la podemos diagonalizar mediante varias iteraciones de factorización QR. Si la matriz resultante de la sección anterior es <a href="https://www.codecogs.com/eqnedit.php?latex=B" target="_blank"><img src="https://latex.codecogs.com/gif.latex?B" title="B" /></a>, entonces se puede descomponer como

<p align="center">
<a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma&space;=&space;X^{T}BY" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma&space;=&space;X^{T}BY" title="\Sigma = X^{T}BY" /></a>
</p>

donde <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> es una matriz diagonal, <a href="https://www.codecogs.com/eqnedit.php?latex=X" target="_blank"><img src="https://latex.codecogs.com/gif.latex?X" title="X" /></a> y <a href="https://www.codecogs.com/eqnedit.php?latex=Y" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y" title="Y" /></a> son matrices unitarias ortogonales.






