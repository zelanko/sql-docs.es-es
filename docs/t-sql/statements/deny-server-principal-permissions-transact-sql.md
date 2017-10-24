---
title: DENEGAR permisos de entidad de seguridad de servidor (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15be2bfb51e6cdd9d111f052c62838c3326c61b5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="deny-server-principal-permissions-transact-sql"></a>DENY (permisos de entidad de seguridad de servidor de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deniega los permisos concedidos para un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede denegar en un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 Inicio de sesión **::** *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el que se deniega el permiso. El calificador de ámbito (**::**) es necesario.  
  
 ROL de servidor **::** *server_role*  
 Especifica el rol de servidor para el que se deniega el permiso. El calificador de ámbito (**::**) es necesario.  
  
 PARA \<entidadseguridadservidor >  
 Especifica el rol de servidor o el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el que se va a conceder el permiso.  
  
 PARA *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el que se va a denegar el permiso.  
  
 *SQL_Server_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde un inicio de sesión de Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a un certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a una clave asimétrica.  
  
 *server_role*  
 Especifica el nombre de un rol de servidor.  
  
 CASCADE  
 Indica que el permiso que se va a denegar también se denegará a otras entidades de seguridad a las que esta entidad de seguridad ha concedido permisos.  
  
 AS *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del que la entidad de seguridad que ejecuta esta consulta deriva su derecho de denegar el permiso.  
  
## <a name="remarks"></a>Comentarios  
 Los permisos del ámbito del servidor solamente pueden denegarse si la base de datos actual es maestra.  
  
 Información acerca de los permisos de servidor está disponible en la [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista de catálogo. Información acerca de las entidades de seguridad de servidor está disponible en la [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo.  
  
 Se produce un error en la instrucción DENY si no se especifica CASCADE al denegar un permiso a una entidad de seguridad que se concedió dicho permiso con GRANT OPTION.  
  
 Los roles de servidor y los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son protegibles en el nivel de servidor. La mayoría de permisos limitados y específicos que se pueden denegar para un rol de servidor o un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestran en la siguiente tabla, junto con los permisos más generales que los incluyen por implicación.  
  
|Permiso de rol de servidor o de inicio de sesión de SQL Server|Permiso de rol de servidor o inicio de sesión implícito de SQL Server|Implícito en el permiso de servidor|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permissions  
 Para los inicios de sesión, se necesita el permiso CONTROL en el inicio de sesión o el permiso ALTER ANY LOGIN en el servidor.  
  
 Para los roles de servidor, se necesita el permiso CONTROL en el rol de servidor o el permiso ALTER ANY SERVER ROLE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. Denegar el permiso IMPERSONATE en un inicio de sesión  
 El siguiente ejemplo se deniega `IMPERSONATE` permiso en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión `WanidaBenshoof` a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión creado por el usuario de Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. Denegar el permiso VIEW DEFINITION con CASCADE  
 En el siguiente ejemplo se deniega el permiso `VIEW DEFINITION` para el inicio de sesión `EricKurjan` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al inicio de sesión `RMeyyappan` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La opción `CASCADE` indica que el permiso `VIEW DEFINITION` para `EricKurjan` también se denegará a las entidades de seguridad a las que `RMeyyappan` concedió este permiso.  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. Denegar el permiso VIEW DEFINITION en un rol de servidor  
 En el siguiente ejemplo se deniega el permiso `VIEW DEFINITION` en el rol de servidor `Sales` al rol de servidor `Auditors`.  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Vea también  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [REVOKE &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

