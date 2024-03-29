# BNEXT - Prueba técnica

En este documento se explican los cálculos realizados y las herramientas utilizadas para contestar a cada supuesto. También se exponen las interpretaciones de los resultados.


### RECURSOS

Para poder realizar esta prueba técnica he utilizado las siguientes herramientas:

- Python: Podéis ver todos los pasos y cálculos que he realizado [aquí](https://github.com/galanx22/Bnext/blob/master/Prueba_técnica_BNEXT.ipynb) (a veces la previsualización no se carga por el tamaño del archivo, si se da este caso, recomiendo descargarlo y abrirlo con Jupyter Notebook).
- Tableau: Aprovechando que trabajáis mucho con Tableau, he querido generar las gráficas para que podáis verlas e interactuar con elloa. He creado un dashboard para cada una de las preguntas. Veréis el link al final de cada respuesta.


### PREGUNTA 1: 
#### La primera pregunta tiene que ver con los usuarios que han gastado en este periodo. ¿Se te ocurre alguna manera de agrupar a los usuarios en función de su valor? Explica por favor la razón de agruparlos de la manera elegida y los cálculos que has realizado para ello.

Para clusterizar a los clientes de Bnext, he querido utilizar dos de las variables que a mi entender son las más importantes, ya que representan la frecuencia de gasto y el importe medio.

Por ello he calculado las siguientes variables:
- Número de gastos diario
- Importe medio por gasto

Como en el supuesto se habla de 'usuarios que han gastado en este periodo', he considerado como gasto todas las operaciones de categoría 'Compra' y 'Transferencia', dejando a un lado la categoría 'Ingresos'.

Para la clusterización de los clientes en función de estas variables, he utilizado el algoritmo no supervisado K-means, ya que es uno de los que más se utiliza en estos casos.

El resultado de la clusterización ha sido el siguiente:

![alt text](https://github.com/galanx22/Bnext/blob/master/Imágenes/Clusterización%20K-Means.PNG)


##### Interpretación de los resultados:

Como podemos ver en el gráfico, hemos clasificado a los clientes en 3 clusters distintos (tal y como nos indicaba el Elbow Method), donde el punto amarillo indica el centroide de cada uno de ellos.

- El cluster nº 1 nos agrupa aquellos clientes que realizan muchas compras diarias pero de pequeños importes. Si observamos la gráfica, la cantidad gastada de este cluster va de 0€ hasta los 500 €, sin embargo la mayoría de los valores están más próximos a 0 € que a 500 €. Además los clientes de este clúster puede realizar hasta 9 compras diarias. 
- El cluster nº2 es el más importante. Es el clúster más numeroso y representa a todos los clientes que realizan varias compras diarias, cuya cantidad siempre es igual o superior a los 500€. Este cluster es de suma importancia ya que representa a la gran parte de clientes de Bnext. Observamos que la mayoría de los clientes realizan entre 0 y 3 compras diarias con cantidades que oscilan entre los 500€ y 1200€. 
- El cluster nº3 es el más reducido. Se trata de aquellos clientes que realizan entre 0 y 2 compras diarias pero gastan cantidades muy altas de dinero

Para ver la gráfica en Tableau, haga click [aquí](https://eu-west-1a.online.tableau.com/t/galanx/views/Bnextgrficos/Outliers?iframeSizedToWindow=true&:embed=y&:showAppBanner=false&:display_count=no&:showVizHome=no&:origin=viz_share_link).

#### Atención 

Tableau también utiliza el método K-means para clusterizar, sin embargo, la clusterización de Tableau es distinta a la que he realizado con Python. He probado a estandarizar las variables para ver si hacía coincidir ambas gráficas, pero Tableau seguía mostrandome el mismo resultado. Esto se debe a las diferencias en la implementación del algoritmo, ya que no hay una respuesta única, mecánica y correcta al problema planteado. 
En mi opinión, deberíamos estudiar cual de las dos opciones es más conveniente para Bnext y cual tiene una mayor compatibilidad con el resto de estudios sobre los clientes.

##### Interpretación de la clusterización en Tableau

- Cluster 1: Es el cluster más pequeño. Representa a los clientes que realizan 2 o más operaciones diarias pero la mayoría de los importes de dichas operaciones no superan los 500 €. El importe máximo de gasto de este cluster es de 2000€ (este importe está generado por outliers).
- Cluster 2 : Este cluster es el más númeroso, por lo que representa a la mayoría de los clientes de Bnext. Realizan entre 1 y 2 operaciones diarias cuyo importe medio por operación ronda los 1000€. El intervalo de gasto va desde poco más de 0€ hasta los 8000€ (importe generado por outliers).
- Cluster 3: Este clúster también es muy numeroso, y representa a los clientes de Bnext que realizan de 0 a 1 gasto diario. Estos clientes también tienen un importe medio de operación que ronda los 1000€, sin embargo el gasto máximo esta en 12.000€ (importe generado opr outliers). La gran diferencia con el cluster 2, es el número de operaciones diarias, ya que si quitasemos los outliers la cantidad de gasto sería muy similar.


### PREGUNTA 2:
#### Te pregunta el CEO que no entiende la evolución de los datos en el periodo escogido, que le parece algo anómala. ¿Encuentras algún patrón que permita encontrar outliers? Esta es una pregunta abierta, puedes analizar los datos de la manera que quieras. 

Para resolver esta pregunta, vamos a representar la evolución de las categorías 'Compras' e 'Ingresos' en el periodo dado.

Para la representación de estos datos he escogido un gráfico de línea, para que cualquier persona pueda entender y visualizar los outliers.

#### - Evolución de los ingresos

![alt text](https://github.com/galanx22/Bnext/blob/master/Imágenes/Income%20Evolution.PNG)


##### Interpretación de los resultados

Visualizando esta gráfica, observamos que el día 23 de noviembre del 2018, existe un pico muy alto que sobresale por encima de la evolución normal de los gastos.

Esto es debido a que dicha fecha corresponde con el Black Friday, el día de mayor consumo del año a nivel mundial.

Además, el Black Friday es un día donde las compras online son mucho mayores, lo que favorece al perfil de cliente de Bnext, que por lo que tengo entendido, muchos de ellos se caracterizan por utilizar su tarjeta Bnext para compras online.

También podemos apreciar una caída de las compras entre el 30/11 y el 01/12, que se debe a la falta de datos para el primer día de diciembre, ya que solo disponemos de datos hasta las 8 de la mañana.


#### - Evolución de los gastos

![alt text](https://github.com/galanx22/Bnext/blob/master/Imágenes/Puchases%20evolution.PNG)


##### Interpretación de los resultados

En esta gráfica que representa la evolución de los ingresos, vemos como en el día del Black Friday existe un pico muy parecido al que hemos visto anteriormente en las compras.

Este outlier es muy probable que sea gracias a las promociones disponibles en el marketplace de Bnext, las cuales incitan a que el cliente ingrese dinero en la cuenta Bnext para aprovechar los descuentos/promociones disponibles de vuestros partners.

También observamos como a final de mes, la evolución de los ingresos va creciendo. La justificación más lógica es que esas fechas coinciden con el periodo en el que los clientes cobran su sueldo.

Sin embargo vemos como entre el día 30/11/2018 y el día 01/12/2018 los ingresos se desploman, pero esto no es significativo ya que del primer día de diciembre solo tenemos datos hasta las 8 de las mañana.

De hecho me aventuraría a decir, que si tuviesemos los datos de los primeros días de diciembre podríamos ver como la evolución sigue siendo positiva, por lo menos, hasta el día 10/01(sigue siendo periodo de cobro de salarios). 

Para ver las gráficas en Tableau, haga click [aquí](https://eu-west-1a.online.tableau.com/t/galanx/views/Bnextgrficos/Outliers?iframeSizedToWindow=true&:embed=y&:showAppBanner=false&:display_count=no&:showVizHome=no&:origin=viz_share_link).

### Pregunta 3: 
#### Busca el concepto de cohorte si no estás familiarizadx con él, y realiza un análisis de cohortes diarias. Puedes considerar que la primera transacción de cada usuario en la muestra fue su primera transacción en Bnext. 


Para resolver la siguiente pregunta, he realizado cohortes diarios considerando que la primera transacción de cada usuario en la muestra, fue su primera transacción en Bnext.

Una vez obtenidos estos datos, he analizado la actividad de dichos clientes observando los días posteriores a su primera transacción.

De esta manera he podido sacar la tasa de retención de cliente para cada uno de los cohortes realizados.

Este análisis se suele realizar con un periodo de tiempo mucho más grande del que disponemos, por lo que dada esta muestra, el resultado no es demasiado representativo.


##### Explicación del gráfico

El eje de ordenadas (Eje Y) representa los distintos grupos de cohortes diarios, que corresponden a cada día de la muestra.

El eje de abscisas (Eje X) representa los días posteriores a cada uno de los cohortes, llamados periodos de cohorte.

Los periodos de cohorte nos indican como ha sido la evolución de usuarios después de su primer uso de la app de Bnext.

Por ejemplo: El 18% de los usuarios que hicieron su primera transacción el 22/11/2018 volvieron a comprar el 24/11/2018 (periodo de cohorte 3).

El periodo 1 de cohorte como coincide con el día del grupo de cohorte siempre va a ser el 100%.



![alt text](https://github.com/galanx22/Bnext/blob/master/Imágenes/Cohorts%20-%20User%20Retention.PNG)



##### Interpretación de los resultados

En este gráfico podemos ver que los usuarios tienden a comprar menos a medida que pasa el tiempo.

Sin embargo, también podemos ver que los dos primeros cohortes son los más fuertes (20/11/2018 y 21/11/2018), lo que hace preguntarnos que atributos comunes en estos usuarios podrían estar causando una mayor implicación con la app de Bnext respecto al resto.

Esto puede deberse a diversos factores, como el método de captación de usuarios, la campaña de marketing que se utilizó, una promoción de registro, etc.

De todas formas, con los datos que disponemos, solo podemos interpretar los 3 ó 4 primero cohortes, y en estos no se puede concluir que exista ni un ascenso ni un descenso significativo del uso de la aplicación. Necesitaríamos más datos sobre la evolución de los cohortes para determinar la retención de clientes.

Para ver la gráfica en Tableau, haga click [aquí](https://eu-west-1a.online.tableau.com/t/galanx/views/Bnextgrficos/Outliers?iframeSizedToWindow=true&:embed=y&:showAppBanner=false&:display_count=no&:showVizHome=no&:origin=viz_share_link).

