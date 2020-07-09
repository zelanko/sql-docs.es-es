---
title: Objetos de mensajería de Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9df112777d7005479e515082859375d95d62839c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726479"
---
# <a name="database-mail-messaging-objects"></a>Objetos de mensajería de Correo electrónico de base de datos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La base de datos **msdb** es la base de datos host del Correo electrónico de base de datos. Esta base de datos contiene los procedimientos almacenados y objetos de mensajería del Correo electrónico de base de datos. Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] incluye el Asistente para configuración del Correo electrónico de base de datos, que permite habilitar el correo electrónico de base de datos, crear y administrar perfiles y cuentas, y configurar las opciones del Correo electrónico de base de datos.  
  
##  <a name="objects-in-msdb-database"></a><a name="ComponentsAndConcepts"></a> Objetos de la base de datos **msdb**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] debe estar habilitado en la base de datos **msdb** . No obstante, el Correo electrónico de base de datos no usa la configuración de red de [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Por ello, los usuarios no tienen que crear un extremo de [!INCLUDE[ssSB](../../includes/sssb-md.md)] para usar el Correo electrónico de base de datos. El proceso externo de Correo electrónico de base de datos usa una conexión [!INCLUDE[vstecado](../../includes/vstecado-md.md)] estándar para comunicarse con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El Correo electrónico de base de datos expone los siguientes objetos en la base de datos **msdb** si el Correo electrónico de base de datos está habilitado.  
  
 Estos objetos son la interfaz del Correo electrónico de base de datos en la base de datos host de correo. Hay instalados otros objetos para implementar las funciones proporcionadas por los objetos enumerados anteriormente. Sin embargo, dichos objetos están reservados para uso interno.  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|[sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)|**Vista**|Enumera todos los mensajes enviados al Correo electrónico de base de datos.|  
|[sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)|**Vista**|Enumera los mensajes acerca del comportamiento del [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md).|  
|[sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)|**Vista**|Información acerca de los mensajes que el Correo electrónico de base de datos no ha podido enviar.|  
|[sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)|**Vista**|Información acerca de los datos adjuntos a mensajes del Correo electrónico de base de datos.|  
|[sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)|**Vista**|Información acerca de los mensajes que se han enviado mediante el Correo electrónico de base de datos.|  
|[sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)|**Vista**|Información acerca de los mensajes que el Correo electrónico de base de datos está intentando enviar.|  
|[sp_send_dbmail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)|**Procedimiento almacenado**|Envía mensajes de correo electrónico utilizando el Correo electrónico de base de datos.|  
|[sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|**Procedimiento almacenado**|Elimina mensajes del registro del Correo electrónico de base de datos.|  
|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)|**Procedimiento almacenado**|Elimina elementos de correo de la cola del Correo electrónico de base de datos.|  
|[sysmail_help_status_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql.md)|**Procedimiento almacenado**|Indica si se ha iniciado el Correo electrónico de base de datos.|  
|[sysmail_start_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)|**Procedimiento almacenado**|Inicia los objetos de Service Broker que utiliza el programa externo. Estos objetos se inician de forma predeterminada.|  
|[sysmail_stop_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)|**Procedimiento almacenado**|Detiene los objetos de Service Broker que usa el programa externo.|  
  
  
## <a name="see-also"></a>Consulte también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
