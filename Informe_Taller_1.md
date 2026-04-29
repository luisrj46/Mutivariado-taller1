# Taller 1. Informe de Analisis de Componentes Principales

**Curso:** Analisis Multivariado  
**Programa:** Maestria en Inteligencia Artificial y Ciencia de Datos  
**Tema:** Analisis de Componentes Principales aplicado a calidad del agua del Rio Cauca  
**Fuente de datos:** `Base de datos/Calidad_del_agua_del_Rio_Cauca_20260419.csv`  
**Fecha de entrega:** Mayo 2 de 2026

## Resumen ejecutivo

El Analisis de Componentes Principales aplicado a siete variables fisico-quimicas del Rio Cauca permitio resumir la informacion en tres componentes con valor propio mayor que 1. Estas tres dimensiones explican el **77,15 %** de la variabilidad total. La primera dimension representa un gradiente de carga contaminante y particulada, dominado por solidos suspendidos, turbiedad, DBO, DQO y fosforo total. La segunda dimension contrasta oxigeno disuelto y conductividad electrica, por lo que aporta una lectura ambiental complementaria.

Los resultados muestran que si es posible construir un indice, pero debe interpretarse como **indice parcial de carga contaminante/particulada**, no como indice global de calidad del agua. Tambien se identificaron observaciones extremas en anos y estaciones especificas, entre ellas JUANCHITO 1993 y varias estaciones en 2010, que deben revisarse como posibles eventos ambientales particulares y no eliminarse automaticamente.

## 1. Introduccion

El presente informe desarrolla una aplicacion tecnica de Analisis de Componentes Principales (ACP) sobre una base de datos real de calidad del agua del Rio Cauca. El objetivo es resumir la estructura multivariada de un conjunto de variables fisico-quimicas, identificar relaciones entre indicadores ambientales, observar patrones entre estaciones de monitoreo y evaluar si es posible construir un indice sintetico a partir de los componentes principales.

El ACP es pertinente para este caso porque las variables de calidad del agua se encuentran medidas en distintas unidades y pueden presentar correlaciones entre si. La tecnica permite transformar el conjunto original de variables en nuevas dimensiones no correlacionadas, denominadas componentes principales, que concentran la mayor parte posible de la variabilidad total.

## 2. Datos y preparacion metodologica

La base original contiene **2368 registros y 56 variables**. Como primer paso, se realizo una limpieza de nombres de columnas, conversion de variables numericas y normalizacion de formatos atipicos, incluyendo separador decimal con coma y notacion cientifica escrita como `*10E`.

Se construyo el identificador `anio_estacion`, combinando el ano de muestreo con la estacion. Esta decision permite interpretar cada individuo como una observacion espacio-temporal, evitando mezclar mediciones de diferentes anos en una misma estacion.

Durante la auditoria de valores faltantes se identificaron variables con ausencia total de informacion, por ejemplo hierro disuelto, manganeso disuelto, sodio disuelto, potasio disuelto, cobre disuelto, zinc disuelto, cianuros, fluoruros, sulfuros y silice. Por esta razon, el ACP se concentro en variables con disponibilidad y relevancia ambiental.

Las variables activas seleccionadas fueron:

| Variable | Interpretacion ambiental |
|---|---|
| Turbiedad | Material particulado y transparencia del agua |
| Solidos suspendidos totales | Carga de sedimentos y particulas |
| Demanda bioquimica de oxigeno (DBO) | Materia organica biodegradable |
| Demanda quimica de oxigeno (DQO) | Carga organica y quimica oxidable |
| Oxigeno disuelto | Condicion de oxigenacion del agua |
| Conductividad electrica | Presencia de sales e iones disueltos |
| Fosforo total | Nutrientes asociados a eutrofizacion |

Todas las variables seleccionadas presentaron asimetria positiva severa, por lo cual se aplico transformacion `log1p`. Posteriormente se eliminaron registros incompletos mediante eliminacion por caso completo. La matriz final del ACP quedo conformada por **1475 observaciones**, equivalentes al **62,29 %** de la base de analisis.

## 3. Estadisticas descriptivas, correlaciones y graficos

La exploracion inicial muestra alta dispersion en las variables seleccionadas. Los coeficientes de variacion fueron elevados, especialmente en DBO, fosforo total y oxigeno disuelto. Esto evidencia heterogeneidad importante en la calidad del agua observada a traves del tiempo y entre estaciones. Ademas, todas las variables presentaron asimetria positiva mayor que 2, por lo cual se justifico la transformacion logaritmica antes del ACP.

| Variable | n | Media | Desv. est. | Min | Max | Asimetria | CV % |
|---|---:|---:|---:|---:|---:|---:|---:|
| Turbiedad | 2185 | 128,00 | 169,00 | 1,00 | 1900,00 | 2,90 | 132,00 |
| Solidos suspendidos totales | 2297 | 161,00 | 199,00 | 1,20 | 2112,00 | 3,13 | 124,00 |
| DBO | 2203 | 5,94 | 19,10 | 0,10 | 427,00 | 12,20 | 322,00 |
| DQO | 2134 | 30,20 | 37,90 | 1,46 | 706,00 | 6,90 | 125,00 |
| Oxigeno disuelto | 2289 | 4,70 | 9,39 | 0,00 | 216,00 | 14,70 | 200,00 |
| Conductividad electrica | 2305 | 123,00 | 106,00 | 0,00 | 4259,00 | 28,10 | 85,50 |
| Fosforo total | 1850 | 0,30 | 0,88 | 0,00 | 14,20 | 9,64 | 293,00 |

El diagnostico de valores extremos mediante el criterio de Tukey mostro presencia de atipicos univariados en todas las variables, especialmente en turbiedad, DQO, solidos suspendidos y DBO. Por esta razon, dichos valores no se eliminaron de forma automatica; se redujo su peso relativo mediante `log1p` y se evaluaron posteriormente en el plano factorial.

| Variable | Atipicos univariados | Accion aplicada |
|---|---:|---|
| Turbiedad | 216 | Transformacion log1p |
| Solidos suspendidos totales | 159 | Transformacion log1p |
| DBO | 152 | Transformacion log1p |
| DQO | 201 | Transformacion log1p |
| Oxigeno disuelto | 35 | Transformacion log1p |
| Conductividad electrica | 15 | Transformacion log1p |
| Fosforo total | 95 | Transformacion log1p |

![Distribuciones fisico-quimicas grupo A](Graficos%20de%20resultados/distribuciones%20fisico-quimica_grupo_A.png)

![Distribuciones fisico-quimicas grupo B](Graficos%20de%20resultados/distribuciones%20fisico-quimica_grupo_B.png)

La matriz de correlacion transformada indica relaciones relevantes. La asociacion mas fuerte se presenta entre **turbiedad y solidos suspendidos totales** (r = 0,80), lo cual es coherente con la interpretacion ambiental de carga particulada. Tambien se observa relacion entre **DBO y fosforo total** (r = 0,60), que puede asociarse a procesos de contaminacion organica y aporte de nutrientes. Por otra parte, el oxigeno disuelto se relaciona negativamente con la conductividad electrica (r = -0,54) y con DQO (r = -0,27), sugiriendo una dimension diferente vinculada con condiciones de oxigenacion frente a carga ionica o quimica.

| Variable | Turbiedad | SST | DBO | DQO | OD | Conductividad | Fosforo |
|---|---:|---:|---:|---:|---:|---:|---:|
| Turbiedad | 1,00 | 0,80 | 0,09 | 0,23 | 0,15 | -0,06 | 0,10 |
| SST | 0,80 | 1,00 | 0,21 | 0,38 | 0,10 | 0,07 | 0,23 |
| DBO | 0,09 | 0,21 | 1,00 | 0,15 | -0,20 | 0,23 | 0,60 |
| DQO | 0,23 | 0,38 | 0,15 | 1,00 | -0,27 | 0,24 | -0,01 |
| OD | 0,15 | 0,10 | -0,20 | -0,27 | 1,00 | -0,54 | 0,16 |
| Conductividad | -0,06 | 0,07 | 0,23 | 0,24 | -0,54 | 1,00 | -0,01 |
| Fosforo | 0,10 | 0,23 | 0,60 | -0,01 | 0,16 | -0,01 | 1,00 |

![Matriz de correlacion](Graficos%20de%20resultados/Matriz%20de%20correlacion:%20Espacion%20de%20variable.png)

## 4. Analisis de Componentes Principales

El ACP se realizo sobre variables transformadas y estandarizadas. La estandarizacion es necesaria porque las variables estan expresadas en unidades diferentes: UNT, mg/L y microS/cm. Las variables `anio_estacion` y `estaciones` se trataron como cualitativas suplementarias para apoyar la interpretacion, sin influir en la construccion de los ejes factoriales.

Los valores propios obtenidos fueron:

| Componente | Valor propio | % varianza | % acumulado |
|---|---:|---:|---:|
| Dim 1 | 2,210 | 31,568 | 31,568 |
| Dim 2 | 1,780 | 25,431 | 56,999 |
| Dim 3 | 1,410 | 20,148 | 77,147 |
| Dim 4 | 0,670 | 9,565 | 86,712 |
| Dim 5 | 0,466 | 6,659 | 93,371 |
| Dim 6 | 0,296 | 4,224 | 97,594 |
| Dim 7 | 0,168 | 2,406 | 100,000 |

Con el criterio de Kaiser, se retienen **tres componentes** con valores propios mayores que 1. Estos tres componentes explican el **77,15 %** de la variabilidad total. El plano factorial 1-2 explica **57,00 %**, porcentaje suficiente para una primera lectura grafica, aunque no agota completamente la estructura multivariada. Por ello, las interpretaciones graficas se concentran en Dim 1 y Dim 2, mientras que la decision de retencion reconoce que existe una tercera dimension con informacion adicional.

![Sedimentacion de varianza](Graficos%20de%20resultados/Sedimentacion%20de%20varianza.png)

## 5. Nube de individuos

La nube de individuos permite observar como se distribuyen las observaciones espacio-temporales en el plano factorial formado por las dimensiones 1 y 2. Los puntos mas alejados del origen representan observaciones con perfiles fisico-quimicos mas diferenciados respecto al comportamiento promedio.

Los individuos mejor representados en el plano, segun el coseno cuadrado acumulado en Dim 1 y Dim 2, fueron:

| Individuo | Dim 1 | Dim 2 | Cos2 plano |
|---|---:|---:|---:|
| 2013_ANTES SUAREZ | -2,145 | 1,375 | 0,992 |
| 2011_PASO DEL COMERCIO | 1,929 | 1,695 | 0,985 |
| 1997_PUENTE HORMIGUERO | -2,190 | 1,341 | 0,978 |
| 1998_ANTES RIO OVEJAS | -4,093 | -0,461 | 0,976 |
| 2000_PASO DE LA BOLSA | -1,714 | 1,469 | 0,972 |

Estos casos tienen una representacion confiable en el plano 1-2, por lo cual su posicion grafica puede interpretarse con mayor seguridad.

![Nube de individuos](Graficos%20de%20resultados/Nube%20de%20individuos.png)

## 6. Circulo de correlaciones

El circulo de correlaciones muestra la relacion entre las variables originales y los componentes principales. En la Dim 1 predominan variables asociadas a carga contaminante y particulada: solidos suspendidos totales, turbiedad, DBO, DQO y fosforo total. En la Dim 2 se destacan principalmente oxigeno disuelto y conductividad electrica, pero con signos opuestos.

La interpretacion de los dos primeros ejes es la siguiente:

| Dimension | Variables principales | Interpretacion |
|---|---|---|
| Dim 1 | Solidos suspendidos, turbiedad, DBO, DQO, fosforo | Gradiente de carga contaminante, organica y particulada |
| Dim 2 | Oxigeno disuelto (+), conductividad electrica (-) | Contraste entre oxigenacion e influencia ionica/conductiva |

![Circulo de correlaciones](Graficos%20de%20resultados/Circulos%20de%20correlaciones%20Plano%201-2.png)

## 7. Biplot y datos atipicos

El biplot integra individuos y variables en una misma representacion. Las observaciones ubicadas en la direccion de una variable tienden a presentar valores relativamente altos en esa variable. En el lado positivo de la Dim 1 se ubican observaciones asociadas a mayor carga particulada y organica; en la Dim 2 se observa el contraste entre oxigeno disuelto y conductividad electrica.

Para identificar posibles datos atipicos se utilizo la distancia al origen en el plano factorial. Los diez casos mas alejados fueron:

| Individuo | Estacion | Dim 1 | Dim 2 | Distancia | Cos2 plano |
|---|---|---:|---:|---:|---:|
| 1993_JUANCHITO | JUANCHITO | -3,216 | 6,571 | 53,519 | 0,393 |
| 2010_MEDIACANOA | MEDIACANOA | 4,819 | 4,587 | 44,265 | 0,329 |
| 2010_PASO DEL COMERCIO | PASO DEL COMERCIO | 4,734 | 4,277 | 40,700 | 0,317 |
| 2010_PUERTO ISAACS | PUERTO ISAACS | 4,691 | 4,267 | 40,219 | 0,313 |
| 2010_JUANCHITO | JUANCHITO | 3,500 | 5,149 | 38,761 | 0,297 |
| 2010_YOTOCO | YOTOCO | 4,478 | 4,081 | 36,700 | 0,274 |
| 1990_ANTES INTERCEPTOR SUR | ANTES INTERCEPTOR SUR | 4,575 | -3,844 | 35,708 | 0,740 |
| 1994_PASO DEL COMERCIO | PASO DEL COMERCIO | 5,086 | -2,800 | 33,702 | 0,753 |
| 2010_ANACARO | ANACARO | 4,887 | 3,125 | 33,653 | 0,240 |
| 1992_ANTES RIO TIMBA | ANTES RIO TIMBA | -4,925 | 3,058 | 33,600 | 0,554 |

Estos registros no deben eliminarse automaticamente, ya que pueden corresponder a eventos reales de contaminacion, condiciones hidrologicas particulares o cambios temporales relevantes. Deben interpretarse como observaciones extremas desde el punto de vista factorial.

![Biplot](Graficos%20de%20resultados/Relacion%20Dual%20individuos%20-%20variables.png)

## 8. Sintesis con contribuciones y cosenos cuadrados

El aporte promedio esperado por variable en cada dimension es 100/7 = **14,29 %**. En la Dim 1, las mayores contribuciones corresponden a solidos suspendidos totales, turbiedad y DBO. En conjunto, estas variables sostienen la interpretacion de la Dim 1 como un gradiente de carga contaminante y particulada.

| Variable | Coord. Dim 1 | Contrib. Dim 1 | Cos2 Dim 1 |
|---|---:|---:|---:|
| Solidos suspendidos totales | 0,846 | 32,358 | 0,715 |
| Turbiedad | 0,720 | 23,453 | 0,518 |
| DBO | 0,589 | 15,712 | 0,347 |
| DQO | 0,547 | 13,519 | 0,299 |
| Fosforo total | 0,491 | 10,913 | 0,241 |
| Conductividad electrica | 0,277 | 3,477 | 0,077 |
| Oxigeno disuelto | -0,112 | 0,568 | 0,013 |

En la Dim 2, las variables dominantes son oxigeno disuelto y conductividad electrica. La oposicion de signos sugiere que este componente expresa una condicion ambiental distinta a la Dim 1.

| Variable | Coord. Dim 2 | Contrib. Dim 2 | Cos2 Dim 2 |
|---|---:|---:|---:|
| Oxigeno disuelto | 0,854 | 41,015 | 0,730 |
| Conductividad electrica | -0,766 | 32,983 | 0,587 |
| Turbiedad | 0,430 | 10,381 | 0,185 |
| DQO | -0,309 | 5,355 | 0,095 |
| Solidos suspendidos totales | 0,307 | 5,288 | 0,094 |
| DBO | -0,267 | 3,992 | 0,071 |
| Fosforo total | 0,133 | 0,986 | 0,018 |

En sintesis, los cosenos cuadrados indican que los solidos suspendidos y la turbiedad estan bien representados por la Dim 1, mientras que oxigeno disuelto y conductividad electrica estan mejor representados por la Dim 2. Esta separacion respalda que el fenomeno no es unidimensional: existe un eje de carga particulada/organica y otro eje de condicion fisico-quimica asociada a oxigenacion y conductividad.

## 9. Construccion de indice

La Dim 1 explica **31,57 %** de la varianza total y presenta cargas positivas en 6 de las 7 variables activas. Ademas, las variables con mayor contribucion en esta dimension tienen una interpretacion ambiental coherente: solidos suspendidos, turbiedad, DBO, DQO y fosforo. Esta coherencia permite construir un indicador ordenado por la posicion de los individuos sobre la Dim 1.

Por lo anterior, **si es posible construir un indice parcial basado en la Dim 1**, pero no se recomienda interpretarlo como un indice global de calidad del agua. La razon es que la Dim 2 contiene informacion ambiental importante, especialmente sobre oxigeno disuelto y conductividad electrica, que no queda completamente representada por la Dim 1. En consecuencia, el indice se interpreta como **indice parcial de carga contaminante/particulada**: valores altos indican mayor carga relativa, no necesariamente peor calidad integral en todos los criterios ambientales.

El indice construido se normalizo en escala 0-100 a partir de la coordenada factorial de cada individuo en la Dim 1:

`Indice_PC1_0_100 = 100 * (PC1 - min(PC1)) / (max(PC1) - min(PC1))`

Valores cercanos a 100 indican mayor carga contaminante/particulada segun la estructura capturada por la Dim 1.

Los mayores valores individuales del indice fueron:

| Individuo | Estacion | PC1 | Indice |
|---|---|---:|---:|
| 2010_LA VICTORIA | LA VICTORIA | 5,104 | 100,000 |
| 1994_PASO DEL COMERCIO | PASO DEL COMERCIO | 5,086 | 99,825 |
| 2010_ANACARO | ANACARO | 4,887 | 97,906 |
| 2010_MEDIACANOA | MEDIACANOA | 4,819 | 97,245 |
| 2010_PASO DEL COMERCIO | PASO DEL COMERCIO | 4,734 | 96,422 |
| 2010_PUERTO ISAACS | PUERTO ISAACS | 4,691 | 96,009 |
| 1990_ANTES INTERCEPTOR SUR | ANTES INTERCEPTOR SUR | 4,575 | 94,881 |
| 2010_YOTOCO | YOTOCO | 4,478 | 93,942 |
| 2010_PUENTE LA VIRGINIA | PUENTE LA VIRGINIA | 4,458 | 93,750 |
| 2010_PASO DE LA TORRE | PASO DE LA TORRE | 4,315 | 92,371 |

Al agrupar por estacion, las estaciones con mayor indice promedio fueron:

| Estacion | n mediciones | Indice promedio | Indice maximo |
|---|---:|---:|---:|
| ANACARO | 92 | 57,6 | 97,9 |
| PUENTE LA VIRGINIA | 89 | 57,5 | 93,8 |
| LA VICTORIA | 90 | 57,4 | 100,0 |
| VIJES | 88 | 56,6 | 88,2 |
| PUENTE GUAYABAL | 92 | 56,6 | 88,6 |
| RIOFRIO | 90 | 56,3 | 91,7 |
| YOTOCO | 87 | 56,0 | 93,9 |
| MEDIACANOA | 100 | 55,9 | 97,2 |
| PASO DE LA TORRE | 87 | 53,9 | 92,4 |
| PASO DEL COMERCIO | 96 | 53,4 | 99,8 |

## 10. Hallazgos principales

1. La base de datos presenta alta heterogeneidad y asimetria positiva en las variables fisico-quimicas analizadas, lo que justifico el uso de transformacion logaritmica.
2. La correlacion mas fuerte se encontro entre turbiedad y solidos suspendidos totales, evidenciando una dimension clara de carga particulada.
3. El ACP retuvo tres componentes segun el criterio de Kaiser, explicando el 77,15 % de la variabilidad total.
4. El plano Dim 1-Dim 2 explico 57,00 % de la variabilidad, suficiente para interpretar patrones generales de individuos y variables.
5. La Dim 1 representa principalmente carga contaminante/particulada, mientras que la Dim 2 refleja un contraste entre oxigeno disuelto y conductividad electrica.
6. Se identificaron observaciones extremas, especialmente en estaciones y anos como JUANCHITO 1993, MEDIACANOA 2010, PASO DEL COMERCIO 2010 y PUERTO ISAACS 2010.
7. Es posible construir un indice parcial de carga contaminante basado en PC1, pero no un indice global de calidad del agua, porque PC2 contiene informacion ambiental relevante no resumida por PC1.
8. Las estaciones con mayores promedios del indice parcial fueron ANACARO, PUENTE LA VIRGINIA, LA VICTORIA, VIJES y PUENTE GUAYABAL.

## 11. Conclusiones

El Analisis de Componentes Principales permitio resumir adecuadamente la estructura multivariada de las variables fisico-quimicas del Rio Cauca. La primera dimension sintetiza un gradiente de contaminacion asociado a solidos suspendidos, turbiedad, DBO, DQO y fosforo total. La segunda dimension complementa la interpretacion al representar principalmente el contraste entre oxigeno disuelto y conductividad electrica.

Los resultados muestran que la calidad del agua no puede describirse de manera completa con un unico eje factorial. Sin embargo, la Dim 1 ofrece una base coherente para construir un indice parcial de carga contaminante/particulada, util para ordenar observaciones y estaciones segun su perfil relativo. Este indice debe interpretarse con cautela y acompanarse de la lectura de la Dim 2 para no perder informacion ambiental importante.

En terminos aplicados, el ACP permitio identificar variables dominantes, estaciones con mayor carga relativa y observaciones extremas que podrian ser objeto de revision ambiental o analisis complementario.
