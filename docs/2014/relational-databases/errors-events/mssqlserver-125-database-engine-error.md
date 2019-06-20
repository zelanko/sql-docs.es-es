---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8287572d31dc136f21717ba45b730936b4fb78ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870462"
---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|125|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Las expresiones Case solo pueden anidarse hasta el nivel %d.|  
  
## <a name="explanation"></a>Explicación  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo permite 10 niveles de anidamiento en las expresiones CASE.  
  
## <a name="user-action"></a>Acción del usuario  
 Reduzca el nivel de las instrucciones CASE a 10 o a un número inferior.  
  
## <a name="see-also"></a>Vea también  
 [CASE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/case-transact-sql)  
  
  
