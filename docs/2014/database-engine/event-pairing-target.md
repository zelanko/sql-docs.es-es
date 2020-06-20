---
title: Destino de emparejamiento de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a1a6beb1c6996e6e12f16c4555fd9dfcab97617d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933050"
---
# <a name="event-pairing-target"></a>Destino de emparejamiento de eventos
  El destino de emparejamiento de eventos asocia dos eventos usando una o varias columnas de datos presentes en cada evento. Muchos eventos vienen en parejas, como por ejemplo, bloqueo y desbloqueo. Una vez emparejada un flujo de eventos, se descartan ambos eventos. El descarte de los conjuntos asociados permite una detección fácil de adquisiciones de bloqueos que no se han liberado.  
  
 Al emplear los filtros de nivel de eventos, el destino de emparejamientos puede usarse para capturar solo eventos que no coincidan con los criterios predefinidos.  
  
 Al usar el destino de emparejamiento de eventos, se podrán elegir los dos eventos que se van a asociar, junto con una secuencia de columnas en la que realizar la asociación. Todas las columnas de este flujo deben ser del mismo tipo.  
  
 La siguiente tabla describe las opciones disponibles para configurar el emparejamiento de eventos.  
  
|Opción|Valores permitidos|Descripción|  
|------------|--------------------|-----------------|  
|begin_event|Un nombre de evento presente en la sesión actual.|El nombre de evento que especifica el evento de inicio en una secuencia emparejada.|  
|end_event|Un nombre de evento presente en la sesión actual.|El nombre de evento que especifica el evento final en una secuencia emparejada.|  
|begin_matching_columns|Una lista ordenada y delimitada por comas de nombres de columna.|Las columnas en las que realizar la asociación.|  
|end_matching_columns|Una lista ordenada y delimitada por comas de nombres de columna.|Las columnas en las que realizar la asociación.|  
|begin_matching_actions|Una lista de acciones ordenada y delimitada por comas.|Las acciones en las que se debe realizar la asociación.|  
|end_matching_actions|Una lista de acciones ordenada y delimitada por comas.|Las acciones en las que se debe realizar la asociación.|  
|respond_to_memory_pressure|Uno de los siguientes valores:<br /><br /> 0 = No responder.<br /><br /> 1 = Dejar de agregar nuevos elementos huérfanos a la lista en caso de que exista presión de memoria.|La respuesta del destino a los eventos de memoria. Si se estable en 1 y la memoria del servidor es insuficiente, se quitará la información no emparejada.|  
|max_orphans||Especifica el número total de eventos no emparejados que se recopilarán en el destino. Una vez alcanzado el límite, los eventos no emparejados se quitan con un orden FIFO (primero en entrar, primero en salir). Valor predeterminado = 10,000.|  
  
 Todos los datos asociados a un evento se capturan y almacenan para futuros emparejamientos. Además, se recopilan los datos agregados por las acciones. Los datos de eventos recopilados se almacenan en la memoria y, por lo tanto, tienen un límite finito. Este límite depende de la actividad y capacidad del sistema. En lugar de tomar la cantidad de memoria máxima que se va a utilizar como un parámetro, la memoria utilizada dependerá de los recursos disponibles del sistema. Cuando no hay recursos, se quitarán los eventos no emparejados que se han conservado. Si un evento no se ha emparejado y se quita, el evento asociado aparecerá como un evento no emparejado.  
  
 El destino de emparejamiento serializa los eventos no emparejados a un formato XML. Este formato no sigue ningún esquema. El formato solo contiene dos tipos de elementos. El **\<unpaired>** elemento es la raíz, seguido de uno. **\<event>** elemento para cada evento no emparejado que se está realizando actualmente. El **\<event>** elemento contiene un atributo que contiene el nombre del evento no emparejado.  
  
## <a name="adding-the-target-to-a-session"></a>Agregar el destino a una sesión  
 Para agregar el destino de búsqueda del par a una sesión de eventos extendidos, debe incluir la siguiente instrucción al crear o modificar una sesión de eventos:  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 Para ello se usaría una instrucción SET, para definir los eventos del principio y el fin, y qué acciones o columnas hacer coincidir. En el ejemplo siguiente se muestra la sintaxis de ejemplo de la coincidencia de pares de los eventos sqlserver.lock_acquired y sqlserver.lock_released.  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 Para obtener más información, vea [Determinar las consultas que mantienen bloqueos](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md).  
  
## <a name="reviewing-the-target-output"></a>Revisar la salida del destino  
 Para revisar la salida del destino de coincidencia del par, puede usar la siguiente consulta, reemplazando *session_name* por el nombre de la sesión de eventos.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 En el siguiente ejemplo se muestra el formato de salida del destino de emparejamiento.  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server destinos de eventos extendidos](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [Sys. dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREAR sesión de eventos &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
