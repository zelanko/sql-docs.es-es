---
title: Especificar recuentos de objetos (Asistente para optimización basada en uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5578f6ef177a6d4b638dac5fdef947147124e18
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201885"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>Especificar recuentos de objetos (Asistente para optimización basada en el uso)
  Use la página **Especificar recuentos de objetos** para calcular automáticamente el recuento de objetos en el cubo o escribir manualmente los recuentos estimados. El Asistente para optimización basada en el uso utiliza los recuentos de objetos para estimar los requisitos de almacenamiento.  
  
## <a name="options"></a>Opciones  
 **Objetos de cubo**  
 Muestra las dimensiones y los atributos del cubo. Solo los atributos que no tienen sus `AggregationUsage` propiedad establecida en None en la **revisar el uso de agregación** página del asistente se muestran porque éstos son los únicos atributos que se deben especificar los recuentos.  
  
 **Recuento estimado**  
 Muestra el número estimado de filas en el grupo de medida y los recuentos estimados de miembros del atributo en las dimensiones de base de datos. Puede escribir un valor para utilizarlo como recuento estimado o calcular los valores estimados del recuento. Para calcular los valores de recuento, escriba 0 en el campo y, a continuación, haga clic en **Recuento**. Los campos que muestren un recuento no están actualizados.  
  
 **Recuento de particiones**  
 (Opcional) Escriba el número estimado de filas en el grupo de medida y los recuentos estimados de miembros del atributo en las particiones.  
  
 **Count**  
 Calcula y rellena los valores de la columna **Recuento estimado** para todos los campos vacíos. Los campos que muestren un recuento no están actualizados.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 del Asistente de diseño de agregación](aggregation-design-wizard-f1-help.md)   
 [Asistentes de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
