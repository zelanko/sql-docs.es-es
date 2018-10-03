---
title: Revise el uso de agregaciones (Asistente para optimización basada en uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.reviewaggregationusage.f1
ms.assetid: 49ce2094-c4dc-4e46-8cef-c17c5db084ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a50c241bc70d48577b558827a278d5423ee8344b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164055"
---
# <a name="review-aggregation-usage-usage-based-optimiation-wizard"></a>Revisar el uso de agregaciones (Asistente para optimización basada en el uso)
  Utilice la página **Revisar el uso de agregaciones** para configurar el uso de agregaciones.  
  
## <a name="options"></a>Opciones  
 **Default**  
 Seleccione esta opción para establecer como predeterminada la configuración del uso de agregaciones del atributo. Esta configuración permite que el diseñador aplique una regla predeterminada basada en el tipo de atributo y dimensión.  
  
 **Completa**  
 Seleccione esta opción para establecer la configuración del uso de agregaciones del atributo en Full. Con esta configuración es necesario que cada agregación del cubo incluya ese atributo o un atributo relacionado que tenga un valor inferior en la cadena de atributos. Se recomienda no establecer la configuración del uso de agregaciones en Full cuando un atributo contiene muchos miembros. Cuando la configuración se ha especificado para varios atributos o atributos con varios miembros, es posible que esta configuración impida que se diseñen las agregaciones debido a un tamaño excesivo.  
  
 **Ninguno**  
 Seleccione esta opción para establecer la configuración del uso de agregaciones del atributo en None. Con esta configuración ninguna agregación del cubo puede incluir el atributo.  
  
 **Sin restricciones**  
 Seleccione esta opción para establecer la configuración del uso de agregaciones del atributo en Unrestricted. Esta configuración impide que se coloquen las restricciones en el diseñador de agregaciones. Sin embargo, el atributo todavía se tiene que evaluar para determinar si es un candidato importante de la agregación.  
  
 **Establezca todas en la configuración predeterminada**  
 Seleccione esta opción para establecer como predeterminada la configuración del uso de agregaciones de todos atributos.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 del Asistente de diseño de agregación](aggregation-design-wizard-f1-help.md)   
 [Asistentes de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
