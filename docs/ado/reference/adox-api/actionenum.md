---
description: ActionEnum
title: ActionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 02422de45f3e0ec28901678528468dc72f021549
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985926"
---
# <a name="actionenum"></a>ActionEnum
Especifica el tipo de acción que se debe realizar cuando se llama a [SetPermissions](./setpermissions-method-adox.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|Al grupo o al usuario se le denegarán los permisos especificados.|  
|**adAccessGrant**|1|El grupo o usuario tendrá al menos los permisos solicitados.|  
|**adAccessRevoke**|4|Se revocarán todos los derechos de acceso explícitos del grupo o usuario.|  
|**adAccessSet**|2|El grupo o usuario tendrá exactamente los permisos solicitados.|