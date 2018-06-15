---
title: Sys.remote_service_bindings (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.remote_service_bindings_TSQL
- remote_service_bindings_TSQL
- remote_service_bindings
- sys.remote_service_bindings
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_service_bindings catalog view
ms.assetid: 4e1a885d-eed1-4993-9c87-e6fd781f437d
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b51b1ad09e3b1dd3252178e45934fafa46d4e688
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181521"
---
# <a name="sysremoteservicebindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por enlace de servicio remoto. 
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de este enlace de servicio remoto. No acepta valores NULL.|  
|**remote_service_binding_id**|**int**|Id. de este enlace de servicio remoto. No acepta valores NULL.|  
|**principal_id**|**int**|Id. de la entidad de seguridad de la base de datos propietaria de este enlace de servicio remoto. ACEPTA VALORES NULL.|  
|**remote_service_name**|**nvarchar(256)**|Nombre del servicio remoto al que se aplica este enlace. ACEPTA VALORES NULL.|  
|**service_contract_id**|**int**|Id. del contrato al que se aplica este enlace. El valor 0 es un comodín que significa que este enlace se aplica a todos los contratos del servicio. No acepta valores NULL.|  
|**remote_principal_id**|**int**|Id. del usuario especificado en el enlace de servicio remoto. Service Broker utiliza un certificado propiedad de este usuario para comunicarse con el servicio especificado en los contratos indicados. ACEPTA VALORES NULL.|  
|**is_anonymous_on**|**bit**|Este enlace de servicio remoto usa seguridad ANONYMOUS. La identidad del usuario que inicia la conversación no se proporciona al servicio de destino. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
