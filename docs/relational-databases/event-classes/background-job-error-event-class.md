---
title: Clase de eventos Background Job Error | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Background Job Error event class
ms.assetid: 9e6d2a0e-919d-4fe2-a306-b20b8d41c197
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1733eb2b4c47cd1297b9839ce9714b3340ba943b
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34329846"
---
# <a name="background-job-error-event-class"></a>Background Job Error [clase de eventos]
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La clase de eventos **Background Job Error** se produce cuando un trabajo en segundo plano finaliza de forma anómala. Esta condición podría requerir la atención de un administrador del sistema.  
  
## <a name="background-job-error-event-class-data-columns"></a>Columnas de datos de la clase de eventos Background Job Error  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|Id. de la base de datos especificada por el trabajo. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**DatabaseName**|**nvarchar**|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|**Error**|**int**|Número de error del último intento (solo**EventSubClass** 1).|31|Sí|  
|**EventClass**|**int**|Tipo de evento = 193.|27|no|  
|**EventSequence**|**int**|Secuencia de un evento determinado dentro de la solicitud.|51|no|  
|**EventSubClass**|**int**|Tipo de la subclase de eventos.<br /><br /> 1 = Abandono del trabajo en segundo plano después de un error.<br /><br /> 2 = Trabajo en segundo plano quitado; la cola está llena.<br /><br /> 3 = El trabajo en segundo plano devolvió un error.|21|Sí|  
|**IndexID**|**int**|Id. del índice del objeto afectado por el evento. Para determinar el Id. de índice de un objeto, utilice la columna **indid** de la tabla del sistema **sysindexes** .|24|Sí|  
|**IntegerData**|**int**|Número de intentos del trabajo (solo**EventSubClass** 1).|25|Sí|  
|**IntegerData2**|**int**|Número de secuencia de trabajo.|55|Sí|  
|**ObjectID**|**int**|Identificador del objeto asignado por el sistema.|22|Sí|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|64|Sí|  
|**Severity**|**int**|Nivel de gravedad del error del último intento (solo**EventSubClass** 1).|20|Sí|  
|**StartTime**|**datetime**|Hora en que se creó el trabajo.|14|Sí|  
|**State**|**int**|Estado del error del último intento (solo**EventSubClass** 1).|30|Sí|  
|**TextData**|**ntext**|Descripción del valor de subclase de evento.|1|Sí|  
|**Tipo**|**int**|Tipo de trabajo.|57|Sí|  
  
## <a name="see-also"></a>Ver también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Auto Stats (clase de eventos)](../../relational-databases/event-classes/auto-stats-event-class.md)  
  
  
