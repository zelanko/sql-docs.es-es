---
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d5217ffc26130497db603e4757d84092c3a4e175
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416494"
---
# <a name="mssqlserver41342"></a>MSSQLSERVER_41342
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41342|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HK_HW_NOT_SUPPORTED|  
|Texto del mensaje|El modelo del procesador del sistema no permite crear *construct*. Este error suele producirse con procesadores antiguos. Para obtener información sobre los modelos admitidos, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="explanation"></a>Explicación  
 Las tablas con optimización para memoria requieren un modelo de procesador compatible con las operaciones atómicas de comparación e intercambio con valores de 128 bits, que requieren la instrucción CMPXCHG16B del lenguaje ensamblador. Ciertos modelos anteriores de procesadores AMD no admiten la instrucción CMPXCHG16B. Además, algunos entornos de virtualización no tienen habilitada esta instrucción de forma predeterminada.  
  
## <a name="user-action"></a>Acción del usuario  
 Actualice el procesador. Si su procesador admite la instrucción y está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina virtual, cambie la configuración para admitir la instrucción CMPXCHG16B.  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
