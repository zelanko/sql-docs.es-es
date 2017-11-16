---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 423f504ba458968c98d0bad3da1e78bf0ed01e84
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1222|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LK_TIMEOUT|  
|Texto del mensaje|Superado el tiempo de espera de solicitud de bloqueo.|  
  
## <a name="explanation"></a>Explicación  
Otra transacción retuvo un bloqueo en un recurso necesario durante más tiempo del que esta consulta podía esperar.  
  
## <a name="user-action"></a>Acción del usuario  
Realice las siguientes tareas para solucionar el problema:  
  
1.  Busque la transacción que está reteniendo el bloqueo en el recurso necesario, si es posible. Use las vistas de administración dinámica **sys.dm_os_waiting_tasks** y **sys.dm_tran_locks**.  
  
2.  Si la transacción sigue reteniendo el bloqueo, finalice la transacción si es necesario.  
  
3.  Vuelva a ejecutar la consulta.  
  
Si este error se produce con frecuencia, cambie el período de tiempo de espera de bloqueo o modifique las transacciones problemáticas para que mantengan el bloqueo durante menos tiempo.  
  
