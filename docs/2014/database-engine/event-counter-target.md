---
title: Destino del contador de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- synchronous event counter target [SQL Server extended events]
- targets [SQL Server extended events], synchronous event counter target
ms.assetid: 342e08d1-dcca-4a71-ae64-cb61b55b85bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddf153da7af2906fe7167c8cb2b77d9100d1154f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064917"
---
# <a name="event-counter-target"></a>Destino del contador de eventos
  El destino del contador de eventos cuenta todos los eventos que se producen durante una sesión de Extended Events. Si utiliza el destino del contador de eventos, puede obtener información sobre las características de la carga de trabajo sin agregar la sobrecarga que supone una recopilación de eventos completa. Este destino no tiene parámetros personalizables.  
  
## <a name="adding-the-target-to-a-session"></a>Agregar el destino a una sesión  
 Para agregar el destino del contador de eventos a una sesión de Extended Events, debe incluir la siguiente instrucción al crear o modificar una sesión de eventos:  
  
```  
ADD TARGET package0.event_counter  
```  
  
## <a name="reviewing-the-target-output"></a>Revisar la salida del destino  
 Para revisar la salida del destino del contador de eventos, puede usar la siguiente consulta, reemplazando *nombre_de_sesión* por el nombre de la sesión de eventos:  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 En el ejemplo siguiente se muestra el formato de la salida del destino del contador de eventos.  
  
```  
<CounterTarget truncated = "0">  
  <Packages>  
    <Package name = "[package name]">  
      <Event name = "[event name]" count = "[number]" />  
    </Package>  
  </Packages>  
</CounterTarget>  
```  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server destinos de eventos extendidos](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [Sys. dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREAR sesión de eventos &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
