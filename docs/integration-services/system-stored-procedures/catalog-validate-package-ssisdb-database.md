---
title: Catalog.validate_package (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- validate_package stored procedure [Integration Services]
- catalog.validate_package stored procedure [Integration Services]
ms.assetid: 0dc03df1-b793-408f-af4c-c11188729abf
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 869b758e3ac922762c293eb8aa9a9537a4397bd6
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogvalidatepackage-ssisdb-database"></a>catalog.validate_package (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Valida de forma asincrónica un paquete del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
catalog.validate_package [ @folder_name = ] folder_name  
    , [ @project_name = ] project_name  
    , [ @package_name = ] package_name  
    , [ @validation_id = ] validation_id OUTPUT  
 [  , [ @use32bitruntime = ] use32bitruntime ]  
 [  , [ @target_environment = ] target_environment ]  
 [  , [ @reference_id = ] reference_id ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 El nombre de la carpeta que contiene el paquete. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project_name =] *Nombre_proyecto*  
 El nombre del proyecto que contiene el paquete. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @package_name =] *nombreDePaquete*  
 Nombre del paquete. El *nombreDePaquete* es **nvarchar (260)**.  
  
 [ @validation_id =] *validation_id*  
 Devuelve el identificador único (ID) de la validación. El *validation_id* es **bigint**.  
  
 [ @use32bitruntime =] *use32bitruntime*  
 Indica si el motor en tiempo de ejecución de 32 bits se debe usar para ejecutar el paquete en un sistema operativo de 64 bits. Utilice el valor de `1` para ejecutar el paquete con el tiempo de ejecución de 32 bits cuando se ejecuta en un sistema operativo de 64 bits. Use el valor `0` para ejecutar el paquete con el motor en tiempo de ejecución de 64 bits cuando se ejecute en un sistema operativo de 64 bits. Este parámetro es opcional. El *use32bitruntime* es **bits**.  
  
 [ @environment_scope =] *environment_scope*  
 Indica las referencias de entorno que la validación tiene en cuenta. Cuando el valor es `A`, todas las referencias de entorno asociadas con el proyecto se incluyen en la validación. Cuando el valor es `S`, solo se incluye una sola referencia de entorno. Cuando el valor es `D`, no se incluyen referencias de entorno y todos los parámetros deben tener un valor literal predeterminado para pasar la validación. Este parámetro es opcional. El carácter `D` se utiliza de forma predeterminada. El *environment_scope* es **char (1)**.  
  
 [ @reference_id =] *reference_id*  
 El identificador único de la referencia de entorno. Este parámetro es necesario únicamente cuando se incluye una sola referencia de entorno en la validación, cuando *environment_scope* es `S`. El *reference_id* es **bigint**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos de lectura en el objeto y, si es aplicable, permisos de lectura en los entornos a los que se hace referencia  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El nombre del proyecto o el nombre del paquete no son válidos  
  
-   El usuario no tiene los permisos adecuados  
  
-   Uno o varios de los entornos a los que se hace referencia incluidos en la validación no contienen variables a las que se haga referencia  
  
-   Se produce un error de validación del paquete  
  
-   El entorno al que se hace referencia no existe  
  
-   Las variables a las que se hace referencia no se pueden encontrar en los entornos a los que se hace referencia incluidos en la validación  
  
-   Se hace referencia a las variables de los parámetros del paquete, pero no se han incluido entornos a los que se haga referencia en la validación  
  
## <a name="remarks"></a>Comentarios  
 La validación ayuda a identificar los problemas que pueden impedir que el paquete se ejecuta correctamente. Use la [catalog.validations](../../integration-services/system-views/catalog-validations-ssisdb-database.md) o [catalog.operations](../../integration-services/system-views/catalog-operations-ssisdb-database.md) vistas para supervisar el estado de validación.  
  
  

