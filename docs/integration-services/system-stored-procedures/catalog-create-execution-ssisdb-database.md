---
title: Catalog.create_execution (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45d0c2f6-1f38-445f-ac06-e2a01f6ac600
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7e9d38935a91bba81359bee7fdbd64dba86d0d26
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogcreateexecution-ssisdb-database"></a>catalog.create_execution (base de datos de SSISDB)
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
 [@folder_name =] *nombreDeCarpeta*  
 El nombre de la carpeta que contiene el paquete que se va a ejecutar. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [@project_name =] *Nombre_proyecto*  
 El nombre del proyecto que contiene el paquete que se va a ejecutar. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [@package_name =] *nombreDePaquete*  
 El nombre del paquete que se va a ejecutar. El *nombreDePaquete* es **nvarchar (260)**.  
  
 [@reference_id =] *reference_id*  
 Un identificador único para una referencia de entorno. Este parámetro es opcional. El *reference_id* es **bigint**.  
  
 [@use32bitruntime =] *use32bitruntime*  
 Indica si el motor en tiempo de ejecución de 32 bits se debe usar para ejecutar el paquete en un sistema operativo de 64 bits. Utilice el valor de 1 para ejecutar el paquete con el tiempo de ejecución de 32 bits cuando se ejecute en un sistema operativo de 64 bits. Use el valor 0 para ejecutar el paquete con el motor de tiempo de ejecución de 64 bits cuando se ejecute en un sistema operativo de 64 bits. Este parámetro es opcional. El *Use32bitruntime* es **bits**.  
 
 [@runinscaleout =] *runinscaleout*  
 Indicar si la ejecución es en horizontalmente. Utilice el valor de 1 para ejecutar el paquete en horizontalmente. Utilice el valor de 0 para ejecutar el paquete sin horizontalmente. Este parámetro es opcional. Si no se especifica, su valor se establece en DEFAULT_EXECUTION_MODE en [SSISDB]. [catalog]. [catalog_properties]. El *runinscaleout* es **bits**. 
 
 [@useanyworker =] *useanyworker*  
  Indique si se permite cualquier escala Out trabajo para realizar la ejecución. Utilice el valor de 1 para ejecutar el paquete con cualquier trabajo de fuera de escala. Use el valor de 0 para indicar que no todos los trabajadores que espera escala tendrán permiso para ejecutar el paquete. Este parámetro es opcional. Si no se especifica, su valor se establece en 1. El *useanyworker* es **bits**. 
  
 [@execution_id =] *execution_id*  
 Devuelve el identificador único de una instancia de ejecución. El *execution_id* es **bigint**.  

  
## <a name="remarks"></a>Comentarios  
 Una ejecución se utiliza para especificar los valores de parámetro que va a usar un paquete durante una instancia única de ejecución del paquete.  
  
 Si se especifica una referencia de entorno con el *reference_id* parámetro, el procedimiento almacenado rellena los parámetros de proyecto y del paquete con los valores literales o valores que se hace referencia desde las variables de entorno correspondiente. Si se especifica la referencia de entorno, los valores de parámetro predeterminados se utilizan durante la ejecución del paquete. Para determinar exactamente qué valores se utilizan para una instancia determinada de ejecución, utilice el *execution_id* valor de parámetro de este procedimiento almacenado y la consulta de salida la [execution_parameter_values](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) vista.  
  
 Solo los paquetes que se marcan como paquetes de punto de entrada se pueden especificar en una ejecución. Si se especifica un paquete que no es un punto de entrada, la ejecución produce un error.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se llama a catalog.create_execution para crear una instancia de ejecución para el paquete Child1.dtsx, que no está en horizontalmente. Project1 de Integration Services contiene el paquete. En el ejemplo se llama a catalog.set_execution_parameter_value para establecer valores para los parámetros Parameter1, Parameter2 y LOGGING_LEVEL. En el ejemplo se llama a catalog.start_execution para iniciar una instancia de ejecución.  
  
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
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos de lectura y ejecución en el proyecto y, si es aplicable, permisos de lectura en el entorno al que se hace referencia  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  

 Si @runinscaleout es 1, el procedimiento almacenado requiere uno de los siguientes permisos:
 
-   La pertenencia a la **ssis_admin** rol de base de datos

-   La pertenencia a la **ssis_cluster_executor** rol de base de datos

-   La pertenencia a la **sysadmin** rol de servidor
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 La siguiente lista describe algunas condiciones que pueden producir un error o una advertencia:  
  
-   El paquete no existe.  
  
-   El usuario no tiene los permisos adecuados.  
  
-   La referencia de entorno, *reference_id*, no es válido.  
  
-   El paquete que se especifica no es un paquete de punto de entrada.  
  
-   El tipo de datos de la variable de entorno a la que se hace referencia es diferente del tipo de datos del parámetro de paquete o proyecto.  
  
-   El proyecto o el paquete contienen parámetros que requieren valores, pero no se ha asignado ningún valor.  
  
-   Las variables de entorno que se hace referencia no se encuentra en el entorno que el entorno de referencia, *reference_id*, especifica.  
  
## <a name="see-also"></a>Vea también  
 [Catalog.start_execution &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)   
 [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 [Catalog.add_execution_worker &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)  
  

