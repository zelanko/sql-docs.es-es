---
title: "MODIFICAR la especificación de auditoría de base de datos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_AUDIT_SPECIFICATION_TSQL
- ALTER DATABASE AUDIT SPECIFICATION
- ALTER_DATABASE_AUDIT_TSQL
- ALTER DATABASE AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER DATABASE AUDIT SPECIFICATION statement
ms.assetid: 85f4e7e6-a330-4de0-9048-64f386ccc314
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06d58a9ecce3175e021e7db484aeadbe41f3b372
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica un objeto de especificación de auditoría de base de datos usando la característica Auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } (   
           { <audit_action_specification> | audit_action_group_name }   
                )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      <action_specification>[ ,...n ] ON [ class :: ] securable   
     BY principal [ ,...n ]   
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *audit_specification_name*  
 El nombre de la especificación de auditoría.  
  
 *audit_name*  
 Nombre de la auditoría a la que se aplica esta especificación.  
  
 *audit_action_specification*  
 Nombre de una o varias acciones de auditoría de nivel de base de datos. Para obtener una lista de grupos de acciones de auditoría, consulte [acciones y grupos de acciones de auditoría de SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *audit_action_group_name*  
 Nombre de uno o varios grupos de acciones de auditoría de nivel de base de datos. Para obtener una lista de grupos de acciones de auditoría, consulte [acciones y grupos de acciones de auditoría de SQL Server](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
 *clase*  
 Nombre de clase (si procede) en el objeto protegible.  
  
 *elemento protegible*  
 Tabla, vista u otro objeto protegible de la base de datos al que se debe aplicar la acción de auditoría o el grupo de acciones de auditoría. Para más información, consulte [Securables](../../relational-databases/security/securables.md).  
  
 *columna*  
 Nombre de columna (si procede) en el objeto protegible.  
  
 *entidad de seguridad*  
 Nombre de la entidad de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se debe aplicar la acción de auditoría o el grupo de acciones de auditoría. Para obtener más información, consulte [entidades de seguridad &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).  
  
 CON **(** ESTADO  **=**  {ON | {OFF} **)**  
 Habilita o deshabilita la recopilación de registros por parte de la auditoría para esta especificación de auditoría. Los cambios de estado de la especificación de auditoría se deben realizar fuera de una transacción de usuario y no puede haber otros cambios en la misma instrucción cuando la transición es de ON a OFF.  
  
## <a name="remarks"></a>Comentarios  
 Las especificaciones de auditoría de base de datos son objetos no protegibles que residen en una base de datos determinada. Debe establecer el estado de una especificación de auditoría en OFF para realizar cambios en una base de datos de la especificación de auditoría. Si se ejecuta ALTER DATABASE AUDIT SPECIFICATION cuando una auditoría está habilitada con opciones distintas de STATE=OFF, aparecerá un mensaje de error. Para obtener más información, consulte [tempdb Database](../../relational-databases/databases/tempdb-database.md).  
  
## <a name="permissions"></a>Permissions  
 Los usuarios con el permiso ALTER ANY DATABASE AUDIT pueden modificar las especificaciones de auditoría de base de datos y enlazarlas a cualquier auditoría.  
  
 Una vez creada una especificación de auditoría de base de datos, se puede ver las entidades de seguridad con el servidor de CONTROL, o permisos ALTER ANY DATABASE AUDIT, la cuenta de administrador del sistema o que tengan acceso explícito a la auditoría de entidades de seguridad.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica una especificación de auditoría de base de datos denominada `HIPPA_Audit_DB_Specification` en la que se auditan las instrucciones `SELECT` emitidas por el usuario `dbo` para una auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada `HIPPA_Audit`.  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPPA_Audit_DB_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 Para obtener un ejemplo completo sobre cómo crear una auditoría, consulte [SQL Server Audit &#40; motor de base de datos &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREAR especificación de auditoría de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREAR especificación de auditoría de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  

