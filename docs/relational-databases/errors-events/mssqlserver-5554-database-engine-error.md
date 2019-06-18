---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ba40eba38d4659f100dd5aa9671e87f51b366b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445540"
---
# <a name="mssqlserver5554"></a>MSSQLSERVER_5554
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|5554|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FS_MINIVER_OVERFLOW|  
|Texto del mensaje|El número total de versiones para un único archivo ha alcanzado el límite máximo establecido por el sistema de archivos.|  
  
## <a name="explanation"></a>Explicación  
En conjuntos de resultados activos múltiples (MARS) o escenarios de desencadenador, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la miniversión especificada por el sistema operativo.  
  
## <a name="user-action"></a>Acción del usuario  
Intente evitar las actualizaciones repetidas en los datos de la misma transacción.  
  
