---
title: Destino de archivo de evento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53cf3aa4b23484bb22f4237fbf61874990381067
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064861"
---
# <a name="event-file-target"></a>Event File Target
  El destino de archivo de eventos es un destino que escribe búferes completos en el disco.  
  
 En la tabla siguiente se describen las opciones disponibles para configurar el destino de archivo de eventos.  
  
|Opción|Valores permitidos|Descripción|  
|------------|--------------------|-----------------|  
|filename|Cualquier cadena de 260 caracteres, como máximo. Este valor es obligatorio.|La ubicación y el nombre del archivo.<br /><br /> Puede utilizar cualquier extensión de nombre de archivo.|  
|max_file_size|Cualquier entero de 64 bits. Este valor es opcional.|El tamaño máximo del archivo en megabytes (MB). Si no se especifica max_file_size, el archivo crecerá hasta que se llene el disco. El tamaño de archivo predeterminado es 1GB.<br /><br /> max_file_size debe ser mayor que el tamaño actual de los búferes de sesión. Si no lo es, el destino del archivo no podrá inicializarse y se notificará que max_file_size no es válido. Para ver el tamaño actual de los búferes, vea la columna buffer_size en la vista de administración dinámica [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) .<br /><br /> Si el tamaño de archivo predeterminado es menor que el tamaño de búfer de la sesión, se recomienda establecer max_file_size en el valor especificado en la columna max_memory de la vista de catálogo [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) .<br /><br /> Cuando max_file_size se establece en un tamaño mayor que el de los búferes de la sesión, se puede redondear hacia abajo al múltiplo más próximo del tamaño de búfer de la sesión. De esta forma puede crearse un archivo de destino que sea menor que el valor especificado para max_file_size. Por ejemplo, si el tamaño del búfer es de 100 MB y max_file_size está establecido en 150 MB, el tamaño de archivo resultante se redondea hacia abajo a 100 MB porque un segundo búfer no cabría en los 50 MB de espacio restantes.<br /><br /> Si el tamaño de archivo predeterminado es menor que el tamaño de búfer de la sesión, se recomienda establecer max_file_size en el valor de la columna max_memory de la vista de catálogo [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) .|  
|max_rollover_files|Cualquier entero de 32 bits. Este valor es opcional.|El número máximo de archivos que se desean conservar en el sistema de archivos. El valor predeterminado es 5.|  
|increment|Cualquier entero de 32 bits. Este valor es opcional.|El crecimiento incremental, en megabytes (MB), para el archivo. Si no se especifica, el valor predeterminado para el incremento es dos veces el tamaño del búfer de la sesión.|  
  
 La primera vez que se crea un destino de archivo de eventos, al nombre de archivo que especifique se le anexa _0\_ y un valor entero largo. El valor entero se calcula como el número de milisegundos entre el 1 de enero de 1601 y la fecha y hora se crea el archivo. Los archivos de sustitución incremental siguientes también utilizan este formato. Al examinar el valor del entero largo, puede determinar el archivo más actual. En el ejemplo siguiente se muestra cómo se denominan los archivos de sustitución incremental en un escenario en el que la opción de nombre de archivo se especifica como C:\OutputFiles\MyOutput.xel:  
  
-   primer archivo creado - C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   primer archivo de sustitución incremental - C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   segundo archivo de sustitución incremental - C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>Agregar el destino a una sesión  
 Para agregar el archivo de evento de destino a una sesión de Eventos extendidos, incluiría las siguientes instrucciones al crear o modificar una sesión de eventos, reemplazando *file_name* por el nombre de archivo y la ruta de acceso que quiera:  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>Revisar la salida del destino  
 Para revisar el resultado del destino del archivo, debe usar la función sys.fn_xe_file_target_read_file. Recomendamos convertir los datos en XML. Puede usar la siguiente sintaxis, reemplazando *file_name* por el nombre de archivo y la ruta de acceso que especificó cuando agregó el destino:  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>Vea también  
 [Destinos de SQL Server Extended Events](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
