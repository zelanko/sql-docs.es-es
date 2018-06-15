---
title: Crear y ejecutar trabajos de SQL Server en Linux | Documentos de Microsoft
description: Este tutorial muestra cómo ejecutar trabajo del Agente SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1d93d95e-9c89-4274-9b3f-fa2608ec2792
ms.openlocfilehash: 162015772bb54023816fcc7d911ca34fbd4a3ac7
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455118"
---
# <a name="create-and-run-sql-server-agent-jobs-on-linux"></a>Crear y ejecutar trabajos del Agente SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Trabajos de SQL Server se utilizan para realizar periódicamente la misma secuencia de comandos en la base de datos de SQL Server. Este tutorial proporciona un ejemplo de cómo crear un trabajo de agente SQL Server en Linux con Transact-SQL y SQL Server Management Studio (SSMS).

> [!div class="checklist"]
> * Instalar el Agente SQL Server en Linux
> * Crear un nuevo trabajo para realizar copias de seguridad diarias de base de datos
> * Programar y ejecutar el trabajo
> * Siga los mismos pasos en SSMS (opcional)

Problemas conocidos relacionados con el Agente SQL Server en Linux, consulte la [notas de la versión](sql-server-linux-release-notes.md).

## <a name="prerequisites"></a>Requisitos previos

Los siguientes requisitos previos son necesarios para completar este tutorial:

* Máquina Linux con los siguientes requisitos previos:
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), o [Ubuntu](quickstart-install-connect-ubuntu.md)) con las herramientas de línea de comandos.

Los requisitos previos siguientes son opcionales:

* Máquina de Windows con SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para pasos opcionales de SSMS.

## <a name="enable-sql-server-agent"></a>Habilitar el Agente SQL Server

Para utilizar el Agente SQL Server en Linux, primero debe habilitar al Agente SQL Server en un equipo que ya tenga SQL Server 2017 instalado.

1. Para habilitar el Agente SQL Server, siga el siguiente paso.
  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  ```

1. Reinicie SQL Server con el siguiente comando:
  ```bash
  sudo systemctl restart mssql-server
  ```

> [!NOTE]
> A partir de SQL Server de 2017 CU4, el Agente SQL Server se incluye con la **mssql server** empaquetar y está deshabilitada de forma predeterminada. Para el agente configurado antes de la visita de CU4, [instalar agente de SQL Server en Linux](sql-server-linux-setup-sql-agent.md).

## <a name="create-a-sample-database"></a>Crear una base de datos de ejemplo

Siga estos pasos para crear una base de datos de ejemplo denominada **SampleDB**. Esta base de datos se usa para el trabajo de copia de seguridad diario.

1. En el equipo Linux, abra una sesión de terminal de bash.

1. Use **sqlcmd** para ejecutar un Transact-SQL **CREATE DATABASE** comando.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'CREATE DATABASE SampleDB'
   ```

1. Compruebe que la base de datos se crea con una lista de las bases de datos en el servidor.

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -Q 'SELECT Name FROM sys.Databases'
   ```

## <a name="create-a-job-with-transact-sql"></a>Crear un trabajo con Transact-SQL

Los pasos siguientes para crear un trabajo de agente SQL Server en Linux con comandos de Transact-SQL. Una copia de seguridad diaria de la base de datos de ejemplo, ejecuta el trabajo **SampleDB**.

> [!TIP]
> Puede utilizar a cualquier cliente de T-SQL para ejecutar estos comandos. Por ejemplo, en Linux puede usar [sqlcmd](sql-server-linux-setup-tools.md) o [código de Visual Studio](sql-server-linux-develop-use-vscode.md). Desde un servidor remoto de Windows, también puede ejecutar consultas en SQL Server Management Studio (SSMS) o usar la interfaz del usuario para la administración del trabajo, que se describe en la sección siguiente.

1. Use [sp_add_job](../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md) para crear un trabajo denominado `Daily SampleDB Backup`.

   ```sql
   -- Adds a new job executed by the SQLServerAgent service
   -- called 'Daily SampleDB Backup'
   USE msdb ;
   GO
   EXEC dbo.sp_add_job
      @job_name = N'Daily SampleDB Backup' ;
   GO
   ```

1. Llame a [sp_add_jobstep](../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) para crear un paso de trabajo que crea una copia de seguridad de la `SampleDB` base de datos.

   ```sql
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

1. A continuación, cree una programación diaria para el trabajo con [sp_add_schedule](../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md).

   ```sql
   -- Creates a schedule called 'Daily'
   EXEC dbo.sp_add_schedule
      @schedule_name = N'Daily SampleDB',
      @freq_type = 4,
      @freq_interval = 1,
      @active_start_time = 233000 ;
   USE msdb ;
   GO
   ```

1. Adjuntar la programación de trabajo para el trabajo con [sp_attach_schedule](../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md).

   ```sql
   -- Sets the 'Daily' schedule to the 'Daily SampleDB Backup' Job
   EXEC sp_attach_schedule
      @job_name = N'Daily SampleDB Backup',
      @schedule_name = N'Daily SampleDB';
   GO
   ```

1. Use [sp_add_jobserver](../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) para asignar el trabajo a un servidor de destino. En este ejemplo, el destino es el servidor local.

   ```sql
   EXEC dbo.sp_add_jobserver
      @job_name = N'Daily SampleDB Backup',
      @server_name = N'(LOCAL)';
   GO
   ```
1. Iniciar el trabajo con [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).

   ```sql
   EXEC dbo.sp_start_job N' Daily SampleDB Backup' ;
   GO
   ```

## <a name="create-a-job-with-ssms"></a>Crear un trabajo con SSMS

También puede crear y administrar los trabajos de forma remota mediante SQL Server Management Studio (SSMS) en Windows.

1. Inicie SSMS en Windows y conéctese a la instancia de SQL Server de Linux. Para obtener más información, consulte [administrar SQL Server en Linux con SSMS](sql-server-linux-manage-ssms.md).

1. Compruebe que ha creado una base de datos de ejemplo denominada **SampleDB**.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-0.png" alt="Create a SampleDB database" style="width: 550px;"/>

1. Compruebe que el Agente SQL se [instalado](sql-server-linux-setup-sql-agent.md) y configurado correctamente. Busque el signo más situado junto a agente de SQL Server en el Explorador de objetos. Si el Agente SQL Server no está habilitado, pruebe a reiniciar el **mssql server** servicio en Linux.

   ![Compruebe que se instaló el Agente SQL Server](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-1.png)

1. Crear un nuevo trabajo.

   ![Crear un nuevo trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-2.png)

1. Asigne un nombre a su trabajo y crear el paso de trabajo.

   ![Crear un paso de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-3.png)

1. Especifique qué subsistema es el que desea usar y qué debe hacer el paso de trabajo.

   ![Subsistema de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-4.png)

   ![Acción de paso de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-5.png)

1. Crear una nueva programación de trabajo.

   ![Programación de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-6.png)

   ![Programación de trabajo](./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-8.png)

1. Iniciar el trabajo.

   <img src="./media/sql-server-linux-run-sql-server-agent-job/ssms-agent-9.png" alt="Start the SQL Server Agent job" style="width: 550px;"/>

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Instalar el Agente SQL Server en Linux
> * Uso de Transact-SQL y sistema de los procedimientos almacenan para crear trabajos
> * Crear un trabajo que realiza copias de seguridad diarias de base de datos
> * Usar SSMS UI para crear y administrar trabajos

A continuación, explore otras funciones para crear y administrar trabajos:

> [!div class="nextstepaction"]
>[Documentación del Agente SQL Server](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)
