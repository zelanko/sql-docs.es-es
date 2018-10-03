---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01325e8d83a5a7d7b65398f4e0cb981b1fca7540
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208935"
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
  
  
