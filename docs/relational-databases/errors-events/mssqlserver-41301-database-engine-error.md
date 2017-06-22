---
title: MSSQLSERVER_41301 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 369aa132cd17fb85957c1bb3f51f4f64396dfd76
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41301"></a>MSSQLSERVER_41301
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41301|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|COMMIT_DEPENDENCY_FAILURE|  
|Texto del mensaje|Una transacción anterior a la transacción actual realizada en una dependencia se ha anulado y la transacción actual ya no puede confirmarse.|  
  
## <a name="explanation"></a>Explicación  
La transacción encontró un error de dependencia y ahora está condenada.  
  
Este error también puede producirse si hay demasiadas transacciones dependientes. Las transacciones de escritura pueden tener un número limitado de transacciones dependientes. Por ejemplo, este error puede producirse si muchas transacciones de lectura intentan depender de la transacción de actualización.  
  
## <a name="user-action"></a>Acción del usuario  
No haga ningún trabajo en la transacción. Llame a ROLLBACK TRAN para revertir la transacción. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vea también  
[Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  

