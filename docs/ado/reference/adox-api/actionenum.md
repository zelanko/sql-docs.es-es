---
description: ActionEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c9032dfdb3394e582541f60afce7b930751a5c0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777784"
---
# <a name="actionenum"></a>ActionEnum
Especifica el tipo de acción que se debe realizar cuando se llama a [SetPermissions](./setpermissions-method-adox.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|Al grupo o al usuario se le denegarán los permisos especificados.|  
|**adAccessGrant**|1|El grupo o usuario tendrá al menos los permisos solicitados.|  
|**adAccessRevoke**|4|Se revocarán todos los derechos de acceso explícitos del grupo o usuario.|  
|**adAccessSet**|2|El grupo o usuario tendrá exactamente los permisos solicitados.|