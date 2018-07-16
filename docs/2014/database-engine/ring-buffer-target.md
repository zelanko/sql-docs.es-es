---
title: Destino de búfer de anillo | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events], ring buffer target
- ring buffer target [SQL Server extended events]
ms.assetid: 54494e11-b56b-43b7-aa5e-c8724e56b251
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b60f4e3c5ca8d207d3eac23047c8cdefc99d9f66
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273081"
---
# <a name="ring-buffer-target"></a>Destino de búfer de anillo
  El destino de búfer de anillo guarda datos de eventos en la memoria durante un corto espacio de tiempo. Este destino puede administrar los eventos de uno de los dos modos siguientes.  
  
-   El primer modo es un orden FIFO (First In, First Out; primero en entrar, primero en salir) estricto, en el que el evento más antiguo se descarta cuando se usa toda la memoria asignada al destino. En este modo (valor predeterminado), la opción occurrence_number se establece en 0.  
  
-   El segundo modo es un orden FIFO por evento, en el que se conserva un número determinado de eventos de cada tipo. En este modo, los eventos más antiguos de cada tipo se descartan cuando se usa toda la memoria asignada al destino. Puede configurar la opción occurrence_number para especificar el número de eventos de cada tipo que se desea conservar.  
  
 En la tabla siguiente se describen las opciones disponibles para configurar el destino de búfer de anillo.  
  
|Opción|Valores permitidos|Descripción|  
|------------|--------------------|-----------------|  
|max_memory|Cualquier entero de 32 bits. Este valor es opcional.|La cantidad de memoria máxima en kilobytes (kB) que se va a usar. Los eventos existentes se quitan en función del límite que se alcance primero: max_event_limit o max_memory.|  
|max_event_limit|Cualquier entero de 32 bits. Este valor es opcional.|El número máximo de eventos que se mantiene en el búfer en anillo. Los eventos existentes se quitan en función del límite que se alcance primero: max_event_limit o max_memory. Valor predeterminado = 1000.|  
|occurrence_number|Los valores pueden ser los siguientes:<br /><br /> 0 (valor predeterminado) = El evento más antiguo se descarta cuando se usa toda la memoria asignada al destino.<br /><br /> Un número entero de 32 bits = El número de eventos de cada tipo que se conserva antes de descartarse siguiendo un orden FIFO por evento.<br /><br /> <br /><br /> Este valor es opcional.|Modo FIFO que se va a usar y, si se establece en un valor mayor que 0, el número preferido de eventos de cada tipo que se desea conservar en el búfer.|
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="adding-the-target-to-a-session"></a>Agregar el destino a una sesión  
 Para agregar el destino del búfer de anillo a una sesión de eventos extendidos, debe incluir la siguiente instrucción al crear o modificar una sesión de eventos:  
  
```sql
ADD TARGET package0.ring_buffer  
```  
  
## <a name="reviewing-the-target-output"></a>Revisar la salida del destino  
 Para revisar la salida del destino de búfer de anillo, puede usar la siguiente consulta, reemplazando *session_name* por el nombre de la sesión de eventos.  
  
```sql
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 En el siguiente ejemplo se muestra el formato de salida del destino de búfer de anillo.  
  
```  
<RingBufferTarget eventsPerSec="" processingTime="" totalEventsProcessed="" eventCount="" droppedCount="" memoryUsed="">  
 <event name="" package="" id="" version="" timestamp="">  
    <data name="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </data>  
    <action name="" package="">  
      <type name="" package="" />  
      <value></value>  
      <text></text>  
    </action>  
  </event>  
</RingBufferTarget>  
```


## <a name="see-also"></a>Vea también

- [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md)
- [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql?view=sql-server-2016)
- [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql?view=sql-server-2016)
- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](https://docs.microsoft.com/sql/t-sql/statements/alter-event-session-transact-sql?view=sql-server-2016)

