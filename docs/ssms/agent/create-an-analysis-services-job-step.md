---
title: Crear un paso de trabajo de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [Analysis Services]
ms.assetid: 03d4bb86-514b-4a55-97b9-c2c0fa08b428
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a59b69bd421b1b20bb59d772e5b393915cd0c5da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759603"
---
# <a name="create-an-analysis-services-job-step"></a>Create an Analysis Services Job Step
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo crear y definir los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que ejecutan comandos y consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server.  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   **Para crear pasos de trabajo de SQL Server utilizando comandos y/o consultas de Analysis Services, con:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [objetos de administración de SQL Server](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   Si el paso de trabajo utiliza un comando de Analysis Services, la instrucción de comando debe ser un método **Execute** de XML for Analysis Services. Puede que la instrucción no contenga un sobre SOAP (Protocolo simple de acceso a objetos) completo o un método **Discover** de XML for Analysis Services. Mientras [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] admite sobres SOAP (Protocolo simple de acceso a objetos) completos y el método **Discover** , los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no los admiten. Para más información sobre XML for Analysis Services, consulte [Información general de XML for Analysis (XMLA)](http://msdn.microsoft.com/library/ms187190.aspx).  
  
-   Si el paso de trabajo utiliza una consulta de Analysis Services, la instrucción de consulta debe ser una consulta de expresiones multidimensionales (MDX). Para más información sobre MDX, consulte [Aspectos básicos de la instrucción MDX (MDX)](http://msdn.microsoft.com/a560383b-bb58-472e-95f5-65d03d8ea08b).  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
  
-   Para ejecutar un paso de trabajo que utilice el subsistema de Analysis Services, un usuario debe ser miembro del rol fijo de servidor **sysadmin** o tener acceso a una cuenta de proxy válida definida para utilizar este subsistema. Además, la cuenta de servicio o el proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben ser un administrador de Analysis Services y una cuenta de dominio de Windows válida.  
  
-   Los miembros del rol fijo de servidor **sysadmin** son los únicos que pueden escribir la salida de un paso de trabajo en un archivo. Si ejecutan el paso de trabajo usuarios miembros del rol de base de datos **SQLAgentUserRole** en la base de datos **msdb** , solo se podrá escribir la salida en una tabla. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe la salida del paso de trabajo en la tabla **sysjobstepslog** de la base de datos **msdb** .  
  
-   Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usar SQL Server Management Studio  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Para crear un paso de trabajo de comando de Analysis Services  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**, cree un trabajo o haga clic con el botón derecho en uno existente y, después, haga clic en **Propiedades**. Para más información sobre cómo crear un trabajo, consulte [Crear trabajos](../../ssms/agent/create-jobs.md).  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** y, a continuación, en **Nuevo**.  
  
4.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un **Nombre del paso**del trabajo.  
  
5.  En la lista **Tipo** , haga clic en **Comando de SQL Server Analysis Services**.  
  
6.  En la lista **Ejecutar como** , seleccione un proxy que se haya definido para utilizar el subsistema de comandos de Analysis Services. Los usuarios miembros del rol fijo de servidor **sysadmin** también pueden seleccionar **Cuenta del servicio del Agente SQL** para ejecutar este paso de trabajo.  
  
7.  Seleccione el **Servidor** en el que se ejecutará el paso de trabajo o escriba su nombre.  
  
8.  En el cuadro **Comando** , escriba la instrucción que se debe ejecutar o haga clic en **Abrir** para seleccionar una instrucción.  
  
9. Haga clic en la página **Avanzadas** para definir opciones para este paso de trabajo, como la acción que debe realizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el paso de trabajo se realiza correctamente o con errores, las veces que se debe intentar ejecutar el paso de trabajo y el lugar en el que se debe escribir la salida.  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Para crear un paso de trabajo de consulta de Analysis Services  
  
1.  En el **Explorador de objetos** , conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]y, después, expándala.  
  
2.  Expanda el **Agente SQL Server**, cree un trabajo o haga clic con el botón derecho en uno existente y, después, haga clic en **Propiedades**. Para más información sobre cómo crear un trabajo, consulte [Crear trabajos](../../ssms/agent/create-jobs.md).  
  
3.  En el cuadro de diálogo **Propiedades del trabajo** , haga clic en la página **Pasos** y, a continuación, haga clic en **Nuevo**.  
  
4.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre para el paso de trabajo en **Nombre del paso**.  
  
5.  En la lista **Tipo** , haga clic en **Consulta de SQL Server Analysis Services**.  
  
6.  En la lista **Ejecutar como** , seleccione un proxy que se haya definido para utilizar el subsistema de consultas de Analysis Services. Los usuarios miembros del rol fijo de servidor **sysadmin** también pueden seleccionar **Cuenta del servicio del Agente SQL** para ejecutar este paso de trabajo.  
  
7.  Seleccione el **Servidor** y la **Base de datos** en los que se ejecutará el paso de trabajo o escriba sus nombres.  
  
8.  En el cuadro **Comando** , escriba la instrucción que se debe ejecutar o haga clic en **Abrir** para seleccionar una instrucción.  
  
9. Haga clic en la página **Avanzadas** para definir opciones para este paso de trabajo, como la acción que debe realizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el paso de trabajo se realiza correctamente o con errores, las veces que se debe intentar ejecutar el paso de trabajo y el lugar en el que se debe escribir la salida.  
  
## <a name="TSQL"></a>Usar Transact-SQL  
  
#### <a name="to-create-an-analysis-services-command-job-step"></a>Para crear un paso de trabajo de comando de Analysis Services  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates a job step that uses XMLA to create a relational data source that
    -- references the AdventureWorks2012 Microsoft SQL Server database.  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name =
            N'Create a relational data source that references the AdventureWorks2012 Microsoft SQL Server database',  
        @subsystem = N'ANALYSISCOMMAND',  
        @command =
            N' <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
        <ParentObject>  
            <DatabaseID>AdventureWorks2012</DatabaseID>  
        </ParentObject>  
        <ObjectDefinition>  
            <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:type="RelationalDataSource">  
                <ID>AdventureWorks2012</ID>  
                <Name>Adventure Works 2012</Name>  
                <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorks2012;Integrated Security=True</ConnectionString>  
                <ImpersonationInfo>  
                    <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
                </ImpersonationInfo>  
                <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
                <Timeout>PT0S</Timeout>  
            </DataSource>  
        </ObjectDefinition>  
    </Create>', ;  
    GO  
    ```  
  
Para más información, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755).  
  
#### <a name="to-create-an-analysis-services-query-job-step"></a>Para crear un paso de trabajo de consulta de Analysis Services  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates a job step that uses MDX to return data  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Returns the Internet sales amount by state',  
        @subsystem = N'ANALYSISQUERY',  
        @command = N' SELECT  
       [Measures].[Internet Sales Amount] ON COLUMNS,  
       [Customer].[State-Province].Members ON ROWS  
    FROM [AdventureWorks2012]',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
Para más información, consulte [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755).  
  
## <a name="SMO"></a>Usar Objetos de administración de SQL Server  
**Para crear un paso de trabajo para script de PowerShell**  
  
Utilice la clase **JobStep** con un lenguaje de programación de su elección, por ejemplo, XMLA o MDX. Para más información, consulte [Objetos de administración de SQL Server (SMO)](http://msdn.microsoft.com/library/ms162169.aspx).  
  
