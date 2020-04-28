---
title: sysdbmaintplan_jobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_jobs
- sysdbmaintplan_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_jobs system table
ms.assetid: bc65cd70-6ef2-4c17-be11-877ecf4efe50
author: stevestein
ms.author: sstein
ms.openlocfilehash: f780199361d9e5741187dd4e5346abb2df98b9cb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68130443"
---
# <a name="sysdbmaintplan_jobs-transact-sql"></a>sysdbmaintplan_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta tabla se incluye en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conservar la información existente de las instancias actualizadas de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cambia el contenido de esta tabla. Esta tabla se almacena en la base de datos **msdb** .  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Id. del plan de mantenimiento de bases de datos.|  
|**job_id**|**uniqueidentifier**|Id. de un trabajo asociado con el plan de mantenimiento de bases de datos.|  
  
  
