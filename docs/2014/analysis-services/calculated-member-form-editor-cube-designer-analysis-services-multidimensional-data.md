---
title: Calcula el Editor de formulario de miembro (pestaña cálculos, Diseñador de cubos) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationexpression.calculatedmember.f1
ms.assetid: f7719b9e-b1e6-4792-90a6-30d9d8eb1196
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a16319b01c6555aa3bf299da201d9662cd59f4b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049115"
---
# <a name="calculated-member-form-editor-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulario de miembro calculado (pestaña Cálculos, Diseñador de cubos) (Analysis Services -  Datos multidimensionales)
  Utilice el panel del **Editor de Formulario de miembro calculado** de la pestaña **Cálculos** del Diseñador de cubos para crear o modificar un miembro calculado.  
  
 **Nota** Este panel solamente se muestra en la vista de formulario.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba el nombre del miembro calculado.  
  
 **Propiedades del miembro primario**  
 Expanda esta opción para ver las opciones **Jerarquía primaria**, **Miembro primario**y **Cambiar** .  
  
 **Jerarquía primaria**  
 Seleccione la dimensión y la jerarquía del cubo seleccionado que debe incluir el miembro calculado. Seleccione MEASURES para definir una medida calculada.  
  
 **Miembro primario**  
 Seleccione el miembro bajo el que debe aparecer el miembro calculado.  
  
 **Nota** Esta opción está disponible si **Jerarquía primaria** especifica una jerarquía distinta de MEASURES.  
  
 **Cambio**  
 Seleccione esta opción para mostrar el cuadro de diálogo **Seleccionar miembro primario** y, luego, un miembro para **Miembro primario**. Para más información sobre el cuadro de diálogo **Seleccionar miembro primario**, vea [Cuadro de diálogo Seleccionar miembro primario &#40;Analysis Services - Datos multidimensionales&#41;](select-parent-member-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Expresión**  
 Expanda esta opción para ver o modificar la expresión MDX (Expresiones multidimensionales) para el miembro calculado.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
> [!NOTE]  
>  Es recomendable que esta expresión se evalúe como una cadena o un valor numérico.  
  
 **Propiedades adicionales**  
 Expanda para ver las opciones **Cadena de formato**, **Visible**, **Comportamiento si no está vacío**, **Expresiones de color**y **Expresiones de fuente** .  
  
 **Cadena de formato**  
 Escriba la cadena de formato MDX utilizada para dar formato al valor que devuelve el miembro calculado o seleccione una cadena de formato predefinida.  
  
 Para más información sobre las cadenas de forato MDX, vea [FORMAT_STRING, contenido &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md).  
  
 **Visible**  
 Seleccione **True** para permitir que las aplicaciones cliente vean el miembro calculado.  
  
 **Comportamiento no está vacío**  
 Seleccione el nombre de la medida utilizada para resolver las consultas NON EMPTY en MDX para el miembro calculado. Si la propiedad **Comportamiento si no está vacío** está en blanco, es necesario evaluar el miembro calculado repetidamente para determinar si está vacío. Si la propiedad **Comportamiento si no está vacío** contiene el nombre de una medida, el miembro calculado se trata como si estuviera vacío si la medida especificada está vacía.  
  
> [!WARNING]  
>  Esta propiedad está en desuso. No la active. Consulte [en desuso características de Analysis Services en SQL Server 2014](deprecated-analysis-services-features-in-sql-server-2014.md) para obtener más información.  
  
 **Expresiones de color**  
 Expanda para ver las opciones **Color en primer plano** y **Color de fondo** .  
  
 **Color de primer plano**  
 Escriba la expresión MDX que proporciona el color del primer plano del miembro calculado.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 Haga clic en el botón de selección del color para mostrar el cuadro de diálogo **Color** e inserte el valor RGB (rojo-verde-azul) para un color específico en la expresión MDX. Para más información sobre los valores RGB, vea [Contenido de FORE_COLOR y BACK_COLOR &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).  
  
 **Color de fondo**  
 Escriba la expresión MDX que proporciona el color de fondo del miembro calculado.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 Haga clic en el botón de selección del color para mostrar el cuadro de diálogo **Color** e inserte el valor RGB (rojo-verde-azul) para un color específico en la expresión MDX. Para más información sobre los valores RGB, vea [Contenido de FORE_COLOR y BACK_COLOR &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md).  
  
 **Expresiones de fuente**  
 Expanda para ver las opciones **Nombre de fuente**, **Tamaño de fuente**e **Indicadores de fuente** .  
  
 **Nombre de fuente**  
 Escriba la expresión MDX que proporciona el nombre de la fuente utilizada para el miembro calculado.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 Haga clic en el botón de selección de fuentes para mostrar el cuadro de diálogo **Fuente** e inserte los valores de propiedad para una fuente determinada en la expresión MDX. Para más información sobre valores de propiedades, vea [Crear y usar los valores de propiedad &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
 **Tamaño de fuente**  
 Escriba la expresión MDX que proporciona el tamaño de la fuente utilizada para el miembro calculado.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 Haga clic en el botón de selección de fuentes para mostrar el cuadro de diálogo **Fuente** e inserte los valores de propiedad para una fuente determinada en la expresión MDX. Para más información sobre valores de propiedades, vea [Crear y usar los valores de propiedad &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
 **Marcas de fuente**  
 Escriba la expresión MDX que proporciona el valor de mapa de bits que contiene las marcas de fuente, como subrayado o negrita, de la fuente utilizada para el miembro calculado.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 Haga clic en el botón de selección de fuentes para mostrar el cuadro de diálogo **Fuente** e inserte los valores de propiedad para una fuente determinada en la expresión MDX. Para más información sobre valores de propiedades, vea [Crear y usar los valores de propiedad &#40;MDX&#41;](creating-and-using-property-values-mdx.md).  
  
## <a name="see-also"></a>Vea también  
 [Cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [Crear miembros calculados](multidimensional-models/create-calculated-members.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Cálculos &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña cálculos, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de script &#40;pestaña cálculos, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Herramientas de cálculo &#40;pestaña cálculos, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](calculation-tools-cube-designer-analysis-services-multidimensional-data.md)   
 [Denominada Editor de formulario de conjunto &#40;pestaña cálculos, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de script &#40;pestaña cálculos, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
