---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 8cb409823bad1370c38b6dc99f04c7e49d58796a
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982405"
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Proporciona estadísticas de uso del espacio del registro de transacciones para todas las bases de datos. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también se puede usar para restablecer las estadísticas de esperas y bloqueos temporales.
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([versión preliminar en algunas regiones](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
LOGSPACE  
Devuelve el tamaño actual del registro de transacciones y el porcentaje de espacio del registro utilizado para cada base de datos. Esta información se puede usar para supervisar la cantidad de espacio que se usa en un registro de transacciones.

> [!IMPORTANT]
> Para obtener más información sobre la información de uso de espacio del registro de transacciones a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], vea la sección [Comentarios](#Remarks) de este tema.
  
**"sys.dm_os_latch_stats"** , CLEAR  
Restablece las estadísticas de bloqueos temporales. Para obtener más información, vea [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Esta opción no está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**"sys.dm_os_wait_stats"** , CLEAR  
Restablece las estadísticas de esperas. Para obtener más información, vea [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Esta opción no está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
WITH NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 En la tabla siguiente se describen las columnas del conjunto de resultados.  
  
|Nombre de columna|Definición|  
|---|---|
|**Database Name**|Nombre de la base de datos para la que se presentan las estadísticas del registro.|  
|**Tamaño del registro (MB)**|Tamaño actual asignado al registro. Este valor siempre es menor que la cantidad asignada originalmente como espacio del registro, ya que [!INCLUDE[ssDE](../../includes/ssde-md.md)] reserva una pequeña cantidad de espacio en disco para información interna de encabezados.|  
|**Espacio de registro utilizado (%)**|Porcentaje del archivo de registro que se usa actualmente para almacenar la información del registro de transacciones.|  
|**Estado**|Estado del archivo de registro. Siempre es 0.|  
  
## <a name="Remarks"></a> Comentarios  
A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], use la DMV [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) en lugar de `DBCC SQLPERF(LOGSPACE)` para devolver información de uso de espacio del registro de transacciones por cada base de datos.    
 
Las entradas del registro de transacciones que realizó cada transacción en una base de datos. Para obtener más información, vea [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) y [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).
  
## <a name="permissions"></a>Permisos  
Para ejecutar consultas `DBCC SQLPERF(LOGSPACE)`, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se necesita el permiso `VIEW SERVER STATE` en el servidor. Para restablecer las estadísticas de esperas y bloqueos temporales, se requiere el permiso `ALTER SERVER STATE` en el servidor.
  
En los niveles Premium y críticos para la empresa de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] se necesita el permiso `VIEW DATABASE STATE` en la base de datos. En los niveles estándar, básico y de uso general de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se requiere la cuenta de administrador de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. No se admiten el reinicio de las estadísticas de espera y bloqueos temporales.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Mostrar información del espacio de registro para todas las bases de datos  
En este ejemplo se presenta la información de `LOGSPACE` de todas las bases de datos contenidas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. Restablecer las estadísticas de esperas  
En el ejemplo siguiente se restablecen las estadísticas de esperas para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

