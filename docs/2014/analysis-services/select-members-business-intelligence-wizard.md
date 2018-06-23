---
title: Seleccionar miembros (Asistente de Business Intelligence) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 75cd6c2aeca77d55b4ec66baa3dccb4c77f4a66e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198284"
---
# <a name="select-members-business-intelligence-wizard"></a>Seleccionar miembros (Asistente de Business Intelligence)
  Utilice la página **Seleccionar miembros** para determinar a qué miembros del Asistente de Business Intelligence se debe aplicar la función de conversión de moneda especificada en la página **Establecer las opciones de conversión de moneda** .  
  
> [!NOTE]  
>  Esta página no aparece si se ha iniciado el Asistente de Business Intelligence desde el Diseñador de dimensiones o al hacer clic con el botón derecho en una dimensión del Explorador de soluciones de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opciones  
 **Dimensión de medidas**  
 Seleccione esta opción para aplicar la función de conversión de moneda a una o varias medidas del cubo.  
  
 Si está seleccionada, la cuadrícula muestra las opciones enumeradas en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Tipos de medidas integradas**|Seleccione esta opción para incluir la función de conversión de moneda correspondiente a la medida especificada.|  
|**Medidas**|Seleccione la medida del grupo de medida de tarifas que contiene la tasa de cambio que se va a usar cuando se convierta la medida seleccionada en **Tipos de medida integrados** .|  
  
 **Jerarquía de cuentas**  
 Seleccione esta opción para aplicar la función de conversión de moneda a uno o varios miembros de la jerarquía de cuentas correspondiente a la dimensión de cuenta incluida en el cubo. La jerarquía de cuentas es la jerarquía dentro de la cuenta de dimensión cuya `Type` propiedad está establecida en *cuenta*.  
  
 Si está seleccionada, la cuadrícula muestra las opciones enumeradas en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Miembro de la cuenta**|Seleccione esta opción para incluir la función de conversión de moneda correspondiente al miembro especificado de la jerarquía de cuentas.|  
|**Medidas**|Seleccione la medida del grupo de medida de tarifas que contiene la tasa de cambio que se va a utilizar cuando se conviertan las medidas correspondientes al miembro seleccionado en **Miembro de la cuenta** .|  
  
 **Jerarquía de cuentas basada en el tipo**  
 Seleccione esta opción para aplicar la función de conversión de moneda a todos los miembros de atributos en la jerarquía de cuentas cuya `Type` propiedad está establecida en un tipo de cuenta especificado.  
  
 Si está seleccionada, la cuadrícula muestra las opciones enumeradas en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Tipo de cuenta**|Seleccione esta opción para incluir la función de conversión de moneda correspondiente al tipo de cuenta especificado.|  
|**Medidas**|Seleccione la medida del grupo de medida de tarifas que contiene la tasa de cambio que se va a utilizar cuando se conviertan los miembros de los atributos utilizando el tipo de cuenta seleccionado en **Tipo de cuenta** .|  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 de Asistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  