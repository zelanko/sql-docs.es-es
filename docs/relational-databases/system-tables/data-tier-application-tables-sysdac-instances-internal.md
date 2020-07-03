---
title: sysdac_instances_internal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 98b33a43eeb52ca99c50235e5c3865c79cd92125
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890562"
---
# <a name="data-tier-application-tables---sysdac_instances_internal"></a>Tablas de aplicación de capa de datos: sysdac_instances_internal
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Muestra una fila para cada instancia de aplicación de capa de datos (DAC) implementada en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Esta tabla se almacena en el esquema DBO de la base de datos msdb.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Identificador de la instancia de DAC.|  
|nombre_instancia|**sysname**|Nombre de la instancia de DAC especificada cuando se implementó la instancia.|  
|type_name|**sysname**|Nombre de la DAC especificada cuando se creó el paquete DAC.|  
|type_version|**nvarchar (64)**|Versión de la DAC especificada cuando se creó el paquete DAC.|  
|description|**nvarchar(4000)**|Descripción de la DAC escrita cuando se creó el paquete DAC.|  
|type_stream|**varbinary(max)**|Flujo de bits que contiene la representación codificada de los objetos lógicos, como tablas y vistas, contenidos en la DAC.|  
|date_created|**datetime**|Fecha y hora en que se creó la instancia de DAC.|  
|created_by|**sysname**|Inicio de sesión que creó la instancia de DAC.|  
  
## <a name="remarks"></a>Comentarios  
 El acceso de solo lectura a esta vista está disponible para todos los usuarios con permisos para conectarse a la base de datos maestra.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor sysadmin.  
  
## <a name="see-also"></a>Consulte también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
