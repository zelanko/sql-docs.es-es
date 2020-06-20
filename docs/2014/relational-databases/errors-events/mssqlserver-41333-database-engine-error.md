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
ms.openlocfilehash: 0fdc950e523fe1851aaf5664e2d40ff311a24ab7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85032985"
---
# <a name="mssqlserver_41333"></a>MSSQLSERVER_41333
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41333|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CROSS_CONTAINER_ISOLATION_FAILURE|  
|Texto del mensaje|Las transacciones siguientes deben tener acceso a las tablas optimizadas en memoria y a los procedimientos almacenados compilados de forma nativa con aislamiento de instantánea: las transacciones RepeatableRead, Serializable y las que tienen acceso a las tablas que no están optimizadas en memoria en el aislamiento RepeatableRead o Serializable.|  
  
## <a name="explanation"></a>Explicación  
 Hay restricciones respecto al usuario de los niveles de aislamiento mayores entre las transacciones basadas en disco y las transacciones XTP.  
  
## <a name="user-action"></a>Acción del usuario  
 No intente operaciones de aislamiento alto nivel de las tablas optimizadas en memoria (y procedimientos compilados de forma nativa) y las tablas basadas en disco.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
