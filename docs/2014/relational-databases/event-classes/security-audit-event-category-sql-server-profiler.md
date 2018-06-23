---
title: Auditoría de seguridad (categoría de eventos, SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
caps.latest.revision: 35
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 67869367f2444e3e432b17e80590a7d0b9c93d42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105858"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Auditoría de seguridad (categoría de eventos, SQL Server Profiler)
  La categoría de eventos **Auditoría de seguridad** contiene eventos de auditoría de seguridad.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Audit Add DB User (clase de eventos)](audit-add-db-user-event-class.md)|Indica que se ha agregado o quitado un inicio de sesión como usuario de base de datos en una base de datos.|  
|[Audit Add Login to Server Role (clase de eventos)](audit-add-login-to-server-role-event-class.md)|Indica que se ha agregado o quitado un inicio de sesión de un rol fijo de servidor.|  
|[Audit Add Member to DB Role (clase de eventos)](audit-add-member-to-db-role-event-class.md)|Indica que se ha agregado o quitado un inicio de sesión de un rol.|  
|[Audit Add Role (clase de eventos)](audit-add-role-event-class.md)|Indica que se ha agregado o quitado un rol de base de datos de una base de datos.|  
|[Audit Addlogin (clase de eventos)](audit-addlogin-event-class.md)|Indica que se ha agregado o quitado un inicio de sesión.|  
|[Audit App Role Change Password (clase de eventos)](audit-app-role-change-password-event-class.md)|Indica que se ha cambiado una contraseña para un rol de aplicación.|  
|[Clase de evento de auditoría de restauración y copia de seguridad](audit-backup-and-restore-event-class.md)|Indica que se ha enviado una instrucción de copia de seguridad o restauración.|  
|[Audit Broker Conversation (clase de eventos)](broker-conversation-event-class.md)|Informa de los mensajes de auditoría relacionados con la seguridad de diálogo de Service Broker.|  
|[Clase de eventos Audit Broker Login](audit-broker-login-event-class.md)|Informa de los mensajes de auditoría relacionados con la seguridad de transporte de Service Broker.|  
|[Audit Change Audit (clase de eventos)](audit-change-audit-event-class.md)|Indica que se ha realizado una modificación de seguimiento de auditoría.|  
|[Audit Change Database Owner (clase de eventos)](audit-change-database-owner-event-class.md)|Indica que se han comprobado los permisos para cambiar el propietario de una base de datos.|  
|[Audit Database Management (clase de eventos)](audit-database-management-event-class.md)|Indica que se ha creado, modificado o quitado una base de datos.|  
|[Audit Database Mirroring Login (clase de eventos)](audit-database-mirroring-login-event-class.md)|Informa de los mensajes de auditoría relacionados con la seguridad en el transporte para la creación del reflejo de una base de datos.|  
|[Audit Database Object Access (clase de eventos)](audit-database-object-access-event-class.md)|Indica que se ha obtenido acceso a un objeto de base de datos, como un esquema.|  
|[Audit Database Object GDR (clase de eventos)](audit-database-object-gdr-event-class.md)|Indica que se ha producido un evento GDR para un objeto de base de datos.|  
|[Audit Database Object Management (clase de eventos)](audit-database-object-management-event-class.md)|Indica que se ha ejecutado una instrucción CREATE, ALTER o DROP en un objeto de base de datos.|  
|[Audit Database Object Take Ownership (clase de eventos)](audit-database-object-take-ownership-event-class.md)|Indica que ha habido un cambio de propietario para objetos en el ámbito de una base de datos.|  
|[Audit Database Operation (clase de eventos)](audit-database-operation-event-class.md)|Indica que se han realizado varias operaciones como la notificación de una consulta de punto de comprobación o suscripción.|  
|[Audit Database Principal Impersonation (clase de eventos)](audit-database-principal-impersonation-event-class.md)|Indica que se ha producido una suplantación en el ámbito de la base de datos.|  
|[Audit Database Principal Management (clase de eventos)](audit-database-principal-management-event-class.md)|Indica que se han creado, modificado o quitado entidades de seguridad en una base de datos.|  
|[Audit Database Scope GDR (clase de eventos)](audit-database-scope-gdr-event-class.md)|Indica que un usuario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ha emitido una instrucción GRANT, REVOKE o DENY para un permiso de instrucción.|  
|[Audit DBCC (clase de eventos)](audit-dbcc-event-class.md)|Indica que se ha emitido un comando DBCC.|  
|[Clase de eventos Audit Fulltext](audit-fulltext-event-class.md)|Indica que se ha producido un evento de texto completo.|  
|[Audit Login Change Password (clase de eventos)](audit-login-change-password-event-class.md)|Indica que un usuario ha cambiado su contraseña de inicio de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Audit Login Change Property (clase de eventos)](audit-login-change-property-event-class.md)|Indica que se ha usado **sp_defaultdb**, **sp_defaultlanguage**o ALTER LOGIN para modificar una propiedad de un inicio de sesión.|  
|[Audit Login (clase de eventos)](audit-login-event-class.md)|Indica que un usuario ha iniciado una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Audit Login Failed (clase de eventos)](audit-login-failed-event-class.md)|Indica que un usuario intentó iniciar una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero no lo consiguió.|  
|[Audit Login GDR (clase de eventos)](audit-login-gdr-event-class.md)|Indica que se ha agregado o quitado un derecho de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|  
|[Audit Logout (clase de eventos)](audit-logout-event-class.md)|Indica que un usuario ha finalizado una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Audit Object Derived Permission (clase de eventos)](audit-object-derived-permission-event-class.md)|Indica que se ha emitido una instrucción CREATE, ALTER o DROP para un objeto.|  
|[Audit Schema Object Access (clase de eventos)](audit-schema-object-access-event-class.md)|Indica que se ha utilizado un permiso de objeto (como SELECT).|  
|[Audit Schema Object GDR (clase de eventos)](audit-schema-object-gdr-event-class.md)|Indica que un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ha emitido una instrucción GRANT, REVOKE o DENY para un permiso de objeto de esquema.|  
|[Audit Schema Object Management (clase de eventos)](audit-schema-object-management-event-class.md)|Indica que se ha creado, modificado o quitado un objeto de servidor.|  
|[Audit Schema Object Take Ownership (clase de eventos)](audit-schema-object-take-ownership-event-class.md)|Indica que se han comprobado los permisos para cambiar el propietario de un objeto de esquema.|  
|[Audit Server Alter Trace (clase de eventos)](audit-server-alter-trace-event-class.md)|Indica que se ha comprobado el permiso ALTER TRACE.|  
|[Audit Server Object GDR (clase de eventos)](audit-server-object-gdr-event-class.md)|Indica que se ha producido un evento GDR para un objeto de esquema.|  
|[Audit Server Object Management (clase de eventos)](audit-server-object-management-event-class.md)|Indica que se ha producido un evento CREATE, ALTER o DROP para un objeto de servidor.|  
|[Audit Server Object Take Ownership (clase de eventos)](audit-server-object-take-ownership-event-class.md)|Indica que ha cambiado el propietario de un objeto de servidor.|  
|[Audit Server Operation (clase de eventos)](audit-server-operation-event-class.md)|Indica que se han realizado operaciones de auditoría en el servidor.|  
|[Audit Server Principal Impersonation (clase de eventos)](audit-server-principal-impersonation-event-class.md)|Indica que se ha producido una suplantación en el ámbito del servidor.|  
|[Audit Server Principal Management (clase de eventos)](audit-server-principal-management-event-class.md)|Indica que se ha emitido una instrucción CREATE, ALTER o DROP para una entidad se seguridad de servidor.|  
|[Audit Server Scope GDR (clase de eventos)](audit-server-scope-gdr-event-class.md)|Indica que se ha producido un evento GDR para permisos de servidor.|  
|[Audit Server Starts and Stops (clase de eventos)](audit-server-starts-and-stops-event-class.md)|Indica que se ha modificado el estado de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Audit Statement Permission (clase de eventos)](audit-statement-permission-event-class.md)|Indica que se ha utilizado un permiso de instrucción.|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Eventos extendidos](../extended-events/extended-events.md)  
  
  