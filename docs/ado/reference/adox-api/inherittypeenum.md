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
author: rothja
ms.author: jroth
ms.openlocfilehash: f420d7d49ad24188f5210001af1209427478f3f6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746679"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica cómo los objetos heredarán los permisos establecidos con [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Los dos objetos y otros contenedores contenidos en el objeto principal heredan la entrada.|  
|**adInheritContainers**|2|Otros contenedores contenidos en el objeto principal heredan la entrada.|  
|**adInheritNone**|0|Predeterminada. No se produce herencia.|  
|**adInheritNoPropagate**|4|Las marcas **adInheritObjects** y **adInheritContainers** no se propagan a una entrada heredada.|  
|**adInheritObjects**|1|Los objetos que no son contenedores del contenedor heredan los permisos.|  
  
## <a name="applies-to"></a>Se aplica a  
 [SetPermissions (método, ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
