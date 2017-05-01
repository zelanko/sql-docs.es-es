---
title: Borrar el registro del historial de trabajos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8ece46cd518c4b94094015e26d1c8d6587edce50
ms.lasthandoff: 04/11/2017

---
# <a name="clear-the-job-history-log"></a>Clear the Job History Log
En este tema se describe cómo eliminar el contenido del registro de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]u Objetos de administración de SQL Server.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para borrar el registro del historial de trabajos, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>Para borrar el registro del historial de trabajos  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**y, a continuación, haga clic en **Trabajos**.  
  
3.  Haga clic con el botón derecho en un trabajo y, luego, haga clic en **Ver historial**.  
  
4.  En el **Visor del archivo de registros**, seleccione el trabajo cuyo historial desee borrar y, a continuación, realice una de las siguientes acciones:  
  
    -   Haga clic en **Eliminar**y, a continuación, haga clic en **Eliminar todo el historial** en el cuadro de diálogo **Eliminar historial** . Puede eliminar todo el historial de trabajos o solamente el historial anterior a una fecha determinada. Si desea eliminar todo el historial de trabajos, haga clic en **Eliminar todo el historial**. Si solo desea eliminar los registros más antiguos del historial de trabajos, haga clic en **Eliminar el historial antes de**y, a continuación, especifique una fecha.  
  
    -   Haga clic en **Estado del trabajo** si desea borrar el registro del historial de un trabajo multiservidor. Haga clic en **Trabajo**, haga clic en el nombre de un trabajo y, a continuación, haga clic en **Ver historial de trabajos remotos**.  
  
5.  Haga clic en **Eliminar**.  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>Para borrar el registro del historial de trabajos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para borrar el registro del historial de trabajos**  
  
Use el método **PurgeJobHistory** de la clase **JobServer** mediante el lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  

