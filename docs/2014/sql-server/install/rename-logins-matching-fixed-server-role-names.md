---
title: Cambiar el nombre de inicios de sesión que coinciden con nombres de roles fijos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: df9d9e51846e286c67a4773823207524755d15dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72278216"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>Cambiar el nombre de los inicios de sesión que coinciden con nombres de roles fijos de servidor
  El Asesor de actualizaciones ha detectado uno o más nombres de inicio de sesión definidos por el usuario que coinciden con los nombres de los roles fijos del servidor. Los nombres de roles fijos de servidor están reservados. Cambie el nombre del inicio de sesión antes de actualizar.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Los siguientes nombres de roles fijos de servidor están reservados y no se pueden usar como nombres de inicio de sesión definidos por el usuario.  
  
-   **sysadmin**  
  
-   **ServerAdmin**  
  
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
  
3.  Utilice el procedimiento del sistema **sp_addlogin** para crear nuevos inicios de sesión. Especifique el SID devuelto en el paso 1 ** \@** en el parámetro SID para cada inicio de sesión correspondiente.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
