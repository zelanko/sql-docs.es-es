---
title: Database Mirroring State Change (clase de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- database mirroring [SQL Server], event notifications
- Database Mirroring State Change event class
ms.assetid: f936a99e-2a81-4768-8177-5c969bbe2e04
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e635ff34d280affd22d5f0d7854b3c8d7f1a717d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257347"
---
# <a name="database-mirroring-state-change-event-class"></a>Database Mirroring State Change, clase de eventos
  La clase de eventos **Database Mirroring State Change** indica cuándo cambia el estado de una base de datos reflejada. Incluya esta clase de eventos en los seguimientos que supervisan las condiciones de bases de datos reflejadas.  
  
 Cuando la clase de eventos **Database Mirroring State Change** se incluye en un seguimiento, la sobrecarga relativa es baja. La sobrecarga puede ser mayor si el estado de las bases de datos reflejadas aumenta.  
  
## <a name="data-database-mirroring-state-change-event-class-data-columns"></a>Columnas de datos de la clase de eventos Database Mirroring State Change  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**DatabaseName**|**nvarchar**|Nombre de la base de datos reflejada.|35|Sí|  
|**EventClass**|**int**|Tipo de evento = 167.|27|no|  
|**EventSequence**|**int**|Secuencia de la clase de eventos en el lote.|51|no|  
|**IntegerData**|**int**|Id. del estado previo.|25|Sí|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|**LoginSid**|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede encontrar esta información en la vista de catálogo **sys.server_principals** . Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**IdSolicitud**|**int**|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|no|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|**SPID**|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**State**|**int**|Id. de los nuevos estados de creación de reflejos:<br /><br /> 0 = Notificación de NULL<br /><br /> 1 = Entidad de seguridad sincronizada con testigo<br /><br /> 2 = Entidad de seguridad sincronizada sin testigo<br /><br /> 3 = Reflejo sincronizado con testigo<br /><br /> 4 = Reflejo sincronizado sin testigo<br /><br /> 5 = Conexión con entidad de seguridad perdida<br /><br /> 6 = Conexión con reflejo perdida<br /><br /> 7 = Conmutación por error manual<br /><br /> 8 = Conmutación automática por error<br /><br /> 9 = Creación de reflejos suspendida<br /><br /> 10 = Sin quórum<br /><br /> 11 = Sincronizando el reflejo<br /><br /> 12 = ·Entidad de seguridad en ejecución expuesta|30|Sí|  
|**TextData**|**ntext**|Descripción del cambio de estado.|1|Sí|  
|**TransactionID**|**bigint**|Id. de la transacción asignado por el sistema.|4|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
