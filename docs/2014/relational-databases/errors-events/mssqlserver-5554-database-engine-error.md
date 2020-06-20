---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5095a50f257abafb6ebde97bb32c57bc71fc4e09
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053849"
---
# <a name="mssqlserver_5554"></a>MSSQLSERVER_5554
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|MSSQLSERVER|  
|Id. de evento|5554|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|FS_MINIVER_OVERFLOW|  
|Texto del mensaje|El número total de versiones para un único archivo ha alcanzado el límite máximo establecido por el sistema de archivos.|  
  
## <a name="explanation"></a>Explicación  
 En conjuntos de resultados activos múltiples (MARS) o escenarios de desencadenador, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la miniversión especificada por el sistema operativo.  
  
## <a name="user-action"></a>Acción del usuario  
 Intente evitar las actualizaciones repetidas en los datos de la misma transacción.  
  
  
