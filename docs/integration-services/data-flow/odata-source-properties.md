---
title: Propiedades de origen OData | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 64e297a37c3b6449551968b5788f8c2c0ddd4ab6
ms.contentlocale: es-es
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source-properties"></a>Propiedades de orígenes OData
Cuando hace doble clic en **origen OData** en el flujo de datos y haga clic en **propiedades**, ver las propiedades de la **origen OData** componente en el **propiedades** ventana.  

## <a name="properties"></a>Propiedades 
|Propiedad|Description|  
|-|-|  
|CollectionName|Nombre de la colección para recuperar del servicio OData. La propiedad **CollectionName** se usa cuando **UseResourcePath** es False.<br /><br /> Esta propiedad es expressionable, que permite establecer el valor en tiempo de ejecución. Sin embargo, si los metadatos de la colección no coinciden con los que existían en tiempo de diseño, produce un error de validación, haciendo que la ejecución del flujo de datos producirá un error.|  
|DefaultStringLength|Este valor especifica la longitud predeterminada de las columnas de cadena que no tienen ninguna longitud máxima.<br /><br /> **Valor predeterminado:** 4000|  
|Query|Parámetros de consulta OData. Esta propiedad es expressionable y se puede establecer en tiempo de ejecución.|  
|ResourcePath|Use esta propiedad cuando necesite especificar una ruta de acceso completa a recursos, en lugar de seleccionar simplemente el nombre de una colección. Esta propiedad se usa cuando **UseResourcePath** es True.|  
|UseResourcePath|Cuando se establece en True, el valor **ResourcePath** se anexa a la dirección URL base para determinar la ubicación de la fuente OData. Cuando se establece en False, se usa el valor **CollectionName** .<br /><br /> **Valor predeterminado:** False|  
  
## <a name="see-also"></a>Vea también
[Origen OData](odata-source.md)

