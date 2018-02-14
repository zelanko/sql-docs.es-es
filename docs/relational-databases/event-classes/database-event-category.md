---
title: "Base de datos (categoría de eventos) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11b3298807357b454de671482a72c5aecb3cabaf
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="database-event-category"></a>Base de datos (categoría de eventos)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
La categoría de evento **Base de datos** contiene clases de eventos para supervisar [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Data File Auto Grow (clase de eventos)](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)|Indica que el archivo de datos creció automáticamente. Este evento no se desencadena si se aumentó explícitamente el archivo de datos mediante ALTER DATABASE.|  
|[Data File Auto Shrink (clase de eventos)](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)|Indica que se ha reducido el archivo de datos.|  
|[Database Mirroring: Connection (clase de eventos)](../../relational-databases/event-classes/database-mirroring-connection-event-class.md)|Evento generado para informar del estado de una conexión de transporte para la creación de reflejo de la base de datos.|  
|[Database Mirroring State Change (clase de eventos)](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)|Indica cuando cambia el estado de una base de datos reflejada.|  
|[Clase de eventos Database Suspect Data Page](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)|Indica cuando una página se agrega a la tabla **suspect_pages** en la base de datos **msdb** .|  
|[Log File Auto Grow (clase de eventos)](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)|Indica que el archivo de registro creció automáticamente. Este evento no se desencadena si el archivo de registro se aumentó explícitamente mediante ALTER DATABASE.|  
|[Log File Auto Shrink (clase de eventos)](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|Indica que el archivo de registro creció automáticamente. Este evento no se desencadena si el archivo de registro se reduce explícitamente mediante la instrucción ALTER DATABASE.|  
  
## <a name="see-also"></a>Ver también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
