---
title: Sys.database_service_objectives (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2016
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords:
- grupo elástico
- grupo elástico, administración
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 320d8d0dd434c4453a8004a0237bc9d2cbd9f352
ms.sourcegitcommit: 84cc5ed00833279da3adbde9cb6133a4e788ed3f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2018
ms.locfileid: "39216976"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>Sys.database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Devuelve la edición (nivel de servicio), el objetivo de servicio (plan de tarifa) y nombre del grupo elástico, si existe, para una base de datos SQL de Azure o Azure SQL Data Warehouse. Si ha iniciado sesión la base de datos maestra en un servidor de Azure SQL Database, devuelve información sobre todas las bases de datos. Para Azure SQL Data Warehouse, debe estar conectado a la base de datos maestra.  
  
  
 Para obtener información sobre los precios, consulte [opciones de base de datos SQL y el rendimiento: precios de SQL Database](https://azure.microsoft.com/pricing/details/sql-database/) y [precios de SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Para cambiar la configuración del servicio, consulte [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) y [ALTER DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
  
 La vista sys.database_service_objectives contiene las siguientes columnas.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|INT|El identificador de la base de datos, único en una instancia del servidor de Azure SQL Database. Puede unir con [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edición|sysname|El nivel de servicio para el almacenamiento de datos o base de datos: **básica**, **estándar**, **Premium** o **Data Warehouse**.|  
|service_objective|sysname|El plan de tarifa de la base de datos. Devuelve si la base de datos está en un grupo elástico, **ElasticPool**.<br /><br /> En el **básica** nivel devuelve **básica**.<br /><br /> **Base de datos única en un nivel de servicio estándar** devuelve uno de los siguientes: S0, S1, S2, S3, S4, S6, S7, S9 o S12.<br /><br /> **Base de datos única en el nivel premium** devuelve de las siguientes acciones: P1, P2, P4, P6, P11 o P15.<br /><br /> **SQL Data Warehouse** devuelve DW100 a través de DW10000c.|  
|elastic_pool_name|sysname|El nombre de la [grupo elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) que pertenece la base de datos. Devuelve **NULL** si la base de datos es una base de datos única o un warehoue de datos.|  
  
## <a name="permissions"></a>Permisos  
 Requiere **dbManager** permiso en la base de datos maestra.  En el nivel de base de datos, el usuario debe ser el creador o propietario.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se puede ejecutar en la base de datos maestra o en las bases de datos de usuario. La consulta devuelve el nombre, el servicio y la información de nivel de rendimiento de las bases de datos.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
