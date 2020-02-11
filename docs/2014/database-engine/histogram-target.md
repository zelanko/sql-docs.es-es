---
title: Destino de histograma | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a584311061a24d674eed114f37d9cbbbda43909
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064699"
---
# <a name="histogram-target"></a>Destino del histograma
  El destino del histograma agrupa las generaciones de un tipo de evento concreto en datos del evento. El recuento de las agrupaciones de eventos se realiza tomando como base una acción o columna de evento especificada. Puede utilizar el destino del histograma para solucionar problemas de rendimiento. Mediante la identificación de los eventos que se producen con más frecuencia, puede buscar "zonas activas" que indiquen la causa posible de un problema de rendimiento.  
  
 En la tabla siguiente se describen las opciones que se pueden utilizar para configurar el destino del histograma.  
  
|Opción|Valores permitidos|Descripción|  
|------------|--------------------|-----------------|  
|slots|Un valor entero. Este valor es opcional.|Un valor especificado por el usuario que indica el número máximo de agrupaciones que se van a conservar. Cuando se alcanza este valor, se omiten los nuevos eventos que no pertenecen a los grupos existentes.<br /><br /> Tenga en cuenta que, para mejorar el rendimiento, el número de zona se redondea a la siguiente potencia de 2.|  
|filtering_event_name|Cualquier evento presente en la sesión de eventos extendidos. Este valor es opcional.|Un valor especificado por el usuario que se utiliza para identificar una clase de eventos. Solamente se crean depósitos de las instancias del evento especificado. Todos los demás eventos se omiten.<br /><br /> Si especifica este valor, debe usar el formato: *package_name*.*event_name*, por ejemplo `'sqlserver.checkpoint_end'`. Puede identificar el nombre del paquete utilizando la consulta siguiente:<br /><br /> Seleccione p.name, se event_name<br />DESDE sys. dm_xe_session_events se<br />JOIN sys. dm_xe_packages p<br />EN se_event_package_guid = p. GUID<br />ORDER BY p.name, se event_name<br /><br /> <br /><br /> Si no especifica el valor filtering_event_name, source_type se debe establecer en 1 (valor predeterminado).|  
|source_type|El tipo de objeto en el que se basa el depósito. Este valor es opcional y si no se especifica, tiene un valor predeterminado de 1.|Puede tener uno de los siguientes valores:<br /><br /> 0 para un evento<br /><br /> 1 para una acción|  
|source|Columna de evento o nombre de acción.|Columna de evento o nombre de acción que se usan como origen de datos.<br /><br /> Al especificar una columna de evento para el origen, debe especificar una columna del evento que se utiliza para el valor filtering_event_name. Puede identificar las columnas posibles utilizando la siguiente consulta:<br /><br /> Seleccione nombre en sys. dm_xe_object_columns<br />WHERE object_name = '\<eventName> '<br />Y column_type! = ' readonly '<br /><br /> Al especificar una columna de evento para el origen, no tiene que incluir el nombre del paquete en el valor de origen.<br /><br /> Al especificar un nombre de acción para el origen, debe utilizar una de las acciones que se configuran para la recopilación en la sesión de eventos para la que se utiliza este destino. Para buscar posibles valores para el nombre de acción, puede consultar la columna de action_name de la vista sys.dm_xe_sesssion_event_actions.<br /><br /> Si usa un nombre de acción como origen de datos, debe especificar el valor de origen mediante el formato: *package_name*.*action_name*.|  
  
 En el ejemplo siguiente se muestra a un alto nivel cómo el destino del histograma recopila datos. En este ejemplo, desea utilizar el destino del histograma para realizar un recuento del número de esperas de cada tipo de espera que se han producido. Para ello, debe especificar las opciones siguientes al definir el destino del histograma:  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0 (dado que wait_type es una columna de evento)  
  
 En el escenario del ejemplo, se registran los datos siguientes para el origen wait_type.  
  
|Nombre de evento de filtrado|Valor de columna de origen|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|red|  
|wait_info|red|  
|wait_info|sleep|  
  
 Los valores de tipo de espera se clasificarían en tres ranuras, con los valores y recuentos de ranura siguientes:  
  
|Value|Recuento de ranura|  
|-----------|----------------|  
|file_io|2|  
|red|2|  
|sleep|1|  
  
 El destino del histograma solo conserva los datos del evento correspondientes al origen especificado. En algunos casos, es posible que los datos del evento sean demasiado grandes para conservarlos al completo, en cuyo caso se truncan los datos. Cuando se truncan los datos de eventos, el número de bytes se graba y se muestra como una salida XML.  
  
## <a name="adding-the-target-to-a-session"></a>Agregar el destino a una sesión  
 Para agregar el destino del histograma a una sesión de Extended Events, se debe incluir cualquiera de las instrucciones siguientes al crear o modificar una sesión de eventos, dependiendo del tipo de destino deseado:  
  
```  
ADD TARGET package0.histogram  
```  
  
 Puede utilizar la instrucción SET para establecer las diversas opciones. En el ejemplo siguiente se muestra la adición del destino de histograma, donde se recopilan los datos del evento sqlserver.checkpoint_end.  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 Para obtener más información, vea [Buscar los objetos que han obtenido más bloqueos](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)y [Supervisar la actividad del sistema mediante eventos extendidos](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  
  
## <a name="reviewing-the-target-output"></a>Revisar la salida del destino  
 El destino del histograma serializa los datos a un procedimiento o programa que realiza la llamada en formato XML. La salida de destino no sigue ningún esquema.  
  
 Para revisar la salida del destino de histograma, puede usar la siguiente consulta, reemplazando *session_name* por el nombre de la sesión de eventos.  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 En el ejemplo siguiente se muestra el formato de salida del destino del histograma.  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Destinos de SQL Server Extended Events](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
