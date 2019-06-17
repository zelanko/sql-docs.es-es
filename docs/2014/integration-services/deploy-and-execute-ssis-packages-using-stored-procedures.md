---
title: Implementar y ejecutar paquetes SSIS mediante procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 56141595c62e5190bf3ef797059acd602f801ed7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059605"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>Implementar y ejecutar paquetes SSIS mediante procedimientos almacenados
  Al configurar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para que use el modelo de implementación de proyectos, puede emplear procedimientos almacenados del catálogo de [!INCLUDE[ssIS](../includes/ssis-md.md)] implementar el proyecto y ejecutar los paquetes. Para obtener información acerca del modelo de implementación de proyectos, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 También puede usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para implementar el proyecto y ejecutar los paquetes. Para obtener más información, vea los temas de la sección **Vea también** .  
  
> [!TIP]
>  Puede generar fácilmente las instrucciones Transact-SQL para los procedimientos almacenados enumerados en el procedimiento siguiente, a excepción de catalog.deploy_project, si hace lo siguiente:  
> 
>  1.  En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], expanda el nodo de **Catálogos de Integration Services** en el Explorador de objetos y navegue hasta el paquete que desea ejecutar.  
> 2.  Haga clic con el botón derecho en el paquete y, después, haga clic en **Ejecutar**.  
> 3.  Según sea necesario, establezca los valores de parámetros, las propiedades del administrador de conexiones y las opciones de la pestaña **Avanzadas** , como el nivel de registro.  
> 
>      Para obtener más información acerca de los niveles de registro, vea [Habilitar el registro para la ejecución de paquetes en el servidor SSIS](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md).  
> 4.  Antes de hacer clic en **Aceptar** para ejecutar el paquete, haga clic en **Script**. Transact-SQL aparece en una ventana del Editor de consultas en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>Para implementar y ejecutar un paquete mediante procedimientos almacenados  
  
1.  Llame a [catalog.deploy_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) para implementar el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Para recuperar el contenido binario del archivo de implementación de proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , para el parámetro *@project_stream* , use una instrucción SELECT con la función OPENROWSET y el proveedor de conjuntos de filas BULK. El proveedor de conjuntos de filas BULK le permite leer datos de un archivo. El argumento SINGLE_BLOB del proveedor de conjuntos de filas BULK devuelve el contenido del archivo de datos como un conjunto de filas de una sola fila y una sola columna de tipo varbinary(max). Para obtener más información, vea [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
     En el ejemplo siguiente, el proyecto SSISPackages_ProjectDeployment se implementa en la carpeta Paquetes SSIS del servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Los datos binarios se leen del archivo de proyecto (SSISPackage_ProjectDeployment.ispac) y se almacenan en el parámetro *@ProjectBinary* de tipo varbinary(max). El valor de parámetro *@ProjectBinary* se asigna al parámetro *@project_stream* .  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  Llame a [catalog.create_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) para crear una instancia de la ejecución de paquetes y llame opcionalmente a [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) para establecer los valores de parámetro en tiempo de ejecución.  
  
     En el ejemplo siguiente, catalog.create_execution crea una instancia de ejecución del package.dtsx contenido en el proyecto SSISPackage_ProjectDeployment. El proyecto se encuentra en la carpeta SSIS Packages. El execution_id devuelto por el procedimiento almacenado se emplea en la llamada a catalog.set_execution_parameter_value. Este segundo procedimiento almacenado establece el parámetro LOGGING_LEVEL en 3 (registro detallado) y establece un parámetro de paquete denominado Parameter1 en un valor de 1.  
  
     Para los parámetros como LOGGING_LEVEL, el valor de object_type es 50. Para los parámetros de paquete, el valor de object_type es 30.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  Llame a [catalog.start_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) para ejecutar el paquete.  
  
     En el ejemplo siguiente, se agrega a Transact-SQL una llamada a catalog.start_execution para iniciar la ejecución del paquete. Se empela el execution_id devuelto por el procedimiento almacenado catalog.create_execution.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>Para implementar un proyecto entre servidores mediante procedimientos almacenados  
 Puede implementar un proyecto entre servidores mediante los procedimientos almacenados [catalog.get_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database) y [catalog.deploy_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database).  
  
 Debe hacer lo siguiente antes de ejecutar los procedimientos almacenados.  
  
-   Cree un objeto de servidor vinculado. Para obtener más información, vea [Crear servidores vinculados &#40;motor de base de datos de SQL Server&#41;](../database-engine/sql-server-database-engine-overview.md).  
  
     En la página **Opciones del servidor** del cuadro de diálogo **Propiedades del servidor vinculado** , establezca **RPC** y **Salida RPC** en **True**. Establezca también **Habilitar la promoción de transacciones distribuidas para RPC** en **False**.  
  
-   Habilite los parámetros dinámicos del proveedor seleccionado para el servidor vinculado; para ello, expanda el nodo de **Proveedores** en **Servidores vinculados** en el Explorador de objetos, haga clic con el botón derecho en el proveedor y, después, haga clic en **Propiedades**. Seleccione **Habilitar** junto a **Parámetro dinámico**.  
  
-   Confirme que el Coordinador de transacciones distribuidas (DTC) se inicia en ambos servidores.  
  
 Llame a catalog.get_project para devolver el contenido binario del proyecto y llame después a catalog.deploy_project. El valor devuelto por catalog.get_project se inserta en una variable de tabla de tipo varbinary(max). El servidor vinculado no puede devolver resultados que son varbinary(max).  
  
 En el ejemplo siguiente, catalog.get_project devuelve un contenido binario para el proyecto SSISPackages del servidor vinculado. catalog.deploy_project implementa el proyecto en el servidor local, en la carpeta denominada DestFolder.  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Implementar proyectos en el servidor de Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [Ejecutar un paquete en herramientas de datos de SQL Server](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [Ejecutar un paquete en el Servidor SSIS con SQL Server Management Studio](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
