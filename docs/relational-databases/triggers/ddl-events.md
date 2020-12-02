---
description: Eventos DDL
title: Eventos DDL | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 25cdef293ced7b58ea41f71f78a1046c6b5dd0ba
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128632"
---
# <a name="ddl-events"></a>Eventos DDL
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  En las tablas siguientes se indican los eventos DDL que se pueden utilizar para activar un desencadenador DDL o una notificación de eventos. Tenga en cuenta que cada evento corresponde a una instrucción o un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] , con la sintaxis modificada para que incluya un carácter de subrayado (_) entre las palabras clave.  
  
> [!IMPORTANT]  
>  Los procedimientos almacenados del sistema que realizan operaciones similares a DDL también pueden activar desencadenadores DLL y notificaciones de eventos. Pruebe los desencadenadores DDL y las notificaciones de eventos para determinar sus respuestas a los procedimientos almacenados del sistema que se ejecutan. Por ejemplo, tanto la instrucción CREATE TYPE como el procedimiento almacenado **sp_addtype** activarán un desencadenador DDL o una notificación de eventos creada en un evento CREATE_TYPE.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>Instrucciones de DDL que tienen como ámbito el servidor o la base de datos  
 Se pueden crear desencadenadores DDL o notificaciones de eventos para que se activen en respuesta a los eventos siguientes cuando se produzcan en la base de datos en que se crea el desencadenador o la notificación de eventos, o bien en cualquier parte de la instancia del servidor.  
  
:::row:::
    :::column:::
        CREATE_APPLICATION_ROLE (se aplica a la instrucción CREATE APPLICATION ROLE y a **sp_addapprole**). si se crea un esquema, este evento desencadena también un evento CREATE_SCHEMA).
    :::column-end:::
    :::column:::
        ALTER_APPLICATION_ROLE (se aplica a la instrucción ALTER APPLICATION ROLE y a **sp_approlepassword**).
    :::column-end:::
    :::column:::
        DROP_APPLICATION_ROLE (se aplica a la instrucción DROP APPLICATION ROLE y a **sp_dropapprole**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASSEMBLY
    :::column-end:::
    :::column:::
        ALTER_ASSEMBLY
    :::column-end:::
    :::column:::
        DROP_ASSEMBLY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_ASYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION
    :::column-end:::
    :::column:::
        ALTER_AUTHORIZATION_DATABASE (se aplica a la instrucción ALTER AUTHORIZATION cuando se especifica ON DATABASE y a **sp_changedbowner**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CERTIFICATE
    :::column-end:::
    :::column:::
        ALTER_CERTIFICATE
    :::column-end:::
    :::column:::
        DROP_CERTIFICATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CONTRACT
    :::column-end:::
    :::column:::
        DROP_CONTRACT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_DATABASE
    :::column-end:::
    :::column:::
        DENY_DATABASE
    :::column-end:::
    :::column:::
        REVOKE_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_DATABASE_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DENY_DATABASE_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        ALTER_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        DROP_DATABASE_ENCRYPTION_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DEFAULT
    :::column-end:::
    :::column:::
        DROP_DEFAULT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_DEFAULT (se aplica a **sp_bindefault**).
    :::column-end:::
    :::column:::
        UNBIND_DEFAULT (se aplica a **sp_unbindefault**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
        DROP_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROPERTY (se aplica a **sp_addextendedproperty**).
    :::column-end:::
    :::column:::
        ALTER_EXTENDED_PROPERTY (se aplica a **sp_updateextendedproperty**).
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROPERTY (se aplica a **sp_dropextendedproperty**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_CATALOG (se aplica a la instrucción CREATE FULLTEXT CATALOG y a **sp_fulltextcatalog** cuando se especifica *create* ).
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_CATALOG (se aplica a la instrucción ALTER FULLTEXT CATALOG, a **sp_fulltextcatalog** cuando se especifica *start_incremental*, *start_full*, *Stop* o *Rebuild* y a **sp_fulltext_database** cuando se especifica *enable* ).
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_CATALOG (se aplica a la instrucción DROP FULLTEXT CATALOG y a **sp_fulltextcatalog** cuando se especifica *drop* ).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_INDEX (se aplica a la instrucción CREATE FULLTEXT INDEX y a **sp_fulltexttable** cuando se especifica *create* ).
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_INDEX (se aplica a la instrucción ALTER FULLTEXT INDEX, a **sp_fulltextcatalog** cuando se especifica *start_full*, *start_incremental* o *stop* y a **sp_fulltext_column** y **sp_fulltext_table** cuando se especifica cualquier acción que no sea *create* ni *drop* ).
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_INDEX (se aplica a la instrucción DROP FULLTEXT INDEX y a **sp_fulltexttable** cuando se especifica *drop* ).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_STOPLIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_FUNCTION
    :::column-end:::
    :::column:::
        DROP_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX (se aplica a la instrucción ALTER INDEX y a **sp_indexoption**).
    :::column-end:::
    :::column:::
        DROP_INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MASTER_KEY
    :::column-end:::
    :::column:::
        ALTER_MASTER_KEY
    :::column-end:::
    :::column:::
        DROP_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        ALTER_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        DROP_MESSAGE_TYPE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        DROP_PARTITION_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        ALTER_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        DROP_PARTITION_SCHEME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PLAN_GUIDE (se aplica a **sp_create_plan_guide**).
    :::column-end:::
    :::column:::
        ALTER_PLAN_GUIDE (se aplica a **sp_control_plan_guide** cuando se especifica ENABLE, ENABLE ALL, DISABLE o DISABLE ALL).
    :::column-end:::
    :::column:::
        DROP_PLAN_GUIDE (se aplica a **sp_control_plan_guide** cuando se especifica DROP o DROP ALL).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PROCEDURE
    :::column-end:::
    :::column:::
        ALTER_PROCEDURE (se aplica a la instrucción ALTER PROCEDURE y a **sp_procoption**).
    :::column-end:::
    :::column:::
        DROP_PROCEDURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_QUEUE
    :::column-end:::
    :::column:::
        ALTER_QUEUE
    :::column-end:::
    :::column:::
        DROP_QUEUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVICE_BINDING
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        RENAME (se aplica a **sp_rename**).
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROLE (se aplica a la instrucción CREATE ROLE, a **sp_addrole** y a **sp_addgroup**).
    :::column-end:::
    :::column:::
        ALTER_ROLE
    :::column-end:::
    :::column:::
        DROP_ROLE (se aplica a la instrucción DROP ROLE, a **sp_droprole** y a **sp_dropgroup**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROUTE
    :::column-end:::
    :::column:::
        ALTER_ROUTE
    :::column-end:::
    :::column:::
        DROP_ROUTE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RULE
    :::column-end:::
    :::column:::
        DROP_RULE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_RULE (se aplica a **sp_bindrule**).
    :::column-end:::
    :::column:::
        UNBIND_RULE (se aplica a **sp_unbindrule**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SCHEMA (se aplica a la instrucción CREATE SCHEMA, a **sp_addrole**, **sp_adduser**, **sp_addgroup** y a **sp_grantdbaccess**).
    :::column-end:::
    :::column:::
        ALTER_SCHEMA (se aplica a la instrucción ALTER SCHEMA y a **sp_changeobjectowner**).
    :::column-end:::
    :::column:::
        DROP_SCHEMA
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        ALTER_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        DROP_SEARCH_PROPERTY_LIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_ROLE
    :::column-end:::
    :::column:::
        ALTER_SERVER_ROLE
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVICE
    :::column-end:::
    :::column:::
        ALTER_SERVICE
    :::column-end:::
    :::column:::
        DROP_SERVICE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        BACKUP_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        RESTORE_SERVICE_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE (para las operaciones de firma en objetos con ámbito no de esquema; base de datos, ensamblado, desencadenador)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE_SCHEMA_OBJECT (para los objetos de ámbito de esquema; procedimientos almacenados, funciones)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE_SCHEMA_OBJECT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX se puede utilizar para los índices espaciales.
    :::column-end:::
    :::column:::
        DROP_INDEX se puede utilizar para los índices espaciales.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_STATISTICS
    :::column-end:::
    :::column:::
        DROP_STATISTICS
    :::column-end:::
    :::column:::
        UPDATE_STATISTICS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_SYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYNONYM
    :::column-end:::
    :::column:::
        DROP_SYNONYM
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TABLE
    :::column-end:::
    :::column:::
        ALTER_TABLE (se aplica a la instrucción ALTER TABLE y a **sp_tableoption**).
    :::column-end:::
    :::column:::
        DROP_TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TRIGGER
    :::column-end:::
    :::column:::
        ALTER_TRIGGER (se aplica a la instrucción ALTER TRIGGER y a **sp_settriggerorder**).
    :::column-end:::
    :::column:::
        DROP_TRIGGER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TYPE (se aplica a la instrucción CREATE TYPE y a **sp_addtype**).
    :::column-end:::
    :::column:::
        DROP_TYPE (se aplica a la instrucción DROP TYPE y a **sp_droptype**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_USER (se aplica a la instrucción CREATE USER, a **sp_adduser** y a **sp_grantdbaccess**).
    :::column-end:::
    :::column:::
        ALTER_USER (se aplica a la instrucción ALTER USER y **sp_change_users_login**).
    :::column-end:::
    :::column:::
        DROP_USER (se aplica a la instrucción DROP USER, a **sp_dropuser** y a **sp_revokedbaccess**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_VIEW
    :::column-end:::
    :::column:::
        ALTER_VIEW
    :::column-end:::
    :::column:::
        DROP_VIEW
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX se puede utilizar para los índices XML.
    :::column-end:::
    :::column:::
        DROP_INDEX se puede utilizar para los índices XML.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        ALTER_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        DROP_XML_SCHEMA_COLLECTION
    :::column-end:::
:::row-end:::
 
## <a name="ddl-statements-that-have-server-scope"></a>Instrucciones de DDL que tienen como ámbito el servidor  
 Se pueden crear desencadenadores DDL o notificaciones de eventos para que se activen en respuesta a los eventos siguientes cuando se produzcan en cualquier parte de la instancia del servidor.  
  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION_SERVER
    :::column-end:::
    :::column:::
        ALTER_SERVER_CONFIGURATION
    :::column-end:::
    :::column:::
        ALTER_INSTANCE (se aplica a **sp_configure** y a **sp_addserver** cuando se especifica una instancia del servidor local).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        ALTER_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        DROP_AVAILABILITY_GROUP
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        ALTER_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        DROP_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE
    :::column-end:::
    :::column:::
        ALTER_DATABASE (se aplica a la instrucción ALTER DATABASE y a **sp_fulltext_database**).
    :::column-end:::
    :::column:::
        DROP_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ENDPOINT
    :::column-end:::
    :::column:::
        ALTER_ENDPOINT
    :::column-end:::
    :::column:::
        DROP_ENDPOINT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_SESSION
    :::column-end:::
    :::column:::
        ALTER_EVENT_SESSION
    :::column-end:::
    :::column:::
        DROP_EVENT_SESSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROCEDURE (se aplica a **sp_addextendedproc**).
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROCEDURE (se aplica a **sp_dropextendedproc**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER (se aplica a **sp_addlinkedserver**).
    :::column-end:::
    :::column:::
        ALTER_LINKED_SERVER (se aplica a **sp_serveroption**).
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER (se aplica a **sp_dropserver** cuando se especifica un servidor vinculado).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER_LOGIN (se aplica a **sp_addlinkedsrvlogin**).
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER_LOGIN (se aplica a **sp_droplinkedsrvlogin**).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LOGIN (se aplica a la instrucción CREATE LOGIN, a **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin** y a **sp_denylogin** cuando se usa en un inicio de sesión inexistente que debe crearse de forma implícita).
    :::column-end:::
    :::column:::
        ALTER_LOGIN (se aplica a la instrucción ALTER LOGIN, a **sp_defaultdb**, **sp_defaultlanguage**, **sp_password** y a **sp_change_users_login** cuando se especifica *Auto_Fix* ).
    :::column-end:::
    :::column:::
        DROP_LOGIN (se aplica a la instrucción DROP LOGIN, a **sp_droplogin**, **sp_revokelogin** y a **xp_revokelogin**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE (se aplica a **sp_addmessage**).
    :::column-end:::
    :::column:::
        ALTER_MESSAGE (se aplica a **sp_altermessage**).
    :::column-end:::
    :::column:::
        DROP_MESSAGE (se aplica a **sp_dropmessage**).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVER (se aplica a **sp_addserver**).
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVER (se aplica a **sp_setnetname**).
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVER (se aplica a **sp_dropserver** cuando se especifica un servidor remoto).
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RESOURCE_POOL
    :::column-end:::
    :::column:::
        ALTER_RESOURCE_POOL
    :::column-end:::
    :::column:::
        DROP_RESOURCE_POOL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_SERVER
    :::column-end:::
    :::column:::
        DENY_SERVER
    :::column-end:::
    :::column:::
        REVOKE_SERVER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        ALTER_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        DROP_WORKLOAD_GROUP
    :::column-end:::
:::row-end:::
 
## <a name="see-also"></a>Vea también  
 [Desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notificaciones de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [Grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
