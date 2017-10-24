---
title: Permisos de extremo GRANT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/17/2017
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
- endpoints [SQL Server], permissions
- granting permissions [SQL Server], endpoints
- GRANT statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 9eda885c-fc3a-4c9d-8de6-ce07fb35a934
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6f89febc7d63bcf36c947aacd90337e7f9478c96
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-endpoint-permissions-transact-sql"></a>GRANT (permisos de extremo de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permisos para un extremo.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
GRANT permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede conceder para un extremo. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 EN el extremo de **::***endpoint_name*  
 Especifica el extremo en el que se va a conceder el permiso. El calificador de ámbito (**::**) es necesario.  
  
 PARA \<entidadseguridadservidor >  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el que se va a conceder el permiso.  
  
 *SQL_Server_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde un inicio de sesión de Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a un certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a una clave asimétrica.  
  
 WITH GRANT OPTION  
 Indica que la entidad de seguridad también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
 AS *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del que la entidad de seguridad que ejecuta esta consulta deriva su derecho de conceder el permiso.  
  
## <a name="remarks"></a>Comentarios  
 Se pueden conceder permisos en el ámbito del servidor solo cuando la base de datos actual **principal**.  
  
 Información acerca de los puntos de conexión está visible en el [sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) vista de catálogo. Información acerca de los permisos de servidor está visible en el [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista de catálogo e información sobre las entidades de seguridad de servidor está visible en el [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo.  
  
 Un extremo es un elemento protegible de nivel de servidor. La mayoría de permisos limitados y específicos que se pueden conceder para un extremo se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de extremo|Implicado por el permiso de extremo|Implícito en el permiso de servidor|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en el extremo o el permiso ALTER ANY ENDPOINT en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-granting-view-definition-permission-on-an-endpoint"></a>A. Conceder el permiso VIEW DEFINITION para un extremo  
 En el siguiente ejemplo se concede el permiso `VIEW DEFINITION` para el extremo `Mirror7` al inicio de sesión `ZArifin` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master;  
GRANT VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. Conceder el permiso TAKE OWNERSHIP con la opción GRANT  
 En el siguiente ejemplo se concede el permiso `TAKE OWNERSHIP` para el extremo `Shipping83` al usuario `PKomosinski` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con `GRANT OPTION`.  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [DENEGAR permisos de extremo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [REVOCAR permisos de extremo &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [Vistas de catálogo de puntos de conexión &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Sys.endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

