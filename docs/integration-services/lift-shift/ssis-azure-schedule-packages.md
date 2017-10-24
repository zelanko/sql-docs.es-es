---
title: "Programar la ejecución de paquetes SSIS en Azure | Documentos de Microsoft"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 2130e68d5e29671a2881d8762666cf852ff51259
ms.contentlocale: es-es
ms.lasthandoff: 10/18/2017

---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Programar la ejecución de un paquete SSIS en Azure
Puede programar la ejecución de paquetes almacenados en la base de datos de catálogo de SSISDB en un servidor de base de datos de SQL Azure eligiendo una de las opciones de programación siguientes:
-   [Agente SQL Server](#agent)
-   [Trabajos elásticos de base de datos SQL](#elastic)
-   [La actividad de Azure datos generador SQL Server Stored Procedure](#sproc)

## <a name="agent"></a>Programar un paquete con el Agente SQL Server

### <a name="prerequisite"></a>Requisito previo

Para poder usar al Agente SQL Server de forma local para programar la ejecución de paquetes almacenados en un servidor de base de datos de SQL Azure, tiene que agregar el servidor de base de datos SQL como un servidor vinculado. Para obtener más información, consulte [crear servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) y [servidores vinculados](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Crear un trabajo de agente SQL Server

Para programar un paquete con el Agente SQL Server de forma local, cree un trabajo con un paso de trabajo que llama el catálogo de SSIS procedimientos almacenados `[catalog].[create_execution]` y, a continuación, `[catalog].[start_execution]`. Para obtener más información, consulte [trabajos del Agente SQL Server para los paquetes](../packages/sql-server-agent-jobs-for-packages.md).

1.  En SQL Server Management Studio, conéctese a la base de datos de SQL Server local en el que desea crear el trabajo.

2.  Haga doble clic en el **Agente SQL Server** nodo, seleccione **New**y, a continuación, seleccione **trabajo** para abrir el **nuevo trabajo** cuadro de diálogo.

3.  En el **nuevo trabajo** cuadro de diálogo, seleccione la **pasos** página y, a continuación, seleccione **New** para abrir el **nuevo paso de trabajo** cuadro de diálogo.

4.  En el **nuevo paso de trabajo** cuadro de diálogo, seleccione `SSISDB` como el **base de datos.**

5.  En el campo comando, escriba un script de Transact-SQL similar a la secuencia de comandos que se muestra en el ejemplo siguiente:

    ```sql
    DECLARE @return_value int, @exe_id bigint 

    EXEC @return_value = [YourLinkedServer].[SSISDB].[catalog].[create_execution] 
    @folder_name=N'folderName', @project_name=N'projectName', 
    @package_name=N'packageName', @use32bitruntime=0, 
    @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT 
 
    EXEC [YourLinkedServer].[SSISDB].[catalog].[start_execution] @execution_id=@exe_id

    GO
    ```

6.  Termine de configurar y programar el trabajo.

## <a name="elastic"></a>Programar un paquete con trabajos elástico de base de datos de SQL

Para obtener más información acerca de los trabajos elásticos de base de datos de SQL, consulte [bases de datos de escala horizontal en la nube de administración](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Requisitos previos

Para poder usar trabajos elásticos para programar paquetes SSIS que se almacena en la base de datos de catálogo de SSISDB en un servidor de base de datos de SQL Azure, deberá hacer lo siguiente:

1.  Instalar y configurar los componentes de trabajos de la base de datos elástica. Para obtener más información, consulte [información general de los trabajos de instalación de base de datos elástica](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Crear credenciales de ámbito de base de datos que los trabajos pueden usar para enviar comandos a la base de datos de catálogo de SSIS. Para obtener más información, consulte [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

### <a name="create-an-elastic-job"></a>Crear un trabajo elástico

Crear el trabajo mediante un script de Transact-SQL similar a la secuencia de comandos que se muestra en el ejemplo siguiente:

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 
? 
-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 
? 
-- Add a job to schedule SSIS package execution
EXEC jobs.sp_add_job @job_name='ExecutePackageJob', @description='Description', 
    @schedule_interval_type='Minutes', @schedule_interval_count=60

-- Add a job step to create/start SSIS package execution using SSISDB catalog stored procedures
EXEC jobs.sp_add_jobstep @job_name='ExecutePackageJob', 
    @command=N'DECLARE @exe_id bigint 
        EXEC [SSISDB].[catalog].[create_execution]
            @folder_name=N''folderName'', @project_name=N''projectName'',
            @package_name=N''packageName'', @use32bitruntime=0,
            @runinscaleout=1, @useanyworker=1, 
            @execution_id=@exe_id OUTPUT         
        EXEC [SSISDB].[catalog].[start_execution] @exe_id, @retry_count=0', 
    @credential_name='YourDBScopedCredentials', 
    @target_group_name='TargetGroup' 

-- Enable the job schedule 
EXEC jobs.sp_update_job @job_name='ExecutePackageJob', @enabled=1, 
    @schedule_interval_type='Minutes', @schedule_interval_count=60 
```

## <a name="sproc"></a>Programar un paquete con la actividad de Azure datos generador SQL Server Stored Procedure

> [!IMPORTANT]
> Usar los scripts JSON en el ejemplo siguiente con la factoría de datos de Azure versión 1 actividad de procedimiento almacenado.

Para programar un paquete con la actividad de Azure datos generador SQL Server Stored Procedure, haga lo siguiente:

1.  Crear un generador de datos.

2.  Crea un servicio vinculado de la base de datos de SQL que hospeda SSISDB.

3.  Crear un conjunto de datos de salida que controla la programación.

4.  Crear una canalización de factoría de datos que utiliza la actividad de procedimiento almacenado de SQL Server para ejecutar el paquete SSIS.

Esta sección proporciona información general de estos pasos. Un tutorial completo de la factoría de datos queda fuera del ámbito de este artículo. Para obtener más información, consulte [la actividad de procedimiento almacenado de SQL Server](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-stored-proc-activity).

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>Crea un servicio vinculado de la base de datos de SQL que hospeda SSISDB
El servicio vinculado permite factoría de datos conectarse a SSISDB.

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "description": "",
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Data Source = tcp: YourSQLDBServer.database.windows.net, 1433; Initial Catalog = SSISDB; User ID = YourUsername; Password = YourPassword; Integrated Security = False; Encrypt = True; Connect Timeout = 30"
        }
    }
}
```

### <a name="create-an-output-dataset"></a>Crear un conjunto de datos de salida
El conjunto de datos de salida contiene la información de programación.

```json
{
    "name": "sprocsampleout",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
### <a name="create-a-data-factory-pipeline"></a>Crear una canalización de factoría de datos
La canalización usa la actividad de procedimiento almacenado de SQL Server para ejecutar el paquete SSIS.

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [{
            "name": "SprocActivitySample",
            "type": "SqlServerStoredProcedure",
            "typeProperties": {
                "storedProcedureName": "sp_executesql",
                "storedProcedureParameters": {
                    "stmt": "Transact-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures"
                }
            },
            "outputs": [{
                "name": "sprocsampleout"
            }],
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            }
        }],
        "start": "2017-10-01T00:00:00Z",
        "end": "2017-10-01T05:00:00Z",
        "isPaused": false
    }
}
```

No tienes que crear un nuevo procedimiento almacenado para encapsular los comandos de Transact-SQL necesarios para crear e iniciar la ejecución de paquetes SSIS. Puede proporcionar el script completo como el valor de la `stmt` parámetro en el anterior ejemplo JSON. Este es un script de ejemplo:

```sql
-- T-SQL script to create and start SSIS package execution using SSISDB catalog stored procedures
DECLARE @return_value INT,@exe_id BIGINT,@err_msg NVARCHAR(150)

-- Create the exectuion
EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'folderName', @project_name=N'projectName', @package_name=N'packageName', @use32bitruntime=0, @runinscaleout=1,@useanyworker=1, @execution_id=@exe_id OUTPUT

-- To synchronize SSIS package execution, set the SYNCHRONIZED execution parameter
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1

-- Start the execution                                                         
EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id,@retry_count=0
                                          
-- Raise an error for unsuccessful package execution
-- Execution status values include the following:
-- created (1)
-- running (2)
-- canceled (3)
-- failed (4)
-- pending (5)
-- ended unexpectedly (6)
-- succeeded (7)
-- stopping (8)
-- completed (9) 
IF(SELECT [status]
   FROM [SSISDB].[catalog].[executions]
   WHERE execution_id=@exe_id)<>7
BEGIN
    SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20))
    RAISERROR(@err_msg,15,1)
END
GO
```

Para obtener más información sobre el código de esta secuencia de comandos, consulte [implementar y ejecutar paquetes SSIS mediante procedimientos almacenados](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca del agente de SQL Server, vea [trabajos del Agente SQL Server para los paquetes](../packages/sql-server-agent-jobs-for-packages.md).

Para obtener más información acerca de los trabajos elásticos de base de datos de SQL, consulte [bases de datos de escala horizontal en la nube de administración](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-elastic-jobs-overview).
