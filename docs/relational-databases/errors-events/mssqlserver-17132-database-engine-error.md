---
title: MSSQLSERVER_17132 | Microsoft Docs
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
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3ea493efb21a7d2f0ed50ef92cb314de394be74
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17132|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|INIT_NODESSPACE|  
|Texto del mensaje|Error al iniciar el servidor debido a una falta de memoria para el descriptor. Reduzca la carga de memoria no esencial o aumente la memoria del sistema.|  
  
## <a name="explanation"></a>Explicación  
No se pudo asignar suficiente memoria para almacenar el descriptor interno del servidor.  
  
## <a name="user-action"></a>Acción del usuario  
Agregue más memoria a la máquina. Puede ser útil seguir un procedimiento para solucionar problemas genéricos de memoria.  
  
