---
title: Elegir mejora (Asistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.bienhancement.f1
ms.assetid: 39e2f36c-2c02-4a71-af8f-5dbd373190dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 687f7fb96ee5a2b96d80562c20d536eeeb308379
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088114"
---
# <a name="choose-enhancement-business-intelligence-wizard"></a>Elegir mejora (Asistente de Business Intelligence)
  Use la página **Elegir mejora** para elegir la mejora de Business Intelligence que se agregará al cubo o a la dimensión.  
  
## <a name="options"></a>Opciones  
 **Mejoras disponibles**  
 Seleccione la mejora de Business Intelligence que se agregará. En la tabla siguiente se enumeran las mejoras disponibles.  
  
|Mejora|Descripción|  
|-----------------|-----------------|  
|**Definir la inteligencia de tiempo**|Agrega vistas de tiempo adicionales a una jerarquía seleccionada. Incluye vistas de período hasta fecha, media rotatoria y período hasta período.<br /><br /> Nota: Esta opción solo está disponible para cubos.|  
|**Definir la inteligencia de cuentas**|Asigna clasificaciones de cuentas estándar, como ingresos y gastos, para miembros de un atributo de cuenta.<br /><br /> Si la función de agregación para la medida se establece en *ByAccount*, la instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa las clasificaciones de cuentas para agregar una medida a los miembros de un atributo de cuenta en el tiempo.|  
|**Definir la inteligencia de dimensiones**|Utilice la inteligencia de dimensiones para especificar un tipo de negocio estándar para una dimensión y especificar tipos válidos para los atributos de la dimensión. Las aplicaciones cliente pueden utilizar estas especificaciones de tipos al analizar datos.|  
|**Especificar un operador unario**|Especifique un operador unario para reemplazar la agregación predeterminada asociada a miembros de una jerarquía de elementos primarios y secundarios incluida en un cubo.<br /><br /> Nota: Esta opción solo está disponible para cubos.|  
|**Crear una fórmula de miembro personalizado**|Cree una fórmula de miembro personalizado para reemplazar la agregación predeterminada asociada a miembros de una dimensión con otro operador.|  
|**Especificar el orden de los atributos**|Especifique cómo se ordenan los miembros de un atributo seleccionado. Pueden ordenarse por el nombre o la clave del atributo seleccionado o por el nombre o la clave de un atributo relacionado con el atributo seleccionado. De forma predeterminada, los miembros se ordenan por el nombre del atributo seleccionado.|  
|**Habilitar reescritura en la dimensión**|Habilite la modificación manual de la estructura de la dimensión. Las actualizaciones de una dimensión habilitada para escritura se registran directamente en la tabla de dimensiones.|  
|**Definir el comportamiento de suma parcial**|Define manualmente el método de agregación para medidas o miembros individuales de un atributo de tipo de cuenta. Si el cubo contiene una dimensión de cuenta, puede usar la opción **Definir la inteligencia de cuentas** para establecer automáticamente el comportamiento de suma parcial basado en el tipo de cuenta.<br /><br /> Nota: Esta opción solo está disponible para cubos.|  
|**Definir la conversión de moneda**|Define las reglas de conversión y análisis de datos multinacionales en el cubo. Las reglas de conversión se aplican al cubo utilizando un script MDX (Expresiones multidimensionales) generado por el Asistente de Business Intelligence.<br /><br /> Nota: Esta opción solo está disponible para cubos.|  
  
 **Descripción**  
 Proporciona una breve descripción de la mejora de Business Intelligence seleccionada.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente de Business Intelligence (ayuda F1)](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services de datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services de datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
