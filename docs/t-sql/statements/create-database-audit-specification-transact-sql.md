---
title: "CREAR especificación de auditoría de base de datos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE DATABASE AUDIT
- DATABASE_AUDIT_SPECIFICATION_TSQL
- DATABASE AUDIT SPECIFICATION
- CREATE_DATABASE_AUDIT_SPECIFICATION_TSQL
- CREATE_DATABASE_AUDIT_TSQL
- CREATE DATABASE AUDIT SPECIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- database audit specification
- CREATE DATABASE AUDIT SPECIFICATION statement
ms.assetid: 0544da48-0ca3-4a01-ba4c-940e23dc315b
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0148505f91cdf572205f34b3854a3c093f5352d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-audit-specification-transact-sql"></a>CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un objeto de especificación de auditoría de base de datos mediante la característica de auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    FOR SERVER AUDIT audit_name   
        [ { ADD ( { <audit_action_specification> | audit_action_group_name } )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      action [ ,...n ]ON [ class :: ] securable BY principal [ ,...n ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *audit_specification_name*  
 Es el nombre de la especificación de auditoría.  
  
 *audit_name*  
 Es el nombre de la auditoría a la que se aplica esta especificación.  
  
 *audit_action_specification*  
 Es la especificación de acciones de elementos protegibles mediante entidades de seguridad que se deben grabar en la auditoría.  
  
 *acción*  
 Es el nombre de una o varias acciones auditables en el nivel de base de datos. Para obtener una lista de acciones de auditoría, consulte [acciones y grupos de acciones de auditoría de SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *audit_action_group_name*  
 Es el nombre de uno o varios grupos de acciones auditables en el nivel de base de datos. Para obtener una lista de grupos de acciones de auditoría, consulte [acciones y grupos de acciones de auditoría de SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *clase*  
 Es el nombre de clase (si procede) en el objeto protegible.  
  
 *elemento protegible*  
 Es la tabla, vista u otro objeto protegible de la base de datos al que se debe aplicar la acción de auditoría o el grupo de acciones de auditoría. Para más información, consulte [Securables](../../relational-databases/security/securables.md).  
  
 *entidad de seguridad*  
 Es el nombre de base de datos principal en el que se va a aplicar la acción de auditoría o el grupo de acciones de auditoría. Para obtener más información, consulte [entidades de seguridad &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
 WITH ( STATE = { ON | OFF } )  
 Habilita o deshabilita la recopilación de registros por parte de la auditoría para esta especificación de auditoría.  
  
## <a name="remarks"></a>Comentarios  
 Las especificaciones de auditoría de base de datos son objetos no protegibles que residen en una base de datos determinada. Cuando se crea una especificación de auditoría de servidor de base de datos, está en un estado deshabilitado.  
  
## <a name="permissions"></a>Permissions  
 Los usuarios con el permiso `ALTER ANY DATABASE AUDIT` pueden crear especificaciones de auditoría de base de datos y enlazarlas a cualquier auditoría.  
  
 Una vez creada una especificación de auditoría de base de datos, se puede ver las entidades de seguridad con la `CONTROL SERVER`, `ALTER ANY DATABASE AUDIT` permisos, o la `sysadmin` cuenta.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una auditoría de servidor denominada `Payrole_Security_Audit` y una especificación de auditoría de base de datos denominada `Payrole_Security_Audit` que audita las instrucciones `SELECT` y `INSERT` por el usuario `dbo`, para la tabla `HumanResources.EmployeePayHistory` de la base de datos `AdventureWorks2012`.  
  
```  
USE master ;  
GO  
-- Create the server audit.  
CREATE SERVER AUDIT Payrole_Security_Audit  
    TO FILE ( FILEPATH =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;  
GO  
-- Enable the server audit.  
ALTER SERVER AUDIT Payrole_Security_Audit   
WITH (STATE = ON) ;  
GO  
-- Move to the target database.  
USE AdventureWorks2012 ;  
GO  
-- Create the database audit specification.  
CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
FOR SERVER AUDIT Payrole_Security_Audit  
ADD (SELECT , INSERT  
     ON HumanResources.EmployeePayHistory BY dbo )  
WITH (STATE = ON) ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREAR especificación de auditoría de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREAR especificación de auditoría de base de datos (Transact-SQL)](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [QUITE la especificación de auditoría de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sys.fn_get_audit_file &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [Sys.server_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [Sys.server_file_audits &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [Sys.server_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [Sys.server_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [Sys.database_audit_specifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [Sys.database_audit_specification_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [Sys.dm_server_audit_status &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [Sys.dm_audit_actions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Crear una auditoría de servidor y una especificación de auditoría de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  

