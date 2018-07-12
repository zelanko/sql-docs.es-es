---
title: Desencadenadores logon | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b42fdfa556a2e7a26a04dd85fd7740ca23d36967
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427204"
---
# <a name="logon-triggers"></a>Desencadenadores logon
  Los desencadenadores LOGON activan procedimientos almacenados en respuesta a un evento LOGON. Este evento se genera cuando se establece una sesión de usuario con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los desencadenadores logon se activan después de que termine la fase de autenticación del inicio de sesión, pero antes de que se establezca la sesión de usuario realmente. Por tanto, todos los mensajes que se originan dentro del desencadenador y que normalmente llegarían hasta el usuario, como los mensajes de error y los mensajes de la instrucción PRINT, se desvían al registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los desencadenadores logon no se activan si se produce un error en la autenticación.  
  
 Puede utilizar desencadenadores logon para realizar auditorías y controlar sesiones de servidor, como el seguimiento de la actividad de inicio de sesión, la restricción de inicios de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o la limitación del número de sesiones para un inicio de sesión específico. Por ejemplo, en el siguiente código, el desencadenador LOGON rechaza los intentos de iniciar sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciados por el inicio de sesión *login_test* si ya hay tres sesiones de usuario creadas por dicho inicio de sesión.  
  
 [!code-sql[TriggerDDL#LogonTrigger1](../../snippets/tsql/SQL14/tsql/triggerddl/transact-sql/snippet_create_alter_drop_trigger.sql#logontrigger1)]  
  
 Tenga en cuenta que el evento LOGON se corresponde con el evento de seguimiento de SQL AUDIT_LOGIN, que se puede usar en [notificaciones de eventos](../service-broker/event-notifications.md). La diferencia principal entre los desencadenadores y las notificaciones de eventos radica en que los desencadenadores se generan de forma sincrónica con los eventos, mientras que las notificaciones de eventos son asincrónicas. Esto significa, por ejemplo, que si desea que no se establezca una sesión, debe utilizar un desencadenador logon. Para este fin, no se puede usar una notificación de eventos en un evento AUDIT_LOGIN.  
  
## <a name="specifying-first-and-last-trigger"></a>Especificar el primer y el último desencadenador  
 Se pueden definir varios desencadenadores en el evento LOGON. Cualquiera de estos desencadenadores se puede designar como el primero o el último en activarse en un evento mediante el procedimiento almacenado del sistema [sp_settriggerorder](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql) . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no garantiza el orden de ejecución del resto de desencadenadores.  
  
## <a name="managing-transactions"></a>Administrar transacciones  
 Antes de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] active un desencadenador logon, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una transacción implícita que es independiente de cualquier transacción de usuario. Por consiguiente, cuando el primer desencadenador LOGON inicia la activación, el recuento de transacciones es 1. Una vez que todos los desencadenadores LOGON finalizan su ejecución, se confirma la transacción. Al igual que ocurre con otros tipos de desencadenadores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error si un desencadenador LOGON termina de ejecutarse con un recuento de transacciones de 0. La instrucción ROLLBACK TRANSACTION restablece el recuento de transacciones en 0, incluso si la instrucción se ha emitido desde una transacción anidada. COMMIT TRANSACTION puede reducir el recuento de transacciones a 0. Por tanto, aconsejamos que no se emitan instrucciones COMMIT TRANSACTION desde desencadenadores LOGON.  
  
 Piense lo siguiente cuando esté utilizando una instrucción ROLLBACK TRANSACTION dentro de los desencadenadores logon:  
  
-   Se revierten todas las modificaciones de datos realizadas antes de emitir la instrucción ROLLBACK TRANSACTION. Estas modificaciones incluyen las realizadas por el desencadenador actual y las realizadas por desencadenadores anteriores ejecutados en el mismo evento. No se ejecutan los desencadenadores restantes para el evento específico.  
  
-   El desencadenador actual continúa ejecutando cualquier instrucción restante que aparezca después de la instrucción ROLLBACK. Si alguna de estas instrucciones modifica datos, no se revierten las modificaciones.  
  
 Una sesión de usuario no está establecida si se produce cualquiera de las siguientes condiciones durante la ejecución de un desencadenador en un evento LOGON:  
  
-   La transacción implícita original se revierte o produce un error.  
  
-   Un error con una gravedad mayor que 20 se genera dentro del cuerpo del desencadenador.  
  
## <a name="disabling-a-logon-trigger"></a>Deshabilitar un desencadenador logon  
 Un desencadenador logon puede impedir la conexión al [!INCLUDE[ssDE](../../../includes/ssde-md.md)] de todos los usuarios, incluidos los miembros del rol fijo de servidor `sysadmin`. Cuando el desencadenador logon impide que se realicen las conexiones, los miembros del rol fijo de servidor `sysadmin` pueden conectarse mediante la conexión de administrador dedicada o iniciando el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] en modo de configuración mínima (-f). Para más información, consulte [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Tema|  
|----------|-----------|  
|Describe cómo crear los desencadenadores logon. Los desencadenadores logon se pueden crear desde cualquier base de datos, pero se registran en el nivel de servidor y residen en la base de datos **maestra** .|[CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)|  
|Describe cómo modificar los desencadenadores logon.|[ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)|  
|Describe cómo eliminar los desencadenadores logon.|[DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)|  
|Describe cómo devolver información acerca de los desencadenadores logon.|[sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)<br /><br /> [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)|  
|Describe cómo capturar los datos de evento de desencadenador logon.||  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores DDL](../triggers/ddl-triggers.md)  
  
  
