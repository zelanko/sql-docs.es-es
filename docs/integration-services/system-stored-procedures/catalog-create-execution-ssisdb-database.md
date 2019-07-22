---
title: catalog.create_execution (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b1454c1112f12800e010974159d4ea7ad3526e1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023443"
---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Crea una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Este procedimiento almacenado usa el nivel de registro de servidor predeterminado.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_execution [@folder_name = folder_name  
     , [@project_name =] project_name  
     , [@package_name =] package_name  
  [  , [@reference_id =] reference_id ]  
  [  , [@use32bitruntime =] use32bitruntime ] 
  [  , [@runinscaleout =] runinscaleout ]
  [  , [@useanyworker =] useanyworker ] 
     , [@execution_id =] execution_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *folder_name*  
 El nombre de la carpeta que contiene el paquete que se va a ejecutar. *folder_name* es **nvarchar(128)** .  
  
 [@project_name =] *project_name*  
 Nombre del proyecto que contiene el paquete que se va a ejecutar. El parámetro *project_name* es de tipo **nvarchar(128)** .  
  
 [@package_name =] *package_name*  
 El nombre del paquete que se va a ejecutar. El parámetro *package_name* es de tipo **nvarchar(260)** .  
  
 [@reference_id =] *reference_id*  
 Un identificador único para una referencia de entorno. Este parámetro es opcional. *reference_id* es **bigint**.  
  
 [@use32bitruntime =] *use32bitruntime*  
 Indica si el motor en tiempo de ejecución de 32 bits se debe usar para ejecutar el paquete en un sistema operativo de 64 bits. Use el valor 1 para ejecutar el paquete con el motor de tiempo de ejecución de 32 bits cuando se ejecute en un sistema operativo de 64 bits. Use el valor 0 para ejecutar el paquete con el motor de tiempo de ejecución de 64 bits cuando se ejecute en un sistema operativo de 64 bits. Este parámetro es opcional. El parámetro *Use32bitruntime* es de tipo **bit**.  
 
 [@runinscaleout =] *runinscaleout*  
 Indique si la ejecución está en Escalabilidad horizontal. Use el valor 1 para ejecutar el paquete en la escalabilidad horizontal. Use el valor 0 para ejecutar el paquete sin escalabilidad horizontal. Este parámetro es opcional. Si no se especifica, su valor se establece en DEFAULT_EXECUTION_MODE en [SSISDB].[catalog].[catalog_properties]. El parámetro *runinscaleout* es de tipo **bit**. 
 
[@useanyworker =] *useanyworker*  
Indique si se permite al trabajo de escalabilidad horizontal para realizar la ejecución.

-   Use el valor 1 para ejecutar el paquete con cualquier trabajo de escalabilidad horizontal. Al establecer `@useanyworker` en true, cualquier trabajo cuyo número máximo de tareas (tal y como se especifica en el archivo de configuración del trabajo) aún no se haya alcanzado, estará disponible para ejecutar el paquete. Para obtener información sobre el archivo de configuración de trabajo, consulte [Trabajador de escalado horizontal de Integration Services (SSIS)](../scale-out/integration-services-ssis-scale-out-worker.md).

-   Use el valor 0 para indicar que no todos los trabajos de escalabilidad horizontal tienen permiso para ejecutar el paquete. Al establecer `@useanyworker` en false, tendrá que especificar los trabajos que están autorizados a ejecutar el paquete mediante el Administrador de escalabilidad horizontal o mediante una llamada al procedimiento almacenado `[catalog].[add_execution_worker]`. Si especifica un trabajo que ya está ejecutando otro paquete, el trabajo finaliza la ejecución del paquete actual antes de solicitar otra ejecución.

Este parámetro es opcional. Si no se especifica, su valor se establece en 1. El parámetro *useanyworker* es de tipo **bit**. 
  
 [@execution_id =] *execution_id*  
 Devuelve el identificador único de una instancia de ejecución. El parámetro *execution_id* es de tipo **bigint**.  

  
## <a name="remarks"></a>Notas  
 Una ejecución se utiliza para especificar los valores de parámetro que va a usar un paquete durante una instancia única de ejecución del paquete.  
  
 Si una referencia de entorno se especifica con el parámetro *reference_id*, el procedimiento almacenado rellena los parámetros de paquete y proyecto con los valores literales o los valores a los que se hace referencia de las variables de entorno correspondientes. Si se especifica la referencia de entorno, los valores de parámetro predeterminados se utilizan durante la ejecución del paquete. Para determinar exactamente qué valores se usan para una instancia determinada de ejecución, utilice el valor del parámetro de salida *execution_id* de este de procedimiento almacenado y consulte la vista [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md).  
  
 Solo los paquetes que se marcan como paquetes de punto de entrada se pueden especificar en una ejecución. Si se especifica un paquete que no es un punto de entrada, la ejecución produce un error.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se llama a catalog.create_execution para crear una instancia de ejecución para el paquete Child1.dtsx, que no se encuentra en escalabilidad horizontal. Project1 de Integration Services contiene el paquete. En el ejemplo se llama a catalog.set_execution_parameter_value para establecer valores para los parámetros Parameter1, Parameter2 y LOGGING_LEVEL. En el ejemplo se llama a catalog.start_execution para iniciar una instancia de ejecución.  
  
```sql  
Declare @execution_id bigint  
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Child1.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'TestDeply4', @project_name=N'Integration Services Project1', @use32bitruntime=False, @reference_id=Null  
Select @execution_id  
DECLARE @var0 sql_variant = N'Child1.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter1', @parameter_value=@var0  
DECLARE @var1 sql_variant = N'Child2.dtsx'  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=20, @parameter_name=N'Parameter2', @parameter_value=@var1  
DECLARE @var2 smallint = 1  
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id, @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var2  
EXEC [SSISDB].[catalog].[start_execution] @execution_id  
GO  
```  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos de lectura y ejecución en el proyecto y, si es aplicable, permisos de lectura en el entorno al que se hace referencia  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  

 Si @runinscaleout es 1, el procedimiento almacenado necesita uno de los permisos siguientes:
 
-   Pertenencia al rol de base de datos de **ssis_admin**

-   Pertenencia al rol de base de datos **ssis_cluster_executor**

-   Pertenencia al rol de servidor de **sysadmin**
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 La siguiente lista describe algunas condiciones que pueden producir un error o una advertencia:  
  
-   El paquete no existe.  
  
-   El usuario no tiene los permisos adecuados.  
  
-   La referencia de entorno, *reference_id*, no es válida.  
  
-   El paquete que se especifica no es un paquete de punto de entrada.  
  
-   El tipo de datos de la variable de entorno a la que se hace referencia es diferente del tipo de datos del parámetro de paquete o proyecto.  
  
-   El proyecto o el paquete contienen parámetros que requieren valores, pero no se ha asignado ningún valor.  
  
-   Las variables de entorno a las que se hace referencia no se encuentran en el entorno especificado por la referencia de entorno, *reference_id*.  
  
## <a name="see-also"></a>Consulte también  
 [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) (catalog.set_execution_parameter_value [base de datos de SSISDB];)  
 [catalog.add_execution_worker &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  
