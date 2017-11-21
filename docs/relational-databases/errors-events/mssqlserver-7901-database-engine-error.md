---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 910ba3ad94d4e6aaca037de207440538b6c39c74
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver7901"></a>MSSQLSERVER_7901
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7901|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Texto del mensaje|Instrucción de reparación no procesada. No se permite este nivel de reparación cuando la base de datos está en modo de emergencia.|  
  
## <a name="explanation"></a>Explicación  
La base de datos está en modo de emergencia y se ha especificado un nivel de reparación distinto de REPAIR_ALLOW_DATA_LOSS. Las reparaciones no pueden llevarse a cabo en el modo de emergencia, a menos que se especifique REPAIR_ALLOW_DATA_LOSS.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a ejecutar el comando y especifique la opción REPAIR_ALLOW_DATA_LOSS.  
  

