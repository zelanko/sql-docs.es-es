---
title: Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49032b9da1de6cd77ddd698b331853feb3d815d7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla determina si la opción Grado máximo de paralelismo (MAXDOP) tiene un valor mayor que 8. Establecer esta opción en un valor mayor a menudo causa un consumo de recursos no deseado y la degradación del rendimiento.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción Grado máximo de paralelismo en 8, o menos, utilizando sp_configure.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Artículo 329204 de Microsoft Knowledge Base](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
