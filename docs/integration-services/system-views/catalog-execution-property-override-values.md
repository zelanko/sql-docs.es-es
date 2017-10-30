---
title: Catalog.execution_property_override_values | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ed9ae4ea7a7165efe53a551832d8e4a0eb7a2114
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los valores de invalidación de la propiedad que se establecieron durante la ejecución del paquete.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|Identificador único para el valor de invalidación de la propiedad.|  
|execution_id|**bigint**|Identificador único para la instancia de ejecución.|  
|property_path|**nvarchar(4000)**|Ruta de acceso a la propiedad en el paquete.|  
|property_value|**nvarchar(max)**|Valor invalidación de la propiedad.|  
|sensitive|**bit**|Cuando el valor es 1, la propiedad es confidencial y se cifra cuando se almacena. Cuando el valor es 0, la propiedad no es confidencial y el valor se almacena como texto simple.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada ejecución en la propiedad que se invalidan los valores mediante la **invalidaciones de propiedad** sección la **avanzadas** pestaña de la **Ejecutar paquete** cuadro de diálogo. La ruta de acceso a la propiedad se deriva de la **ruta de acceso del paquete** propiedad de la tarea de paquete.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  

