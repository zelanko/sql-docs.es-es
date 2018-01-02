---
title: "Programar la ejecución de paquetes SSIS en Azure | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0b8dbc635523b33a480ad887b73d9f395d71c8d
ms.sourcegitcommit: ffa4ce9bd71ecf363604966c20cbd2710d029831
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2017
---
# <a name="schedule-the-execution-of-an-ssis-package-on-azure"></a>Programar la ejecución de un paquete SSIS en Azure
Puede programar la ejecución de paquetes almacenados en la base de datos del catálogo de SSISDB en un servidor de Azure SQL Database. Para ello, elija una de las opciones de programación siguientes:
-   [Agente SQL Server](#agent)
-   [Trabajos elásticos de SQL Database](#elastic)
-   [Actividad de procedimiento almacenado de SQL Server de Azure Data Factory](#sproc)

## <a name="agent"></a> Programar un paquete mediante el Agente SQL Server

### <a name="prerequisite"></a>Requisito previo

Para poder usar el Agente SQL Server de forma local para programar la ejecución de paquetes almacenados en un servidor de Azure SQL Database, tiene que agregar el servidor de SQL Database como un servidor vinculado. Para obtener más información, consulte [Crear servidores vinculados](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md) y [Servidores vinculados](../../relational-databases/linked-servers/linked-servers-database-engine.md).

### <a name="create-a-sql-server-agent-job"></a>Crear un trabajo del Agente SQL Server

Para programar un paquete con el Agente SQL Server de forma local, cree un trabajo con un paso de trabajo que llame a los procedimientos almacenados `[catalog].[create_execution]` y, a continuación, `[catalog].[start_execution]` del catálogo de SSIS. Para obtener más información, consulte [Trabajos del Agente SQL Server para paquetes](../packages/sql-server-agent-jobs-for-packages.md).

1.  En SQL Server Management Studio, conéctese a la base de datos de SQL Server local en la que desee crear el trabajo.

2.  Haga doble clic en el nodo **Agente SQL Server**, seleccione **Nuevo** y, a continuación, seleccione **Trabajo** para abrir el cuadro de diálogo **Nuevo trabajo**.

3.  En el cuadro de diálogo **Nuevo trabajo**, seleccione la página **Pasos** y, a continuación, seleccione **Nuevo**  para abrir el cuadro de diálogo **Nuevo paso de trabajo**.

4.  En el cuadro de diálogo **Nuevo paso de trabajo**, seleccione `SSISDB` en **Base de datos.**

5.  En el campo de comandos, escriba un script Transact-SQL similar al que se muestra en el ejemplo siguiente:

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

## <a name="elastic"></a> Programar un paquete con trabajos elásticos de SQL Database

Para obtener más información acerca de los trabajos elásticos en SQL Database, consulte [Administración de bases de datos escaladas horizontalmente en la nube](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).

### <a name="prerequisites"></a>Requisitos previos

Para poder usar trabajos elásticos para programar paquetes SSIS almacenados en la base de datos del catálogo de SSISDB en un servidor Azure SQL Database, debe realizar las acciones siguientes:

1.  Instale y configure los componentes de trabajos de Elastic Database. Para obtener más información, consulte [Información general sobre la instalación de trabajos de Elastic Database](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-service-installation).

2. Cree credenciales de ámbito de base de datos que los trabajos puedan usar para enviar comandos a la base de datos del catálogo de SSIS. Para obtener más información, vea [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) [CREAR CREDENCIAL DE ÁMBITO DE BASE DE DATOS (Transact-SQL)].

### <a name="create-an-elastic-job"></a>Crear un trabajo elástico

Cree un trabajo mediante un script Transact-SQL similar al que se muestra en el ejemplo siguiente:

```sql
-- Create Elastic Jobs target group 
EXEC jobs.sp_add_target_group 'TargetGroup' 

-- Add Elastic Jobs target group member 
EXEC jobs.sp_add_target_group_member @target_group_name='TargetGroup', 
    @target_type='SqlDatabase', @server_name='YourSQLDBServer.database.windows.net',
    @database_name='SSISDB' 

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

## <a name="sproc"> Programar un paquete con la actividad de procedimiento almacenado de SQL Server de Azure Data Factory</a>

> [!IMPORTANT]
> Use los scripts JSON del ejemplo siguiente con la actividad de procedimiento almacenado de la versión 1 de Azure Data Factory.

Para programar un paquete con la actividad de procedimiento almacenado de SQL Server de Azure Data Factory, realice las acciones siguientes:

1.  Cree una canalización de Data Factory.

2.  Cree un servicio vinculado para la instancia de SQL Database que hospeda SSISDB.

3.  Cree un conjunto de datos de salida que controle la programación.

4.  Cree una canalización de Data Factory que use la actividad de procedimiento almacenado de SQL Server para ejecutar el paquete SSIS.

En esta sección se proporciona información general sobre estos pasos. Existe un tutorial completo de Data Factory que queda fuera del ámbito de este artículo. Para obtener más información, consulte [Actividad de procedimiento almacenado de SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-stored-proc-activity).

Si se produce un error en una ejecución programada y la actividad del procedimiento almacenada de ADF muestra un identificador de ejecución de la ejecución con el error, busque dicho identificador en el informe de ejecución en SSMS, en el Catálogo de SSIS.

### <a name="created-a-linked-service-for-the-sql-database-that-hosts-ssisdb"></a>Crear un servicio vinculado para la instancia de SQL Database que hospeda SSISDB
El servicio vinculado permite que Data Factory se conecte a SSISDB.

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
### <a name="create-a-data-factory-pipeline"></a>Crear una canalización de Data Factory
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

No tiene que crear un nuevo procedimiento almacenado para encapsular los comandos Transact-SQL necesarios para crear e iniciar la ejecución de paquetes SSIS. Puede proporcionar el script completo como el valor del parámetro `stmt` del ejemplo de JSON anterior. A continuación, se muestra un script de ejemplo:

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

Para proporcionar el script SQL anterior como valor del parámetro `stmt`, normalmente hay que incluir el script completo en una sola línea, como se muestra en el ejemplo siguiente. El [estándar de JSON](https://json.org/) no admite caracteres de control, incluido el nuevo carácter de control de línea `\n` que se emplea en otros lenguajes para separar las líneas en una cadena con varias líneas.

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_executesql",
                    "storedProcedureParameters": {
                        "stmt": "DECLARE @return_value INT, @exe_id BIGINT, @err_msg NVARCHAR(150)    EXEC @return_value=[SSISDB].[catalog].[create_execution] @folder_name=N'test', @project_name=N'TestProject', @package_name=N'STestPackage.dtsx', @use32bitruntime=0, @runinscaleout=1, @useanyworker=1, @execution_id=@exe_id OUTPUT    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @exe_id, @object_type=50, @parameter_name=N'SYNCHRONIZED', @parameter_value=1    EXEC [SSISDB].[catalog].[start_execution] @execution_id=@exe_id, @retry_count=0    IF(SELECT [status] FROM [SSISDB].[catalog].[executions] WHERE execution_id=@exe_id)<>7 BEGIN SET @err_msg=N'Your package execution did not succeed for execution ID: ' + CAST(@exe_id AS NVARCHAR(20)) RAISERROR(@err_msg,15,1) END"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Minute",
                    "interval": 15
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2017-12-06T12:00:00Z",
        "end": "2017-12-06T12:30:00Z",
        "isPaused": false,
        "hubName": "test_hub",
        "pipelineMode": "Scheduled"
    }
}
```

Para obtener más información sobre el código de este script, consulte [Implementar y ejecutar paquetes SSIS mediante procedimientos almacenados](../packages/deploy-integration-services-ssis-projects-and-packages.md#deploy-and-execute-ssis-packages-using-stored-procedures).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, sobre el Agente SQL Server, consulte [Trabajos del Agente SQL Server para paquetes](../packages/sql-server-agent-jobs-for-packages.md).

Para obtener más información acerca de los trabajos elásticos en SQL Database, consulte [Administración de bases de datos escaladas horizontalmente en la nube](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview).
