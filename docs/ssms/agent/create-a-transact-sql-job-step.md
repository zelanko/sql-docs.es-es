---
title: Crear un paso de trabajo de Transact-SQL | Microsoft Docs
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
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 30d692969db247383010a268c9dd58ee5d2bd3ea
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
En este tema se describe cómo crear un paso de trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que ejecute scripts [!INCLUDE[tsql](../../includes/tsql_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]u Objetos de administración de SQL Server.  
  
Estos scripts de pasos de trabajo pueden llamar a procedimientos almacenados y procedimientos almacenados extendidos. Un solo paso de trabajo de [!INCLUDE[tsql](../../includes/tsql_md.md)] puede contener varios procesos por lotes y comandos GO incrustados. Para obtener más información acerca de la creación de un trabajo, vea [Crear trabajos](../../ssms/agent/create-jobs.md).  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para crear un paso de trabajo de Transact-SQL, utilizando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Para crear un paso de trabajo de Transact-SQL  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**, cree un trabajo o haga clic con el botón derecho en uno existente y, después, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** y, a continuación, haga clic en **Nuevo**.  
  
4.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre para el paso de trabajo en **Nombre del paso**.  
  
5.  En la lista **Tipo** , haga clic en **Transact-SQL Script (TSQL)**.  
  
6.  En el cuadro **Comando** , escriba el nombre de los lotes de comandos [!INCLUDE[tsql](../../includes/tsql_md.md)] , o bien haga clic en **Abrir** para seleccionar un archivo [!INCLUDE[tsql](../../includes/tsql_md.md)] para utilizarlo como comando.  
  
7.  Haga clic en **Analizar** para comprobar la sintaxis.  
  
8.  El mensaje "Análisis correcto" aparece cuando la sintaxis es correcta. Si se encuentra un error, corrija la sintaxis antes de continuar.  
  
9. Haga clic en la página **Avanzadas** para establecer las opciones de los pasos de trabajo, como qué acción realizar si el paso de trabajo funciona o no correctamente, cuántas veces el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe intentar ejecutar el paso de trabajo y el archivo o la tabla en la que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] puede escribir la salida de paso de trabajo. Solo los miembros del rol fijo de servidor **sysadmin** pueden escribir la salida de paso de trabajo en un archivo del sistema operativo. Todos los usuarios del Agente SQL Server pueden registrar la salida en una tabla.  
  
10. Si es miembro del rol fijo de servidor **sysadmin** y desea ejecutar este paso de trabajo con otro inicio de sesión de SQL, seleccione el inicio de sesión de SQL en la lista **Ejecutar como usuario** .  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>Para crear un paso de trabajo de Transact-SQL  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- creates a job step that that uses Transact-SQL  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Para más información, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para crear un paso de trabajo de Transact-SQL**  
  
Use la clase **JobStep** mediante un lenguaje de programación de su elección, como Visual Basic, Visual C# o PowerShell.  
  

