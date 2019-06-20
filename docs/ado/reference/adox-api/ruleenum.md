---
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 77d488bd128f4f5cfa905586f2130cd90be6354c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705837"
---
# <a name="ruleenum"></a>RuleEnum
Especifica la regla para seguir cuando un [clave](../../../ado/reference/adox-api/key-object-adox.md) se elimina.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Realizar cambios en cascada.|  
|**adRINone**|0|Predeterminado: No se realiza ninguna acción.|  
|**adRISetDefault**|3|Valor de clave externa se establece en el valor predeterminado.|  
|**adRISetNull**|2|Valor de clave externa se establece en null.|  
  
## <a name="applies-to"></a>Se aplica a  
 [DeleteRule (propiedad, ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
