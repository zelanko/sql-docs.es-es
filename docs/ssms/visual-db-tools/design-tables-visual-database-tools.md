---
title: Creación y actualización de tablas
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Visual Database Tools [SQL Server], Table Designer
- Table Designer, designing tables
- opening tables
- opening Table Designer
- tables [SQL Server], opening
- Table Designer, opening
ms.assetid: c49e0155-5dcb-481f-9538-e1bde77105e2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/25/2017
ms.openlocfilehash: 026080e2eedf38cb65b3c8860335ab5432504a0a
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196863"
---
# <a name="create-and-update-database-tables"></a>Creación y actualización de tablas de bases de datos

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

El Diseñador de tablas es una herramienta visual que permite diseñar y visualizar [tablas de bases de datos](../../relational-databases/tables/tables.md). Puede usar el Diseñador de tablas de SQL Server Management Studio (SSMS) para crear, editar o eliminar tablas, columnas, claves, índices, relaciones y restricciones.  

## <a name="create-a-table"></a>Creación de una tabla

1. Haga clic con el botón derecho en el nodo **Tablas** de la base de datos y seleccione **Crear** > **Tabla**:

    ![Tabla nueva](../media/design-tables/new-table.png)

2. Agregue [columnas](column-properties-visual-database-tools.md) a la tabla:

    ![Diseño de una tabla](../media/design-tables/new-table2.png)

3. Cierre el diseñador y guarde los cambios.

## <a name="update-a-table"></a>Actualización de una tabla

1. Haga clic con el botón derecho en la tabla situada en el nodo **Tablas** de la base de datos y seleccione **Diseñar**:

    ![Actualización de una tabla](../media/design-tables/update-table.png)

2. Actualice la configuración de la tabla según sea necesario:

    ![Creación de una tabla](../media/design-tables/update-table2.png)

3. Cierre el diseñador y guarde los cambios.

## <a name="see-also"></a>Consulte también

- [Tablas](../../relational-databases/tables/tables.md)
- [Propiedades de la tabla &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/table-properties-visual-database-tools.md)
- [Propiedades de columna](column-properties-visual-database-tools.md)
- [Agregar columnas a una tabla](../../relational-databases/tables/add-columns-to-a-table-database-engine.md)
- [Claves principales y externas](../../relational-databases/tables/primary-and-foreign-key-constraints.md)
- [Índices](../../relational-databases/indexes/indexes.md)
- [Tipos de datos (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
- [Descarga de SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)
- [Crear una base de datos y agregar las tablas en Visual Studio](/visualstudio/data-tools/create-a-sql-database-by-using-a-designer)
