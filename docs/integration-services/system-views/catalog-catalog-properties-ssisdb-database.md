---
title: Catalog.catalog_properties (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca3d5da05126d5b71bf6d714f9e8449f9f5c8335
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties (base de datos SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las propiedades del catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Nombre de la propiedad de catálogo.|  
|property_value|**nvarchar(256)**|Valor de la propiedad de catálogo.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada propiedad de catálogo. Las propiedades mostradas en esta vista incluyen lo siguiente:  
  
|Nombre de propiedad|Description|  
|-------------------|-----------------|  
|**ENCRYPTION_ALGORITHM**|El tipo de algoritmo de cifrado que se utiliza para cifrar los datos confidenciales. Entre los valores compatibles se incluyen: `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192` y `AES_256`. Nota: para modificar esta propiedad la base de datos de catálogo debe estar en modo de usuario único.|  
|**MAX_PROJECT_VERSIONS**|El número de nuevas versiones del proyecto que se retendrán para un proyecto único. Si está habilitada la limpieza de versiones, se eliminarán las versiones anteriores que superen este número.|  
|**OPERATION_CLEANUP_ENABLED**|Cuando el valor es `TRUE`, detalles de la operación y los mensajes de operación anteriores a **RETENTION_WINDOW** (días) se eliminan desde el catálogo. Si el valor es `FALSE`, se almacenarán todos los detalles y los mensajes de la operación en el catálogo. Nota: un trabajo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza la limpieza de operaciones.|  
|**RETENTION_WINDOW**|Número de días que los detalles y los mensajes de la operación estarán almacenados en el catálogo. Si el valor es `-1`, la ventana de retención es infinita. Nota: Si no se desea ninguna limpieza, establezca **OPERATION_CLEANUP_ENABLED** a **FALSE**.|  
|**VALIDATION_TIMEOUT**|Se detendrán las validaciones si no se completan en el número de segundos especificado por esta propiedad.|  
|**VERSION_CLEANUP_ENABLED**|Cuando el valor es `TRUE`, solo el **MAX_PROJECT_VERSIONS** número de versiones del proyecto se almacenan en el catálogo y se eliminan todas las demás versiones del proyecto. Cuando el valor es **FALSE**, todas las versiones del proyecto se almacenan en el catálogo. Nota: un trabajo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza la limpieza de operaciones.|  
|**SERVER_LOGGING_LEVEL**|Nivel de registro predeterminado del servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
  

