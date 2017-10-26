---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 25109bc21ea0ec035aa30e7ba439dcd967c4ac55
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|5245|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Texto del mensaje|Id. de objeto O_ID (objeto 'NAME'): DBCC no pudo obtener un bloqueo en este objeto porque se superó el tiempo de espera de la solicitud de bloqueo. Este objeto ha sido omitido y no se va a procesar.|  
  
## <a name="explanation"></a>Explicación  
Se produjo un tiempo de espera de bloqueo mientras DBCC estaba esperando un bloqueo de tabla para el objeto especificado.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a ejecutar el comando DBCC.  
  

