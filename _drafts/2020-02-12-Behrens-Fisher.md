---
layout: post
title:
categories: [jekyll, rstats]
tags: [blogdown, knitr, servr, httpuv, websocket]
---

**Nivel: intermedio**

**Nota:** La primera sección es teórica o conceptual aunque se presentan formulas el énfasis no es en las computaciones matemáticas. Al final se presentan ejemplos en el lenguaje de programación estadística R.  

## &iquest Qué es el problema de Behrens-Fisher?

En general cuando deseamos comparar los promedios entre dos grupos independientes (eje. desempeño académico de dos grupos de estudiantes, entre sexos en una medida psicológica, etc.) podemos utilizar un prueba T para muestras independientes.  Siempre que podamos asumir que la variabilidad entre los grupos en la población es igual esto no es un problema.

En estos casos utilizamos la siguiente formula de T para muestras independientes:

$$\frac{(\mu_{2} - \mu_{1})-(\bar{X_{2}} - \bar{X_{1})}} {\sqrt{\frac{S_{pooled}^{2}}{n_{1}-1} + \frac{S_{pooled}^{2}}{n_{1}-1}}}$$

En donde el valor de *S <sub>pooled</sub>* se obtiene con la siguiente formula:

$$\frac{ (n_{1} - 1)S^2_{1} + n_{2} - 1)S^2_{2} }{n_{1} + n_{2} - 2}$$

Utilizando estas dos formula se obtiene un valor crítico de T. Este valor crítico se busca en las tablas de distribución de T con n - 2 grados de libertad para obtener la probabilidad acumulada. 

En el siguiente ejemplo observamos el codigo en *R* para comparar dos grupo asumiendo que provienen de poblaciones con varianzas iguales. 


{% highlight r %}
grupo1 = c(19, 15, 22, 13, 18, 15, 20, 25, 22)
grupo2 = c(14, 18, 17, 12, 21, 21, 24, 14)

t.test(x = grupo2, y = grupo1, alternative = "two.sided", mu = 0, paired = FALSE, var.equal = TRUE)
{% endhighlight %}



{% highlight text %}
## 
## 	Two Sample t-test
## 
## data:  grupo2 and grupo1
## t = -0.59, df = 15, p-value = 0.6
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  -5.342  3.037
## sample estimates:
## mean of x mean of y 
##     17.62     18.78
{% endhighlight %}

En la mayoría de las situaciones en Psicología y Educación que comparamos entre dos grupos independientes desconocemos si poseen una variabilidad igual en la población. Es en estas situaciones donde nos encontramos con el **problema de Behrens-Fisher**. Este problema se trata de como comparar los promedios de dos poblaciones cuando se desconoce la proporción de sus varianzas (Scheffé, 1970). En otras palabras, es un problema de como determinar cual es el denominador que debemos utilizar en la ecuación anterior, o que grados de libertad usar con la distribución de T.

A pesar de tener mas de 100 años este problema no posee una solución exacta en la estadísticas (OJO CONFIRMAR). Aunque existen varias soluciones aproximadas a este problema como: 1) aproximación de Welch–Satterthwaite, 2)

¿Existen pruebas que me permitan conocer si las varianzas de mis grupos son iguales?
Prueba de Levene
Prueba de O'Brien
Brown and Forsythe
Prueba de T para varianzas desiguales

# Referencias

Howell, D. C. (2013). Statistical Methods for Psychology (8th ed.). Belmont, CA: Wadsworth, Cengage Learning.

Scheffé, H. (1970). Practical Solutions of the Behrens-Fisher Problem. Journal of the American Statistical Association, 65(332), 1501-1508.





