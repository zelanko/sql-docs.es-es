---
title: dbo.sysdac_instances (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 813a786f68fe02431073033172d37ffe2c682ee0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="data-tier-application-views---dbosysdacinstances"></a>Vistas de aplicación de capa de datos - dbo.sysdac_instances
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Muestra una fila para cada instancia de aplicación de capa de datos (DAC) implementada en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. sysdac_instances pertenece al esquema dbo en la base de datos msdb. En la tabla siguiente se describe las columnas en la vista sysdac_instances.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Identificador de la instancia de DAC.|  
|nombre_instancia|**sysname**|Nombre de la instancia de DAC especificada cuando se implementó la DAC.|  
|type_name|**sysname**|Nombre de la DAC especificada cuando se creó el paquete DAC.|  
|type_version|**nvarchar(64)**|Versión de la DAC especificada cuando se creó el paquete DAC.|  
|description|**nvarchar(4000)**|Descripción de la DAC escrita cuando se creó el paquete DAC.|  
|type_stream|**varbinary(max)**|Flujo de bits que contiene una representación codificada de los objetos lógicos, como tablas y vistas, que contiene la DAC.|  
|date_created|**datetime**|Fecha y hora en que se creó la instancia de DAC.|  
|created_by|**sysname**|Inicio de sesión que creó la instancia DAC.|  
|database_name|**sysname**|Nombre de la base de datos creada para la instancia de DAC.|  
  
## <a name="remarks"></a>Comentarios  
 Una DAC incluye un tipo de DAC, que es una definición de los objetos de capa de datos lógicos utilizados por una aplicación, como las tablas y las vistas. Un paquete DAC es un archivo que se utiliza para implementar una DAC. El paquete DAC contiene una representación de todos los objetos lógicos contenidos en el tipo de DAC. El paquete DAC se puede utilizar para implementar una o más copias, o instancias, de la DAC en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cada instancia de DAC implementada a partir del mismo paquete DAC comparte el mismo tipo, pero tiene asignado un identificador y un nombre de instancia únicos.  
  
## <a name="permissions"></a>Permissions  
 Se requiere la pertenencia al rol fijo de servidor sysadmin para ver todas las columnas. Los miembros del rol público pueden ver las columnas instance_name, description y type_version.  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Vistas de aplicación de capa de datos &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)  
  
  
