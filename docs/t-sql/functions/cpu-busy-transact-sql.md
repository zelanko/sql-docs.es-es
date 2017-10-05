---
title: '@@CPU_BUSY (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: f01d73c9ec0a0aca7237603169f8a290af0ce225
ms.contentlocale: es-es
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40cpubusy-transact-sql"></a>& #x 40; & #x 40; Cpu_busy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Devuelve el tiempo durante el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha estado funcionando desde su último inicio. Resultado es en incrementos de tiempo de CPU o "tics" y es acumulativo para todas las CPU, por lo que puede superar el tiempo transcurrido real. Multiplique por@TIMETICKS para convertir a microsegundos.
  
> [!NOTE]  
>  Si devuelve la hora de@CPU_BUSY o @@IO_BUSY supera aproximadamente 49 días de tiempo de CPU acumulado, recibirá una advertencia de desbordamiento aritmético. En ese caso, el valor de @@CPU_BUSY, @@IO_BUSY y @@IDLE variables no son precisas.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto
**integer**
  
## <a name="remarks"></a>Comentarios  
Para mostrar un informe que contenga varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las estadísticas, incluyendo la actividad de la CPU, ejecutan [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se muestra la actividad de CPU de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta la fecha y hora actuales. Para evitar el desbordamiento aritmético al convertir el valor a microsegundos, en el ejemplo se convierte uno de los valores al tipo de datos `float`.
  
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
  
## <a name="see-also"></a>Vea también
[Sys.dm_os_sys_info &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[Funciones estadísticas del sistema &#40; Transact-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  

