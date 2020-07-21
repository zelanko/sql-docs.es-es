---
title: Trabajos del Agente SQL Server para paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c834dcc5302244d4127aaf75ed9e16a53f3342aa
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423732"
---
# <a name="sql-server-agent-jobs-for-packages"></a>Trabajos del Agente SQL Server para paquetes
  Puede automatizar y programar la ejecución de paquetes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede programar paquetes que se implementan en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y se almacena en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el almacén de paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] y el sistema de archivos.  
  
## <a name="sections-in-this-topic"></a>Secciones de este tema  
 Este tema contiene las siguientes secciones:  
  
-   [Programar trabajos en el Agente SQL Server](#jobs)  
  
-   [Programar paquetes de Integration Services](#packages)  
  
-   [Solucionar problemas de los paquetes programados](#trouble)  
  
##  <a name="scheduling-jobs-in-sql-server-agent"></a><a name="jobs"></a>Programación de trabajos en Agente SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un servicio instalado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite automatizar y programar tareas ejecutando trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutarse antes de que los trabajos pueden ejecutarse automáticamente. Para obtener más información, consulte [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md).  
  
 El nodo **Agente SQL Server** aparece en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al establecer conexión con una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Para automatizar una tarea periódica, se crea un trabajo a través del cuadro de diálogo **Nuevo trabajo** . Para más información, vea [Implementar trabajos](../../ssms/agent/implement-jobs.md).  
  
 Después de crear el trabajo, debe agregar al menos un paso. Un trabajo puede incluir varios pasos, y cada paso puede realizar una tarea distinta. Para más información, consulte [Manage Job Steps](../../ssms/agent/manage-job-steps.md).  
  
 Después de crear el trabajo y los pasos del trabajo, puede crear una programación para ejecutar el trabajo. No obstante, también puede crear un trabajo sin programar que se ejecute manualmente. Para obtener más información, vea [Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 Puede mejorar el trabajo estableciendo opciones de notificación; por ejemplo, especificando un operador que envíe un mensaje de correo electrónico cuando finalice el trabajo o agregando alertas. Para más información, consulte [Alertas](../../ssms/agent/alerts.md).  
  
##  <a name="scheduling-integration-services-packages"></a><a name="packages"></a> Scheduling Integration Services Packages  
 Después de crear un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , debe agregar al menos un paso y definir el tipo de paso en **Paquete SQL Server Integration Services**. Un trabajo puede incluir varios pasos, y cada paso puede ejecutar un paquete diferente.  
  
 Ejecutar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desde un paso de trabajo es como ejecutar un paquete con las utilidades **dtexec** (dtexec.exe) y **DTExecUI** (dtexecui.exe). En lugar de establecer las opciones de tiempo de ejecución de un paquete con opciones de la línea de comandos o con el cuadro de diálogo **Utilidad de ejecución de paquetes** , establezca las opciones de tiempo de ejecución en el cuadro de diálogo **Nuevo paso de trabajo** . Para obtener más información acerca de las opciones para ejecutar un paquete, vea [dtexec Utility](dtexec-utility.md).  
  
 Para más información, vea [Programar un paquete mediante el Agente SQL Server](../schedule-a-package-by-using-sql-server-agent.md).  
  
 Para ver un vídeo donde se muestra cómo usar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar un paquete, visite la página principal del vídeo [Cómo automatizar la ejecución de paquetes SSIS usando el Agente SQL Server (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkId=141771)en MSDN Library.  
  
##  <a name="troubleshooting"></a><a name="trouble"></a> Solución de problemas  
 Es posible que un paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueda iniciar un paquete aunque el paquete se ejecute correctamente en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y desde la línea de comandos. Hay algunos motivos frecuentes para este problema y varias soluciones recomendadas. Para obtener más información, vea los recursos siguientes.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base, [Un paquete SSIS no se ejecuta al llamarlo desde un paso de trabajo del Agente SQL Server](https://support.microsoft.com/kb/918760)  
  
-   Vídeo, [solución de problemas: ejecución de paquetes mediante agente SQL Server (SQL Server vídeo)](https://go.microsoft.com/fwlink/?LinkId=141772), en MSDN Library.  
  
 Una vez que un paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia un paquete, se puede producir un error en la ejecución del paquete o el paquete se puede ejecutar correctamente pero con resultados inesperados. Puede usar las herramientas siguientes para solucionar estos problemas.  
  
-   Para los paquetes almacenados en la base de datos MSDB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el almacén de paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o una carpeta del equipo local, puede usar el **Visor del archivo de registros** , así como los registros y los archivos de volcado de depuración generados durante la ejecución del paquete.  
  
     **Para usar el Visor del archivo de registros, haga lo siguiente.**  
  
    1.  Haga clic con el botón derecho en el trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Explorador de objetos y, después, haga clic en **Ver historial**.  
  
    2.  Busque la ejecución del trabajo en el cuadro **Resumen de archivos del registro** que tengan el mensaje **error del trabajo** en la columna **Mensaje** .  
  
    3.  Expanda el nodo de trabajo y haga clic en el paso de trabajo para ver los detalles del mensaje en el área situada debajo del cuadro **Resumen de archivos del registro** .  
  
-   Para los paquetes almacenados en la base de datos de SSISDB, puede usar el **Visor del archivo de registros** , así como los registros y los archivos de volcado de depuración generados durante la ejecución del paquete. También puede usar los informes del servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     **Para buscar información en los informes sobre la ejecución del paquete asociada a la ejecución de un trabajo, haga lo siguiente.**  
  
    1.  Siga los pasos anteriores para ver los detalles del mensaje para el paso de trabajo.  
  
    2.  Busque el identificador de ejecución que aparece en el mensaje.  
  
    3.  Expanda el nodo Catálogos de Integration Services del Explorador de objetos.  
  
    4.  Haga clic con el botón secundario en SSISDB, apunte a Informes y a Informes estándar, y haga clic en Todas las ejecuciones.  
  
    5.  En el informe **Todas las ejecuciones** , busque el identificador de ejecución en la columna **Id.** Haga clic en **Información general**, en **Todos los mensajes**o en **Rendimiento de la ejecución** para ver información sobre la ejecución de este paquete.  
  
         Para obtener más información acerca de los informes Información general, Todos los mensajes y Rendimiento de la ejecución, vea [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md).  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artículo de Knowledge Base, [Un paquete SSIS no se ejecuta al llamarlo desde un paso de trabajo del Agente SQL Server](https://support.microsoft.com/kb/918760), en el sitio web de [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Vídeo [Solucionar problemas de ejecución de paquetes SSIS usando el Agente SQL Server (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkId=141772)en MSDN Library  
  
-   Vídeo [Cómo automatizar la ejecución de paquetes SSIS usando el Agente SQL Server (vídeo de SQL Server)](https://go.microsoft.com/fwlink/?LinkId=141771)en MSDN Library  
  
-   Artículo técnico relativo a la [comprobación de trabajos del Agente SQL Server mediante Windows PowerShell](https://go.microsoft.com/fwlink/?LinkId=165675), en mssqltips.com  
  
-   Artículo técnico relativo a la [alerta automática de los trabajos del Agente SQL cuando están habilitados o deshabilitados](https://go.microsoft.com/fwlink/?LinkId=165676), en mssqltips.com  
  
-   Entrada de blog, [Configuring SQL Agent Jobs to Write to Windows Event Log](https://go.microsoft.com/fwlink/?LinkId=220745), en mssqltips.com.  
  
  
