---
title: Tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14dddf81-b502-49dc-a6b6-d18b1ae32d2b
author: rothja
ms.author: jroth
ms.openlocfilehash: 63566d7759c3a88f6c088707d6c7724cb4087f05
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050067"
---
# <a name="memory-optimized-tables"></a>Tablas con optimización para memoria
  OLTP en memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ayuda a mejorar el rendimiento de las aplicaciones OLTP mediante un acceso a los datos eficiente y optimizado para memoria, compilación nativa de la lógica de negocios, y algoritmos sin bloqueos y bloqueos temporales. La característica OLTP en memoria incluye tablas optimizadas para memoria y tipos de tablas, así como la compilación nativa de procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] para un acceso eficiente a estas tablas.  
  
 Para obtener más información acerca de las tablas optimizadas para memoria, vea:  
  
-   [Introducción a las tablas con optimización para memoria](memory-optimized-tables.md)  
  
     Define las tablas optimizadas para memoria y proporciona información acerca de la durabilidad de los datos, el acceso a datos de tablas optimizadas para memoria, el rendimiento y la escalabilidad.  
  
-   [Compilación nativa de tablas y procedimientos almacenados](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
     Define cómo se compilan en DLL las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa, y proporciona consideraciones de seguridad relacionadas.  
  
-   [Modificar tablas con optimización para memoria](altering-memory-optimized-tables.md)  
  
     Directrices para la actualización de tablas optimizadas para memoria (incluye el cambio de columnas de tabla, índices y bucket_count).  
  
-   [Descripción de las transacciones en tablas con optimización para memoria](../../database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
     En esta sección se proporcionan varios temas relacionados con la realización de transacciones en tablas optimizadas para memoria, incluidos los niveles de aislamiento de las transacciones y las transacciones entre contenedores.  
  
-   [Patrón de aplicación para crear particiones de tablas con optimización para memoria](application-pattern-for-partitioning-memory-optimized-tables.md)  
  
     Código de ejemplo detallado que muestra cómo emular tablas particionadas al usar tablas optimizadas para memoria.  
  
-   [Estadísticas para las tablas con optimización para memoria](statistics-for-memory-optimized-tables.md)  
  
     Define cómo se compilan las estadísticas para las tablas optimizadas para memoria y cómo mantener y actualizar manualmente estadísticas para tablas optimizadas para memoria.  
  
-   [Intercalaciones y páginas de códigos](../../database-engine/collations-and-code-pages.md)  
  
     Define las restricciones sobre intercalaciones compatibles y páginas de código para tablas optimizadas para memoria.  
  
-   [Tamaño de tabla y fila de las tablas con optimización para memoria](table-and-row-size-in-memory-optimized-tables.md)  
  
     Define el límite de 8060 sobre filas de tablas optimizadas para memoria y proporciona un ejemplo para calcular los tamaños de tablas y filas.  
  
-   [Guía del procesamiento de consultas para tablas con optimización para memoria](a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
     Proporciona información general del procesamiento de consultas tanto para las tablas optimizadas para memoria como para los procedimientos almacenados compilados de forma nativa.  
  
## <a name="see-also"></a>Consulte también  
 [OLTP en memoria &#40;optimización en memoria&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
