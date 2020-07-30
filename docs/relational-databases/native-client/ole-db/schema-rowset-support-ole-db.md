---
title: Compatibilidad con conjuntos de filas de esquema (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: faa764aae707ae785c7cfd1cb324427b9a941376
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243896"
---
# <a name="schema-rowset-support-in-sql-server-native-client-ole-db"></a>Compatibilidad con conjuntos de filas de esquema en SQL Server Native Client (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client también admite la devolución de información de esquema de un servidor vinculado cuando se procesan [!INCLUDE[tsql](../../../includes/tsql-md.md)] consultas distribuidas.  
  
> [!NOTE]  
>  Aunque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite los sinónimos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no devuelve los metadatos de los sinónimos.  
  
 En las tablas siguientes se enumeran los conjuntos de filas de esquema y las columnas de restricción admitidas por el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client.  
  
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
 [Compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS Rowset &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usar tipos definidos por el usuario](../../../relational-databases/native-client/features/using-user-defined-types.md)  
  
  
