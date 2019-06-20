---
title: Introducción a minería de datos (complementos de minería de datos para Excel de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: cbe10a19-e194-408e-a65b-5fdf3fb1e880
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e5a24a158681c3f596355b1b9abca6ada990531
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080937"
---
# <a name="getting-started-with-data-mining-data-mining-add-ins-for-excel"></a>Introducción a la minería de datos (Complementos de minería de datos para Excel)
  La minería de datos es el proceso de detectar patrones significativos en los datos. La minería de datos es un complemento natural al proceso de explorar y entender los datos a través de BI tradicional. Los algoritmos automáticos pueden procesar cantidades de datos muy grandes y detectar patrones y tendencias que, de lo contrario, estarían ocultos.  
  
 Para realizar la minería de datos, recopila datos que es relevantes para una pregunta específica, como "¿quién son mis clientes?" o "¿qué productos adquirieron?" y, a continuación, aplique un algoritmo para encontrar correlaciones estadísticas en los datos. Los patrones y las tendencias que se detectan en el análisis se almacenan en forma de modelo de minería de datos. Después puede aplicar el modelo de minería de datos a nuevos datos en escenarios empresariales como los siguientes:  
  
-   Usar tendencias anteriores para predecir las ventas del siguiente trimestre, los requisitos de inventario o la satisfacción de los clientes.  
  
-   Aplicar el conocimiento de los clientes actuales para generar perfiles de nuevos clientes y recomendar nuevos productos o oportunidades.  
  
-   Buscar correlaciones entre eventos pasados para predecir los errores o el tiempo de inactividad del servidor.  
  
-   Analizar qué productos adquieren juntos los clientes y usar la información para recomendar paquetes o planear la posición de los productos.  
  
 El método de análisis que elija dependerá de los objetivos. Los Complementos de minería de datos admiten estos tipos de análisis:  
  
-   Aprendizaje supervisado y no supervisado  
  
-   Agrupación en clústeres (segmentación)  
  
-   Análisis factorial, utilizando redes bayesianas y neuronales  
  
-   Análisis de series temporales  
  
-   Análisis de asociación, análisis de recomendaciones y análisis de la cesta de compras  
  
-   Resultados binarios de puntuación  
  
-   Regresión lineal  
  
 Además, los complementos ayudan en la fase de preparación de datos: selección de datos, exploración y limpieza de datos.  
  
## <a name="define-your-goal"></a>Definir el objetivo  
 Antes de empezar, dedique un par de minutos a considerar cuál es la pregunta a la que verdaderamente quiere dar una respuesta. La exploración en sí misma es reveladora, pero si desea aplicar sus hallazgos a nuevos datos, debe ser capaz de indicar claramente qué espera que genere el modelo y cómo medirá si el modelo logra los objetivos.  
  
 Por ejemplo, en lugar de un objetivo de "Buscar nuevos clientes", aclarar su objetivo a algo más concreto, como "identificar la demografía de clientes que están probables que compren nuestro producto, con una probabilidad de al menos un 65%".  
  
-   El conjunto de datos debe contener al menos un atributo de "resultado" que puede usar para el entrenamiento y predicción. Si no existe ese tipo de atributo, puede etiquetar manualmente algunos datos de entrenamiento o usar otras columnas para crear un proxy para el resultado.  
  
     Por ejemplo, si desea predecir "las mejores perspectivas", se debe aplicar alguna regla de negocios con antelación para etiquetar los clientes existentes, por lo que puede aprender la minería de datos de los ejemplos que proporciona.  
  
-   Si trabaja con un valor que cambia con el paso del tiempo y desea predecir las tendencias futuras, piense en cuál va a ser la granularidad de los resultados que necesita. ¿Desea que las predicciones se realicen diaria, mensual o anualmente? Los datos tienen que analizarse con las mismas unidades que desea predecir.  
  
     Con los patrones cíclicos, si no obtiene buenos resultados con datos diarios, pruebe distintos intervalos de tiempo o pruebe a usar días de la semana, meses o incluso días no laborables.  
  
-   Antes de iniciar un asistente para encontrar correlaciones nuevas en los datos, examine una vez más los datos y considere qué clase de relaciones existentes podría haber en el conjunto de datos. ¿Hay variables poco claras? ¿Hay duplicados o servidores proxy?  
  
-   ¿Cuáles son las métricas por el que se va a evaluar el éxito del modelo? ¿Cómo sabrá que el modelo es "suficientemente bueno"?  
  
-   ¿Desea realizar predicciones a partir del modelo de minería de datos o sólo buscar asociaciones y patrones interesantes?  
  
## <a name="explore-your-data-and-explore-the-model"></a>Explorar los datos y explorar el modelo  
 Quizás ya tenga un conocimiento profundo de los datos y el dominio. Incluso aunque lo tenga, debe dedicar cierto tiempo a generar perfiles de los datos teniendo en cuenta el modelado.  
  
 Dedique un minuto a ver la distribución de valores e identificar posibles problemas como valores o marcadores de posición ausentes.  
  
 Si va a realizar la minería de datos en un conjunto de datos que era demasiado grande y complejo que no se pudo analizar con otros métodos, considere la posibilidad de muestreo o la reducción de datos.  
  
-   ¿Cómo se distribuyen los datos?  
  
-   ¿Cómo se relacionan las columnas? o en caso de haber varias tablas, ¿cómo se relacionan las tablas?  
  
-   ¿Falta algún valor? ¿Hay valores que necesitan convertirse o procesarse previamente?  
  
-   ¿Los datos son sobre todo texto, mayormente números o una combinación de texto y números?  
  
-   ¿Dispone de datos suficientes para analizar los resultados de destino? Si va a analizar asociaciones entre productos, seguramente necesite muchos datos más. Cuando se predicen resultados binarios, son necesarios muchos menos datos, siempre y cuando el conjunto de datos esté equilibrado.  
  
 Una vez completado el modelo, dedique un tiempo a revisar los resultados e identifique maneras de modificar datos u obtener mejores resultados. Es excepcionalmente raro que el primer modelo proporcione todas las respuestas. La minería de datos suele ser un proceso iterativo.  
  
 Cuando intente discretizar los datos de distintas formas, o agregar nuevas columnas, recuerde que debe usar el **documentar modelo** Asistente para capturar una instantánea de los metadatos y los resultados de cada modelo. El hecho de tener un registro facilitará el seguimiento del progreso en la exploración.  
  
 [Exploración y limpieza de datos](exploring-and-cleaning-data.md)  
  
## <a name="validate-your-model"></a>Validar el modelo  
 A medida que se ejecuta cada asistente o herramienta, el algoritmo analiza el contenido de los datos y determina si existe un patrón estadísticamente válido. Si el algoritmo no puede encontrar patrones válidos, obtendrá un mensaje de error. Sin embargo, incluso si se ha creado correctamente un modelo, desea probar el modelo para ver si valida sus suposiciones. Puede usar herramientas como el [gráfico de precisión &#40;complementos de minería de datos de SQL Server&#41; ](accuracy-chart-sql-server-data-mining-add-ins.md) o [validación cruzada &#40;complementos de minería de datos de SQL Server&#41; ](cross-validation-sql-server-data-mining-add-ins.md) para generar estadísticas medidas de calidad del modelo.  
  
 Cuando evalúe los resultados del primer modelo, hágase preguntas como estas:  
  
-   ¿Qué tipos de patrones se han encontrado? ¿Cuáles son las probabilidades y los valores de compatibilidad?  
  
-   ¿Eran correctas las suposiciones acerca de las tendencias, o había correlaciones inesperadas?  
  
-   ¿Recopilamos suficientes datos? ¿Produciría la discretización de los datos patrones más claros?  
  
-   ¿Está equilibrado el conjunto de datos? La validación cruzada puede probar la representatividad de los datos.  
  
 [Herramientas de análisis de tablas para Excel](table-analysis-tools-for-excel.md)  
  
 [Cliente de minería de datos para Excel &#40;complementos de minería de datos de SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
 [Elegir un modelo](choosing-a-model.md)  
  
## <a name="explore-and-refine"></a>Explorar y refinar  
 Si el modelo parece ser válido, puede usarlo para realizar predicciones y recomendaciones, derivar percepciones o planear estrategias empresariales.  
  
-   Use el explorador de minería de datos del Cliente de minería de datos para Excel con el fin de explorar e interactuar con el modelo.  
  
-   Use Excel para reorganizar y filtrar los resultados.  
  
-   Use Visio para crear presentaciones y resaltar las relaciones que se encuentran en los datos.  
  
 A menudo, el primer resultado del análisis es la percepción de que existen formas de mejorar el análisis o de que es necesario obtener nuevos y mejores datos. Dado que los modelos que se crean con los Complementos de minería de datos para Excel se pueden guardar en una instancia de Analysis Service, es relativamente fácil actualizar el modelo con nuevos datos y continuar refinando y reutilizando modelos válidos.  
  
 Un uso importante de los modelos de minería de datos es la creación de predicciones y recomendaciones. Los Complementos de minería de datos para Excel incluyen herramientas que facilitan la generación de consultas de predicción complejas para convertir nuevas percepciones en resultados procesables. Todas estas herramientas están totalmente integradas con Excel.  
  
 [Ver modelos &#40;datos complementos de minería de datos para Office&#41;](viewing-models-data-mining-add-ins-for-office.md)  
  
 [Validar modelos y usar modelos para la predicción &#40;datos complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
## <a name="see-also"></a>Vea también  
 [Qué incluye en los datos de los complementos de minería de datos para Office](what-s-included-in-the-data-mining-add-ins-for-office.md)   
 [Referencia técnica &#40;datos complementos de minería de datos para Excel&#41;](technical-reference-data-mining-add-ins-for-excel.md)  
  
  
