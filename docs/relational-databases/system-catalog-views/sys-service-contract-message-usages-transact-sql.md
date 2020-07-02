---
title: Sys. service_contract_message_usages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a8c60eca5c6306703f2ffd0ca7428422d8827851
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85664516"
---
# <a name="sysservice_contract_message_usages-transact-sql"></a>sys.service_contract_message_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Esta vista de catálogo contiene una fila por cada par (contrato, tipo de mensaje).  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|Id. del contrato utilizado por el tipo de mensaje. No acepta valores NULL.|  
|**message_type_id**|**int**|Id. del tipo de mensaje utilizado por el contrato. No acepta valores NULL.|  
|**is_sent_by_initiator**|**bit**|Iniciador de la conversación puede enviar este tipo de mensaje. No acepta valores NULL.|  
|**is_sent_by_target**|**bit**|Destino de la conversación puede enviar este tipo de mensaje. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
