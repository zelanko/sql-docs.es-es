---
title: Catalog.object_parameters (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9d538e5b55ef4e8880afb2d008b11c17d9a03189
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los parámetros para todos los paquetes y proyectos en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|Identificador (id.) único del parámetro.|  
|identificador de proyecto|**bigint**|Identificador único del proyecto.|  
|object_type|**smallint**|El tipo del parámetro. El valor es `20` para un parámetro de proyecto y `30` para un parámetro de paquete.|  
|object_name|**sysname**|Nombre del proyecto o paquete correspondiente.|  
|parameter_name|**sysname(nvarchar(128))**|Nombre del parámetro.|  
|data_type|**nvarchar (128)**|El tipo de datos del parámetro.|  
|required|**bit**|Cuando el valor es `1`, se requiere el valor del parámetro para iniciar la ejecución. Cuando el valor es `0`, no se requiere el valor del parámetro para iniciar la ejecución.|  
|sensitive|**bit**|Cuando el valor es `1`, el valor del parámetro es confidencial. Cuando el valor es `0`, el valor del parámetro no es confidencial.|  
|description|**nvarchar (1024)**|Una descripción opcional del paquete.|  
|design_default_value|**sql_variant**|Valor predeterminado para el parámetro que se asignó durante el diseño del proyecto o paquete.|  
|default_value|**sql_variant**|Valor predeterminado que se utiliza actualmente en el servidor.|  
|value_type|**Char (1)**|Indica el tipo de valor del parámetro. Este campo muestra `V` cuando parameter_value es un valor literal y `R` cuando se asigna el valor haciendo referencia a una variable de entorno.|  
|value_set|**bit**|Cuando el valor es `1`, el valor del parámetro se ha asignado. Cuando el valor es `0`, el valor del parámetro no se ha asignado.|  
|referenced_variable_name|**nvarchar (128)**|Nombre de la variable de entorno que se asigna al valor del parámetro. El valor predeterminado es **NULL**.|  
|validation_status|**Char (1)**|Solamente se identifica con fines informativos. No se usa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|last_validation_time|**DateTimeOffset(7)**|Solamente se identifica con fines informativos. No se usa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="permissions"></a>Permissions  
 Para ver las filas en esta vista, debe tener uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   Pertenencia en el **sysadmin** rol de servidor.  
  
 Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  

