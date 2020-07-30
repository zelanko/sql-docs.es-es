---
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
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
ms.openlocfilehash: c975242a65da5ef29374267262deb6d8bf370f25
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2020
ms.locfileid: "87397024"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT SET CACHING (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Controla el comportamiento de almacenamiento en caché para la sesión de cliente actual del conjunto de resultados.  

Se aplica a Azure SQL Data Warehouse  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis

```syntaxsql
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Observaciones  

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

## <a name="see-also"></a>Consulte también

- [Ajuste del rendimiento con la copia en caché del conjunto de resultados](/azure/sql-data-warehouse/performance-tuning-result-set-caching)
- [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)
- [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)
- [DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)
- [DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)
