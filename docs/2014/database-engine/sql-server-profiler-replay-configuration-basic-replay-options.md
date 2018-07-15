---
title: SQL Server Profiler - configuración de reproducción (opciones básicas de reproducción) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.pro.replay.generaloptions.f1
helpviewer_keywords:
- Replay Configuration dialog box
ms.assetid: 85a1dec6-9bbc-477a-86c5-b463db9ebb31
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cef06029d3ac1af86955f7a2df89fbe570c15245
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178382"
---
# <a name="sql-server-profiler---replay-configuration-basic-replay-options"></a>Analizador SQL Server (Configuración de reproducción/página Opciones básicas de reproducción)
  En el cuadro de diálogo **Configuración de reproducción** , utilice la página **Opciones básicas de reproducción** para especificar cómo reproducir una tabla o un archivo de seguimiento.  
  
 Para ver esta ventana, utilice el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para abrir un seguimiento o un archivo de seguimiento que contenga los eventos adecuados para la reproducción. Para más información, consulte [Replay Requirements](../tools/sql-server-profiler/replay-requirements.md). Cuando la tabla o el archivo de seguimiento están abiertos, en el menú **Reproducir** , haga clic en **Iniciar**y, a continuación, establezca la conexión con la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] donde desea reproducir el seguimiento.  
  
## <a name="options"></a>Opciones  
 **Servidor de reproducción**  
 Muestra la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la que se establece la conexión para la reproducción.  
  
 **Cambiar...**  
 Inicia el cuadro de diálogo **Conectar al servidor** para conectarse a otro servidor.  
  
 **Guardar en el archivo**  
 Guarda los resultados de la reproducción en un archivo. [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] Muestra el cuadro de diálogo de archivo estándar, donde puede especificar la ubicación para guardar el archivo.  
  
 **Guardar en la tabla**  
 Guarda los resultados de la reproducción en una tabla. [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] muestra el cuadro de diálogo de selección de tabla, en el puede especificar la ubicación en la que se guarda la tabla.  
  
 **Número de subprocesos de reproducción**  
 Especifique el número de subprocesos de reproducción que se utilizarán simultáneamente. Un número mayor consume más recursos durante la reproducción, pero ésta es más rápida y simultánea.  
  
 **Reproducir eventos en el orden del seguimiento**  
 Reproduce los eventos de forma secuencial. Utilice esta opción si reproduce un seguimiento para depuración.  
  
 **Reproducir eventos mediante múltiples subprocesos**  
 Reproduce los eventos de forma simultánea. Esta opción es más rápida que la reproducción secuencial, pero deshabilita la depuración. Los eventos se ordenan dentro de sus identificadores de proceso del sistema (SPID).  
  
 **Mostrar los resultados de la reproducción**  
 Muestra el resultado de la reproducción en el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproducir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Reproducir seguimientos](../tools/sql-server-profiler/replay-traces.md)  
  
  
