---
title: Sys.server_triggers (Transact-SQL) | Documentos de Microsoft
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
- server_triggers
- sys.server_triggers_TSQL
- server_triggers_TSQL
- sys.server_triggers
dev_langs: TSQL
helpviewer_keywords: sys.server_triggers catalog view
ms.assetid: 25926ff4-9271-45bf-bc32-d5d3344bd47a
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15dd37e207117020fb1771e5ebf746db8a2cc145
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysservertriggers-transact-sql"></a>sys.server_triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene el conjunto de todos los desencadenadores DDL de servidor cuyo object_type es TR o TA. En el caso de los desencadenadores CLR, el ensamblado deben cargarse en el **maestro** base de datos. Todos los nombres de desencadenadores DDL de nivel de servidor se encuentran en un único ámbito global.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del desencadenador.|  
|**object_id**|**int**|Id. del objeto.|  
|**parent_class**|**tinyint**|Clase del elemento primario. Siempre es:<br /><br /> 100 = Servidor|  
|**parent_class_desc**|**nvarchar (60)**|Descripción de la clase de elemento primario. Siempre es:<br /><br /> SERVIDOR.|  
|**parent_id**|**int**|Siempre es 0 para los desencadenadores de SERVER.|  
|**tipo**|**Char(2)**|Tipo de objeto:<br /><br /> TA = Desencadenador de ensamblado (CLR)<br /><br /> TR = Desencadenador SQL|  
|**type_desc**|**nvarchar (60)**|Descripción de la clase del tipo de objeto.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|Fecha de creación del desencadenador.|  
|**modify_date**|**datetime**|Fecha en que se modificó el desencadenador por última vez mediante una instrucción ALTER.|  
|**is_ms_shipped**|**bit**|Desencadenador creado en nombre del usuario por un componente interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_disabled**|**bit**|1 = El desencadenador está deshabilitado.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
