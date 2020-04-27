---
title: Revisar el uso de agregaciones (Asistente para diseñar agregaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f52ec05ddadc6bb23968f6b5f8ee7fda9adc65a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070218"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>Revisar el uso de agregaciones (Asistente para diseño de agregaciones)
  Utilice la página **Revisar el uso de agregaciones** para configurar el uso de agregaciones.  
  
## <a name="options"></a>Opciones  
 **Valor predeterminado**  
 Seleccione esta opción para establecer como predeterminada la configuración del uso de agregaciones del atributo. Esta configuración permite que el diseñador aplique una regla predeterminada basada en el tipo de atributo y dimensión.  
  
 `Full`  
 Seleccione esta opción para establecer la configuración del uso de agregaciones del atributo en `Full`. Con esta configuración es necesario que cada agregación del cubo incluya ese atributo o un atributo relacionado que tenga un valor inferior en la cadena de atributos. Se recomienda no establecer el valor `Full` del uso de agregaciones cuando un atributo contiene muchos miembros. Cuando la configuración se ha especificado para varios atributos o atributos con varios miembros, es posible que esta configuración impida que se diseñen las agregaciones debido a un tamaño excesivo.  
  
 **None**  
 Seleccione esta opción para establecer la configuración del uso de agregaciones del atributo en None. Con esta configuración ninguna agregación del cubo puede incluir el atributo.  
  
 `Unrestricted`  
 Seleccione esta opción para establecer la configuración del uso de agregaciones del atributo en `Unrestricted`. Esta configuración impide que se coloquen restricciones en el diseñador de agregaciones. Sin embargo, es necesario que el atributo se evalúe para determinar si es un candidato importante de la agregación.  
  
 **Set All to Default**  
 Seleccione esta opción para establecer como predeterminada la configuración del uso de agregaciones de todos atributos.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para diseñar agregaciones (ayuda F1)](aggregation-design-wizard-f1-help.md)   
 [Analysis Services asistentes &#40;datos multidimensionales&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
