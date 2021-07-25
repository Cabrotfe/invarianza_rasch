Análisis de propiedad de invarianza en modelos de Rasch
================

# Propiedad de invarianza:

¿Qué es medir en psicología? Para intentar contestar esta pregunta deberíamos ver qué propiedades tiene la medición:

Sistema intervalar: sistema de asignación de números que contiene una unidad de medida y el 0 es arbitrario. Podemos pensar este sistema como una escala o línea, en la que podemos ubicar una propiedad de un objeto. En este caso ya hablamos de medición pues se preserva una característica fundamental, que es la constancia de las diferencias de unidades en la escala. La diferencia entre 1 y 3 es igual a la diferencia de 3 y 5. Esto ocurre con la medida de temperatura, en que la diferencia entre 5 y 10 grados es igual a la de 10 y 15, para la variable de interés. Sin embargo, en este tipo de mecanismo de asignación de números, no es aplicable la razones, de modo que no es posible decir que 20 grados es el doble que 10 grados. Esto es porque el 0 es arbitrario, y no indica ausencia del atributo.

Independencia: la otra propiedad, relacionada a lo anterior, es que la propiedad medida es independiente al objeto usado para su medición. La distancia entre las unidades de medida respecto a un objeto no depende del objeto de comparación. Del mismo modo, la distancia entre dos variables (propiedades) medidas entre objetos no dependen de la unidad de medida del instrumento de medición.

Linealidad: debe poder expresarse en una línea que indica la ubicación del objeto medido.

Debe entregar un significado

Debe poder ser usado para decir algo respecto a cómo se comportará esa propiedad respecto a otros instrumentos de medida. Es decir, debe ser generalizable.

Veamos cómo el modelo de Rasch permite medir y en qué sentido la TCT no permite hacer medición propiamente tal.

## Invarianza de los parámetros de las personas:

Dado un nivel de habilidad, el modelo de Rasch y el IRT permite estimar ese nivel de habilidad usando distintos ítems, debido a que considera la dificultad (y la discriminación) o ubicación de los ítems al hacer la medición. Así, no es lo mismo para estimar la habilidad contestar ítems fáciles que difíciles, y puede ser que, por ejemplo, al contestar 4 ítems difíciles sea equivalente a contestar 12 fáciles. Para ello debo estimar la habilidad considerando la ubicación de los ítems. ¿Para qué sirve esto? Sirve para estimar la habilidad usando distintos ítems, incluso si estos no son versiones paralelas o utilizan distinto número de ítems o incluso un número variable de ítems. Veamos un ejemplo:

Supongamos que las personas contestan dos formas de una pruena, pero una es fácil y otra difícil:

``` r
set.seed(10)
n=30
a1 = matrix(rep(1, n),ncol=1)
d1 = matrix(rnorm(n, 0, 1),ncol=1)
d2 = matrix(rnorm(n, -2,1), ncol=1)
thet = matrix(rnorm(400, 0, 1), ncol=1)
```

``` r
prueba_facil=simdata(Theta = thet, a=a1, d=d1, itemtype = "2PL")
prueba_dificil=simdata(Theta = thet, a=a1, d=d2, itemtype = "2PL")
```

### Análisis inicial de los datos:

Lo que primero haríamos al enfrentar estos datos es visualizar y describir lo que estamos observando.

``` r
sjPlot::sjt.itemanalysis(prueba_facil)
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">
Component 1
</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left;text-align:left; ">
Row
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Missings
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Mean
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
SD
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Skew
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Item Difficulty
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; col7">
Item Discrimination
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; col8">
α if deleted
</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_1
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.05
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_2
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_3
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.98
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_4
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.52
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.33
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.62
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
-0.47
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.62
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.34
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_6
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.6
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
-0.43
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.60
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_7
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
1
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_8
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_9
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.2
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.4
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
1.53
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.20
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_10
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.33
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.43
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_11
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.73
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
-1.05
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.73
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.69
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.47
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
-0.8
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.69
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.47
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.47
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.39
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_14
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.72
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
-1
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.72
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.64
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
-0.57
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.64
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_16
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.50
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.59
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_18
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_19
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.67
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.47
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
-0.74
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.67
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.32
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_20
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.61
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
-0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.61
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.52
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
1.94
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.46
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.81
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.33
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
2.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.86
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_25
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.46
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.84
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.33
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.39
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.56
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.54
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_29
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.08
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.48
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.43
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.85
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; border-bottom: double; background-color:#f2f2f2; ">
Item\_30
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; col7">
0.39
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; col8">
0.85
</td>
</tr>
<tr>
<td colspan="9" style="font-style:italic; border-top:double black; text-align:right;">
Mean inter-item-correlation=0.445 · Cronbach's α=0.857
</td>
</tr>
</table>
``` r
sjPlot::sjt.itemanalysis(prueba_dificil)
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">
Component 1
</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left;text-align:left; ">
Row
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Missings
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Mean
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
SD
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Skew
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">
Item Difficulty
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; col7">
Item Discrimination
</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; col8">
α if deleted
</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_1
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.03
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.16
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
6.11
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.03
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.01
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_2
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.33
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
2.24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_3
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.3
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.46
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.9
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.30
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_4
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
1.94
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.06
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.25
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
3.54
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.06
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_6
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.04
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.18
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
5.08
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.04
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_7
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
1.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.32
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_8
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.05
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
4.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.05
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_9
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.34
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
2.21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.30
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_10
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.09
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
2.99
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.09
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_11
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.46
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.82
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.09
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.29
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
2.88
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.09
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.18
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.07
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
3.24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.07
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.31
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_14
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.96
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_15
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.08
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
3.17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.08
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_16
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
1.79
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.2
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.4
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
1.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.20
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_18
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.32
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
2.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.25
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_19
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.08
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
3.11
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.08
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_20
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
1.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_21
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.1
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.3
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
2.63
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.10
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.34
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
2.18
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_23
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.39
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.49
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.45
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.39
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.35
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.53
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.5
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
-0.13
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.53
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_25
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
1.34
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.36
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
1.11
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.30
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.07
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
3.24
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.07
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.29
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; background-color:#f2f2f2; ">
Item\_28
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.41
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
1.39
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; ">
0.22
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col7">
0.40
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; background-color:#f2f2f2; col8">
0.76
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; ">
Item\_29
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.09
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.29
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
2.88
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">
0.09
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col7">
0.26
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; col8">
0.77
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left;text-align:left; border-bottom: double; background-color:#f2f2f2; ">
Item\_30
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.00 %
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.38
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
1.76
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; ">
0.17
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; col7">
0.32
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; background-color:#f2f2f2; col8">
0.76
</td>
</tr>
<tr>
<td colspan="9" style="font-style:italic; border-top:double black; text-align:right;">
Mean inter-item-correlation=0.167 · Cronbach's α=0.771
</td>
</tr>
</table>
Para ello podemos hacer un gráfico de Guttman:

``` r
empirical_plot(prueba_facil, which.items=1:n, main = "Prueba fácil")
```

![](README_files/figure-markdown_github/unnamed-chunk-3-1.png)

``` r
empirical_plot(prueba_dificil, which.items=1:n, main = "Prueba difícil")
```

![](README_files/figure-markdown_github/unnamed-chunk-3-2.png)

## Modelos IRT:

``` r
mod_p_facil = mirt(model=1, itemtype = "Rasch", data=prueba_facil, SE=T)
```

``` r
mod_p_dificil = mirt(model=1, itemtype = "Rasch", data=prueba_dificil, SE=T)
```

Los sujetos tienen la misma habilidad (son los mismos sujetos) pero contestaron pruebas (set de ítems) distintos. O sea, es la misma propiedad medida pero con dos instrumentos distintos. Si las medidas son consistentes deberían generar una línea recta:

``` r
data.frame(cbind(facil = fscores(mod_p_facil)[,1], dificil = fscores(mod_p_dificil)[,1])) %>% 
  ggplot(aes(x=facil, y=dificil)) + geom_point() + geom_smooth()
```

![](README_files/figure-markdown_github/unnamed-chunk-6-1.png)

Veamos qué pasa si sumamos los puntajes:

``` r
data.frame(facil = rowSums(prueba_facil) , dificil= rowSums(prueba_dificil) ) %>% 
  ggplot(aes(x=facil, y=dificil)) + geom_point() + geom_smooth()
```

![](README_files/figure-markdown_github/unnamed-chunk-7-1.png)

Lo que ocurre es que los puntajes obtenidos con un instrumento no mantienen la forma lineal respecto a los puntajes obtenidos con otro instrumento. Por ejemplo, la diferencia entre obtener 0 a 10 puntos, en la prueba difícil, equivale a obtener una diferencia de 0 a 5 puntos, aproximadamente en la prueba difícil. En cambio, una diferencia de 20 a 30 puntos equivale a una diferencia de más o menos 8 puntos en la prueba difícil.

## Segundo ejemplo, con más ítems:

Para mostrar la propiedad de invarianza (la no dependencia) de la propiedad medida respecto al objeto medido, vamos a poner una situación más favorable (más estable), en la que hay más información. En este caso, más ítems es más información (mayor certeza de la ubicación de las personas o bien de su puntaje total) para cada uno de los tests

``` r
set.seed(10)
n=150
a1 = matrix(rep(1, n),ncol=1)
d1 = matrix(rnorm(n, 0, 1),ncol=1)
d2 = matrix(rnorm(n, -2,1), ncol=1)
thet = matrix(rnorm(400, 0, 1), ncol=1)
```

``` r
prueba_facil=simdata(Theta = thet, a=a1, d=d1, itemtype = "2PL")
prueba_dificil=simdata(Theta = thet, a=a1, d=d2, itemtype = "2PL")
```

## Modelos IRT:

``` r
mod_p_facil = mirt(model=1, itemtype = "Rasch", data=prueba_facil, SE=T)
```

``` r
mod_p_dificil = mirt(model=1, itemtype = "Rasch", data=prueba_dificil, SE=T)
```

Si tenemos 150 ítems en cada una de las pruebas, es claro lo que ocurre. El modelo de Rasch permite obtener medidas consistentes, en donde lo que cambia es la escala de medida pero no la ubicación de los individuos relativa a esa escala. Así, tal como cuando medimos en grados celsius o grados fahrenheit estamos midiendo la misma propiedad en escalas equivalentes, en el caso de un modelo de Rasch, bien ajustado, nos permite observar la misma relación.

``` r
data.frame(cbind(facil = fscores(mod_p_facil)[,1], dificil = fscores(mod_p_dificil)[,1])) %>% 
  ggscatter(x="facil", y = "dificil")+
  stat_cor(method = "pearson", label.x = 0, label.y = 3) + geom_smooth()
```

![](README_files/figure-markdown_github/unnamed-chunk-12-1.png)

En el caso de los puntajes observados, lo que ocurre queda demostrado con mayor evidencia. La distancia entre los puntajes en una escala no son equivalentes a los de otra escala. Esta falta de equivalencia impide, por ejemplo, hacer comparaciones utilizando distintos ítems para evaluar distintas personas.

``` r
data.frame(facil = rowSums(prueba_facil) , dificil= rowSums(prueba_dificil) ) %>% 
  ggscatter(x="facil", y = "dificil") +
  stat_cor(method = "pearson", label.x = 20, label.y = 60) + geom_smooth()
```

![](README_files/figure-markdown_github/unnamed-chunk-13-1.png)

Lo que estamos mostrando en el caso del modelo de Rasch, es que podemos calibrar distintos ítems (construir escalas) con pruebas distintas y obtener escalas equivalentes. En este caso, las habilidades de los sujetos son las mismas y ello genera que las escalas de medida estén corridas respecto a la misma muestra (una tiene parámetros de dificultad más altos), y ello genera que en la estimación de la habilidad, la ubicación de las personas considere esta diferencia de dificultad, de modo que el modelo permite ubicar a la persona en el mismo lugar (o en un lugar cercano a) el lugar determinado por la otra escala (de la prueba fácil, que corresponde a otra calibración).

``` r
data.frame(cbind(facil = fscores(mod_p_facil)[,1], dificil =fscores(mod_p_dificil)[,1])) %>% gather(key=prueba, value=medición) %>% ggdensity(x="medición",fill = "prueba", add = "mean") + labs(title="Distribución de habilidades usando modelo de Rasch")
```

![](README_files/figure-markdown_github/unnamed-chunk-14-1.png)

Veamos qué pasa con la suma de puntajes como método de puntuación:

``` r
data.frame(facil = rowSums(prueba_facil) , dificil= rowSums(prueba_dificil) ) %>% gather(key=prueba, value=medición) %>% ggdensity(x="medición",fill = "prueba", add = "mean") + labs(title="Distribución de habilidades usando Puntajes")
```

![](README_files/figure-markdown_github/unnamed-chunk-15-1.png)

Lamentablemente en este último caso vemos que los puntajes se distribuyen de modos diferentes dependiendo de la prueba de que se rinde, a pesar de que las personas tienen la misma habilidad. Así, la puntuación es dependiente de la dificultad, y no la considera para la estimación de las habilidades. En el modelo de Rasch (e IRT) la estimación de la habilidad es un proceso en el cual se considera la dificultad (la ubicación del ítem en la escala) de modo que la ubicación del atributo medido se determina considerando la ubicación de los ítems.

Ahora veamos un caso más realista, en el cual tenemos un banco de ítems calibrados y administramos formas distintas a un mismo grupo de personas. ¿podemos obtener estimaciones de habilidad que iguales usando ítems distintos?

## Estimación de habilidad usando ítems precalibrados:

Supongamos que tenemos 80 ítems calibrados con un modelo de Rasch

``` r
pacman::p_load(mirt, mirtCAT, tidyverse)

theta = matrix(rnorm(300, 0,1),ncol=1)
d = matrix(rnorm(80, 0, 1.7), ncol=1)
a = matrix(rep(1,80),ncol=1)
```

``` r
pool_items = simdata(Theta = theta, d=d, a=a, itemtype = "2PL")
params_md = mirt(data = pool_items, itemtype = "Rasch", SE=T, model = 1)
```

    ## 
    Iteration: 1, Log-Lik: -11649.482, Max-Change: 0.15764
    Iteration: 2, Log-Lik: -11645.995, Max-Change: 0.03211
    Iteration: 3, Log-Lik: -11645.768, Max-Change: 0.00960
    Iteration: 4, Log-Lik: -11645.751, Max-Change: 0.00349
    Iteration: 5, Log-Lik: -11645.745, Max-Change: 0.00132
    Iteration: 6, Log-Lik: -11645.745, Max-Change: 0.00040
    Iteration: 7, Log-Lik: -11645.745, Max-Change: 0.00015
    Iteration: 8, Log-Lik: -11645.745, Max-Change: 0.00009
    ## 
    ## Calculating information matrix...

Podemos observar algunas características de nuestros ítems, por ejemplo las curvas y su ubicación

``` r
plot(params_md, type="trace", facet_items = F)
```

![](README_files/figure-markdown_github/unnamed-chunk-18-1.png)

Una forma interesante de ver nuestros ítems es usando un mapa de Wright, que muestra la ubicación de los ítems y la ubicación de las habilidades (estas últimas pueden ser simuladas)

``` r
library(WrightMap)
scores_hab = fscores(params_md)
wrightMap(thetas = scores_hab, thresholds = coef(params_md, simplify=T, IRTpars = T)$items[,2], show.thr.lab = FALSE, label.items.srt = 45)
```

![](README_files/figure-markdown_github/unnamed-chunk-19-1.png)

Segunda versión, esta vez ordenado.

``` r
orden = thresholds = coef(params_md, simplify=T, IRTpars = T)$items[,2]
wrightMap(thetas = scores_hab, thresholds = orden[order(orden)], show.thr.lab = FALSE, label.items.srt = 45, main.title = "Mapa de Wright ordenado")
```

![](README_files/figure-markdown_github/unnamed-chunk-20-1.png)

Esto nos da una idea de que contamos con ítems con diversas ubicaciones, que en teoría nos podrían permitir armar formas diversas que permitan estimar habilidades con igual presición usando distintos ítems.

Nuestra herramienta son las ubicaciones de los ítems, ocupémoslas!:

``` r
parametros_pool = coef(params_md, IRTpars = F, simplify=T)$items ## ocupamos la nomenclatura clásica de intercepto + pendiente.
parametros_pool = data.frame(parametros_pool)
colnames(parametros_pool) = c("a1", "d", "g", "u") ## hay que cambiar el nombre del parámetro, b por d. En la nomenclatura clásica se llama d, no b.
```

Vamos armar 4 formas distintas de pruebas:

``` r
items_imp = parametros_pool[seq(1,80,2),] ## impares
items_par = parametros_pool[seq(2,80,2),] ## pares

## solo fáciles:
items_faciles = parametros_pool %>% mutate(n_row = row_number()) %>% arrange(d) %>%
  slice(sample(50:80,20,replace = F)) %>% pull(n_row) ## selección de ítems fáciles

## mayormente difíciles:
items_dificiles = parametros_pool %>% mutate(n_row = row_number()) %>% arrange(d) %>%
  slice(c(sample(1:30,20,replace = F), sample(31:80,10,replace = F))) %>% pull(n_row) ## selección de ítems difíciles y algunos fáciles

items_dificiles=sort(items_dificiles)
items_faciles = sort(items_faciles)

parametros_dificiles = parametros_pool[items_dificiles,] 
parametros_faciles = parametros_pool[items_faciles,]
```

Comparemos la selección de ítems utilizando mapas de Wright:

``` r
wrightMap(thetas = scores_hab, thresholds = sort(items_imp$d*-1),show.thr.lab = FALSE, label.items.srt = 45, main.title = "Mapa de Wright items impares")
```

![](README_files/figure-markdown_github/unnamed-chunk-23-1.png)

``` r
wrightMap(thetas = scores_hab, thresholds = sort(items_par$d*-1),show.thr.lab = FALSE, label.items.srt = 45, main.title = "Mapa de Wright items pares")
```

![](README_files/figure-markdown_github/unnamed-chunk-24-1.png)

``` r
wrightMap(thetas = scores_hab, thresholds = sort(parametros_faciles$d*-1),show.thr.lab = FALSE, label.items.srt = 45, main.title = "Mapa de Wright items fáciles")
```

![](README_files/figure-markdown_github/unnamed-chunk-25-1.png)

``` r
wrightMap(thetas = scores_hab, thresholds = sort(parametros_dificiles$d*-1),show.thr.lab = FALSE, label.items.srt = 45, main.title = "Mapa de Wright items difíciles")
```

![](README_files/figure-markdown_github/unnamed-chunk-26-1.png)

Tenemos 4 formas de pruebas muy distintas, y lo que pretendemos es estimar la habilidad de una misma muestra de personas usando estas 4 formas. ¿Obtendrémos resultados comparables a aquellos obtenidos ocupando el total de las preguntas?

A primera vista podemos hipotetizar que la selección de ítems impares hará un buen trabajo estimando la habilidad para personas en el rango medio, donde está la mayor proporción de personas. La de ítems impares tendrá mayor precisión para personas en el rango alto de habilidad, la de ítems fáciles hará un muy mal trabajo estimando la habilidad de personas con alto nivel de habilidad, y la selección de ítems difíciles a la inversa. Veamos qué ocurre:

``` r
model_imp = generate.mirt_object(parameters = items_imp, itemtype = "Rasch")
```

``` r
model_par = generate.mirt_object(parameters = items_par, itemtype = "Rasch")
```

``` r
model_dificiles = generate.mirt_object(parameters = parametros_dificiles, itemtype = "Rasch")
```

``` r
model_faciles = generate.mirt_object(parameters = parametros_faciles, itemtype = "Rasch")
```

``` r
items_impares = pool_items[,seq(1,80,2)]
items_pares = pool_items[,seq(2,80,2)]
items_Dificiles = pool_items[,items_dificiles]
items_Faciles = pool_items[,items_faciles]
```

Primero veamos la estimación de habilidad obtenida usando todos los ítems:

``` r
fscore_imp = fscores(object  =model_imp, response.pattern=items_impares, full.scores = F, method = "EAP")[,c("F1")]
fscore_par = fscores(object  =model_par, response.pattern=items_pares, full.scores = F, method = "EAP")[,c("F1")]
fscore_dificiles = fscores(object=model_dificiles, response.pattern = items_Dificiles, full.scores = F, method = "EAP")[,c("F1")]
fscores_faciles = fscores(object = model_faciles, response.pattern = items_Faciles, full.scores = F, method = "EAP")[,c("F1")]
```

``` r
fscores = data.frame(cbind(scores_hab, fscore_imp, fscore_par, fscore_dificiles, fscores_faciles)) ## los 4
```

``` r
library(corrmorant)
corrmorant::corrmorant(fscores)
```

![](README_files/figure-markdown_github/unnamed-chunk-31-1.png)

Lo primero que notamos es que la selección de ítems para los ítems fáciles fue muy mal realizada, unos pocos ítems de mayor dificultad seguramente hubiesen evitado el efecto techo que estamos encontrando. La selección de ítems de mayor dificultad logró un buen resultado, puesto que agregando 10 ítems de mayor facilidad evitamos un efecto piso. El mapa de Wright fue útil para evitar este problema. Podemos ver también para qué personas obtuvimos mayor presición.

``` r
fscores %>% mutate(dif_imp = F1-fscore_imp,
                   dif_par = F1-fscore_par,
                   dif_dif = F1-fscore_dificiles,
                   dif_fac = F1-fscores_faciles) %>% select(F1,dif_imp:dif_fac) %>% 
  gather(key=diferencia, value=valor, 2:5) %>% 
  ggplot(aes(x=F1, y=valor, color=diferencia)) + geom_point() + facet_wrap(~diferencia) +
  geom_hline(yintercept = 0.5) + geom_hline(yintercept = -0.5) + theme_bw()
```

![](README_files/figure-markdown_github/unnamed-chunk-32-1.png)

``` r
fscores %>%  
  gather(key=forma, value=valor, 1:5) %>% ggplot(aes(x=valor,color=forma, fill=forma)) + geom_density(alpha=.3)
```

![](README_files/figure-markdown_github/unnamed-chunk-33-1.png)

En todos los casos tenemos algún grado de precisión adecuado. Para la selección de ítems pares e impares, nuestra estimación de la habilidad usando ítems distintos es adecuada, con pocos casos en que el error de estimación de es más de 0.5 logits. En el caso de la selección de ítems mayormente difíciles y unos pocos fáciles, se observa alta precisión para personas con alta habilidad, pero mucha imprecisión para personas con baja habilidad. En el caso de la selección de ítems fáciles, tenemos un serio problema de efecto techo, acrecentándose el error cuando el nivel de habilidad es alto (y no puede distinguirse la persona de otra con un nivel, por ejemplo, medio alto). En este último caso, nos faltaron ítems de mayor dificultad.

¿Qué pasaría si no usamos un modelo que permite separar la habilidad (el atributo medido) del instrumento utilizado para medir? Es lo que pasa con el uso de puntajes totales. Veamos:

``` r
ctt_scores = data.frame(cbind(rowSums(pool_items)/80, rowSums(pool_items[,seq(1,80,2)])/40, rowSums(pool_items[,seq(2,80,2)])/40, rowSums(pool_items[,items_dificiles])/30, rowSums(pool_items[,items_faciles]/20)))
```

``` r
colnames(ctt_scores) = c("total", "impares", "pares", "difíciles", "fáciles")
corrmorant(ctt_scores)
```

![](README_files/figure-markdown_github/unnamed-chunk-35-1.png)

Veamos la diferencia entre la proporción obtenida de correctas de las distintas formas respecto a la proporción de respuestas correctas obtenidas en el total de los ítems.

``` r
ctt_scores %>% mutate(dif_imp = total-impares,
                      dif_par = total-pares,
                      dif_dific = total-difíciles,
                      dif_fac = total-fáciles) %>% select(total, dif_imp:dif_fac) %>% 
  gather(key=diferencia, value=valor, 2:5) %>% ggplot(aes(x=total, y = valor, color=diferencia)) + geom_point() + facet_wrap(~diferencia)
```

![](README_files/figure-markdown_github/unnamed-chunk-36-1.png)

``` r
ctt_scores %>%  
  gather(key=forma, value=valor, 1:5) %>% ggplot(aes(x=valor,color=forma, fill=forma)) + geom_density(alpha=.3)
```

![](README_files/figure-markdown_github/unnamed-chunk-37-1.png)

A nivel de correlación, la asociación es la misma. La única gran diferencia es en el significado del puntaje. En el caso del modelo de Rasch (e IRT) es la misma escala, de modo que estamos comparando a las personas con una misma vara. En el caso del CTT no es la misma escala (podríamos decir que de hecho no hay una escala), de modo que no podemos comparar el puntaje de un/una estudiante que contestó ítems difíciles con el que contextó ítems fáciles. En CTT tenemos únicamente un puntaje total que corresponde a cantidad de correctas o una suma, lo cual nos sitúa en una posición observacional respecto al objeto que queremos medir. Podemos constatar que alguien contesta más preguntas que otra persona; que alguien saca más puntos y que alguien saca menos. Sabemos que quello es dependiente de la prueba, de modo que el sacar más o menos depende y es producto de la dificultad de la prueba. En el caso del ejemplo anterior, podemos ver que, de hecho, cuando los ítems son difíciles, la proporción de respuestas correctas baja y por tanto existe una subestimación sistemática de la proporción de correctas respecto a lo que obtendría la persona si contestara el total de los ítems. Lo mismo pero en sentido inverso ocurre cuando se contestan ítems fáciles. El problema de ello radica en que el nivel de dificultad de la prueba genera puntajes sistemáticamete distintos entre formas que no son estrictamente equivalentes. Cuando observamos la forma conformada por ítems pares e impares, obtenemos un muestreo aleatorio de ítems que resultan tener dificultad similar al total de ítems. El problema ocurre cuando no tenemos formas similares, y en muchos casos no podemos aplicar formas similares o no queremos tenerlas, o bien no queremos que un asunto problemático.

La independencia entre la habilidad estimada y el instrumento utilizado para medirla, permite medir utilizando técnicas computacionales, como las pruebas adaptativas.

# Invarianza de los parámetros de los ítems:

En el caso de la CTT nos interesa tener una muestra representativa para calcular los parámetros de los ítems. En el caso del modelo de Rasch (e IRT) eso no es así, y deberíamos poder calcular los parámetros de los ítems con distintas muestras, con distintas características. Los parámetros de los ítems debieran ser linealmente dependientes o consistentes, de lo contrarío encontraríamos sesgo (mide de forma distinta a distintos grupos). Como corresponden a distintas calibraciones, lo que veremos es si los parámetros son consistentes o no

La consistencia se produce cuando dos escalas son equivalentes bajo una transformación lineal, tal como es el cambio de libras a kilógramos, o de millas a metros. La posibilidad de tener invarianza en la estimación de parámetros bajo una transformación lineal es una propiedad vital, porque permite generar bancos de ítems con distintas muestras, a través de un proceso de linking.

Hay que considerar que el linking descansa en esta característica: la posibilidad de tener parámetros consistentes (linealmente dependientes) puesto que nos interesa preservar la distancia relativa de los ítems en cada calibración.

Asumamos que tenemos personas con distinto nivel de habilidad y que van a rendir los mismos ítems:

``` r
set.seed(101)
n=30
a1 = matrix(rep(1, n),ncol=1)
d1 = matrix(rnorm(n, 0, 1),ncol=1)
thet = matrix(rnorm(400, 0, 1), ncol=1)
thet2 = matrix(rnorm(400, 1, 1.6), ncol=1)
```

``` r
dat_bh = mirt::simdata(a=a1, d=d1, Theta = thet, itemtype = "2PL")
dat_ah = mirt::simdata(a=a1, d=d1, Theta = thet2, itemtype = "2PL")
```

``` r
model_bh = mirt(dat_bh, itemtype = "Rasch", model=1)
model_ah = mirt(dat_ah, itemtype = "Rasch", model=1)
```

``` r
it_pars_bh = coef(model_bh, simplify = T, IRTpars = T)$items[,2]
it_pars_ah = coef(model_ah, simplify = T, IRTpars = T)$items[,2]

data.frame(cbind(baja=it_pars_bh, alta=it_pars_ah)) %>% ggplot(aes(x=baja, y=alta)) + geom_point() +
  stat_cor(method = "pearson", label.x = 1, label.y = 2) + geom_smooth()
```

![](README_files/figure-markdown_github/unnamed-chunk-41-1.png)

Observamos la línea recta que buscábamos. Veamolos en una tabla:

``` r
library(knitr)
kable(data.frame(cbind(baja=it_pars_bh, alta=it_pars_ah)))
```

|          |        baja|        alta|
|:---------|-----------:|-----------:|
| Item\_1  |   0.2043146|  -0.5836590|
| Item\_2  |  -0.4082582|  -1.4744453|
| Item\_3  |   0.6598852|   0.0062826|
| Item\_4  |  -0.1183763|  -1.2377652|
| Item\_5  |  -0.1902523|  -1.3540739|
| Item\_6  |  -1.1034731|  -2.1903725|
| Item\_7  |  -0.6198793|  -1.4744453|
| Item\_8  |  -0.0705751|  -0.7436632|
| Item\_9  |  -1.0463417|  -1.8078225|
| Item\_10 |   0.2524278|  -0.6414262|
| Item\_11 |  -0.4821430|  -1.3372241|
| Item\_12 |   0.8422311|  -0.1187705|
| Item\_13 |  -1.5587082|  -2.3586264|
| Item\_14 |   1.4578619|   0.6275552|
| Item\_15 |   0.3007229|  -0.4693190|
| Item\_16 |   0.2765503|  -0.7289607|
| Item\_17 |   0.9093991|   0.0618677|
| Item\_18 |  -0.0586344|  -0.9078735|
| Item\_19 |   0.8024893|   0.1035926|
| Item\_20 |   2.3358521|   1.1624685|
| Item\_21 |   0.1443742|  -0.8776509|
| Item\_22 |  -0.6836735|  -1.1890166|
| Item\_23 |   0.2644831|  -0.7142920|
| Item\_24 |   1.4414287|   0.6567389|
| Item\_25 |  -0.5945852|  -1.4396014|
| Item\_26 |   1.5938314|   0.3838193|
| Item\_27 |  -0.4945345|  -1.5632858|
| Item\_28 |   0.1923105|  -0.6124879|
| Item\_29 |  -0.5318551|  -1.3710065|
| Item\_30 |  -0.5318551|  -1.4920111|

Hay una diferencia, pues efectivamente al grupo de alta habilidad le pareció que los ítems eran más fáciles. Hay que recordar no obstante que la escala es arbitraria en términos de su ubicación, y que podemos reubicarla donde queramos. Podríamos reubicar la escala del segundo grupo en términos de la escala del primer grupo, restando al segundo grupo la distancia promedio entre ambas escalas. El promedio es:

``` r
colMeans(data.frame(cbind(baja=it_pars_bh, alta=it_pars_ah)))
```

    ##       baja       alta 
    ##  0.1061672 -0.7895158

y la distancia promedio es:

``` r
difs = colMeans(data.frame(cbind(baja=it_pars_bh, alta=it_pars_ah)))
diferencia = difs[1] - difs[2]
```

Si restamos 0.8956831 a los parámetros obtenidos por el grupo de alta habilidad obtenemos parámetros similares (no iguales) a los parámetros de la escala del grupo de baja habilidad.

``` r
kable(data.frame(cbind(baja=it_pars_bh, alta=it_pars_ah, alta_rescaled = it_pars_ah+diferencia)))
```

|          |        baja|        alta|  alta\_rescaled|
|:---------|-----------:|-----------:|---------------:|
| Item\_1  |   0.2043146|  -0.5836590|       0.3120241|
| Item\_2  |  -0.4082582|  -1.4744453|      -0.5787622|
| Item\_3  |   0.6598852|   0.0062826|       0.9019656|
| Item\_4  |  -0.1183763|  -1.2377652|      -0.3420821|
| Item\_5  |  -0.1902523|  -1.3540739|      -0.4583909|
| Item\_6  |  -1.1034731|  -2.1903725|      -1.2946894|
| Item\_7  |  -0.6198793|  -1.4744453|      -0.5787622|
| Item\_8  |  -0.0705751|  -0.7436632|       0.1520199|
| Item\_9  |  -1.0463417|  -1.8078225|      -0.9121394|
| Item\_10 |   0.2524278|  -0.6414262|       0.2542568|
| Item\_11 |  -0.4821430|  -1.3372241|      -0.4415410|
| Item\_12 |   0.8422311|  -0.1187705|       0.7769126|
| Item\_13 |  -1.5587082|  -2.3586264|      -1.4629434|
| Item\_14 |   1.4578619|   0.6275552|       1.5232382|
| Item\_15 |   0.3007229|  -0.4693190|       0.4263641|
| Item\_16 |   0.2765503|  -0.7289607|       0.1667224|
| Item\_17 |   0.9093991|   0.0618677|       0.9575507|
| Item\_18 |  -0.0586344|  -0.9078735|      -0.0121905|
| Item\_19 |   0.8024893|   0.1035926|       0.9992757|
| Item\_20 |   2.3358521|   1.1624685|       2.0581515|
| Item\_21 |   0.1443742|  -0.8776509|       0.0180321|
| Item\_22 |  -0.6836735|  -1.1890166|      -0.2933335|
| Item\_23 |   0.2644831|  -0.7142920|       0.1813911|
| Item\_24 |   1.4414287|   0.6567389|       1.5524220|
| Item\_25 |  -0.5945852|  -1.4396014|      -0.5439183|
| Item\_26 |   1.5938314|   0.3838193|       1.2795024|
| Item\_27 |  -0.4945345|  -1.5632858|      -0.6676028|
| Item\_28 |   0.1923105|  -0.6124879|       0.2831952|
| Item\_29 |  -0.5318551|  -1.3710065|      -0.4753234|
| Item\_30 |  -0.5318551|  -1.4920111|      -0.5963281|
