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
ms.openlocfilehash: f2ce32667d4f9615edcc7f15bf3d29d5d32490ad
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553920"
---
# <a name="mssqlserver_1222"></a>MSSQLSERVER_1222
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
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
  
  
