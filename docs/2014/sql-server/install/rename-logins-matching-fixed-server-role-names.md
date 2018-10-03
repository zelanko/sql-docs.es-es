---
title: Cambiar el nombre de los inicios de sesión que coincidan con nombres de rol fijo de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c5c46c934dff0e882b50dcf7520ba231ba5187eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181934"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>Cambiar el nombre de los inicios de sesión que coinciden con nombres de roles fijos de servidor
  El Asesor de actualizaciones ha detectado uno o más nombres de inicio de sesión definidos por el usuario que coinciden con los nombres de los roles fijos del servidor. Los nombres de roles fijos de servidor están reservados. Cambie el nombre del inicio de sesión antes de actualizar.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Los siguientes nombres de roles fijos de servidor están reservados y no se pueden usar como nombres de inicio de sesión definidos por el usuario.  
  
-   **sysadmin**  
  
-   **serveradmin**  
  
-   **setupadmin**  
  
-   **securityadmin**  
  
-   **processadmin**  
  
-   **dbcreator**  
  
-   **diskadmin**  
  
-   **bulkadmin**  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de actualizar, siga los pasos que se detallan a continuación:  
  
1.  Registre los identificadores de seguridad (SID) de los inicios de sesión ejecutando la siguiente instrucción.  
  
    ```  
    SELECT name, sid   
    FROM master.dbo.syslogins   
    WHERE name IN('sysadmin', 'serveradmin','setupadmin', 'securityadmin','processadmin', 'dbcreator','diskadmin','bulkadmin')  
    ```  
  
2.  Elimine los inicios de sesión.  
  
3.  Use la **sp_addlogin** procedimiento del sistema para crear nuevos inicios de sesión. Especifique el SID devuelto en el paso 1 en el **@sid** parámetro para cada inicio de sesión correspondiente.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
