---
title: InheritTypeEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: InheritTypeEnum
helpviewer_keywords: InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9269c58d9f5c172a6c640668382b00fd66c5dda0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica cómo heredan permisos establecidos con los objetos [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objetos y otros contenedores contenidos en el objeto principal heredan la entrada.|  
|**adInheritContainers**|2|Otros contenedores que se encuentran en el objeto principal heredan la entrada.|  
|**adInheritNone**|0|Predeterminado: Se produce ninguna herencia.|  
|**adInheritNoPropagate**|4|El **marcas adInheritObjects** y **adInheritContainers** marcas no se propagan a una entrada heredada.|  
|**marcas adInheritObjects**|1|Objetos de contenedor no en el contenedor heredan los permisos.|  
  
## <a name="applies-to"></a>Se aplica a  
 [SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
