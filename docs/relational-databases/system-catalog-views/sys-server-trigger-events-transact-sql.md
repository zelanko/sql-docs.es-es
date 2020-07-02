---
title: Sys. server_trigger_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_trigger_events_TSQL
- server_trigger_events_TSQL
- sys.server_trigger_events
- server_trigger_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_trigger_events catalog view
ms.assetid: be7d8a59-3c00-4f1b-b4b0-3dcd5572e002
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: da5fdbf9cded1ea58e3d1dc2ab29cea6df0e9693
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775220"
---
# <a name="sysserver_trigger_events-transact-sql"></a>sys.server_trigger_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila por cada evento para el que se activa un desencadenador de nivel de servidor (sincrónico).  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**columnas heredadas**||Hereda todas las columnas de [Sys. server_events](../../relational-databases/system-catalog-views/sys-server-events-transact-sql.md).|  
|**is_first**|**bit**|El desencadenador está marcado como el primero que se activará para este evento.|  
|**is_last**|**bit**|El desencadenador está marcado como el último que se activará para este evento.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
