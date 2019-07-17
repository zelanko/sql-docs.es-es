---
title: Reproducir un script Transact-SQL (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6570eeacfe7da346cc0d41352888f5acc57baf2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211067"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Reproducir un script Transact-SQL (SQL Server Profiler)
  Cuando pruebe posibles soluciones para un problema de rendimiento, utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para reproducir scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] y compare el rendimiento antes y después de los cambios.  
  
### <a name="to-replay-a-transact-sql-script"></a>Para reproducir un script Transact-SQL  
  
1.  En el menú **Archivo** , seleccione **Abrir**y haga clic en **Archivo de script**.  
  
2.  Seleccione el archivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que desee abrir. Asegúrese de que el script [!INCLUDE[tsql](../../includes/tsql-md.md)] contiene los eventos necesarios para la reproducción. Para más información, consulte [Replay Requirements](replay-requirements.md).  
  
3.  En el menú **Reproducir** , haga clic en **Iniciar**y conéctese al servidor en el que desee reproducir el script.  
  
4.  Compruebe la configuración en el cuadro de diálogo **Configuración de reproducción** y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Reproducir seguimientos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
