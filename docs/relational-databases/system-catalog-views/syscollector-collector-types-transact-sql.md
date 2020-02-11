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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124918"
---
# <a name="syscollector_collector_types-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información sobre un tipo de recopilador para un elemento de recopilación.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|GUID de un tipo de recopilador. No admite valores NULL.|  
|**Name**|**sysname**|Nombre del tipo de recopilador. No admite valores NULL.|  
|**parameter_schema**|**lenguaje**|Esquema XML que describe la apariencia de la configuración para el tipo de recopilador especificado. Este esquema XML se utiliza para validar la configuración XML real asociada con una instancia determinada del elemento de recopilación. Acepta valores NULL.|  
|**parameter_formatter**|**lenguaje**|Determina la plantilla que debe usarse para transformar el XML a fin de usarlo en la página de propiedades del conjunto de recopilación. Acepta valores NULL.|  
|**collection_package_id**|**uniqueidentifer**|GUID de un paquete de recopilación. No admite valores NULL.|  
|**collection_package_path**|**nvarchar(4000)**|Proporciona la ruta de acceso al paquete de recopilación. Acepta valores NULL.|  
|**collection_package_name**|**sysname**|Nombre del paquete de recopilación. No admite valores NULL.|  
|**upload_package_id**|**uniqueidentifer**|GUID del paquete de carga. No admite valores NULL.|  
|**upload_package_path**|**nvarchar(4000)**|Proporciona la ruta de acceso al paquete de carga. Acepta valores NULL.|  
|**upload_package_name**|**sysname**|Nombre del paquete de carga. No admite valores NULL.|  
|**is_system**|**bit**|Está activado (1) o desactivado (0) para indicar si el tipo de recopilador se envió con el recopilador de datos o si se agregó más tarde mediante el **dc_admin**. Éste podría ser un tipo personalizado desarrollado internamente o por terceros. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Requiere SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se actualizó **collection_type_uid** nombre de la columna a **collector_type_uid**.|  
|Se corrigió la descripción de la columna **parameter_schema** para indicar que el valor admite valores NULL.|  
|Se ha agregado la columna **parameter_formatter** .|  
|Se ha corregido el tipo de datos de la columna **collection_package_path** y se ha actualizado la descripción para indicar que el valor admite valores NULL.|  
|Se ha corregido el tipo de datos de la columna **upload_package_path** y se ha actualizado la descripción para indicar que el valor admite valores NULL.|  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
