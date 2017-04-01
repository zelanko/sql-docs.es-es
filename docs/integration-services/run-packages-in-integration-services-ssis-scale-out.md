---
title: "Run Packages in Integration Services (SSIS) Scale Out (Ejecutar paquetes en el escalado horizontal de Integration Services [SSIS]) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f4cd7-9c47-416d-bb1e-40acc3e05342
caps.latest.revision: 5
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 5
---
# Run Packages in Integration Services (SSIS) Scale Out (Ejecutar paquetes en el escalado horizontal de Integration Services [SSIS])
Una vez implementados los paquetes en el servidor de Integration Services, puede ejecutarlos en el escalado horizontal.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Ejecutar paquetes con el cuadro de diálogo **Ejecutar paquete en escalado horizontal** 

1. ### <a name="open-the-execute-package-in-scale-out-dialog-box"></a>Abrir el cuadro de diálogo Ejecutar paquete en escalado horizontal ###
    En [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)], conecte con el servidor de Integration Services. En el Explorador de objetos, expanda el árbol para ver los nodos de **Catálogos de Integration Services**. Haga clic en el nodo **SSISDB** o el proyecto o el paquete que quiera ejecutar y, luego, haga clic en **Ejecutar en escalado horizontal**.
2. ### <a name="select-packages-and-set-the-options"></a>Seleccionar paquetes y establecer las opciones ###
    En la página **Selección de paquetes**, seleccione varios paquetes para ejecutar y establecer el entorno, los parámetros, los administradores de conexión y las opciones avanzadas para cada paquete. Haga clic en un paquete para establecer estas opciones.
    
    En la pestaña **Avanzadas**, establezca una opción de escalado horizontal denominada **Número de reintentos**. Establece el número de veces que se vuelve a intentar ejecutar un paquete si se produce un error.
3. ### <a name="select-machines"></a>Seleccionar equipos ###
    En la página **Selección de equipo**, seleccione los equipos de trabajador de escalado horizontal para ejecutar los paquetes. De forma predeterminada, cualquier máquina puede ejecutar los paquetes. 

   > [!NOTE]
> Los paquetes se ejecutan con las credenciales de las cuentas de usuario de los servicios de trabajador de escalado horizontal, que se muestran en la página **Selección de equipo**. De forma predeterminada, la cuenta es NT Service\SSISScaleOutWorker140. Es posible que quiera cambiar a sus propias cuentas de laboratorio.

4. ### <a name="run-the-packages-and-view-reports"></a>Ejecutar los paquetes y ver informes 
    Haga clic en **Aceptar** para iniciar las ejecuciones de paquetes. Para ver el informe de ejecución de un paquete, haga clic con el botón derecho en el paquete en el Explorador de objetos, haga clic en **Informes**, en **Todas las ejecuciones** y busque la ejecución.
    
    
## <a name="run-packages-with-stored-procedures"></a>Ejecutar paquetes con procedimientos almacenados

1. ### <a name="create-executions"></a>Crear ejecuciones ###
    Llame a [catalog].[create_execution] para cada paquete. Establezca el parámetro **@runincluster** en True. Si no se permite a todas las máquinas de trabajador de escalado horizontal ejecutar el paquete, establezca el parámetro **@useanyworker** en False.   
2. ### <a name="set-execution-parameters"></a>Establecer parámetros de ejecución ###
    Llame a [catalog].[set_execution_parameter_value] para cada ejecución.
3. ### <a name="set-scale-out-workers"></a>Establecer trabajadores de escalado horizontal ###
    Llame a [catalog].[add_execution_worker]. Si se permite a cualquier máquina ejecutar el paquete, no tiene que llamar a este procedimiento almacenado. 
4. ### <a name="start-executions"></a>Iniciar ejecuciones ###
    Llame a [catalog].[start_execution]. Establezca el parámetro **@retry_count** para definir el número de veces que se vuelve a intentar ejecutar un paquete si se produce un error.
    
    ### <a name="example"></a>Ejemplo  ###  
    En el ejemplo siguiente se ejecutan dos paquetes, package1.dtsx y package2.dtsx, en escalado horizontal con un trabajador de escalado horizontal.  
    ```
    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO

    Declare @execution_id bigint
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runincluster=True
    Select @execution_id
    DECLARE @var0 smallint = 1
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
    EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
    EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
    GO
    ```


## <a name="permissions"></a>Permissions
Para ejecutar paquetes en escalado horizontal se necesita alguno de los siguientes permisos:

-   Pertenencia al rol de base de datos **ssis_admin**  

-   Pertenencia al rol de base de datos **ssis_cluster_executor**  
  
-   Pertenencia al rol de servidor **sysadmin**  
    