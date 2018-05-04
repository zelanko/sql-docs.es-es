---
title: Sys.dm_xe_object_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_object_columns
- sys.dm_xe_object_columns_TSQL
- dm_xe_object_columns_TSQL
- dm_xe_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_object_columns dynamic management view
- extended events [SQL Server], views
ms.assetid: d96a14f3-4284-45ff-b1fe-4858e540a013
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5810e57f4529ef417f46ab88d97b86a964e2e6f5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmxeobjectcolumns-transact-sql"></a>sys.dm_xe_object_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la información del esquema para todos los objetos.  
  
> [!NOTE]  
>  Los objetos de eventos ofrecen esquemas fijos para los datos de solo lectura y de escritura.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|Nombre de la columna. nombre es único dentro del objeto. No admite valores NULL.|  
|column_id|**int**|El identificador de la columna. column_id es único dentro del objeto cuando se utiliza con column_type. No admite valores NULL.|  
|object_name|**nvarchar(60)**|Nombre del objeto al que pertenece esta columna. Hay una relación de varios a uno con sys.dm_xe_objects.id. No admite valores NULL.|  
|object_package_guid|**uniqueidentifier**|GUID del paquete que contiene el objeto. No admite valores NULL.|  
|type_name|**nvarchar(60)**|Nombre del tipo de esta columna. No admite valores NULL.|  
|type_package_guid|**uniqueidentifier**|GUID del paquete que contiene el tipo de datos de la columna. No admite valores NULL.|  
|column_type|**nvarchar(60)**|Indica cómo se utiliza esta columna. No admite valores NULL. COLUMN_TYPE puede ser uno de los siguientes:<br /><br /> readonly. La columna contiene un valor estático que no se puede cambiar.<br /><br /> data. La columna contiene datos en tiempo de ejecución expuestos por el objeto.<br /><br /> customizable. La columna contiene un valor que puede cambiarse.<br /><br /> Nota: Si cambia este valor puede modificar el comportamiento del objeto.|  
|column_value|**nvarchar(256)**|Muestra los valores estáticos asociados con la columna de objetos. Acepta valores NULL.|  
|capabilities|**int**|Un mapa de bits que describe las capacidades de la columna. Acepta valores NULL.|  
|capabilities_desc|**nvarchar(256)**|Una descripción de las capacidades de esta columna de objetos. Este valor puede ser uno de los siguientes:<br /><br /> Mandatory. Se debe establecer el valor al enlazar el objeto primario a una sesión de eventos.<br /><br /> NULL|  
|description|**nvarchar(256)**|Descripción de esta columna de objetos. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|sys.dm_xe_object_columns.object_name, sys.dm_xe_object_columns.object_package_guid|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_objects.package_guid|Varios a uno|  
|sys.dm_xe_object_columns.type_name<br /><br /> sys.dm_xe_object_columns.type_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

