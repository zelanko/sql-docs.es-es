---
description: InheritTypeEnum
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 37c6eba57eb7efb05d2b718e294e33b9616cac77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984106"
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