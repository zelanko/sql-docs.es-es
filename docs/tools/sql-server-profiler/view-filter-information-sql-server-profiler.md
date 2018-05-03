---
title: Ver información del filtro (SQL Server Profiler) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8199efbe27c798195e814aeffbf10a4b250fe0de
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="view-filter-information-sql-server-profiler"></a>Ver información de un filtro (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo ver filtros de columnas de datos para clases de eventos mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-view-filter-information"></a>Para ver la información del filtro  
  
1.  Abra un archivo de seguimiento, tabla de seguimiento o script SQL y, en el menú **Archivo** , haga clic en **Propiedades**. Si edita una plantilla de seguimiento o crea un seguimiento nuevo, omita este paso.  
  
2.  En la pestaña **Selección de eventos** , haga clic con el botón derecho en el nombre de la columna de datos del filtro que quiere ver y haga clic en **Editar filtro de columna**.  
  
3.  En el cuadro de diálogo **Editar filtro** , expanda los operadores de comparación de filtros para ver el valor asignado al criterio especificado. Repita los pasos 2 y 3 para todas las columnas para las que desee ver información del filtro.  
  
> [!NOTE]  
>  Los operadores de comparación con valores asignados se muestran en negrita.  
  
## <a name="see-also"></a>Ver también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
