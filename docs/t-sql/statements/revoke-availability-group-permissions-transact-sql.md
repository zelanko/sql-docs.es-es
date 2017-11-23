---
title: Permisos de grupo de disponibilidad REVOKE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
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
- REVOKE statement, availability groups
- revoking permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 02c77378-a36d-4286-9235-d8867a2b92ad
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7bd88af97183e7cb5f3bd36a4bc5194be62a4d6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-availability-group-permissions-transact-sql"></a>Disponibilidad de los permisos de grupo REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Revoca los permisos en un grupo de disponibilidad Always On. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON AVAILABILITY GROUP :: availability_group_name  
    { FROM | TO } < server_principal >  [ ,...n ]  
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
 Especifica un permiso que se puede revocar en un grupo de disponibilidad. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 EN el grupo de disponibilidad **::***availability_group_name*  
 Especifica el grupo de disponibilidad en el que se va a revocar el permiso. El calificador de ámbito (**::**) es necesario.  
  
 {DESDE | A} \<entidadseguridadservidor > especifica el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se va a revocar el permiso de inicio de sesión.  
  
 *SQL_Server_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde un inicio de sesión de Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a un certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica el nombre de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignado a una clave asimétrica.  
  
 GRANT OPTION  
 Indica que se revocará el derecho de conceder el permiso especificado a otras entidades de seguridad. No se revocará el permiso.  
  
> [!IMPORTANT]  
>  Si la entidad de seguridad dispone del permiso especificado sin la opción GRANT, se revocará el permiso.  
  
 CASCADE  
 Indica que el permiso que se va a revocar también se revocará de otras entidades de seguridad a las que esta entidad de seguridad ha concedido o denegado permisos.  
  
> [!IMPORTANT]  
>  Una revocación en cascada de un permiso concedido WITH GRANT OPTION revocará tanto GRANT como DENY de dicho permiso.  
  
 AS *SQL_Server_login*  
 Especifica el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del que la entidad de seguridad que ejecuta esta consulta deriva su derecho para revocar el permiso.  
  
## <a name="remarks"></a>Comentarios  
 Se pueden revocar los permisos del ámbito de servidor solo cuando la base de datos actual es **principal**.  
  
 Información acerca de los grupos de disponibilidad está visible en el [sys.availability_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) vista de catálogo. Información acerca de los permisos de servidor está visible en el [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista de catálogo e información sobre las entidades de seguridad de servidor está visible en el [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo.  
  
 Un grupo de disponibilidad es un elemento protegible en el nivel servidor. La mayoría de permisos limitados y específicos que se pueden revocar en un grupo de disponibilidad se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
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
  
### <a name="a-revoking-view-definition-permission-on-an-availability-group"></a>A. Revocar el permiso VIEW DEFINITION en un grupo de disponibilidad  
 En el siguiente ejemplo se revoca el `VIEW DEFINITION`permiso en el grupo de disponibilidad`MyAg` para el inicio de sesión `ZArifin`de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade"></a>B. Revocar el permiso TAKE OWNERSHIP con la cascada  
 En el siguiente ejemplo se revoca el permiso `TAKE OWNERSHIP` en el grupo de disponibilidad `MyAg` para el usuario [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `PKomosinski` y desde todas las entidades de seguridad a las que `PKomosinski` concedio TAKE OWNERSHIP en MyAg.  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
### <a name="c-revoking-a-previously-granted-with-grant-option-clause"></a>C. Revocar una cláusula WITH GRANT OPTION previamente concedida  
 Si se concede un permiso con WITH GRANT OPTION, use REVOKE GRANT OPTION FOR … Para quitar WITH GRANT OPTION. El siguiente ejemplo concede el permiso y después quita la parte WITH GRANT del mismo.  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
REVOKE GRANT OPTION FOR CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski  
CASCADE  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Permisos de grupo de disponibilidad de GRANT &#40; Transact-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [DENEGAR permisos de grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Sys.availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

