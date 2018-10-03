---
title: Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7313f93381c9a3e2dd4e821d98e35bf3b5d5a06f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123575"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo
  Esta regla determina si la opción Grado máximo de paralelismo (MAXDOP) tiene un valor mayor que 8. Establecer esta opción en un valor mayor a menudo causa un consumo de recursos no deseado y la degradación del rendimiento.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción Grado máximo de paralelismo en 8, o menos, utilizando sp_configure.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Artículo 329204 de Microsoft Knowledge Base](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
