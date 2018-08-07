---
title: CURRENT_TIMESTAMP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMESTAMP
- CURRENT_TIMESTAMP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- niladic functions
- current date and time [SQL Server]
- time [SQL Server], current
- date and time [SQL Server], CURRENT_TIMESTAMP
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- CURRENT_TIMESTAMP function [SQL Server]
- time [SQL Server], system
ms.assetid: c724d9cc-7b1f-4c71-bdf5-08bc52b33afc
caps.latest.revision: 48
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: eb2c972b34e5699177f3aab38e72603da0d2b3e3
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451929"
---
# <a name="currenttimestamp-transact-sql"></a>CURRENT_TIMESTAMP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve la marca de tiempo del sistema de base de datos actual como un valor **datetime** sin el desplazamiento de zona horaria de la base de datos. `CURRENT_TIMESTAMP` deriva este valor del sistema operativo del equipo en el que se ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
> [!NOTE]  
>  `SYSDATETIME` y `SYSUTCDATE` tienen más precisión, de acuerdo con la medición de la precisión de las fracciones de segundo, que `GETDATE` y `GETUTCDATE`. La función `SYSDATETIMEOFFSET` incluye el ajuste de zona horaria del sistema. Puede asignar `SYSDATETIME`, `SYSUTCDATE` y `SYSDATETIMEOFFSET` a una variable de cualquiera de los tipos de fecha y hora.  
  
Esta función es el equivalente de ANSI SQL a [GETDATE](../../t-sql/functions/getdate-transact-sql.md).
  
Vea [Tipos de datos y funciones de fecha y hora](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para ver información de todos los tipos y funciones de datos de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CURRENT_TIMESTAMP  
```  
  
## <a name="arguments"></a>Argumentos  
Esta función no toma ningún argumento.
  
## <a name="return-type"></a>Tipo devuelto  
**datetime**
  
## <a name="remarks"></a>Notas  
Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden hacer referencia a `CURRENT_TIMESTAMP` desde cualquier parte desde donde puedan hacer referencia a una expresión **datetime**.
  
`CURRENT_TIMESTAMP` es una función no determinista. Las vistas y las expresiones que hacen referencia a esta columna no se pueden indizar.
  
## <a name="examples"></a>Ejemplos  
Estos ejemplos usan las seis funciones de sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que devuelven los valores de fecha y hora actuales para devolver la fecha, la hora o ambas. Los ejemplos devuelven los valores en series, por lo que sus fracciones de segundo podrían diferir. Tenga en cuenta que los valores reales devueltos reflejarán la fecha y hora real de la ejecución.
  
### <a name="a-get-the-current-system-date-and-time"></a>A. Obtener la fecha y hora actuales del sistema  
  
```sql
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
/* Returned:  
SYSDATETIME()      2007-04-30 13:10:02.0474381  
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00  
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381  
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047  
GETDATE()          2007-04-30 13:10:02.047  
GETUTCDATE()       2007-04-30 20:10:02.047  
*/
```  
  
### <a name="b-get-the-current-system-date"></a>B. Obtener la fecha actual del sistema  
  
```sql
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
/* Returned   
SYSDATETIME()      2007-05-03  
SYSDATETIMEOFFSET()2007-05-03  
SYSUTCDATETIME()   2007-05-04  
CURRENT_TIMESTAMP  2007-05-03  
GETDATE()          2007-05-03  
GETUTCDATE()       2007-05-04  
*/  
```  
  
### <a name="c-get-the-current-system-time"></a>C. Obtener la hora actual del sistema  
  
```sql
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
/* Returned  
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT CURRENT_TIMESTAMP;  
```  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

