---
title: Detener un trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78986e85dd8ee808f5fb621182d903a94bbc5eb7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067522"
---
# <a name="stop-a-job"></a>Stop a Job
  En este tema se describe cómo detener un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajo del agente. Un trabajo es una serie especificada de acciones que realiza el Agente SQL Server.  
  
-   **Antes de empezar:** ,  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para detener un trabajo, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si un trabajo está ejecutando un paso de tipo **CmdExec** o **PowerShell**, se forzará la finalización prematura del proceso en ejecución (por ejemplo, MyProgram.exe). Esto puede provocar un comportamiento imprevisible como, por ejemplo, que se mantengan abiertos los archivos utilizados por el proceso.  
  
-   Si se trata de un trabajo multiservidor, se expone una instrucción STOP para el trabajo en todos los servidores de destino correspondientes.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>Para detener un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desea detener y haga clic en **Detener trabajo**.  
  
3.  Si desea detener varios trabajos, haga clic con el botón derecho en **Monitor de actividad de trabajo**y, a continuación, haga clic en **Ver actividad de trabajo**. En Monitor de actividad de trabajo, seleccione los trabajos que desee detener, haga clic con el botón derecho en la selección y, a continuación, haga clic en **Detener trabajos**.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usar Transact-SQL  
  
### <a name="to-stop-a-job"></a>Para detener un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 Para obtener más información, vea [sp_stop_job &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-stop-job-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usar Objetos de administración de SQL Server  

### <a name="to-stop-a-job"></a>Para detener un trabajo
  
 Llame al método `Stop` de la clase `Job` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
