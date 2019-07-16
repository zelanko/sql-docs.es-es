---
title: Sys.sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 111986a771b9cfb156c0d37688565b39401411f8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037229"
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>sys.sp_cleanup_temporal_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

Quita todas las filas de tabla temporal de historial que coincide con el período HISTORY_RETENTION configurado en una única transacción.
  
## <a name="syntax"></a>Sintaxis  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>Argumentos  

*@table_name*

El nombre de la tabla temporal para la retención de qué se invoca la limpieza.

*schema_name*

El nombre del esquema al que pertenece la tabla temporal actual

*row_count_var* [OUTPUT]

El parámetro de salida que devuelve el número de filas eliminadas. Si la tabla de historial agrupado de almacén de columnas, se devolverá este parámetro siempre es 0.
  
## <a name="remarks"></a>Comentarios
Este procedimiento almacenado puede utilizarse solo con tablas temporales que ha especificado el período de retención finito.
Utilice este procedimiento almacenado solo si tiene que limpiar inmediatamente todas las filas antiguas de la tabla de historial. Debe saber que puede tener un impacto significativo en el registro de base de datos y el subsistema de E/S como lo elimina todas las filas válidas en la misma transacción. 

Siempre se recomienda depender de una tarea interna en segundo plano de limpieza que quita antiguos filas con un impacto mínimo en las cargas de trabajo normales y la base de datos en general.

## <a name="permissions"></a>Permisos  
 Se requieren permisos db_owner.  

## <a name="example"></a>Ejemplo

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>Vea también

[Directiva de retención de las tablas temporales](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
