---
title: Ejecutar el Analizador SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 7/7/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6bcf4356a7531fc681cbcf3559cab79e01e4ad2b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="run-sql-server-profiler"></a>Ejecutar SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Puede ejecutar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de varias maneras diferentes admitir la recopilación de seguimiento de salida en una variedad de escenarios. Puede iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de Windows 10 **iniciar** menú, desde el **herramientas** menú [!INCLUDE[ssDE](../../includes/ssde-md.md)] Asistente para la optimización y desde varias ubicaciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
Al iniciar por primera vez [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y seleccione **nuevo seguimiento** desde el **archivo** menú, la aplicación muestra un **conectar al servidor** cuadro de diálogo donde puede especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia para conectarse a.  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Para iniciar a SQL Server Profiler desde el menú Inicio de Windows 10  
-  Haga clic en las ventanas de **iniciar** icono o presione teclas de Windows y empiece a escribir "SQL Server Profiler 17". Cuando el **SQL Server Profiler 17** aparece el icono, haga clic en él.   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>Para iniciar SQL Server Profiler en el Asistente para la optimización de motor de base de datos  
-  En el menú [!INCLUDE[ssDE](../../includes/ssde-md.md)] Herramientas **del Asistente para la optimización de** , haga clic en **SQL Server Profiler**.  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>Para iniciar a SQL Server Profiler en SQL Server Management Studio  
 Puede iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] desde varias ubicaciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Cuando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] se inicia, carga el contexto de conexión, la plantilla de seguimiento y el contexto de filtro de su punto de inicio. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]inicia cada sesión de SQL Server Profiler en su propia instancia y el generador de perfiles continuará ejecutándose si apaga [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>Para iniciar SQL Server Profiler desde el menú Herramientas  
-  En el menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Herramientas** , haga clic en **SQL Server Profiler**.  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>Para iniciar SQL Server Profiler desde el Editor de consultas  
- En el Editor de consultas, haga clic con el botón derecho y seleccione **Realizar seguimiento de la consulta en SQL Server Profiler**.  

  > [!NOTE]  
  >  El contexto de conexión es la conexión del editor, la plantilla de seguimiento es TSQL_SPs y el filtro aplicado es SPID = ventana de consulta SPID.  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>Para iniciar SQL Server Profiler desde el Monitor de actividad  
- En el Monitor de actividad, haga clic en el **procesos** panel, haga clic en el proceso que desea generar perfiles y, a continuación, haga clic en **proceso de seguimiento de SQL Server Profiler**.  

    > [!NOTE]  
    >  Cuando se selecciona un proceso, el contexto de conexión es la conexión del Explorador de objetos cuando se abrió el Monitor de actividad. La plantilla de seguimiento es el valor predeterminado según el tipo de servidor y el SPID es igual al SPID del proceso seleccionado.  
    
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
- En el modo de autenticación de Windows, la cuenta de usuario que ejecuta [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe tener permiso para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
- Para realizar seguimientos con el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], los usuarios también deben disponer del permiso ALTER TRACE.  

## <a name="next-steps"></a>Pasos siguientes  
 [Información general de SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Usar SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
