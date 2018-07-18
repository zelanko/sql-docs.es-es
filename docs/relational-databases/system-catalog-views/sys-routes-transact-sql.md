---
title: Sys.Routes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 89fb63380c95e38f97f02b24eb68c178182b873a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985234"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Estas vistas de catálogo contienen una fila por ruta. Service Broker usa rutas para localizar la dirección de red de un servicio.   

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la ruta, único en la base de datos. No acepta valores NULL.|  
|**Route_ID**|**int**|Identificador de la ruta. No acepta valores NULL.|  
|**principal_id**|**int**|Identificador de la base de datos de la entidad de seguridad propietaria de la ruta. QUE ACEPTA VALORES NULL.|  
|**remote_service_name**|**nvarchar(256)**|Nombre del servicio remoto. QUE ACEPTA VALORES NULL.|  
|**BROKER_INSTANCE**|**nvarchar(128)**|Identificador del agente que hospeda el servicio remoto. QUE ACEPTA VALORES NULL.|  
|**duración**|**datetime**|Fecha y hora de expiración de la ruta. Tenga en cuenta que este valor no usa la zona horaria local. En lugar de ello, el valor muestra la fecha de expiración de UTC. QUE ACEPTA VALORES NULL.|  
|**dirección**|**nvarchar(256)**|Dirección de red a la que Service Broker envía mensajes para el servicio remoto. QUE ACEPTA VALORES NULL. Base de datos de instancia administrada de SQL, la dirección debe ser local.|  
|**mirror_address**|**nvarchar(256)**|Dirección de red del asociado de reflejo para el servidor especificado en la dirección. QUE ACEPTA VALORES NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
