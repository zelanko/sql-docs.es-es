---
title: Sys.Endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61a541457f170ee884a1f0b8c3560b04601ffde5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736803"
---
# <a name="sysendpoints-transact-sql"></a>sys.endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por extremo que se crea en el sistema. En todo momento hay exactamente un extremo SYSTEM.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del punto de conexión. Es único en el servidor. No admite valores NULL.|  
|**endpoint_id**|**int**|Id. del extremo. Es único en el servidor. Un extremo con un identificador inferior a 65536 es un extremo del sistema. No admite valores NULL.|  
|**principal_id**|**int**|Id. de la entidad de seguridad del servidor que creó y es propietaria de este extremo. Acepta valores NULL.|  
|**Protocolo**|**tinyint**|Protocolo del extremo.<br /><br /> 1 = HTTP<br /><br /> 2 = TCP<br /><br /> 3 = Canalizaciones con nombre<br /><br /> 4 = Memoria compartida<br /><br /> 5 = Adaptador de interfaz virtual (VIA)<br /><br /> No admite valores NULL.|  
|**protocol_desc**|**nvarchar(60)**|Descripción del protocolo del extremo. QUE ACEPTA VALORES NULL. Los valores pueden ser los siguientes:<br /><br /> **HTTP**<br /><br /> **TCP**<br /><br /> **NAMED_PIPES**<br /><br /> **SHARED_MEMORY**<br /><br /> **A través de** Nota: el protocolo VIA está en desuso. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**Tipo**|**tinyint**|Tipo de carga del extremo.<br /><br /> 1 = SOAP<br /><br /> 2 = TSQL<br /><br /> 3 = SERVICE_BROKER<br /><br /> 4 = DATABASE_MIRRORING<br /><br /> No admite valores NULL.|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de carga del extremo. Acepta valores NULL. Los valores pueden ser los siguientes:<br /><br /> **SOAP**<br /><br /> **TSQL**<br /><br /> **SERVICE_BROKER**<br /><br /> **DATABASE_MIRRORING**|  
|**state**|**tinyint**|Estado del extremo.<br /><br /> 0 = INICIADO, escucha y procesa solicitudes.<br /><br /> 1 = DETENIDO, escucha pero no procesa solicitudes.<br /><br /> 2 = DESHABILITADO, no escucha.<br /><br /> El estado predeterminado es 1. Acepta valores NULL.|  
|**state_desc**|**nvarchar(60)**|Descripción del estado del extremo.<br /><br /> INICIADO = Escucha y procesa solicitudes.<br /><br /> DETENIDO = Escucha pero no procesa solicitudes.<br /><br /> DESHABILITADO = No escucha.<br /><br /> El estado predeterminado es DETENIDO.<br /><br /> Acepta valores NULL.|  
|**is_admin_endpoint**|**bit**|Indica si el extremo es para uso administrativo.<br /><br /> 0 = Extremo no administrativo.<br /><br /> 1 = Extremo administrativo.<br /><br /> No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Endpoints Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  [Vistas de catálogo de extremos &#40;Transact-SQL&#41;]  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
