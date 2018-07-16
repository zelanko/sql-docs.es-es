---
title: Cliente de minería de datos para Excel (complementos de minería de datos de servidor SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78a71f5fed5bfcc46742f8554ff69329c3a30b0d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257511"
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
  
-   [Modelos de vista](#bkmk_ViewModels)  
  
     Los gráficos generados por la mayoría de las herramientas pueden guardarse directamente en Excel. Use la [examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) herramienta para explorar los modelos.  
  
-   [Administrar, documentar e implementar](#bkmk_UsageMgmt)  
  
     El Cliente de minería de datos para Excel mantiene una conexión activa con el servidor, por lo que se puede guardar el modelo de minería de datos en el servidor, para usarlo en otras pruebas o implementarlo en un servidor de producción para conseguir una mayor escalabilidad.  
  
##  <a name="bkmk_Data"></a> Trabajar con datos  
 El **preparación de datos** grupo contiene los siguientes asistentes que le ayudarán a revisión y limpieza de datos como preparación para tareas de minería de datos. La mayoría de los asistentes también permitirán separar los datos en conjuntos de aprendizaje y de prueba.  
  
 [Explorar datos &#40;complementos de minería de datos de SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 Para generar y almacenar modelos, el complemento admite estas conexiones de datos:  
  
-   Conexión con un servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], para almacenar y procesar los modelos.  
  
-   Conexiones opcionales a los orígenes de datos externos. Puede generar el modelo utilizando cualquier tipo de datos que se pueda definir como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], o simplemente utilizar los datos que ya están en Excel.  
  
 [Explorar datos &#40;complementos de minería de datos de SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 El **explorar datos** asistente le ayuda a conocer el tipo y cantidad de datos en la tabla de datos mediante una representación gráfica de la distribución y los valores de las columnas seleccionadas, una vez.  
  
 [Datos de ejemplo &#40;complementos de minería de datos de SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 La creación del tipo de datos más apropiado para entrenar y probar los modelos es una parte importante de la minería de datos, pero también puede resultar una tarea tediosa si no se dispone de las herramientas adecuadas. El **datos de ejemplo** asistente facilita la tarea se va a dividir los datos utilizados para un modelo en dos grupos, uno para generar el modelo y otro para probarlo. Puede utilizar el muestreo aleatorio o el sobremuestreo.  
  
 [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 El **quitar valores atípicos** asistente le ofrece varias herramientas para identificar y tratar correctamente los valores atípicos. Muestra la distribución de valores y la relación de los valores atípicos con otros datos, y permite decidir si se deben quitar o cambiar los valores atípicos.  
  
 [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 El **cambiar etiquetas** asistente le ayuda a crear nuevas etiquetas para los datos para que resulte más fácil entender los resultados del análisis. Por ejemplo, puede cambiar el nombre de un intervalo de datos por un nombre más descriptivo o puede elegir un valor representativo en la lista.  
  
##  <a name="bkmk_Model"></a> Generar modelos y analizar  
 Las opciones de la **modelado de datos** sección de la barra de herramientas le permite crear patrones de datos; agrupar filas de datos basado en atributos o exploración asociaciones. Los asistentes de esta cinta de herramientas se basan en los eficaces algoritmos de minería de datos disponibles en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A diferencia de las herramientas similares de las Herramientas de análisis de tabla para Excel, estos asistentes le permitirán personalizar el comportamiento del algoritmo y usar diversos orígenes de datos.  
  
 [Asistente para clasificar &#40;datos complementos de minería de datos para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
 El **clasificar** asistente le ayuda a crear un modelo de clasificación basado en datos existentes en una tabla de Excel, un rango de Excel o un origen de datos externo. Un modelo de clasificación extrae patrones de los datos que indican similitudes y permiten realizar predicciones basadas en las agrupaciones de valores. Por ejemplo, un modelo de clasificación podría utilizarse para predecir el riesgo en función de los patrones de ingresos o gastos.  
  
 El **clasificar** asistente admite el uso de estos algoritmos de minería de datos de Microsoft: algoritmo de árboles de decisión, regresión logística, Naïve Bayes, las redes neuronales.  
  
 [Asistente para estimación &#40;datos complementos de minería de datos para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 El **estimación** asistente le ayuda a crear un modelo de estimación. Un modelo de estimación extrae patrones de los datos y los usa para predecir un resultado numérico, como valores de moneda, importes de venta, fechas u horas.  
  
 El **estimación** asistente usa estos algoritmos de minería de datos de Microsoft: árboles de decisión, regresión lineal, regresión logística y redes neuronales.  
  
 [Analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 El Asistente para clúster ayuda a crear un modelo de agrupación en clústeres. Un modelo de clústeres detecta grupos de filas que comparten características similares. Este asistente resulta útil para examinar patrones en todo tipo de datos.  
  
 El **clúster** asistente usa el algoritmo Microsoft Clustering, lo que incluye mediana-k y EM.  
  
 [Asistente para asociación &#40;cliente de minería de datos para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
 El **asociar** asistente le ayuda a crear un modelo de minería de datos utilizando el algoritmo de reglas de asociación de Microsoft, que detecta elementos conjuntamente frecuentes o eventos. Estos modelos de asociación son especialmente útiles para realizar recomendaciones.  
  
 El **asociar** asistente usa el algoritmo de reglas de asociación de Microsoft.  
  
 [Asistente para pronóstico &#40;datos complementos de minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
 El **previsión** asistente le ayuda a predecir valores en una serie temporal. Normalmente, los datos que se utilizan en un pronóstico contienen algún tipo de serie temporal, bien una marca de fecha o algún identificador de secuencia, y se usan para derivar patrones con objeto de predecir valores futuros.  
  
 El **previsión** asistente usa el algoritmo de serie temporal de Microsoft.  
  
 [Advanced modelado &#40;datos complementos de minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
 ¿Ya está familiarizado con la minería de datos? Puede usar el **avanzadas** opciones para crear estructuras de datos personalizadas y generar modelos con personalizaciones no incluidas en las otras herramientas y asistentes de modelado de datos.  
  
##  <a name="bkmk_Validate"></a> Probar, consultar y validar modelos  
 Utilice los asistentes de la **precisión y validación** barra de herramientas para usar las pruebas estándar del sector para validar la precisión de los modelos y para evaluar la viabilidad del conjunto de datos para la creación de modelos.  
  
 [Analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Evalúa el rendimiento de un modelo de minería de datos generando un gráfico de elevación o un gráfico de dispersión.  
  
 [Matriz de clasificación &#40;complementos de minería de datos de SQL Server&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 Ayuda a evaluar el rendimiento de un modelo de clasificación mediante la creación de un gráfico que resume las predicciones precisas e imprecisas realizadas por el modelo.  
  
 [Gráfico de beneficios &#40;complementos de minería de datos de SQL Server&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 Le permite entender el impacto de un modelo de minería de datos mediante la representación gráfica de la precisión de las predicciones junto con los costos y las ventajas de tomar medidas basadas en la predicción.  
  
 [La validación cruzada &#40;complementos de minería de datos de SQL Server&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 Crea un informe que resume la precisión del modelo en muchos subconjuntos del conjunto de datos para que pueda determinar lo estable que es.  
  
 También puede usar datos de una tabla de Excel como entrada de una consulta de predicción en un modelo de minería de datos almacenado en el servidor.  
  
 [Consulta &#40;complementos de minería de datos de SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
 El **consulta** asistente le ayuda a crear predicciones basadas en un modelo de minería de datos existente.  
  
 [Editor de consultas avanzadas de minería de datos](advanced-data-mining-query-editor.md)  
 Para los usuarios avanzados, esta herramienta proporciona una interfaz de arrastrar y colocar en DMX. Puede crear con facilidad consultas de predicción o modelos nuevos sin preocuparse de la sintaxis.  
  
##  <a name="bkmk_ViewModels"></a> Modelos de vista  
 Los modelos que cree se abren automáticamente para examinarlos. Sin embargo, también puede examinar los modelos en el servidor y generar nuevas visualizaciones. Use la [formas de Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md) para exportar los diagramas de modelo a un lienzo personalizable.  
  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 Vea los modelos que ha creado, utilizando gráficos interactivos personalizados para cada tipo de modelo.  
  
 [Documentar modelos de minería de datos &#40;datos complementos de minería de datos para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 Este asistente crea informes que proporcionan un resumen estadístico del conjunto de datos y metadatos sobre el modelo, para ayudar en la investigación y la interpretación.  
  
##  <a name="bkmk_UsageMgmt"></a> Administrar, documentar e implementar  
 Estas herramientas le ayudan a conectarse con un servidor de minería de datos, a administrar y exportar modelos, y a supervisar la actividad de la minería de datos.  
  
 [Administrar modelos &#40;complementos de minería de datos de SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 Si tiene los permisos necesarios, podrá eliminar, modificar, cambiar el nombre o procesar las estructuras y los modelos de minería de datos existentes sin salir de Excel.  
  
 [Seguimiento &#40;cliente de minería de datos para Excel&#41;](trace-data-mining-client-for-excel.md)  
 Haga clic en **seguimiento** para ver una captura actual de la interacción entre el cliente de Excel y el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] server. Todas las actividades se almacenan como instrucciones DMX o XMLA, por lo que puede solucionar problemas de la sesión de minería de datos o guardar la información para su uso posterior.  
  
 [Conectar con un servidor de minería de datos](connect-to-a-data-mining-server.md)  
 Para usar Excel como cliente para la minería de datos, debe establecer una conexión con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La conexión le proporcionará acceso al motor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Si tiene permisos, la conexión le permitirá almacenar cualquier patrón que haya detectado y modificar objetos de minería de datos existentes.  
  
 El **conexiones** barra de herramientas proporciona asistentes para administrar las conexiones a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para usar las herramientas de minería de datos y los algoritmos, debe definir una conexión con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede crear la conexión cuando instale el complemento o agregar una conexión posteriormente.  
  
 **Introducción**  
 Haga clic en el **Introducción** botón para iniciar un asistente de configuración que le guiará a través del proceso de creación de una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]y obtener los permisos necesarios para realizar la minería de datos.  
  
 **Ayuda**  
 El **ayuda** menú desplegable proporciona vínculos a Ayuda en línea, sitios Web y un asistente de configuración que le ayudarán a completar la instalación y minería de datos de inicio.  
  
 La página de Ayuda también incluye vínculos a los recursos en línea, incluida la Ayuda del complemento, y vídeos, demostraciones y ejemplos adicionales.  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)   
 [Solución de problemas de diagramas de minería de datos de Visio &#40;complementos de minería de datos de SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
