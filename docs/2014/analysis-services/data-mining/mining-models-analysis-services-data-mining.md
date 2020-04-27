---
title: Modelos de minería de datos (Analysis Services, minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- mining models [Analysis Services]
- logical architecture [Analysis Services Multidimensional Data]
- properties [Analysis Services]
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: cd4df273-0c6a-4b3e-9572-8a7e313111e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57f62b125872e6b851235c1517925c6ee10058d8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174454"
---
# <a name="mining-models-analysis-services---data-mining"></a>Modelos de minería de datos (Analysis Services - Minería de datos)
  Un *modelo de minería de datos* se crea mediante la aplicación de un algoritmo a los datos, pero es algo más que un algoritmo o un contenedor de metadatos: es un conjunto de datos, estadísticas y patrones que se pueden aplicar a los nuevos datos para generar predicciones y deducir relaciones.

 En esta sección se explica qué es un modelo de minería de datos y cuál puede ser su uso: la arquitectura básica de modelos y estructuras, las propiedades de los modelos de minería de datos y las maneras de crear modelos de minería de datos y trabajar con ellos.

 [Arquitectura del modelo de minería de datos](#bkmk_mdlArch)

 [Definir modelos de minería de datos](#bkmk_mdlDefine)

 [Propiedades del modelo de minería de datos](#bkmk_mdlProps)

 [Columnas del modelo de minería de datos](#bkmk_mdlCols)

 [Procesar modelos de minería de datos](#bkmk_mdlProcess)

 [Ver y consultar modelos de minería de datos](#bkmk_mdlView)

##  <a name="mining-model-architecture"></a><a name="bkmk_mdlArch"></a> Arquitectura del modelo de minería de datos
 Un modelo de minería de datos recibe los datos de una estructura de minería de datos y, a continuación, los analiza utilizando un algoritmo de minería de datos. La estructura y el modelo de minería de datos son objetos independientes. La estructura de minería de datos almacena la información que define el origen de datos. Un modelo de minería de datos almacena la información derivada del procesamiento estadístico de los datos, como los patrones encontrados como resultado del análisis.

 Un modelo de minería de datos está vacío hasta que los datos que proporciona la estructura de minería de datos se procesan y analizan. Una vez procesado el modelo, contiene los metadatos, resultados y enlaces de la estructura de minería de datos.

 ![el elemento contiene los metadatos, patrones y enlaces](../media/dmcon-modelarch2.gif "el elemento contiene los metadatos, patrones y enlaces")

 Los metadatos especifican el nombre del modelo y el servidor donde está almacenado, así como una definición del mismo, incluidas las columnas de la estructura de minería de datos que se usaron para generarlo, las definiciones de los filtros que se aplicaron al procesarlo y el algoritmo empleado para analizar los datos. Todas estas opciones: las columnas de datos y sus tipos de datos, filtros y algoritmos, tienen una influencia eficaz sobre los resultados del análisis.

 Por ejemplo, puede usar los mismos datos para crear varios modelos, quizás mediante un algoritmo de clústeres, un algoritmo de árboles de decisión y un algoritmo Bayes Naïve. Cada tipo de modelo crea un conjunto diferente de patrones, conjuntos de elementos, reglas o fórmulas, que puede usar para realizar predicciones. Por lo general, cada algoritmo analiza los datos de forma diferente, por lo que el *contenido* del modelo resultante también se organiza en estructuras diferentes. En un tipo de modelo, los datos y los modelos pueden estar agrupados en *clústeres*; en otro, los datos pueden estar organizados en árboles, ramas y las reglas que los dividen y definen.

 El modelo también se ve afectado por los datos usados en el entrenamiento: incluso los modelos cuyo entrenamiento se ha realizado en la misma estructura de minería de datos pueden producir resultados distintos si se filtran los datos de manera diferente o se usan semillas distintas durante el análisis. Sin embargo, los datos reales no se almacenan en las estadísticas de Resumen de solo modelo que se almacenan, con los datos reales que residen en la estructura de minería de datos. Si ha creado filtros en los datos al realizar el entrenamiento del modelo, las definiciones de filtro también se guardan con el objeto de modelo.

 El modelo contiene un conjunto de enlaces, que señalan a los datos almacenados en memoria caché en la estructura de minería de datos. Si los datos se han almacenado en memoria caché en la estructura y no se han borrado después del procesamiento, estos enlaces le permiten obtener detalles de los resultados para llegar a los casos en que se basan los resultados. Sin embargo, los datos reales están almacenados en la memoria caché de la estructura, no en el modelo.

 [Arquitectura del modelo de minería de datos](#bkmk_mdlArch)

##  <a name="defining-data-mining-models"></a><a name="bkmk_mdlDefine"></a>Definir modelos de minería de datos
 Para crear un modelo de minería de datos, siga estos pasos generales:

-   Cree la estructura de minería de datos subyacente e incluya las columnas de datos que sean necesarias.

-   Seleccione el algoritmo más adecuado para la tarea analítica.

-   Elija las columnas de la estructura que se van a usar en el modelo y especifique cómo se deben usar (qué columna contiene el resultado que desea predecir, qué columnas son solo para la entrada, etc.).

-   Opcionalmente, puede establecer los parámetros para ajustar el procesamiento del algoritmo.

-   Rellene el modelo con datos *procesando* la estructura y el modelo.

 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona las herramientas siguientes para ayudarle a administrar los modelos de minería de datos:

-   El Asistente para minería de datos le ayuda a crear una estructura y el modelo de minería de datos relacionado. Éste es el método más fácil de utilizar. El asistente crea automáticamente la estructura de minería de datos necesaria y le ayuda con la configuración de los valores importantes.

-   Una instrucción DMX CREATE MODEL se puede utilizar para definir un modelo. La estructura necesaria se crea automáticamente como parte del proceso; por consiguiente, no puede reutilizar una estructura existente con este método. Use este método si ya sabe exactamente qué modelo desea crear o si desea crear scripts de modelos.

-   Una instrucción DMX ALTER STRUCTURE ADD MODEL se puede usar para agregar un nuevo modelo de minería de datos a una estructura existente. Utilice este método si desea experimentar con diferentes modelos que se basen en el mismo conjunto de datos.

 También puede crear mediante programación modelos de minería de datos, utilizando AMO o XML/A, u otros clientes como el Cliente de minería de datos para Excel. Para obtener más información, vea los temas siguientes:

 [Arquitectura del modelo de minería de datos](#bkmk_mdlArch)

##  <a name="mining-model-properties"></a><a name="bkmk_mdlProps"></a>Propiedades del modelo de minería de datos
 Cada modelo de minería de datos tiene propiedades que definen el modelo y sus metadatos. Estos incluyen el nombre, la descripción, la fecha en que se procesó el modelo por última vez, los permisos del modelo y los filtros que se usan en los datos para el entrenamiento.

 Cada modelo de minería de datos también tiene propiedades que se derivan de la estructura de minería de datos y que describen las columnas de datos que usa. Si alguna de las columnas que usa el modelo es una tabla anidada, también se le puede aplicar un filtro independiente.

 Además, cada modelo de minería de datos contiene dos propiedades especiales: <xref:Microsoft.AnalysisServices.MiningModel.Algorithm%2A> y <xref:Microsoft.AnalysisServices.MiningModelColumn.Usage%2A>.

-   **Propiedad del algoritmo** : especifica el algoritmo que se utiliza para crear el modelo. Los algoritmos que están disponibles dependen del proveedor que se use. Para obtener una lista de los algoritmos incluidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md). La propiedad `Algorithm` se aplica al modelo de minería de datos y puede establecerse solo una vez para cada modelo. Puede cambiar el algoritmo más tarde pero algunas columnas del modelo de minería de datos podrían dejar de ser válidas si el algoritmo elegido no las admite. Siempre debe volver a procesar el modelo después de modificar esta propiedad.

-   La propiedad**Usage** define cómo usa el modelo cada columna. Puede definir el uso de la columna como `Input`, `Predict`, `Predict Only` o `Key`. La propiedad `Usage` se aplica a las columnas de modelo de minería de datos individuales y debe establecerse individualmente para cada columna que se incluye en un modelo. Si la estructura contiene una columna que no se usa en el modelo, el uso se establece en `Ignore`. Algunos ejemplos de datos que puede incluir en la estructura de minería de datos pero no usar en el análisis son los nombres de clientes o las direcciones de correo electrónico. De este modo puede consultarlos en otro momento sin necesidad de incluirlos durante la fase de análisis.

 Puede cambiar el valor de las propiedades de un modelo de minería de datos después de crearlo. Sin embargo, cualquier cambio, incluso el nombre del modelo, requiere que vuelva a procesarlo. Después de volver a procesar el modelo, podría ver resultados diferentes.

 [Arquitectura del modelo de minería de datos](#bkmk_mdlArch)

##  <a name="mining-model-columns"></a><a name="bkmk_mdlCols"></a>Columnas del modelo de minería de datos
 El modelo de minería de datos contiene columnas de datos que se obtienen de las columnas definidas en la estructura de minería de datos. Además de elegir las columnas de la estructura de minería de datos que desea usar en el modelo, puede crear copias de las mismas y, a continuación, cambiar su nombre o su uso. Como parte del proceso de generación del modelo, también debe definir el uso que va a dar el modelo a la columna. Eso incluye información que indique si la columna es una clave, si se usa para la predicción o si puede omitirla el algoritmo.

 Cuando genere un modelo, en lugar de agregar automáticamente todas las columnas de datos disponibles, se recomienda que revise cuidadosamente los datos de la estructura e incluya en el modelo solo las columnas que tengan sentido para el análisis. Por ejemplo, debe evitar incluir varias columnas que repitan los mismos datos, así como el uso de columnas que contengan principalmente valores únicos. Si cree que una columna no se debería usar, no es necesario eliminarla de la estructura o del modelo de minería de datos; en su lugar, basta con establecer una marca en la columna que especifique que se debería omitir al generar el modelo. Esto significa que la columna permanecerá en la estructura de minería de datos, pero no se usará en el modelo. Si ha habilitado la obtención de detalles del modelo para la estructura de minería de datos, puede recuperar después la información de la columna.

 Según el algoritmo que elija, algunas columnas de la estructura de minería de datos podrían ser incompatibles con ciertos tipos de modelos o proporcionar resultados inexactos. Por ejemplo, si los datos contienen datos numéricos continuos, como una columna Ingresos, y el modelo requiere valores discretos, es posible que necesite convertir los datos en intervalos discretos o quitarlos del modelo. En algunos casos, el algoritmo convertirá o enlazará los datos automáticamente, pero es posible que los resultados no sean siempre los esperados. Considere la posibilidad de realizar copias adicionales de la columna y probar varios modelos. También puede establecer marcas en columnas individuales para indicar dónde se requiere un procesamiento especial. Por ejemplo, si los datos contienen valores NULL, puede usar una marca de modelado para controlar su administración. Si desea que una determinada columna sea considerada como un regresor en un modelo, puede hacerlo mediante una marca de modelado.

 Después de haber creado el modelo, puede realizar cambios como agregar o quitar columnas, o cambiar el nombre del modelo. Sin embargo, cualquier cambio, incluidos solo los de los metadatos del modelo, requiere que el modelo se vuelva a procesar.

 [Arquitectura del modelo de minería de datos](#bkmk_mdlArch)

##  <a name="processing-mining-models"></a><a name="bkmk_mdlProcess"></a> Procesar modelos de minería de datos
 Un modelo de minería de datos es un objeto vacío hasta que se procesa. Al procesar un modelo, los datos que la estructura almacena en memoria caché se pasan a través de un filtro, si se ha definido alguno en el modelo, y el algoritmo los analiza. El algoritmo calcula un conjunto de estadísticas de resumen que describen los datos, identifica las reglas y los patrones en los datos, y después usa dichas reglas y patrones para rellenar el modelo.

 Una vez procesado, el modelo de minería de datos contiene una gran cantidad de información sobre los datos y los patrones encontrados mediante el análisis, incluyendo estadísticas, reglas y fórmulas de regresión. Puede usar los visores personalizados para examinar esta información, o puede crear consultas de minería de datos para recuperarla y usarla para el análisis y la presentación.

 [Arquitectura del modelo de minería de datos](#bkmk_mdlArch)

##  <a name="viewing-and-querying-mining-models"></a><a name="bkmk_mdlView"></a> Ver y consultar modelos de minería de datos
 Después de haber procesado un modelo, puede explorarlo usando los visores personalizados que se proporcionan en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para

 También puede crear consultas en el modelo de minería de datos para realizar predicciones o recuperar los metadatos del modelo o los patrones que este crea. Las consultas se crean con Extensiones de minería de datos (DMX).

## <a name="related-content"></a>Contenido relacionado

|Temas|Vínculos|
|------------|-----------|
|Cómo generar estructuras de minería de datos que pueden admitir varios modelos de minería de datos. Cómo usar las columnas en los modelos.|[Columnas de la estructura de minería de datos](mining-structure-columns.md)<br /><br /> [Columnas del modelo de minería de datos](mining-model-columns.md)<br /><br /> [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md)|
|Obtener información sobre los distintos algoritmos, y cómo la elección del algoritmo afecta al contenido del modelo.|[Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md)<br /><br /> [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)|
|Cómo establecer propiedades en el modelo que afecten a su composición y comportamiento.|[Propiedades del modelo de minería de datos](mining-model-properties.md)<br /><br /> [Marcas de modelado &#40;Minería de datos&#41;](modeling-flags-data-mining.md)|
|Obtener información sobre las interfaces programables para la minería de datos.|[Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)<br /><br /> [Referencia de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)|
|Cómo usar los visores personalizados de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Visores de modelos de minería de datos](data-mining-model-viewers.md)|
|Ver ejemplos de los diferentes tipos de consultas que se pueden usar con los modelos de minería de datos.|[Consultas de minería de datos](data-mining-queries.md)|

## <a name="related-tasks"></a>Related Tasks
 Use los vínculos siguientes para obtener información más específica sobre cómo trabajar con modelos de minería de datos

|Tarea|Vínculo|
|----------|----------|
|Agregar y eliminar modelos de minería de datos|[Agregar un modelo de minería de datos a una estructura de minería de datos existente](add-a-mining-model-to-an-existing-mining-structure.md)<br /><br /> [Eliminar un modelo de minería de datos de una estructura de minería de datos](delete-a-mining-model-from-a-mining-structure.md)|
|Trabajar con las columnas del modelo de minería de datos|[Excluir una columna de un modelo de minería de datos](exclude-a-column-from-a-mining-model.md)<br /><br /> [Crear un alias para una columna de modelo](create-an-alias-for-a-model-column.md)<br /><br /> [Cambiar la discretización de una columna en un modelo de minería de datos](change-the-discretization-of-a-column-in-a-mining-model.md)<br /><br /> [Especificar una columna para utilizar como regresor en un modelo](specify-a-column-to-use-as-regressor-in-a-model.md)|
|Modificar las propiedades del modelo|[Cambiar las propiedades de un modelo de minería de datos](change-the-properties-of-a-mining-model.md)<br /><br /> [Aplicar un filtro a un modelo de minería de datos](apply-a-filter-to-a-mining-model.md)<br /><br /> [Eliminar un filtro de un modelo de minería de datos](delete-a-filter-from-a-mining-model.md)<br /><br /> [Habilitar la obtención de detalles para un modelo de minería](enable-drillthrough-for-a-mining-model.md)<br /><br /> [Ver o cambiar parámetros del algoritmo](view-or-change-algorithm-parameters.md)|
|Copy. mover o administrar modelos|[Realizar una copia de un modelo de minería de datos](make-a-copy-of-a-mining-model.md)<br /><br /> [Copiar una vista de un modelo de minería de datos](copy-a-view-of-a-mining-model.md)<br /><br /> [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx)<br /><br /> [IMPORT &#40;DMX&#41;](/sql/dmx/import-dmx)|
|Rellenar los modelos con datos, o actualizar los datos de un modelo|[Procesar un modelo de minería de datos](process-a-mining-model.md)|
|Trabajar con modelos OLAP|[Crear una dimensión de minería de datos](create-a-data-mining-dimension.md)|

## <a name="see-also"></a>Consulte también
 [Objetos de base de datos &#40;Analysis Services - Datos multidimensionales&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)


