---
title: Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fe1a48e74503e93199a6e91f8b9aa60c21bb9ee1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62691527"
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM.
  Esta regla comprueba si la opción de base de datos PAGE_VERIFY está establecida en CHECKSUM. Cuando CHECKSUM se habilita para la opción de base de datos PAGE_VERIFY, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula una suma de comprobación teniendo en cuenta el contenido de toda la página y almacena el valor en el encabezado de página cuando esta se escribe en el disco. Si la página se lee desde el disco, la suma de comprobación se vuelve a calcular y se compara con el valor de suma de comprobación que está almacenado en el encabezado de página. De este modo se ayuda a proporcionar un alto nivel de integridad de los archivos de datos.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos PAGE_VERIFY en CHECKSUM.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  
