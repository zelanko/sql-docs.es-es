---
title: Clase de eventos Database Suspect Data Page | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d062eace204c298285f39426f56a954a147e4783
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="database-suspect-data-page-event-class"></a>clase de eventos Database Suspect Data Page
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La clase de eventos **Database Suspect Data Page** indica cuándo se agrega una página a la tabla [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) en [msdb](../../relational-databases/databases/msdb-database.md). Incluya esta clase de eventos en los seguimientos que supervisan la aparición de páginas sospechosas.  
  
> [!NOTE]  
>  Este evento se emite de forma asincrónica desde la inserción de una fila correspondiente en la tabla **suspect_pages** . Por consiguiente, es posible que un trabajo que realice escuchas en este evento no encuentre inmediatamente la entrada **suspect_pages** correspondiente.  
  
 Cuando la clase de eventos **Database Mirroring State Change** se incluye en un seguimiento, la sobrecarga relativa es baja. La sobrecarga puede ser mayor si aumenta el número de páginas sospechosas, por ejemplo una unidad de disco tiene problemas.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Columnas de datos de la clase de eventos Database Suspect Data Page  
  
|Nombre de columna de datos|Tipo de datos|Description|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|Id. de la base de datos para la que se ha producido la alerta de evento de página sospechosa. Esto es lo mismo que la columna **database_id** de la tabla **suspect_pages** .|3|Sí|  
|**EventClass**|**int**|El tipo de evento es 213.|27|no|  
|**EventSequence**|**int**|Secuencia de la clase de eventos en el lote.|51|no|  
|**SPID**|**int**|Id. de la tarea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que encontró la página sospechosa.|12|Sí|  
|**StartTime**|**datetime**|Momento en el que se produjo el evento.|14|Sí|  
|**ObjectID**|**int**|Id. de la fila de la base de datos que contiene la página sospechosa. Esto es el mismo que la columna **file_id** de la tabla **suspect_pages** .|22|Sí|  
|**ObjectID2**|**int**|Id. de la página sospechosa del archivo. Esto es el mismo que la columna **page_id** de la tabla **suspect_pages** .|56|Sí|  
|**Error**|**int**|Tipo de error que se encontró. Este valor es el mismo que el valor **event_type** de la página en la tabla **suspect_pages** .|31|Sí|  
  
## <a name="see-also"></a>Ver también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
