---
title: Sys.index_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.index_columns
- sys.index_columns_TSQL
- index_columns
- index_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.index_columns catalog view
ms.assetid: 211471aa-558a-475c-9b94-5913c143ed12
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aee9551240096547e37d4157179f80ca7e936182
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysindexcolumns-transact-sql"></a>sys.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada columna que forma parte de un **sys.indexes** índice o tabla no ordenada (montón).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. del objeto en el que se define el índice.|  
|**index_id**|**int**|Id. del índice en el que se define la columna.|  
|**index_column_id**|**int**|Id. de la columna de índice. **index_column_id** es único solo dentro de **index_id**.|  
|**column_id**|**int**|Identificador de la columna en **object_id**.<br /><br /> 0 = Identificador de fila (RID) en un índice no clúster.<br /><br /> **column_id** es único solo dentro de **object_id**.|  
|**key_ordinal**|**tinyint**|Ordinal (de base 1) en el conjunto de columnas de clave.<br /><br /> 0 = No es una columna de clave; es un índice XML, un índice de almacén de columnas o un índice espacial.<br /><br /> Nota: Un índice espacial o XML no puede ser una clave porque las columnas subyacentes no son comparables, lo que significa que no se puede ordenar sus valores.|  
|**partition_ordinal**|**tinyint**|Ordinal (de base 1) en el conjunto de columnas de partición. Un índice de almacén de columnas en clúster puede tener como máximo 1 columna de particionamiento.<br /><br /> 0 = No es una columna de partición.|  
|**is_descending_key**|**bit**|1 = El orden de la columna de clave de índice es descendente.<br /><br /> 0 = La columna de clave de índice tiene una dirección de orden ascendente, o bien la columna es parte de un índice de almacén de columnas o hash.|  
|**is_included_column**|**bit**|1 = La columna es una columna sin clave que se agrega al índice utilizando la cláusula CREATE INDEX INCLUDE, o bien la columna forma parte de un índice de almacén de columnas.<br /><br /> 0 = La columna no es una columna incluida.<br /><br /> No se muestran las columnas agregadas implícitamente porque forman parte de la clave de agrupación en clústeres en **sys.index_columns**.<br /><br /> Las columnas agregadas implícitamente porque son una columna de partición se devuelven como 0.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelven todos los índices y columnas de índice para la tabla `Production.BillOfMaterials`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.object_id = OBJECT_ID('Production.BillOfMaterials');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
index_name                                                 column_name        index_column_id key_ordinal is_included_column  
---------------------------------------------------------- -----------------  --------------- ----------- -------------  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ProductAssemblyID  1               1           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ComponentID        2               2           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate StartDate          3               3           0  
PK_BillOfMaterials_BillOfMaterialsID                       BillOfMaterialsID  1               1           0  
IX_BillOfMaterials_UnitMeasureCode                         UnitMeasureCode    1               1           0  
  
(5 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
