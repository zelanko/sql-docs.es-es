---
title: Sys.Routes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e27f943e14ad6ef9340764bbd376d754f43dc26b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Estas vistas de catálogo contienen una fila por ruta. Service Broker usa rutas para localizar la dirección de red de un servicio.   
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la ruta, único en la base de datos. No acepta valores NULL.|  
|**Route_ID**|**int**|Identificador de la ruta. No acepta valores NULL.|  
|**principal_id**|**int**|Identificador de la base de datos de la entidad de seguridad propietaria de la ruta. ACEPTA VALORES NULL.|  
|**remote_service_name**|**nvarchar(256)**|Nombre del servicio remoto. ACEPTA VALORES NULL.|  
|**BROKER_INSTANCE**|**nvarchar (128)**|Identificador del agente que hospeda el servicio remoto. ACEPTA VALORES NULL.|  
|**duración**|**datetime**|Fecha y hora de expiración de la ruta. Tenga en cuenta que este valor no usa la zona horaria local. En lugar de ello, el valor muestra la fecha de expiración de UTC. ACEPTA VALORES NULL.|  
|**dirección**|**nvarchar(256)**|Dirección de red a la que Service Broker envía mensajes para el servicio remoto. ACEPTA VALORES NULL.|  
|**MIRROR_ADDRESS**|**nvarchar(256)**|Dirección de red del asociado de reflejo para el servidor especificado en la dirección. ACEPTA VALORES NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
