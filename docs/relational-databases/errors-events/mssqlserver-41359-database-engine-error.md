---
title: MSSQLSERVER_41359 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: d968578a85366ab4fb6c72057434473dc5a0e909
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver41359"></a>MSSQLSERVER_41359
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41359|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|Texto del mensaje|Una consulta que tiene acceso a las tablas optimizadas en memoria con el nivel de aislamiento READ COMMITTED no puede tener acceso a las tablas basadas en disco cuando la opción de base de datos READ_COMMITTED_SNAPSHOT está establecida en ON. Proporciona un nivel de aislamiento admitido para la tabla optimizada en memoria mediante una sugerencia de tabla, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicación  
La base de datos con READ_COMMITTED_SNAPSHOT=ON no admite las transacciones que tienen acceso a las tablas optimizadas en memoria a las y tablas basadas en disco.  
  
## <a name="user-action"></a>Acción del usuario  
Establezca READ_COMMITTED_SNAPSHOT en OFF o proporcione un nivel de aislamiento admitido para la tabla optimizada en memoria mediante una sugerencia de nivela de tabla, como WITH (SNAPSHOT). Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vea también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
