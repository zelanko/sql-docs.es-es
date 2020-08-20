---
description: sys.service_message_types (Transact-SQL)
title: Sys. service_message_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b56665ff1a780cdcf8052c063f817b542e65ac3c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455188"
---
# <a name="sysservice_message_types-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta vista de catálogo contiene una fila por cada tipo de mensaje registrado en Service Broker.
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del tipo de mensaje, único en la base de datos. No acepta valores NULL.|  
|**message_type_id**|**int**|Identificador del tipo de mensaje, único en la base de datos. No acepta valores NULL.|  
|**principal_id**|**int**|Identificador de la entidad de seguridad de base de datos propietaria de este tipo de mensaje. Acepta valores NULL.|  
|**valida**|**char(2)**|Validación realizada por Broker antes de enviar mensajes de este tipo. No acepta valores NULL. Uno de los valores siguientes:<br /><br /> N = Ninguno<br /><br /> X = XML<br /><br /> E = Vacío|  
|**validation_desc**|**nvarchar(60)**|Descripción de la validación realizada por Broker antes de enviar mensajes de este tipo. Acepta valores NULL. Uno de los valores siguientes:<br /><br /> Ninguno<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|En una validación que usa un esquema XML, es el identificador de la colección de esquemas utilizado.<br /><br /> En caso contrario, NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
