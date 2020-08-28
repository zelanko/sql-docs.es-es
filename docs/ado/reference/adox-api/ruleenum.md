---
description: RuleEnum
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 66367d872e27629f1bf437961b99908d0c42e9f2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983376"
---
# <a name="ruleenum"></a>RuleEnum
Especifica la regla que se debe seguir cuando se elimina una [clave](./key-object-adox.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Cambios en cascada.|  
|**adRINone**|0|Predeterminada. No se realiza ninguna acción.|  
|**adRISetDefault**|3|El valor de clave externa se establece en el valor predeterminado.|  
|**adRISetNull**|2|El valor de clave externa se establece en NULL.|  
  
## <a name="applies-to"></a>Se aplica a  
 [DeleteRule (propiedad, ADOX)](./deleterule-property-adox.md)