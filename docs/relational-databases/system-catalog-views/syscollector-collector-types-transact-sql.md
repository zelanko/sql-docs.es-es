---
title: syscollector_collector_types (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9c56b03d902a329e47496b81d4f16e7f35f4bd39
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información sobre un tipo de recopilador para un elemento de recopilación.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifier**|GUID de un tipo de recopilador. No admite valores NULL.|  
|**Nombre**|**sysname**|Nombre del tipo de recopilador. No admite valores NULL.|  
|**parameter_schema**|**xml**|Esquema XML que describe la apariencia de la configuración para el tipo de recopilador especificado. Este esquema XML se utiliza para validar la configuración XML real asociada con una instancia determinada del elemento de recopilación. Acepta valores NULL.|  
|**parameter_formatter**|**xml**|Determina la plantilla que debe usarse para transformar el XML a fin de usarlo en la página de propiedades del conjunto de recopilación. Acepta valores NULL.|  
|**collection_package_id**|**uniqueidentifier**|GUID de un paquete de recopilación. No admite valores NULL.|  
|**collection_package_path**|**nvarchar(4000)**|Proporciona la ruta de acceso al paquete de recopilación. Acepta valores NULL.|  
|**collection_package_name**|**sysname**|Nombre del paquete de recopilación. No admite valores NULL.|  
|**upload_package_id**|**uniqueidentifier**|GUID del paquete de carga. No admite valores NULL.|  
|**upload_package_path**|**nvarchar(4000)**|Proporciona la ruta de acceso al paquete de carga. Acepta valores NULL.|  
|**upload_package_name**|**sysname**|Nombre del paquete de carga. No admite valores NULL.|  
|**is_system**|**bit**|Activado (1) u off (0) para indicar si el tipo de recopilador se distribuyó con el recopilador de datos o si se agregó más tarde por medio del **dc_admin**. Éste podría ser un tipo personalizado desarrollado internamente o por terceros. No admite valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 Requiere SELECT para **dc_operator**, **dc_proxy**.  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Actualizar **collection_type_uid** nombre de columna para **collector_type_uid**.|  
|Se ha corregido la descripción de la **parameter_schema** columna para indicar que el valor que aceptan valores NULL.|  
|Agrega el **parameter_formatter** columna.|  
|Se ha corregido el tipo de datos para la **collection_package_path** columna y se actualiza la descripción para indicar que el valor que aceptan valores NULL.|  
|Se ha corregido el tipo de datos para la **upload_package_path** columna y se actualiza la descripción para indicar que el valor que aceptan valores NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
