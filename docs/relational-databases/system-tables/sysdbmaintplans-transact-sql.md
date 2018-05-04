---
title: sysdbmaintplans (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d4f8b7c90d644cb9153bf716e91c38c56bee7f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta tabla se incluye en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conservar la información existente para las instancias actualizadas desde una versión anterior de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cambia el contenido de esta tabla. Esta tabla se almacena en la **msdb** base de datos.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Id. del plan de mantenimiento de bases de datos.|  
|**plan_name**|**sysname**|Nombre del plan de mantenimiento de bases de datos.|  
|**date_created**|**datetime**|Fecha de creación del plan de mantenimiento de bases de datos.|  
|**propietario**|**sysname**|Propietario del plan de mantenimiento de bases de datos.|  
|**max_history_rows**|**int**|Número máximo de filas asignadas para registrar el historial del plan de mantenimiento de bases de datos de la tabla del sistema.|  
|**remote_history_server**|**sysname**|Nombre del servidor remoto en el que se puede escribir el informe del historial.|  
|**max_remote_history_rows**|**int**|Número máximo de filas asignadas en la tabla del sistema de un servidor remoto en el que se puede escribir el informe del historial.|  
|**user_defined_1**|**int**|Valor predeterminado es NULL.|  
|**user_defined_2**|**nvarchar (100)**|Valor predeterminado es NULL.|  
|**user_defined_3**|**datetime**|Valor predeterminado es NULL.|  
|**user_defined_4**|**uniqueidentifier**|Valor predeterminado es NULL.|  
|**log_shipping**|**bit**|Estado del trasvase de registros:<br /><br /> **0** = disabled **1** = habilitado|  
  
  
