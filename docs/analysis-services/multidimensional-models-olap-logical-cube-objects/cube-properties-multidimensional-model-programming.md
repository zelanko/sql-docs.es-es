---
title: "Programación del modelo de propiedades del cubo - multidimensionales | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
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
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 47a4d008318277ff684e1c627549187d9aca797a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="cube-properties---multidimensional-model-programming"></a>Programación del modelo de propiedades del cubo - multidimensionales
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Los cubos tienen un número de propiedades que se pueden establecer para modificar el comportamiento de todo el cubo. Estas propiedades se resumen en la tabla siguiente.  
  
> [!NOTE]  
>  Algunas propiedades se establecen automáticamente cuando se crea el cubo y no se pueden cambiar.  
  
 Para obtener más información sobre cómo establecer propiedades del cubo, consulte [Diseñador de cubos &#40; Analysis Services - datos multidimensionales &#41; ](http://msdn.microsoft.com/library/a6692467-da88-4312-8b03-d812f2ae5a96).  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**AggregationPrefix**|Especifica el prefijo normal que se utiliza para los nombres de agregación.|  
|**Intercalación**|Especifica el identificador de configuración regional (LCID) y la marca de comparación, separados por un carácter de subrayado. por ejemplo, Latin1_General_C1_AS.|  
|**DefaultMeasure**|Contiene una expresión MDX (Expresiones multidimensionales) que define la medida predeterminada para el cubo.|  
|**Descripción**|Proporciona una descripción del cubo, que se puede mostrar en aplicaciones cliente.|  
|**ErrorConfiguration**|Contiene valores de control de errores configurables para controlar claves duplicadas, claves desconocidas, límites de error, acciones al detectar errores, archivos de registro de errores y control de claves nulas.|  
|**EstimatedRows**|Especifica el número de filas estimadas del cubo.|  
|**ID**|Contiene el identificador único (Id.) del cubo.|  
|**Lenguaje**|Especifica el identificador de idioma predeterminado del cubo.|  
|**Nombre**|Especifica el nombre descriptivo del cubo.|  
|**ProactiveCaching**|Define la configuración de almacenamiento en caché automático para el cubo.|  
|**ProcessingMode**|Indica si la indización y la agregación se deben producir durante o después del procesamiento. Opciones son **regular** o **diferida**.|  
|**ProcessingPriority**|Determina la prioridad de procesamiento del cubo durante las operaciones de fondo, como indizaciones y agregaciones diferidas. El valor predeterminado es **0**.|  
|**ScriptCacheProcessingMode**|Indica si la caché de script se debe generar durante o después del procesamiento. Opciones son **regular** y **diferida**.|  
|**ScriptErrorHandlingMode**|Determina el control de errores. Opciones son **IgnoreNone** o **IgnoreAll**|  
|**Source**|Muestra la vista del origen de datos utilizada para el cubo.|  
|**StorageLocation**|Especifica la ubicación de almacenamiento del sistema de archivos para el cubo. Si no se especifica ninguna ubicación, se hereda de la base de datos que contiene el objeto de cubo.|  
|**StorageMode**|Especifica el modo de almacenamiento del cubo. Los valores son **MOLAP**, **ROLAP**, o **HOLAP ***.**|  
|**Visible**|Determina la visibilidad del cubo|  
  
> [!NOTE]  
>  Para obtener más información acerca de cómo establecer valores para la propiedad ErrorConfiguration cuando se trabaja con valores nulos y otros problemas de integridad de datos, vea [controlar problemas de integridad de datos en Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento en caché automático &#40; Particiones &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)  
  
  
