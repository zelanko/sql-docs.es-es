---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8908c1075c0df7cb60d5e8b79c9d9067c03876ee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|4064|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DB_UFAIL_FATAL|  
|Texto del mensaje|No se puede abrir la base de datos predeterminada del usuario. Error de inicio de sesión.|  
  
## <a name="explanation"></a>Explicación  
El inicio de sesión de SQL Server no pudo conectarse debido a un problema con su base de datos predeterminada. Bien la propia base de datos no es válida o el inicio de sesión no tiene permiso CONNECT para la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
Use ALTER LOGIN para cambiar la base de datos predeterminada del inicio de sesión. Conceda el permiso CONNECT al inicio de sesión.  
  
