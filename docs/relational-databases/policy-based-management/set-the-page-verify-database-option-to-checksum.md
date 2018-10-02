---
title: Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20f97815b85b7cf88baad386bda43596c5ac81a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784633"
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si la opción de base de datos PAGE_VERIFY está establecida en CHECKSUM. Cuando CHECKSUM se habilita para la opción de base de datos PAGE_VERIFY, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula una suma de comprobación teniendo en cuenta el contenido de toda la página y almacena el valor en el encabezado de página cuando esta se escribe en el disco. Si la página se lee desde el disco, la suma de comprobación se vuelve a calcular y se compara con el valor de suma de comprobación que está almacenado en el encabezado de página. De este modo se ayuda a proporcionar un alto nivel de integridad de los archivos de datos.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos PAGE_VERIFY en CHECKSUM.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
