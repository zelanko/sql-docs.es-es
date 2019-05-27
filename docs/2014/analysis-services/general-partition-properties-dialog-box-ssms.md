---
title: General (cuadro de diálogo Propiedades de partición) (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05d840d4e43d9856dedeb3fd446c8158f23275b4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081070"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>General (cuadro de diálogo Propiedades de la partición, SSMS)
  Use la página **General** del cuadro de diálogo **Propiedades de la partición** en SQL Server Management Studio para establecer las propiedades generales de una partición en un grupo de medida para un cubo de una base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Id. de diseño de agregaciones**|Muestra el identificador del diseño de agregaciones utilizado por la partición.|  
|**Prefijo de agregación**|Muestra el prefijo predeterminado de las instancias de agregación que contiene la partición.|  
|**Marca de tiempo de creación**|Muestra la fecha y hora en que se creó la partición.|  
|**Modo de almacenamiento actual**|Muestra el modo de almacenamiento actual de la partición.<br /><br /> Nota: Este modo puede variar según la configuración del almacenamiento en caché automático para la partición. Para más información sobre almacenamiento en caché automático, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|**Descripción**|Escriba o modifique la descripción de la partición.|  
|**Filas estimadas**|Escriba el número estimado de filas del origen de datos subyacente representadas por la partición. Este valor se utiliza durante el procesamiento para estimar el tiempo y el almacenamiento necesarios para procesar la partición.|  
|**Tamaño estimado**|Muestra el tamaño estimado de la partición.|  
|**ID**|Muestra el identificador de la partición.|  
|**Procesado por última vez**|Muestra la fecha y la hora de la última vez en que se procesó la partición.|  
|**Última actualización de esquema**|Muestra la fecha y la hora de la última vez en que se actualizaron los metadatos de la partición.|  
|**Name**|Muestra el nombre de la partición.|  
|**Modo de procesamiento**|Seleccione el modo de procesamiento para la partición. Para obtener más información acerca del procesamiento de los modos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objetos, vea [procesamiento del objeto de modelo Multidimensional](multidimensional-models/processing-a-multidimensional-model-analysis-services.md).|  
|**Id. de origen de datos remoto**|Muestra el identificador del origen de datos remoto desde el que se recuperan los datos de origen para la partición.<br /><br /> Nota: Esta propiedad contiene un valor únicamente para las particiones remotas.|  
|**segmento**|Muestra la expresión que identifica el segmento de datos representado por la partición.|  
|**Source**|Muestra la tabla o consulta que proporciona el origen de datos para la partición.|  
|**Estado**|Muestra el estado de procesamiento actual de la partición.|  
|**Ubicación de almacenamiento**|Muestra la carpeta en la que se almacenan los datos de la partición.<br /><br /> Nota: Esta propiedad contiene un valor solo si una ubicación de almacenamiento distinta de la ubicación de almacenamiento predeterminada para el [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se especifica la instancia.|  
|**Tipo**|Muestra el tipo de la partición.|  
  
## <a name="see-also"></a>Vea también  
 [Particiones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Particiones remotas](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [Cuadro de diálogo Propiedades de la partición &#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [Selección &#40;cuadro de diálogo Propiedades de la partición&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [Almacenamiento en caché automático &#40;cuadro de diálogo Propiedades de la partición&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [Configuración de errores de procesamiento de dimensiones, particiones y cubos &#40;SSAS - multidimensionales&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
