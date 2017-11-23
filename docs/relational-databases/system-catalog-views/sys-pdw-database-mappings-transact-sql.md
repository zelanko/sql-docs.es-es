---
title: Sys.pdw_database_mappings (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 4ae2c71e-dd56-41ea-a16b-64936175b459
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a08d9b0fdb770918c1bb7c8b08e253af58be314
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwdatabasemappings-transact-sql"></a>Sys.pdw_database_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Se asigna el **database_id**de bases de datos para el nombre físico utilizado en nodos de proceso y proporciona el **Id. principal** del propietario de base de datos en el sistema. Unir **sys.pdw_database_mappings** a **sys.databases** y **sys.pdw_nodes_pdw_physical_databases**.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar(36)**|El nombre físico de la base de datos de los nodos.<br /><br /> **el argumento physical_name** y **database_id** forman la clave para esta vista.||  
|database_id|**int**|El identificador de objeto de la base de datos. Vea [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).<br /><br /> **el argumento physical_name** y **database_id** forman la clave para esta vista.||  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se une sys.pdw_database_mappings a otras tablas del sistema para mostrar cómo se asignan las bases de datos.  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Sys.pdw_index_mappings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [Sys.pdw_table_mappings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [Sys.pdw_nodes_pdw_physical_databases &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  

