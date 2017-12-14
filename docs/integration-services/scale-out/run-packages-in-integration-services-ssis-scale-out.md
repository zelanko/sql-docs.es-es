---
title: Ejecutar paquetes en la escalabilidad horizontal de SQL Server Integration Services (SSIS) | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
f1_keywords: sql13.ssis.ssms.ispackageexecuteinscaleout.f1
ms.workload: Inactive
ms.openlocfilehash: 88537ff52ada042d642b8915342e374ecca3246e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="run-packages-in-integration-services-ssis-scale-out"></a>Ejecutar paquetes en la escalabilidad horizontal de Integration Services (SSIS)
Una vez implementados los paquetes en el servidor de Integration Services, puede ejecutarlos en el escalado horizontal.

## <a name="run-packages-with-execute-package-in-scale-out-dialog"></a>Ejecutar paquetes con el cuadro de diálogo Ejecutar paquete en escalabilidad horizontal 

1. Abrir el cuadro de diálogo Ejecutar paquete en escalado horizontal

    En [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)], conecte con el servidor de Integration Services. En el Explorador de objetos, expanda el árbol para ver los nodos de **Catálogos de Integration Services**. Haga clic en el nodo **SSISDB** o el proyecto o el paquete que quiera ejecutar y, luego, haga clic en **Ejecutar en escalado horizontal**.

2. Seleccionar paquetes y establecer las opciones

    En la página **Selección de paquetes** , seleccione varios paquetes para ejecutar y establecer el entorno, los parámetros, los administradores de conexión y las opciones avanzadas para cada paquete. Haga clic en un paquete para establecer estas opciones.
    
    En la pestaña **Avanzadas** , establezca una opción de escalado horizontal denominada **Número de reintentos**. Establece el número de veces que se vuelve a intentar ejecutar un paquete si se produce un error.

    > [!Note]
    > La opción **Volcado de errores** solo surte efecto cuando la cuenta que ejecuta el servicio Trabajador de escalabilidad horizontal es un administrador del equipo local.

3. Seleccionar equipos

    En la página **Selección de equipo** , seleccione los equipos de trabajador de escalado horizontal para ejecutar los paquetes. De forma predeterminada, cualquier máquina puede ejecutar los paquetes. 

   > [!Note] 
   > Los paquetes se ejecutan con las credenciales de las cuentas de usuario de los servicios de trabajador de escalado horizontal, que se muestran en la página **Selección de equipo** . De forma predeterminada, la cuenta es NT Service\SSISScaleOutWorker140. Es posible que quiera cambiar a sus propias cuentas de laboratorio.

   >[!WARNING]
   >Las ejecuciones de paquetes que desencadenan usuarios diferentes en el mismo trabajo se ejecutan con la misma cuenta. No presentan ningún límite de seguridad entre sí. 

4. Ejecutar los paquetes y ver informes 

    Haga clic en **Aceptar** para iniciar las ejecuciones de paquetes. Para ver el informe de ejecución de un paquete, haga clic con el botón derecho en el paquete en el Explorador de objetos, haga clic en **Informes**, en **Todas las ejecuciones**y busque la ejecución.
    
## <a name="run-packages-with-stored-procedures"></a>Ejecutar paquetes con procedimientos almacenados

1. Crear ejecuciones

    Llame a [catalog].[create_execution] para cada paquete. Establezca el parámetro **@runinscaleout** en True. Si no se permite a todas las máquinas de trabajador de escalado horizontal ejecutar el paquete, establezca el parámetro **@useanyworker** en False.   

2. Establecer parámetros de ejecución

    Llame a [catalog].[set_execution_parameter_value] para cada ejecución.

3. Establecer trabajadores de escalado horizontal

    Llame a [catalog].[add_execution_worker]. Si se permite a cualquier máquina ejecutar el paquete, no tiene que llamar a este procedimiento almacenado. 

4. Iniciar ejecuciones

    Llame a [catalog].[start_execution]. Establezca el parámetro **@retry_count** para definir el número de veces que se vuelve a intentar ejecutar un paquete si se produce un error.
    
#### <a name="example"></a>Ejemplo
En el ejemplo siguiente se ejecutan dos paquetes, package1.dtsx y package2.dtsx, en escalado horizontal con un trabajador de escalado horizontal.  

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder1', @project_name=N'project1', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO

Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'package2.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'folder2', @project_name=N'project2', @use32bitruntime=False, @reference_id=Null, @useanyworker=False, @runinscaleout=True
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0
EXEC [SSISDB].[catalog].[add_execution_worker] @execution_id,  @workeragent_id=N'64c020e2-f819-4c2d-a22f-efb31a91e70a'
EXEC [SSISDB].[catalog].[start_execution] @execution_id,  @retry_count=0
GO
```

### <a name="permissions"></a>Permissions
Para ejecutar paquetes en escalado horizontal se necesita alguno de los siguientes permisos:

-   Pertenencia al rol de base de datos **ssis_admin**  

-   Pertenencia al rol de base de datos **ssis_cluster_executor**  
  
-   Pertenencia al rol de servidor **sysadmin**  

## <a name="set-default-execution-mode"></a>Establecer el modo de ejecución predeterminado
Para establecer el modo de ejecución predeterminado en "Escalabilidad horizontal", haga clic en el nodo **SSISDB** del Explorador de objetos de SSMS y seleccione **Propiedades**.
En el cuadro de diálogo **Propiedades del catálogo**, establezca **Modo de ejecución predeterminado de todo el servidor** en **Escalabilidad horizontal**.

Después de esta configuración, no es necesario especificar el parámetro **@runinscaleout** para [catalog].[create_execution]. Las ejecuciones se ejecutan automáticamente con Escalabilidad horizontal. 

![Modo de ejecución](media\exe-mode.PNG)

Para volver a cambiar el modo de ejecución predeterminado a Escalabilidad horizontal, establezca **Modo de ejecución predeterminado de todo el servidor** en **Servidor**.

## <a name="run-package-in-sql-agent-job"></a>Ejecutar el paquete en el trabajo del Agente SQL
En el trabajo del agente SQL, puede optar por ejecutar un paquete SSIS como un paso del trabajo. Para ejecutar el paquete con Escalabilidad horizontal, puede aprovechar el modo de ejecución predeterminado anterior. Después de configurar el modo de ejecución predeterminado en "Escalabilidad horizontal", los trabajos del agente SQL se ejecutarán con Escalabilidad horizontal.
