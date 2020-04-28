---
title: DBO. systaskids (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ed9ac8e81abaf6367d3a9c5518f1f18cb94ef8b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990397"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una asignación de las tareas creadas en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a trabajos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] de la versión actual. Esta tabla se almacena en la base de datos **msdb** .  
  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|Id. de la tarea|  
|**job_id**|**uniqueidentifier**|Id. del trabajo al que está asignada la tarea|  
  
  
