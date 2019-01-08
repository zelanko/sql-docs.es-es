---
title: Crear un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed3c7cf100d0105d393bb8c22bbc0d38d2e9de26
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808887"
---
# <a name="create-a-job"></a>Crear un trabajo
  En este tema se describe cómo crear un trabajo del Agente SQL Server en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server (SMO).  
  
 Para agregar pasos de trabajo, programas, alertas y notificaciones que puedan enviarse a los operadores, vea los vínculos a los temas de la sección Vea también.  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear un trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [objetos de administración de SQL Server](#SMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Para crear un trabajo, el usuario debe ser miembro de uno de los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del rol fijo de servidor **sysadmin** . Solo pueden editar el trabajo el propietario de éste o los miembros del rol **sysadmin** . Para más información sobre los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Roles fijos de base de datos del Agente SQL Server](sql-server-agent-fixed-database-roles.md).  
  
-   La asignación de un trabajo a otro inicio de sesión no garantiza que el nuevo propietario disponga de los permisos suficientes para ejecutar el trabajo.  
  
-   El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local almacena los trabajos locales en la caché. Por lo tanto, cualquier modificación obliga implícitamente al Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a volver a almacenar el trabajo en la caché. Puesto que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no almacena el trabajo en la caché hasta que se llama a **sp_add_jobserver** , resulta más eficaz llamar a **sp_add_jobserver** al final.  
  
###  <a name="Security"></a> Seguridad  
  
-   Para cambiar el propietario de un trabajo debe ser administrador de sistema.  
  
-   Por razones de seguridad, solo el propietario del trabajo o un miembro del rol **sysadmin** puede cambiar la definición del trabajo. Solo los miembros del rol fijo de servidor **sysadmin** pueden asignar la propiedad de un trabajo a otros usuarios y pueden ejecutar cualquier trabajo, independientemente de quién sea el propietario del mismo.  
  
    > [!NOTE]  
    >  Si cambia la propiedad de un trabajo a un usuario que no es miembro del rol fijo de servidor **sysadmin** y el trabajo está ejecutando unos pasos que necesitan las cuentas de un servidor proxy (por ejemplo, la ejecución de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] ), asegúrese de que el usuario tenga acceso a ese servidor proxy o, de lo contrario, se producirán errores en el trabajo.  
  
####  <a name="Permissions"></a> Permissions  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Para crear un trabajo del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que desea crear un trabajo del Agente SQL Server.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Trabajos** y, después, seleccione **Nuevo trabajo...**.  
  
4.  En el cuadro de diálogo **Nuevo trabajo** , en la página **General** , modifique las propiedades generales del trabajo. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo y el nuevo trabajo &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  En la página **Pasos** , organice los pasos de trabajo. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo: nuevo trabajo &#40;página pasos&#41;](job-properties-new-job-steps-page.md)  
  
6.  En la página **Programaciones** , organice las programaciones del trabajo. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo: Nuevo trabajo &#40;página de programaciones&#41;](job-properties-new-job-schedules-page.md)  
  
7.  En la página **Alertas** , organice las alertas del trabajo. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo: Nuevo trabajo &#40;página de alertas&#41;](job-properties-new-job-alerts-page.md)  
  
8.  En la página **Notificaciones** , establezca las acciones que el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe realizar cuando se complete el trabajo. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo: Nuevo trabajo &#40;página notificaciones&#41;](job-properties-new-job-notifications-page.md).  
  
9. En la página **Destinos** , administre los servidores de destino del trabajo. Para obtener más información sobre las opciones disponibles en esta página, vea [propiedades del trabajo: Nuevo trabajo &#40;tiene como destino de la página&#41;](job-properties-new-job-targets-page.md).  
  
10. Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-job"></a>Para crear un trabajo del Agente SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backup';  
    GO  
    ```  
  
 Para obtener más información, vea:  
  
-   [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
##  <a name="SMOProcedure"></a> Usar objetos de administración de SQL Server  
 **Para crear un trabajo del Agente SQL Server**  
  
 Llame al método `Create` de la clase `Job` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para el código de ejemplo, consulte [Programar tareas administrativas automáticas en el Agente SQL Server](sql-server-agent.md).  
  
##  <a name="SSMSProc2"></a>  
