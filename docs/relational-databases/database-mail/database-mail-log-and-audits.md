---
title: "Registro y auditor&#237;as del Correo electr&#243;nico de base de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "auditoría [SQL Server]"
  - "Correo electrónico de base de datos [SQL Server], auditar"
  - "registros [Correo electrónico de base de datos]"
  - "auditorías [SQL Server], Correo electrónico de base de datos"
  - "Correo electrónico de base de datos [SQL Server], registrar"
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
caps.latest.revision: 30
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 30
---
# Registro y auditor&#237;as del Correo electr&#243;nico de base de datos
  La funcionalidad de registro del Correo electrónico de base de datos está diseñado para proporcionar una manera de aislar y de corregir problemas. El Correo electrónico de base de datos almacena información de registro en la base de datos **msdb** . La información acerca del contenido del correo electrónico de base de datos, el estado de los mensajes, y cualquier mensaje recibido, como errores, está registrada por el Correo electrónico de base de datos y se puede usar para solucionar problemas y auditar ordenación.  
  
## Registros de Correo electrónico de base de datos  
 Tablas en la información de registro de la base de datos **msdb** de [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md). [Vistas del Correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) expone las tablas para solucionar problemas. Aparecen errores en la vista [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) si Service Broker no puede activar el programa externo, si el programa externo encuentra errores de red o si el servidor SMTP (protocolo simple de transferencia de correo) rechaza un mensaje de correo electrónico. Si el programa externo no puede conectarse a las tablas **msdb** , el programa registra los errores en el registro de eventos de aplicación Windows.  
  
 Las tablas internas de la base de datos **msdb** contienen los mensajes de correo electrónico y los datos adjuntos enviados desde el Correo electrónico de base de datos, junto con el estado actual de cada mensaje. El Correo electrónico de base de datos actualiza estas tablas a medida que se procesa cada mensaje.  
  
## Tareas de auditoría de Correo electrónico de base de datos  
  
|||  
|-|-|  
|**Revisar y administrar los registros de Correo electrónico de base de datos**|**Vínculo al tema**|  
|Comprobar el estado de entrega de un mensaje individual|[Comprobar el estado de los mensajes de correo electrónico enviados con Correo electrónico de base de datos](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|Limpiar los mensajes, los datos adjuntos, y las entradas de registro del Correo electrónico de base de datos|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|Almacenar los mensajes de correo electrónico y los registros de la base de datos|[Crear un trabajo del Agente SQL Server para archivar mensajes y registros de eventos del Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## Vea también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  