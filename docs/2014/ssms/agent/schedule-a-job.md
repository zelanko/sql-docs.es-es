---
title: Programar un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
ms.assetid: f626390a-a3df-4970-b7a7-a0529e4a109c
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: feb21e74909aa89d3a43e392a434d22b7c07d9d3
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814811"
---
# <a name="schedule-a-job"></a>Schedule a Job
  En este tema se describe cómo programar un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Antes de empezar:** ,  
  
     [Seguridad](#Security)  
  
-   **Para programar un trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-and-attach-a-schedule-to-a-job"></a>Para crear y asociar una programación a un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desee programar y haga clic en **Propiedades**.  
  
3.  Seleccione la página **Programaciones** y, a continuación, haga clic en **Nueva**.  
  
4.  En el cuadro **Nombre** , escriba el nombre de la nueva programación.  
  
5.  Desactive la casilla **Habilitado** si no desea que la programación tenga efecto inmediatamente después de su creación.  
  
6.  En **Tipo de programación**, seleccione una de las siguientes operaciones:  
  
    -   Haga clic en **Iniciar automáticamente al iniciar el Agente SQL Server** para iniciar el trabajo cuando se inicie el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Haga clic en **Iniciar al quedar inactivas las CPU** para iniciar el trabajo cuando las CPU alcancen la condición de inactivas.  
  
    -   Haga clic en **Periódica** si desea que una programación se ejecute varias veces. Para establecer la programación periódica, rellene los grupos **Frecuencia**, **Frecuencia diaria**y **Duración** en el cuadro de diálogo.  
  
    -   Haga clic en **Una vez** si desea que la programación se ejecute solo una vez. Para establecer la programación en **Una vez** , rellene el grupo **Repetición una vez** del cuadro de diálogo.  
  
#### <a name="to-attach-a-schedule-to-a-job"></a>Para asociar una programación a un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server**y **Trabajos**, haga clic con el botón derecho en el trabajo que desee programar, y haga clic en **Propiedades**.  
  
3.  Seleccione la página **Programaciones** y, a continuación, haga clic en **Elegir**.  
  
4.  Seleccione la programación que desee asociar y, a continuación, haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **Propiedades del trabajo** , haga doble clic en la programación asociada.  
  
6.  Compruebe que **Fecha de inicio** se ha establecido correctamente. Si no es así, establezca la fecha en el valor que desee para que la programación se inicie y, a continuación, hace clic en **Aceptar**.  
  
7.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en **Aceptar**.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-schedule-a-job"></a>Para programar un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- creates a schedule named NightlyJobs.   
    -- Jobs that use this schedule execute every day when the time on the server is 01:00.   
    EXEC sp_add_schedule  
        @schedule_name = N'NightlyJobs' ,  
        @freq_type = 4,  
        @freq_interval = 1,  
        @active_start_time = 010000 ;  
    GO  
    -- attaches the schedule to the job BackupDatabase  
    EXEC sp_attach_schedule  
       @job_name = N'BackupDatabase',  
       @schedule_name = N'NightlyJobs' ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_add_schedule &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql) y [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql).  
  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 Use la `JobSchedule` clase mediante el uso de un lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para más información, consulte[Objetos de administración de SQL Server (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
  
