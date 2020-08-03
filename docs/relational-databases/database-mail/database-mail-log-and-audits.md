---
title: Registro y auditorías del Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 4354def42884887539693073bf3108d7227170de
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363575"
---
# <a name="database-mail-log-and-audits"></a>Registro y auditorías del Correo electrónico de base de datos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La funcionalidad de registro del Correo electrónico de base de datos está diseñado para proporcionar una manera de aislar y de corregir problemas. El Correo electrónico de base de datos almacena información de registro en la base de datos **msdb** . La información acerca del contenido del correo electrónico de base de datos, el estado de los mensajes, y cualquier mensaje recibido, como errores, está registrada por el Correo electrónico de base de datos y se puede usar para solucionar problemas y auditar ordenación.  
  
## <a name="database-mail-logs"></a>Registros de Correo electrónico de base de datos  
 Tablas en la información de registro de la base de datos **msdb** de [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md). [Vistas del Correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) expone las tablas para solucionar problemas. Aparecen errores en la vista [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) si Service Broker no puede activar el programa externo, si el programa externo encuentra errores de red o si el servidor SMTP (protocolo simple de transferencia de correo) rechaza un mensaje de correo electrónico. Si el programa externo no puede conectarse a las tablas **msdb** , el programa registra los errores en el registro de eventos de aplicación Windows.  
  
 Las tablas internas de la base de datos **msdb** contienen los mensajes de correo electrónico y los datos adjuntos enviados desde el Correo electrónico de base de datos, junto con el estado actual de cada mensaje. El Correo electrónico de base de datos actualiza estas tablas a medida que se procesa cada mensaje.  
  
## <a name="database-mail-auditing-tasks"></a>Tareas de auditoría de Correo electrónico de base de datos  
  
|Revisar y administrar los registros de Correo electrónico de base de datos|Vínculo al tema|  
|-|-|  
|Comprobar el estado de entrega de un mensaje individual|[Comprobar el estado de los mensajes de correo electrónico enviados con Correo electrónico de base de datos](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|Limpiar los mensajes, los datos adjuntos, y las entradas de registro del Correo electrónico de base de datos|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|Almacenar los mensajes de correo electrónico y los registros de la base de datos|[Crear un trabajo del Agente SQL Server para archivar mensajes y registros de eventos del Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
