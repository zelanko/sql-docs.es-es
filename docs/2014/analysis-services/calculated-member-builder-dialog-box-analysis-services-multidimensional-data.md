---
title: Calcula el cuadro de diálogo del generador de miembros (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.calculatedmemberbuilderdialog.f1
ms.assetid: 73b89a9f-f403-4ab8-99f7-e3ceb870c260
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c11d690ce6e240d9054da37ff9b85632b0d831ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077275"
---
# <a name="calculated-member-builder-dialog-box-analysis-services---multidimensional-data"></a>Generador de miembros calculados (Cuadro de diálogo) (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Generador de miembros calculados** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para generar un miembro calculado.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Nombre**|Escriba el nombre del miembro calculado.|  
|**Jerarquía primaria**|Seleccione la jerarquía en la que desea crear el miembro calculado.|  
|**Miembro primario**|Esta opción se habilita si selecciona una jerarquía primaria (que no sea el `Measures` dimensión) que tiene más de un nivel. Haga clic en el botón de puntos suspensivos (**…**) para seleccionar un miembro primario. El miembro primario determina la ubicación del miembro calculado en la estructura de dimensión.|  
|**Expresión**|Escriba la expresión MDX que se utilizará.|  
|**Comprobación**|Haga clic en **Comprobar** para probar la expresión MDX definida en **Expresión**.|  
|**Metadatos**|Muestra los metadatos del objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] actual que pueden incluirse en la expresión MDX definida en **Expresión**.<br /><br /> Para copiar la sintaxis MDX del elemento seleccionado, haga clic con el botón derecho en el elemento y seleccione **Copiar**, o arrastre el elemento seleccionado a **Expresión**.|  
|**Funciones**|Muestra las funciones de MDX disponibles para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] actual. Los elementos enumerados se recuperan del conjunto de filas del esquema MDSCHEMA_FUNCTIONS.<br /><br /> Para copiar la sintaxis MDX del elemento seleccionado, haga clic con el botón derecho en el elemento y seleccione **Copiar**, o arrastre el elemento seleccionado a **Expresión**.|  
  
## <a name="see-also"></a>Vea también  
 [Expresiones multidimensionales &#40;MDX&#41; referencia](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
