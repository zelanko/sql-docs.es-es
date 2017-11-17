---
title: DBCC SQLPERF (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f854ce5ff1261829df621931d3a736426f32c8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Proporciona estadísticas de uso del espacio del registro de transacciones para todas las bases de datos. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también se puede utilizar para restablecer las estadísticas de esperas y bloqueos temporales.
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([vista previa en algunas regiones](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     |  
          [ "sys.dm_os_latch_stats" , CLEAR ]  
     |  
     [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
LOGSPACE  
Devuelve el tamaño actual del registro de transacciones y el porcentaje de espacio del registro utilizado para cada base de datos. Puede utilizar esta información para supervisar la cantidad de espacio utilizada en un registro de transacciones.  
  
**"** **sys.dm_os_latch_stats",** claro  
Restablece las estadísticas de bloqueos temporales. Para obtener más información, consulte [sys.dm_os_latch_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). Esta opción no está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
**"sys.dm_os_wait_stats"** claro  
Restablece las estadísticas de esperas. Para obtener más información, vea [sys.dm_os_wait_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). Esta opción no está disponible en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
WITH NO_INFOMSGS  
Suprime todos los mensajes informativos con niveles de gravedad entre 0 y 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 En la tabla siguiente se describen las columnas del conjunto de resultados.  
  
|Nombre de columna|Definición|  
|---|---|
|**Nombre de la base de datos**|Nombre de la base de datos para la que se presentan las estadísticas del registro.|  
|**Tamaño del registro (MB)**|Tamaño actual asignado al registro. Este valor siempre es menor que la cantidad asignada originalmente como espacio del registro, ya que [!INCLUDE[ssDE](../../includes/ssde-md.md)] reserva una pequeña cantidad de espacio en disco para información interna de encabezados.|  
|**Espacio del registro usada (%)**|Porcentaje del archivo de registro actualmente en uso para almacenar información de registro de transacciones.|  
|**Estado**|Estado del archivo de registro. Siempre es 0.|  
  
## <a name="remarks"></a>Comentarios  
Las entradas del registro de transacciones que realizó cada transacción en una base de datos. Para obtener más información consulte [el registro de transacciones &#40; SQL Server &#41; ](../../relational-databases/logs/the-transaction-log-sql-server.md).
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar DBCC SQLPERF (LOGSPACE) requiere el permiso VIEW SERVER STATE en el servidor. Para restablecer las estadísticas de esperas y bloqueos temporales, se requiere el permiso ALTER SERVER STATE en el servidor.
  
En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el permiso VIEW DATABASE STATE en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador. No se admiten el reinicio de las estadísticas de espera y bloqueos temporales.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. Mostrar información del espacio de registro para todas las bases de datos  
En este ejemplo se presenta la información de `LOGSPACE` de todas las bases de datos contenidas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
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
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
  
  


