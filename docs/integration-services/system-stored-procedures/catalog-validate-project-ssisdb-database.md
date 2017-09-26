---
title: Catalog.validate_project (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 5270689a-46d4-4847-b41f-3bed1899e955
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 83439015694f4235af4a67e994e916651ec63cc1
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogvalidateproject-ssisdb-database"></a>catalog.validate_project (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Valida de forma asincrónica un proyecto del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
validate_project [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @validate_type = ] validate_type  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de una carpeta que contiene el proyecto. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project_name =] *Nombre_proyecto*  
 Nombre del proyecto. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @validate_type =] *validate_type*  
 Indica el tipo de validación que se llevará a cabo. Utilice el carácter `F` para realizar una validación completa. El *validate_type* es **char (1)**.  
  
 [ @validation_id =] *validation_id*  
 Devuelve el identificador único (ID) de la validación. El *validation_id* es **bigint**.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 Indica si el motor en tiempo de ejecución de 32 bits se debe usar para ejecutar el paquete en un sistema operativo de 64 bits. Utilice el valor de `1` para ejecutar el paquete con el tiempo de ejecución de 32 bits cuando se ejecuta en un sistema operativo de 64 bits. Use el valor `0` para ejecutar el paquete con el motor en tiempo de ejecución de 64 bits cuando se ejecute en un sistema operativo de 64 bits. Este parámetro es opcional. El *use32bitruntime* es **bits**.  
  
 [ @environment_scope =] *environment_scope*  
 Indica las referencias de entorno que la validación tiene en cuenta. Cuando el valor es `A`, todas las referencias de entorno asociadas con el proyecto se incluyen en la validación. Cuando el valor es `S`, solo se incluye una sola referencia de entorno. Cuando el valor es `D`, no se incluyen referencias de entorno y todos los parámetros deben tener un valor literal predeterminado para pasar la validación. Este parámetro es opcional, el carácter `D` se usará de forma predeterminada. El *environment_scope* es **char (1)**.  
  
 [ @reference_id =] *reference_id*  
 El identificador único de la referencia de entorno. Este parámetro es necesario únicamente cuando se incluye una sola referencia de entorno en la validación, cuando *environment_scope* es `S`. El *reference_id* es **bigint**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 La salida de los pasos de la validación se devuelve como secciones diferentes del conjunto de resultados.  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos de lectura en el objeto y, si es aplicable, permisos de lectura en los entornos a los que se hace referencia  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se proporcionan algunas condiciones que pueden producir un error o una advertencia:  
  
-   La validación no puede realizarse para uno o más paquetes del proyecto  
  
-   La validación no puede realizarse si uno o varios de los entornos a los que se hace referencia y que están incluidos en la validación no contienen variables a las que se haga referencia  
  
-   El tipo de validación especificado no es válido  
  
-   El nombre del proyecto o el identificador de la referencia del entorno es no válido  
  
-   El usuario no tiene los permisos adecuados  
  
## <a name="remarks"></a>Comentarios  
 La validación ayuda a identificar problemas que impedirán que los paquetes del proyecto se ejecuten correctamente. Use la [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) o [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) vistas para supervisar el estado de validación.  
  
 Solo los entornos que son accesibles por el usuario se pueden utilizar en la validación. El resultado de la validación se envía al cliente como un conjunto de resultados.  
  
 En esta versión, la validación del proyecto no admite la validación de dependencias.  
  
 La validación completa confirma que todas las variables de entorno a las que se hace referencia se encuentran dentro de los entornos a los que se hace referencia y que se incluyeron en la validación. Los resultados de la validación completa enumeran las referencias de entorno que no son válidas y las variables de entorno a las que se hace referencia que podrían no encontrarse en ninguno de los entornos a los que se hace referencia y que se incluyeron en la validación.  
  
  
