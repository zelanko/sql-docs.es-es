---
title: MSSQLSERVER_8649 | Microsoft Docs
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
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3da65279260e142385a7b872c7234cb0f0b6bc8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104903"
---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8649|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|COST_TOO_HIGH|  
|Texto del mensaje|Se ha cancelado la consulta porque el costo estimado de esta consulta (%d) supera el umbral configurado de %d. Póngase en contacto con el administrador del sistema.|  
  
## <a name="explanation"></a>Explicación  
 La consulta se canceló porque el costo estimado de la misma supera el umbral configurado establecido para QUERY_GOVERNOR_COST_LIMIT.  
  
## <a name="user-action"></a>Acción del usuario  
 Establezca la opción QUERY_GOVERNOR_COST_LIMIT en un valor mayor.  
  
## <a name="see-also"></a>Vea también  
 [SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-query-governor-cost-limit-transact-sql)  
  
  
