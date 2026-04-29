# Sustentacion Taller 1. ACP calidad del agua del Rio Cauca

Duracion maxima sugerida: 10 minutos  
Base: Informe final `Informe_Taller_1.md` / `Informe_Taller_1.tex`

**Integrantes:**  
- JHONATAN ANDRES TAPIA CORDOBA  
- JORGE ANDRES JARAMILLO NEME  
- LUIS FERNANDO MEZA RAMREZ  

## Diapositiva 1. Titulo

**Analisis de Componentes Principales aplicado a calidad del agua del Rio Cauca**

Buenos dias. En esta sustentacion presentamos una aplicacion de Analisis de Componentes Principales sobre variables fisico-quimicas de calidad del agua del Rio Cauca. El objetivo fue resumir la informacion multivariada, interpretar los principales gradientes ambientales, identificar observaciones atipicas y evaluar si era posible construir un indice.

**Importante:** El ACP permite pasar de varias variables correlacionadas a pocas dimensiones interpretables.

Tiempo sugerido: 40 segundos.

## Diapositiva 2. Datos y preparacion

La base original contenia **2368 registros y 56 variables**. Primero se limpiaron nombres de columnas, se corrigieron formatos numericos y se normalizaron valores con coma decimal o notacion cientifica escrita como `*10E`.

Tambien se construyo el identificador `anio_estacion`, que combina el ano de muestreo y la estacion. Esto permite que cada individuo represente una observacion espacio-temporal, no solo una estacion agregada.

Durante la auditoria se encontraron variables con 100 % de valores faltantes, por lo que fueron descartadas del ACP.

Tiempo sugerido: 1 minuto.

## Diapositiva 3. Variables activas y tratamiento

Se seleccionaron siete variables activas:

- Turbiedad.
- Solidos suspendidos totales.
- DBO.
- DQO.
- Oxigeno disuelto.
- Conductividad electrica.
- Fosforo total.

Estas variables capturan carga particulada, contaminacion organica y quimica, oxigenacion, presencia de iones y nutrientes.

Todas presentaron asimetria positiva severa, por eso se aplico transformacion `log1p`. Luego se estandarizaron porque las variables estaban en unidades diferentes. La matriz final usada en el ACP quedo con **1475 observaciones**, equivalentes al **62,29 %** de la base de analisis.

Tiempo sugerido: 1 minuto.

## Diapositiva 4. Estadisticas descriptivas y correlaciones

La exploracion descriptiva mostro alta heterogeneidad. Los coeficientes de variacion fueron especialmente altos en DBO, fosforo total y oxigeno disuelto.

En la matriz de correlacion transformada se destacaron tres relaciones:

- Turbiedad y solidos suspendidos totales: **r = 0,80**.
- DBO y fosforo total: **r = 0,60**.
- Oxigeno disuelto y conductividad electrica: **r = -0,54**.

Esto sugiere que los datos tienen estructura multivariada: una dimension de carga particulada/organica y otra asociada al contraste entre oxigenacion y conductividad.

![Distribuciones fisico-quimicas grupo A](Graficos%20de%20resultados/distribuciones%20fisico-quimica_grupo_A.png)

![Distribuciones fisico-quimicas grupo B](Graficos%20de%20resultados/distribuciones%20fisico-quimica_grupo_B.png)

![Matriz de correlacion](Graficos%20de%20resultados/Matriz%20de%20correlacion:%20Espacion%20de%20variable.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 5. Varianza explicada por el ACP

El ACP se realizo sobre variables transformadas y estandarizadas. Segun el criterio de Kaiser, se retuvieron **tres componentes** con valores propios mayores que 1.

Resultados principales:

- Dim 1: **31,57 %** de la varianza.
- Dim 2: **25,43 %** de la varianza.
- Dim 3: **20,15 %** de la varianza.
- Acumulado en tres dimensiones: **77,15 %**.
- Plano 1-2: **57,00 %**.

El plano 1-2 es util para interpretar graficamente, aunque existe una tercera dimension con informacion adicional.

![Sedimentacion de varianza](Graficos%20de%20resultados/Sedimentacion%20de%20varianza.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 6. Nube de individuos

La nube de individuos muestra la posicion de las observaciones espacio-temporales en el plano factorial 1-2.

Los puntos cerca del origen representan perfiles mas promedio. Los puntos alejados representan perfiles fisico-quimicos mas diferenciados.

Entre los individuos mejor representados en el plano, por mayor coseno cuadrado, estuvieron:

- 2013_ANTES SUAREZ.
- 2011_PASO DEL COMERCIO.
- 1997_PUENTE HORMIGUERO.
- 1998_ANTES RIO OVEJAS.
- 2000_PASO DE LA BOLSA.

Su posicion se puede interpretar con mayor confianza porque tienen cosenos cuadrados altos.

![Nube de individuos](Graficos%20de%20resultados/Nube%20de%20individuos.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 7. Circulo de correlaciones

El circulo de correlaciones permite interpretar que representa cada eje.

La **Dim 1** esta dominada por:

- Solidos suspendidos totales.
- Turbiedad.
- DBO.
- DQO.
- Fosforo total.

Por eso se interpreta como un **gradiente de carga contaminante, organica y particulada**.

La **Dim 2** esta dominada por oxigeno disuelto y conductividad electrica, con signos opuestos. Por eso representa un **contraste entre oxigenacion e influencia ionica/conductiva**.

![Circulo de correlaciones](Graficos%20de%20resultados/Circulos%20de%20correlaciones%20Plano%201-2.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 8. Biplot y datos atipicos

El biplot integra individuos y variables en una misma representacion. Las observaciones ubicadas en la direccion de una variable tienden a presentar valores relativamente altos en esa variable.

Para identificar posibles atipicos se uso la distancia al origen en el plano factorial. Los casos mas alejados fueron:

- 1993_JUANCHITO.
- 2010_MEDIACANOA.
- 2010_PASO DEL COMERCIO.
- 2010_PUERTO ISAACS.
- 2010_JUANCHITO.
- 2010_YOTOCO.

Estos registros no se deben eliminar automaticamente. Pueden representar eventos reales de contaminacion, cambios hidrologicos o condiciones ambientales particulares.

![Biplot](Graficos%20de%20resultados/Relacion%20Dual%20individuos%20-%20variables.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 9. Sintesis con contribuciones y cosenos

El aporte promedio esperado por variable en cada dimension es **14,29 %**.

En la Dim 1, las mayores contribuciones fueron:

- Solidos suspendidos totales: **32,36 %**.
- Turbiedad: **23,45 %**.
- DBO: **15,71 %**.

Estas variables tambien tienen buenos cosenos cuadrados en la Dim 1, especialmente solidos suspendidos y turbiedad, lo que confirma que ese eje representa carga particulada y contaminante.

En la Dim 2 dominaron:

- Oxigeno disuelto: **41,02 %**.
- Conductividad electrica: **32,98 %**.

Esto confirma que la Dim 2 aporta una lectura distinta y complementaria.

Tiempo sugerido: 1 minuto.

## Diapositiva 10. Indice parcial

La pregunta del taller era si era posible construir un indice. La respuesta es: **si, pero como indice parcial**, no como indice global de calidad del agua.

La Dim 1 explica **31,57 %** y tiene una interpretacion ambiental coherente: carga contaminante/particulada. Por eso se construyo un indice normalizado de 0 a 100 a partir de la coordenada PC1.

Valores cercanos a 100 indican mayor carga contaminante/particulada segun PC1.

Los mayores valores individuales fueron:

- 2010_LA VICTORIA.
- 1994_PASO DEL COMERCIO.
- 2010_ANACARO.
- 2010_MEDIACANOA.
- 2010_PASO DEL COMERCIO.

Las estaciones con mayor indice promedio fueron ANACARO, PUENTE LA VIRGINIA, LA VICTORIA, VIJES y PUENTE GUAYABAL.

Tiempo sugerido: 1 minuto.

## Diapositiva 11. Conclusiones

Como conclusiones principales:

1. El ACP permitio resumir siete variables fisico-quimicas en dimensiones interpretables.
2. La Dim 1 representa carga contaminante y particulada.
3. La Dim 2 complementa la lectura mediante el contraste entre oxigeno disuelto y conductividad electrica.
4. Se identificaron observaciones extremas que pueden ser ambientalmente relevantes.
5. Si es posible construir un indice, pero debe interpretarse como indice parcial de carga contaminante, no como indice global de calidad del agua.

El principal aporte del ACP fue mostrar que la calidad del agua del Rio Cauca no se resume completamente en un solo eje; se requiere leer conjuntamente la carga contaminante y las condiciones de oxigenacion/conductividad.

Tiempo sugerido: 1 minuto.

## Preguntas probables del profesor y respuestas breves

**Por que aplicaron transformacion log1p?**  
Porque todas las variables seleccionadas presentaban asimetria positiva severa y valores extremos. La transformacion reduce el peso excesivo de esos valores y mejora la lectura factorial.

**Por que estandarizaron las variables?**  
Porque estaban medidas en unidades distintas. Sin estandarizacion, las variables con mayor escala numerica podrian dominar artificialmente el ACP.

**Por que se retuvieron tres componentes?**  
Porque segun el criterio de Kaiser, tres componentes tuvieron valores propios mayores que 1. En conjunto explicaron el 77,15 % de la variabilidad total.

**Por que el indice no es global?**  
Porque PC1 resume principalmente carga contaminante/particulada, pero PC2 contiene informacion importante sobre oxigeno disuelto y conductividad. Usar solo PC1 perderia esa dimension ambiental.

**Que significa un atipico en el ACP?**  
Es una observacion alejada del centro del plano factorial. No necesariamente es un error; puede ser una condicion ambiental extrema o un evento real.

**Cual es el hallazgo mas importante?**  
Que la estructura multivariada del Rio Cauca se organiza principalmente en dos lecturas: carga contaminante/particulada y contraste entre oxigenacion y conductividad.
