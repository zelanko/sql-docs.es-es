---
title: Sys.database_service_objectives (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- grupo elástico
- grupo elástico, administración
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 4174e59fd451d1d709decbbc8955c9fe2329703e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079413"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>Sys.database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Devuelve la edición (nivel de servicio), el objetivo de servicio (plan de tarifa) y nombre del grupo elástico, si existe, para una base de datos SQL de Azure o Azure SQL Data Warehouse. Si inició sesión en la base de datos maestra en un servidor de Azure SQL Database, devuelve información sobre todas las bases de datos. Para Azure SQL Data Warehouse, debe estar conectado a la base de datos maestra.  
  
  
 Para obtener información sobre los precios, consulte [opciones de base de datos SQL y el rendimiento: Precios de SQL Database](https://azure.microsoft.com/pricing/details/sql-database/) y [los precios de SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Para cambiar la configuración del servicio, consulte [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) y [ALTER DATABASE (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest).  
  
 La vista sys.database_service_objectives contiene las siguientes columnas.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|int|El identificador de la base de datos, único en una instancia del servidor de Azure SQL Database. Puede unir con [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edición|sysname|El nivel de servicio para el almacenamiento de datos o base de datos: **Básico**, **estándar**, **Premium** o **almacenamiento de datos**.|  
|service_objective|sysname|El plan de tarifa de la base de datos. Devuelve si la base de datos está en un grupo elástico, **ElasticPool**.<br /><br /> En el **básica** nivel devuelve **básica**.<br /><br /> **Base de datos única en un nivel de servicio estándar** devuelve uno de los siguientes: S0, S1, S2, S3, S4, S6, S7, S9 o S12.<br /><br /> **Base de datos única en el nivel premium** devuelve de las acciones siguientes: P1, P2, P4, P6, P11 o P15.<br /><br /> **SQL Data Warehouse** devuelve DW100 a través de DW30000c.|  
|elastic_pool_name|sysname|El nombre de la [grupo elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) que pertenece la base de datos. Devuelve **NULL** si la base de datos es una base de datos única o un warehoue de datos.|  
  
## <a name="permissions"></a>Permisos  
 Requiere **dbManager** permiso en la base de datos maestra.  En el nivel de base de datos, el usuario debe ser el creador o propietario.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se puede ejecutar en la base de datos maestra o en las bases de datos de usuario de Azure SQL Database. La consulta devuelve el nombre, el servicio y la información de nivel de rendimiento de las bases de datos.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
