---
title: Permisos de grupos de disponibilidad GRANT
description: Concede los permisos en un grupo de disponibilidad AlwaysOn.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0a9954e823ae66017c3a6105f0f0ec27964b7043
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246167"
---
# <a name="grant-availability-group-permissions-transact-sql"></a>Disponibilidad de los permisos de grupo GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Concede los permisos en un grupo de disponibilidad Always On.  
  

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
 *permission*  
 Especifica un permiso que se puede conceder en un grupo de disponibilidad. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 ON AVAILABILITY GROUP **::** _availability_group_name_  
 Especifica el grupo de disponibilidad en el que se va a conceder el permiso. El calificador de ámbito ( **::** ) es obligatorio.  
  
 TO \<server_principal>  
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
  
## <a name="remarks"></a>Observaciones  
 Los permisos del ámbito del servidor solo pueden concederse si la base de datos actual es **master**.  
  
 Encontrará información sobre los grupos de disponibilidad en la vista de catálogo [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md). La información sobre los permisos del servidor está disponible en la vista de catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md), mientras que la información sobre las entidades de seguridad de servidor puede verse en la vista de catálogo [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Un grupo de disponibilidad es un elemento protegible en el nivel servidor. La mayoría de permisos limitados y específicos que se pueden conceder en un grupo de disponibilidad se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de grupos de disponibilidad|Permiso implícito en el grupo de disponibilidad|Implícito en el permiso de servidor|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 Para ver un gráfico de todos los permisos de [!INCLUDE[ssDE](../../includes/ssde-md.md)], consulte [Cartel de permisos del motor de base de datos](https://aka.ms/sql-permissions-poster).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en el grupo de disponibilidad o el permiso ALTER ANY AVAILABILITY GROUP en el servidor.  
  
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
 En el siguiente ejemplo se concede el `CONTROL`permiso en el grupo de disponibilidad`MyAg` para el usuario `PKomosinski`de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. CONTROL permite un control completo de inicio de sesión del grupo de disponibilidad, aunque no es el propietario del mismo. Para cambiar la propiedad de una base de datos, consulte [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [REVOKE Availability Group Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)  [REVOKE &#40;permisos de grupos de disponibilidad de Transact-SQL&#41;]  
 [Disponibilidad de los permisos de grupo DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
