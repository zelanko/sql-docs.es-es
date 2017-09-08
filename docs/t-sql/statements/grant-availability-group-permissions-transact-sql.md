---
title: Permisos de grupo de disponibilidad de GRANT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/12/2017
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
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 154c99ddfb9f3a69a4a9eeae35f20c5e9720100d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-availability-group-permissions-transact-sql"></a>Disponibilidad de los permisos de grupo GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Concede permisos para un grupo de disponibilidad AlwaysOn.  
  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
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
 Especifica un permiso que se puede conceder en un grupo de disponibilidad. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 EN el grupo de disponibilidad **::***availability_group_name*  
 Especifica el grupo de disponibilidad en el que se va a conceder el permiso. El calificador de ámbito (**::**) es necesario.  
  
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
  
 Información acerca de los grupos de disponibilidad está visible en el [sys.availability_groups &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) vista de catálogo. Información acerca de los permisos de servidor está visible en el [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista de catálogo e información sobre las entidades de seguridad de servidor está visible en el [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) vista de catálogo.  
  
 Un grupo de disponibilidad es un elemento protegible en el nivel servidor. La mayoría de permisos limitados y específicos que se pueden conceder en un grupo de disponibilidad se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de grupos de disponibilidad|Permiso implícito en el grupo de disponibilidad|Implícito en el permiso de servidor|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 Para un gráfico de todos los [!INCLUDE[ssDE](../../includes/ssde-md.md)] permisos, consulte [Cartel de permisos del motor de base de datos](http://go.microsoft.com/fwlink/?LinkId=229142).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en el grupo de disponibilidad o el permiso ALTER ANY AVAILABILTIY GROUP en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>A. Conceder el permiso VIEW DEFINITION en un grupo de disponibilidad  
 En el siguiente ejemplo se concede el `VIEW DEFINITION`permiso en el grupo de disponibilidad`MyAg` para el inicio de sesión `ZArifin`de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. Conceder el permiso TAKE OWNERSHIP con la opción GRANT  
 En el siguiente ejemplo se concede el permiso `TAKE OWNERSHIP` para el grupo de disponibilidad `MyAg` al usuario `PKomosinski` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con `GRANT OPTION`.  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. Concede el permiso CONTROL para una grupo de disponibilidad  
 En el siguiente ejemplo se concede el `CONTROL`permiso en el grupo de disponibilidad`MyAg` para el usuario `PKomosinski`de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. CONTROL permite un control completo de inicio de sesión del grupo de disponibilidad, aunque no es el propietario del mismo. Para cambiar la propiedad, vea [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Permisos de grupo de disponibilidad REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [DENEGAR permisos de grupo de disponibilidad &#40; Transact-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Sys.availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Vistas de catálogo &#40; grupos de disponibilidad AlwaysOn Transact-SQL &#41; ](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [Permisos &#40; motor de base de datos &#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

