# Guion largo para sustentar el Taller 1

Este guion esta pensado para explicar la presentacion de forma natural, no para leerlo palabra por palabra. La idea es que sirva como apoyo para entender que se hizo, por que se hizo y como interpretar cada resultado.

**Integrantes:**  
- JHONATAN ANDRES TAPIA CORDOBA  
- JORGE ANDRES JARAMILLO NEME  
- LUIS FERNANDO MEZA RAMREZ  

## Diapositiva 1. Titulo

Buenos dias. En este trabajo presentamos una aplicacion de Analisis de Componentes Principales, o ACP, sobre una base de datos de calidad del agua del Rio Cauca.

El proposito principal fue tomar varias variables fisico-quimicas medidas en el rio y resumirlas en unas pocas dimensiones que fueran mas faciles de interpretar. En lugar de analizar cada variable por separado, el ACP permite encontrar patrones comunes entre ellas.

En este taller buscamos responder varias preguntas: primero, como se comportan descriptivamente las variables; segundo, que relaciones existen entre ellas; tercero, como se organizan las observaciones en el plano factorial; cuarto, si existen observaciones atipicas; y finalmente, si es posible construir un indice a partir de los resultados.

La idea central de la presentacion es que la calidad del agua no se resume completamente en una sola variable. Hay una dimension asociada a carga contaminante y particulada, y otra dimension relacionada con oxigenacion y conductividad.

## Diapositiva 2. Datos y preparacion

La base original tenia 2368 registros y 56 variables. Antes de aplicar el ACP fue necesario hacer una preparacion de los datos, porque la informacion venia con formatos que podian generar problemas al momento del analisis.

Primero se limpiaron los nombres de las columnas para trabajar con nombres mas consistentes. Luego se convirtieron las variables numericas, corrigiendo casos donde los numeros aparecian con coma decimal o con notacion cientifica escrita de forma no estandar, por ejemplo con `*10E`.

Tambien se creo una variable llamada `anio_estacion`. Esta variable combina el ano de muestreo con la estacion. Esto fue importante porque no queriamos tratar una estacion como si fuera siempre el mismo individuo, sin importar el ano. La calidad del agua puede cambiar con el tiempo, entonces una observacion de una estacion en 1993 no necesariamente representa lo mismo que esa misma estacion en 2010.

Por eso, en el ACP cada individuo representa una combinacion espacio-temporal: un ano y una estacion de monitoreo.

Adicionalmente, se revisaron los valores faltantes. Algunas variables tenian ausencia total de informacion, es decir, 100 % de datos faltantes. Esas variables no aportaban informacion al ACP y se descartaron.

## Diapositiva 3. Variables activas y tratamiento

Despues de revisar la base, se seleccionaron siete variables activas para el ACP: turbiedad, solidos suspendidos totales, DBO, DQO, oxigeno disuelto, conductividad electrica y fosforo total.

Estas variables fueron seleccionadas porque tienen relevancia ambiental y disponibilidad suficiente de informacion.

La turbiedad y los solidos suspendidos totales se relacionan con material particulado en el agua. La DBO y la DQO se relacionan con carga organica y quimica. El oxigeno disuelto es clave porque indica condiciones de oxigenacion del agua. La conductividad electrica refleja la presencia de sales e iones disueltos. Finalmente, el fosforo total se asocia con nutrientes y posibles procesos de eutrofizacion.

Un punto importante es que todas estas variables presentaron asimetria positiva severa. Esto quiere decir que la mayoria de observaciones tenian valores relativamente bajos o medios, pero existian algunos valores muy altos que jalaban la distribucion hacia la derecha.

Para reducir el efecto excesivo de esos valores extremos, se aplico una transformacion `log1p`, que equivale a calcular el logaritmo de uno mas la variable. Se usa `log1p` porque permite manejar valores cero sin generar problemas.

Luego se estandarizaron las variables. Esto era necesario porque estaban medidas en unidades distintas: algunas en miligramos por litro, otra en UNT, otra en microSiemens por centimetro. Si no se estandarizaban, las variables con mayor escala numerica podrian dominar artificialmente el ACP.

Despues de eliminar registros incompletos, la matriz final quedo con 1475 observaciones, que representan el 62,29 % de la base de analisis.

## Diapositiva 4. Estadisticas descriptivas y correlaciones

En la exploracion descriptiva se observo una alta heterogeneidad en las variables. Esto se ve en los coeficientes de variacion, que fueron especialmente altos en DBO, fosforo total y oxigeno disuelto.

Un coeficiente de variacion alto significa que la desviacion estandar es grande en relacion con la media. En terminos practicos, quiere decir que los valores cambian bastante entre observaciones, estaciones o anos.

Tambien se identificaron valores atipicos univariados mediante el criterio de Tukey. Sin embargo, estos valores no se eliminaron automaticamente, porque en estudios ambientales un valor extremo puede representar un evento real: una descarga, una condicion hidrologica especial o un episodio de contaminacion.

Por eso, en lugar de borrar esos datos, se transformaron con `log1p` y luego se analizaron dentro del ACP.

En la matriz de correlacion ya transformada se observaron relaciones importantes. La mas fuerte fue entre turbiedad y solidos suspendidos totales, con una correlacion de 0,80. Esto tiene sentido ambiental, porque ambas variables estan asociadas con material particulado en el agua.

Tambien se encontro una correlacion de 0,60 entre DBO y fosforo total. Esto puede indicar que los procesos asociados a materia organica tambien estan relacionados con aportes de nutrientes.

Por otro lado, el oxigeno disuelto tuvo una correlacion negativa con la conductividad electrica, de -0,54. Esto sugiere que cuando aumenta la conductividad, el oxigeno disuelto tiende a disminuir, lo cual puede reflejar una condicion ambiental distinta a la carga particulada.

Estas correlaciones justifican el uso del ACP, porque muestran que las variables no son totalmente independientes y que hay estructura multivariada para resumir.

## Diapositiva 5. Varianza explicada por el ACP

El ACP genera nuevas variables llamadas componentes principales. Cada componente explica una parte de la variabilidad total de los datos.

En este caso, se uso el criterio de Kaiser para decidir cuantas componentes retener. Este criterio recomienda conservar las componentes con valor propio mayor que 1.

Los resultados muestran que se retienen tres componentes. La primera dimension explica el 31,57 % de la varianza. La segunda explica el 25,43 %. La tercera explica el 20,15 %. En conjunto, estas tres dimensiones explican el 77,15 % de la variabilidad total.

Esto es un buen porcentaje, porque significa que tres componentes resumen mas de tres cuartas partes de la informacion contenida en las siete variables originales.

El plano formado por la Dim 1 y la Dim 2 explica el 57,00 %. Este plano es el que se usa en la mayoria de graficos porque permite una interpretacion visual clara. Sin embargo, es importante aclarar que no contiene toda la informacion; la tercera dimension tambien aporta.

Por eso, las graficas del plano 1-2 son utiles para interpretar patrones generales, pero no deben tomarse como la unica lectura posible de los datos.

## Diapositiva 6. Nube de individuos

La nube de individuos muestra como se ubican las observaciones en el plano factorial formado por las dimensiones 1 y 2.

Cada punto representa una combinacion de ano y estacion. Los puntos cercanos al origen representan observaciones con perfiles mas cercanos al promedio. En cambio, los puntos alejados del origen representan observaciones con perfiles fisico-quimicos mas diferenciados.

Para interpretar una observacion en este plano, no basta con mirar que tan lejos esta. Tambien es importante mirar el coseno cuadrado, o cos2. El cos2 indica que tan bien representado esta un individuo en ese plano. Un cos2 alto significa que la posicion del punto en el grafico es confiable para interpretacion.

En el informe se destacan algunos individuos bien representados, como 2013_ANTES SUAREZ, 2011_PASO DEL COMERCIO, 1997_PUENTE HORMIGUERO, 1998_ANTES RIO OVEJAS y 2000_PASO DE LA BOLSA.

Estos casos tienen cosenos cuadrados altos, por lo tanto su ubicacion en el plano 1-2 se puede interpretar con mayor seguridad.

En terminos generales, esta nube permite ver que no todas las observaciones tienen el mismo perfil de calidad del agua. Algunas se alejan bastante del centro, lo que sugiere condiciones particulares en ciertos anos o estaciones.

## Diapositiva 7. Circulo de correlaciones

El circulo de correlaciones es una de las graficas mas importantes para interpretar el ACP, porque muestra como se relacionan las variables originales con las componentes principales.

En la primera dimension se observan cargas importantes de solidos suspendidos totales, turbiedad, DBO, DQO y fosforo total. Todas estas variables apuntan hacia una interpretacion comun: mayor carga contaminante, organica y particulada.

Por eso, la Dim 1 se interpreta como un gradiente de carga contaminante y particulada. Cuando una observacion tiene un valor alto en esta dimension, tiende a estar asociada con mayores niveles relativos de esas variables.

La segunda dimension esta dominada principalmente por oxigeno disuelto y conductividad electrica, pero en sentidos opuestos. Esto significa que esta dimension no esta explicando lo mismo que la Dim 1.

La Dim 2 se interpreta como un contraste entre oxigenacion e influencia ionica o conductiva. En un extremo aparecen condiciones asociadas con mayor oxigeno disuelto, y en el otro extremo condiciones asociadas con mayor conductividad.

Esta separacion es clave para el taller, porque muestra que la calidad del agua no se puede resumir completamente en una sola dimension. Hay por lo menos dos lecturas importantes: carga contaminante y condicion de oxigenacion/conductividad.

## Diapositiva 8. Biplot y datos atipicos

El biplot combina en una misma grafica la nube de individuos y las variables. Esto permite observar simultaneamente donde estan las observaciones y hacia donde apuntan las variables.

La regla general para interpretar un biplot es que las observaciones ubicadas en la direccion de una variable tienden a tener valores relativamente altos en esa variable. Por ejemplo, si un punto esta en la direccion de solidos suspendidos o turbiedad, se puede interpretar como una observacion asociada con mayor carga particulada.

Tambien se uso el biplot y las coordenadas factoriales para identificar posibles datos atipicos. En este caso, se definieron como atipicos factoriales los individuos con mayor distancia al origen en el plano 1-2.

Entre los casos mas alejados se encontraron 1993_JUANCHITO, 2010_MEDIACANOA, 2010_PASO DEL COMERCIO, 2010_PUERTO ISAACS, 2010_JUANCHITO y 2010_YOTOCO.

Es importante aclarar que estos registros no deben eliminarse automaticamente. En un analisis ambiental, un punto extremo puede ser muy informativo. Puede indicar un evento real de contaminacion, un cambio en el regimen del rio, una condicion temporal particular o una situacion que merece seguimiento.

Entonces, en este taller se interpretan como observaciones extremas desde el punto de vista factorial, no necesariamente como errores.

## Diapositiva 9. Sintesis con contribuciones y cosenos

Para sustentar la interpretacion de los ejes, se revisaron las contribuciones y los cosenos cuadrados.

La contribucion indica que tanto aporta una variable a la construccion de una dimension. Como hay siete variables, el aporte promedio esperado es 100 dividido entre 7, es decir, 14,29 %. Una variable con contribucion superior a ese valor aporta mas de lo esperado a esa dimension.

En la Dim 1, las variables con mayor contribucion fueron solidos suspendidos totales con 32,36 %, turbiedad con 23,45 % y DBO con 15,71 %. Esto confirma que la Dim 1 esta dominada por variables asociadas con carga particulada y contaminante.

Ademas, los cosenos cuadrados muestran que solidos suspendidos y turbiedad estan bien representados por la Dim 1. Esto fortalece la interpretacion, porque no solo contribuyen mucho, sino que ademas quedan bien explicadas por ese eje.

En la Dim 2, las variables dominantes fueron oxigeno disuelto con 41,02 % y conductividad electrica con 32,98 %. Estas contribuciones estan muy por encima del promedio esperado, por lo que son las variables centrales para interpretar la segunda dimension.

En resumen, las contribuciones y cosenos respaldan que la Dim 1 representa carga contaminante/particulada, mientras que la Dim 2 representa el contraste oxigenacion-conductividad.

## Diapositiva 10. Indice parcial

Una de las preguntas del taller era si era posible construir un indice.

La respuesta es si, pero con una precision importante: se puede construir un indice parcial basado en la primera componente, pero no conviene llamarlo indice global de calidad del agua.

La razon es que la Dim 1 explica el 31,57 % de la variabilidad y tiene una interpretacion ambiental coherente. En esa dimension, valores altos se relacionan con mayor carga contaminante y particulada.

Entonces se construyo un indice a partir de la coordenada de cada individuo en PC1 y se normalizo en una escala de 0 a 100. Con esta normalizacion, los valores cercanos a 100 indican mayor carga contaminante o particulada segun la estructura capturada por PC1.

Sin embargo, este indice no resume toda la calidad del agua, porque la Dim 2 contiene informacion importante sobre oxigeno disuelto y conductividad electrica. Si se usara solo PC1 como indice global, se perderia esa informacion.

Por eso, la interpretacion correcta es: indice parcial de carga contaminante/particulada.

Los mayores valores individuales del indice aparecieron en casos como 2010_LA VICTORIA, 1994_PASO DEL COMERCIO, 2010_ANACARO, 2010_MEDIACANOA y 2010_PASO DEL COMERCIO.

Cuando se agrupo por estacion, las estaciones con mayor indice promedio fueron ANACARO, PUENTE LA VIRGINIA, LA VICTORIA, VIJES y PUENTE GUAYABAL.

Esto permite ordenar observaciones y estaciones segun su carga relativa, pero siempre con la advertencia de que es un indice parcial.

## Diapositiva 11. Conclusiones

Como conclusion general, el ACP permitio resumir la estructura multivariada de las variables fisico-quimicas del Rio Cauca.

La primera dimension representa principalmente una lectura de carga contaminante y particulada, asociada con solidos suspendidos, turbiedad, DBO, DQO y fosforo total.

La segunda dimension complementa esa lectura, porque representa el contraste entre oxigeno disuelto y conductividad electrica. Esto muestra que la calidad del agua no puede explicarse completamente con un solo eje.

Tambien se identificaron observaciones extremas, especialmente en algunos anos y estaciones. Estas observaciones son importantes porque pueden señalar eventos ambientales particulares y no deben descartarse sin una revision adicional.

Finalmente, si fue posible construir un indice, pero se debe interpretar como un indice parcial de carga contaminante/particulada. No es un indice global de calidad del agua, porque no incorpora completamente la informacion de la segunda dimension.

El principal hallazgo es que el comportamiento multivariado del Rio Cauca se organiza alrededor de dos lecturas: una de carga contaminante y particulada, y otra de oxigenacion frente a conductividad.

## Preguntas probables y respuestas ampliadas

### ¿Por que aplicaron transformacion log1p?

Porque las variables tenian asimetria positiva severa y valores extremos. La transformacion `log1p` reduce el peso de esos valores muy altos sin eliminarlos. Esto es importante porque en datos ambientales los extremos pueden ser reales. Ademas, `log1p` permite trabajar con valores cero, porque calcula logaritmo de uno mas la variable.

### ¿Por que estandarizaron las variables?

Porque las variables estaban en unidades diferentes. Por ejemplo, la turbiedad se mide en UNT, otras variables en mg/L y la conductividad en microSiemens por centimetro. Si no se estandarizan, las variables con escalas numericas mas grandes pueden dominar el ACP. La estandarizacion permite que todas entren al analisis en condiciones comparables.

### ¿Por que usaron el criterio de Kaiser?

El criterio de Kaiser conserva las componentes con valor propio mayor que 1. En un ACP normado, un valor propio mayor que 1 significa que esa componente explica mas varianza que una variable original promedio. En este caso, tres componentes cumplieron ese criterio y explicaron el 77,15 % de la variabilidad total.

### ¿Por que el indice no es global?

Porque PC1 resume principalmente la carga contaminante y particulada, pero no recoge completamente la informacion de oxigeno disuelto y conductividad electrica, que aparece con fuerza en PC2. Entonces, si se usa solo PC1, se obtiene un buen indice parcial de carga contaminante, pero no una medida completa de calidad del agua.

### ¿Que significa un dato atipico en el ACP?

Un dato atipico en el ACP es una observacion alejada del centro del plano factorial. Esto significa que su perfil multivariado es diferente al promedio. No necesariamente es un error. Puede ser una medicion real asociada con una condicion ambiental extrema o con un evento particular.

### ¿Cual seria la frase final para cerrar la sustentacion?

El ACP mostro que la calidad del agua del Rio Cauca tiene una estructura multivariada clara: una primera dimension asociada con carga contaminante y particulada, y una segunda dimension asociada con oxigenacion y conductividad. Por eso, el indice basado en PC1 es util, pero debe interpretarse como un indice parcial y no como una medida global de calidad del agua.
