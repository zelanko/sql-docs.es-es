---
title: dbo.syscategories (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs: TSQL
helpviewer_keywords: syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c61063d79e64cbd5350caad5eb374b12f028fa5c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene las categorías que usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar los trabajos, las alertas y los operadores. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Id. de la categoría.|  
|**category_class**|**int**|Tipo de elemento en la categoría:<br /><br /> **1** = trabajo<br /><br /> **2** = alerta<br /><br /> **3** = (operador)|  
|**category_type**|**tinyint**|Tipo de categoría:<br /><br /> **1** = local<br /><br /> **2** = multiservidor<br /><br /> **3** = ninguno|  
|**Nombre**|**sysname**|Nombre de la categoría|  
  
  
