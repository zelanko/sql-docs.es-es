---
title: Sys.masked_columns (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e059265dc5f5e0d2e4bc4a3b1396d2401386d7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102372"
---
# <a name="sysmaskedcolumns-transact-sql"></a>Sys.masked_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use la **sys.masked_columns** vista para consultar columnas de tabla que tiene un aplicada la función de enmascaramiento dinámico de datos. Esta vista se hereda de la vista **sys.columns** . Devuelve todas las columnas de la vista **sys.columns** , junto con las columnas **is_masked** y **masking_function** . Además, indica si estas están enmascaradas y, en caso afirmativo, qué función de enmascaramiento se ha definido. Esta vista solo muestra las columnas en las que se ha aplicado la función de enmascaramiento.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Identificador del objeto al que pertenece esta columna.|  
|name|**sysname**|Nombre de la columna. Es único en el objeto.|  
|column_id|**int**|Identificador de la columna. Es único en el objeto.<br /><br /> Los Id. de columna no tienen que ser secuenciales.|  
|**Sys.masked_columns** devuelve muchas más columnas que se hereda de **sys.columns**.|varios|Consulte [sys.columns &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) para obtener más definiciones de columna.|  
|is_masked|**bit**|Indica si la columna se enmascara. 1 indica enmascarado.|  
|masking_function|**nvarchar(4000)**|La función de enmascaramiento para la columna.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="permissions"></a>Permisos  
 Esta vista devuelve información acerca de las tablas donde el usuario tiene algún tipo de permiso en la tabla o si el usuario tiene el permiso VIEW ANY DEFINITION.  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta combinaciones **sys.masked_columns** a **sys.tables** devolver información acerca de todos los enmascara las columnas.  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [Enmascaramiento dinámico de datos](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
