---
description: dbo.syscategories (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 84d72b2ec08573b7c7aa72903eab1bc828d6f774
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525347"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene las categorías que usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar los trabajos, las alertas y los operadores. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Id. de la categoría.|  
|**category_class**|**int**|Tipo de elemento en la categoría:<br /><br /> **1** = trabajo<br /><br /> **2** = alerta<br /><br /> **3** = (operador)|  
|**category_type**|**tinyint**|Tipo de categoría:<br /><br /> **1** = local<br /><br /> **2** = multiservidor<br /><br /> **3** = ninguno|  
|**name**|**sysname**|Nombre de la categoría|  
  
  
