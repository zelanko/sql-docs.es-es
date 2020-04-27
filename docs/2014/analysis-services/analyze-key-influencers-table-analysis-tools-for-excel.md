---
title: Analizar influenciadores clave (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- key influencers
- factor analysis
ms.assetid: 54d7b4ce-7b79-407a-985c-aa655ad19280
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df6622abc3a507d917aefd2a8a5a1bf9505a2622
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66062258"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>Analizar influenciadores clave (Herramientas de análisis de tabla para Excel)
  ![Botón Analizar influenciadores clave de la cinta](media/tat-aki.gif "Botón Analizar influenciadores clave de la cinta")  
  
 Con la herramienta **analizar influenciadores clave** , elija una columna que contenga un resultado de destino y el algoritmo determinará qué factores tenían la influencia más fuerte en el resultado.  
  
 La herramienta crea nuevas tablas de datos que informan sobre los factores asociados con cada resultado e ilustra gráficamente la probabilidad de la relación. Puede filtrar las tablas por factores y resultados diferentes para explorar los resultados de forma más minuciosa.  
  
 También puede seleccionar un par de resultados posibles y compararlos. Por ejemplo, puede comparar grupos de consumidores para determinar los posibles factores que influyen en la toma de decisiones.  
  
## <a name="using-the-analyze-key-influencers-tool"></a>Usar la herramienta Analizar influenciadores clave  
  
1.  Abra una tabla de datos de Excel.  
  
2.  En **herramientas de tabla**, en la cinta de opciones **analizar** , haga clic en **analizar influenciadores clave.**  
  
3.  Seleccione la columna individual que constituye el objetivo del análisis.  
  
4.  Opcionalmente, haga clic en **elegir las columnas que se van a usar para el análisis**. En el cuadro de diálogo **selección avanzada de columnas** , elija las columnas que tengan más probabilidades de contener datos relevantes. Para mejorar el rendimiento y la precisión, anule la selección de las columnas que contengan identificadores o nombres, que no son importantes para el análisis de patrones. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **selección avanzada de columnas** .  
  
5.  Haga clic en **Ejecutar**.  
  
     La herramienta **analizar influenciadores clave** realiza un análisis de los datos para determinar la configuración óptima y establece todos los parámetros de forma automática.  
  
6.  Si no se detecta ningún modelo, el asistente crea una nueva hoja de cálculo que contiene una descripción del problema.  
  
7.  Si se detectan patrones, el asistente crea un informe en una nueva hoja de cálculo que muestra los patrones. El informe se denomina **influenciadores clave para \<>de columna **. Puede personalizar el informe como se describe en el procedimiento siguiente.  
  
#### <a name="create-a-custom-report"></a>Creación de un informe personalizado  
  
1.  En el cuadro de diálogo **distinción basada en influenciadores clave** , elija los dos valores que desea comparar seleccionándolos en las listas desplegables **valor 1** y **valor 2** . Por ejemplo, puede comparar los compradores con los no compradores.  
  
2.  Haga clic en **Agregar Informe**.  
  
     El asistente crea una nueva hoja de cálculo y agrega una tabla por cada par de comparaciones de factores clave.  
  
3.  Cuando haya terminado de realizar comparaciones, haga clic en **cerrar**.  
  
## <a name="understanding-the-key-influencers-report"></a>Descripción del informe de influenciadores clave  
 Una vez creado el modelo de datos, la herramienta **analizar influenciadores clave** crea informes que le ayudan a explorar y a comparar los influenciadores clave.  
  
-   El informe del lado izquierdo es el que se ha generado de forma predeterminada. Muestra los predictores más eficaces de la columna de resultados (la variable dependiente).  
  
-   El informe del lado derecho es opcional y puede crearlo comparando dos valores específicos de resultados. Este informe compara a los compradores y a los no compradores.  
  
-   Tenga en cuenta que se agrega una nueva hoja de cálculo para cada informe que cree. Puede mover las tablas una vez creadas; las colocamos en paralelo para la comparación.  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **Impacto relativo**  
 La barra sombreada en el primer informe indica la solidez de la asociación de este atributo con el resultado.  
  
 La longitud de la barra indica la probabilidad de que el factor contribuya al resultado; por tanto, cuanto más larga sea la barra sombreada, más fuerte es la asociación.  
  
 **Favorece**  
 En el segundo informe, los valores de destino que se comparan se muestran en dos columnas, con los factores relacionados enumerados en orden de confianza descendente.  
  
-   La barra **azul** muestra los atributos que contribuyen al resultado, "no" (= no adquirió).  
  
-   La barra **roja** muestra los atributos que contribuyen al resultado, "sí" (= compra una bicicleta).  
  
 Los colores de la barra de sombreado son arbitrarios. Puede cambiar estos colores estableciendo las opciones para el diseño de la tabla en Excel.  
  
 En un informe que contrasta dos valores, el segundo informe clasifica los influenciadores clave según el impacto que tienen en los valores deseados.  
  
 Puesto que todos los gráficos se basan en las tablas de Excel, puede filtrar y ordenar para centrarse en resultados o factores específicos.  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>Más información acerca de la herramienta Analizar influenciadores clave  
 Cuando la herramienta **analizar influenciadores clave** analiza los datos, hace lo siguiente:  
  
-   Crea una estructura de datos que almacena información clave sobre la distribución de los datos.  
  
-   Crea un modelo mediante el algoritmo Bayes Naive de Microsoft.  
  
-   Crea predicciones que ponen en correlación cada columna de datos con el resultado especificado.  
  
-   Utiliza la puntuación de confianza para cada una de las predicciones a fin de identificar los factores que son más influyentes al generar el resultado pretendido.  
  
-   Crea un informe que describe los influenciadores clave, ordenados por las puntuaciones de confianza.  
  
### <a name="requirements"></a>Requisitos  
 Si la columna de destino contiene valores numéricos continuos, la herramienta segmenta automáticamente los valores numéricos en grupos. Estas agrupaciones representan clústeres de casos que tienen características similares. Sin embargo, los valores numéricos podrían no estar divididos en grupos fáciles de usar. Por ejemplo, el informe puede contener una agrupación como "\<12,85701", mientras que los usuarios de informes normalmente desean ver las agrupaciones que utilizan números enteros, como 10-19, 20-29, etc.  
  
 Si desea agrupar los datos numéricos de otra forma, debe segmentar los datos de la forma deseada antes de crear el análisis. Por ejemplo, puede usar la herramienta cambiar [etiquetas](relabel-sql-server-data-mining-add-ins.md) del cliente de minería de datos para Excel para crear una nueva etiqueta de agrupación en una columna independiente y, a continuación, utilizar solo esa nueva columna en el análisis.  
  
### <a name="related-tools"></a>Herramientas relacionadas  
 La cinta de opciones **minería de datos** proporciona herramientas más avanzadas, incluida la capacidad de personalizar modelos de minería de datos  
  
 Si guarda el modelo mediante la herramienta **analizar influenciadores clave** , puede usar el cliente de minería de datos para examinar el modelo y explorar las relaciones con más detalle. Para obtener más información, vea [examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md). También puede usar Microsoft Office Visio para crear gráficos y diagramas que muestren las relaciones como clúster o como redes de dependencias. Para obtener más información, vea [solucionar problemas de diagramas de minería de datos de Visio &#40;SQL Server complementos de minería de datos&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md).  
  
> [!NOTE]  
>  Los modelos creados cuando se usan las Herramientas de análisis de tabla se eliminan al cerrar la hoja de cálculo o terminar la conexión con el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Por tanto, solo puede examinar los modelos mientras la conexión permanezca abierta. No puede representar los modelos en Visio si cierra la conexión o cierra la hoja de cálculo.  
  
 Para obtener más información acerca del algoritmo usado por la herramienta **analizar influenciadores clave** , vea el tema sobre el algoritmo Bayes Naive de Microsoft en libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)   
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)  
  
  
