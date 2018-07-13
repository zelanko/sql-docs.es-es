---
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7464be4dbdbd9df089c9219d79bede920f22891
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418294"
---
# <a name="mssqlserver41365"></a>MSSQLSERVER_41365
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41365|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HK_MERGE_SCHEDULE_ERROR|  
|Texto del mensaje|La solicitud de combinación para el intervalo de transacción [%ld, %ld] en la base de datos %.*ls no se ha programado. Los archivos de puntos de comprobación que representan el intervalo no están disponibles para la combinación o para parte de una combinación en curso.|  
  
## <a name="explanation"></a>Explicación  
 Los archivos de puntos de comprobación que representan el intervalo no están disponibles para la combinación o para parte de una combinación en curso.  
  
## <a name="user-action"></a>Acción del usuario  
 Proporciona un mejor intervalo de transacciones para la combinación y la espera antes de emitir la misma solicitud de nuevo. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
