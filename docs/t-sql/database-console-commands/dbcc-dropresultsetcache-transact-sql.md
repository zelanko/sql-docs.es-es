---
description: DBCC DROPRESULTSETCACHE  (Transact-SQL)
title: DBCC DROPRESULTSETCACHE (Transact-SQL)
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
ms.openlocfilehash: 11f62d090768920114e617e06901dad0c65003e6
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670622"
---
# <a name="dbcc-dropresultsetcache--transact-sql"></a>DBCC DROPRESULTSETCACHE  (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Quita todas las entradas de la caché del conjunto de resultados de una base de datos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] de Azure.
  
![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
DBCC DROPRESULTSETCACHE
[;]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="permissions"></a>Permisos

Requiere pertenencia al rol fijo de servidor DB_OWNER.

## <a name="remarks"></a>Observaciones

- Este comando vacía la caché del conjunto de resultados para todas las consultas.  

- Al desactivar la característica de caché del conjunto de resultados para una base de datos, también se eliminan todos los resultados almacenados en caché.  

- Al pausar una base de datos habilitada con almacenamiento en caché del conjunto de resultados, no se eliminarán los resultados almacenados en caché.  

## <a name="see-also"></a>Consulte también

- [Ajuste del rendimiento con la copia en caché del conjunto de resultados](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
- [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
- [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
- [SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
- [DBCC SHOWRESULTCACHESPACEUSED &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)
