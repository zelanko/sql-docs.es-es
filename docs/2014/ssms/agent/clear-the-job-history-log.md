---
title: Borrar el registro del historial de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d6d4943bf3884933cd60e1c0ef51a54771ee00af
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782766"
---
# <a name="clear-the-job-history-log"></a>Clear the Job History Log
  En este tema se describe cómo eliminar el contenido del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro de historial de trabajos [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del agente [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]en [!INCLUDE[tsql](../../includes/tsql-md.md)]mediante, o objetos de administración de SQL Server.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para borrar el registro del historial de trabajos, utilizando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [objetos de administración de SQL Server](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>Para borrar el registro del historial de trabajos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda el **Agente SQL Server**y, a continuación, haga clic en **Trabajos**.  
  
3.  Haga clic con el botón derecho en un trabajo y, luego, haga clic en **Ver historial**.  
  
4.  En el **Visor del archivo de registros**, seleccione el trabajo cuyo historial desee borrar y, a continuación, realice una de las siguientes acciones:  
  
    -   Haga clic en **Eliminar**y, a continuación, haga clic en **Eliminar todo el historial** en el cuadro de diálogo **Eliminar historial** . Puede eliminar todo el historial de trabajos o solamente el historial anterior a una fecha determinada. Si desea eliminar todo el historial de trabajos, haga clic en **Eliminar todo el historial**. Si solo desea eliminar los registros más antiguos del historial de trabajos, haga clic en **Eliminar el historial antes de**y, a continuación, especifique una fecha.  
  
    -   Haga clic en **Estado del trabajo** si desea borrar el registro del historial de un trabajo multiservidor. Haga clic en **Trabajo**, haga clic en el nombre de un trabajo y, a continuación, haga clic en **Ver historial de trabajos remotos**.  
  
5.  Haga clic en **Eliminar**.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>Para borrar el registro del historial de trabajos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para borrar el registro del historial de trabajos**  
  
 Use el método `PurgeJobHistory` de la clase `JobServer` mediante el lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
