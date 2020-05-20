---
title: sysdbmaintplans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b787b62f1f4f68c279449aa9bf4bc905898ec66d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82803149"
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta tabla se incluye en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conservar la información existente de las instancias actualizadas de una versión anterior de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no cambia el contenido de esta tabla. Esta tabla se almacena en la base de datos **msdb** .  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Id. del plan de mantenimiento de bases de datos.|  
|**plan_name**|**sysname**|Nombre del plan de mantenimiento de bases de datos.|  
|**date_created**|**datetime**|Fecha de creación del plan de mantenimiento de bases de datos.|  
|**propietario**|**sysname**|Propietario del plan de mantenimiento de bases de datos.|  
|**max_history_rows**|**int**|Número máximo de filas asignadas para registrar el historial del plan de mantenimiento de bases de datos de la tabla del sistema.|  
|**remote_history_server**|**sysname**|Nombre del servidor remoto en el que se puede escribir el informe del historial.|  
|**max_remote_history_rows**|**int**|Número máximo de filas asignadas en la tabla del sistema de un servidor remoto en el que se puede escribir el informe del historial.|  
|**user_defined_1**|**int**|El valor predeterminado es NULL.|  
|**user_defined_2**|**nvarchar(100**|El valor predeterminado es NULL.|  
|**user_defined_3**|**datetime**|El valor predeterminado es NULL.|  
|**user_defined_4**|**uniqueidentifier**|El valor predeterminado es NULL.|  
|**log_shipping**|**bit**|Estado del trasvase de registros:<br /><br /> **0** = deshabilitado **1** = habilitado|  
  
  
