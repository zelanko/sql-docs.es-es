---
description: Establecer la opción de base de datos AUTO_SHRINK en OFF
title: Establecer la opción de base de datos AUTO_SHRINK en OFF | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bff50dd9a7ee85cf94f378f2967551b43ef108f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428107"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>Establecer la opción de base de datos AUTO_SHRINK en OFF
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regla comprueba si la opción de base de datos AUTO_SHRINK está establecida en OFF. Si se reduce y se expande con frecuencia una base de datos, puede provocar la fragmentación física.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos AUTO_SHRINK en OFF. Si sabe que el espacio que está reclamando no se va a necesitar en el futuro, puede reclamarlo reduciendo manualmente la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 Artículo [315512](https://go.microsoft.com/fwlink/?linkid=117750)de Microsoft Knowledge Base  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
