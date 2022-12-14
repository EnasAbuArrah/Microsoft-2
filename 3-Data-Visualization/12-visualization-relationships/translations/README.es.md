# Visualizaci贸n de Relaciones: Todo sobre la miel 馃嵂

|![ Sketchnote by [(@sketchthedocs)](https://sketchthedocs.dev) ](../../../sketchnotes/12-Visualizing-Relationships.png)|
|:---:|
|Visualizaci贸n de Relaciones - _Sketchnote by [@nitya](https://twitter.com/nitya)_ |

Siguiendo con el enfoque de la naturaleza de nuestra investigaci贸n, vamos a descubrir interesantes visualizaciones para mostrar las relaciones entre los distintos tipos de miel, seg煤n un conjunto de datos procedentes del [Departamento de Agricultura de Estados Unidos](https://www.nass.usda.gov/About_NASS/index.php). 

Este conjunto de datos, compuesto por unos 600 elementos, muestra la producci贸n de miel en muchos estados de Estados Unidos. As铆, por ejemplo, se puede ver el n煤mero de colonias, el rendimiento por colonia, la producci贸n total, las existencias, el precio por libra y el valor de la miel producida en un determinado estado entre 1998 y 2012, con una fila por a帽o para cada estado. 

Ser谩 interesante visualizar la relaci贸n entre la producci贸n de un estado determinado por a帽o y, por ejemplo, el precio de la miel en ese estado. Tambi茅n se podr铆a visualizar la relaci贸n entre la producci贸n de miel por colonia de los estados. Este intervalo de a帽os abarca el devastador "CCD" o "Colony Collapse Disorder" que se observ贸 por primera vez en 2006 (http://npic.orst.edu/envir/ccd.html), por lo que es un conjunto de datos conmovedor para estudiar. 馃悵

## [Cuestionario previo](https://purple-hill-04aebfb03.1.azurestaticapps.net/quiz/22)

En esta lecci贸n, puedes utilizar Seaborn, que ya has utilizado anteriormente, como una buena librer铆a para visualizar las relaciones entre las variables. Es especialmente interesante el uso de la funci贸n `relplot` de Seaborn, que permite realizar gr谩ficos de dispersi贸n y de l铆neas para visualizar r谩pidamente las '[relaciones estad铆sticas](https://seaborn.pydata.org/tutorial/relational.html?highlight=relationships)', que permiten al cient铆fico de datos comprender mejor c贸mo se relacionan las variables entre s铆.

## Gr谩ficos de dispersi贸n

Utiliza un gr谩fico de dispersi贸n para mostrar c贸mo ha evolucionado el precio de la miel, a帽o tras a帽o, por estado. Seaborn, utilizando `relplot`, agrupa convenientemente los datos de los estados y muestra puntos de datos tanto categ贸ricos como num茅ricos. 

Empecemos por importar los datos y Seaborn:

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
honey = pd.read_csv('../../data/honey.csv')
honey.head()
```
Observar谩 que los datos de la miel tienen varias columnas interesantes, como el a帽o y el precio por libra. Exploremos estos datos, agrupados por estados de Estados Unidos:

| state | numcol | yieldpercol | totalprod | stocks   | priceperlb | prodvalue | year |
| ----- | ------ | ----------- | --------- | -------- | ---------- | --------- | ---- |
| AL    | 16000  | 71          | 1136000   | 159000   | 0.72       | 818000    | 1998 |
| AZ    | 55000  | 60          | 3300000   | 1485000  | 0.64       | 2112000   | 1998 |
| AR    | 53000  | 65          | 3445000   | 1688000  | 0.59       | 2033000   | 1998 |
| CA    | 450000 | 83          | 37350000  | 12326000 | 0.62       | 23157000  | 1998 |
| CO    | 27000  | 72          | 1944000   | 1594000  | 0.7        | 1361000   | 1998 |


Crea un gr谩fico de dispersi贸n b谩sico para mostrar la relaci贸n entre el precio por libra de miel y su estado de origen en EE.UU. Haz que el eje `y` sea lo suficientemente alto como para mostrar todos los estados:

```python
sns.relplot(x="priceperlb", y="state", data=honey, height=15, aspect=.5);
```
![gr谩fico de dispersi贸n 1](../images/scatter1.png)

Ahora, muestra los mismos datos con un esquema de color miel para exponer c贸mo evoluciona el precio a lo largo de los a帽os. Puedes hacerlo a帽adiendo un par谩metro 'hue' para visualizar el cambio, a帽o tras a帽o:

> 鉁? Aprende m谩s sobre las [paletas de colores que puedes usar en Seaborn](https://seaborn.pydata.org/tutorial/color_palettes.html) - 隆prueba una hermosa combinaci贸n de colores del arco iris!

```python
sns.relplot(x="priceperlb", y="state", hue="year", palette="YlOrBr", data=honey, height=15, aspect=.5);
```
![gr谩fico de dispersi贸n 2](../images/scatter2.png)

Con este cambio de color, se puede ver que obviamente hay una fuerte progresi贸n a lo largo de los a帽os en cuanto al precio de la miel por libra. De hecho, si se observa un conjunto de muestras en los datos para comprobarlo (elige un estado determinado, Arizona por ejemplo) se puede ver un patr贸n de aumento de precios a帽o tras a帽o, con pocas excepciones:

| state | numcol | yieldpercol | totalprod | stocks  | priceperlb | prodvalue | year |
| ----- | ------ | ----------- | --------- | ------- | ---------- | --------- | ---- |
| AZ    | 55000  | 60          | 3300000   | 1485000 | 0.64       | 2112000   | 1998 |
| AZ    | 52000  | 62          | 3224000   | 1548000 | 0.62       | 1999000   | 1999 |
| AZ    | 40000  | 59          | 2360000   | 1322000 | 0.73       | 1723000   | 2000 |
| AZ    | 43000  | 59          | 2537000   | 1142000 | 0.72       | 1827000   | 2001 |
| AZ    | 38000  | 63          | 2394000   | 1197000 | 1.08       | 2586000   | 2002 |
| AZ    | 35000  | 72          | 2520000   | 983000  | 1.34       | 3377000   | 2003 |
| AZ    | 32000  | 55          | 1760000   | 774000  | 1.11       | 1954000   | 2004 |
| AZ    | 36000  | 50          | 1800000   | 720000  | 1.04       | 1872000   | 2005 |
| AZ    | 30000  | 65          | 1950000   | 839000  | 0.91       | 1775000   | 2006 |
| AZ    | 30000  | 64          | 1920000   | 902000  | 1.26       | 2419000   | 2007 |
| AZ    | 25000  | 64          | 1600000   | 336000  | 1.26       | 2016000   | 2008 |
| AZ    | 20000  | 52          | 1040000   | 562000  | 1.45       | 1508000   | 2009 |
| AZ    | 24000  | 77          | 1848000   | 665000  | 1.52       | 2809000   | 2010 |
| AZ    | 23000  | 53          | 1219000   | 427000  | 1.55       | 1889000   | 2011 |
| AZ    | 22000  | 46          | 1012000   | 253000  | 1.79       | 1811000   | 2012 |

Otra forma de visualizar esta progresi贸n es utilizar el tama帽o, en lugar del color. Para los usuarios dalt贸nicos, 茅sta podr铆a ser una mejor opci贸n. Edita tu visualizaci贸n para mostrar un aumento de precio por un aumento de la circunferencia del punto:

```python
sns.relplot(x="priceperlb", y="state", size="year", data=honey, height=15, aspect=.5);
```
Puedes ver que el tama帽o de los puntos aumenta gradualmente.

![gr谩fico de dispersi贸n 3](../images/scatter3.png)

驴Se trata de un simple caso de oferta y demanda? Debido a factores como el cambio clim谩tico y el colapso de las colonias, 驴hay menos miel disponible para la compra a帽o tras a帽o y, por tanto, el precio aumenta?

Para descubrir una correlaci贸n entre algunas de las variables de este conjunto de datos, exploremos algunos gr谩ficos de l铆neas.

## Gr谩ficos de l铆neas

Pregunta: 驴Existe un claro aumento del precio de la miel por libra a帽o tras a帽o? Lo m谩s f谩cil es descubrirlo creando un gr谩fico de l铆neas:

```python
sns.relplot(x="year", y="priceperlb", kind="line", data=honey);
```
Answer: Yes, with some exceptions around the year 2003:

![gr谩fico de l铆neas 1](../images/line1.png)

鉁? Como Seaborn est谩 agregando datos en torno a una l铆nea, muestra "las m煤ltiples mediciones en cada valor de x trazando la media y el intervalo de confianza del 95% en torno a la media". [Fuente](https://seaborn.pydata.org/tutorial/relational.html). Este comportamiento, que consume mucho tiempo, puede desactivarse a帽adiendo `ci=None`.

Pregunta: En 2003, 驴tambi茅n podemos ver un pico en la oferta de miel? 驴Y si se observa la producci贸n total a帽o tras a帽o?

```python
sns.relplot(x="year", y="totalprod", kind="line", data=honey);
```

![gr谩fico de l铆neas 2](../images/line2.png)

Respuesta: La verdad es que no. Si se observa la producci贸n total, parece haber aumentado en ese a帽o concreto, aunque en general la cantidad de miel que se produce disminuye en esos a帽os.

Pregunta: En ese caso, 驴qu茅 pudo causar ese repunte del precio de la miel en torno a 2003? 

Para descubrirlo, puedes explorar una cuadr铆cula de facetas.

## Cuadr铆culas de facetas

Las cuadr铆culas de facetas toman una faceta de su conjunto de datos (en nuestro caso, puede elegir "a帽o" para evitar que se produzcan demasiadas facetas). Seaborn puede entonces hacer un gr谩fico para cada una de esas facetas de sus coordenadas x e y elegidas para una comparaci贸n visual m谩s f谩cil. 驴Destaca el a帽o 2003 en este tipo de comparaci贸n?

Cree una cuadr铆cula de facetas continuando con el uso de `relplot` como recomienda [la documentaci贸n de Seaborn](https://seaborn.pydata.org/generated/seaborn.FacetGrid.html?highlight=facetgrid#seaborn.FacetGrid). 

```python
sns.relplot(
    data=honey, 
    x="yieldpercol", y="numcol",
    col="year", 
    col_wrap=3,
    kind="line"
```
En esta visualizaci贸n, se puede comparar el rendimiento por colonia y el n煤mero de colonias a帽o tras a帽o, uno al lado del otro con un ajuste de 3 para las columnas:

[cuadr铆cula de facetas](../images/facet.png)

Para este conjunto de datos, no hay nada que destaque especialmente en cuanto al n煤mero de colonias y su rendimiento, a帽o tras a帽o y estado tras estado. 驴Hay alguna forma diferente de buscar una correlaci贸n entre estas dos variables?

## Gr谩ficos de dos l铆neas

Prueba con un gr谩fico multil铆nea superponiendo dos gr谩ficos de l铆neas uno encima del otro, utilizando el 'despine' de Seaborn para eliminar sus espinas superiores y derechas, y utilizando `ax.twinx` [derivado de Matplotlib](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.twinx.html). Twinx permite que un gr谩fico comparta el eje x y muestre dos ejes y. As铆, mostrar el rendimiento por colonia y el n煤mero de colonias, superpuestos:

```python
fig, ax = plt.subplots(figsize=(12,6))
lineplot = sns.lineplot(x=honey['year'], y=honey['numcol'], data=honey, 
                        label = 'Number of bee colonies', legend=False)
sns.despine()
plt.ylabel('# colonies')
plt.title('Honey Production Year over Year');

ax2 = ax.twinx()
lineplot2 = sns.lineplot(x=honey['year'], y=honey['yieldpercol'], ax=ax2, color="r", 
                         label ='Yield per colony', legend=False) 
sns.despine(right=False)
plt.ylabel('colony yield')
ax.figure.legend();
```
![parcelas superpuestas](../images/dual-line.png)

Aunque no hay nada que salte a la vista en torno al a帽o 2003, nos permite terminar esta lecci贸n con una nota un poco m谩s alegre: aunque en general hay un n煤mero de colonias en descenso, el n煤mero de colonias se est谩 estabilizando aunque su rendimiento por colonia est茅 disminuyendo.

隆Vamos, abejas, vamos!

馃悵鉂わ笍
## 馃殌 Desaf铆o

En esta lecci贸n, has aprendido un poco m谩s sobre otros usos de los gr谩ficos de dispersi贸n y las cuadr铆culas de l铆neas, incluyendo las cuadr铆culas de facetas. Desaf铆ate a crear una cuadr铆cula de facetas utilizando un conjunto de datos diferente, tal vez uno que hayas utilizado antes de estas lecciones. F铆jate en el tiempo que se tarda en crearlas y en la necesidad de tener cuidado con el n煤mero de cuadr铆culas que necesitas dibujar utilizando estas t茅cnicas.
## [Cuestionario posterior a la clase](https://purple-hill-04aebfb03.1.azurestaticapps.net/quiz/23)

## Repaso y autoestudio

Los gr谩ficos de l铆neas pueden ser simples o bastante complejos. Lee un poco en la [documentaci贸n de Seaborn](https://seaborn.pydata.org/generated/seaborn.lineplot.html) sobre las diversas formas en que puedes construirlos. Intenta mejorar los gr谩ficos de l铆neas que construiste en esta lecci贸n con otros m茅todos listados en la documentaci贸n.
## Asignaci贸n

[Sum茅rgete en la colmena](assignment.es.md)
