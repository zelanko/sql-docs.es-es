---
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: aeb29216e36e208a1475a117e4ad653854fd50d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198453"
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|17084|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P3_ATOMIC_WITH_MISSING_OPTION|  
|Texto del mensaje|La cláusula WITH de la instrucción BEGIN ATOMIC debe especificar un valor para la opción '%ls'.|  
  
## <a name="explanation"></a>Explicación  
 La cláusula WITH de la instrucción BEGIN ATOMIC no especificó un valor para una opción.  
  
## <a name="user-action"></a>Acción del usuario  
 Los bloques `ATOMIC` requieren valores de las opciones `WITH` y `TRANSACTION ISOLATION LEVEL`de `LANGUAGE`. Por ejemplo:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  