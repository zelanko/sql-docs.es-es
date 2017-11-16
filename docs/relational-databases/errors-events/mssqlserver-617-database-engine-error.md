---
title: MSSQLSERVER_617 | Microsoft Docs
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
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 570073a75fd1a325837812aa0f75dba2e1a90902
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver617"></a>MSSQLSERVER_617
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|617|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NODESHASH|  
|Texto del mensaje|No se encontró el descriptor del id. de objeto %ld del id. de base de datos %d en la tabla hash al intentar deshacer el hash. Falta una entrada en una tabla de trabajo. Vuelva a ejecutar la consulta. Si hay un cursor en el proceso, ciérrelo y vuelva a abrirlo.|  
  
## <a name="explanation"></a>Explicación  
SQL Server no puede encontrar la tabla de trabajo para una entrada concreta.  
  
## <a name="user-action"></a>Acción del usuario  
  
1.  Si hay un cursor en el proceso, ciérrelo y vuelve a abrirlo.  
  
2.  Ejecute de nuevo la consulta.  
  

