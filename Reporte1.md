## Reporte del módulo de cómputo matricial

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

donde <a href="https://www.codecogs.com/eqnedit.php?latex=U" target="_blank"><img src="https://latex.codecogs.com/gif.latex?U" title="U" /></a> es una matriz ortogonal de <a href="https://www.codecogs.com/eqnedit.php?latex=m&space;\times&space;m" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m&space;\times&space;m" title="m \times m" /></a>,
