---
title: dbo.syscategorías (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 50d79a9043c952fe124b2cfca1917df29a76394f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722940"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contiene las categorías que usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar los trabajos, las alertas y los operadores. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Id. de la categoría.|  
|**category_class**|**int**|Tipo de elemento en la categoría:<br /><br /> **1** = trabajo<br /><br /> **2** = alerta<br /><br /> **3** = (operador)|  
|**category_type**|**tinyint**|Tipo de categoría:<br /><br /> **1** = local<br /><br /> **2** = multiservidor<br /><br /> **3** = ninguno|  
|**name**|**sysname**|Nombre de la categoría|  
  
  
