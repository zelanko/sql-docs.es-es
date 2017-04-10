---
title: "Iniciar SQL Server Profiler | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Profiler [SQL Server Profiler], iniciar"
  - "SQL Server Profiler, inicio"
  - "iniciar SQL Server Profiler"
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Iniciar SQL Server Profiler
  Puede iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de varias formas distintas para admitir la recopilación de resultados de seguimiento en diversos escenarios. Entre las diferentes formas de iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] se incluyen: desde el menú **Inicio** , desde el menú **Herramientas** en el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y desde varias ubicaciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Al iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] por primera vez y seleccionar **Nuevo seguimiento** en el menú **Archivo** , la aplicación muestra un cuadro de diálogo **Conectar al servidor** en el que se puede especificar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se desea conectar.  
  
### Para iniciar SQL Server Profiler desde el menú Inicio  
  
1.  En el menú **Inicio** , elija **Todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de rendimiento**y, a continuación, haga clic en **SQL Server Profiler**.  
  
### Para iniciar SQL Server Profiler en el Asistente para la optimización de motor de base de datos  
  
1.  En el menú [!INCLUDE[ssDE](../../includes/ssde-md.md)] Herramientas **del Asistente para la optimización de** , haga clic en **SQL Server Profiler**.  
  
## Iniciar SQL Server Profiler en Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inicia cada sesión del generador de perfiles en su propia instancia y continúa ejecutándose después de cerrar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Puede iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] desde varias ubicaciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], tal y como se muestra en los procedimientos siguientes. Cuando se inicia [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , éste carga el contexto de conexión, la plantilla de seguimiento y el contexto del filtro de su punto de inicio.  
  
#### Para iniciar SQL Server Profiler desde el menú Herramientas  
  
1.  En el menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Herramientas** , haga clic en **SQL Server Profiler**.  
  
#### Para iniciar SQL Server Profiler desde el Editor de consultas  
  
1.  En la barra de menús de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic en **Nueva consulta**.  
  
2.  En el Editor de consultas, haga clic con el botón derecho y seleccione **Realizar seguimiento de la consulta en SQL Server Profiler**.  
  
    > [!NOTE]  
    >  El contexto de conexión es la conexión del editor, la plantilla de seguimiento es TSQL_SPs y el filtro aplicado es SPID = ventana de consulta SPID.  
  
#### Para iniciar SQL Server Profiler desde el Monitor de actividad  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y haga clic en **Monitor de actividad**.  
  
2.  Haga clic en el panel **Procesos**, haga clic con el botón derecho en el proceso cuyo perfil quiera generar y haga clic en **Realizar seguimiento de proceso en SQL Server Profiler**.  
  
    > [!NOTE]  
    >  Cuando se selecciona un proceso, el contexto de conexión es la conexión del Explorador de objetos cuando se abrió el Monitor de actividad. La plantilla de seguimiento es el valor predeterminado según el tipo de servidor y el SPID es igual al SPID del proceso seleccionado.  
  
## Seguridad de .NET Framework  
 En el modo de autenticación de Windows, la cuenta de usuario que ejecuta [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe tener permiso para conectarse a una instancia de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para realizar seguimientos con el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], los usuarios también deben disponer del permiso ALTER TRACE.  
  
## Vea también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Usar SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  