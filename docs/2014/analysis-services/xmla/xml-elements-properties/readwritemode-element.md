---
title: Elemento ReadWriteMode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3577feacc65bc1d7259d95af9b5bc6179e72b3b9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285791"
---
# <a name="readwritemode-element"></a>Elemento ReadWriteMode
  La propiedad de base de datos `ReadWriteMode` especifica si la base de datos está en modo `ReadWrite` o en modo `ReadOnly`. Éstos son los dos únicos valores posibles de la propiedad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|ReadWrite|  
|Cardinalidad|0-1: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](database-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Las bases de datos se crean únicamente en el modo `ReadWrite`. Las bases de datos no se pueden crear en el modo `ReadOnly`.  
  
 El valor del elemento `ReadWriteMode` se limita a las cadenas listadas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*ReadOnly*|No se pueden aplicar cambios o actualizaciones a la base de datos.|  
|*Lectura y escritura*|Se pueden aplicar cambios o actualizaciones a la base de datos.|  
  
## <a name="see-also"></a>Vea también  
 [Elemento Attach](../xml-elements-commands/attach-element.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover una base de datos de Analysis Services](../../multidimensional-models/move-an-analysis-services-database.md)   
 [ReadWriteModes de base de datos](../../multidimensional-models/database-readwritemodes.md)   
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
