---
title: Propiedades del cubo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Collation property
- ID property
- ErrorConfiguration property
- cubes [Analysis Services], properties
- Description property
- DefaultMeasure property
- ProcessingMode property
- AggregationPrefix property
- EstimatedRows property
- Visible property
- StorageLocation property
- StorageMode property
- ScriptErrorHandlingMode property
- Source property
- ScriptCacheProcessingMode property
- Language property
- Name property
- properties [Analysis Services], cubes
- ProcessingPriority property
- ProactiveCaching property
ms.assetid: 72ca3387-620d-4473-8e23-7fe1f2b3d5bf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2b99362f242ff7f815e9ceb9f67db9c80983c8
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60153999"
---
# <a name="cube-properties"></a>Propiedades del cubo
  Los cubos tienen varias propiedades que se pueden establecer para modificar el comportamiento del cubo. Estas propiedades se resumen en la tabla siguiente.  
  
> [!NOTE]  
>  Algunas propiedades se establecen automáticamente cuando se crea el cubo y no se pueden cambiar.  
  
 Para obtener más información sobre cómo establecer las propiedades de cubo, vea [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](../cube-designer-analysis-services-multidimensional-data.md).  
  
|Property|Descripción|  
|--------------|-----------------|  
|`AggregationPrefix`|Especifica el prefijo normal que se utiliza para los nombres de agregación.|  
|`Collation`|Especifica el identificador de configuración regional (LCID) y la marca de comparación, separados por un carácter de subrayado. por ejemplo, Latin1_General_C1_AS.|  
|`DefaultMeasure`|Contiene una expresión MDX (Expresiones multidimensionales) que define la medida predeterminada para el cubo.|  
|`Description`|Proporciona una descripción del cubo, que se puede mostrar en aplicaciones cliente.|  
|`ErrorConfiguration`|Contiene valores de control de errores configurables para controlar claves duplicadas, claves desconocidas, límites de error, acciones al detectar errores, archivos de registro de errores y control de claves nulas.|  
|`EstimatedRows`|Especifica el número de filas estimadas del cubo.|  
|`ID`|Contiene el identificador único (Id.) del cubo.|  
|`Language`|Especifica el identificador de idioma predeterminado del cubo.|  
|`Name`|Especifica el nombre descriptivo del cubo.|  
|`ProactiveCaching`|Define la configuración de almacenamiento en caché automático para el cubo.|  
|`ProcessingMode`|Indica si la indización y la agregación se deben producir durante o después del procesamiento. Las opciones son **regular** o `lazy`.|  
|`ProcessingPriority`|Determina la prioridad de procesamiento del cubo durante las operaciones de fondo, como indizaciones y agregaciones diferidas. El valor predeterminado es **0**.|  
|`ScriptCacheProcessingMode`|Indica si la caché de script se debe generar durante o después del procesamiento. Las opciones son **regular** y `lazy`.|  
|`ScriptErrorHandlingMode`|Determina el control de errores. Las opciones son `IgnoreNone` o `IgnoreAll`|  
|`Source`|Muestra la vista del origen de datos utilizada para el cubo.|  
|`StorageLocation`|Especifica la ubicación de almacenamiento del sistema de archivos para el cubo. Si no se especifica ninguna ubicación, se hereda de la base de datos que contiene el objeto de cubo.|  
|`StorageMode`|Especifica el modo de almacenamiento del cubo. Los valores son `MOLAP`, `ROLAP`, o `HOLAP``.`|  
|`Visible`|Determina la visibilidad del cubo|  
  
> [!NOTE]  
>  Para obtener más información acerca de cómo establecer valores para la propiedad ErrorConfiguration cuando se trabaja con valores nulos y otros problemas de integridad de datos, vea [controlar problemas de integridad de datos en Analysis Services 2005](https://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento en caché automático &#40;particiones&#41;](partitions-proactive-caching.md)  
  
  
