---
title: Crear un script de Transact-SQL para ejecutar un seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
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
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1915ac39a66ab2aee74db29ade8485755348a76d
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>Crear un script de Transact-SQL para ejecutar un seguimiento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo crear un script de Transact-SQL a partir de un archivo o una tabla de seguimiento existente mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>Para crear un script de Transact-SQL para ejecutar un seguimiento  
  
1.  Abra un archivo o una tabla de seguimiento. Para obtener más información, vea [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) o el Asistente para la optimización del [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
2.  En el menú**Archivo**seleccione **Exportar**, **Definición de seguimiento de scripts**y, a continuación, haga clic en la versión que corresponda al servidor cuyo seguimiento desee realizar.  
  
3.  En el cuadro de diálogo **Guardar como** , especifique un nombre para el archivo de script y haga clic en **Guardar**.  
  
## <a name="see-also"></a>Ver también  
 [Plantillas y permisos de SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
