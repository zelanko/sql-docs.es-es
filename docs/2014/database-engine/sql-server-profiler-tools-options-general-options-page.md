---
title: SQL Server Profiler - opciones de herramientas (página de opciones generales) | Microsoft Docs
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
- sql12.pro.replay.tools.generaloptions.f1
helpviewer_keywords:
- General Options dialog box
ms.assetid: a888246d-ccfe-415f-bbdc-d6adafac250a
caps.latest.revision: 26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 695c1fc16604c4ce0e0a49da67016acbaa663d50
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243075"
---
# <a name="sql-server-profiler---tools-options-general-options-page"></a>SQL Server Profiler - opciones de herramientas (página de opciones generales)
  Utilice el cuadro de diálogo **Opciones generales** para ver o especificar las siguientes opciones.  
  
## <a name="options"></a>Opciones  
  
### <a name="display-options"></a>Opciones de visualización  
 **Nombre de fuente**  
 Muestra el nombre de la fuente utilizada en la cuadrícula de resultados de seguimiento durante los seguimientos.  
  
 **Tamaño de fuente**  
 Muestra el tamaño de la fuente utilizada en la cuadrícula de resultados de seguimiento durante los seguimientos.  
  
 **Elegir fuente**  
 Abre un cuadro de diálogo para cambiar la configuración de fuente.  
  
 **Usar la configuración regional para mostrar valores de fecha y hora**  
 Muestra los valores de fecha y hora en la configuración regional establecida en el equipo. Si no selecciona esta opción, los valores de fecha y hora se muestran en el formato fijo que utiliza Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], que incluye milisegundos.  
  
> [!NOTE]  
>  Si activa o desactiva esta casilla se cambia el formato de presentación de las columnas de hora como **Hora de inicio** y **Hora de finalización**. Pero no cambia los parámetros del valor **DateTime** dentro de los eventos de lenguaje o las llamadas a procedimientos remotos (RPC).  
  
 **Mostrar valores en la columna Duración en microsegundos**  
 Muestra los valores en microsegundos en la columna de datos **Duración** de los seguimientos. De manera predeterminada, la columna **Duración** muestra los valores en milisegundos.  
  
### <a name="tracing-options"></a>Opciones de traza  
 **Iniciar la traza inmediatamente tras realizar la conexión**  
 Inicia un seguimiento con la plantilla predeterminada en cuanto se establece una conexión.  
  
 **Actualizar definición de seguimiento cuando cambie la versión del proveedor**  
 Aplica la definición de seguimiento más actual a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuando se actualiza el proveedor. Esta opción no está activada de manera predeterminada. Esto obliga a que el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] consulte al servidor la definición de seguimiento y vuelva a crear, si existe, el archivo en el disco.  
  
### <a name="file-rollover-options"></a>Opciones de sustitución incremental de archivos  
 **Cargar todos los archivos de sustitución incremental en secuencia sin preguntar**  
 Carga automáticamente los archivos de sustitución incremental cuando se abre un archivo de seguimiento. Si se ha creado más de un archivo durante la traza, la selección de esta opción carga automáticamente todos los archivos de sustitución incremental.  
  
 **Preguntar antes de cargar archivos de sustitución incremental**  
 Cuando se abre un archivo de seguimiento, el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] pregunta antes de agregar un archivo de sustitución incremental.  
  
 **No cargar nunca los archivos siguientes de sustitución incremental**  
 Cuando se abre un archivo de seguimiento, el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] no carga archivos de sustitución incremental.  
  
### <a name="replay-options"></a>Opciones de reproducción  
 **Número predeterminado de subprocesos de reproducción**  
 Especifique el número de subprocesos de reproducción que se utilizarán simultáneamente. Un número más alto consume más recursos durante la reproducción, pero aumenta la simultaneidad.  
  
 **Intervalo de espera del monitor de estado predeterminado (seg.)**  
 Especifique el intervalo de espera de la reproducción en segundos. El valor predeterminado es 3600 segundos (1 hora). Esta configuración afecta al tiempo que puede ejecutarse un subproceso antes de que lo finalice el monitor de estado.  
  
 **Intervalo de sondeo del monitor de estado predeterminado (seg.)**  
 Especifique el intervalo de sondeo del monitor de estado durante la reproducción en segundos. El valor predeterminado es 60 segundos. Este valor permite al usuario configurar la frecuencia con que el monitor de estado sondea los candidatos para terminar.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar un seguimiento automáticamente después de conectarse a un servidor &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [Establecer valores predeterminados de presentación de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [Reproducir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproducir un archivo de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Reproducir seguimientos](../tools/sql-server-profiler/replay-traces.md)   
 [Establecer opciones globales de seguimiento &#40;SQL Server Profiler&#41;](../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)   
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
