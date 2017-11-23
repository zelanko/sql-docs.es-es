---
title: dbo.sysnotifications (Transact-SQL) | Documentos de Microsoft
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
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs: TSQL
helpviewer_keywords: sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61f9e69444b8df91a7c92f38ecc4b9b577b7b405
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada notificación.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|Id. de la alerta.|  
|**operator_id**|**int**|Id. del operador al que se debe enviar la notificación.|  
|**notification_method**|**tinyint**|Método de notificación:<br /><br /> **1** = correo electrónico<br /><br /> **2** = buscapersonas<br /><br /> **4** = **netsend**<br /><br /> **7** = all|  
  
  
