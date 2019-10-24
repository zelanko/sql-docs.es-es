---
title: Ver el historial de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- viewing job history
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
- displaying job history
ms.assetid: 3bbd1556-abdb-48a3-b249-546eace76343
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1ba38b6a3c425972ef0b893d302df78e3d835f85
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783388"
---
# <a name="view-the-job-history"></a>View the Job History
  En este tema se describe cómo ver el registro de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server.  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver el registro de historial de trabajos, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-the-job-history-log"></a>Para ver el registro de historial de trabajos  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**y, a continuación, haga clic en **Trabajos**.  
  
3.  Haga clic con el botón derecho en un trabajo y, luego, haga clic en **Ver historial**.  
  
4.  En el Visor del archivo de registros, vea el historial de trabajos.  
  
5.  Para actualizar el historial de trabajos, haga clic en **Actualizar**. Para ver menos filas, haga clic en el botón **Filtro** y escriba los parámetros de filtro.  
  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-view-the-job-history-log"></a>Para ver el registro de historial de trabajos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- lists all job information for the NightlyBackups job.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobhistory   
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 Para obtener más información, [vea &#40;SP_HELP_JOBHISTORY Transact-&#41;SQL](/sql/relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql).  
  
##  <a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para ver el registro de historial de trabajos**  
  
 Llame al método `EnumHistory` de la clase `Job` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
