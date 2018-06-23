---
title: Ver información del filtro (SQL Server Profiler) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7936ad4df64746697b5c9d0ff8f2be1c7a5cbef1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109395"
---
# <a name="view-filter-information-sql-server-profiler"></a>Ver información de un filtro (SQL Server Profiler)
  En este tema se describe cómo ver filtros de columnas de datos para clases de eventos mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-view-filter-information"></a>Para ver la información del filtro  
  
1.  Abra un archivo de seguimiento, tabla de seguimiento o script SQL y, en el menú **Archivo** , haga clic en **Propiedades**. Si edita una plantilla de seguimiento o crea un seguimiento nuevo, omita este paso.  
  
2.  En la pestaña **Selección de eventos** , haga clic con el botón derecho en el nombre de la columna de datos del filtro que quiere ver y haga clic en **Editar filtro de columna**.  
  
3.  En el cuadro de diálogo **Editar filtro** , expanda los operadores de comparación de filtros para ver el valor asignado al criterio especificado. Repita los pasos 2 y 3 para todas las columnas para las que desee ver información del filtro.  
  
> [!NOTE]  
>  Los operadores de comparación con valores asignados se muestran en negrita.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  