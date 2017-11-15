---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: e7d9f10267821e03d89bd8a0c32ea8ceb55499fd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver41332"></a>MSSQLSERVER_41332
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41332|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Texto del mensaje|No se puede tener acceso ni crear tablas optimizadas en memoria ni procedimientos almacenados compilados de forma nativa cuando la configuración de TRANSACTION ISOLATION LEVEL para la sesión se ha establecido en SNAPSHOT.|  
  
## <a name="explanation"></a>Explicación  
La transacción se inició con el nivel de aislamiento de instantánea y luego se intentó utilizar una función incompatible.  
  
## <a name="user-action"></a>Acción del usuario  
Inicie la transacción con otro nivel de aislamiento. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vea también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
