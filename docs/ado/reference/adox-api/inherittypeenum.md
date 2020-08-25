---
description: InheritTypeEnum
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
ms.openlocfilehash: d1fed614d90bbf53fdb2198e3ddd657a1e44acd1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770124"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica cómo los objetos heredarán los permisos establecidos con [SetPermissions](./setpermissions-method-adox.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Los dos objetos y otros contenedores contenidos en el objeto principal heredan la entrada.|  
|**adInheritContainers**|2|Otros contenedores contenidos en el objeto principal heredan la entrada.|  
|**adInheritNone**|0|Predeterminada. No se produce herencia.|  
|**adInheritNoPropagate**|4|Las marcas **adInheritObjects** y **adInheritContainers** no se propagan a una entrada heredada.|  
|**adInheritObjects**|1|Los objetos que no son contenedores del contenedor heredan los permisos.|  
  
## <a name="applies-to"></a>Se aplica a  
 [SetPermissions (método, ADOX)](./setpermissions-method-adox.md)