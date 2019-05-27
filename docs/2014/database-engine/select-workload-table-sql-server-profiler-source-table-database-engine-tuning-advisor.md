---
title: SQL Server Profiler - Asesor de optimización de motor de base de datos de tabla origen - Seleccionar tabla de carga de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.tools.sourcetable.f1
helpviewer_keywords:
- Select Workload Table dialog box
- Source Table dialog box
ms.assetid: 51185be7-7092-480a-a52c-cf7786c4a0a0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 973680d07c3bd6a304e63f4b3fde0e228f0f7bff
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088879"
---
# <a name="sql-server-profiler---source-table-database-engine-tuning-advisor---select-workload-table"></a>-Asistente para la optimización el motor de base de datos de tabla origen - carga de trabajo seleccione tabla de SQL Server Profiler
  El Asistente para la optimización de [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] y el [!INCLUDE[ssDE](../includes/ssde-md.md)] de Microsoft utilizan este cuadro de diálogo para seleccionar las tablas.  
  
 En [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], use el cuadro de diálogo **Tabla de origen** a fin de especificar una tabla de origen para una tabla de seguimiento. Esta última es una tabla desde la que se carga un seguimiento y su contenido se ve y usa para reproducir el seguimiento.  
  
 En el Asistente para la optimización de [!INCLUDE[ssDE](../includes/ssde-md.md)], use el cuadro de diálogo **Seleccionar tabla de carga de trabajo** para seleccionar una tabla de base de datos que contenga información de seguimiento de [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], que puede usarse como carga de trabajo de optimización, o bien para obtener una vista previa del contenido de la tabla antes de iniciar el análisis de optimización.  
  
## <a name="options"></a>Opciones  
 **SQL Server**  
 Especifica la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conectada actualmente. Este campo se llena automáticamente y no puede actualizarse.  
  
 **Base de datos**  
 Especifica la base de datos en la que se ubica la tabla de seguimiento.  
  
 **Propietario**  
 Specifies the owner of the trace table. Este campo se llena automáticamente como **dbo**.  
  
 **Table**  
 Especifica el nombre de la tabla de seguimiento desde la que debe leerse el seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Guardar los resultados de un seguimiento en una tabla &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Database Engine Tuning Advisor](../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
