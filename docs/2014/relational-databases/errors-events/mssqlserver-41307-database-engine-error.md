---
title: MSSQLSERVER_41307 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98407a65d5529fd73bccc638df11167131bd9f8d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033031"
---
# <a name="mssqlserver_41307"></a>MSSQLSERVER_41307
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41307|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HK_HEKATON_ROW_LIMIT|  
|Texto del mensaje|Se ha superado el límite de tamaño de fila de *number* bytes para las tablas optimizadas en memoria. Simplifique la definición de la tabla.|  
  
## <a name="explanation"></a>Explicación  
 El límite de tamaño de fila para las tablas optimizadas en memoria es de 8.060 bytes. Para obtener más información, vea [Tamaño de tabla y fila de las tablas con optimización para memoria](../in-memory-oltp/memory-optimized-tables.md). Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
