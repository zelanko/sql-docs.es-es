---
title: Grupos de acciones y acciones de SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- audit actions [SQL Server]
- audits [SQL Server], groups
- server-level audit actions [SQL Server]
- SQL Server Audit
- audit-level audit actions [SQL Server]
- database-level audit actions [SQL Server]
- audit action groups [SQL Server]
- audits [SQL Server], actions
ms.assetid: b7422911-7524-4bcd-9ab9-e460d5897b3d
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: deef1b6db596acc7462fbd67eaae827fec759640
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32973680"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>Grupos de acciones y acciones de SQL Server Audit
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La característica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit permite auditar grupos de eventos y eventos individuales de nivel de servidor y de base de datos. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] constan de cero o más elementos de acción de auditoría. Estos elementos pueden ser grupos de acciones, como Server_Object_Change_Group, o acciones individuales tales como las operaciones SELECT en una tabla.  
  
> [!NOTE]  
>  Server_Object_Change_Group incluye CREATE, ALTER y DROP para cualquier objeto de servidor (base de datos o extremo).  
  
 Las auditorías pueden tener las siguientes categorías de acciones:  
  
-   Nivel de servidor. Estas acciones incluyen las operaciones del servidor, como cambios de administración y operaciones de inicio y cierre de sesión.  
  
-   Nivel de base de datos. Estas acciones comprenden operaciones de lenguaje de manipulación de datos (DML) y de lenguaje de definición de datos (DDL).  
  
-   Nivel de auditoría. Son las acciones relacionadas con el proceso de auditoría.  
  
 Algunas acciones realizadas en los componentes de auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se auditan de forma intrínseca en una auditoría concreta, y en estos casos los eventos de auditoría se llevan a cabo automáticamente, ya que el evento se produjo en el objeto primario.  
  
 Las acciones siguientes se auditan de forma intrínseca:  
  
-   Server Audit State Change (al establecer el estado en ON u OFF)  
  
 Los eventos siguientes no se auditan de forma intrínseca:  
  
-   CREATE SERVER AUDIT SPECIFICATION  
  
-   ALTER SERVER AUDIT SPECIFICATION  
  
-   DROP SERVER AUDIT SPECIFICATION  
  
-   CREATE DATABASE AUDIT SPECIFICATION  
  
-   ALTER DATABASE AUDIT SPECIFICATION  
  
-   DROP DATABASE AUDIT SPECIFICATION  
  
 Todas las auditorías están deshabilitadas cuando se crean por primera vez.  
  
## <a name="server-level-audit-action-groups"></a>Grupos de acciones de auditoría de nivel de servidor  
 Los grupos de acciones de auditoría de nivel de servidor son acciones similares a las clases de eventos de Auditoría de seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [SQL Server Event Class Reference](../../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 En la tabla siguiente se describen los grupos de acciones de auditoría de nivel de servidor y se proporciona la clase de eventos de SQL Server equivalente cuando corresponda.  
  
|Nombre del grupo de acciones|Description|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Este evento se desencadena cuando se cambia una contraseña para un rol de aplicación. Equivalente a [Audit App Role Change Password Event Class](../../../relational-databases/event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Este evento se desencadena al crear, modificar o eliminar una auditoría. Este evento se desencadena al crear, modificar o eliminar una especificación de auditoría. Todos los cambios realizados en una auditoría se auditan en ella. Equivalente a [Audit Change Audit Event Class](../../../relational-databases/event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Este evento tiene lugar cuando se emite un comando de copia de seguridad o de restauración. Equivalente a la clase de eventos [Audit Backup and Restore](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md).|  
|BROKER_LOGIN_GROUP|Este evento se provoca para notificar mensajes de auditoría relacionados con la seguridad de transporte de Service Broker. Equivalente a [Audit Broker Login Event Class](../../../relational-databases/event-classes/audit-broker-login-event-class.md).|  
|DATABASE_CHANGE_GROUP|Este evento se desencadena al crear, modificar o quitar una base de datos. Este evento se desencadena al crear, modificar o quitar cualquier base de datos. Equivalente a [Audit Database Management Event Class](../../../relational-databases/event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Este evento se desencadena cuando el usuario de una base de datos independiente cierra la sesión de una base de datos. Equivalente a la clase de eventos de auditoría de cierre de sesión de base de datos.|  
|DATABASE_MIRRORING_LOGIN_GROUP|Este evento se provoca para notificar mensajes de auditoría relacionados con la seguridad de transporte en la creación de reflejo de la base de datos. Equivalente a [Audit Database Mirroring Login Event Class](../../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Este evento se desencadena siempre que se tenga acceso a los objetos de la base de datos tales como el tipo de mensaje, ensamblado o contrato. Este evento se desencadena para cualquier tipo de acceso a cualquier base de datos. Nota: Esto puede generar registros de auditoría de gran tamaño.<br /><br /> Equivalente a [Audit Database Object Access Event Class](../../../relational-databases/event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Este evento se desencadena al ejecutar una instrucción CREATE, ALTER o DROP en objetos de base de datos como, por ejemplo, esquemas. Este evento se desencadena al crear, modificar o quitar cualquier objeto de base de datos. Nota: Esto puede generar grandes cantidades de registros de auditoría.<br /><br /> Equivalente a [Audit Database Object Management Event Class](../../../relational-databases/event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Este evento se provoca al cambiar el propietario de los objetos en el ámbito de la base de datos. Este evento se provoca para cualquier cambio de propiedad de objetos en cualquier base de datos del servidor. Equivalente a [Audit Database Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Este evento se desencadena al emitir una instrucción GRANT, REVOKE o DENY para los objetos de bases de datos, como los ensamblados y los esquemas. Este evento se desencadena para cualquier cambio de permisos de objetos en cualquier base de datos del servidor. Equivalente a [Audit Database Object GDR Event Class](../../../relational-databases/event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Este evento se desencadena cuando se realizan operaciones en una base de datos, como un punto de comprobación o una notificación de consulta de suscripción. Este evento tiene lugar en cualquier operación de base de datos y en cualquier base de datos. Equivalente a [Audit Database Operation Event Class](../../../relational-databases/event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Este evento tiene lugar cuando se utiliza la instrucción ALTER AUTHORIZATION para cambiar el propietario de una base de datos y se comprueban los permisos necesarios para hacerlo. Este evento se desencadena para cualquier cambio de propiedad de base de datos en cualquier base de datos del servidor. Equivalente a [Audit Change Database Owner Event Class](../../../relational-databases/event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Este evento se desencadena cuando una entidad de seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] emite una instrucción GRANT, REVOKE o DENY para un permiso de instrucción (esto se aplica a eventos exclusivos de base de datos, como la concesión de permisos en una base de datos).<br /><br /> Este evento se desencadena para cualquier cambio de permisos de base de datos (GDR) en cualquier base de datos en el servidor. Equivalente a [Audit Database Scope GDR Event Class](../../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Este evento se provoca al crear, modificar o quitar entidades de seguridad, como usuarios, en una base de datos. Equivalente a [Audit Database Principal Management Event Class](../../../relational-databases/event-classes/audit-database-principal-management-event-class.md). También es equivalente a la clase de eventos Audit Add DB Principal, que se produce en los procedimientos almacenados desusados sp_grantdbaccess, sp_revokedbaccess, sp_addPrincipal y sp_dropPrincipal.<br /><br /> Este evento se desencadena al agregar o quitar un rol de base de datos usando los procedimientos almacenados sp_addrole y sp_droprole. Este evento se desencadena al crear, modificar o quitar cualquier entidad de seguridad de base de datos en cualquier base de datos. Equivalente a [Audit Add Role Event Class](../../../relational-databases/event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Este evento se desencadena cuando hay una suplantación en el ámbito de la base de datos, por ejemplo, EXECUTE AS \<principal> o SETPRINCIPAL. Este evento se desencadena para las suplantaciones realizadas en cualquier base de datos. Equivalente a [Audit Database Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Este evento se desencadena cuando se agrega o se quita un inicio de sesión en un rol de base de datos. Esta clase de eventos se desencadena para los procedimientos almacenados sp_addrolemember, sp_changegroup y sp_droprolemember. Este evento se desencadena cuando se produce cualquier cambio en los miembros del rol de base de datos en cualquier base de datos. Equivalente a [Audit Add Member to DB Role Event Class](../../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md).|  
|DBCC_GROUP|Este evento se desencadena cuando una entidad de seguridad emite un comando DBCC. Equivalente a [Audit DBCC Event Class](../../../relational-databases/event-classes/audit-dbcc-event-class.md).|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|Indica que una entidad de seguridad intentó iniciar una sesión en una base de datos independiente y no pudo conseguirlo. Los eventos de esta clase los producen nuevas conexiones o conexiones reutilizadas de un grupo de conexiones. Equivalente a [Audit Login Failed Event Class](../../../relational-databases/event-classes/audit-login-failed-event-class.md).|  
|FAILED_LOGIN_GROUP|Indica que una entidad de seguridad intentó iniciar una sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , pero no lo consiguió. Los eventos de esta clase los producen nuevas conexiones o conexiones reutilizadas de un grupo de conexiones. Equivalente a [Audit Login Failed Event Class](../../../relational-databases/event-classes/audit-login-failed-event-class.md).|  
|FULLTEXT_GROUP|Indica que se produjo un evento de texto completo. Equivalente a [Audit Fulltext Event Class](../../../relational-databases/event-classes/audit-fulltext-event-class.md).|  
|LOGIN_CHANGE_PASSWORD_GROUP|Este evento se desencadena cuando se cambia una contraseña de inicio de sesión mediante la instrucción ALTER LOGIN o el procedimiento almacenado sp_password. Equivalente a [Audit Login Change Password Event Class](../../../relational-databases/event-classes/audit-login-change-password-event-class.md).|  
|LOGOUT_GROUP|Indica que una entidad de seguridad ha finalizado una sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los eventos de esta clase los producen nuevas conexiones o conexiones reutilizadas de un grupo de conexiones. Equivalente a [Audit Logout Event Class](../../../relational-databases/event-classes/audit-logout-event-class.md).|  
|SCHEMA_OBJECT_ACCESS_GROUP|Este evento se desencadena al usar un permiso de objeto en el esquema. Equivalente a [Audit Schema Object Access Event Class](../../../relational-databases/event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Este evento se desencadena al realizar una operación CREATE, ALTER o DROP en un esquema. Equivalente a [Audit Schema Object Management Event Class](../../../relational-databases/event-classes/audit-schema-object-management-event-class.md).<br /><br /> Este evento se desencadena en objetos de esquema. Equivalente a [Audit Object Derived Permission Event Class](../../../relational-databases/event-classes/audit-object-derived-permission-event-class.md).<br /><br /> Este evento se produce al modificar cualquier esquema de cualquier base de datos. Equivalente a [Audit Statement Permission Event Class](../../../relational-databases/event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Este evento se desencadena cuando se comprueban los permisos para cambiar el propietario de un objeto de esquema (como una tabla, un procedimiento o una función). Esto sucede cuando se utiliza la instrucción ALTER AUTHORIZATION para asignar un propietario a un objeto. Este evento se desencadena para cualquier cambio de propiedad de esquema en cualquier base de datos del servidor. Equivalente a [Audit Schema Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Este evento se desencadena al realizar una operación de concesión, denegación o revocación en un objeto de esquema. Equivalente a [Audit Schema Object GDR Event Class](../../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md).|  
|SERVER_OBJECT_CHANGE_GROUP|Este evento se desencadena con las operaciones CREATE, ALTER o DROP en objetos de servidor. Equivalente a [Audit Server Object Management Event Class](../../../relational-databases/event-classes/audit-server-object-management-event-class.md).|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|Este evento se desencadena al cambiar el propietario de los objetos en el ámbito del servidor. Equivalente a [Audit Server Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md).|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|Este evento se desencadena cuando una entidad de seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]emite una instrucción GRANT, REVOKE o DENY para un permiso de objeto de servidor. Equivalente a [Audit Server Object GDR Event Class](../../../relational-databases/event-classes/audit-server-object-gdr-event-class.md).|  
|SERVER_OPERATION_GROUP|Este evento se desencadena al usar operaciones de auditoría de seguridad, como la modificación de la configuración, los recursos, el acceso externo o la autorización. Equivalente a [Audit Server Operation Event Class](../../../relational-databases/event-classes/audit-server-operation-event-class.md).|  
|SERVER_PERMISSION_CHANGE_GROUP|Este evento se desencadena al emitir una instrucción GRANT, REVOKE o DENY para los permisos en el ámbito del servidor, como la creación de un inicio de sesión. Equivalente a [Audit Server Scope GDR Event Class](../../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md).|  
|SERVER_PRINCIPAL_CHANGE_GROUP|Este evento se desencadena al crear, modificar o quitar entidades de seguridad de servidor. Equivalente a [Audit Server Principal Management Event Class](../../../relational-databases/event-classes/audit-server-principal-management-event-class.md).<br /><br /> Este evento se desencadena cuando una entidad de seguridad emite los procedimientos almacenados sp_defaultdb o sp_defaultlanguage o las instrucciones ALTER LOGIN. Equivalente a [Audit Addlogin Event Class](../../../relational-databases/event-classes/audit-addlogin-event-class.md).<br /><br /> Este evento se desencadena en los procedimientos almacenados sp_addlogin y sp_droplogin. También es equivalente a [Audit Login Change Property Event Class](../../../relational-databases/event-classes/audit-login-change-property-event-class.md).<br /><br /> Este evento se desencadena para los procedimientos almacenados sp_grantlogin y sp_revokelogin. Equivalente a [Audit Login GDR Event Class](../../../relational-databases/event-classes/audit-login-gdr-event-class.md).|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|Este evento se desencadena cuando hay una suplantación en el ámbito del servidor, como EXECUTE AS \<inicioDeSesión>. Equivalente a [Audit Server Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md).|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|Este evento se desencadena cuando se agrega o quita un inicio de sesión en un rol fijo de servidor. Este evento se desencadena para los procedimientos almacenados sp_addsrvrolemember y sp_dropsrvrolemember. Equivalente a [Audit Add Login to Server Role Event Class](../../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md).|  
|SERVER_STATE_CHANGE_GROUP|Este evento se desencadena al modificar el estado del servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Equivalente a [Audit Server Starts and Stops Event Class](../../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que una entidad de seguridad inició una sesión correctamente en una base de datos independiente. Equivalente a la clase de eventos de auditoría correcta de autenticación de base de datos.|  
|SUCCESSFUL_LOGIN_GROUP|Indica que una entidad de seguridad ha iniciado correctamente una sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los eventos de esta clase los producen nuevas conexiones o conexiones reutilizadas de un grupo de conexiones. Equivalente a [Audit Login Event Class](../../../relational-databases/event-classes/audit-login-event-class.md).|  
|TRACE_CHANGE_GROUP|Este evento se desencadena para todas las instrucciones que comprueban el permiso ALTER TRACE. Equivalente a [Audit Server Alter Trace Event Class](../../../relational-databases/event-classes/audit-server-alter-trace-event-class.md).|  
|TRANSACTION_GROUP|Este evento se desencadena para las operaciones de BEGIN TRANSACTION, ROLLBACK TRANSACTION y COMMIT TRANSACTION, tanto en llamadas explícitas a esas instrucciones como en operaciones de transacciones implícitas. Este evento también se desencadena para las UNDO en el caso de instrucciones individuales provocadas por la reversión de una transacción.|  
|USER_CHANGE_PASSWORD_GROUP|Este evento se desencadena cuando la contraseña del usuario de una base de datos independiente se cambia utilizando la instrucción ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Este grupo supervisa los eventos producidos por medio de [sp_audit_write &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md). Normalmente, los desencadenadores o los procedimientos almacenados incluyen llamadas a **sp_audit_write** para habilitar la auditoría de eventos importantes.|  
  
### <a name="considerations"></a>Consideraciones  
 Los grupos de acciones de nivel de servidor cubren las acciones de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por ejemplo, se registrará cualquier comprobación de acceso a un objeto de esquema en cualquier base de datos si se agrega el grupo de acciones apropiado a una especificación de auditoría de servidor. En una especificación de auditoría de base de datos, solo se registran los accesos al objeto de esquema en la base de datos en cuestión.  
  
 Las acciones de nivel de servidor no permiten un filtrado detallado sobre las acciones de nivel de base de datos. Es necesario realizar una auditoría de base de datos, como la de las acciones SELECT en la tabla Customers para los inicios de sesión en el grupo Employee, para implementar un filtrado detallado sobre las acciones. No incluya objetos con ámbito en el servidor, como las vistas del sistema, en una especificación de auditoría de base de datos.  
  
## <a name="database-level-audit-action-groups"></a>Grupos de acciones de auditoría en el nivel de base de datos  
 Los grupos de acciones de auditoría en el nivel de base de datos son acciones similares a las clases de evento de auditoría de seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información sobre las clases de eventos, vea [SQL Server Event Class Reference](../../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 En la tabla siguiente se describen los grupos de acciones de auditoría de nivel de base de datos y se proporciona la clase de eventos de SQL Server equivalente cuando corresponda.  
  
|Nombre del grupo de acciones|Description|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Este evento se desencadena cuando se cambia una contraseña para un rol de aplicación. Equivalente a [Audit App Role Change Password Event Class](../../../relational-databases/event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Este evento se desencadena al crear, modificar o eliminar una auditoría. Este evento se desencadena al crear, modificar o eliminar una especificación de auditoría. Todos los cambios realizados en una auditoría se auditan en ella. Equivalente a [Audit Change Audit Event Class](../../../relational-databases/event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Este evento tiene lugar cuando se emite un comando de copia de seguridad o de restauración. Equivalente a la clase de eventos [Audit Backup and Restore](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_CHANGE_GROUP|Este evento se desencadena al crear, modificar o quitar una base de datos. Equivalente a [Audit Database Management Event Class](../../../relational-databases/event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Este evento se desencadena cuando el usuario de una base de datos independiente cierra la sesión de una base de datos. Equivalente a la clase de eventos [Audit Backup and Restore](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Este evento se desencadena al tener acceso a objetos de bases de datos como certificados y claves asimétricas. Equivalente a [Audit Database Object Access Event Class](../../../relational-databases/event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Este evento se desencadena al ejecutar una instrucción CREATE, ALTER o DROP en objetos de base de datos como, por ejemplo, esquemas. Equivalente a [Audit Database Object Management Event Class](../../../relational-databases/event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Este evento se desencadena cuando se produce un cambio de propietario de los objetos en el ámbito de la base de datos. Equivalente a [Audit Database Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Este evento se desencadena al emitir una instrucción GRANT, REVOKE o DENY para los objetos de bases de datos, como los ensamblados y los esquemas. Equivalente a [Audit Database Object GDR Event Class](../../../relational-databases/event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Este evento se desencadena cuando se realizan operaciones en una base de datos, como un punto de comprobación o una notificación de consulta de suscripción. Equivalente a [Audit Database Operation Event Class](../../../relational-databases/event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Este evento tiene lugar cuando se utiliza la instrucción ALTER AUTHORIZATION para cambiar el propietario de una base de datos y se comprueban los permisos necesarios para hacerlo. Equivalente a [Audit Change Database Owner Event Class](../../../relational-databases/event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Este evento se desencadena cuando un usuario de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] emite una instrucción GRANT, REVOKE o DENY para un permiso de instrucción aplicable solo a eventos exclusivos de base de datos, como la concesión de permisos en una base de datos. Equivalente a [Audit Database Scope GDR Event Class](../../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Este evento se provoca al crear, modificar o quitar entidades de seguridad, como usuarios, en una base de datos. Equivalente a [Audit Database Principal Management Event Class](../../../relational-databases/event-classes/audit-database-principal-management-event-class.md). También es equivalente a la clase de eventos [Audit Add DB User](../../../relational-databases/event-classes/audit-add-db-user-event-class.md), que se produce en los procedimientos almacenados en desuso sp_grantdbaccess, sp_revokedbaccess y sp_adduser sp_dropuser.<br /><br /> Este evento se desencadena al agregar o quitar un rol de base de datos usando los procedimientos almacenados desusados sp_addrole y sp_droprole. Equivalente a [Audit Add Role Event Class](../../../relational-databases/event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Este evento se desencadena cuando hay una suplantación en el ámbito de la base de datos, como EXECUTE AS \<usuario>. Equivalente a [Audit Database Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Este evento se desencadena cuando se agrega o se quita un inicio de sesión en un rol de base de datos. Esta clase de eventos se usa con los procedimientos almacenados sp_addrolemember, sp_changegroup y sp_droprolemember. Equivalente a la clase de eventos [Audit Add Member to DB Role](../../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md).|  
|DBCC_GROUP|Este evento se desencadena cuando una entidad de seguridad emite un comando DBCC. Equivalente a [Audit DBCC Event Class](../../../relational-databases/event-classes/audit-dbcc-event-class.md).|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|Indica que una entidad de seguridad intentó iniciar una sesión en una base de datos independiente y no pudo conseguirlo. Los eventos de esta clase los producen nuevas conexiones o conexiones reutilizadas de un grupo de conexiones. Este evento se desencadena.|  
|SCHEMA_OBJECT_ACCESS_GROUP|Este evento se desencadena al usar un permiso de objeto en el esquema. Equivalente a [Audit Schema Object Access Event Class](../../../relational-databases/event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Este evento se desencadena al realizar una operación CREATE, ALTER o DROP en un esquema. Equivalente a [Audit Schema Object Management Event Class](../../../relational-databases/event-classes/audit-schema-object-management-event-class.md).<br /><br /> Este evento se desencadena en objetos de esquema. Equivalente a [Audit Object Derived Permission Event Class](../../../relational-databases/event-classes/audit-object-derived-permission-event-class.md). También es equivalente a [Audit Statement Permission Event Class](../../../relational-databases/event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Este evento se desencadena cuando se comprueban los permisos para cambiar el propietario de un objeto de esquema, como una tabla, un procedimiento o una función. Esto sucede cuando se utiliza la instrucción ALTER AUTHORIZATION para asignar un propietario a un objeto. Equivalente a [Audit Schema Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Este evento se provoca siempre que se emite una concesión, denegación o revocación en un objeto de esquema. Equivalente a [Audit Schema Object GDR Event Class](../../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que una entidad de seguridad inició una sesión correctamente en una base de datos independiente. Equivalente a la clase de eventos de auditoría correcta de autenticación de base de datos.|  
|USER_CHANGE_PASSWORD_GROUP|Este evento se desencadena cuando la contraseña del usuario de una base de datos independiente se cambia utilizando la instrucción ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Este grupo supervisa los eventos producidos por medio de [sp_audit_write &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md).|  
  
## <a name="database-level-audit-actions"></a>Acciones de auditoría de nivel de base de datos  
 Las acciones de nivel de base de datos admiten la auditoría de acciones específicas directamente en objetos de esquema y de esquema de la base de datos, como por ejemplo tablas, vistas, procedimientos almacenados, funciones, procedimientos almacenados extendidos, colas o sinónimos. No se auditan los tipos, colección de esquemas XML, base de datos y esquema. La auditoría de objetos de esquema se puede configurar en esquema y base de datos, que indica que se auditarán los eventos en todos los objetos de esquema que contiene el esquema especificado o la base de datos. En la tabla siguiente se describen las acciones de auditoría de nivel de base de datos.  
  
|Acción|Description|  
|------------|-----------------|  
|SELECT|Este evento se desencadena al emitir una instrucción SELECT.|  
|UPDATE|Este evento se desencadena al emitir una instrucción UPDATE.|  
|INSERT|Este evento se desencadena al emitir una instrucción INSERT.|  
|Delete|Este evento se desencadena al emitir una instrucción DELETE.|  
|Ejecute|Este evento se desencadena al emitir una instrucción EXECUTE.|  
|RECEIVE|Este evento se desencadena al emitir una instrucción RECEIVE.|  
|REFERENCES|Este evento se desencadena al comprobar un permiso REFERENCES.|  
  
### <a name="considerations"></a>Consideraciones  
*  Las acciones de auditoría de nivel de base de datos no se aplican a las columnas.  
  
*  Cuando el procesador de consultas parametriza la consulta, el parámetro puede aparecer en el registro de eventos de auditoría en lugar de los valores de columna de la consulta. 
 
*  No se registran las instrucciones RPC. 
  
## <a name="audit-level-audit-action-groups"></a>Grupos de acciones de auditoría de nivel de auditoría  
 También es posible auditar las acciones del proceso de auditoría. Esto puede realizarse en el ámbito del servidor o en el ámbito de la base de datos. En el ámbito de la base de datos, solo se produce para las especificaciones de auditoría de base de datos. En la tabla siguiente se describen los grupos de acciones de auditoría de nivel de auditoría.  
  
|Nombre del grupo de acciones|Description|  
|-----------------------|-----------------|  
|AUDIT_ CHANGE_GROUP|Este evento se desencadena al emitir uno de los comandos siguientes:<br /><br /> CREATE SERVER AUDIT<br /><br /> ALTER SERVER AUDIT<br /><br /> DROP SERVER AUDIT<br /><br /> CREATE SERVER AUDIT SPECIFICATION<br /><br /> ALTER SERVER AUDIT SPECIFICATION<br /><br /> DROP SERVER AUDIT SPECIFICATION<br /><br /> CREATE DATABASE AUDIT SPECIFICATION<br /><br /> ALTER DATABASE AUDIT SPECIFICATION<br /><br /> DROP DATABASE AUDIT SPECIFICATION|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Crear una auditoría de servidor y una especificación de auditoría de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
 [Crear una especificación de auditoría de servidor y de auditoría de base de datos](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-transact-sql.md)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-transact-sql.md)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-authorization-transact-sql.md)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
  
  
