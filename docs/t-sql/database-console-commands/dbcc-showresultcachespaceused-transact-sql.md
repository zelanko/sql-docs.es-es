---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ffd0ad4ddcdae91071811e57cdb8c5f6aaaea656
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476304"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Muestra el espacio de almacenamiento utilizado en la caché de un conjunto de resultados para una base de datos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] de Azure.
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Notas

El comando `DBCC SHOWRESULTCACHESPACEUSED` no toma ningún parámetro y devuelve el espacio usado por la base de datos donde se ejecuta.

El tamaño máximo de la caché del conjunto de resultados es 1 TB por base de datos.  Azure SQL Data Warehouse extrae automáticamente las entradas de la caché del conjunto de resultados:

- cada 48 horas si el conjunto de resultados no se ha usado.
- cuando la caché del conjunto de resultados se acerca al tamaño máximo.

Los usuarios pueden vaciar manualmente la caché del conjunto de resultados de una base de datos desactivando dicha caché o con el comando `DBCC DROPRESULTSETCACHE`.   El hecho de poner en pausa una base de datos no vaciará la caché del conjunto de resultados.  

## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|columna|Tipo de datos|Descripción|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Espacio total usado para la base de datos, en KB. Este número cambiará a medida que el conjunto de resultados almacenado en caché aumente.|  
|data_space|BIGINT|Espacio usado para los datos, en KB.|  
|index_space|BIGINT|Espacio usado para los índices, en KB.|  
|unused_space|BIGINT|Espacio que forma parte del espacio reservado y que no se usa, en KB.|  


## <a name="see-also"></a>Vea también

[Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)