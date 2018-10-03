---
title: Sys.dm_os_loaded_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_loaded_modules
- dm_os_loaded_modules
- sys.dm_os_loaded_modules_TSQL
- dm_os_loaded_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_loaded_modules dynamic management view
ms.assetid: 56c7743a-b568-4943-bd3b-73c57d9d641c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3967e3f8548a7b8ef804d054cf746243a8fb5b96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794323"
---
# <a name="sysdmosloadedmodules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada módulo cargado en el espacio de direcciones del servidor.  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_loaded_modules**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary (8)**|Dirección del módulo en proceso.|  
|**file_version**|**varchar(23)**|Versión del archivo. Aparece en el siguiente formato:<br /><br /> x.x:x.x|  
|**product_version**|**varchar(23)**|Versión del producto. Aparece en el siguiente formato:<br /><br /> x.x:x.x|  
|**Depurar**|**bit**|1 = El módulo es una versión de depuración del módulo cargado.|  
|**revisado**|**bit**|1 = El módulo se ha revisado.|  
|**versión preliminar**|**bit**|1 = El módulo es una versión preliminar del módulo cargado.|  
|**private_build**|**bit**|1 = El módulo es una versión privada del módulo cargado.|  
|**special_build**|**bit**|1 = El módulo es una versión especial del módulo cargado.|  
|**Idioma**|**int**|Información del idioma de la versión del módulo.|  
|**Empresa**|**nvarchar(256)**|Nombre de la compañía que ha creado el módulo.|  
|**Descripción**|**nvarchar(256)**|Descripción del módulo.|  
|**Nombre**|**nvarchar(255)**|Nombre del módulo. Incluye la ruta de acceso completa del módulo.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
