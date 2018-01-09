---
title: "Propiedades de la dimensión de base de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d05ca23a224bd7c702bd54ef4355c568cf593327
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="database-dimension-properties"></a>Propiedades de la dimensión de base de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], las características de una dimensión se definen mediante los metadatos de la dimensión, basándose en los valores de varias propiedades de dimensión y en los atributos o jerarquías que están incluidas en la dimensión. En la siguiente tabla se describen las propiedades de dimensión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**AttributeAllMemberName**|Especifica el nombre del miembro Todos de los atributos de una dimensión.|  
|**Intercalación**|Determina la intercalación utilizada por la dimensión.|  
|**CurrentStorageMode**|Contiene el modo de almacenamiento actual de la dimensión.|  
|**DependsOnDimension**|Contiene el Id. de otra dimensión de la que depende la dimensión, si la hubiera.|  
|**Descripción**|Contiene la descripción de la dimensión.|  
|**ErrorConfiguration**|Configuración de control de errores configurable para controlar las claves duplicadas, las claves no conocidas, los límites de error, las acciones tras la detección de errores, el archivo de registro de errores y el control de claves NULL.|  
|**ID**|Contiene el identificador (Id.) único de la dimensión.|  
|**Lenguaje**|Especifica el idioma predeterminado de la dimensión.|  
|**MdxMissingMemberMode**|Determina cómo se gestionan los miembros que faltan en las instrucciones MDX (Expresiones multidimensionales).|  
|**MiningModelID**|Contiene el Id. del modelo de minería de datos al que se asocia la dimensión de minería de datos. Esta propiedad solo se aplica si la dimensión es una dimensión de modelo de minería de datos.|  
|**Nombre**|Especifica el nombre de la dimensión.|  
|**ProactiveCaching**|Define la configuración de almacenamiento en caché automático de la dimensión.|  
|**ProcessingGroup**|Especifica el grupo de procesamiento. Sus valores son ByAttribute o ByTable. Valor predeterminado es **ByAttribute**.|  
|**ProcessingMode**|Indica si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe indizar y agregar durante o después del procesamiento.|  
|**ProcessingPriority**|Determina la prioridad de procesamiento de la dimensión durante operaciones en segundo plano como la agregación diferida, la indización o la agrupación en clústeres.|  
|**Source**|Identifica la vista del origen de datos a la que está enlazada la dimensión.|  
|**StorageMode**|Determina el modo de almacenamiento de la dimensión.|  
|**Tipo**|Especifica el tipo de dimensión.|  
|**UnknownMember**|Indica si el miembro desconocido está visible.|  
|**UnknownMemberName**|Especifica el título, en el idioma predeterminado de la dimensión, del miembro desconocido de la dimensión.|  
|**WriteEnabled**|Indica si las reescrituras de dimensión están disponibles (sujetas a permisos de seguridad).|  
  
> [!NOTE]  
>  Para obtener más información acerca de cómo establecer valores para las propiedades ErrorConfiguration y UnknownMember cuando se trabaja con valores nulos y otros problemas de integridad de datos, vea [controlar problemas de integridad de datos en Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Relaciones de dimensión](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
