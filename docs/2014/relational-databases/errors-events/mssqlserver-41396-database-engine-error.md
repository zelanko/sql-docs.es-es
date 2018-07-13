---
title: MSSQLSERVER_41396 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21de5c18d090afad5461c344d7a6704ecd8dabe4
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421434"
---
# <a name="mssqlserver41396"></a>MSSQLSERVER_41396
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41396|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|MAX_SORT_ROWS_EXCEEDED|  
|Texto del mensaje|La operación de ordenación ha superado el límite del búfer. La ejecución del procedimiento almacenado se anuló. Consulte los Libros en pantalla de SQL Server para obtener más información.|  
  
## <a name="explanation"></a>Explicación  
 Los procedimientos almacenados compilados de forma nativa realizan operaciones de ordenación en memoria. Hay un límite en cuanto al tamaño del búfer de ordenación. Este error indica que el tamaño del búfer de ordenación supera este límite. La operación de ordenación y la ejecución del procedimiento almacenado se han anulado.  
  
 El tamaño de cada fila o entrada del búfer de ordenación lo determinan el número de filas ordenadas junto con el número de combinaciones y el número y el tipo de funciones de agregado de la consulta. Si simplifica la consulta, puede reducir el tamaño de cada fila, con lo que cabrán más filas en el búfer de ordenación. El tamaño de las filas de las tablas base no afecta al tamaño de cada fila o entrada del búfer de ordenación.  
  
## <a name="user-action"></a>Acción del usuario  
 Seleccione menos filas o reduzca la complejidad de la consulta quitando combinaciones o funciones de agregado.  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
