---
title: DENEGAR permisos de grupo de disponibilidad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- permissions [SQL Server], availability group
- DENY statement, availability groups
- denying permissions, [SQL Server], availability groups
ms.assetid: bda60b36-a0b9-4c20-80c1-6a5cb1d638a5
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4c51420215c7de26caea8a3feed66d67bb2ba07
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="deny-availability-group-permissions-transact-sql"></a>Disponibilidad de los permisos de grupo DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Deniega permisos en un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DENY permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
        TO < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede denegar en un grupo de disponibilidad. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 EN el grupo de disponibilidad **::***availability_group_name*  
 Especifica el grupo de disponibilidad en el que se va a denegar el permiso. El calificador de ámbito (**::**) es necesario.  
  
 PARA \<entidadseguridadservidor >  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el que se va a denegar el permiso.  
  
 *SQL_Server_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde un inicio de sesión de Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a un certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a una clave asimétrica.  
  
 CASCADE  
 Indica que el permiso que se va a denegar también se denegará a otras entidades de seguridad a las que esta entidad de seguridad ha concedido permisos.  
  
 AS *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del que la entidad de seguridad que ejecuta esta consulta deriva su derecho de denegar el permiso.  
  
## <a name="remarks"></a>Comentarios  
 Se pueden denegar permisos en el ámbito del servidor solo cuando la base de datos actual es **principal**.  
  
 Información acerca de los grupos de disponibilidad está visible en el [sys.availability_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) vista de catálogo. Información acerca de los permisos de servidor está visible en el [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista de catálogo e información sobre las entidades de seguridad de servidor está visible en el [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo.  
  
 Un grupo de disponibilidad es un elemento protegible en el nivel servidor. La mayoría de permisos limitados y específicos que se pueden denegar en un grupo de disponibilidad se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de grupos de disponibilidad|Permiso implícito en el grupo de disponibilidad|Implícito en el permiso de servidor|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en el grupo de disponibilidad o el permiso ALTER ANY AVAILABILTIY GROUP en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-denying-view-definition-permission-on-an-availability-group"></a>A. Denegar el permiso VIEW DEFINITION en un grupo de disponibilidad  
 En el siguiente ejemplo se deniega el permiso `VIEW DEFINITION` en el grupo de disponibilidad `MyAg` para el inicio de sesión `ZArifin`de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master;  
DENY VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-the-cascade-option"></a>B. Denegar el permiso TAKE OWNERSHIP con la opción CASCADE  
 En el siguiente ejemplo se deniega el permiso `TAKE OWNERSHIP` en el grupo de disponibilidad `MyAg` al usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `PKomosinski` con la opción `CASCADE`.  
  
```  
USE master;  
DENY TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Permisos de grupo de disponibilidad REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [Permisos de grupo de disponibilidad de GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Sys.availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
