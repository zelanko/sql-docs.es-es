---
title: Catalog.set_execution_parameter_value (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 055d86c9-befd-4e63-acb1-6dfe833549d2
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 7b13e7b1c28bad6e573e829183372da4bb62f92d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="catalogsetexecutionparametervalue-ssisdb-database"></a>catalog.set_execution_parameter_value (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el valor de un parámetro para una instancia de ejecución en el catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 No se puede cambiar un valor de parámetro después de que se haya iniciado una instancia de ejecución.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_execution_parameter_value [ @execution_id = execution_id  
    , [ @object_type = ] object_type  
    , [ @parameter_name = ] parameter_name  
    , [ @parameter_value = ] parameter_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 Identificador único de la instancia de ejecución. El *execution_id* es **bigint**.  
  
 [ @object_type =] *object_type*  
 El tipo del parámetro.  
  
 Para los parámetros siguientes, establezca *object_type* a 50  
  
-   LOGGING_LEVEL  
  
-   CUSTOMIZED_LOGGING_LEVEL  
  
-   DUMP_ON_ERROR  
  
-   DUMP_ON_EVENT  
  
-   DUMP_EVENT_CODE  
  
-   CALLER_INFO  
  
-   SYNCHRONIZED  
  
 Use el valor `20` para indicar un parámetro de proyecto o el valor `30` para indicar un parámetro de paquete.  
  
 El *object_type* es **smallint**.  
  
 [ @parameter_name =] *parameter_name*  
 Nombre del parámetro. El *parameter_name* es **nvarchar (128)**.  
  
 [ @parameter_value =] *parameter_value*  
 El valor del parámetro. El *parameter_value* es **sql_variant**.  
  
## <a name="remarks"></a>Comentarios  
 Para determinar los valores de parámetros usados para una ejecución determinada, consulte la vista catalog.execution_parameter_values.  
  
 Para especificar el ámbito de la información que se registra durante la ejecución del paquete, establezca *parameter_name* en LOGGING_LEVEL y *parameter_value* a uno de los siguientes valores.  
  
 Establecer el *object_type* parámetro en 50.  
  
|Value|Descripción|  
|-----------|-----------------|  
|0|None<br /><br /> El registro está desactivado. Solo se registra el estado de ejecución del paquete.|  
|1|Básico<br /><br /> Se registran todos los eventos, excepto los eventos personalizados y de diagnóstico. Es el valor predeterminado.|  
|2|Rendimiento<br /><br /> Solo se registran las estadísticas de rendimiento, y los eventos OnError y OnWarning.|  
|3|Detallado<br /><br /> Se registran todos los eventos, incluidos los eventos personalizados y de diagnóstico. <br />Los eventos personalizados incluyen los eventos registrados por las tareas de Integration Services. Para obtener más información, vea [Custom Messages for Logging](../../integration-services/performance/integration-services-ssis-logging.md#custom_messages)|  
|4|Linaje en tiempo de ejecución<br /><br /> Recopila los datos necesarios para realizar el seguimiento de linaje en el flujo de datos.|  
|100|Nivel de registro personalizado<br /><br /> Especifique la configuración en el parámetro CUSTOMIZED_LOGGING_LEVEL. Para obtener más información acerca de los valores que se pueden especificar, vea [catalog.create_customized_logging_level](../../integration-services/system-stored-procedures/catalog-create-customized-logging-level.md).<br /><br /> Para obtener más información acerca de los niveles de registro personalizados, consulte [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).|  
  
 Para especificar que el servidor de Integration Services genere archivos de volcado cuando se produzca algún error durante la ejecución del paquete, establezca los valores de los parámetros siguientes para una instancia de ejecución que no se haya ejecutado.  
  
|Parámetro|Value|  
|---------------|-----------|  
|*execution_id*|El identificador único para la instancia de ejecución|  
|*object_type*|50|  
|*parameter_name*|‘DUMP_ON_ERROR|  
|*parameter_value*|1|  
  
 Para especificar que el servidor de Integration Services genere archivos de volcado cuando se produzcan eventos durante la ejecución del paquete, establezca los valores de los parámetros siguientes para una instancia de ejecución que no se haya ejecutado.  
  
|Parámetro|Value|  
|---------------|-----------|  
|*execution_id*|El identificador único para la instancia de ejecución|  
|*object_type*|50|  
|*parameter_name*|‘DUMP_ON_EVENT|  
|*parameter_value*|1|  
  
 Para especificar los eventos durante la ejecución del paquete que hacen que el servidor de Integration Services genere archivos de volcado, establezca los valores de los parámetros siguientes para una instancia de ejecución que no se haya ejecutado. Separe los diversos códigos de evento mediante un punto y coma.  
  
|Parámetro|Value|  
|---------------|-----------|  
|*execution_id*|El identificador único para la instancia de ejecución|  
|*object_type*|50|  
|*parameter_name*|DUMP_EVENT_CODE|  
|*parameter_value*|Uno o varios códigos de evento.|  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se especifica que el servidor de Integration Services genera archivos de volcado cuando se produce un error durante la ejecución del paquete.  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_ERROR',1  
```  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se especifica que el servidor de Integration Services genera archivos de volcado cuando se producen eventos durante la ejecución del paquete, y se especifica el evento que hace que el servidor genere los archivos.  
  
```sql
exec catalog.create_execution  'TR2','Recurring ETL', 'Dim_DCVendor.dtsx',NULL, 0,@execution_id out  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_ON_EVENT',1  
  
declare @event_code nvarchar(50)  
set @event_code = '0xC020801C'  
exec catalog.set_execution_parameter_value  @execution_id, 50, 'DUMP_EVENT_CODE', @event_code  
```  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados  
  
-   El identificador de ejecución no es válido  
  
-   El nombre de parámetro no es válido  
  
-   El tipo de datos del valor de parámetro no coincide con el tipo de datos del parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Catalog.execution_parameter_values &#40; Base de datos SSISDB &#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)   
 [Generar archivos de volcado para la ejecución de paquetes](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
