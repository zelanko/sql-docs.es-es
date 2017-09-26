---
title: Catalog.set_object_parameter_value (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9c27cff7ad828ab5c19183febd2ad562d5c9b925
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el valor de un parámetro del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Asocia el valor a una variable de entorno o asigna un valor literal que se va a usar como valor predeterminado si no se asignan otros valores.  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
set_object_parameter_value [ @object_type = ] object_type   
    , [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @parameter_name = ] parameter _name   
    , [ @parameter_value = ] parameter_value   
 [  , [ @object_name = ] object_name ]  
 [  , [ @value_type = ] value_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @object_type =] *object_type*  
 El tipo del parámetro. Use el valor `20` para indicar un parámetro de proyecto o el valor `30` para indicar un parámetro de paquete. El *object_type* es **smallInt**.  
  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contiene el parámetro. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project_name =] *Nombre_proyecto*  
 Nombre del proyecto que contiene el parámetro. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @parameter_name =] *parameter_name*  
 Nombre del parámetro. El *parameter_name* es **nvarchar (128)**.  
  
 [ @parameter_value =] *parameter_value*  
 El valor del parámetro. El *parameter_value* es **sql_variant**.  
  
 [ @object_name =] *object_name*  
 Nombre del paquete. Este argumento es necesario cuando el parámetro es un parámetro de paquete. El *object_name* es **nvarchar (260)**.  
  
 [ @value_type =] *value_type*  
 Tipo de valor del parámetro. Use el carácter `V` para indicar que *parameter_value* es un valor literal que se usará de forma predeterminada no hay otros valores se asignan antes de la ejecución. Use el carácter `R` para indicar que *parameter_value* es un valor que se hace referencia y se ha establecido en el nombre de una variable de entorno. Este argumento es opcional; de forma predeterminada, se usa el carácter `V`. El *value_type* es **char (1)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen algunas condiciones que pueden hacer que el procedimiento almacenado produzca un error:  
  
-   El tipo de parámetro no es válido  
  
-   El nombre de proyecto no es válido  
  
-   En los parámetros de paquete, el nombre del paquete no es válido  
  
-   El tipo de valor no es válido.  
  
-   El usuario no tiene los permisos adecuados  
  
## <a name="remarks"></a>Comentarios  
  
-   Si no hay ningún *value_type* se especifica, un valor literal para *parameter_value* se utiliza de forma predeterminada. Cuando se utiliza un valor literal, el *value_set* en el [object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) ver se estableció como `1`. No se permiten valores de parámetro NULL.  
  
-   Si *value_type* contiene el carácter `R`, que indica un valor que se hace referencia, *parameter_value* hace referencia al nombre de una variable de entorno.  
  
-   El valor `20` puede utilizarse para *object_type* para indicar un parámetro de proyecto. En este caso, un valor para *object_name* no es necesario y los valores especificados para *object_name* se omite. Este valor se usa cuando el usuario desea establecer un parámetro de proyecto.  
  
-   El valor `30` puede utilizarse para *object_type* para indicar un parámetro de paquete. En este caso, un valor para *object_name* se utiliza para denotar el paquete correspondiente. Si *object_name* no se especifica, el procedimiento almacenado devuelve un error y finaliza.  
  
  
