---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab94977bcd3bf5a9b0b26ac7be76cb67d58e0755
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913991"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41333|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CROSS_CONTAINER_ISOLATION_FAILURE|  
|Texto del mensaje|Las siguientes transacciones deben acceder a tablas optimizadas para memoria y a procedimientos almacenados compilados de forma nativa en el aislamiento de instantáneas: transacciones RepeatableRead, transacciones Serializable y transacciones que accedan a las tablas que no estén optimizadas para memoria en aislamiento RepeatableRead o Serializable.|  
  
## <a name="explanation"></a>Explicación  
 Hay restricciones respecto al usuario de los niveles de aislamiento mayores entre las transacciones basadas en disco y las transacciones XTP.  
  
## <a name="user-action"></a>Acción del usuario  
 No intente operaciones de aislamiento alto nivel de las tablas optimizadas en memoria (y procedimientos compilados de forma nativa) y las tablas basadas en disco.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
