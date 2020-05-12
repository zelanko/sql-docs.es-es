---
title: '@@CPU_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs:
- TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a3ecaf4a142cdb2c722340b546b84873bd5a962d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823969"
---
# <a name="x40x40cpu_busy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Esta función devuelve el tiempo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha pasado en funcionamiento activo desde su último inicio. `@@CPU_BUSY` devuelve un resultado medido en incrementos de tiempo de CPU, o "tics". Este valor es acumulativo para todas las CPU, de modo que puede superar el tiempo transcurrido real. Para convertir a microsegundos, multiplique por [@@TIMETICKS](./timeticks-transact-sql.md).
  
> [!NOTE]  
>  Si el tiempo devuelto en @@CPU_BUSY o @@IO_BUSY supera 49 días (aproximadamente) de tiempo de CPU acumulado, puede recibir una advertencia de desbordamiento aritmético. En este caso, el valor de las variables `@@CPU_BUSY`, `@@IO_BUSY` y `@@IDLE` no es exacto.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>Tipos de valores devueltos
**integer**
  
## <a name="remarks"></a>Observaciones  
Ejecute [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sp_monitor[ para ver un informe que contenga varias estadísticas de ](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md), incluida la actividad de CPU.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se devuelve la actividad de CPU de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta la fecha y hora actuales. El ejemplo convierte uno de los valores al tipo de datos `float`. Esto evita problemas de desbordamiento aritmético cuando se calcula un valor en microsegundos.
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS float) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>Consulte también
[sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[Funciones estadísticas del sistema &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  
