---
title: Sys.database_connection_stats (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/25/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 0ab4255a4c13199a445335eef491ca0986ab3287
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contiene las estadísticas de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] base de datos **conectividad** eventos, que proporcionan una visión general de aciertos de la conexión de base de datos y con errores. Para obtener más información acerca de los eventos de conectividad, vea tipos de eventos en [sys.event_log &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
|Estadística|Tipo|Description|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|Nombre de la base de datos.|  
|**start_time**|**datetime2**|Fecha y hora UTC del inicio del intervalo de agregación. La hora es siempre un múltiplo de 5 minutos. Por ejemplo:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|Fecha y hora UTC del final del intervalo de agregación. **End_time** es siempre exactamente 5 minutos posterior a la correspondiente **start_time** en la misma fila.|  
|**success_count**|**int**|Número de conexiones correctas.|  
|**total_failure_count**|**int**|Número total de conexiones con error. Esta es la suma de **connection_failure_count**, **terminated_connection_count**, y **throttled_connection_count**y no incluye los eventos de interbloqueo.|  
|**connection_failure_count**|**int**|Número total de errores de inicio de sesión.|  
|**terminated_connection_count**|**int**|***Solo se aplica para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11.***<br /><br /> Número de conexiones terminadas.|  
|**throttled_connection_count**|**int**|***Solo se aplica para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11.***<br /><br /> Número máximo de conexiones aceleradas.|  
  
## <a name="remarks"></a>Comentarios  
  
### <a name="event-aggregation"></a>Agregación de eventos  
 La información de eventos de esta vista se recopila y se agrega a intervalos de 5 minutos. Las columnas de recuento representan el número de veces que se produjo un evento de conectividad determinado para una base de datos específica en un intervalo de tiempo dado.  
  
 Por ejemplo, si un usuario no se puede conectar con la base de datos Database1 siete veces entre las 11:00 y las 11:05 del 2/5/2012 (UTC), esta información está disponible en una única fila en esta vista:  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>Start_time y end_time de intervalo  
 Un evento se incluye en un intervalo de agregación cuando se produce el evento *en* o *después *** start_time** y *antes *** end_time** para ese intervalo. Por ejemplo, un evento que ocurra exactamente el `2012-10-30 19:25:00.0000000` solo se incluiría en el segundo intervalo que se muestra a continuación:  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>Actualizaciones de datos  
 Los datos de esta vista se acumulan a lo largo del tiempo. Normalmente, los datos se acumulan en la hora siguiente al inicio del intervalo de agregación, pero puede llevar hasta 24 horas que todos los datos aparezcan en la vista. Durante ese tiempo, la información de una sola fila puede actualizarse de forma periódica.  
  
### <a name="data-retention"></a>Retención de datos  
 Los datos de esta vista se conservan durante un período máximo de 30 días o posiblemente menos dependiendo del número de bases de datos de los servidores lógicos y del número de eventos únicos que cada base de datos genere. Para conservar esta información durante más tiempo, copie los datos en una base de datos independiente. Una vez realizada una copia inicial de la vista, las filas de esta pueden actualizarse a medida que se acumulan datos. Para mantener actualizada su copia de los datos, realice periódicamente una exploración de las filas de la tabla para ver si se ha producido un aumento del número de eventos de las filas existentes y para identificar nuevas filas (se pueden identificar filas únicas usando las horas de inicio y fin), después actualice su copia de los datos con esos cambios.  
  
### <a name="errors-not-included"></a>Errores no incluidos  
 Esta vista puede no incluir toda la información de conexión y de error:  
  
-   Esta vista no incluye todos los [!INCLUDE[ssSDS](../../includes/sssds-md.md)] errores que pueden producirse, solo los especificados en tipos de evento en la base de datos [sys.event_log &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
-   Si se produce un fallo en el equipo del centro de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], es posible que se pierda una pequeña cantidad de datos del servidor lógico de la tabla de eventos.  
  
-   Si se ha bloqueado una dirección IP a través de DoSGuard, los eventos de intento de conexión de esa dirección IP no pueden recopilarse y no aparecerán en esta vista.  
  
## <a name="permissions"></a>Permissions  
 Los usuarios con permiso para tener acceso a la **maestro** base de datos tienen acceso de sólo lectura a esta vista.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra una consulta de **sys.database_connection_stats** para devolver un resumen de las conexiones de base de datos que se produjeron entre el mediodía del 25/9/2011 y el mediodía del 28/9/2011 (UTC). De forma predeterminada, los resultados de la consulta se ordenan por **start_time** (en orden ascendente).  
  
```  
SELECT *  
FROM sys.database_connection_stats   
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de base de datos SQL Azure de Windows](http://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
