---
title: Borrar el registro del historial de trabajos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c548cb5ac6fcb722dc1130aea5317871592f8544
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105966"
---
# <a name="clear-the-job-history-log"></a>Clear the Job History Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo eliminar el contenido del registro de historial de trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para borrar el registro del historial de trabajos, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
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
  
Use el método **PurgeJobHistory** de la clase **JobServer** mediante el lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
