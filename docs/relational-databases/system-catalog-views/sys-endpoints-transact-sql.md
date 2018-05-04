---
title: Sys.Endpoints (Transact-SQL) | Documentos de Microsoft
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
- endpoints
- sys.endpoints
- endpoints_TSQL
- sys.endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoints catalog view
ms.assetid: e6dafa4e-e47e-43ec-acfc-88c0af53c1a1
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f29e73c661e38a8b359bda37955e825c09e2d4d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por extremo que se crea en el sistema. En todo momento hay exactamente un extremo SYSTEM.  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del extremo. Es único en el servidor. No admite valores NULL.|  
|**endpoint_id**|**int**|Id. del extremo. Es único en el servidor. Un extremo con un identificador inferior a 65536 es un extremo del sistema. No admite valores NULL.|  
|**principal_id**|**int**|Id. de la entidad de seguridad del servidor que creó y es propietaria de este extremo. Acepta valores NULL.|  
|**Protocolo**|**tinyint**|Protocolo del extremo.<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = Canalizaciones con nombre<br /><br /> 4 = Memoria compartida<br /><br /> 5 = Adaptador de interfaz virtual (VIA)<br /><br /> No admite valores NULL.|  
|**protocol_desc**|**nvarchar(60)**|Descripción del protocolo del extremo. ACEPTA VALORES NULL. Los valores pueden ser los siguientes:<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **A través de** Nota: el protocolo VIA está en desuso. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**Tipo**|**tinyint**|Tipo de carga del extremo.<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> No admite valores NULL.|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de carga del extremo. Acepta valores NULL. Los valores pueden ser los siguientes:<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**state**|**tinyint**|Estado del extremo.<br /><br /> 0 = INICIADO, escucha y procesa solicitudes.<br /><br /> 1 = DETENIDO, escucha pero no procesa solicitudes.<br /><br /> 2 = DESHABILITADO, no escucha.<br /><br /> El estado predeterminado es 1. Acepta valores NULL.|  
|**state_desc**|**nvarchar(60)**|Descripción del estado del extremo.<br /><br /> INICIADO = Escucha y procesa solicitudes.<br /><br /> DETENIDO = Escucha pero no procesa solicitudes.<br /><br /> DESHABILITADO = No escucha.<br /><br /> El estado predeterminado es DETENIDO.<br /><br /> Acepta valores NULL.|  
|**is_admin_endpoint**|**bit**|Indica si el extremo es para uso administrativo.<br /><br /> 0 = Extremo no administrativo.<br /><br /> 1 = Extremo administrativo.<br /><br /> No admite valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Endpoints Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  [Vistas de catálogo de extremos &#40;Transact-SQL&#41;]  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
