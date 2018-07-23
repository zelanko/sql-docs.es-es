---
title: Limitaciones de Stretch Database | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5537ba71505cf14657e69f0e3ec5ccb8b125ebf3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38044188"
---
# <a name="limitations-for-stretch-database"></a>Limitaciones de Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Obtenga información sobre las limitaciones de las tablas habilitadas para Stretch y sobre las limitaciones que evitan actualmente habilitar Stretch para una tabla.  
  
##  <a name="Caveats"></a> Limitaciones de las tablas habilitadas para Stretch  
  
Las tablas habilitadas para Stretch tienen las siguientes limitaciones.  
  
### <a name="constraints"></a>Restricciones  
-   No se exige la unicidad de restricciones UNIQUE y restricciones PRIMARY KEY en la tabla de Azure que contiene los datos migrados.  
  
### <a name="dml-operations"></a>Operaciones DML  
-   No se pueden actualizar ni eliminar filas que se hayan migrado ni filas aptas para migración en una tabla habilitada para Stretch ni en una vista que incluya tablas habilitadas para Stretch.  
  
-   No se pueden insertar filas en una tabla habilitada para Stretch en un servidor vinculado.  
  
### <a name="indexes"></a>Índices  
-   No se puede crear un índice de una vista que incluya tablas habilitadas para Stretch.  
  
-   Los filtros de los índices de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se propagan a la tabla remota.  
  
##  <a name="Limitations"></a> Limitaciones que actualmente evitan habilitar Stretch para una tabla  
   
 Los siguientes aspectos actualmente evitan habilitar Stretch para una tabla.  
  
 ### <a name="table-properties"></a>Propiedades de tabla  
-   Tablas que tienen más de 1023 columnas o más de 998 índices  
  
-   Tablas de archivos o tablas que contienen datos FILESTREAM  
  
-   Tablas que se replican o que usan activamente el seguimiento de cambios o la captura de datos modificados  
  
-   Tablas con optimización para memoria  
  
### <a name="data-types"></a>Tipos de datos  
-   text, ntext e image  
  
-   TIMESTAMP  
  
-   sql_variant  
  
-   XML  
  
-   Tipos de datos CLR, incluidos tipos CLR definidos por el usuario geometry, geography, hierarchyid  
  
 ### <a name="column-types"></a>Tipos de columna  
 -   COLUMN_SET  
  
-   Columnas calculadas  
  
### <a name="constraints"></a>Restricciones  
-   Restricciones DEFAULT y restricciones CHECK  
  
-   Restricciones de clave externa que hacen referencia a la tabla. En una relación de elementos primarios y secundarios (por ejemplo, Order y Order_Detail), puede habilitar Stretch para la tabla secundaria (Order_Detail) pero no para la tabla principal (Order).  
  
### <a name="indexes"></a>Índices  
-   Índices de texto completo  
  
-   índices XML  
  
-   Índices espaciales  
  
-   Vistas indexadas que hacen referencia a la tabla  
  
## <a name="see-also"></a>Ver también  
 [Identificar bases de datos y tablas para Stretch Database al ejecutar el Asesor de Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table (Habilitar Stretch Database para una tabla)](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
