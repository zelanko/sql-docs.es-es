---
title: Inicios de sesión de SQL Server 6.5 inactivos no se puede actualizar | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- passwords [SQL Server], dormant logins
- dormant logins
- logins [SQL Server], upgrading dormant logins
- identifying dormant logins
- password hashes [SQL Server]
ms.assetid: ebe18a74-0375-4df4-b894-239f8fdabb64
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0381e04ae1df53e5502c49eb17d0823fcf611e89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62645814"
---
# <a name="dormant-sql-server-65-logins-cannot-be-upgraded"></a>No se pueden actualizar los inicios de sesión inactivos de SQL Server 6.5
  El Asesor de actualizaciones detectó un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuya contraseña no se puede actualizar directamente a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para habilitar este inicio de sesión, debe restablecer su contraseña. Puede restablecer la contraseña utilizando ALTER LOGIN.  
  
```  
ALTER LOGIN <login name> WITH PASSWORD = '<new password>' MUST_CHANGE  
```  
  
 La nueva contraseña se validará con la directiva de complejidad de contraseñas del sistema, a menos que la comprobación de directivas esté deshabilitada. Se recomienda utilizar contraseñas complejas y no deshabilitar la comprobación de directivas. La opción MUST_CHANGE obliga al usuario a seleccionar una contraseña nueva. Esto no es necesario, pero es recomendable.  
  
 Puede identificar los inicios de sesión inactivos utilizando la siguiente consulta:  
  
```  
SELECT * FROM sysxlogins WHERE (xstatus & 2048) = 2048;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
