---
title: Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 00123da615c420fa3d58daae9a287ce3c13b8329
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316663"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla determina si la opción Grado máximo de paralelismo (MAXDOP) tiene un valor mayor que 8. Establecer esta opción en un valor mayor a menudo causa un consumo de recursos no deseado y la degradación del rendimiento.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción Grado máximo de paralelismo en 8, o menos, utilizando sp_configure.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Recomendaciones y directrices para la opción de configuración "grado máximo de paralelismo" en SQL Server](https://go.microsoft.com/fwlink/?linkid=117786)  
  
 [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
