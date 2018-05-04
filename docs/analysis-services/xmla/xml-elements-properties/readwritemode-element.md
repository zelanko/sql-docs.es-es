---
title: Elemento ReadWriteMode | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 13c64a8c30b3be6a6c31ad9856299a1f3b80ecb2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="readwritemode-element"></a>Elemento ReadWriteMode
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  La propiedad de base de datos **ReadWriteMode** especifica si la base de datos está en modo **ReadWrite** o en modo **ReadOnly** . Éstos son los dos únicos valores posibles de la propiedad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|ReadWrite|  
|Cardinalidad|0-1: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Las bases de datos se crean únicamente en el modo **ReadWrite** . Las bases de datos no se pueden crear en el modo **ReadOnly** .  
  
 El valor del elemento **ReadWriteMode** se limita a las cadenas listadas en la tabla siguiente.  
  
|Value|Description|  
|-----------|-----------------|  
|*Solo lectura*|No se pueden aplicar cambios o actualizaciones a la base de datos.|  
|*Lectura y escritura*|Se pueden aplicar cambios o actualizaciones a la base de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Elemento Attach](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover una base de datos de Analysis Services](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [ReadWriteModes de base de datos](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
