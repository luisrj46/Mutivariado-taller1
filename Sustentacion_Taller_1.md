# Sustentacion Taller 1. ACP calidad del agua del Rio Cauca

Duracion maxima: 10 minutos

## Diapositiva 1. Titulo

**Analisis de Componentes Principales aplicado a calidad del agua del Rio Cauca**

Buenos dias. En esta sustentacion presentamos la aplicacion de ACP sobre una base real de calidad del agua del Rio Cauca. El objetivo fue resumir la informacion fisico-quimica, interpretar los principales gradientes ambientales, identificar observaciones atipicas y evaluar la construccion de un indice.

Tiempo sugerido: 40 segundos.

## Diapositiva 2. Datos y preparacion

La base original tenia 2368 registros y 56 variables. Se limpiaron nombres, se corrigieron formatos numericos y se construyo el identificador `anio_estacion`, para que cada individuo representara una combinacion entre ano y estacion de monitoreo.

Tambien se revisaron faltantes. Algunas variables tenian 100 % de ausencia, asi que el analisis se enfoco en siete variables activas con relevancia ambiental y mejor disponibilidad.

Tiempo sugerido: 1 minuto.

## Diapositiva 3. Variables activas

Las variables usadas fueron turbiedad, solidos suspendidos totales, DBO, DQO, oxigeno disuelto, conductividad electrica y fosforo total.

Estas variables permiten capturar carga particulada, contaminacion organica/quimica, oxigenacion, presencia de iones y nutrientes. Como todas presentaban asimetria positiva fuerte, se aplico transformacion `log1p` y luego estandarizacion antes del ACP.

Tiempo sugerido: 1 minuto.

## Diapositiva 4. Exploracion descriptiva y correlaciones

En la exploracion descriptiva se observo alta variabilidad. Por ejemplo, DBO y fosforo total tuvieron coeficientes de variacion muy altos.

La correlacion mas importante fue entre turbiedad y solidos suspendidos totales, con r = 0,80. Tambien se encontro una relacion entre DBO y fosforo total, con r = 0,60. El oxigeno disuelto se relaciono negativamente con conductividad electrica, r = -0,54.

Mensaje clave: los datos muestran una estructura multivariada real, por eso el ACP es apropiado.

Tiempo sugerido: 1 minuto.

## Diapositiva 5. Varianza explicada

El ACP se realizo sobre datos transformados y estandarizados. Con el criterio de Kaiser se retuvieron tres componentes, porque tuvieron valores propios mayores que 1.

La Dim 1 explico 31,57 %, la Dim 2 explico 25,43 % y la Dim 3 explico 20,15 %. En conjunto, las tres dimensiones explicaron 77,15 % de la variabilidad total. El plano 1-2 explico aproximadamente 57 %.

Tiempo sugerido: 1 minuto.

## Diapositiva 6. Nube de individuos

La nube de individuos muestra observaciones espacio-temporales. Los puntos cercanos al origen tienen perfiles mas promedio, mientras que los puntos alejados representan perfiles mas diferenciados.

Los individuos mejor representados en el plano incluyeron 2013_ANTES SUAREZ, 2011_PASO DEL COMERCIO, 1997_PUENTE HORMIGUERO, 1998_ANTES RIO OVEJAS y 2000_PASO DE LA BOLSA. Estos tienen cosenos cuadrados altos, por lo que su posicion en el plano es confiable.

Tiempo sugerido: 1 minuto.

## Diapositiva 7. Circulo de correlaciones

El circulo de correlaciones permitio interpretar los ejes.

La Dim 1 esta dominada por solidos suspendidos, turbiedad, DBO, DQO y fosforo total. Por eso la interpretamos como un gradiente de carga contaminante y particulada.

La Dim 2 esta dominada por oxigeno disuelto y conductividad electrica, en sentidos opuestos. Esto sugiere un contraste entre oxigenacion y carga ionica/conductiva.

Tiempo sugerido: 1 minuto.

## Diapositiva 8. Biplot y atipicos

El biplot integra individuos y variables. Las observaciones ubicadas en la direccion de una variable tienden a tener valores relativamente altos en esa variable.

Los posibles atipicos se identificaron por distancia al origen. Entre los mas destacados estuvieron 1993_JUANCHITO, 2010_MEDIACANOA, 2010_PASO DEL COMERCIO, 2010_PUERTO ISAACS y 2010_JUANCHITO.

Es importante aclarar que no se eliminan automaticamente: pueden representar eventos reales o condiciones ambientales particulares.

Tiempo sugerido: 1 minuto.

## Diapositiva 9. Indice parcial

La pregunta era si se podia construir un indice. La respuesta es si, pero como indice parcial, no como indice global de calidad del agua.

La razon es que PC1 explica 31,57 % y tiene una interpretacion coherente de carga contaminante/particulada. Sin embargo, PC2 contiene informacion importante sobre oxigeno disuelto y conductividad. Entonces usar solo PC1 perderia parte de la calidad ambiental.

El indice se normalizo de 0 a 100. Valores altos indican mayor carga contaminante/particulada segun PC1. Las estaciones con mayor promedio fueron ANACARO, PUENTE LA VIRGINIA, LA VICTORIA, VIJES y PUENTE GUAYABAL.

Tiempo sugerido: 1 minuto.

## Diapositiva 10. Conclusiones

Como conclusiones principales:

El ACP permitio reducir siete variables fisico-quimicas a dimensiones interpretables.

La Dim 1 representa carga contaminante y particulada.

La Dim 2 complementa la interpretacion con oxigeno disuelto y conductividad electrica.

Se identificaron observaciones extremas que pueden ser relevantes ambientalmente.

Se construyo un indice parcial basado en PC1, util para ordenar observaciones y estaciones, pero no suficiente para representar toda la calidad del agua.

Tiempo sugerido: 1 minuto.

## Preguntas probables del profesor y respuestas breves

**Por que hicieron transformacion log1p?**  
Porque todas las variables seleccionadas presentaban asimetria positiva severa y valores extremos. La transformacion reduce el peso excesivo de esos valores y mejora la lectura del ACP.

**Por que estandarizaron las variables?**  
Porque estaban en unidades diferentes. Sin estandarizacion, las variables con mayor escala numerica dominarian los componentes.

**Por que no construyeron un indice global?**  
Porque PC1 no recoge toda la estructura ambiental. PC2 contiene informacion relevante de oxigeno disuelto y conductividad, por lo que un indice unico basado solo en PC1 seria incompleto.

**Que significa un atipico en el ACP?**  
Es una observacion alejada del centro del plano factorial. No necesariamente es un error; puede ser una condicion ambiental extrema o un evento real.

**Cual es el principal hallazgo?**  
Que el comportamiento multivariado se organiza principalmente en dos lecturas: una de carga contaminante/particulada y otra de oxigenacion frente a conductividad.

