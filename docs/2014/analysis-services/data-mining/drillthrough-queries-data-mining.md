---
title: Consultas de obtención de detalles (minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AllowDrillThrough property
- drillthrough [Analysis Services]
- drillthrough [DMX]
ms.assetid: 246c784b-1b0c-4f0b-96f7-3af265e67051
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca74fe9ec36262130e01a58280f9d966c35c3485
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084552"
---
# <a name="drillthrough-queries-data-mining"></a>Consultas de obtención de detalles (minería de datos)
  Una *consulta de obtención de detalles* permite recuperar los detalles de los casos o de los datos de estructura subyacentes mediante el envío de una consulta al modelo de minería de datos. La obtención de detalles resulta útil para ver los casos usados para entrenar el modelo frente a los casos que se usaron para probarlo, o si desea revisar detalles adicionales de los datos de los casos.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona dos opciones diferentes para la obtención de detalles:  
  
-   Obtener detalles de los **casos del modelo**  
  
     La obtención de detalles de los casos del modelo se usa cuando se desea pasar de un patrón específico del modelo, como un clúster o una rama de un árbol de decisión, y ver detalles sobre los casos individuales.  
  
-   Obtener detalles de los **casos de la estructura**  
  
     La obtención de detalles de los casos de la estructura resulta útil cuando la estructura contiene información que podría no estar disponible en el modelo. Por ejemplo, no usaría información de contacto del cliente en un modelo de agrupación en clústeres ni aunque los datos estuvieran incluidos en la estructura. Sin embargo, después de crear el modelo, puede que desee recuperar información de contacto para los clientes agrupados en un clúster determinado.  
  
 En esta sección se proporcionan ejemplos de cómo puede crear estas consultas.  
  
 [Usar la obtención de detalles en el diseñador de minería de datos](#bkmk_Designer)  
  
 [Crear consultas de obtención de detalles mediante DMX](#bkmk_DMX)  
  
 [Consideraciones al usar la obtención de detalles](#bkmk_Considerations)  
  
-   [Problemas de seguridad](#bkmk_Security)  
  
-   [Limitaciones](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a>Usar la obtención de detalles en el diseñador de minería de datos  
 Si se ha configurado un modelo de minería de datos para permitir la obtención de detalles y tiene los permisos adecuados, al examinar el modelo puede hacer clic en un nodo en el visor adecuado y recuperar la información detallada sobre los casos de ese nodo concreto.  
  
 Obtener [detalles de los datos de los casos de un modelo de minería de datos](drill-through-to-case-data-from-a-mining-model.md).  
  
 Si los casos de entrenamiento se almacenaron en caché al procesar la estructura de minería de datos y dispone de los permisos necesarios, puede devolver información de los casos del modelo y de la estructura de minería de datos, incluso las columnas que no estaban incluidas en el modelo de minería de datos.  
  
##  <a name="bkmk_DMX"></a>Crear consultas de obtención de detalles mediante DMX  
 Puede obtener información detallada de los datos de los casos creando una consulta DMX si tiene los permisos para el modelo o para la estructura. Para obtener ejemplos de la sintaxis para crear las consultas de obtención de detalles en DMX, consulte el siguiente tema:  
  
 [Crear consultas de obtención de detalles usando DMX](create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a>Consideraciones al usar la obtención de detalles  
  
-   Si usa el Asistente para minería de datos, la opción para habilitar la obtención de detalles en los casos del modelo está en la página final del asistente. La obtención de detalles está deshabilitada de forma predeterminada. Para obtener más información, vea [Finalización del asistente &#40;Asistente para minería de datos&#41;](../completing-the-wizard-data-mining-wizard.md).  
  
-   Puede agregar la capacidad de obtener detalles a un modelo de minería de datos existente pero, si lo hace, hay que volver a procesar el modelo para poder obtener detalles de los datos.  
  
-   La obtención de detalles funciona recuperando la información sobre los casos de entrenamiento que se almacenó en memoria caché al procesar la estructura de minería de datos. Por lo tanto, si borró los datos almacenados en caché después de procesar la estructura cambiando la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a `ClearAfterProcessing`, la obtención de detalles no funcionará. Para habilitar la obtención de detalles en las columnas de la estructura, debe cambiar la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a `KeepTrainingCases` y, a continuación, volver a procesar la estructura.  
  
-   Si la estructura de minería de datos no permite la obtención de detalles pero sí lo hace el modelo de minería de datos, solo puede ver la información de los casos de modelos y no de la estructura de minería de datos.  
  
###  <a name="bkmk_Security"></a>Problemas de seguridad para la obtención de detalles  
 Si desea obtener detalles de los casos de estructura del modelo, debe comprobar que la estructura de minería de datos y el modelo de minería de [](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) datos tienen la propiedad `True`AllowDrillThrough establecida en. Es más, debe ser miembro de un rol con los permisos de obtención de detalles para la estructura y el modelo. Para obtener información sobre cómo crear roles, vea [Diseñador de funciones &#40;Analysis Services - Datos multidimensionales&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx). vea.  
  
 Los permisos de obtención de detalles se establecen por separado en la estructura y en el modelo. El permiso del modelo le permite obtener detalles del modelo, aunque no tenga permisos en la estructura. Los permisos de obtención de detalles en la estructura ofrecen la posibilidad adicional de incluir columnas de la estructura en las consultas de obtención de detalles del modelo, mediante la función [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx).  
  
> [!NOTE]  
>  Si habilita la obtención de detalles en la estructura de minería de datos y el modelo de minería de datos, cualquier usuario que sea miembro de un rol con permisos de obtención de detalles en el modelo de minería de datos, podrá ver también las columnas en la estructura de minería de datos, aun cuando esas columnas no estén incluidas en el modelo de minería de datos. Por consiguiente, para proteger los datos confidenciales, debe preparar la vista del origen de datos de manera que enmascare la información personal y permita el acceso para la obtención de detalles en la estructura de minería de datos solo cuando sea necesario.  
  
###  <a name="bkmk_Limits"></a>Limitaciones en la obtención de detalles  
  
-   Las siguientes limitaciones se aplican a las operaciones de obtención de detalles en un modelo, dependiendo del algoritmo utilizado para crearlo:  
  
|Nombre del algoritmo|Problema|  
|--------------------|-----------|  
|Algoritmo Bayes Naïve de Microsoft|No compatible. Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de red neuronal de Microsoft|No compatible. Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de regresión logística de Microsoft|No compatible. Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de regresión lineal de Microsoft| Se admite. Sin embargo, dado que el modelo crea un nodo único, `All`, la obtención de detalles devuelve todos los casos de entrenamiento para el modelo. Si el conjunto de entrenamiento es grande, la carga de resultados puede tardar mucho tiempo.|  
|Algoritmo de serie temporal de Microsoft| Se admite. Sin embargo, no puede obtener información de estructuras o casos mediante el **Visor de modelos de minería de datos** en el Diseñador de minería de datos. En su lugar, debe crear una consulta de DMX.<br /><br /> Tampoco puede obtener detalles de nodos específicos, ni escribir una consulta DMX para recuperar casos en nodos específicos de un modelo de serie temporal. Puede recuperar datos de casos del modelo o la estructura usando otros criterios, como valores de fecha o de atributo.<br /><br /> También puede devolver las fechas de los casos del modelo mediante la función [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx).<br /><br /> Si quiere ver detalles de los nodos ARTXP y ARIMA creados por el algoritmo de serie temporal de Microsoft, puede usar el [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).|  
  
##  <a name="bkmk_Tasks"></a> Tareas relacionadas  
 Use los vínculos siguientes para trabajar con la obtención de detalles en escenarios concretos.  
  
|Tarea|Vínculo|  
|----------|----------|  
|Procedimiento que describe el uso de la obtención de detalles en el Diseñador de minería de datos|[Obtener detalles de datos de caso a partir de un modelo de minería de datos](drill-through-to-case-data-from-a-mining-model.md)|  
|Para modificar un modelo de minería de datos existente de tal forma que permita la obtención de detalles|[Habilitar la obtención de detalles para un modelo de minería](enable-drillthrough-for-a-mining-model.md)|  
|Habilitar la obtención de detalles en una estructura de minería de datos mediante la cláusula DMX WITH DRILLTHROUGH|[CREAR ESTRUCTURA DE MINERÍA DE DATOS &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)|  
|Para obtener información sobre cómo asignar permisos que se aplican a la obtención de detalles en estructuras y modelos de minería de datos|[Conceder permisos para estructuras y modelos de minería de datos &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)   
 [Consultas de minería de datos](data-mining-queries.md)  
  
  
