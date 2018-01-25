---
title: "Rendimiento de las tablas temporales con control de versiones del sistema con optimización para memoria | Microsoft Docs"
ms.custom: 
ms.date: 03/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
caps.latest.revision: "14"
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cc7a8ac4a47a479e87702ddd429a95ca00b8336
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>Rendimiento de las tablas temporales con control de versiones del sistema con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describen algunos aspectos a tener en cuenta sobre el rendimiento cuando se utilizan tablas temporales con control de versiones optimizadas para memoria.  
  
-   Al agregar control de versiones del sistema a una tabla no temporal existente, el rendimiento esperado se puede ver afectado por las operaciones de actualización y eliminación porque la tabla de historial se actualiza automáticamente.  
  
-   Cada actualización y eliminación se registra en una tabla de historial interna optimizada para memoria, por lo que puede experimentar un consumo de memoria inesperado si su carga de trabajo usa esas dos operaciones de forma masiva. Por lo tanto, recomendamos lo siguiente:  
  
    -   No libre espacio para aumentar la memoria RAM disponible cuando realice eliminaciones masivas de la tabla actual. Considere la posibilidad de eliminar los datos en varios lotes con el vaciado manual de los datos invocados entre uno y otro invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md), o mientras **SYSTEM_VERSIONING = OFF**.  
  
    -   No realice actualizaciones masivas de tablas de una vez, ya que puede dar lugar a un consumo de memoria equivalente a dos veces la cantidad necesaria para actualizar una tabla optimizada para memoria no temporal. El consumo doble de memoria es temporal porque la tarea de vaciado de datos trabaja regularmente para mantener el consumo de memoria de la tabla de almacenamiento provisional externa dentro de los límites proyectados en el estado estable (aproximadamente el 10 % del consumo de memoria de la tabla temporal actual). Considere la posibilidad de realizar actualizaciones masivas en varios lotes o mientras **SYSTEM_VERSIONING = OFF**, por ejemplo, usar actualizaciones para establecer los valores predeterminados para las columnas recién agregadas.  
  
-   El período de activación de la tarea de vaciado de datos no es configurable, pero puede aplicar el proceso invocando [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md).  
  
-   Considere la posibilidad de usar el almacén de columnas en clúster como opción de almacenamiento para tablas de historial basadas en disco, en especial si tiene pensado ejecutar solicitudes de análisis sobre datos históricos que utilizan funciones de agregación o de división de particiones. En ese caso, el almacén de columnas en clúster será una buena opción para las tablas de historial dado que proporciona una buena compresión de los datos y un comportamiento que facilita las inserciones, lo que está en consonancia con el modo en que se generan los datos de historial.  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Performance%20Considerations%20with%20Memory-Optimized%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>Ver también  
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Creación de una tabla temporal con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [Trabajo con tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [Supervisión de tablas temporales con control de versiones del sistema con optimización para memoria](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Funciones y vistas de metadatos de la tabla temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
