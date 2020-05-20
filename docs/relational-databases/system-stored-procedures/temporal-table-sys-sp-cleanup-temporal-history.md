---
title: Sys. sp_cleanup_temporal_history | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 668948af95fd33c57414b50aa888e185b3e4d089
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807397"
---
# <a name="syssp_cleanup_temporal_history-transact-sql"></a>Sys. sp_cleanup_temporal_history (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

Quita todas las filas de la tabla de historial temporal que coinciden con el período de HISTORY_RETENTION configurado dentro de una única transacción.

## <a name="syntax"></a>Sintaxis

```
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```

## <a name="arguments"></a>Argumentos

*\@table_name*

Nombre de la tabla temporal para la que se invoca la limpieza de retención.

*schema_name*

Nombre del esquema al que pertenece la tabla temporal actual.

*row_count_var* [salida]

Parámetro de salida que devuelve el número de filas eliminadas. Si la tabla de historial tiene un índice de almacén de columnas agrupado, este parámetro devolverá siempre 0.

## <a name="remarks"></a>Observaciones

Este procedimiento almacenado solo se puede usar con tablas temporales que tengan especificado un período de retención finito.
Utilice este procedimiento almacenado solo si necesita limpiar inmediatamente todas las filas antiguas de la tabla de historial. Debe saber que puede tener un impacto significativo en el registro de la base de datos y en el subsistema de e/s, ya que elimina todas las filas válidas dentro de la misma transacción.

Siempre se recomienda confiar en una tarea en segundo plano interna para la limpieza que quita las filas antiguas con el mínimo impacto en las cargas de trabajo y la base de datos normales en general.

## <a name="permissions"></a>Permisos

Requiere permisos de db_owner.

## <a name="example"></a>Ejemplo

```sql
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="next-steps"></a>Pasos siguientes

[Directiva de retención de tablas temporales](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
