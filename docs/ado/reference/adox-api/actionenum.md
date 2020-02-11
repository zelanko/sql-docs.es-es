---
title: ActionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fad40c6daed6fd86f93da3f658af6a21c33ca762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928622"
---
# <a name="actionenum"></a>ActionEnum
Especifica el tipo de acción que se debe realizar cuando se llama a [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|Al grupo o al usuario se le denegarán los permisos especificados.|  
|**adAccessGrant**|1|El grupo o usuario tendrá al menos los permisos solicitados.|  
|**adAccessRevoke**|4|Se revocarán todos los derechos de acceso explícitos del grupo o usuario.|  
|**adAccessSet**|2|El grupo o usuario tendrá exactamente los permisos solicitados.|
