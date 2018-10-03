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
manager: craigg
ms.openlocfilehash: 81c93601dbc47033618fdc72106d91e1b670fd8c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787053"
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
