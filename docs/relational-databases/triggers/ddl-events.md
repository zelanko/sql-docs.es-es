---
title: Eventos DDL | Microsoft Docs
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 411eb6c824b073818fbda216ba801d34ee5bcf0b
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="ddl-events"></a>Eventos DDL
  En las tablas siguientes se indican los eventos DDL que se pueden utilizar para activar un desencadenador DDL o una notificación de eventos. Tenga en cuenta que cada evento corresponde a una instrucción o un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] , con la sintaxis modificada para que incluya un carácter de subrayado (_) entre las palabras clave.  
  
> [!IMPORTANT]  
>  Los procedimientos almacenados del sistema que realizan operaciones similares a DDL también pueden activar desencadenadores DLL y notificaciones de eventos. Pruebe los desencadenadores DDL y las notificaciones de eventos para determinar sus respuestas a los procedimientos almacenados del sistema que se ejecutan. Por ejemplo, tanto la instrucción CREATE TYPE como el procedimiento almacenado **sp_addtype** activarán un desencadenador DDL o una notificación de eventos creada en un evento CREATE_TYPE.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>Instrucciones de DDL que tienen como ámbito el servidor o la base de datos  
 Se pueden crear desencadenadores DDL o notificaciones de eventos para que se activen en respuesta a los eventos siguientes cuando se produzcan en la base de datos en que se crea el desencadenador o la notificación de eventos, o bien en cualquier parte de la instancia del servidor.  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE (se aplica a la instrucción CREATE APPLICATION ROLE y a **sp_addapprole**). si se crea un esquema, este evento desencadena también un evento CREATE_SCHEMA).|ALTER_APPLICATION_ROLE (se aplica a la instrucción ALTER APPLICATION ROLE y a **sp_approlepassword**).|DROP_APPLICATION_ROLE (se aplica a la instrucción DROP APPLICATION ROLE y a **sp_dropapprole**).|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE (se aplica a la instrucción ALTER AUTHORIZATION cuando se especifica ON DATABASE y a **sp_changedbowner**).||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPECIFICATION|ALTER_DATABASE_AUDIT_SPECIFICATION|DENY_DATABASE_AUDIT_SPECIFICATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT (se aplica a **sp_bindefault**).|UNBIND_DEFAULT (se aplica a **sp_unbindefault**).||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY (se aplica a **sp_addextendedproperty**).|ALTER_EXTENDED_PROPERTY (se aplica a **sp_updateextendedproperty**).|DROP_EXTENDED_PROPERTY (se aplica a **sp_dropextendedproperty**).|  
|CREATE_FULLTEXT_CATALOG (se aplica a la instrucción CREATE FULLTEXT CATALOG y a **sp_fulltextcatalog** cuando se especifica *create* ).|ALTER_FULLTEXT_CATALOG (se aplica a la instrucción ALTER FULLTEXT CATALOG, a **sp_fulltextcatalog** cuando se especifica *start_incremental*, *start_full*, *Stop*o *Rebuild* y a **sp_fulltext_database** cuando se especifica *enable* ).|DROP_FULLTEXT_CATALOG (se aplica a la instrucción DROP FULLTEXT CATALOG y a **sp_fulltextcatalog** cuando se especifica *drop* ).|  
|CREATE_FULLTEXT_INDEX (se aplica a la instrucción CREATE FULLTEXT INDEX y a **sp_fulltexttable** cuando se especifica *create* ).|ALTER_FULLTEXT_INDEX (se aplica a la instrucción ALTER FULLTEXT INDEX, a **sp_fulltextcatalog** cuando se especifica *start_full*, *start_incremental*o *stop* y a **sp_fulltext_column**y **sp_fulltext_table** cuando se especifica cualquier acción que no sea *create* ni *drop* ).|DROP_FULLTEXT_INDEX (se aplica a la instrucción DROP FULLTEXT INDEX y a **sp_fulltexttable** cuando se especifica *drop* ).|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX (se aplica a la instrucción ALTER INDEX y a **sp_indexoption**).|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE (se aplica a **sp_create_plan_guide**).|ALTER_PLAN_GUIDE (se aplica a **sp_control_plan_guide** cuando se especifica ENABLE, ENABLE ALL, DISABLE o DISABLE ALL).|DROP_PLAN_GUIDE (se aplica a **sp_control_plan_guide** cuando se especifica DROP o DROP ALL).|  
|CREATE_PROCEDURE|ALTER_PROCEDURE (se aplica a la instrucción ALTER PROCEDURE y a **sp_procoption**).|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME (se aplica a **sp_rename**).|||  
|CREATE_ROLE (se aplica a la instrucción CREATE ROLE, a **sp_addrole**y a **sp_addgroup**).|ALTER_ROLE|DROP_ROLE (se aplica a la instrucción DROP ROLE, a **sp_droprole**y a **sp_dropgroup**).|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE (se aplica a **sp_bindrule**).|UNBIND_RULE (se aplica a **sp_unbindrule**).||  
|CREATE_SCHEMA (se aplica a la instrucción CREATE SCHEMA, a **sp_addrole**, **sp_adduser**, **sp_addgroup**y a **sp_grantdbaccess**).|ALTER_SCHEMA (se aplica a la instrucción ALTER SCHEMA y a **sp_changeobjectowner**).|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE (para las operaciones de firma en objetos con ámbito no de esquema; base de datos, ensamblado, desencadenador)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT (para los objetos de ámbito de esquema; procedimientos almacenados, funciones)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX se puede utilizar para los índices espaciales.|DROP_INDEX se puede utilizar para los índices espaciales.|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE (se aplica a la instrucción ALTER TABLE y a **sp_tableoption**).|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER (se aplica a la instrucción ALTER TRIGGER y a **sp_settriggerorder**).|DROP_TRIGGER|  
|CREATE_TYPE (se aplica a la instrucción CREATE TYPE y a **sp_addtype**).|DROP_TYPE (se aplica a la instrucción DROP TYPE y a **sp_droptype**).||  
|CREATE_USER (se aplica a la instrucción CREATE USER, a **sp_adduser**y a **sp_grantdbaccess**).|ALTER_USER (se aplica a la instrucción ALTER USER y **sp_change_users_login**).|DROP_USER (se aplica a la instrucción DROP USER, a **sp_dropuser**y a **sp_revokedbaccess**).|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX se puede utilizar para los índices XML.|DROP_INDEX se puede utilizar para los índices XML.|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>Instrucciones de DDL que tienen como ámbito el servidor  
 Se pueden crear desencadenadores DDL o notificaciones de eventos para que se activen en respuesta a los eventos siguientes cuando se produzcan en cualquier parte de la instancia del servidor.  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE (se aplica a **sp_configure** y a **sp_addserver** cuando se especifica una instancia del servidor local).|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE (se aplica a la instrucción ALTER DATABASE y a **sp_fulltext_database**).|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE (se aplica a **sp_addextendedproc**).|DROP_EXTENDED_PROCEDURE (se aplica a **sp_dropextendedproc**).||  
|CREATE_LINKED_SERVER (se aplica a **sp_addlinkedserver**).|ALTER_LINKED_SERVER (se aplica a **sp_serveroption**).|DROP_LINKED_SERVER (se aplica a **sp_dropserver** cuando se especifica un servidor vinculado).|  
|CREATE_LINKED_SERVER_LOGIN (se aplica a **sp_addlinkedsrvlogin**).|DROP_LINKED_SERVER_LOGIN (se aplica a **sp_droplinkedsrvlogin**).||  
|CREATE_LOGIN (se aplica a la instrucción CREATE LOGIN, a **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**y a **sp_denylogin** cuando se usa en un inicio de sesión inexistente que debe crearse de forma implícita).|ALTER_LOGIN (se aplica a la instrucción ALTER LOGIN, a **sp_defaultdb**, **sp_defaultlanguage**, **sp_password**y a **sp_change_users_login** cuando se especifica *Auto_Fix* ).|DROP_LOGIN (se aplica a la instrucción DROP LOGIN, a **sp_droplogin**, **sp_revokelogin**y a **xp_revokelogin**).|  
|CREATE_MESSAGE (se aplica a **sp_addmessage**).|ALTER_MESSAGE (se aplica a **sp_altermessage**).|DROP_MESSAGE (se aplica a **sp_dropmessage**).|  
|CREATE_REMOTE_SERVER (se aplica a **sp_addserver**).|ALTER_REMOTE_SERVER (se aplica a **sp_setnetname**).|DROP_REMOTE_SERVER (se aplica a **sp_dropserver** cuando se especifica un servidor remoto).|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|ALTER_WORKLOAD_GROUP|DROP_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notificaciones de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [Grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md)  
  
  

