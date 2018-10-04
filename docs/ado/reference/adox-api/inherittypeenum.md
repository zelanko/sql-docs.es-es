---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 249616f2f08b8b8f6138ce13621d26c5f7af9e1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647813"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica cómo heredan los permisos establecidos con los objetos [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objetos y otros contenedores contenidos en el objeto principal heredan la entrada.|  
|**adInheritContainers**|2|Otros contenedores que se encuentran en el objeto principal heredan la entrada.|  
|**adInheritNone**|0|Predeterminado: Se produce ninguna herencia.|  
|**adInheritNoPropagate**|4|El **marcas adInheritObjects** y **adInheritContainers** marcas no se propagan a una entrada heredada.|  
|**marcas adInheritObjects**|1|Objetos que no son contenedores en el contenedor heredan los permisos.|  
  
## <a name="applies-to"></a>Se aplica a  
 [SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
