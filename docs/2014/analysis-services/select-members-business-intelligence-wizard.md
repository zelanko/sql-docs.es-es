---
title: Seleccione los miembros (Asistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cc66896eb1735d09991644dd49c03b5a94c208d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069432"
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
|**Tipos de medida integrados**|Seleccione esta opción para incluir la función de conversión de moneda correspondiente a la medida especificada.|  
|**Medidas**|Seleccione la medida del grupo de medida de tarifas que contiene la tasa de cambio que se va a usar cuando se convierta la medida seleccionada en **Tipos de medida integrados** .|  
  
 **Jerarquía de cuentas**  
 Seleccione esta opción para aplicar la función de conversión de moneda a uno o varios miembros de la jerarquía de cuentas correspondiente a la dimensión de cuenta incluida en el cubo. La jerarquía de cuentas es la dimensión de la jerarquía dentro de la cuenta cuya `Type` propiedad está establecida en *cuenta*.  
  
 Si está seleccionada, la cuadrícula muestra las opciones enumeradas en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Miembro de la cuenta**|Seleccione esta opción para incluir la función de conversión de moneda correspondiente al miembro especificado de la jerarquía de cuentas.|  
|**Medidas**|Seleccione la medida del grupo de medida de tarifas que contiene la tasa de cambio que se va a utilizar cuando se conviertan las medidas correspondientes al miembro seleccionado en **Miembro de la cuenta** .|  
  
 **Según el tipo de jerarquía de cuentas**  
 Seleccione esta opción para aplicar la función de conversión de moneda a todos los miembros de los atributos de la jerarquía de cuentas, cuya propiedad `Type` esté establecida en un tipo de cuenta especificado.  
  
 Si está seleccionada, la cuadrícula muestra las opciones enumeradas en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Tipo de cuenta**|Seleccione esta opción para incluir la función de conversión de moneda correspondiente al tipo de cuenta especificado.|  
|**Medidas**|Seleccione la medida del grupo de medida de tarifas que contiene la tasa de cambio que se va a utilizar cuando se conviertan los miembros de los atributos utilizando el tipo de cuenta seleccionado en **Tipo de cuenta** .|  
  
## <a name="see-also"></a>Vea también  
 [Asistente de Business Intelligence (Ayuda F1)](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
