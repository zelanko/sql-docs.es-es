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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915905"
---
# <a name="mssqlserver_1222"></a>MSSQLSERVER_1222
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1222|  
|Origen de eventos|MSSQLSERVER|  
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
  
  
