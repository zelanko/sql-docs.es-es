---
title: Especificar recuentos de objetos (Asistente para diseñar agregaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 305d9d79-d1ab-4704-a7b5-3283842b3996
author: minewiskan
ms.author: owend
ms.openlocfilehash: c66b972395f86746b2d08df234db8aa0c71d03fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940326"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>Especificar recuentos de objetos (Asistente para diseñar agregaciones)
  Use la página **Especificar recuentos de objetos** para calcular automáticamente el recuento de objetos en el cubo o escribir manualmente los recuentos estimados. El Asistente para diseñar agregaciones utiliza los recuentos de objetos para estimar los requisitos de almacenamiento.  
  
## <a name="options"></a>Opciones  
 **Objetos de cubo**  
 Muestra las dimensiones y los atributos del cubo. Solo se muestran los atributos que no tienen la `AggregationUsage` propiedad establecida `None` en en la página **revisar el uso de agregaciones** del asistente, ya que son los únicos atributos que requieren que se especifiquen los recuentos.  
  
 **Recuento estimado**  
 Muestra el número estimado de filas en el grupo de medida y los recuentos estimados de miembros del atributo en las dimensiones de base de datos. Puede escribir un valor para utilizarlo como recuento estimado o calcular los valores estimados del recuento. Para calcular los valores de recuento, escriba `0` en el campo y, a continuación, haga clic en **recuento**. Los campos que muestren un recuento no están actualizados.  
  
 **Número de particiones**  
 (Opcional) Escriba el número estimado de filas en el grupo de medida y el tipo de los recuentos estimados de miembros del atributo en las particiones.  
  
 **Recuento**  
 Calcula y rellena los valores de la columna **Recuento estimado** para todos los campos vacíos. Los campos que muestren un recuento no están actualizados.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para diseñar agregaciones (ayuda F1)](aggregation-design-wizard-f1-help.md)   
 [Analysis Services asistentes &#40;datos multidimensionales&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
