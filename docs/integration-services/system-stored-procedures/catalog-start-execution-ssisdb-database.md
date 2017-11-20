---
title: Catalog.start_execution (base de datos de SSISDB) | Documentos de Microsoft
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
ms.assetid: f8663ff3-aa98-4dd8-b850-b21efada0b87
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 8edb51596198f27f00c1b78ddc8b3075ad035143
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogstartexecution-ssisdb-database"></a>catalog.start_execution (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Inicia una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.start_execution [@execution_id =] execution_id [, [@retry_count =] retry_count]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@execution_id =] *execution_id*  
 Identificador único de la instancia de ejecución. El *execution_id* es **bigint**.
 
 [@retry_count =] *número_reintentos*  
 El número de reintentos si se produce un error en la ejecución. Entrará en vigor solo si la ejecución en horizontalmente. Este parámetro es opcional. Si no se especifica, su valor se establece en 0. El *cuenta_reintentos* es **int**.
  
## <a name="remarks"></a>Comentarios  
 Una ejecución se utiliza para especificar los valores de parámetro que es utilizado por un paquete durante una única instancia de ejecución del paquete. Puede ocurrir que, después de crear una instancia de ejecución y antes de que se inicie, el proyecto correspondiente se implemente de nuevo. En este caso, la instancia de ejecución hace referencia a un proyecto que no está actualizado. Esta referencia no válida hace que el procedimiento almacenado genere un error.  
  
> [!NOTE]  
>  Las ejecuciones solo pueden iniciarse una vez. Para iniciar una instancia de ejecución, debe estar en estado creado (un valor de `1` en el **estado** columna de la [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) vista).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se llama a catalog.create_execution para crear una instancia de ejecución para el paquete Child1.dtsx. Project1 de Integration Services contiene el paquete. En el ejemplo se llama a catalog.set_execution_parameter_value para establecer valores para los parámetros Parameter1, Parameter2 y LOGGING_LEVEL. En el ejemplo se llama a catalog.start_execution para iniciar una instancia de ejecución.  
  
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
  
-   Los permisos READ y MODIFY de la instancia de ejecución, los permisos READ y EXECUTE del proyecto y, si procede, los permisos READ del entorno al que se hace referencia  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El usuario no tiene los permisos adecuados  
  
-   El identificador de ejecución no es válido  
  
-   La ejecución se ha iniciado previamente o se ha completado ya; las ejecuciones pueden iniciarse una sola vez  
  
-   La referencia de entorno asociado al proyecto no es válida  
  
-   No se han establecido los valores de parámetro necesarios  
  
-   La versión del proyecto asociada a la instancia de ejecución está obsoleta; solo se puede ejecutar la versión más actual de un proyecto  
  
  

