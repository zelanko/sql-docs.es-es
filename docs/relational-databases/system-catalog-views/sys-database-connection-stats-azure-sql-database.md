---
title: Sys.database_connection_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/25/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 801074dd7e82f5e1564564125486e0845e2303fb
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589489"
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contiene las estadísticas de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] base de datos **conectividad** eventos, que proporcionan una visión general de aciertos de conexión de base de datos y errores. Para obtener más información acerca de los eventos de conectividad, consulte tipos de eventos en [sys.event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
|Estadística|Tipo|Descripción|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|Nombre de la base de datos.|  
|**start_time**|**datetime2**|Fecha y hora UTC del inicio del intervalo de agregación. La hora es siempre un múltiplo de 5 minutos. Por ejemplo:<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|Fecha y hora UTC del final del intervalo de agregación. **End_time** es siempre exactamente 5 minutos posterior a la correspondiente **start_time** en la misma fila.|  
|**success_count**|**int**|Número de conexiones correctas.|  
|**total_failure_count**|**int**|Número total de conexiones con error. Esta es la suma de **connection_failure_count**, **terminated_connection_count**, y **throttled_connection_count**y no incluye los eventos de interbloqueo.|  
|**connection_failure_count**|**int**|Número total de errores de inicio de sesión.|  
|**terminated_connection_count**|**int**|**_Solo es aplicable para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11._**<br /><br /> Número de conexiones terminadas.|  
|**throttled_connection_count**|**int**|**_Solo es aplicable para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] v11._**<br /><br /> Número máximo de conexiones aceleradas.|  
  
## <a name="remarks"></a>Comentarios  
  
### <a name="event-aggregation"></a>Agregación de eventos  
 La información de eventos de esta vista se recopila y se agrega a intervalos de 5 minutos. Las columnas de recuento representan el número de veces que se produjo un evento de conectividad determinado para una base de datos específica en un intervalo de tiempo dado.  
  
 Por ejemplo, si un usuario no se puede conectar con la base de datos Database1 siete veces entre las 11:00 y las 11:05 del 2/5/2012 (UTC), esta información está disponible en una única fila en esta vista:  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>Start_time y end_time de intervalo  
 Un evento se incluye en un intervalo de agregación cuando se produce el evento *en* o _después_**start_time** y _antes_  **end_time** para ese intervalo. Por ejemplo, un evento que ocurra exactamente el `2012-10-30 19:25:00.0000000` solo se incluiría en el segundo intervalo que se muestra a continuación:  
  
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
  
-   Esta vista no incluye todos los [!INCLUDE[ssSDS](../../includes/sssds-md.md)] errores que pueden producirse, solo los especificados en los tipos de eventos en la base de datos [sys.event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md).  
  
-   Si se produce un fallo en el equipo del centro de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], es posible que se pierda una pequeña cantidad de datos del servidor lógico de la tabla de eventos.  
  
-   Si se ha bloqueado una dirección IP a través de DoSGuard, los eventos de intento de conexión de esa dirección IP no pueden recopilarse y no aparecerán en esta vista.  
  
## <a name="permissions"></a>Permisos  
 Los usuarios con permiso para tener acceso a la **maestro** base de datos tiene acceso de solo lectura a esta vista.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra una consulta de **sys.database_connection_stats** para devolver un resumen de las conexiones de base de datos que se produjeron entre el mediodía del 25/9/2011 y el mediodía del 28/9/2011 (UTC). De forma predeterminada, los resultados de la consulta se ordenan por **start_time** (orden ascendente).  
  
```  
SELECT *  
FROM sys.database_connection_stats   
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de Microsoft Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
