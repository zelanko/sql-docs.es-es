---
title: Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 794dfea63b193ff79fb5831cb3a4e519d7d5f63e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62691386"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo
  Esta regla determina si la opción Grado máximo de paralelismo (MAXDOP) tiene un valor mayor que 8. Establecer esta opción en un valor mayor a menudo causa un consumo de recursos no deseado y la degradación del rendimiento.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción Grado máximo de paralelismo en 8, o menos, utilizando sp_configure.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Artículo 329204 de Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?linkid=117786)  
  
 [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
