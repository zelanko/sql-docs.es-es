---
title: Configurar las propiedades de grupo de medida | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2f650fd897c68e10044a02d55c08f9545a0e6046
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="configure-measure-group-properties"></a>Configurar las propiedades de los grupos de medida
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Grupos de medidas tienen propiedades que le permiten definir cómo los grupos de medida.  
  
## <a name="measure-group-properties"></a>Propiedades de los grupos de medida  
 Las propiedades de los grupos de medida determinan el comportamiento de todo el grupo de medida y establecen los comportamientos predeterminados de ciertas propiedades de medidas dentro de un grupo de medida.  
  
|Propiedad|Definición|  
|--------------|----------------|  
|**AggregationPrefix**|Se aplica al almacenamiento ROLAP. Asigna un prefijo común a las vistas indizadas en SQL Server, que se usa para almacenar agregaciones para las particiones asociadas con este grupo de medida.|  
|**DataAggregation**|Esta propiedad se reserva para uso futuro y actualmente no tiene ningún efecto. Por lo tanto, se recomienda que no modifique esta configuración.|  
|**Description**|Puede usar esta propiedad para documentar el grupo de medida.|  
|**ErrorConfiguration**|Valores de control de errores configurables para controlar las claves duplicadas, las claves desconocidas, las claves NULL, los límites de error, las acciones tras la detección de errores y el archivo de registro de errores. Vea [Configuración de errores para el procesamiento de cubos, particiones y dimensiones &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md).|  
|**EstimatedRows**|Especifica el número estimado de filas de la tabla de hechos.|  
|**EstimatedSize**|Especifica el tamaño estimado (en bytes) del grupo de medida.|  
|**ID**|Especifica el identificador del objeto.|  
|**IgnoreUnrelatedDimensions**|Determina si las dimensiones no relacionadas están forzadas a su nivel superior cuando los miembros de las dimensiones que no están relacionadas con el grupo de medida se incluyen en una consulta. El valor predeterminado es **True**.|  
|**Nombre**|Nombre de la medida. Esta propiedad es de solo lectura.|  
|**ProactiveCaching**|Valores de control de errores configurables para controlar las claves duplicadas, las claves desconocidas, las claves NULL, los límites de error, las acciones tras la detección de errores y el archivo de registro de errores.|  
|**ProcessingMode**|Indica si la indización y la agregación se deben producir durante o después del procesamiento. Las opciones son Regular y LazyAggregations. LazyAggregations puede usarse para ejecutar la agregación como una tarea en segundo plano.|  
|**ProcessingPriority**|Determina la prioridad de procesamiento del cubo durante las operaciones de fondo, como indizaciones y agregaciones diferidas. El valor predeterminado es **0**.|  
|**StorageLocation**|La ubicación del almacenamiento del sistema de archivos para el grupo de medida. Si no se especifica ningún valor, la ubicación se heredará del cubo que contiene el grupo de medida.|  
|**StorageMode**|El modo de almacenamiento del grupo de medida. Los valores disponibles son MOLAP, ROLAP u HOLAP.|  
|**Tipo**|Especifica el tipo del grupo de medida.|  
  
  
