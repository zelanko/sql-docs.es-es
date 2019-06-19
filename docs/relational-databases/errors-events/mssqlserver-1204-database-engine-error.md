---
title: MSSQLSERVER_1204 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1204 (Database Engine error)
ms.assetid: de6ece78-79de-484d-9224-ca0f7645815f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b334eda517f7f4a2283f3ac24f0dd0bb1a84b846
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048386"
---
# <a name="mssqlserver1204"></a>MSSQLSERVER_1204
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1204|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LK_OUTOF|  
|Texto del mensaje|La instancia del motor de base de datos de SQL Server no puede obtener un recurso LOCK en este momento. Vuelva a ejecutar la instrucción cuando haya menos usuarios activos. Pida al administrador de la base de datos que compruebe la configuración de bloqueos y memoria de esta instancia o si hay transacciones que se ejecutan durante mucho tiempo.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede obtener un recurso de bloqueo. Esto puede suceder por una de las siguientes razones:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede asignar más memoria del sistema operativo, ya sea porque la están usando otros procesos o porque el servidor está funcionando con la opción **max server memory** configurada.  
  
-   El administrador de bloqueos no utilizará más del 60 por ciento de la memoria disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
Si sospecha que SQL Server no puede asignar suficiente memoria, intente lo siguiente:  
  
-   Si hay otras aplicaciones que consumen recursos aparte de SQL Server, intente detener dichas aplicaciones o considere la posibilidad de ejecutarlas en un servidor independiente. De esta forma, se liberará memoria de otros procesos para SQL Server.  
  
-   Si ha configurado la opción max server memory, aumente el valor de la opción.  
  
Si sospecha que el administrador de bloqueos ha utilizado la cantidad máxima de memoria disponible, identifique la transacción que retiene más bloqueos y finalícela. Mediante el siguiente script se identifica la transacción que tiene más bloqueos:  
  
```  
SELECT request_session_id, COUNT (*) num_locks  
FROM sys.dm_tran_locks  
GROUP BY request_session_id   
ORDER BY count (*) DESC  
```  
  
Finalice el identificador de sesión más alto mediante el comando KILL.  
  
