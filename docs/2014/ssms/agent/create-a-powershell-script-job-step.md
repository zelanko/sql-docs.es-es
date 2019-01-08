---
title: Crear un paso de trabajo para script de PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], job steps
- jobs [SQL Server Agent], PowerShell
- job steps [PowerShell]
- SQL Server Agent jobs, PowerShell steps
ms.assetid: 50afcf84-fae0-4eb5-9b0f-f2cf144c1433
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 08a27fd6edbfa93fd76ae99186e2425e5279e8aa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818148"
---
# <a name="create-a-powershell-script-job-step"></a>Crear un paso de trabajo para script de PowerShell
  En este tema se describe cómo crear y definir un paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecute un script de PowerShell en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para crear un paso de trabajo para script de PowerShell, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-powershell-script-job-step"></a>Para crear un paso de trabajo para script de PowerShell  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**, cree un trabajo o haga clic con el botón derecho en uno existente y, después, haga clic en **Propiedades**. Para obtener más información acerca de la creación de un trabajo, vea [Crear trabajos](create-jobs.md).  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** y, a continuación, haga clic en **Nuevo**.  
  
4.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre para el paso de trabajo en **Nombre del paso**.  
  
5.  En la lista **Tipo** , haga clic en **PowerShell**.  
  
6.  En la lista **Ejecutar como** , seleccione la cuenta de proxy con las credenciales que utilizará el trabajo.  
  
7.  En el cuadro **Comando** , especifique la sintaxis del script de PowerShell que se ejecutará para el paso de trabajo. También puede hacer clic en **Abrir** y seleccionar un archivo que contenga la sintaxis del script. Para un ejemplo de un script de PowerShell, consulte **Usar Transact-SQL** más adelante.  
  
8.  Haga clic en la página **Avanzadas** para establecer las siguientes opciones de paso de trabajo: acción que se llevará a cabo si el paso de trabajo progresa o no, número de veces que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe intentar ejecutar el paso de trabajo y frecuencia de los intentos.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-powershell-script-job-step"></a>Para crear un paso de trabajo para script de PowerShell  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- creates a PowerShell job step that finds the processes that use more than 1000 MB of memory and kills them  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Kills all processes that use more than 1000 MB of memory',  
        @subsystem = N'PowerShell',  
        @command = N'Get-Process | Where-Object { $_.WS -gt 1000MB } | Stop-Process',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para crear un paso de trabajo para script de PowerShell**  
  
 Utilice la clase `JobStep` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell.  
  
  
