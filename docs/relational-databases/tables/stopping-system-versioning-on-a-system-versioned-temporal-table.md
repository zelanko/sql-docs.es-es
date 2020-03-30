---
title: Detención del control de versiones en una tabla temporal con control de versiones | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74b222b8014b3a0e41e34d588d5893b7f4aaf9b8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "74165455"
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>Detención del control de versiones en una tabla temporal con control de versiones del sistema

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Es posible que quiera detener el control de versiones en una tabla temporal de forma temporal o permanente. Puede hacerlo estableciendo la cláusula **SYSTEM_VERSIONING** en **OFF**.

## <a name="setting-system_versioning--off"></a>Valor SYSTEM_VERSIONING = OFF

Detenga el control de versiones del sistema si quiere realizar operaciones de mantenimiento concretas en una tabla temporal o si ya no necesita una tabla con control de versiones. Como resultado de esta operación obtendrá dos tablas independientes:

- Tabla actual con definición del período

- Tabla de historial como una tabla normal

### <a name="important-remarks"></a>Notas importantes

- La tabla de historial **dejará** de capturar la actualizaciones mientras dure **SYSTEM_VERSIONING = OFF**.
- No se produce ninguna pérdida de datos en la **tabla temporal** cuando se establece **SYSTEM_VERSIONING = OFF** o se quita el período **SYSTEM_TIME**.
- Si establece **SYSTEM_VERSIONING = OFF** y no quita el período **SYSTEM_TIME** , el sistema seguirá actualizando las columnas de período en cada operación de inserción y actualización. Las eliminaciones en la tabla actual serán permanentes.
- Quite el período **SYSTEM_TIME** para quitar las columnas de período completamente.
- Al establecer **SYSTEM_VERSIONING = OFF**, todos los usuarios que tengan permisos suficientes podrán modificar el esquema y el contenido de la tabla de historial o incluso eliminarla permanentemente.

### <a name="permanently-remove-system_versioning"></a>Quitar permanentemente SYSTEM_VERSIONING

En este ejemplo se quita permanentemente SYSTEM_VERSIONING y se quitan las columnas de período completamente. La eliminación de las columnas de período es opcional.

```sql
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/
ALTER TABLE dbo.Department
DROP PERIOD FOR SYSTEM_TIME;
```

### <a name="temporarily-remove-system_versioning"></a>Quitar temporalmente SYSTEM_VERSIONING

Esta es la lista de operaciones que exigen que el control de versiones del sistema esté establecido en **OFF**:

- Eliminación de datos innecesarios del historial (**DELETE** or **TRUNCATE**)
- Eliminación de datos de la tabla actual sin control de versiones (**DELETE**, **TRUNCATE**)
- Partición **SWITCH OUT** de la tabla actual
- Partición **SWITCH IN** en la tabla de historial

En este ejemplo se detiene temporalmente SYSTEM_VERSIONING para que se puedan realizar operaciones de mantenimiento concretas. Si se detiene temporalmente el control de versiones como un requisito previo para el mantenimiento de una tabla, se recomienda encarecidamente hacerlo en una transacción para mantener la coherencia de los datos.

> [!NOTE]
> Al volver a activar el control de versiones del sistema, no olvide especificar el argumento HISTORY_TABLE. Si no lo hace, el resultado será la creación de una tabla de historial que se asociará a la tabla actual. La tabla de historial original seguirá existiendo como una tabla normal, pero no se asociará con la tabla actual.

```sql
BEGIN TRAN
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
TRUNCATE TABLE [History].[DepartmentHistory]
WITH (PARTITIONS (1,2))
ALTER TABLE dbo.Department SET
(
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
COMMIT ;
```

## <a name="next-steps"></a>Pasos siguientes

- [Tablas temporales](../../relational-databases/tables/temporal-tables.md)
- [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Administración de la retención de datos históricos en las tablas temporales con control de versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Creación de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [Modificación de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [Cambiar el esquema de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
