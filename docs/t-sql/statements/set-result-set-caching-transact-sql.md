---
title: SET RESULT SET CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: cd0141a6fbd21c11f7401fa2c45dae0cc75b983d
ms.sourcegitcommit: ccea98fa0768d01076cb6ffef0b4bdb221b2f9d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2019
ms.locfileid: "65561498"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Hace que Azure SQL Data Warehouse almacene en caché los conjuntos de resultados de las consultas.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Notas  
  
Este comando debe ejecutarse mientras se está conectado a la base de datos maestra.  Los cambios realizados a esta configuración de base de datos se aplicarán inmediatamente.  Los costos de almacenamiento se aplican mediante el almacenamiento en caché de conjuntos de resultados de consultas. Después de deshabilitar el almacenamiento en caché de resultados para una base de datos, la caché de resultados que persistía anteriormente se eliminará inmediatamente del almacenamiento de Azure SQL Data Warehouse. Se ha incorporado una nueva columna denominada is_result_set_caching_on en [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?view=azure-sqldw-latest
) para mostrar la configuración de almacenamiento en caché de resultados para una base de datos.  

**ON** especifica que los conjuntos de resultados de consultas devueltos de esta base de datos se almacenarán en caché en el almacenamiento de Azure SQL Data Warehouse.

**OFF** especifica que los conjuntos de resultados de consultas devueltos de esta base de datos no se almacenarán en caché en el almacenamiento de Azure SQL Data Warehouse.

Los usuarios pueden ver si una consulta se ejecutó con un acierto o un fallo de caché de resultados realizando una consulta a [sys.pdw_request_steps](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql?view=azure-sqldw-latest) con un valor de request_id específico. Si hay un acierto de caché, el resultado de la consulta tendrá un único paso con los siguientes detalles:

|**Nombre de columna**|**Operador**|**Value**|
|----|----|----|
|operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Control|
|comando|Like|%DWResultCacheDb%|
||||
  
## <a name="permissions"></a>Permisos

Se requieren estos permisos:

- Inicio de sesión principal en el nivel de servidor (creado por el proceso de aprovisionamiento) o
- Miembro del rol de base de datos dbmanager.

El propietario de la base de datos no puede modificarla a menos que sea miembro del rol dbmanager.
  
## <a name="examples"></a>Ejemplos

### <a name="enable-result-set-caching-for-a-database"></a>Habilitación del almacenamiento en caché de conjuntos de resultados para una base de datos

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>Deshabilitación del almacenamiento en caché de conjuntos de resultados para una base de datos

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>Comprobación de la configuración de almacenamiento en caché de conjuntos de resultados para una base de datos

```sql
SELECT name, is_result_set_caching  
FROM sys.databases
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>Comprobación del número de consultas con acierto de caché y fallo de caché de conjuntos de resultados

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses,
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) ,
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end)
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>Comprobación del acierto de caché y fallo de caché de conjunto de resultados para una consulta

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286'
      and operation_type = 'ReturnOperation'
      and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>Comprobación de todas las consultas con aciertos de caché de conjunto de resultados

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0
```

## <a name="see-also"></a>Consulte también

[Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)