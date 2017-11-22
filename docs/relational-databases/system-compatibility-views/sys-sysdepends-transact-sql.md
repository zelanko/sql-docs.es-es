---
title: Sys.sysdepends (Transact-SQL) | Documentos de Microsoft
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
- sys.sysdepends_TSQL
- sysdepends
- sysdepends_TSQL
- sys.sysdepends
dev_langs: TSQL
helpviewer_keywords:
- sysdepends system table
- sys.sysdepends compatibility view
ms.assetid: f9c182cb-386f-4e72-859f-9f1115b389f9
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76a51f07ef8b504c616cd4ef080d0c84e9f782a5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syssysdepends-transact-sql"></a>sys.sysdepends (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información de dependencia entre objetos (vistas, procedimientos y desencadenadores) de la base de datos y los objetos (tablas, vistas y procedimientos) contenidos en su definición.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. de objeto.|  
|**depid**|**int**|Id. del objeto dependiente.|  
|**número**|**smallint**|Número de procedimiento.|  
|**depnumber**|**smallint**|Número del procedimiento dependiente.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deptype**|**tinyint**|Identifica el tipo de objeto dependiente:<br /><br /> 0 = Objeto o columna (solo referencias no enlazadas a esquemas)<br /><br /> 0 = Objeto o columna (referencias enlazadas a esquemas)|  
|**depdbid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**depsiteid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**selall**|**bit**|1 = El objeto se utiliza en una instrucción SELECT *.<br /><br /> 0 = No.|  
|**resultobj**|**bit**|1 = Se está actualizando el objeto.<br /><br /> 0 = No.|  
|**readobj**|**bit**|1 = Se está leyendo el objeto.<br /><br /> 0 = No.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40; Transact-SQL &#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [sp_depends &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-depends-transact-sql.md)   
 [Sys.sql_dependencies &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)  
  
  
