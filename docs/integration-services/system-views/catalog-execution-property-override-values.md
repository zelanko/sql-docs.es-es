---
title: catalog.execution_property_override_values | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 138938f3ae015675c7815416dc2b17bcdc5988f4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los valores de invalidación de la propiedad que se establecieron durante la ejecución del paquete.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|Identificador único para el valor de invalidación de la propiedad.|  
|execution_id|**bigint**|Identificador único de la instancia de ejecución.|  
|property_path|**nvarchar(4000)**|Ruta de acceso a la propiedad en el paquete.|  
|property_value|**nvarchar(max)**|Valor invalidación de la propiedad.|  
|sensitive|**bit**|Cuando el valor es 1, la propiedad es confidencial y se cifra cuando se almacena. Cuando el valor es 0, la propiedad no es confidencial y el valor se almacena como texto simple.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada ejecución en la que los valores de propiedad se invalidan mediante la sección **Invalidaciones de propiedad** en la pestaña **Opciones avanzadas** del diálogo **Ejecutar paquete**. La ruta de acceso a la propiedad se deriva de la propiedad **Ruta de acceso del paquete** de la tarea del paquete.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
