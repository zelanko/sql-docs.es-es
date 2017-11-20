---
title: Catalog.get_parameter_values (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4ad8f0c367e38581db696d2aa32afd5b92d635d2
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Resuelve y recupera los valores de los parámetros predeterminados de un proyecto y los paquetes correspondientes en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta que contiene el proyecto. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project_name =] *Nombre_proyecto*  
 Nombre del proyecto donde los parámetros residen. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @package_name =] *nombreDePaquete*  
 Nombre del paquete. Especifique el nombre del paquete para recuperar todos los parámetros de proyecto y los parámetros de un paquete concreto. Utilice NULL para recuperar todos los parámetros de proyecto y los parámetros de todos los paquetes. El *nombreDePaquete* es **nvarchar (260)**.  
  
 [ @reference_id =] *reference_id*  
 Identificador único de una referencia de entorno. Este parámetro es opcional. El *reference_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve una tabla que tiene el siguiente formato:  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|El tipo del parámetro. El valor es `20` para un parámetro de proyecto y `30` para un parámetro de paquete.|  
|parameter_data_type|**nvarchar (128)**|El tipo de datos del parámetro.|  
|parameter_name|**sysname**|Nombre del parámetro.|  
|parameter_value|**sql_variant**|El valor del parámetro.|  
|sensitive|**bit**|Cuando el valor es `1`, el valor del parámetro es confidencial. Cuando el valor es `0`, el valor del parámetro no es confidencial.|  
|required|**bit**|Cuando el valor es `1`, se requiere el valor del parámetro para iniciar la ejecución. Cuando el valor es `0`, no se requiere el valor del parámetro para iniciar la ejecución.|  
|value_set|**bit**|Cuando el valor es `1`, el valor del parámetro se ha asignado. Cuando el valor es `0`, el valor del parámetro no se ha asignado.|  
  
> [!NOTE]  
>  Los valores literales se muestran en texto simple. **NULL** se muestra en lugar de los valores confidenciales.  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos de lectura en el objeto y, si es aplicable, el permiso de lectura en el entorno al que se hace referencia  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El paquete no se puede encontrar en la carpeta o proyecto especificados  
  
-   El usuario no tiene los permisos adecuados  
  
-   La referencia del entorno especificado no existe  
  
  

