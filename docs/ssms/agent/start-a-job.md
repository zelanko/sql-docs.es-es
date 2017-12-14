---
title: Iniciar un trabajo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4839795e85958d9751eeeff146e90edb1ed540f4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="start-a-job"></a>Start a Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo iniciar la ejecución de un trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] u Objetos de administración de SQL Server.  
  
Un trabajo es una serie especificada de acciones que realiza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se pueden ejecutar en un servidor local o en varios servidores remotos.  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para iniciar un trabajo,utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-start-a-job"></a>Para iniciar un trabajo  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Expanda **Agente SQL Server** y **Trabajos**. En función de cómo desea que se inicie el trabajo, realice uno de los siguientes procedimientos:  
  
    -   Si está trabajando en un solo servidor o en un servidor de destino, o está ejecutando un trabajo de servidor local en un servidor maestro, haga clic con el botón derecho en el trabajo que quiere iniciar y, después, haga clic en **Iniciar trabajo**.  
  
    -   Si desea iniciar varios trabajos, haga clic con el botón derecho en **Monitor de actividad de trabajo**y, a continuación, haga clic en **Ver actividad de trabajo**. En el Monitor de actividad de trabajo puede seleccionar varios trabajos, hacer clic con el botón derecho en su selección y hacer clic en **Iniciar trabajos**.  
  
    -   Si está trabajando en un servidor maestro y quiere que todos los servidores de destino ejecuten el trabajo simultáneamente, haga clic con el botón derecho en el trabajo que quiere iniciar, haga clic en **Iniciar trabajo**y, después, haga clic en **Iniciar en todos los servidores de destino**.  
  
    -   Si está trabajando en un servidor maestro y quiere especificar los servidores de destino para el trabajo, haga clic con el botón derecho en el trabajo que quiere iniciar, haga clic en **Iniciar trabajo**y, después, haga clic en **Iniciar en servidores de destino específicos**. En el cuadro de diálogo **Exponer instrucciones de descarga** , active la casilla **Estos servidores de destino** y, a continuación, seleccione cada servidor de destino en el que debe ejecutarse este trabajo.  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-start-a-job"></a>Para iniciar un trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
Para más información, consulte [sp_start_job (Transact-SQL)](http://msdn.microsoft.com/en-us/8a91df6a-eb84-4512-9a17-4a6e32a9538a).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para iniciar un trabajo**  
  
Llame al método **Start** de la clase **Job** mediante el lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell. Para más información, consulte [Objetos de administración de SQL Server (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
