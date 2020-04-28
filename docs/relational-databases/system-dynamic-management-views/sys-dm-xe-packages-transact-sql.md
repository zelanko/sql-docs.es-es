---
title: Sys. dm_xe_packages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 065625fdaca015de9c445e6e6f0e1ad0013f38e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68090257"
---
# <a name="sysdm_xe_packages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enumera todos los paquetes registrados con el motor de Extended Events.  
  
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|Nombre del paquete. La descripción se expone a partir del propio paquete. No admite valores NULL.|  
|guid|**uniqueidentifier**|GUID que identifica el paquete. No admite valores NULL.|  
|description|**nvarchar (a.**|Descripción del paquete. la descripción está establecida por el autor del paquete y no admite valores NULL.|  
|capabilities|**int**|Mapa de bits que describe la funcionalidad de este paquete. Acepta valores NULL.|  
|capabilities_desc|**nvarchar(256)**|Lista de toda la funcionalidad posible de este paquete. Acepta valores NULL.|  
|module_guid|**nvarchar(60)**|GUID del módulo que expone este paquete. No admite valores NULL.|  
|module_address|**varbinary(8**|La dirección base donde se carga el módulo que contiene el paquete. Un módulo único puede exponer varios paquetes. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="remarks"></a>Observaciones  
 Los paquetes registrados con el motor de Extended Events exponen eventos, acciones que se pueden realizar en el momento de la activación de los eventos, y destinos para el procesamiento sincrónico y asincrónico de datos de eventos.  
  
 Estos paquetes se pueden cargar dinámicamente en un espacio de direcciones del proceso. En el momento de cargarse el paquete, registra todos los objetos que expone con el motor de eventos extendidos.  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
||||  
|-|-|-|  
|De|En|Relación|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|Varios a uno|  
  
## <a name="see-also"></a>Consulte también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

