---
title: Especificar recuentos de objetos (Asistente para optimización basada en el uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 306c7c25-ae24-4852-ab8c-c82f68a4bc1f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0503192c3c948110f8301c8eb375e1c8203e42f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068234"
---
# <a name="specify-object-counts-usage-based-optimization-wizard"></a>Especificar recuentos de objetos (Asistente para optimización basada en el uso)
  Use la página **Especificar recuentos de objetos** para calcular automáticamente el recuento de objetos en el cubo o escribir manualmente los recuentos estimados. El Asistente para optimización basada en el uso utiliza los recuentos de objetos para estimar los requisitos de almacenamiento.  
  
## <a name="options"></a>Opciones  
 **Objetos de cubo**  
 Muestra las dimensiones y los atributos del cubo. Solo se muestran los atributos que no tienen `AggregationUsage` la propiedad establecida en None en la página **revisar el uso de agregaciones** del asistente, ya que son los únicos atributos que necesitan que se especifiquen los recuentos.  
  
 **Recuento estimado**  
 Muestra el número estimado de filas en el grupo de medida y los recuentos estimados de miembros del atributo en las dimensiones de base de datos. Puede escribir un valor para utilizarlo como recuento estimado o calcular los valores estimados del recuento. Para calcular los valores de recuento, escriba 0 en el campo y luego haga clic en **Recuento**. Los campos que muestren un recuento no están actualizados.  
  
 **Recuento de particiones**  
 (Opcional) Escriba el número estimado de filas en el grupo de medida y los recuentos estimados de miembros del atributo en las particiones.  
  
 **Contabiliza**  
 Calcula y rellena los valores de la columna **Recuento estimado** para todos los campos vacíos. Los campos que muestren un recuento no están actualizados.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para diseñar agregaciones (ayuda F1)](aggregation-design-wizard-f1-help.md)   
 [Analysis Services asistentes &#40;datos multidimensionales&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
