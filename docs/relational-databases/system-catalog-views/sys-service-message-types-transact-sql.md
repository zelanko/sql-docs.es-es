---
title: sys.service_message_types (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 560ee8a4ccc03f747df2b475394af092db589e7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078741"
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por cada tipo de mensaje registrado en Service Broker.
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del tipo de mensaje, único en la base de datos. No acepta valores NULL.|  
|**message_type_id**|**int**|Identificador del tipo de mensaje, único en la base de datos. No acepta valores NULL.|  
|**principal_id**|**int**|Identificador de la entidad de seguridad de base de datos propietaria de este tipo de mensaje. QUE ACEPTA VALORES NULL.|  
|**validation**|**char(2)**|Validación realizada por Broker antes de enviar mensajes de este tipo. No acepta valores NULL. Una de las siguientes opciones:<br /><br /> N = Ninguno<br /><br /> X = XML<br /><br /> E = Vacío|  
|**validation_desc**|**nvarchar(60)**|Descripción de la validación realizada por Broker antes de enviar mensajes de este tipo. QUE ACEPTA VALORES NULL. Una de las siguientes opciones:<br /><br /> Ninguno<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|En una validación que usa un esquema XML, es el identificador de la colección de esquemas utilizado.<br /><br /> En caso contrario, NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
