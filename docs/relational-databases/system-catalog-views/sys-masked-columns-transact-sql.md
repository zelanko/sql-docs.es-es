---
title: Sys. masked_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.masked_columns
- masked_columns_tsql
- sys.masked_columns_tsql
- masked_columns
helpviewer_keywords:
- sys.masked_columns catalog view
ms.assetid: 671577e4-d757-4b8d-9aa9-0fc8d51ea9ca
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d1872dfd9d7ffd90696743972d38d7ad4af1171c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85648752"
---
# <a name="sysmasked_columns-transact-sql"></a>Sys. masked_columns (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asdw.md)]

  Use la vista **Sys. masked_columns** para consultar las columnas de tabla que tienen aplicada una función de enmascaramiento dinámico de datos. Esta vista se hereda de la vista **sys.columns** . Devuelve todas las columnas de la vista **sys.columns** , junto con las columnas **is_masked** y **masking_function** . Además, indica si estas están enmascaradas y, en caso afirmativo, qué función de enmascaramiento se ha definido. Esta vista solo muestra las columnas en las que se ha aplicado la función de enmascaramiento.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Identificador del objeto al que pertenece esta columna.|  
|name|**sysname**|Nombre de la columna. Es único en el objeto.|  
|column_id|**int**|Identificador de la columna. Es único en el objeto.<br /><br /> Los Id. de columna no tienen que ser secuenciales.|  
|**Sys. masked_columns** devuelve muchas más columnas heredadas de **Sys. Columns**.|varias|Vea [Sys. columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) para obtener más definiciones de columna.|  
|is_masked|**bit**|Indica si la columna está enmascarada. 1 indica enmascarado.|  
|masking_function|**nvarchar(4000)**|Función de enmascaramiento para la columna.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="permissions"></a>Permisos  
 Esta vista devuelve información acerca de las tablas en las que el usuario tiene algún tipo de permiso en la tabla o si el usuario tiene el permiso VIEW ANY DEFINITION.  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta combina **Sys. masked_columns** con **Sys. Tables** para devolver información sobre todas las columnas enmascaradas.  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Enmascaramiento dinámico de datos](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
