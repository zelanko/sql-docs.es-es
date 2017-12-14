---
title: catalog.set_object_parameter_value (base de datos de SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: fb887543-f92f-404d-9495-a1dd23a6716e
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fe142dd0fdf6e896c6930528b563514c3aa2fb8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogsetobjectparametervalue-ssisdb-database"></a>catalog.set_object_parameter_value (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Establece el valor de un parámetro del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Asocia el valor a una variable de entorno o asigna un valor literal que se va a usar como valor predeterminado si no se asignan otros valores.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.set_object_parameter_value [@object_type =] object_type   
    , [@folder_name =] folder_name   
    , [@project_name =] project_name   
    , [@parameter_name =] parameter _name   
    , [@parameter_value =] parameter_value   
 [  , [@object_name =] object_name ]  
 [  , [@value_type =] value_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [@object_type =] *object_type*  
 Es el tipo de parámetro. Use el valor `20` para indicar un parámetro de proyecto o el valor `30` para indicar un parámetro de paquete. El parámetro *object_type* es **smallInt**.  
  
 [@folder_name =] *folder_name*  
 Nombre de la carpeta que contiene el parámetro. El parámetro *folder_name* es **nvarchar(128)**.  
  
 [@project_name =] *project_name*  
 Nombre del proyecto que contiene el parámetro. El parámetro *project_name* es **nvarchar(128)**.  
  
 [@parameter_name =] *parameter_name*  
 Nombre del parámetro. El parámetro *parameter_name* es **nvarchar(128)**.  
  
 [@parameter_value =] *parameter_value*  
 El valor del parámetro. El parámetro *parameter_value* es **sql_variant**.  
  
 [@object_name =] *object_name*  
 Nombre del paquete. Este argumento es necesario cuando el parámetro es un parámetro de paquete. El parámetro *object_name* es **nvarchar(260)**.  
  
 [@value_type =] *value_type*  
 Tipo de valor del parámetro. Use el carácter `V` para indicar que *parameter_value* es un valor literal que se usa de forma predeterminada cuando no hay otros valores asignados antes de la ejecución. Use el carácter `R` para indicar que *parameter_value* es un valor al que se hace referencia y que se ha establecido en el nombre de una variable de entorno. Este argumento es opcional; de forma predeterminada, se usa el carácter `V`. El parámetro *value_type* es **char(1)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (Correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos READ y MODIFY en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen algunas condiciones que pueden hacer que el procedimiento almacenado produzca un error:  
  
-   El tipo de parámetro no es válido  
  
-   El nombre de proyecto no es válido  
  
-   En los parámetros de paquete, el nombre del paquete no es válido  
  
-   El tipo de valor no es válido.  
  
-   El usuario no tiene los permisos adecuados  
  
## <a name="remarks"></a>Comentarios  
  
-   Si no se especifica ningún parámetro *value_type*, se usa un valor literal de *parameter_value* de forma predeterminada. Cuando se usa un valor literal, el parámetro*value_set* de la vista [object_parameters](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) se establece en `1`. No se permiten valores de parámetro NULL.  
  
-   Si *value_type* contiene el carácter `R` (el cual denota un valor de referencia), el parámetro *parameter_value* hace referencia al nombre de una variable de entorno.  
  
-   El valor `20` se puede usar para que *object_type* denote un parámetro de proyecto. En este caso, el valor de *object_name* no es necesario y cualquier valor especificado para *object_name* se omite. Este valor se usa cuando el usuario desea establecer un parámetro de proyecto.  
  
-   El valor `30` se puede usar para que *object_type* denote un parámetro de paquete. En este caso, se usa un valor de *object_name* para denotar el paquete correspondiente. Si no se especifica *object_name*, el procedimiento almacenado devuelve un error y finaliza.  
  
  
