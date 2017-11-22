---
title: MSSQLSERVER_5245 | Microsoft Docs
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
helpviewer_keywords: 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a2898d64dc0d73156ee9a721a762492de85674c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
