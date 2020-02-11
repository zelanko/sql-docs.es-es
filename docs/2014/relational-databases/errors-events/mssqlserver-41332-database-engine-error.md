---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0bbd8b256145a9d91e8615aaf7d87a4b8ce7b8b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62867899"
---
# <a name="mssqlserver_41332"></a>MSSQLSERVER_41332
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|41332|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Texto del mensaje|No se puede tener acceso ni crear tablas optimizadas en memoria ni procedimientos almacenados compilados de forma nativa cuando la configuración de TRANSACTION ISOLATION LEVEL para la sesión se ha establecido en SNAPSHOT.|  
  
## <a name="explanation"></a>Explicación  
 La transacción se inició con el nivel de aislamiento de instantánea y luego se intentó utilizar una función incompatible.  
  
## <a name="user-action"></a>Acción del usuario  
 Inicie la transacción con otro nivel de aislamiento. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
