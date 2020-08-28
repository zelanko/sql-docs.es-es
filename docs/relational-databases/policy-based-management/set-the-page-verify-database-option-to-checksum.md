---
title: Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM | Microsoft Docs
description: Compruebe si la opción PAGE_VERIFY es CHECKSUM, que controla si el Motor de base de datos de SQL Server calcula una suma de comprobación para ayudar a proporcionar integridad de los archivos de datos.
ms.custom: ''
ms.date: 08/19/2020
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
ms.openlocfilehash: 4dda2b9138882490b1556b9dbb39f71e35767f5f
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646515"
---
# <a name="set-the-page_verify-database-option-to-checksum"></a>Establecer la opción de base de datos PAGE_VERIFY en CHECKSUM.
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regla comprueba si la opción de base de datos PAGE_VERIFY está establecida en CHECKSUM. Cuando CHECKSUM se habilita para la opción de base de datos PAGE_VERIFY, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula una suma de comprobación teniendo en cuenta el contenido de toda la página y almacena el valor en el encabezado de página cuando esta se escribe en el disco. Si la página se lee desde el disco, la suma de comprobación se vuelve a calcular y se compara con el valor de suma de comprobación que está almacenado en el encabezado de página. De este modo se ayuda a proporcionar un alto nivel de integridad de los archivos de datos.  Si usa la opción PAGE_VERIFY en CHECKSUM para una base de datos, cuando SQL Server detecta que una página se ha modificado después de haberse escrito en el disco, SQL Server emite el [mensaje 824](../errors-events/mssqlserver-824-database-engine-error.md) tras volver a leer la página desde el disco. 
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos PAGE_VERIFY en CHECKSUM. Usar la opción de base de datos PAGE_VERIFY en CHECKSUM permite detectar de la forma más sólida los problemas de coherencia en la base de datos causados por la ruta de acceso de E/S del sistema.
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
