---
title: REVOKE (permisos de entidad de seguridad de servidor de Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, impersonation
- permissions [SQL Server], impersonation
- permissions [SQL Server], logins
- impersonate [SQL Server], revoking
- logins [SQL Server], revoking
- REVOKE statement, logins
ms.assetid: 75409024-f150-4326-af16-9d60e900df18
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d297d1e51c4f14393da86b68fdd76a610f9ddde9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="revoke-server-principal-permissions-transact-sql"></a>REVOKE (permisos de entidad de seguridad de servidor de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca los permisos concedidos o denegados para un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    { FROM | TO } <server_principal> [ ,...n ]  
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
 *permission*  
 Especifica un permiso que se puede revocar en un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 LOGIN **::** *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se va a revocar el permiso. Se necesita el calificador de ámbito (**::**).  
  
 SERVER ROLE **::** *server_role*  
 Especifica el rol de servidor para el que se revoca el permiso. El calificador de ámbito (**::**) es obligatorio.  
  
 { FROM | TO } \<server_principal> Especifica el inicio de sesión o el rol de servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde el que se va a revocar el permiso.  
  
 *SQL_Server_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde un inicio de sesión de Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a un certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a una clave asimétrica.  
  
 *server_role*  
 Especifica el nombre de un rol de servidor definido por el usuario.  
  
 GRANT OPTION  
 Indica que se revocará el derecho de conceder el permiso especificado a otras entidades de seguridad. No se revocará el permiso.  
  
> [!IMPORTANT]  
>  Si la entidad de seguridad dispone del permiso especificado sin la opción GRANT, se revocará el permiso.  
  
 CASCADE  
 Indica que el permiso que se va a revocar también se revocará de otras entidades de seguridad a las que esta entidad de seguridad ha concedido o denegado permisos.  
  
> [!CAUTION]  
>  Una revocación en cascada de un permiso concedido WITH GRANT OPTION revocará tanto GRANT como DENY de dicho permiso.  
  
 AS *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del que la entidad de seguridad que ejecuta esta consulta deriva su derecho para revocar el permiso.  
  
## <a name="remarks"></a>Notas  
 Los roles de servidor y los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son protegibles en el nivel de servidor. La mayoría de permisos limitados y específicos que se pueden revocar para un rol de servidor o un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestran en la siguiente tabla, junto con los permisos más generales que los incluyen por implicación.  
  
|Permiso de rol de servidor o de inicio de sesión de SQL Server|Permiso de rol de servidor o inicio de sesión implícito de SQL Server|Implícito en el permiso de servidor|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permisos  
 Para los inicios de sesión, se necesita el permiso CONTROL en el inicio de sesión o el permiso ALTER ANY LOGIN en el servidor.  
  
 Para los roles de servidor, se necesita el permiso CONTROL en el rol de servidor o el permiso ALTER ANY SERVER ROLE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-revoking-impersonate-permission-on-a-login"></a>A. Revocar el permiso IMPERSONATE en un inicio de sesión  
 En el siguiente ejemplo se revoca el permiso `IMPERSONATE` para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `WanidaBenshoof` desde un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde el usuario de Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
REVOKE IMPERSONATE ON LOGIN::WanidaBenshoof FROM [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-with-cascade"></a>B. Revocar el permiso VIEW DEFINITION con CASCADE  
 En el siguiente ejemplo se revoca el permiso `VIEW DEFINITION` para el inicio de sesión `EricKurjan` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del inicio de sesión `RMeyyappan` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La opción `CASCADE` indica que el permiso `VIEW DEFINITION` para `EricKurjan` también se revocará a las entidades de seguridad a las que `RMeyyappan` concedió el permiso.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON LOGIN::EricKurjan FROM RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-revoking-view-definition-permission-on-a-server-role"></a>C. Revocar el permiso VIEW DEFINITION en un rol de servidor  
 En el siguiente ejemplo se revoca el permiso `VIEW DEFINITION` en el rol de servidor `Sales` al rol de servidor `Auditors`.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Ver también  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [GRANT &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [DENY &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

