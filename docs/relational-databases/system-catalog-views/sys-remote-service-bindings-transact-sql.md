---
title: Sys. remote_service_bindings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 76ef28d83fca3fd0eb904f0d98b798866b9715eb
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896482"
---
# <a name="sysremote_service_bindings-transact-sql"></a>sys.remote_service_bindings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta vista de catálogo contiene una fila por enlace de servicio remoto. 
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de este enlace de servicio remoto. No acepta valores NULL.|  
|**remote_service_binding_id**|**int**|Id. de este enlace de servicio remoto. No acepta valores NULL.|  
|**principal_id**|**int**|Id. de la entidad de seguridad de la base de datos propietaria de este enlace de servicio remoto. Acepta valores NULL.|  
|**remote_service_name**|**nvarchar(256)**|Nombre del servicio remoto al que se aplica este enlace. Acepta valores NULL.|  
|**service_contract_id**|**int**|Id. del contrato al que se aplica este enlace. El valor 0 es un comodín que significa que este enlace se aplica a todos los contratos del servicio. No acepta valores NULL.|  
|**remote_principal_id**|**int**|Id. del usuario especificado en el enlace de servicio remoto. Service Broker utiliza un certificado propiedad de este usuario para comunicarse con el servicio especificado en los contratos indicados. Acepta valores NULL.|  
|**is_anonymous_on**|**bit**|Este enlace de servicio remoto usa seguridad ANONYMOUS. La identidad del usuario que inicia la conversación no se proporciona al servicio de destino. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
