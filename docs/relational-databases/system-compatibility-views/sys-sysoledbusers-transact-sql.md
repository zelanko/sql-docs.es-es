---
title: Sys.sysoledbusers (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
caps.latest.revision: 34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9bed55c42d7d656f53e24acb1d859658666ce901
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220846"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  Esta tabla del sistema de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] se incluye en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como una vista para la compatibilidad con versiones anteriores. Se recomienda que use [vistas de catálogo](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) en su lugar.  
  
 Contiene una fila por cada correspondencia entre usuario y contraseña en el servidor vinculado especificado. **sysoledbusers** se almacena en la **maestro** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|SID (número de identificación de seguridad) del servidor.|  
|**rmtloginame**|**nvarchar (** 128 **)**|Nombre del inicio de sesión remoto que **loginsid** para vinculado se asigna a **rmtservid**.|  
|**rmtpassword**|**nvarchar (** 128 **)**|Devuelve NULL.|  
|**loginsid**|**varbinary (** 85 **)**|SID del inicio de sesión local que se va a asignar.|  
|**status**|**smallint**|Si este valor es 1, la asignación debe utilizar las credenciales del usuario.|  
|**ChangeDate**|**datetime**|Fecha en que cambió por última vez la información de asignación.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
