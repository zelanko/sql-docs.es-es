---
title: Mejorar el rendimiento de las consultas de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0658dc74-25eb-4486-bbd6-e85c1f92c272
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 26267a9c302e7bdc8ed833d19e026a8a76e2e977
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33178811"
---
# <a name="improve-the-performance-of-full-text-queries"></a>Mejorar el rendimiento de las consultas de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A continuación se ofrece una lista de recomendaciones que servirán para mejorar el rendimiento de las consultas de texto completo.  
  
 El rendimiento de las consultas de texto completo también se ve afectado por los recursos de hardware, como la memoria, la velocidad de disco y de CPU, y la arquitectura del equipo.  
  
-   Desfragmente el índice de la tabla base mediante [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   Reorganice el catálogo de texto completo mediante [ALTER FULLTEXT CATALOG REORGANIZE](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md). Asegúrese de hacerlo antes de realizar pruebas de rendimiento porque la ejecución de esta instrucción produce una mezcla maestra de los índices de texto completo del catálogo.  
  
-   Limite la selección de columnas de clave de texto completo a una columna pequeña. Aunque se admite una columna de 900 bytes, recomendamos usar una columna de clave menor en un índice de texto completo. **int** y **bigint** ofrecen el mejor rendimiento.  
  
-   Al usar una clave de texto completo de un tipo entero, se evita una combinación con la tabla de asignación **docid** . Por consiguiente, este tipo de clave mejora el rendimiento de las consultas en un orden de magnitud y mejora el rendimiento del rastreo. Podrían producirse ventajas adicionales en el rendimiento si la clave de texto completo también es la del índice clúster.  
  
-   Combine varios predicados [CONTAINS](../../t-sql/queries/contains-transact-sql.md) en un predicado CONTAINS. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede especificar una lista de columnas en la consulta CONTAINS.  
  
-   Si solo necesita información de clave de texto completo o de clasificación, use [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) o [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) en lugar de CONTAINS o FREETEXT, respectivamente.  
  
-   Para limitar los resultados y aumentar el rendimiento, use el parámetro *top_n_by_rank* de las funciones CONTAINSTABLE y FREETEXTTABLE. *top_n_by_rank* permite volver a recuperar solo las coincidencias más pertinentes. Use este parámetro únicamente si su escenario empresarial no requiere recuperar todas las coincidencias posibles (es decir, no requiere *recuperación total*).  
  
    > [!NOTE]  
    >  La recuperación total suele ser necesaria en escenarios legales, pero puede ser menos importante que el rendimiento en escenarios empresariales como un sistema de comercio electrónico.  
  
-   Compruebe el plan de consultas de texto completo para asegurarse de que se selecciona el plan de combinaciones adecuado. Use una sugerencia de combinación o una sugerencia de consulta si es necesario. Si se usa un parámetro en la consulta de texto completo, el valor de primera vez del parámetro determina el plan de consultas. Puede usar la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) OPTIMIZE FOR para hacer que la consulta realice la compilación con el valor deseado. Así se contribuye a lograr un plan de consultas determinista y un mejor rendimiento.  
  
-   Demasiados fragmentos del índice de texto completo pueden conducir a una degradación sustancial del rendimiento de las consultas. Para reducir el número de fragmentos, reorganice el catálogo de texto completo mediante la opción REORGANIZE de la instrucción [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esencialmente, esta instrucción combina todos los fragmentos en un único fragmento mayor y quita todas las entradas obsoletas del índice de texto completo.  
  
-   En la búsqueda de texto completo de , los operadores lógicos especificados en CONTAINSTABLE (AND, OR) se pueden implementar bien como combinaciones de SQL o dentro de las funciones con valores de tabla de transmisión por secuencias (STVF) de ejecución de texto completo. Normalmente, las consultas con solo un tipo de operadores lógicos se implementan meramente mediante la ejecución de texto completo, mientras que las consultas que mezclan operadores lógicos también presentan combinaciones de SQL. La implementación de un operador lógico dentro de la STVF de ejecución de texto completo utiliza algunas propiedades de índice especiales que hacen que sean mucho más rápidas que las combinaciones de SQL. Por esta razón, recomendamos que, siempre que sea posible, cree las consultas utilizando únicamente un tipo de operador lógico.  
  
-   Con las aplicaciones que contienen predicados de relación selectiva, las consultas que usan predicados relacionales selectivos y predicados de texto completo no selectivos podrían demostrar un mejor comportamiento cuando se escriben para utilizar el optimizador de consultas. Esto permite al optimizador de consultas decidir si puede explotar el predicado o una pila de intervalo para generar un plan de consulta efectivo. Este enfoque es más sencillo y a menudo más eficaz que indizar los datos relacionales como datos de texto completo.  
  
## <a name="related-resources"></a>Recursos relacionados  
 [Búsqueda de texto completo en SQL Server 2008: características internas y mejoras](http://go.microsoft.com/fwlink/?LinkId=129544)  
  
## <a name="see-also"></a>Ver también  
 [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)   
 [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
  
