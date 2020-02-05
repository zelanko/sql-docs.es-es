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
ms.openlocfilehash: 4a701a56ba5a71037317f6c404fa394a466febba
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "73729885"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Muestra el espacio de almacenamiento utilizado en la caché de un conjunto de resultados para una base de datos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] de Azure.
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Observaciones

El comando `DBCC SHOWRESULTCACHESPACEUSED` no toma ningún parámetro y devuelve el espacio usado por la base de datos donde se ejecuta.

## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Columna|Tipo de datos|Descripción|  
|------------|---------------|-----------------|  
|reserved_space|bigint|Espacio total usado para la base de datos, en KB. Este número cambiará a medida que el conjunto de resultados almacenado en caché aumente.|  
|data_space|bigint|Espacio usado para los datos, en KB.|  
|index_space|bigint|Espacio usado para los índices, en KB.|  
|unused_space|bigint|Espacio que forma parte del espacio reservado y que no se usa, en KB.|  


## <a name="see-also"></a>Consulte también

[Ajuste del rendimiento con la copia en caché del conjunto de resultados](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)