---
title: Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM | Microsoft Docs
description: Compruebe si la opción PAGE_VERIFY es CHECKSUM, que controla si el Motor de base de datos de SQL Server calcula una suma de comprobación para ayudar a proporcionar integridad de los archivos de datos.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5f296dc9aedf96c3258dc256d9bc8fc8fdf05f12
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774174"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM.
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regla comprueba si la opción de base de datos PAGE_VERIFY está establecida en CHECKSUM. Cuando CHECKSUM se habilita para la opción de base de datos PAGE_VERIFY, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula una suma de comprobación teniendo en cuenta el contenido de toda la página y almacena el valor en el encabezado de página cuando esta se escribe en el disco. Si la página se lee desde el disco, la suma de comprobación se vuelve a calcular y se compara con el valor de suma de comprobación que está almacenado en el encabezado de página. De este modo se ayuda a proporcionar un alto nivel de integridad de los archivos de datos.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos PAGE_VERIFY en CHECKSUM.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
