---
title: Cambiar el nombre de usuario sys | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 959eb9877fa4b73ff9bd307019976a05514b8f8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106034"
---
# <a name="rename-user-sys"></a>Cambiar el nombre de usuario del sistema
  El Asesor de actualizaciones ha detectado el nombre de usuario **sys** en una base de datos. Este nombre está reservado. Cambie el nombre del usuario antes de actualizar. Si no se cambia el nombre del usuario, la base de datos quedará en estado sospechoso y no estará disponible hasta que se ponga en línea.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 El usuario **sys** está reservado.  
  
## <a name="corrective-action"></a>Acción correctora  
  
### <a name="before-upgrade-procedure"></a>Procedimiento antes de la actualización  
 Antes de actualizar, en cada base de datos que contenga el usuario **sys**, haga lo siguiente:  
  
1.  Cree un nuevo usuario.  
  
2.  Utilice la siguiente instrucción para mostrar todos los permisos concedidos por el usuario **sys** y concedidos al usuario **sys**.  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  Para transferir al nuevo usuario la propiedad de todos los objetos pertenecientes a **sys** , utilice **sp_changeobjectowner**.  
  
4.  Quite el usuario **sys**.  
  
5.  Para restaurar los permisos originales capturados en el paso 2, utilice la cláusula AS *new_user* de la instrucción GRANT.  
  
6.  Modifique los scripts que hacen referencia al nuevo usuario. Por ejemplo, los scripts que contengan instrucciones como `SELECT * FROM sys.my`_`table` se deben cambiar a `SELECT * FROM new_user.my_table`.  
  
### <a name="after-upgrade-procedure"></a>Procedimiento después de la actualización  
 Si no se ha cambiado el nombre del usuario **sys** antes de la actualización, haga lo siguiente:  
  
1.  Ejecute la instrucción `ALTER DATABASE db_name SET ONLINE`. La base de datos estará en modo SINGLE_USER.  
  
2.  Siga todos los pasos de la sección Procedimiento antes de la actualización.  
  
3.  Ejecute la instrucción `ALTER DATABASE db_name SET MULTI_USER`.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
