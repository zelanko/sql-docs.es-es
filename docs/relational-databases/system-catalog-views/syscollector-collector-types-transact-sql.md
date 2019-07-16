---
title: syscollector_collector_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1d232d602f2496fff03ed050a8faf11b53e718b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124918"
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información sobre un tipo de recopilador para un elemento de recopilación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|GUID de un tipo de recopilador. No admite valores NULL.|  
|**name**|**sysname**|Nombre del tipo de recopilador. No admite valores NULL.|  
|**parameter_schema**|**xml**|Esquema XML que describe la apariencia de la configuración para el tipo de recopilador especificado. Este esquema XML se utiliza para validar la configuración XML real asociada con una instancia determinada del elemento de recopilación. Acepta valores NULL.|  
|**parameter_formatter**|**xml**|Determina la plantilla que debe usarse para transformar el XML a fin de usarlo en la página de propiedades del conjunto de recopilación. Acepta valores NULL.|  
|**collection_package_id**|**uniqueidentifer**|GUID de un paquete de recopilación. No admite valores NULL.|  
|**collection_package_path**|**nvarchar(4000)**|Proporciona la ruta de acceso al paquete de recopilación. Acepta valores NULL.|  
|**collection_package_name**|**sysname**|Nombre del paquete de recopilación. No admite valores NULL.|  
|**upload_package_id**|**uniqueidentifer**|GUID del paquete de carga. No admite valores NULL.|  
|**upload_package_path**|**nvarchar(4000)**|Proporciona la ruta de acceso al paquete de carga. Acepta valores NULL.|  
|**upload_package_name**|**sysname**|Nombre del paquete de carga. No admite valores NULL.|  
|**is_system**|**bit**|Activado (1) u off (0) para indicar si el tipo de recopilador se distribuyó con el recopilador de datos o si se agregó más tarde por medio del **dc_admin**. Éste podría ser un tipo personalizado desarrollado internamente o por terceros. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Requiere SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Actualizar **collection_type_uid** nombre de columna para **collector_type_uid**.|  
|Se ha corregido la descripción para el **parameter_schema** columna para indicar que el valor que acepta valores NULL.|  
|Agrega el **parameter_formatter** columna.|  
|Se corrige el tipo de datos para el **collection_package_path** columna y se ha actualizado la descripción para indicar que el valor que acepta valores NULL.|  
|Se corrige el tipo de datos para el **upload_package_path** columna y se ha actualizado la descripción para indicar que el valor que acepta valores NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
