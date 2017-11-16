---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 117bc8fb03796a14176727baf66d3ea468becddd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver4064"></a>MSSQLSERVER_4064
  
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
  
