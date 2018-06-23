---
title: Elegir un modelo | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining algorithms
- mining models
- mining structures
- data mining models
- data mining structures
ms.assetid: 444bbf9c-cec8-460e-881d-38784fb146fa
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 60cba88e3674e72fc824edf450bdbd87ae4e4aea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204303"
---
# <a name="choosing-a-model"></a>Elegir un modelo
  **Algoritmo de minería de datos:** la minería de datos *algoritmo* es el mecanismo que crea patrones a partir de los datos. El algoritmo define cómo se cuentan los datos, cómo se derivan las relaciones, y cómo se guardan los patrones. La selección de un algoritmo depende en parte del tipo de datos que se desea analizar. Por ejemplo, algunos algoritmos solo funcionan con números continuos, mientras que otros funcionan mejor con un número limitado de valores diferentes.  
  
 **Modelo de minería de datos:** el resultado del análisis de datos mediante un algoritmo se guarda en un *modelo de minería de datos*. Un modelo de minería de datos es una colección de reglas, estadísticas y patrones. El *contenido* del modelo de minería de datos depende del algoritmo que utiliza para procesar los datos, pero puede incluir lo siguiente:  
  
-   Reglas if-then que describen cómo se agrupan los productos en una transacción.  
  
-   Un árbol de decisión que realiza un seguimiento de las rutas que llevan a un resultado, con las probabilidades de que se repita cada una de las rutas.  
  
-   Un modelo matemático con ecuaciones para el modelo en su conjunto o para los segmentos del modelo.  
  
-   Colecciones de elementos similares (denominado *clústeres* o *segmentos*) que se definen las características que comparten y una puntuación de similitud.  
  
-   *Nodos* en una red, conectada mediante *bordes*. Los nodos representan elementos o grupos de elementos. Los bordes se puntúan de acuerdo con la importancia de las relaciones existentes entre los nodos.  
  
 **Con el modelo:** después de crear un modelo, puede utilizar los visores proporcionados para explorarlo o puede crear una consulta en el modelo. Las consultas se pueden usar para:  
  
-   Predecir valores futuros.  
  
-   Generar un conjunto de productos relacionados o recomendados.  
  
-   Devolver reglas, patrones o fórmulas del modelo.  
  
-   Obtener metadatos del modelo.  
  
-   Proporcionar probabilidades y sustentar puntuaciones de todas o algunas de las predicciones.  
  
## <a name="types-of-machine-learning-algorithms"></a>Tipos de algoritmos de aprendizaje automático  
 Dado que los distintos tipos de algoritmos usan datos de diferentes formas, al crear un modelo debe seleccionar el algoritmo adecuado para sus objetivos y para los datos que desea analizar.  
  
 Los Complementos de minería de datos para Excel incluyen los siguientes tipos genéricos de algoritmos:  
  
-   *Algoritmos de clasificación*.  
  
     Prediga una o más variables discretas, basándose en los demás atributos del conjunto de datos.  
  
-   *Algoritmos de regresión*  
  
     Prediga una o más variables continuas, como las pérdidas o los beneficios, basándose en otros atributos del conjunto de datos.  
  
-   *Algoritmos de segmentación*  
  
     Divida los datos en grupos o clústeres, con elementos que tengan propiedades similares.  
  
-   *Algoritmos de asociación*  
  
     Busque correlaciones entre distintos atributos de un conjunto de datos. Este tipo de algoritmo se suele usar para crear reglas de asociación. Las reglas de asociación se pueden usar en el análisis de la cesta de compras.  
  
-   *Algoritmos de análisis de secuencia*  
  
     Resuma secuencias o episodios frecuentes en los datos, como las rutas que siguen los usuarios al navegar por un sitio web.  
  
 Los algoritmos utilizados por los Complementos de minería de datos de SQL Server para Office están basados en los algoritmos proporcionados por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. También puede utilizar algoritmos de terceros que cumplan con la especificación OLE DB para minería de datos, si la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a la que está conectado se ha configurado para permitir los algoritmos de terceros.  
  
## <a name="requirements"></a>Requisitos  
 Los algoritmos se diferencian entre sí en el tipo de datos con los que pueden funcionar.  
  
-   Un modelo de regresión lineal solo puede modelar valores numéricos. Tanto las variables de entrada como los resultados de destino deben ser tipos de números continuos. Utilice un árbol de decisión o un modelo de estimación si necesita mezclar variables discretas y continuas.  
  
-   Un modelo Bayes naive requiere que todos los números se discreticen. Si usa uno de los asistentes basados en este algoritmo, la discretización se realiza automáticamente.  
  
-   Un modelo de árboles de decisión puede contener variables discretas y continuas. Sin embargo, los números se discretizan automáticamente según sea necesario para las divisiones del árbol.  
  
-   Los modelos de redes neuronales y de regresión logística discretizan automáticamente los números usados como resultados o como variables de entrada. Si desea agrupar los números de acuerdo con otros criterios, debe utilizar la herramienta Cambiar etiquetas para crear las agrupaciones antes del modelado. Por ejemplo, podría desea valores de grupo en un **Age** columna por deciles (10-20, 21-30 y así sucesivamente), en lugar de las agrupaciones estadísticamente significativas que encuentra el modelo (un ejemplo podría ser 35,6-41, 8 años).  
  
-   Un modelo de asociación requiere que los datos estén agrupados en transacciones, cada una de las cuales hará referencia a varios elementos o filas. Si usas el [Asistente asociar &#40;cliente de minería de datos para Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) asistente o [análisis de cesta de la compra &#40;herramientas de análisis de tabla para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) herramienta, los datos debería mostrarse como se muestra en el **asociar** ficha del libro de ejemplo.  
  
     Si desea usar tablas anidadas en un origen de datos externo, debe utilizar el [avanzadas de modelado &#40;complementos de minería de datos para Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) opciones para crear una estructura de minería de datos y un modelo de minería de datos que se guarda en el servidor de modelado. Excel no admite tablas anidadas.  
  
## <a name="feature-selection"></a>Selección de características  
 Dependiendo del conjunto de datos, puede aplicar el algoritmo *selección de características*, eliminar las columnas que no son útiles y determinar qué columnas de datos son estadísticamente significativas en relación con el resultado.  
  
 Cada algoritmo utiliza métodos de selección de características ligeramente diferentes (como la entropía o varias puntuaciones de información) para determinar qué tendencias son importantes y qué diferencias se pueden descartar.  
  
 En los Complementos de minería de datos para Excel, la selección de características se aplica automáticamente, utilizando el método de puntuación adecuado para cada algoritmo. Si desea que afecte a los resultados de la selección de características, utilice los asistentes de la **minería de datos** la cinta de opciones y haga clic en **avanzadas** para establecer los parámetros mediante la **parámetros del algoritmo**cuadro de diálogo.  
  
 Para obtener una lista de la selección de características, métodos utilizados por cada algoritmo vea el tema en [selección de características &#40;minería de datos&#41; ](data-mining/feature-selection-data-mining.md) en libros en pantalla de SQL Server.  
  
## <a name="list-of-supported-algorithms"></a>Lista de algoritmos admitidos  
 Los algoritmos siguientes se proporcionan de manera predeterminada.  
  
|Nombre del algoritmo|Descripción|Se usa en|  
|--------------------|-----------------|-------------|  
|Reglas de asociación de Microsoft|Crea reglas que describen qué artículos es probable que aparezcan juntos en una transacción.|[Asistente para asociación &#40;cliente de minería de datos para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [Análisis de cesta de la compra &#40;herramientas de análisis de tabla para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Clústeres de Microsoft|Identifica relaciones en un conjunto de datos que no podría extraer lógicamente mediante la observación casual. Usa técnicas iterativas para agrupar los registros en clústeres que contengan características similares.|[Detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [Asistente para clúster &#40;datos complementos de minería de datos para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Árboles de decisión de Microsoft|Realiza predicciones basándose en las relaciones entre las columnas del conjunto de datos y modela las relaciones como series de divisiones en forma de árbol en valores específicos.<br /><br /> Admite la predicción de atributos discretos y continuos.|[Asistente para clasificar &#40;datos complementos de minería de datos para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [Asistente para estimación &#40;datos complementos de minería de datos para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Regresión lineal de Microsoft|Si existe una dependencia lineal entre la variable de destino y las variables que se examinan, encuentra la relación más eficiente entre el destino y sus entradas.<br /><br /> Admite la predicción de atributos continuos.|Este algoritmo está disponible en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. En los Complementos de minería de datos para Office, para crear un modelo que utilice este algoritmo se puede crear una estructura y, a continuación, agregar manualmente un modelo.<br /><br /> Para obtener más información, consulte [avanzadas de modelado &#40;complementos minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Regresión logística de Microsoft|Analiza los factores que contribuyen a un resultado, donde el resultado está restringido a dos valores, que suelen ser la aparición o no de un evento.<br /><br /> Admite la predicción de atributos discretos y continuos.|[Rellenar desde ejemplo &#40;herramientas de análisis de tabla para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [Escenario Buscar objetivo &#40;herramientas de análisis de tabla para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [Escenario y si &#40;herramientas de análisis de tabla para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Bayes naive de Microsoft|Encuentra la probabilidad de la relación entre todas las columnas de entrada y de predicción. Este algoritmo es útil para generar rápidamente modelos de minería de datos para descubrir relaciones.<br /><br /> Admite sólo atributos discretos o discretizados.<br /><br /> Trata todos los atributos de entrada como independientes.|[Analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Red neuronal de Microsoft|Analiza datos complejos de entrada o problemas empresariales para los que hay disponible una cantidad significativa de datos de aprendizaje pero de los que no se pueden derivar reglas fácilmente con otros algoritmos.<br /><br /> Puede predecir varios atributos.<br /><br /> Se puede usar para clasificar atributos discretos y la regresión de atributos continuos.|Este algoritmo está disponible en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. En los Complementos de minería de datos para Office, para crear un modelo que utilice este algoritmo se puede crear una estructura y, a continuación, agregar manualmente un modelo.<br /><br /> Para obtener más información, consulte [avanzadas de modelado &#40;complementos minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Clústeres de secuencia de Microsoft|Identifica los clústeres de eventos ordenados de forma similar en una secuencia.<br /><br /> Proporciona una combinación de análisis de secuencia y de agrupación en clústeres.|Este algoritmo solo está disponible en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Sin embargo, en los Complementos de minería de datos para Office, para crear un modelo que utilice este algoritmo se puede crear una estructura y, a continuación, agregar manualmente un modelo.<br /><br /> Para obtener más información, consulte [avanzadas de modelado &#40;complementos minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Serie temporal de Microsoft|Analiza datos relacionados con el tiempo mediante un árbol de decisión lineal.<br /><br /> Se pueden usar patrones para predecir valores futuros en la serie temporal.|[Previsión &#40;herramientas de análisis de tabla para Excel&#41;](forecast-table-analysis-tools-for-excel.md)<br /><br /> [Asistente para pronóstico &#40;datos complementos de minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>Vea también  
 [Qué incluye en los datos de los complementos de minería de datos para Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  