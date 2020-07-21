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
author: rothja
ms.author: jroth
ms.openlocfilehash: c04bbd079de68891cf271ff2ea668696e29a4394
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762806"
---
# <a name="ruleenum"></a>RuleEnum
Especifica la regla que se debe seguir cuando se elimina una [clave](../../../ado/reference/adox-api/key-object-adox.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Cambios en cascada.|  
|**adRINone**|0|Predeterminada. No se realiza ninguna acción.|  
|**adRISetDefault**|3|El valor de clave externa se establece en el valor predeterminado.|  
|**adRISetNull**|2|El valor de clave externa se establece en NULL.|  
  
## <a name="applies-to"></a>Se aplica a  
 [DeleteRule (propiedad, ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
