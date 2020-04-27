---
title: Cliente de minería de datos para Excel (complementos de minería de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c2f11ecbdf90aeeb5e0e5a3ef097152898042d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086430"
---
# <a name="data-mining-client-for-excel-sql-server-data-mining-add-ins"></a>Cliente de minería de datos para Excel (Complementos de minería de datos de SQL Server)
  El Cliente de minería de datos para Excel es un conjunto de herramientas que permiten realizar tareas comunes de minería de datos, desde limpieza de datos hasta generación de modelos y consultas de predicción. Puede utilizar los datos de las tablas o los rangos de Excel, o tener acceso a orígenes de datos externos.  
  
 ![DM](media/dm-tabletools.gif "DM")  
  
-   [Trabajar con datos](#bkmk_Data)  
  
     Cargue los datos en Excel, límpielos, compruebe la existencia de valores atípicos y cree resúmenes estadísticos. También puede realizar diferentes tipos de muestreo, perfiles de los datos y probar los modelos con datos externos. El Cliente de minería de datos es el modo más sencillo de preparar datos para el análisis sin necesidad de complejos scripts o procesos ETL.  
  
-   [Generar modelos y analizar](#bkmk_Model)  
  
     Estas herramientas proporcionan interfaces de asistente para algoritmos de minería de datos conocidos y probados empíricamente, incluida la agrupación en clústeres (mediana-k y EM), el análisis de la asociación, el análisis de series temporales y los árboles de decisión. Las opciones avanzadas de modelado para cada asistente le permiten elegir algoritmos diferentes, como Naïve Bayes o las redes neuronales, y personalizar el comportamiento como la inicialización del clúster o el tamaño del muestreo inicial.  
  
     Todos los algoritmos de minería de datos se hospedan en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], lo que le ofrece más capacidad para generar modelos complejos.  
  
-   [Probar, consultar y validar modelos](#bkmk_Validate)  
  
     El Cliente de minería de datos proporciona herramientas estándar del sector para probar los modelos, incluidos los gráficos de elevación y la validación cruzada. Los asistentes proporcionados facilitan las pruebas de la validez del conjunto de datos y su precisión. El asistente de consulta genera consultas para usar los modelos para la predicción y la puntuación.  
  
-   [Ver modelos](#bkmk_ViewModels)  
  
     Los gráficos generados por la mayoría de las herramientas pueden guardarse directamente en Excel. Use los [modelos de exploración en Excel &#40;SQL Server](browsing-models-in-excel-sql-server-data-mining-add-ins.md) herramientas de&#41;complementos de minería de datos para explorar los modelos.  
  
-   [Administrar, documentar e implementar](#bkmk_UsageMgmt)  
  
     El Cliente de minería de datos para Excel mantiene una conexión activa con el servidor, por lo que se puede guardar el modelo de minería de datos en el servidor, para usarlo en otras pruebas o implementarlo en un servidor de producción para conseguir una mayor escalabilidad.  
  
##  <a name="work-with-data"></a><a name="bkmk_Data"></a>Trabajar con datos  
 El grupo **preparación de datos** contiene los siguientes asistentes que le ayudarán a revisar y limpiar los datos como preparación para las tareas de minería de datos. La mayoría de los asistentes también permitirán separar los datos en conjuntos de aprendizaje y de prueba.  
  
 [Explorar datos &#40;SQL Server complementos de minería de datos&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 Para generar y almacenar modelos, el complemento admite estas conexiones de datos:  
  
-   Conexión con un servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], para almacenar y procesar los modelos.  
  
-   Conexiones opcionales a los orígenes de datos externos. Puede generar el modelo utilizando cualquier tipo de datos que se pueda definir como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o simplemente utilizar los datos que ya están en Excel.  
  
 [Explorar datos &#40;SQL Server complementos de minería de datos&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 El Asistente para **explorar datos** le ayuda a comprender el tipo y la cantidad de datos de la tabla de datos mediante la representación gráfica de la distribución y los valores de las columnas seleccionadas, de una en una.  
  
 [&#40;de datos de ejemplo SQL Server complementos de minería de datos&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 La creación del tipo de datos más apropiado para entrenar y probar los modelos es una parte importante de la minería de datos, pero también puede resultar una tarea tediosa si no se dispone de las herramientas adecuadas. El Asistente para **datos de muestra** facilita la división de los datos usados para un modelo en dos grupos, uno para generar el modelo y otro para probarlo. Puede utilizar el muestreo aleatorio o el sobremuestreo.  
  
 [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 El Asistente para **quitar valores atípicos** ofrece varias herramientas para identificar y administrar los valores atípicos de forma adecuada. Muestra la distribución de valores y la relación de los valores atípicos con otros datos, y permite decidir si se deben quitar o cambiar los valores atípicos.  
  
 [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 El asistente cambiar **etiquetas** permite crear nuevas etiquetas para los datos para facilitar la comprensión de los resultados del análisis. Por ejemplo, puede cambiar el nombre de un intervalo de datos por un nombre más descriptivo o puede elegir un valor representativo en la lista.  
  
##  <a name="build-models-and-analyze"></a><a name="bkmk_Model"></a>Compilar modelos y analizar  
 Las opciones de la sección **modelado de datos** de la barra de herramientas permiten derivar patrones a partir de datos; Agrupe filas de datos basándose en atributos o explore asociaciones. Los asistentes de esta cinta de herramientas se basan en los eficaces algoritmos de minería de datos disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A diferencia de las herramientas similares de las Herramientas de análisis de tabla para Excel, estos asistentes le permitirán personalizar el comportamiento del algoritmo y usar diversos orígenes de datos.  
  
 [Asistente para clasificar &#40;complementos de minería de datos para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
 El Asistente para **clasificar** le ayuda a generar un modelo de clasificación basado en los datos existentes en una tabla de Excel, un intervalo de Excel o un origen de datos externo. Un modelo de clasificación extrae patrones de los datos que indican similitudes y permiten realizar predicciones basadas en las agrupaciones de valores. Por ejemplo, un modelo de clasificación podría utilizarse para predecir el riesgo en función de los patrones de ingresos o gastos.  
  
 El Asistente para **clasificar** admite el uso de estos algoritmos de minería de datos de Microsoft: algoritmo de árboles de decisión, regresión logística, Bayes Naive, redes neuronal.  
  
 [Asistente para estimación &#40;complementos de minería de datos para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 El Asistente para **estimación** le ayuda a crear un modelo de estimación. Un modelo de estimación extrae patrones de los datos y los usa para predecir un resultado numérico, como valores de moneda, importes de venta, fechas u horas.  
  
 El asistente **Estimación** utiliza estos algoritmos de minería de datos de Microsoft: árboles de decisión, regresión lineal, regresión logística y redes neuronales.  
  
 [Analizar influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 El Asistente para clúster ayuda a crear un modelo de agrupación en clústeres. Un modelo de clústeres detecta grupos de filas que comparten características similares. Este asistente resulta útil para examinar patrones en todo tipo de datos.  
  
 El Asistente para **clúster** utiliza el algoritmo de clústeres de Microsoft, que incluye K-means y em.  
  
 [Asistente para Asociación &#40;cliente de minería de datos para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
 El Asistente para **Asociación** le ayuda a crear un modelo de minería de datos mediante el algoritmo de reglas de Asociación de Microsoft, que detecta elementos o eventos que se colocan con frecuencia. Estos modelos de asociación son especialmente útiles para realizar recomendaciones.  
  
 El **Asistente para asociaciones usa** el algoritmo de reglas de Asociación de Microsoft.  
  
 [Asistente para previsión &#40;complementos de minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
 El Asistente para **previsión** le ayuda a predecir valores en una serie temporal. Normalmente, los datos que se utilizan en un pronóstico contienen algún tipo de serie temporal, bien una marca de fecha o algún identificador de secuencia, y se usan para derivar patrones con objeto de predecir valores futuros.  
  
 El Asistente para **pronóstico** utiliza el algoritmo de serie temporal de Microsoft.  
  
 [Modelado avanzado &#40;complementos de minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
 ¿Ya está familiarizado con la minería de datos? Puede usar las opciones de modelado de datos **avanzadas** para crear estructuras de datos personalizadas y generar modelos mediante personalizaciones que no se incluyen en las otras herramientas y asistentes.  
  
##  <a name="test-query-and-validate-models"></a><a name="bkmk_Validate"></a>Probar, consultar y validar modelos  
 Use los asistentes de la barra de herramientas de **precisión y validación** para usar pruebas estándar del sector con el fin de validar la precisión de los modelos y evaluar la viabilidad del conjunto de datos para crear modelos.  
  
 [Analizar influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Evalúa el rendimiento de un modelo de minería de datos generando un gráfico de elevación o un gráfico de dispersión.  
  
 [Matriz de clasificación &#40;SQL Server complementos de minería de datos&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 Ayuda a evaluar el rendimiento de un modelo de clasificación mediante la creación de un gráfico que resume las predicciones precisas e imprecisas realizadas por el modelo.  
  
 [Gráfico de beneficios &#40;SQL Server complementos de minería de datos&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 Le permite entender el impacto de un modelo de minería de datos mediante la representación gráfica de la precisión de las predicciones junto con los costos y las ventajas de tomar medidas basadas en la predicción.  
  
 [&#40;de validación cruzada SQL Server complementos de minería de datos&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 Crea un informe que resume la precisión del modelo en muchos subconjuntos del conjunto de datos para que pueda determinar lo estable que es.  
  
 También puede usar datos de una tabla de Excel como entrada de una consulta de predicción en un modelo de minería de datos almacenado en el servidor.  
  
 [&#40;de consultas SQL Server complementos de minería de datos&#41;](query-sql-server-data-mining-add-ins.md)  
 El Asistente para **consultas** le ayuda a crear predicciones en un modelo de minería de datos existente.  
  
 [Editor de consultas avanzadas de minería de datos](advanced-data-mining-query-editor.md)  
 Para los usuarios avanzados, esta herramienta proporciona una interfaz de arrastrar y colocar en DMX. Puede crear con facilidad consultas de predicción o modelos nuevos sin preocuparse de la sintaxis.  
  
##  <a name="view-models"></a><a name="bkmk_ViewModels"></a>Ver modelos  
 Los modelos que cree se abren automáticamente para examinarlos. Sin embargo, también puede examinar los modelos en el servidor y generar nuevas visualizaciones. Use las [formas de Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md) para exportar diagramas de modelos a un lienzo personalizable.  
  
 [Examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 Vea los modelos que ha creado, utilizando gráficos interactivos personalizados para cada tipo de modelo.  
  
 [Documentar modelos de minería de datos &#40;complementos de minería de datos para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 Este asistente crea informes que proporcionan un resumen estadístico del conjunto de datos y metadatos sobre el modelo, para ayudar en la investigación y la interpretación.  
  
##  <a name="manage-document-and-deploy"></a><a name="bkmk_UsageMgmt"></a>Administrar, documentar e implementar  
 Estas herramientas le ayudan a conectarse con un servidor de minería de datos, a administrar y exportar modelos, y a supervisar la actividad de la minería de datos.  
  
 [Administrar modelos &#40;SQL Server complementos de minería de datos&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 Si tiene los permisos necesarios, podrá eliminar, modificar, cambiar el nombre o procesar las estructuras y los modelos de minería de datos existentes sin salir de Excel.  
  
 [Seguimiento &#40;cliente de minería de datos para Excel&#41;](trace-data-mining-client-for-excel.md)  
 Haga clic en **seguimiento** para ver una captura continua de la interacción entre el cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Excel y el servidor de. Todas las actividades se almacenan como instrucciones DMX o XMLA, por lo que puede solucionar problemas de la sesión de minería de datos o guardar la información para su uso posterior.  
  
 [Conectar con un servidor de minería de datos](connect-to-a-data-mining-server.md)  
 Para usar Excel como cliente para la minería de datos, debe establecer una conexión con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La conexión le proporcionará acceso al motor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Si tiene permisos, la conexión le permitirá almacenar cualquier patrón que haya detectado y modificar objetos de minería de datos existentes.  
  
 La barra de herramientas **conexiones** proporciona asistentes para administrar las conexiones a una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]instancia de. Para usar las herramientas de minería de datos y los algoritmos, debe definir una conexión con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede crear la conexión cuando instale el complemento o agregar una conexión posteriormente.  
  
 **Introducción**  
 Haga clic en el botón **Introducción** para iniciar un asistente de configuración que le guía por el proceso de creación de una conexión [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]a una instancia de y la obtención de los permisos necesarios para la minería de datos.  
  
 **Ayuda**  
 El menú desplegable **ayuda** proporciona vínculos a la ayuda en línea, sitios web y un asistente de configuración para ayudarle a completar la configuración e iniciar la minería de datos.  
  
 La página de Ayuda también incluye vínculos a los recursos en línea, incluida la Ayuda del complemento, y vídeos, demostraciones y ejemplos adicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)   
 [Solucionar problemas de diagramas de minería de datos de Visio &#40;SQL Server complementos de minería de datos&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
