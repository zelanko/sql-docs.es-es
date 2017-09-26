---
title: Catalog.execution_parameter_values (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 60907a82f3d0bb9f273355fd6bfbd7378ce72c9f
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionparametervalues-ssisdb-database"></a>catalog.execution_parameter_values (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los valores de parámetro reales utilizados por los paquetes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante una instancia de ejecución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|Identificador único (ID) del parámetro de ejecución.|  
|execution_id|**bigint**|Identificador único para la instancia de ejecución.|  
|object_type|**smallint**|Cuando el valor es `20`, el valor del parámetro es un parámetro de proyecto. Cuando el valor es `30`, el valor del parámetro es un parámetro de paquete. Cuando el valor es `50`, el parámetro es uno de los siguientes:<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SINCRONIZADA**|  
|parameter_data_type|**nvarchar (128)**|El tipo de datos del parámetro.|  
|parameter_name|**sysname**|Nombre del parámetro.|  
|parameter_value|**sql_variant**|El valor del parámetro. Cuando confidencial es `0`, se muestra el valor de texto simple. Cuando confidencial es `1`, **NULL** se muestra el valor.|  
|sensitive|**bit**|Cuando el valor es `1`, el valor del parámetro es confidencial. Cuando el valor es `0`, el valor del parámetro no es confidencial.|  
|required|**bit**|Cuando el valor es `1`, se requiere el valor del parámetro para iniciar la ejecución. Cuando el valor es `0`, no se requiere el valor del parámetro para iniciar la ejecución.|  
|value_set|**bit**|Cuando el valor es `1`, el valor del parámetro se ha asignado. Cuando el valor es `0`, el valor del parámetro no se ha asignado.|  
|runtime_override|**bit**|Si el valor es `1`, el valor original del parámetro se modificó antes de que se iniciara la ejecución. Si el valor es `0`, el valor del parámetro es el valor original que se estableció.|  
  
## <a name="remarks"></a>Comentarios  
 En esta vista se muestra una fila para cada parámetro de ejecución del catálogo. Un valor de parámetro de ejecución es el valor asignado a un parámetro de proyecto o un parámetro del paquete durante una única instancia de ejecución.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
