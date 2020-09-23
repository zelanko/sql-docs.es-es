---
title: Compatibilidad con conjuntos de filas de esquema (OLE DB) | Microsoft Docs
description: OLE DB para SQL Server permite devolver información del esquema de un servidor vinculado al procesar consultas distribuidas de Transact-SQL.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- OLE DB Driver for SQL Server, schema rowsets
- rowsets [OLE DB], schema
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38571c97516309b3a90731f8e95f928dc0ad5591
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861802"
---
# <a name="schema-rowset-support-ole-db"></a>Compatibilidad con conjuntos de filas de esquema (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server también permite devolver información del esquema de un servidor vinculado al procesar consultas distribuidas de [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  Aunque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite los sinónimos, OLE DB Driver for SQL Server no devuelve metadatos de sinónimos.  
  
 En las tablas siguientes, se enumeran los conjuntos de filas de esquema y las columnas de restricción que admite el controlador OLE DB para SQL Server.  
  
|Conjunto de filas de esquema|Columnas de restricción|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> Las siguientes columnas adicionales son específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:<br /><br /> COLUMN_LCID, que es el identificador de configuración regional de la intercalación. COLUMN_LCID es el mismo valor que un LCID de Windows.<br /><br /> COLUMN_COMPFLAGS define las comparaciones que se admiten en la intercalación. El formato de datos es igual que en DBPROB_FINDCOMPAREOPS.<br /><br /> COLUMN_SORTID, que es el estilo de ordenación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la intercalación.<br /><br /> COLUMN_TDSCOLLATION, que es la intercalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de la columna.<br /><br /> IS_COMPUTED, que es VARIANT_TRUE si la columna es una columna calculada y VARIANT_FALSE de lo contrario.|  
|DBSCHEMA_FOREIGN_KEYS|Se admiten todas las restricciones.<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|Solo se admiten las restricciones 1, 2, 3 y 5.<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Se admiten todas las restricciones.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|Se admiten las restricciones 1, 2 y 3.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES solo devuelve procedimientos que puede ejecutar el usuario actual o para los que se ha concedido permiso VIEW DEFINITION al usuario actual.|  
|DBSCHEMA_PROVIDER_TYPES|Se admiten todas las restricciones.<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|Se admiten todas las restricciones.<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|Se admiten todas las restricciones.<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|Se admiten todas las restricciones.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../../oledb/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS Rowset &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [Usar tipos definidos por el usuario](../../oledb/features/using-user-defined-types.md)  
  
  
