---
title: sysdbmaintplan_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_databases
- sysdbmaintplan_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_databases system table
ms.assetid: f8413a44-8fcc-4899-84f2-b4afe0f8ec08
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6bd1622e898d6554d5eb9fbc66fae729f5a8e973
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130477"
---
# <a name="sysdbmaintplandatabases-transact-sql"></a>sysdbmaintplan_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta tabla se incluye para conservar la información existente de las instancias actualizadas desde una versión anterior de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores no cambian el contenido de esta tabla. Esta tabla se almacena en el **msdb** base de datos.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Id. del plan de mantenimiento.|  
|**database_name**|**sysname**|Nombre de la base de datos asociada al plan de mantenimiento de bases de datos.|  
  
  
