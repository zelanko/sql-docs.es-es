---
title: Sys.sysfilegroups (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysfilegroups_TSQL
- sys.sysfilegroups
- sysfilegroups
- sys.sysfilegroups_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysfilegroups system table
- sys.sysfilegroups compatibility view
ms.assetid: e567fa07-31cd-43cc-b8c7-ba6108baca80
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8870478ba690b800effd974437fbabff3ae3817e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syssysfilegroups-transact-sql"></a>sys.sysfilegroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada grupo de archivos de una base de datos. Esta tabla contiene al menos la entrada correspondiente al grupo de archivos principal.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Id. de grupo**|**smallint**|Número de identificación de grupo, único en cada base de datos.|  
|**allocpolicy**|**smallint**|Reservado|  
|**status**|**int**|0x8 = Solo lectura<br /><br /> 0x10 = Predeterminado|  
|**nombre de grupo**|**sysname**|Nombre del grupo de archivos.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
