---
title: Iniciar SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a3219168a070a9c264d4fb5457f9e5844734844a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775567"
---
# <a name="start-sql-server-profiler"></a>Iniciar SQL Server Profiler
  Puede iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de varias formas distintas para admitir la recopilación de resultados de seguimiento en diversos escenarios. Entre las diferentes formas de iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] se incluyen: desde el menú **Inicio** , desde el menú **Herramientas** en el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y desde varias ubicaciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Al iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] por primera vez y seleccionar **Nuevo seguimiento** en el menú **Archivo** , la aplicación muestra un cuadro de diálogo **Conectar al servidor** en el que se puede especificar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se desea conectar.  
  
### <a name="to-start-sql-server-profiler-from-the-start-menu"></a>Para iniciar SQL Server Profiler desde el menú Inicio  
  
1.  En el menú **Inicio** , elija **Todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de rendimiento**y, a continuación, haga clic en **SQL Server Profiler**.  
  
### <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>Para iniciar SQL Server Profiler en el Asistente para la optimización de motor de base de datos  
  
1.  En el menú [!INCLUDE[ssDE](../../includes/ssde-md.md)] Herramientas **del Asistente para la optimización de** , haga clic en **SQL Server Profiler**.  
  
## <a name="starting-sql-server-profiler-in-management-studio"></a>Iniciar SQL Server Profiler en Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inicia cada sesión del generador de perfiles en su propia instancia y continúa ejecutándose después de cerrar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Puede iniciar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] desde varias ubicaciones en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], tal y como se muestra en los procedimientos siguientes. Cuando se inicia [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , éste carga el contexto de conexión, la plantilla de seguimiento y el contexto del filtro de su punto de inicio.  
  
#### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>Para iniciar SQL Server Profiler desde el menú Herramientas  
  
1.  En el menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Herramientas** , haga clic en **SQL Server Profiler**.  
  
#### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>Para iniciar SQL Server Profiler desde el Editor de consultas  
  
1.  En la barra de menús de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic en **Nueva consulta**.  
  
2.  En el Editor de consultas, haga clic con el botón derecho y seleccione **Realizar seguimiento de la consulta en SQL Server Profiler**.  
  
    > [!NOTE]  
    >  El contexto de conexión es la conexión del editor, la plantilla de seguimiento es TSQL_SPs y el filtro aplicado es SPID = ventana de consulta SPID.  
  
#### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>Para iniciar SQL Server Profiler desde el Monitor de actividad  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y haga clic en **Monitor de actividad**.  
  
2.  Haga clic en el panel **Procesos** , haga clic con el botón derecho en el proceso cuyo perfil quiera generar y haga clic en **Realizar seguimiento de proceso en SQL Server Profiler**.  
  
    > [!NOTE]  
    >  Cuando se selecciona un proceso, el contexto de conexión es la conexión del Explorador de objetos cuando se abrió el Monitor de actividad. La plantilla de seguimiento es el valor predeterminado según el tipo de servidor y el SPID es igual al SPID del proceso seleccionado.  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
 En el modo de autenticación de Windows, la cuenta de usuario que ejecuta [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] debe tener permiso para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para realizar seguimientos con el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], los usuarios también deben disponer del permiso ALTER TRACE.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)   
 [Usar SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)  
  
  
