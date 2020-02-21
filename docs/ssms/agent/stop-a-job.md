---
title: Stop a Job
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 26fbc4c13cca5a84c92130fd7541e7d3e63d3ae9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75257908"
---
# <a name="stop-a-job"></a>Stop a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo detener un trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un trabajo es una serie especificada de acciones que realiza el Agente SQL Server.  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para detener un trabajo, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   Si un trabajo está ejecutando un paso de tipo **CmdExec** o **PowerShell**, se forzará la finalización prematura del proceso en ejecución (por ejemplo, MyProgram.exe). Esto puede provocar un comportamiento imprevisible como, por ejemplo, que se mantengan abiertos los archivos utilizados por el proceso.  
  
-   Si se trata de un trabajo multiservidor, se expone una instrucción STOP para el trabajo en todos los servidores de destino correspondientes.  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>Para detener un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que desea detener y haga clic en **Detener trabajo**.  
  
3.  Si desea detener varios trabajos, haga clic con el botón derecho en **Monitor de actividad de trabajo**y, a continuación, haga clic en **Ver actividad de trabajo**. En Monitor de actividad de trabajo, seleccione los trabajos que desee detener, haga clic con el botón derecho en la selección y, a continuación, haga clic en **Detener trabajos**.  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-stop-a-job"></a>Para detener un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
Para más información, consulte [sp_stop_job (Transact-SQL)](https://msdn.microsoft.com/64b4cc75-99a0-421e-b418-94e37595bbb0).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para detener un trabajo**  
  
Llame al método **Stop** de la clase **Job** mediante el lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
