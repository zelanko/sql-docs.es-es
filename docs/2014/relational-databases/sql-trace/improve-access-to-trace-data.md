---
title: Mejorar el acceso a los datos de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], space
- SQL Server Profiler, space
- space [SQL Server], SQL Server Profiler
ms.assetid: c260c000-fd53-4831-993f-df6894f3228b
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86844ecd42735e74fbacf8909c1fa1bdb8c40ce7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37242375"
---
# <a name="improve-access-to-trace-data"></a>Mejorar el acceso a los datos de seguimiento
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] usa el espacio del directorio **temp** para mejorar el acceso a los datos de seguimiento. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] requiere al menos 10 megabytes (MB) de espacio libre. Si se redujera la cantidad de espacio disponible a menos de 10 MB mientras se utiliza el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], se detendrían todas las funciones del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
 Cuando el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] utiliza espacio del directorio **temp** , este uso de espacio puede dar lugar a que el directorio **temp** crezca rápidamente. Para evitar problemas del crecimiento de un archivo, puede colocar el directorio **temp** en una unidad que no pertenezca al sistema si cambia el valor de la variable de entorno TEMP.  
  
 El procedimiento siguiente describe cómo cambiar el valor de la variable de entorno TEMP en la mayoría de los sistemas operativos Microsoft Windows. Para obtener más información acerca del establecimiento de variables de entorno, consulte la documentación del sistema operativo Windows.  
  
### <a name="to-change-the-temp-environment-variable-in-windows-operating-systems"></a>Para cambiar la variable de entorno TEMP en sistemas operativos Windows  
  
1.  En el menú **Inicio** , elija **Panel de control**y haga clic en **Sistema**.  
  
2.  En el cuadro de diálogo **Propiedades del sistema** , haga clic en la pestaña **Opciones avanzadas** y, a continuación, haga clic en **Variables de entorno**.  
  
3.  Desplácese hacia abajo por la lista **Variables del sistema**, seleccione la fila que corresponda a la variable **TEMP** y haga clic en **Modificar**.  
  
4.  En el cuadro de diálogo **Modificar la variable del sistema** , especifique la ruta de acceso y el nombre de la unidad y el directorio en los que desea colocar el directorio **temp** .  
  
5.  Haga clic en **Aceptar** para guardar el cambio.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
