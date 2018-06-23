---
title: MSSQLSERVER_1204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 1204 (Database Engine error)
ms.assetid: de6ece78-79de-484d-9224-ca0f7645815f
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 48d4bdc9cd12892a9bef96e26e54e158ede05391
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200363"
---
# <a name="mssqlserver1204"></a>MSSQLSERVER_1204
    
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
  
  