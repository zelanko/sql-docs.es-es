---
title: Creación de una tabla temporal con control de versiones del sistema con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3eabb6fd9e0089140d2670c708c2190de649eabb
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002127"
---
# <a name="creating-a-memory-optimized-system-versioned-temporal-table"></a>Creación de una tabla temporal con control de versiones del sistema con optimización para memoria

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Igual que crea una tabla de historial basada en disco, puede crear una tabla temporal optimizada para memoria de varias maneras.

> [!NOTE]
> Para crear tablas optimizadas para memoria, primero debe crear el [grupo de archivos optimizados para memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md).

Esta opción es práctica en casos en los que quiera controlar la nomenclatura y, aun así, delegar al sistema la generación de la tabla de historial con la configuración predeterminada. En el ejemplo siguiente, una tabla temporal con control de versiones del sistema optimizada para memoria se vincula a una nueva tabla del historial basada en disco.

```sql
CREATE SCHEMA History
GO
CREATE TABLE dbo.Department
   (  
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
       MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,
          SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )
    );
```

La creación de una tabla temporal vinculada a una tabla de historial existente resulta útil cuando desea control de versiones del sistema mediante una tabla existente, por ejemplo, cuando quiera migrar una solución temporal personalizada como cuando desea migrar una solución temporal personalizada a compatibilidad integrada. En el ejemplo siguiente, se crea una nueva tabla temporal vinculada a una tabla de historial existente.

```sql
--Existing table
CREATE TABLE Department_History
   (
      DepartmentNumber char(10) NOT NULL,
      DepartmentName varchar(50) NOT NULL,
      ManagerID int NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 NOT NULL, SysEndTime datetime2 NOT NULL
   )
;
--Temporal table
CREATE TABLE Department
   (
      DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,
      DepartmentName varchar(50) NOT NULL,
      ManagerID INT NULL,
      ParentDepartmentNumber char(10) NULL,
      SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,
      SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,
      PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
   )
WITH
   (
      SYSTEM_VERSIONING = ON
         (  
            HISTORY_TABLE = dbo.Department_History
            , DATA_CONSISTENCY_CHECK = ON
         )  
      , MEMORY_OPTIMIZED = ON
      , DURABILITY = SCHEMA_AND_DATA
   )
;
```

## <a name="see"></a>Vea

- [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Trabajo con tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [Supervisión de tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [Consideraciones de rendimiento con tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)
- [Tablas temporales](../../relational-databases/tables/temporal-tables.md)
- [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Administración de la retención de datos históricos en las tablas temporales con control de versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Funciones y vistas de metadatos de la tabla temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
