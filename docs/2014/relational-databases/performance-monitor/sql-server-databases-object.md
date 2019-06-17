---
title: Databases (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4c0c7a5626f3eb48509d7a4cfbf239f7cb931da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250647"
---
# <a name="sql-server-databases-object"></a>Databases (objeto de SQL Server)
  El objeto **SQLServer:Databases** de SQL Server proporciona contadores para supervisar las operaciones de copia masiva, el rendimiento de las copias de seguridad y restauración, y las actividades del registro de transacciones. La supervisión de las transacciones y del registro de transacciones determina el volumen de actividad de los usuarios en la base de datos y el espacio libre que queda en el registro de transacciones. El volumen de actividad de los usuarios puede determinar el rendimiento de la base de datos y puede afectar al tamaño del registro, los bloqueos y la replicación. La supervisión de la actividad de registro de bajo nivel para medir la actividad de los usuarios y el uso de los recursos puede ayudar a identificar cuellos de botella en el rendimiento.  
  
 Se pueden supervisar simultáneamente varias instancias del objeto **Databases** que representen una única base de datos cada una.  
  
 En la siguiente tabla se describen los contadores de **Databases** de SQL Server.  
  
|Contadores de Databases de SQL Server|Descripción|  
|-----------------------------------|-----------------|  
|**Transacciones activas**|Número de transacciones activas de la base de datos|  
|**Rendimiento de copia de seguridad y restauración/seg.**|Rendimiento de lectura/escritura por segundo en copias de seguridad y restauración de bases de datos. Por ejemplo, puede medir la variación en el rendimiento de la operación de copia de seguridad de una base de datos cuando se utilizan en paralelo más dispositivos de copia de seguridad o cuando se utilizan dispositivos más rápidos. El rendimiento de la operación de copia de seguridad o restauración de una base de datos permite determinar el progreso y el rendimiento de estas operaciones.|  
|**Copia masiva de filas/seg.**|Número de filas copiadas de forma masiva por segundo.|  
|**Rendimiento de la copia masiva/seg.**|Cantidad de datos copiados de forma masiva (en kilobytes) por segundo.|  
|**Entradas de la tabla de confirmación**|Tamaño de la parte de memoria de la tabla de confirmación para la base de datos. Para obtener más información, vea [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table).|  
|**Tamaño de los archivos de datos (KB)**|Tamaño acumulado (en kilobytes) de todos los archivos de datos de la base de datos, incluido el crecimiento automático. La supervisión de este contador resulta útil, por ejemplo, para determinar el tamaño correcto de **tempdb**.|  
|**Bytes de recorrido lógico DBCC/seg.**|Número de bytes del examen de lectura lógica por segundo para los comandos de la consola de base de datos (DBCC).|  
|**Frecuencia de aciertos de caché del registro**|Porcentaje de lecturas de la caché del registro atendidas desde la caché del registro.|  
|**Lecturas de caché del registro/seg.**|Lecturas realizadas por segundo a través de la caché del administrador de registros.|  
|**Tamaño de los archivos de registro (KB)**|Tamaño acumulado (en kilobytes) de todos los archivos de registro de transacciones de la base de datos.|  
|**Tamaño (KB) utilizado en los archivos de registro**|Tamaño acumulado de todos los archivos de registro de la base de datos.|  
|**Tiempo de espera de vaciado de registro**|Tiempo de espera total (en milisegundos) para vaciar el registro. En una base de datos secundaria de AlwaysOn, este valor indica el tiempo de espera para que las entradas de registro se protejan en el disco.|  
|**Esperas al vaciar el registro/seg.**|Número de confirmaciones por segundo que esperan el vaciado del registro.|  
|**Tiempo de escritura de vaciados de registro (ms)**|Tiempo, en milisegundos, para realizar operaciones de escritura de vaciados de registro que se completaron en el último segundo.|  
|**Vaciados del registro/seg.**|Número de vaciados del registro por segundo.|  
|**Ampliaciones del registro**|Número total de ampliaciones del registro de transacciones de la base de datos.|  
|**Reducciones del registro**|Número total de reducciones del registro de transacciones de la base de datos.|  
|**Errores de caché de grupo de registros/s**|Número de solicitudes para las que no estuvo disponibles el bloque de registro en el grupo de registros. El *grupo de registro* es una memoria caché en memoria del registro de transacciones. Esta memoria caché se utiliza para optimizar la lectura en el registro para la recuperación, la replicación de transacciones, la recuperación y [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**Lecturas de disco de grupo de registros/s**|Número de lecturas de disco que el grupo de registros emitió para capturar bloques de registro.|  
|**Solicitudes de grupo de registros/s**|Número de solicitudes de bloque de registro procesadas por el grupo de registros.|  
|**Truncamientos de registro**|El número de veces que se ha reducido el registro de transacciones.|  
|**Porcentaje utilizado del registro**|Porcentaje de espacio del registro que está en uso.|  
|**Transacciones pendientes de réplica**|Número de transacciones del registro de transacciones de la base de datos de publicación que están marcadas para replicación, pero que no se han entregado todavía a la base de datos de distribución.|  
|**Transacciones de transacciones de replicación**|Número de transacciones leídas por segundo del registro de transacciones de la base de datos de publicación y entregadas a la base de datos de distribución.|  
|**Bytes de movimiento de datos de reducción/seg.**|Cantidad de datos que se mueven por segundo en operaciones de reducción automática, o instrucciones DBCC SHRINKDATABASE o DBCC SHRINKFILE.|  
|**Transacciones con seguimiento/s**|Número de transacciones confirmadas que se registraron en la tabla de confirmación para la base de datos.|  
|**Transacciones/seg.**|Número de transacciones iniciadas para la base de datos por segundo.<br /><br /> **Transacciones/s** no cuenta las transacciones solo de XTP (las transacciones iniciadas por un procedimiento almacenado compilado de forma nativa).|  
|**Transacciones de escritura/s**|Número de transacciones que se escribieron en la base de datos y se confirmaron, en el último segundo.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, réplica de base de datos](sql-server-database-replica.md)  
  
  
