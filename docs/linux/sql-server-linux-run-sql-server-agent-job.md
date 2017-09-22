---
title: Crear y ejecutar trabajos de SQL Server en Linux | Documentos de Microsoft
description: "Este tutorial muestra cómo ejecutar trabajo del Agente SQL Server en Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 8d05ec1ae3be89b7a087938c44b356ccc9dbca43
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Crear y ejecutar trabajos del Agente SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Trabajos de SQL Server se utilizan para realizar periódicamente la misma secuencia de comandos en la base de datos de SQL Server. En este tema se proporciona ejemplos de cómo crear trabajos del Agente SQL Server en Linux con Transact-SQL y SQL Server Management Studio (SSMS).

Problemas conocidos relacionados con el Agente SQL Server en esta versión, consulte el [notas de la versión](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Requisitos previos 
Para crear y ejecutar trabajos, primero debe instalar el servicio Agente SQL Server. Para obtener instrucciones de instalación, consulte el [tema de instalación del Agente SQL Server](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-job-with-transact-sql"></a>Crear un trabajo con Transact-SQL

Los pasos siguientes proporcionan un ejemplo de cómo crear un trabajo de agente SQL Server en Linux con comandos de Transact-SQL. Estos trabajos en este ejemplo ejecuta una copia de seguridad diaria en una base de datos de ejemplo `SampleDB`. 


> [!TIP]
> Puede utilizar a cualquier cliente de T-SQL para ejecutar estos comandos. Por ejemplo, en Linux puede usar [sqlcmd](sql-server-linux-setup-tools.md) o [código de Visual Studio](sql-server-linux-develop-use-vscode.md). Desde un servidor remoto de Windows, también puede ejecutar consultas en SQL Server Management Studio (SSMS) o usar la interfaz del usuario para la administración del trabajo, que se describe en la sección siguiente.

1. **Crear el trabajo**. En el ejemplo siguiente se utiliza [sp_add_job](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-job-transact-sql) para crear un trabajo denominado `Daily AdventureWorks Backup`.

    ```tsql
     -- Adds a new job executed by the SQLServerAgent service 
     -- called 'Daily SampleDB Backup'  
     CREATE DATABASE SampleDB
     USE msdb ;  
     GO  
     EXEC dbo.sp_add_job  
         @job_name = N'Daily SampleDB Backup' ;  
     GO

    ```

2. **Agregar uno o varios pasos de trabajo**. El siguiente script de Transact-SQL usa [sp_add_jobstep](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) para crear un paso de trabajo que crea una copia de seguridad de la `AdventureWlorks2014` base de datos.

    ```tsql
    -- Adds a step (operation) to the job  
    EXEC sp_add_jobstep  
      @job_name = N'Daily SampleDB Backup',  
      @step_name = N'Backup database',  
      @subsystem = N'TSQL',  
      @command = N'BACKUP DATABASE SampleDB TO DISK = \
      N''/var/opt/mssql/data/SampleDB.bak'' WITH NOFORMAT, NOINIT, \
              NAME = ''SampleDB-full'', SKIP, NOREWIND, NOUNLOAD, STATS = 10',   
      @retry_attempts = 5,  
      @retry_interval = 5 ;  
    GO
    ```

3. **Crear una programación de trabajo**. Este ejemplo se utiliza [sp_add_schedule](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) para crear una programación diaria para el trabajo.

    ```tsql
    -- Creates a schedule called 'Daily'  
    EXEC dbo.sp_add_schedule  
     @schedule_name = N'Daily SampleDB',  
     @freq_type = 4,  
     @freq_interval = 1,
     @active_start_time = 233000 ;  
   USE msdb ;  
   GO
    ```

4. **Adjuntar la programación de trabajo para el trabajo**. Use [sp_attach_schedule](/sql-docs/docs/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql) para adjuntar la programación de trabajo para el trabajo.

    ```tsql
    -- Sets the 'Daily' schedule to the 'Daily AdventureWorks Backup' Job  
    EXEC sp_attach_schedule  
     @job_name = N'Daily SampleDB Backup',  
     @schedule_name = N'Daily SampleDB';  
    GO
    ```

5. **Asigne el trabajo a un servidor de destino**. Asigne el trabajo a un servidor de destino con [sp_add_jobserver](/sql-docs/docs/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql). En este ejemplo, el servidor local es el destino.

    ```tsql
    EXEC dbo.sp_add_jobserver  
     @job_name = N'Daily SampleDB Backup',  
     @server_name = N'(LOCAL)';  
    GO
    ```
6. **Iniciar el trabajo**. 

    ```tsql
    EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
    GO
    ```
## <a name="create-a-job-with-ssms"></a>Crear un trabajo con SSMS

También puede crear y administrar los trabajos de forma remota mediante SQL Server Management Studio (SSMS) en Windows.

1. **Inicie SSMS en Windows y conéctese a la instancia de SQL Server de Linux.** Para obtener más información, consulte [administrar SQL Server en Linux con SSMS](sql-server-linux-develop-use-ssms.md).

1. **Crear una nueva base de datos denominada SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

2. **Compruebe que el Agente SQL se ha instalado y configurado correctamente.** Busque el signo más situado junto a agente de SQL Server en el Explorador de objetos. Si no está instalado el Agente SQL Server, vea [instalar agente de SQL Server en Linux](sql-server-linux-setup-sql-agent.md).

    ![Compruebe que se instaló el Agente SQL Server](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)


3. **Crear un nuevo trabajo.**

    ![Crear un nuevo trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)


4. **Asigne un nombre a su trabajo y crear el paso de trabajo.**

    ![Crear un paso de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)


5. **Especifique qué subsistema es el que desea usar y qué debe hacer el paso de trabajo.**

    ![Subsistema de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

    ![Acción de paso de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

6. **Crear una nueva programación de trabajo.**

    ![Programación de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)
  
    ![Programación de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

7. **Iniciar el trabajo.**

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo crear y administrar trabajos del Agente SQL Server, vea [Agente SQL Server](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent).

