---
title: Obtención de detalles en estructuras de minería de datos | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d2ea3d80496f84330802640ff99d951fd2416bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210043"
---
# <a name="drillthrough-on-mining-structures"></a>Obtención de detalles en estructuras de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La*obtención de detalles* se refiere a la capacidad de consultar un modelo o una estructura de minería de datos y obtener datos detallados que no se exponen en el modelo.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] proporciona dos opciones diferentes para obtener detalles sobre los datos de los casos. Puede obtener detalles tanto de los datos utilizados para generar el modelo de minería de datos como de los datos de origen de la estructura de minería de datos.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Obtención de detalles de los casos del modelo frente a obtención de detalles de la estructura  
 La obtención de detalles de los **casos del modelo** resulta útil para buscar detalles adicionales sobre las reglas, los patrones o los clústeres de un modelo.  
  
 En cambio, la **obtención de detalles de los datos de la estructura** pretende proporcionar acceso a la información que no está disponible en el modelo. Por ejemplo, si dispone de los permisos adecuados, es posible que desee averiguar cuáles fueron las filas de datos utilizadas para entrenar el modelo y cuáles se utilizaron para las pruebas.  
  
 También puede ver los atributos de los datos que no se utilizaron en el análisis, siempre que estos se hayan incluido en la definición de la estructura. Por ejemplo, con frecuencia las estructuras de minería de datos admiten varios tipos diferentes de modelos, y es posible que algunas columnas de la estructura se hayan excluido de un modelo debido a que el tipo de datos era incompatible o los datos no resultaban útiles para el análisis. Por ejemplo, no utilizaría información de contacto del cliente en un modelo de agrupación en clústeres aunque los datos estuvieran incluidos en la estructura, pero si habilita la obtención de detalles obtendrá acceso a esta información sin necesidad de ejecutar consultas independientes en el origen de datos.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>Habilitar la obtención de detalles en los datos de la estructura  
 Para utilizar la obtención de detalles en la estructura de minería de datos, se deben cumplir las condiciones siguientes:  
  
-   La obtención de detalles en el modelo también debe estar habilitada. De forma predeterminada, ambos tipos de obtención de detalles están deshabilitados. Para habilitar la obtención de detalles en el Asistente para minería de datos, seleccione la opción para habilitar la obtención de detalles en los casos del modelo en la página final del asistente. También puede agregar más adelante la capacidad de obtener detalles en un modelo cambiando la propiedad **AllowDrillthrough** .  
  
-   Si crea la estructura de minería de datos mediante DMX, use la cláusula WITH DRILLTHROUGH. Para obtener más información, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md).  
  
-   La obtención de detalles funciona recuperando la información sobre los casos de entrenamiento que se almacenó en memoria caché al procesar la estructura de minería de datos. Por lo tanto, si borra los datos almacenados en caché después de procesar la estructura cambiando la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **ClearAfterProcessing**, la obtención de detalles no funcionará. Para habilitar la obtención de detalles en las columnas de la estructura, debe cambiar la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **KeepTrainingCases** y, después, volver a procesar la estructura.  
  
-   Compruebe que la estructura de minería de datos y el modelo de minería de datos tienen la propiedad [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) establecida en **True**. Es más, debe ser miembro de un rol con los permisos de obtención de detalles para la estructura y el modelo.  
  
## <a name="security-issues-for-drillthrough"></a>Problemas de seguridad para la obtención de detalles  
 Los permisos de obtención de detalles se establecen por separado en la estructura y en el modelo. El permiso del modelo le permite obtener detalles del modelo, aunque no tenga permisos en la estructura. Los permisos de obtención de detalles en la estructura ofrecen la posibilidad adicional de incluir columnas de la estructura en las consultas de obtención de detalles del modelo, mediante la función [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md).  
  
 Para obtener información sobre cómo crear roles y asignar permisos en Analysis Services, vea [Diseñador de funciones &#40;Analysis Services - Datos multidimensionales&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192).  
  
> [!NOTE]  
>  Si habilita la obtención de detalles en la estructura de minería de datos y el modelo de minería de datos, cualquier usuario que sea miembro de un rol con permisos de obtención de detalles en el modelo de minería de datos, podrá ver también las columnas en la estructura de minería de datos, aun cuando esas columnas no estén incluidas en el modelo de minería de datos. Por consiguiente, para proteger los datos confidenciales, debe preparar la vista del origen de datos de manera que enmascare la información personal y permita el acceso para la obtención de detalles en la estructura de minería de datos solo cuando sea necesario.  
  
## <a name="related-tasks"></a>Related Tasks  
 Vea los temas siguientes para obtener más información sobre el uso de la obtención de detalles con los modelos de minería de datos.  
  
|||  
|-|-|  
|Utilizar la obtención de detalles en la estructura desde los visores de modelos de minería de datos|[Usar la obtención de detalles desde los visores de modelos](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|Ver ejemplos de consultas de obtención de detalles para tipos de modelos concretos.|[Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)|  
|Obtener información sobre cómo asignar permisos que se aplican a estructuras de minería de datos y modelos de minería de datos concretos.|[Otorgar permisos para estructuras y modelos de minería de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Vea también  
 [Obtención de detalles en modelos de minería de datos](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
  
