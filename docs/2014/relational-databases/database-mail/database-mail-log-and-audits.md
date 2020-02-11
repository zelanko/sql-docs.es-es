---
title: Registro y auditorías del Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- Database Mail [SQL Server], auditing
- logs [Database Mail]
- audits [SQL Server], Database Mail
- Database Mail [SQL Server], logging
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e500eb47af39502e1bcf59f60b3dd24fed0713fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62872132"
---
# <a name="database-mail-log-and-audits"></a>Registro y auditorías del Correo electrónico de base de datos
  La funcionalidad de registro del Correo electrónico de base de datos está diseñado para proporcionar una manera de aislar y de corregir problemas. El Correo electrónico de base de datos almacena información de registro en la base de datos **msdb** . La información acerca del contenido del correo electrónico de base de datos, el estado de los mensajes, y cualquier mensaje recibido, como errores, está registrada por el Correo electrónico de base de datos y se puede usar para solucionar problemas y auditar ordenación.  
  
## <a name="database-mail-logs"></a>Registros de Correo electrónico de base de datos  
 Tablas en la información de registro de la base de datos **msdb** de [Database Mail External Program](database-mail-external-program.md). [Vistas del Correo electrónico de base de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/database-mail-views-transact-sql) expone las tablas para solucionar problemas. Aparecen errores en la vista [sysmail_event_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-event-log-transact-sql) si Service Broker no puede activar el programa externo, si el programa externo encuentra errores de red o si el servidor SMTP (protocolo simple de transferencia de correo) rechaza un mensaje de correo electrónico. Si el programa externo no puede conectarse a las tablas **msdb** , el programa registra los errores en el registro de eventos de aplicación Windows.  
  
 Las tablas internas de la base de datos **msdb** contienen los mensajes de correo electrónico y los datos adjuntos enviados desde el Correo electrónico de base de datos, junto con el estado actual de cada mensaje. El Correo electrónico de base de datos actualiza estas tablas a medida que se procesa cada mensaje.  
  
## <a name="database-mail-auditing-tasks"></a>Tareas de auditoría de Correo electrónico de base de datos  
  
|||  
|-|-|  
|**Revisar y administrar los registros de Correo electrónico de base de datos**|**Vínculo al tema**|  
|Comprobar el estado de entrega de un mensaje individual|[Comprobar el estado de los mensajes de correo electrónico enviados con Correo electrónico de base de datos](check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|Limpiar los mensajes, los datos adjuntos, y las entradas de registro del Correo electrónico de base de datos|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql)|  
|Almacenar los mensajes de correo electrónico y los registros de la base de datos|[Crear un trabajo del Agente SQL Server para archivar mensajes y registros de eventos del Correo electrónico de base de datos](create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
