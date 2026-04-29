# Sustentacion Taller 1. ACP calidad del agua del Rio Cauca

Duracion maxima sugerida: 10 minutos  
Base: Informe final `Informe_Taller_1.md` / `Informe_Taller_1.tex`

**Integrantes:**  
- JHONATAN ANDRES TAPIA CORDOBA  
- JORGE ANDRES JARAMILLO NEME  
- LUIS FERNANDO MEZA RAMREZ  

## Diapositiva 1. Titulo

**Analisis de Componentes Principales aplicado a calidad del agua del Rio Cauca**

Buenos dias. En esta sustentacion presentamos una aplicacion de ACP sobre variables fisico-quimicas de calidad del agua del Rio Cauca. El objetivo fue resumir la informacion multivariada, interpretar los principales gradientes ambientales, identificar observaciones atipicas y evaluar si era posible construir un indice.

Tiempo sugerido: 40 segundos.

## Diapositiva 2. Datos y preparacion

La base original contenia **2368 registros y 56 variables**. Se limpiaron nombres, se corrigieron formatos numericos y se descartaron variables sin informacion util.

Se seleccionaron siete variables activas: turbiedad, solidos suspendidos totales, DBO, DQO, oxigeno disuelto, conductividad electrica y fosforo total.

Como las variables tenian asimetria positiva severa y unidades diferentes, se aplico transformacion `log1p` y luego estandarizacion. La matriz final del ACP quedo con **1475 observaciones**, equivalentes al **62,29 %** de la base de analisis.

Tiempo sugerido: 1 minuto.

## Diapositiva 3. Exploracion y correlaciones

La exploracion mostro alta heterogeneidad, especialmente en DBO, fosforo total y oxigeno disuelto.

Las correlaciones mas importantes fueron:

- Turbiedad y solidos suspendidos totales: **r = 0,80**.
- DBO y fosforo total: **r = 0,60**.
- Oxigeno disuelto y conductividad electrica: **r = -0,54**.

Estas relaciones justifican el ACP porque muestran una estructura multivariada: una dimension de carga particulada/organica y otra asociada al contraste entre oxigenacion y conductividad.

![Matriz de correlacion](Graficos%20de%20resultados/Matriz%20de%20correlacion:%20Espacion%20de%20variable.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 4. Varianza explicada

Segun el criterio de Kaiser, se retuvieron **tres componentes** con valores propios mayores que 1.

- Dim 1: **31,57 %**.
- Dim 2: **25,43 %**.
- Dim 3: **20,15 %**.
- Acumulado en tres dimensiones: **77,15 %**.
- Plano 1-2: **57,00 %**.

El plano 1-2 permite interpretar graficamente los patrones principales, aunque la tercera dimension tambien conserva informacion relevante.

![Sedimentacion de varianza](Graficos%20de%20resultados/Sedimentacion%20de%20varianza.png)

Tiempo sugerido: 1 minuto.

## Diapositiva 5. Interpretacion de los ejes

El circulo de correlaciones permite interpretar los dos primeros componentes.

La **Dim 1** esta dominada por solidos suspendidos, turbiedad, DBO, DQO y fosforo total. Por eso se interpreta como un **gradiente de carga contaminante, organica y particulada**.

La **Dim 2** esta dominada por oxigeno disuelto y conductividad electrica, con signos opuestos. Por eso representa un **contraste entre oxigenacion e influencia ionica/conductiva**.

![Circulo de correlaciones](Graficos%20de%20resultados/Circulos%20de%20correlaciones%20Plano%201-2.png)

Tiempo sugerido: 1 minuto 20 segundos.

## Diapositiva 6. Nube de individuos y biplot

La nube de individuos muestra observaciones espacio-temporales. Los puntos cercanos al origen tienen perfiles mas promedio; los puntos alejados tienen perfiles fisico-quimicos diferenciados.

El biplot integra individuos y variables. Las observaciones ubicadas en la direccion de una variable tienden a presentar valores relativamente altos en esa variable.

![Biplot](Graficos%20de%20resultados/Relacion%20Dual%20individuos%20-%20variables.png)

Tiempo sugerido: 1 minuto 20 segundos.

## Diapositiva 7. Datos atipicos y aportes

Los posibles atipicos se identificaron por mayor distancia al origen en el plano factorial. Entre los casos mas destacados estuvieron:

- 1993_JUANCHITO.
- 2010_MEDIACANOA.
- 2010_PASO DEL COMERCIO.
- 2010_PUERTO ISAACS.
- 2010_JUANCHITO.

No se deben eliminar automaticamente: pueden representar eventos reales de contaminacion o condiciones ambientales particulares.

En contribuciones, la Dim 1 estuvo dominada por solidos suspendidos (**32,36 %**), turbiedad (**23,45 %**) y DBO (**15,71 %**). La Dim 2 estuvo dominada por oxigeno disuelto (**41,02 %**) y conductividad electrica (**32,98 %**).

Tiempo sugerido: 1 minuto 20 segundos.

## Diapositiva 8. Indice parcial

Si es posible construir un indice, pero debe interpretarse como **indice parcial de carga contaminante/particulada**, no como indice global de calidad del agua.

La razon es que PC1 explica **31,57 %** y resume principalmente carga contaminante, mientras PC2 conserva informacion ambiental importante sobre oxigeno disuelto y conductividad.

El indice se normalizo de 0 a 100 a partir de PC1. Valores cercanos a 100 indican mayor carga contaminante/particulada.

Mayores valores individuales: 2010_LA VICTORIA, 1994_PASO DEL COMERCIO, 2010_ANACARO, 2010_MEDIACANOA y 2010_PASO DEL COMERCIO.

Mayores promedios por estacion: ANACARO, PUENTE LA VIRGINIA, LA VICTORIA, VIJES y PUENTE GUAYABAL.

Tiempo sugerido: 1 minuto 20 segundos.

## Diapositiva 9. Conclusiones

1. El ACP redujo siete variables fisico-quimicas a dimensiones interpretables.
2. La Dim 1 representa carga contaminante y particulada.
3. La Dim 2 complementa la lectura mediante oxigeno disuelto y conductividad electrica.
4. Se identificaron observaciones extremas que pueden ser ambientalmente relevantes.
5. El indice construido es util para ordenar observaciones y estaciones, pero debe leerse como indice parcial.

Mensaje final: la calidad del agua del Rio Cauca no se resume completamente en un solo eje; debe leerse conjuntamente desde la carga contaminante y las condiciones de oxigenacion/conductividad.

Tiempo sugerido: 1 minuto.

## Preguntas probables

**Por que aplicaron log1p?**  
Porque habia asimetria positiva severa y valores extremos.

**Por que estandarizaron?**  
Porque las variables estaban en unidades diferentes.

**Por que tres componentes?**  
Porque tres valores propios fueron mayores que 1 y explicaron 77,15 %.

**Por que el indice no es global?**  
Porque PC2 contiene informacion ambiental relevante que PC1 no resume.
