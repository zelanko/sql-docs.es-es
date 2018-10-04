---
title: Clase de eventos Database Suspect Data Page | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 50ee8a83c87ec6f2b14ac07caa77774b7a7c2d15
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137912"
---
# <a name="database-suspect-data-page-event-class"></a>clase de eventos Database Suspect Data Page
  La clase de eventos **Database Suspect Data Page** indica cuándo se agrega una página a la tabla [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) en [msdb](../databases/msdb-database.md). Incluya esta clase de eventos en los seguimientos que supervisan la aparición de páginas sospechosas.  
  
> [!NOTE]  
>  Este evento se emite de forma asincrónica desde la inserción de una fila correspondiente en la tabla **suspect_pages** . Por consiguiente, es posible que un trabajo que realice escuchas en este evento no encuentre inmediatamente la entrada **suspect_pages** correspondiente.  
  
 Cuando la clase de eventos **Database Mirroring State Change** se incluye en un seguimiento, la sobrecarga relativa es baja. La sobrecarga puede ser mayor si aumenta el número de páginas sospechosas, por ejemplo una unidad de disco tiene problemas.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Columnas de datos de la clase de eventos Database Suspect Data Page  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|Id. de la base de datos para la que se ha producido la alerta de evento de página sospechosa. Esto es lo mismo que la columna **database_id** de la tabla **suspect_pages** .|3|Sí|  
|**EventClass**|**int**|El tipo de evento es 213.|27|no|  
|**EventSequence**|**int**|Secuencia de la clase de eventos en el lote.|51|no|  
|**SPID**|**int**|Id. de la tarea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que encontró la página sospechosa.|12|Sí|  
|**StartTime**|**datetime**|Momento en el que se produjo el evento.|14|Sí|  
|**ObjectID**|**int**|Id. de la fila de la base de datos que contiene la página sospechosa. Esto es el mismo que la columna **file_id** de la tabla **suspect_pages** .|22|Sí|  
|**ObjectID2**|**int**|Id. de la página sospechosa del archivo. Esto es el mismo que la columna **page_id** de la tabla **suspect_pages** .|56|Sí|  
|**Error**|**int**|Tipo de error que se encontró. Este valor es el mismo que el valor **event_type** de la página en la tabla **suspect_pages** .|31|Sí|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
