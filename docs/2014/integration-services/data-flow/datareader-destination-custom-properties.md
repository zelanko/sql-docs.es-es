---
title: Propiedades personalizadas del destino DataReader | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 948ebbc696048915662caaa24b791e6258c459be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827609"
---
# <a name="datareader-destination-custom-properties"></a>Propiedades personalizadas del destino DataReader
  El destino DataReader tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino DataReader. Todas las propiedades excepto `DataReader` son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|DataReader|String|Nombre de clase del destino DataReader.|  
|FailOnTimeout|Boolean|Indica si generar un error cuando se produce un `ReadTimeout`. El valor predeterminado de esta propiedad es **False**.|  
|ReadTimeout|Entero|Número de milisegundos que transcurren antes de que se agote el tiempo de espera. El valor predeterminado de esta propiedad es 30000 (30 segundos).|  
  
 La entrada y las columnas de entrada del destino DataReader no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [DataReader Destination](datareader-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](../common-properties.md)  
  
  
