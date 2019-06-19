---
title: catalog.get_parameter_values (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 391a47edc45145bac21ce351e36c613f2a76addd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65716102"
---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta que contiene el proyecto. *folder_name* es **nvarchar(128)** .  
  
 [ @project_name = ] *project_name*  
 Nombre del proyecto donde los parámetros residen. *project_name* es **nvarchar(128)** .  
  
 [ @package_name = ] *package_name*  
 Nombre del paquete. Especifique el nombre del paquete para recuperar todos los parámetros de proyecto y los parámetros de un paquete concreto. Utilice NULL para recuperar todos los parámetros de proyecto y los parámetros de todos los paquetes. El parámetro *package_name* es de tipo **nvarchar(260)** .  
  
 [ @reference_id = ] *reference_id*  
 Identificador único de una referencia de entorno. Este parámetro es opcional. *reference_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve una tabla que tiene el siguiente formato:  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Tipo de parámetro. El valor es `20` para un parámetro de proyecto y `30` para un parámetro de paquete.|  
|parameter_data_type|**nvarchar(128)**|El tipo de datos del parámetro.|  
|parameter_name|**sysname**|Nombre del parámetro.|  
|parameter_value|**sql_variant**|El valor del parámetro.|  
|sensitive|**bit**|Cuando el valor es `1`, el valor del parámetro es confidencial. Cuando el valor es `0`, el valor del parámetro no es confidencial.|  
|required|**bit**|Cuando el valor es `1`, se requiere el valor del parámetro para iniciar la ejecución. Cuando el valor es `0`, no se requiere el valor del parámetro para iniciar la ejecución.|  
|value_set|**bit**|Cuando el valor es `1`, el valor del parámetro se ha asignado. Cuando el valor es `0`, el valor del parámetro no se ha asignado.|  
  
> [!NOTE]  
>  Los valores literales se muestran en texto simple. **NULL** se muestra en lugar de los valores confidenciales.  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos de lectura en el objeto y, si es aplicable, el permiso de lectura en el entorno al que se hace referencia  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   El paquete no se puede encontrar en la carpeta o proyecto especificados  
  
-   El usuario no tiene los permisos adecuados.  
  
-   La referencia del entorno especificado no existe  
  
  
