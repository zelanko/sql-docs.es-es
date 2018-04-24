---
title: Sys.sp_cleanup_temporal_history | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: 4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f86d01146c3861f599e85e7bb7c61f716a3bf4b8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>Sys.sp_cleanup_temporal_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

Quita todas las filas de tabla de historial temporal que coinciden con el período de HISTORY_RETENTION configurado en una única transacción.
  
## <a name="syntax"></a>Sintaxis  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>Argumentos  

*@table_name*

El nombre de la tabla temporal para la retención se invoca el Liberador de espacio.

*schema_name*

El nombre del esquema que la tabla temporal actual pertenece a

*row_count_var* [salida]

El parámetro de salida que devuelve el número de filas eliminadas. Si la tabla de historial agrupado índice de almacén de columnas, se devolverá este parámetro siempre es 0.
  
## <a name="remarks"></a>Comentarios
Este procedimiento almacenado puede utilizarse solo con las tablas temporales que ha especificado el período de retención finito.
Utilice este procedimiento almacenado solo si necesita limpiar inmediatamente todas las filas de datos antiguas de la tabla de historial. Debe saber que puede tener un impacto significativo en el registro de base de datos y el subsistema de E/S como eliminan todas las filas aptas dentro de la misma transacción. 

Se recomienda siempre se basan en una tarea de segundo plano interno para la limpieza que quita antiguos filas con un impacto mínimo en las cargas de trabajo normales y la base de datos en general.

## <a name="permissions"></a>Permissions  
 Se requieren permisos db_owner.  

## <a name="example"></a>Ejemplo

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>Vea también

[Directiva de retención de las tablas temporales](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
