---
title: Databases (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a8114722ac95c1404a45d8c85bf1736e541fa0ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093600"
---
# <a name="sql-server-databases-object"></a>Databases (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto **SQLServer:Databases** de SQL Server proporciona contadores para supervisar las operaciones de copia masiva, el rendimiento de las copias de seguridad y restauración, y las actividades del registro de transacciones. La supervisión de las transacciones y del registro de transacciones determina el volumen de actividad de los usuarios en la base de datos y el espacio libre que queda en el registro de transacciones. El volumen de actividad de los usuarios puede determinar el rendimiento de la base de datos y puede afectar al tamaño del registro, los bloqueos y la replicación. La supervisión de la actividad de registro de bajo nivel para medir la actividad de los usuarios y el uso de los recursos puede ayudar a identificar cuellos de botella en el rendimiento.  
  
 Se pueden supervisar simultáneamente varias instancias del objeto **Databases** que representen una única base de datos cada una.  
  
 En la siguiente tabla se describen los contadores de **Databases** de SQL Server.  
  
|Contadores de Databases de SQL Server|Descripción|  
|-----------------------------------|-----------------|  
|**Transacciones activas**|Número de transacciones activas de la base de datos|  
|**Dist promedio desde EOL/Solicitud de LP**|Distancia promedio en bytes desde el final del registro por solicitud de grupo de registros, para solicitudes en el último VLF.| 
|**Rendimiento de copia de seguridad y restauración/seg.**|Rendimiento de lectura/escritura por segundo en copias de seguridad y restauración de bases de datos. Por ejemplo, puede medir la variación en el rendimiento de la operación de copia de seguridad de una base de datos cuando se utilizan en paralelo más dispositivos de copia de seguridad o cuando se utilizan dispositivos más rápidos. El rendimiento de la operación de copia de seguridad o restauración de una base de datos permite determinar el progreso y el rendimiento de estas operaciones.|  
|**Copia masiva de filas/seg.**|Número de filas copiadas de forma masiva por segundo.|  
|**Rendimiento de la copia masiva/seg.**|Cantidad de datos copiados de forma masiva (en kilobytes) por segundo.|  
|**Entradas de la tabla de confirmación**|Tamaño (recuento de filas) de la parte de memoria de la tabla de confirmación para la base de datos. Para obtener más información, vea [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md).|  
|**Tamaño de los archivos de datos (KB)**|Tamaño acumulado (en kilobytes) de todos los archivos de datos de la base de datos, incluido el crecimiento automático. La supervisión de este contador resulta útil, por ejemplo, para determinar el tamaño correcto de **tempdb**.|  
|**Bytes de recorrido lógico DBCC/seg.**|Número de bytes del examen de lectura lógica por segundo para los comandos de la consola de base de datos (DBCC).|  
|**Tiempo de confirmación de grupo/seg.**|Tiempo de obstrucción de grupo (microsegundos) por segundo.|
|**Bytes de registro vaciados/s**|Número total de bytes de registro vaciados.|  
|**Frecuencia de aciertos de caché del registro**|Porcentaje de lecturas de la caché del registro atendidas desde la caché del registro.|  
|**Base de frecuencia de aciertos de caché de registro**|Exclusivamente para uso interno.| 
|**Lecturas de caché del registro/seg.**|Lecturas realizadas por segundo a través de la caché del administrador de registros.|  
|**Tamaño de los archivos de registro (KB)**|Tamaño acumulado (en kilobytes) de todos los archivos de registro de transacciones de la base de datos.|  
|**Tamaño (KB) utilizado en los archivos de registro**|Tamaño acumulado de todos los archivos de registro de la base de datos.|  
|**Tiempo de espera de vaciado de registro**|Tiempo de espera total (en milisegundos) para vaciar el registro. En una base de datos secundaria de AlwaysOn, este valor indica el tiempo de espera para que las entradas de registro se protejan en el disco.|  
|**Esperas al vaciar el registro/seg.**|Número de confirmaciones por segundo que esperan el vaciado del registro.|  
|**Tiempo de escritura de vaciados de registro (ms)**|Tiempo, en milisegundos, para realizar operaciones de escritura de vaciados de registro que se completaron en el último segundo.|  
|**Vaciados del registro/seg.**|Número de vaciados del registro por segundo.|  
|**Ampliaciones del registro**|Número total de ampliaciones del registro de transacciones de la base de datos.|  
|**Errores de caché de grupo de registros/s**|Número de solicitudes para las que no estuvo disponibles el bloque de registro en el grupo de registros. El *grupo de registro* es una memoria caché en memoria del registro de transacciones. Esta memoria caché se utiliza para optimizar la lectura en el registro para la recuperación, la replicación de transacciones, la recuperación y [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**Lecturas de disco de grupo de registros/s**|Número de lecturas de disco que el grupo de registros emitió para capturar bloques de registro.|  
|**Eliminaciones de hash de grupo de registros/seg**|Índice de eliminaciones de entradas de hash sin formato del grupo de registros.|
|**Inserciones hash de grupo de registros por segundo**|Frecuencia de inserción de entradas hash sin procesar en el grupo de registros.|
|**Entrada de hash no válida del grupo de registros/seg**|Error de búsquedas de hash con error por no ser válidas.|
|**Inserciones de examen de registro del grupo de registros/seg**|Índice de inserciones de bloque de registros por exámenes de registros, que pueden provenir del disco o la memoria.|
|**Inserciones del LogWriter del grupo de registros/seg**|Índice de inserciones del bloque de registros por subproceso del escritor de registros.|
|**Grupo libre vacío de inserción de grupo de registros/s**|Tasa de errores de inserción de bloques de registro debido a un grupo libre vacío.|
|**Baja memoria de inserción de grupo de registros/s**|Tasa de errores de inserción de bloques de registro debido a una memoria baja.|
|**Búfer no disponible de inserción de grupo de registros/s**|Tasa de errores de inserción de bloques de registro debido a un búfer no disponible.|
|**Requisitos de grupo de registro detrás de truncamiento por segundo**|Errores de caché de grupo de registros debidos a que el bloque solicitado se encuentra detrás del LSN de truncamiento.|
|**Base de solicitudes de grupo de registro**|Exclusivamente para uso interno.| 
|**VLF antiguo de solicitudes de grupo de registros/seg**|Solicitudes del grupo de registros que no estaban en el último VLF del registro.|  
|**Solicitudes de grupo de registros/s**|Número de solicitudes de bloque de registro procesadas por el grupo de registros.|  
|**Tamaño de registro activo total de grupo de registros**|Registro activo total actual almacenado en el administrador de búfer de caché compartido en bytes.|
|**Tamaño de grupo compartido total del grupo de registros**|Uso de memoria total actual del administrador de búfer de caché compartido en bytes.|
|**Reducciones del registro**|Número total de reducciones del registro para esta base de datos.|  
|**Truncamientos de registro**|Número de truncamientos del registro de transacciones (en el modelo de recuperación simple).|  
|**Porcentaje utilizado del registro**|Porcentaje de espacio del registro que está en uso.|  
|**Transacciones pendientes de réplica**|Número de transacciones del registro de transacciones de la base de datos de publicación que están marcadas para replicación, pero que no se han entregado todavía a la base de datos de distribución.|  
|**Transacciones de transacciones de replicación**|Número de transacciones leídas por segundo del registro de transacciones de la base de datos de publicación y entregadas a la base de datos de distribución.|  
|**Bytes de movimiento de datos de reducción/seg.**|Cantidad de datos que se mueven por segundo en operaciones de reducción automática, o instrucciones DBCC SHRINKDATABASE o DBCC SHRINKFILE.|  
|**Transacciones con seguimiento/s**|Número de transacciones confirmadas que se registraron en la tabla de confirmación para la base de datos.|  
|**Transacciones/seg.**|Número de transacciones iniciadas para la base de datos por segundo.<br /><br /> **Transacciones/s** no cuenta las transacciones solo de XTP (las transacciones iniciadas por un procedimiento almacenado compilado de forma nativa).|  
|**Transacciones de escritura/s**|Número de transacciones que se escribieron en la base de datos y se confirmaron, en el último segundo.|  
|**Base de latencia del DLC del controlador del XTP**|Exclusivamente para uso interno.| 
|**Latencia/recuperación del DLC del controlador del XTP**|Latencia promedio en microsegundos desde que los bloques del registro entran al consumidor directo del registro hasta que son tomados por el controlador del XTP, por segundo.|
|**Latencia máxima del DLC del controlador del XTP**|La mayor latencia registrada, en microsegundos, de una recuperación del consumidor directo del registro por el controlador del XTP.|
|**Procesados/seg por el registro del controlador de XTP**|La cantidad de bytes del registro procesada por el subproceso controlador del XTP, por segundo.|
|**Memoria XTP usada (KB)**|Cantidad de memoria usada por XTP en la base de datos.| 
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, réplica de base de datos](../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
  
