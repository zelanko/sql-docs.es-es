---
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ab4ca9241452450b248e709d0cd04c5c6d02c969
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452838"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Controla el comportamiento de almacenamiento en caché para la sesión de cliente actual del conjunto de resultados.  

Se aplica a Azure SQL Data Warehouse (versión preliminar)
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Notas  

Ejecute este comando cuando esté conectado a la base de datos de usuario para donde quiere configurar el valor de result_set_caching.

**ON**   
Habilita el almacenamiento en caché del conjunto de resultados para la sesión de cliente actual.  El almacenamiento en caché del conjunto de resultados no se puede activar en una sesión si está desactivado en el nivel de base de datos.

**OFF**   
Deshabilita el almacenamiento en caché del conjunto de resultados para la sesión de cliente actual.

## <a name="examples"></a>Ejemplos

Consulte la columna result_cache_hit en [ sys.dm_pdw_exec_requests ](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql) con el valor request_id de una consulta para ver si esta consulta se ejecutó con un acierto o un error en la caché de resultados.

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>Permisos

Debe pertenecer al rol público.

## <a name="see-also"></a>Vea también
[Ajuste del rendimiento con almacenamiento en caché de los resultados](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)</br>
[DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)