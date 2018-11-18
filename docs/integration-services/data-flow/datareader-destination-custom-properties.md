---
title: Propiedades personalizadas del destino DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c54d0c7c254f07d06c34ffc3860d03d8ccfba124
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51638233"
---
# <a name="datareader-destination-custom-properties"></a>Propiedades personalizadas del destino DataReader
  El destino DataReader tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino DataReader. Todas las propiedades excepto **DataReader** son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|DataReader|String|Nombre de clase del destino DataReader.|  
|FailOnTimeout|Boolean|Indica si generar un error cuando se produce un **ReadTimeout** . El valor predeterminado de esta propiedad es **False**.|  
|ReadTimeout|Integer|Número de milisegundos que transcurren antes de que se agote el tiempo de espera. El valor predeterminado de esta propiedad es 30000 (30 segundos).|  
  
 La entrada y las columnas de entrada del destino DataReader no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [DataReader Destination](../../integration-services/data-flow/datareader-destination.md).  
  
## <a name="see-also"></a>Ver también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
