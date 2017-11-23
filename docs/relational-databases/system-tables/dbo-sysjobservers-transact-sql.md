---
title: dbo.sysjobservers (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a706c537f4f983563dacb1f137314680824dd30
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena la asociación o relación de un trabajo determinado con uno o más servidores de destino. Esta tabla se almacena en la base de datos msdb.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|Número de identificación del trabajo.|  
|server_id|**int**|Número de identificación del servidor.|  
|last_run_outcome|**tinyint**|Resultado de la última ejecución del trabajo:<br /><br /> **0** = error<br /><br /> **1** = correctamente<br /><br /> **3** = cancelado|  
|mensaje de last_outcome_|**nvarchar (1024)**|Mensaje asociado, si existe, a la columna last_run_outcome.|  
|last_run_date|**int**|Fecha en que se ejecutó el trabajo por última vez.|  
|last_run_time|**int**|Hora a la que se ejecutó el trabajo por última vez.|  
|last_run_duration|**int**|Duración de la ejecución del trabajo, en horas, minutos y segundos. Calculado mediante la fórmula: (*horas*\*10000) + (*minutos*\*100) + *segundos*.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas del Agente SQL Server &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
