---
title: Correlacionar un seguimiento con los datos del registro de rendimiento de Windows (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], logs
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2d1b66cbbed716a4ce7b2d5cf9611e161141f162
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934586"
---
# <a name="correlate-a-trace-with-windows-performance-log-data-sql-server-profiler"></a>Establecer correlaciones de un seguimiento con datos del registro de rendimiento de Windows (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]puede poner en correlación los contadores del monitor de sistema de Microsoft Windows con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] eventos o. El Monitor del sistema de Windows registra la actividad del sistema para contadores específicos en registros de rendimiento.  
  
> [!NOTE]  
>  Para obtener más información acerca de compartir registros entre diferentes versiones de Windows, vea el procedimiento al final de este tema.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>Para establecer correlaciones de un seguimiento con datos del registro de rendimiento  
  
1.  En [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], abra un archivo de seguimiento o una tabla de seguimiento guardados. No puede establecer correlaciones de un seguimiento en ejecución que aún está recopilando datos de eventos. Para lograr una correlación precisa con los datos del Monitor de sistema, el seguimiento debe contener las columnas de datos **StartTime** y **EndTime** .  
  
2.  En el menú  **Archivo** de [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], haga clic en **Importar datos de rendimiento**.  
  
3.  En el cuadro de diálogo **Abrir** , seleccione un archivo que contenga un registro de rendimiento. Los datos del registro de rendimiento deben haber sido capturados durante el mismo período de tiempo en que se capturaron los datos de seguimiento.  
  
4.  En el cuadro de diálogo **Límite de contadores de rendimiento** , active las casillas que corresponden a los objetos y contadores del Monitor del sistema que desea mostrar junto con el seguimiento. Haga clic en **Aceptar**.  
  
5.  Seleccione un evento en la ventana de eventos de seguimiento o navegue por varias filas adyacentes en la ventana de eventos de seguimiento utilizando las teclas de flecha. La barra vertical roja de la ventana **Datos del Monitor de sistema** indica los datos del registro de rendimiento correlacionados con el evento de seguimiento seleccionado.  
  
6.  Haga clic en un punto de interés en el gráfico Monitor del sistema. Se selecciona la fila correspondiente del seguimiento más cercana en el tiempo. Para ver más de cerca un intervalo de tiempo, presione el mouse (ratón) y arrastre el puntero en el gráfico Monitor del sistema.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>Para crear registros de rendimiento que puedan compartirse entre diferentes versiones de Windows  
  
1.  En el Panel de control, abra **Herramientas administrativas**y haga doble clic en **Rendimiento**.  
  
2.  En el cuadro de diálogo **Rendimiento** , expanda **Registros y alertas de rendimiento**, haga clic con el botón derecho en **Registros de contador**y, después, haga clic en **Nueva configuración de registro**.  
  
3.  Escriba un nombre para el registro de contador y, a continuación, haga clic en **Aceptar**.  
  
4.  En la pestaña **General** , haga clic en **Agregar contadores**.  
  
5.  En la lista **Objeto de rendimiento** , seleccione un objeto de rendimiento que desee supervisar. Los nombres de los objetos de rendimiento de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para instancias predeterminadas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] comienzan con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las instancias con nombre comienzan con MSSQL$*instanceName*.  
  
6.  Agregue tantos contadores como sean necesarios para la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y otros valores importantes, como el tiempo de procesador y el tiempo de disco.  
  
7.  Cuando haya terminado de agregar los contadores, haga clic en **Cerrar**.  
  
8.  Establezca los valores del intervalo **Tomar datos de muestra cada** . Comience por un intervalo de muestreo moderado, como 5 minutos, y después ajuste el intervalo si es necesario.  
  
9. En la pestaña **Archivos de registro** , elija **Archivo de texto (delimitado por comas)** en la lista **Tipo del archivo de registro** . Los archivos de registro de texto delimitado por comas se pueden compartir entre diferentes versiones de Windows y se pueden ver más tarde en herramientas de elaboración de informes como Microsoft Excel.  
  
10. En la pestaña **Programación** , especifique una programación de supervisión.  
  
11. Haga clic en **Aceptar** para crear el registro de rendimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Iniciar SQL Server Profiler](../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
