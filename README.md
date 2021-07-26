Análisis de propiedad de invarianza en modelos de Rasch
================

# Propiedad de invarianza:

¿Qué es medir en psicología? Para intentar contestar esta pregunta deberíamos ver qué propiedades tiene la medición:

**Sistema intervalar:** sistema de asignación de números que contiene una unidad de medida y el 0 es arbitrario. Podemos pensar este sistema como una escala o línea, en la que podemos ubicar una propiedad de un objeto. En este caso ya hablamos de medición pues se preserva una característica fundamental, que es la constancia de las diferencias de unidades en la escala. La diferencia entre 1 y 3 es igual a la diferencia de 3 y 5. Esto ocurre con la medida de temperatura, en que la diferencia entre 5 y 10 grados es igual a la de 10 y 15, para la variable de interés. Sin embargo, en este tipo de mecanismo de asignación de números, no es aplicable la razones, de modo que no es posible decir que 20 grados es el doble que 10 grados. Esto es porque el 0 es arbitrario, y no indica ausencia del atributo. Como veremos, esta característica es exclusiva del modelo de Rasch, y lo distingue de otros modelos IRT (2PL y 3 PL).

**Independencia:** la otra característica de la medición, relacionada a lo anterior, es que la propiedad medida es independiente al objeto usado para su medición. La distancia entre las unidades de medida (de la escala) respecto a un objeto (en este caso el atributo de la persona) no depende del objeto de comparación (de la persona). Del mismo modo, la distancia entre dos variables (propiedades) medidas entre objetos no dependen de la unidad de medida del instrumento de medición.

**Linealidad:** debe poder expresarse en una línea que indica la ubicación del objeto medido.

**Significado:** debe entregar un significado. ¿en qué sentido una persona tiene más de un atributo que otra persona? En el modelo de Rasch (e IRT) este significado es la probabilidad de obtener una respuesta dada (condicional a) la ubicación del atributo.

**Generalizable:** debe poder ser usado para decir algo respecto a cómo se comportará esa propiedad respecto a otros instrumentos de medida. Es decir, debe ser generalizable.

Veamos cómo el modelo de Rasch permite medir y en qué sentido la TCT no permite hacer medición propiamente tal, y que el modelo de Rasch lo logra.

## Invarianza de los parámetros de las personas:

Dado un nivel de habilidad, el modelo de Rasch (y el IRT) permite estimar ese nivel de habilidad usando distintos ítems, debido a que considera la dificultad (y la discriminación) o ubicación de los ítems al hacer la medición. Así, no es lo mismo para estimar la habilidad contestar ítems fáciles que difíciles, y puede ser que, por ejemplo, al contestar 4 ítems difíciles sea equivalente a contestar 12 fáciles. Para ello debo estimar la habilidad considerando la ubicación de los ítems. ¿Para qué sirve esto? Sirve para estimar la habilidad usando distintos ítems, incluso si estos no son versiones paralelas o utilizan distinto número de ítems o incluso un número variable de ítems. Veamos un ejemplo:

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

En el caso de la CTT nos interesa tener una muestra representativa para calcular los parámetros de los ítems. En el caso del modelo de Rasch (e IRT) eso no es así, y deberíamos poder calcular los parámetros de los ítems con distintas muestras, que a su vez no son comparables en términos de su habilidad. Los parámetros de los ítems debieran ser linealmente dependientes o consistentes, de lo contrarío encontraríamos sesgo (mide de forma distinta a distintos grupos). Como corresponden a distintas calibraciones, lo que veremos es si los parámetros son consistentes o no.

La **consistencia** se produce cuando dos escalas son equivalentes bajo una transformación lineal, tal como es el cambio de libras a kilógramos, o de millas a metros. La posibilidad de tener invarianza en la estimación de parámetros bajo una transformación lineal es una propiedad vital, porque permite generar bancos de ítems con distintas muestras, a través de un proceso de linking. En el modelo de Rasch, como mantenemos el **logit** como unidad de medida (las distancias entre ítems y personas, o entre personas, debende únicamente de la ubicación en la escala), el tipo de linking que se utiliza es el mean-mean (resta de promedios). Existen otras formas de linking, pero modifican la unidad de medida, y por tanto, no salimos de la filosofía del modelo de Rasch.

Hay que considerar que el linking descansa en esta característica: la posibilidad de tener parámetros consistentes (linealmente dependientes) puesto que nos interesa preservar la distancia de los ítems en cada calibración.

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

Podemos observar que hay algún tipo de dependencia entre la estimación de parámetros en el modelo de Rasch y la habilidad de la muestra. No pretendemos lograr un ajuste absoluto, pero sí a un nivel que nos de un grado de seguridad adecuado, pensando en que siempre, cuando estimamos parámetros con distintas muestras, obtenemos algún grado de diferencia.

### ¿Qué aplicación práctica tiene esta propiedad?

Son dos:

1.- Ampliar bancos de ítems a través de la estimación de parámetros de nuevos ítems, una vez que se tiene calibrado un número específico de ítems. Así podemos ir ampliando nuestro banco de ítems y modificando nuestros instrumentos.

2.- Comparar muestras distintas, que contestan a su vez, ítems distintos (aunque no todos sean distintos). Esto se llama escalamiento vertical. **Vertical scaling** busca hacer comparables a través de diferente grados educacionales por ejemplo, o hacer comparable los puntajes de un mismo grupo que cambia en su nivel de habilidad debido a una intervención. Es decir, un grupo es sistemáticamente distinto a otro grupo, aunque este grupo sean los mismos sujetos que se han movido en su nivel de habilidad.

# Vertical scaling:

Veamos un ejemplo:

``` r
set.seed(12345)
a = matrix(rep(1, 50),ncol=1)
set_items1 = matrix(rnorm(50,0,1),ncol=1)

## Vamos a intentar hacer una buena selección de ítems, para ancla, teniendo de diversa ubicación:

anchor = data.frame(set_items1) %>% mutate(numero = row_number()) %>% arrange((set_items1)) %>% 
  slice(round(seq(1,50,length.out = 16))) %>% arrange(numero)

names(anchor)[1] = "item"

n_anchor = anchor %>% pull(numero)

set_items2 = matrix(rnorm(50, -1, 1.5), ncol=1) ## ítems distintos

set_items2 = data.frame(set_items2) %>% mutate(numero = row_number()) %>% slice(-n_anchor)
names(set_items2)[1] = "item"

set_items2 = bind_rows(set_items2, anchor, .id = "group") %>% mutate(group = ifelse(group==1, "test2", "ancla")) %>% arrange(numero) ## Acá incerté los parámetros de los ítems ancla
```

Veamos los parámetros de los ítems, y si estos son o no son ancla:

``` r
library(knitr)
kable(set_items2)
```

| group |        item|  numero|
|:------|-----------:|-------:|
| ancla |   0.5855288|       1|
| test2 |   1.9215390|       2|
| ancla |  -0.1093033|       3|
| ancla |  -0.4534972|       4|
| test2 |  -2.0064648|       5|
| test2 |  -0.5830695|       6|
| ancla |   0.6300986|       7|
| test2 |   0.2356930|       8|
| ancla |  -0.2841597|       9|
| test2 |  -4.5204160|      10|
| test2 |  -0.7756120|      11|
| test2 |  -3.0137972|      12|
| test2 |  -0.1700454|      13|
| ancla |   0.5202165|      14|
| ancla |  -0.7505320|      15|
| test2 |  -3.7485660|      16|
| test2 |   0.3322091|      17|
| test2 |   1.3902327|      18|
| test2 |  -0.2247180|      19|
| ancla |   0.2987237|      20|
| test2 |  -0.9180766|      21|
| ancla |   1.4557851|      22|
| test2 |  -2.5740292|      23|
| test2 |   2.4957679|      24|
| ancla |  -1.5977095|      25|
| ancla |   1.8050975|      26|
| test2 |   0.2393874|      27|
| test2 |  -2.2173107|      28|
| test2 |  -0.2856276|      29|
| test2 |   0.5318876|      30|
| ancla |   0.8118732|      31|
| ancla |   2.1968335|      32|
| test2 |  -1.4565537|      33|
| test2 |   2.7156664|      34|
| test2 |   0.4568310|      35|
| test2 |   1.8006488|      36|
| test2 |   0.0080637|      37|
| test2 |  -1.4619301|      38|
| test2 |  -0.1952144|      39|
| test2 |   0.2373051|      40|
| test2 |  -2.4458522|      41|
| ancla |  -2.3803581|      42|
| ancla |  -1.0602656|      43|
| ancla |   0.9371405|      44|
| test2 |  -2.4709494|      45|
| test2 |   0.0309982|      46|
| test2 |  -1.7575653|      47|
| test2 |   2.2365797|      48|
| test2 |  -1.8996963|      49|
| test2 |  -2.0418200|      50|

Ahora, hagamos la simulación de los datos:

``` r
library(mirt)
theta = matrix(rnorm(400, 0, 1),ncol=1)
theta2 = matrix(rnorm(400, 1, 1.5), ncol=1)

prueba1 = simdata(Theta = theta, a=a, d=set_items1, itemtype = "2PL")
prueba2 = simdata(Theta = theta2, a=a, d=matrix(set_items2$item, ncol=1), itemtype = "2PL")  ## test2

prueba1=data.frame(prueba1)
prueba2=data.frame(prueba2)
```

Cambiemos los nombres a los ítems para poder estimar los parámetros de los ítems:

``` r
names(prueba1)[n_anchor] = paste0(colnames(prueba1[,n_anchor]), "anc", n_anchor)
names(prueba2)[n_anchor] = paste0(colnames(prueba2[,n_anchor]), "anc", n_anchor)

names(prueba1)[-n_anchor] = paste0("t1",colnames(prueba1[,-n_anchor]))
names(prueba2)[-n_anchor] = paste0("t2",colnames(prueba1[,-n_anchor]))
```

Estimación de los parámetros:

``` r
params_test1 = mirt(prueba1, itemtype = "Rasch", model = 1, SE=T)
params_test2 = mirt(prueba2, itemtype = "Rasch", model = 1, SE=T)
```

Tenemos los parámetros estimados con ambas muestras, las cuales son sistemáticamente distintas. Comparten, no obstante, ítems en común en sus pruebas, y ello nos va a permitir generar una escala común.

``` r
beta1 = coef(params_test1, IRTpars = T, simplify = T)$items[,2]
beta2 = coef(params_test2, IRTpars = T, simplify = T)$items[,2]
knitr::kable(data.frame(cbind(beta1, beta2)))
```

|               |       beta1|       beta2|
|:--------------|-----------:|-----------:|
| Item\_1anc1   |  -0.5139122|  -1.4634575|
| t1Item\_2     |  -0.8481755|  -3.0897386|
| Item\_3anc3   |   0.0435231|  -0.9366597|
| Item\_4anc4   |   0.6705987|  -0.5076498|
| t1Item\_5     |  -0.6143995|   0.9914437|
| t1Item\_6     |   1.8044921|  -0.6121024|
| Item\_7anc7   |  -0.6270878|  -2.0703412|
| t1Item\_8     |   0.4436718|  -1.2853622|
| Item\_9anc9   |   0.1756101|  -0.6121024|
| t1Item\_10    |   0.8145917|   3.5351300|
| t1Item\_11    |   0.2359485|  -0.2592703|
| t1Item\_12    |  -1.7661659|   1.7980647|
| t1Item\_13    |  -0.4395856|  -0.7488842|
| Item\_14anc14 |  -0.6398068|  -1.5562172|
| Item\_15anc15 |   0.8012953|  -0.3026638|
| t1Item\_16    |  -1.0259934|   2.6295556|
| t1Item\_17    |   0.9640556|  -1.5002387|
| t1Item\_18    |   0.4066460|  -2.0703412|
| t1Item\_19    |  -1.0969848|  -0.9686622|
| Item\_20anc20 |  -0.4027044|  -1.3027682|
| t1Item\_21    |  -0.8884348|  -0.3026638|
| Item\_22anc22 |  -1.5667485|  -2.6323535|
| t1Item\_23    |   0.5559982|   1.5551916|
| t1Item\_24    |   1.6535498|  -3.5054710|
| Item\_25anc25 |   1.5299457|   0.5135411|
| Item\_26anc26 |  -1.6731239|  -3.0897386|
| t1Item\_27    |   0.4189673|  -1.0496750|
| t1Item\_28    |  -0.4766490|   1.1172366|
| t1Item\_29    |  -0.7819812|  -0.4780731|
| t1Item\_30    |   0.1274972|  -1.6324626|
| Item\_31anc31 |  -0.8481755|  -1.7911198|
| Item\_32anc32 |  -2.1690528|  -3.8170793|
| t1Item\_33    |  -1.8638447|   0.3550709|
| t1Item\_34    |  -1.5841127|  -3.6535600|
| t1Item\_35    |  -0.3051161|  -1.5002387|
| t1Item\_36    |  -0.4890469|  -2.6914909|
| t1Item\_37    |   0.2844209|  -1.1489655|
| t1Item\_38    |   1.6902380|   0.3264312|
| t1Item\_39    |  -1.8241728|  -0.8575798|
| t1Item\_40    |   0.0914811|  -1.2165515|
| t1Item\_41    |  -1.1258479|   1.3129808|
| Item\_42anc42 |   2.2212606|   1.3634859|
| Item\_43anc43 |   1.0059555|  -0.0156244|
| Item\_44anc44 |  -0.9980337|  -2.4376847|
| t1Item\_45    |  -0.7819812|   1.2631455|
| t1Item\_46    |  -1.4819189|  -1.3732578|
| t1Item\_47    |   1.2396679|   0.6008849|
| t1Item\_48    |  -0.6017413|  -3.6026550|
| t1Item\_49    |  -0.4890469|   0.8082684|
| t1Item\_50    |   1.1498068|   1.0854722|

Los ítems ancla no tienen los mismos parámetros, porque las personas que contestaron los ítems son distintas. Lo podemos verlo con un mapa de Wright.

``` r
f_score_test1 = fscores(params_test1)[,"F1"]
f_score_test2 = fscores(params_test2)[,"F1"]


anchor1 = coef(params_test1, IRTpars = T, simplify=T)$items[n_anchor,2]
anchor2 = coef(params_test2, IRTpars = T, simplify=T)$items[n_anchor,2]
```

``` r
WrightMap::wrightMap(thetas = f_score_test1, thresholds = anchor1, show.thr.lab = FALSE, label.items.srt = 45, main.title = "Ítems ancla en test 1")
```

![](README_files/figure-markdown_github/unnamed-chunk-53-1.png)

    ##                     [,1]
    ## Item_1anc1   -0.51391223
    ## Item_3anc3    0.04352311
    ## Item_4anc4    0.67059871
    ## Item_7anc7   -0.62708776
    ## Item_9anc9    0.17561015
    ## Item_14anc14 -0.63980683
    ## Item_15anc15  0.80129533
    ## Item_20anc20 -0.40270442
    ## Item_22anc22 -1.56674845
    ## Item_25anc25  1.52994569
    ## Item_26anc26 -1.67312387
    ## Item_31anc31 -0.84817552
    ## Item_32anc32 -2.16905279
    ## Item_42anc42  2.22126059
    ## Item_43anc43  1.00595553
    ## Item_44anc44 -0.99803371

``` r
WrightMap::wrightMap(thetas = f_score_test2, thresholds = anchor2, show.thr.lab = FALSE, label.items.srt = 45, main.title = "Ítems ancla en test 2")
```

![](README_files/figure-markdown_github/unnamed-chunk-54-1.png)

    ##                     [,1]
    ## Item_1anc1   -1.46345748
    ## Item_3anc3   -0.93665971
    ## Item_4anc4   -0.50764981
    ## Item_7anc7   -2.07034121
    ## Item_9anc9   -0.61210244
    ## Item_14anc14 -1.55621723
    ## Item_15anc15 -0.30266379
    ## Item_20anc20 -1.30276820
    ## Item_22anc22 -2.63235351
    ## Item_25anc25  0.51354111
    ## Item_26anc26 -3.08973860
    ## Item_31anc31 -1.79111979
    ## Item_32anc32 -3.81707931
    ## Item_42anc42  1.36348590
    ## Item_43anc43 -0.01562441
    ## Item_44anc44 -2.43768471

En el test 2 los ítems ancla resultaron más fáciles, lo que típicamente observaríamos en escalamiento vertical.

### Linking propiamente tal:

Lo anterior fue simular datos, estimar parámetros y graficar los resultados. Ahora vamos a hacer el linking.

``` r
library(equateIRT)
forma1 = import.mirt(params_test1) ## Los extrae ocupando los parámetros como en el modelo de regresión, no en nomenclatura IRT
```

    ##              value.d  SE.d
    ## Item_1anc1     0.514 0.122
    ## t1Item_2       0.848 0.126
    ## Item_3anc3    -0.044 0.120
    ## Item_4anc4    -0.671 0.124
    ## t1Item_5       0.614 0.123
    ## t1Item_6      -1.804 0.149
    ## Item_7anc7     0.627 0.123
    ## t1Item_8      -0.444 0.122
    ## Item_9anc9    -0.176 0.120
    ## t1Item_10     -0.815 0.125
    ## t1Item_11     -0.236 0.120
    ## t1Item_12      1.766 0.147
    ## t1Item_13      0.440 0.121
    ## Item_14anc14   0.640 0.123
    ## Item_15anc15  -0.801 0.125
    ## t1Item_16      1.026 0.128
    ## t1Item_17     -0.964 0.128
    ## t1Item_18     -0.407 0.121
    ## t1Item_19      1.097 0.130
    ## Item_20anc20   0.403 0.121
    ## t1Item_21      0.888 0.126
    ## Item_22anc22   1.567 0.141
    ## t1Item_23     -0.556 0.122
    ## t1Item_24     -1.654 0.144
    ## Item_25anc25  -1.530 0.140
    ## Item_26anc26   1.673 0.144
    ## t1Item_27     -0.419 0.121
    ## t1Item_28      0.477 0.122
    ## t1Item_29      0.782 0.125
    ## t1Item_30     -0.127 0.120
    ## Item_31anc31   0.848 0.126
    ## Item_32anc32   2.169 0.162
    ## t1Item_33      1.864 0.150
    ## t1Item_34      1.584 0.141
    ## t1Item_35      0.305 0.121
    ## t1Item_36      0.489 0.122
    ## t1Item_37     -0.284 0.121
    ## t1Item_38     -1.690 0.145
    ## t1Item_39      1.824 0.149
    ## t1Item_40     -0.091 0.120
    ## t1Item_41      1.126 0.130
    ## Item_42anc42  -2.221 0.165
    ## Item_43anc43  -1.006 0.128
    ## Item_44anc44   0.998 0.128
    ## t1Item_45      0.782 0.125
    ## t1Item_46      1.482 0.138
    ## t1Item_47     -1.240 0.133
    ## t1Item_48      0.602 0.123
    ## t1Item_49      0.489 0.122
    ## t1Item_50     -1.150 0.131
    ## 
    ## NOTE: Use the modIRT function to transform parameters in the usual IRT parameterization

``` r
forma2 = import.mirt(params_test2)
```

    ##              value.d  SE.d
    ## Item_1anc1     1.463 0.156
    ## t2t1Item_2     3.090 0.209
    ## Item_3anc3     0.937 0.148
    ## Item_4anc4     0.508 0.144
    ## t2t1Item_5    -0.991 0.147
    ## t2t1Item_6     0.612 0.145
    ## Item_7anc7     2.070 0.170
    ## t2t1Item_8     1.285 0.153
    ## Item_9anc9     0.612 0.145
    ## t2t1Item_10   -3.535 0.236
    ## t2t1Item_11    0.259 0.143
    ## t2t1Item_12   -1.798 0.160
    ## t2t1Item_13    0.749 0.146
    ## Item_14anc14   1.556 0.158
    ## Item_15anc15   0.303 0.143
    ## t2t1Item_16   -2.630 0.186
    ## t2t1Item_17    1.500 0.157
    ## t2t1Item_18    2.070 0.170
    ## t2t1Item_19    0.969 0.149
    ## Item_20anc20   1.303 0.154
    ## t2t1Item_21    0.303 0.143
    ## Item_22anc22   2.632 0.189
    ## t2t1Item_23   -1.555 0.155
    ## t2t1Item_24    3.505 0.232
    ## Item_25anc25  -0.514 0.143
    ## Item_26anc26   3.090 0.209
    ## t2t1Item_27    1.050 0.150
    ## t2t1Item_28   -1.117 0.148
    ## t2t1Item_29    0.478 0.144
    ## t2t1Item_30    1.632 0.160
    ## Item_31anc31   1.791 0.163
    ## Item_32anc32   3.817 0.254
    ## t2t1Item_33   -0.355 0.143
    ## t2t1Item_34    3.654 0.242
    ## t2t1Item_35    1.500 0.157
    ## t2t1Item_36    2.691 0.191
    ## t2t1Item_37    1.149 0.151
    ## t2t1Item_38   -0.326 0.143
    ## t2t1Item_39    0.858 0.148
    ## t2t1Item_40    1.217 0.152
    ## t2t1Item_41   -1.313 0.151
    ## Item_42anc42  -1.363 0.152
    ## Item_43anc43   0.016 0.142
    ## Item_44anc44   2.438 0.182
    ## t2t1Item_45   -1.263 0.150
    ## t2t1Item_46    1.373 0.155
    ## t2t1Item_47   -0.601 0.144
    ## t2t1Item_48    3.603 0.239
    ## t2t1Item_49   -0.808 0.145
    ## t2t1Item_50   -1.085 0.148
    ## 
    ## NOTE: Use the modIRT function to transform parameters in the usual IRT parameterization

La siguiente tabla indica que hay 16 ítems en común (porque tienen el mismo nombre).

``` r
linkp(coef = list(forma1$coef, forma2$coef)) ## Este es el plan!
```

    ##      [,1] [,2]
    ## [1,]   50   16
    ## [2,]   16   50

``` r
modelo_eq_rasch = modIRT(coef=list(forma1$coef, forma2$coef),
       var = list(forma1$var,forma2$var),
       names = c("f1","f2"))
```

``` r
eq_vert = alldirec(mods = modelo_eq_rasch, method = "mean-mean")
summary(eq_vert)
```

    ## Link: f1.f2 
    ## Method: mean-mean 
    ## Equating coefficients:
    ##   Estimate  StdErr
    ## A   1.0000 0.00000
    ## B  -1.1042 0.10394
    ## 
    ## 
    ## Link: f2.f1 
    ## Method: mean-mean 
    ## Equating coefficients:
    ##   Estimate  StdErr
    ## A   1.0000 0.00000
    ## B   1.1042 0.10394

Nuestro valor **B** es .94791, lo cual indica que podemos poner los ítems en la misma escala (en términos del primer test) sumando el valor anterior a los parámetros y a los valores theta obtenidos en el test 2. Al sumar .94 a los parámetros del test 2 obtenemos los siguientes:

``` r
B = .94791
params_test2_corregido = coef(params_test2, IRTpars = T, simplify=T)$items[,2] + B
kable(data.frame(cbind(anchor1, params_test2_corregido[n_anchor])))
```

|               |     anchor1|          V2|
|:--------------|-----------:|-----------:|
| Item\_1anc1   |  -0.5139122|  -0.5155475|
| Item\_3anc3   |   0.0435231|   0.0112503|
| Item\_4anc4   |   0.6705987|   0.4402602|
| Item\_7anc7   |  -0.6270878|  -1.1224312|
| Item\_9anc9   |   0.1756101|   0.3358076|
| Item\_14anc14 |  -0.6398068|  -0.6083072|
| Item\_15anc15 |   0.8012953|   0.6452462|
| Item\_20anc20 |  -0.4027044|  -0.3548582|
| Item\_22anc22 |  -1.5667485|  -1.6844435|
| Item\_25anc25 |   1.5299457|   1.4614511|
| Item\_26anc26 |  -1.6731239|  -2.1418286|
| Item\_31anc31 |  -0.8481755|  -0.8432098|
| Item\_32anc32 |  -2.1690528|  -2.8691693|
| Item\_42anc42 |   2.2212606|   2.3113959|
| Item\_43anc43 |   1.0059555|   0.9322856|
| Item\_44anc44 |  -0.9980337|  -1.4897747|

Vemos que hay una asociación lineal fuerte, por lo que nos quedamos tranquilos con el resultado del proceso de linking

``` r
plot(anchor1, params_test2_corregido[n_anchor])
```

![](README_files/figure-markdown_github/unnamed-chunk-60-1.png)

Los resultados no son exactos, pero podemos aceptar la diferencia encontrada
