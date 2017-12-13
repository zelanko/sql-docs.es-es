---
title: "Consultas de obtención de detalles (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AllowDrillThrough property
- drillthrough [Analysis Services]
- drillthrough [DMX]
ms.assetid: 246c784b-1b0c-4f0b-96f7-3af265e67051
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d8a4cc823298eb1e1e36dce0141507dc4be05a1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="drillthrough-queries-data-mining"></a>Consultas de obtención de detalles (minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]A *consulta de obtención de detalles* le permite recuperar los detalles de los casos subyacentes o la estructura de datos, mediante el envío de una consulta para el modelo de minería de datos. La obtención de detalles resulta útil para ver los casos usados para entrenar el modelo frente a los casos que se usaron para probarlo, o si desea revisar detalles adicionales de los datos de los casos.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona dos opciones diferentes para la obtención de detalles:  
  
-   Obtener detalles de los **casos del modelo**  
  
     La obtención de detalles de los casos del modelo se usa cuando se desea partir de un patrón específico del modelo, como un clúster o una rama de un árbol de decisión, para ver más detalles sobre los casos individuales.  
  
-   Obtener detalles de los **casos de la estructura**  
  
     La obtención de detalles de los casos de la estructura resulta útil cuando la estructura contiene información que podría no estar disponible en el modelo. Por ejemplo, no usaría información de contacto del cliente en un modelo de agrupación en clústeres ni aunque los datos estuvieran incluidos en la estructura. Sin embargo, después de crear el modelo, puede que desee recuperar información de contacto para los clientes agrupados en un clúster determinado.  
  
 En esta sección se proporcionan ejemplos de cómo puede crear estas consultas.  
  
 [Usar la obtención de detalles en el Diseñador de minería de datos](#bkmk_Designer)  
  
 [Crear consultas de obtención de detalles mediante DMX](#bkmk_DMX)  
  
 [Consideraciones al usar la obtención de detalles](#bkmk_Considerations)  
  
-   [Cuestiones de seguridad](#bkmk_Security)  
  
-   [Limitaciones](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a> Usar la obtención de detalles en el Diseñador de minería de datos  
 Si se ha configurado un modelo de minería de datos para permitir la obtención de detalles y tiene los permisos adecuados, al examinar el modelo puede hacer clic en un nodo en el visor adecuado y recuperar la información detallada sobre los casos de ese nodo concreto.  
  
 [Obtenga detalles de datos de caso a partir de un modelo de minería de datos](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
 Si los casos de entrenamiento se almacenaron en caché al procesar la estructura de minería de datos y dispone de los permisos necesarios, puede devolver información de los casos del modelo y de la estructura de minería de datos, incluso las columnas que no estaban incluidas en el modelo de minería de datos.  
  
##  <a name="bkmk_DMX"></a> Crear consultas de obtención de detalles mediante DMX  
 Puede obtener información detallada de los datos de los casos creando una consulta DMX si tiene los permisos para el modelo o para la estructura. Para obtener ejemplos de la sintaxis para crear las consultas de obtención de detalles en DMX, consulte el siguiente tema:  
  
 [Crear consultas de obtención de detalles usando DMX](../../analysis-services/data-mining/create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a> Consideraciones al usar la obtención de detalles  
  
-   Si usa el Asistente para minería de datos, la opción para habilitar la obtención de detalles en los casos del modelo está en la página final del asistente. La obtención de detalles está deshabilitada de forma predeterminada. Para obtener más información, vea [Finalización del asistente &#40;Asistente para minería de datos&#41;](http://msdn.microsoft.com/library/6aef1548-35eb-42fd-ae87-63650a79eda1).  
  
-   Puede agregar la capacidad de obtener detalles a un modelo de minería de datos existente pero, si lo hace, hay que volver a procesar el modelo para poder obtener detalles de los datos.  
  
-   La obtención de detalles funciona recuperando la información sobre los casos de entrenamiento que se almacenó en memoria caché al procesar la estructura de minería de datos. Por lo tanto, si borró los datos almacenados en caché después de procesar la estructura cambiando la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **ClearAfterProcessing**, la obtención de detalles no funcionará. Para habilitar la obtención de detalles en las columnas de la estructura, debe cambiar la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **KeepTrainingCases** y, después, volver a procesar la estructura.  
  
-   Si la estructura de minería de datos no permite la obtención de detalles pero sí lo hace el modelo de minería de datos, solo puede ver la información de los casos de modelos y no de la estructura de minería de datos.  
  
###  <a name="bkmk_Security"></a> Problemas de seguridad para la obtención de detalles  
 Si desea obtener detalles de los casos de estructura del modelo, debe comprobar que la estructura de minería de datos y el modelo de minería de datos tienen la propiedad [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) establecida en **True**. Es más, debe ser miembro de un rol con los permisos de obtención de detalles para la estructura y el modelo. Para obtener información sobre cómo crear roles, vea [Diseñador de funciones &#40;Analysis Services - Datos multidimensionales&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192). vea.  
  
 Los permisos de obtención de detalles se establecen por separado en la estructura y en el modelo. El permiso del modelo le permite obtener detalles del modelo, aunque no tenga permisos en la estructura. Los permisos de obtención de detalles en la estructura ofrecen la posibilidad adicional de incluir columnas de la estructura en las consultas de obtención de detalles del modelo, mediante la función [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md).  
  
> [!NOTE]  
>  Si habilita la obtención de detalles en la estructura de minería de datos y el modelo de minería de datos, cualquier usuario que sea miembro de un rol con permisos de obtención de detalles en el modelo de minería de datos, podrá ver también las columnas en la estructura de minería de datos, aun cuando esas columnas no estén incluidas en el modelo de minería de datos. Por consiguiente, para proteger los datos confidenciales, debe preparar la vista del origen de datos de manera que enmascare la información personal y permita el acceso para la obtención de detalles en la estructura de minería de datos solo cuando sea necesario.  
  
###  <a name="bkmk_Limits"></a> Limitaciones en la obtención de detalles  
  
-   Las siguientes limitaciones se aplican a las operaciones de obtención de detalles en un modelo, dependiendo del algoritmo utilizado para crearlo:  
  
|Nombre del algoritmo|Problema|  
|--------------------|-----------|  
|Algoritmo Bayes Naïve de Microsoft|No compatible. Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de red neuronal de Microsoft|No compatible. Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de regresión logística de Microsoft|No compatible. Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de regresión lineal de Microsoft|Compatible. Sin embargo, dado que el modelo crea un nodo único, **All**, la obtención de detalles devuelve todos los casos de entrenamiento para el modelo. Si el conjunto de entrenamiento es grande, la carga de resultados puede tardar mucho tiempo.|  
|Algoritmo de serie temporal de Microsoft|Compatible. Sin embargo, no puede obtener información de estructuras o casos mediante el **Visor de modelos de minería de datos** en el Diseñador de minería de datos. En su lugar, debe crear una consulta de DMX.<br /><br /> Tampoco puede obtener detalles de nodos específicos, ni escribir una consulta DMX para recuperar casos en nodos específicos de un modelo de serie temporal. Puede recuperar datos de casos del modelo o la estructura usando otros criterios, como valores de fecha o de atributo.<br /><br /> También puede devolver las fechas de los casos del modelo mediante la función [Lag &#40;DMX&#41;](../../dmx/lag-dmx.md).<br /><br /> Si quiere ver detalles de los nodos ARTXP y ARIMA creados por el algoritmo de serie temporal de Microsoft, puede usar el [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).|  
  
##  <a name="bkmk_Tasks"></a> Tareas relacionadas  
 Use los vínculos siguientes para trabajar con la obtención de detalles en escenarios concretos.  
  
|Tarea|Vínculo|  
|----------|----------|  
|Procedimiento que describe el uso de la obtención de detalles en el Diseñador de minería de datos|[Obtenga detalles de datos de caso a partir de un modelo de minería de datos](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|Para modificar un modelo de minería de datos existente de tal forma que permita la obtención de detalles|[Habilitar la obtención de detalles para un modelo de minería](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|Habilitar la obtención de detalles en una estructura de minería de datos mediante la cláusula DMX WITH DRILLTHROUGH|[CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|Para obtener información sobre cómo asignar permisos que se aplican a la obtención de detalles en estructuras y modelos de minería de datos|[Otorgar permisos para estructuras y modelos de minería de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Vea también  
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
