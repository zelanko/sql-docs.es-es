---
title: Funciones y vistas de metadatos de la tabla temporal | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e5d23ec9-7d18-40f6-add4-bea13132d0b9
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5151fdea0335c8f2ec67133091a451d1a20ffe20
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "74165731"
---
# <a name="temporal-table-metadata-views-and-functions"></a>Funciones y vistas de metadatos de la tabla temporal

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] incluyen una serie de funciones y vistas de metabase que permiten a los administradores recuperar información acerca de las tablas temporales.

La información acerca de las tablas temporales se expone en las siguientes vistas de metadatos:

- [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)
- [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)
- [sys.periods &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-periods-transact-sql.md)

 La información acerca de las tablas temporales se expone en las siguientes funciones de metadatos:

- [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)

- [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)

- [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)

## <a name="next-steps"></a>Pasos siguientes

- [Tablas temporales](../../relational-databases/tables/temporal-tables.md)
- [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Creación de particiones con tablas temporales](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Limitaciones y consideraciones de las tablas temporales](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Seguridad de la tabla temporal](../../relational-databases/tables/temporal-table-security.md)
- [Administración de la retención de datos históricos en las tablas temporales con control de versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
