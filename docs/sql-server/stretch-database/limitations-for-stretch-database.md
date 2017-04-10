---
title: "Limitaciones de Stretch Database | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/14/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch Database, limitaciones"
  - "Stretch Database, problemas de bloqueo"
  - "limitaciones (Stretch Database)"
  - "problemas de bloqueo (Stretch Database)"
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Limitaciones de Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Obtenga información sobre las limitaciones de las tablas habilitadas para Stretch y sobre las limitaciones que evitan actualmente habilitar Stretch para una tabla.  
  
##  <a name="Caveats"></a> Limitaciones de las tablas habilitadas para Stretch  
  
Las tablas habilitadas para Stretch tienen las siguientes limitaciones.  
  
### Restricciones  
-   No se exige la unicidad de restricciones UNIQUE y restricciones PRIMARY KEY en la tabla de Azure que contiene los datos migrados.  
  
### Operaciones DML  
-   No se pueden actualizar ni eliminar filas que se hayan migrado ni filas aptas para migración en una tabla habilitada para Stretch ni en una vista que incluya tablas habilitadas para Stretch.  
  
-   No se pueden insertar filas en una tabla habilitada para Stretch en un servidor vinculado.  
  
### Índices  
-   No se puede crear un índice de una vista que incluya tablas habilitadas para Stretch.  
  
-   Los filtros de los índices de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se propagan a la tabla remota.  
  
##  <a name="Limitations"></a> Limitaciones que actualmente evitan habilitar Stretch para una tabla  
   
 Los siguientes aspectos actualmente evitan habilitar Stretch para una tabla.  
  
 ### Propiedades de tabla  
-   Tablas que tienen más de 1023 columnas o más de 998 índices  
  
-   Tablas de archivos o tablas que contienen datos FILESTREAM  
  
-   Tablas que se replican o que usan activamente el seguimiento de cambios o la captura de datos modificados  
  
-   Tablas con optimización para memoria  
  
 ### Tipos de datos  
 -   text, ntext e image  
  
-   timestamp  
  
-   sql_variant  
  
-   XML  
  
-   Tipos de datos CLR, incluidos tipos CLR definidos por el usuario geometry, geography, hierarchyid  
  
 ### Tipos de columna  
 -   COLUMN_SET  
  
-   Columnas calculadas  
  
### Restricciones  
-   Restricciones DEFAULT y restricciones CHECK  
  
-   Restricciones de clave externa que hacen referencia a la tabla. En una relación de elementos primarios y secundarios (por ejemplo, Order y Order_Detail), puede habilitar Stretch para la tabla secundaria (Order_Detail) pero no para la tabla principal (Order).  
  
### Índices  
-   Índices de texto completo  
  
-   índices XML  
  
-   Índices espaciales  
  
-   Vistas indexadas que hacen referencia a la tabla  
  
## Vea también  
 [Identificar bases de datos y tablas para Stretch Database al ejecutar el Asesor de Stretch Database](../../sql-server/stretch-database/stretch database databases and tables - stretch database advisor.md)   
 [Habilitación de Stretch Database para una base de datos](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Habilitar Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  