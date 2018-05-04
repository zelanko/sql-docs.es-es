---
title: Propiedades de la dimensión de base de datos | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31c6ae0dd0bb942860c5518bba7defe2f8eef6c0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="database-dimension-properties"></a>Propiedades de la dimensión de base de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], las características de una dimensión se definen mediante los metadatos de la dimensión, basándose en los valores de varias propiedades de dimensión y en los atributos o jerarquías que están incluidas en la dimensión. En la siguiente tabla se describen las propiedades de dimensión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**AttributeAllMemberName**|Especifica el nombre del miembro Todos de los atributos de una dimensión.|  
|**Intercalación**|Determina la intercalación utilizada por la dimensión.|  
|**CurrentStorageMode**|Contiene el modo de almacenamiento actual de la dimensión.|  
|**DependsOnDimension**|Contiene el Id. de otra dimensión de la que depende la dimensión, si la hubiera.|  
|**Description**|Contiene la descripción de la dimensión.|  
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
 [Atributos y jerarquías de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Relaciones de dimensión](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Dimensiones & #40; Analysis Services - datos multidimensionales & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
