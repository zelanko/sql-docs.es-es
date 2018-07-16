---
title: Cambiar el texto de un elemento de leyenda (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b9e18fe47a84785d7450a481c1eb6f1173b8bcf9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292135"
---
# <a name="change-the-text-of-a-legend-item-report-builder-and-ssrs"></a>Cambiar el texto de un elemento de leyenda (Generador de informes y SSRS)
  Cuando se coloca un campo en el área Valores del gráfico, se genera automáticamente un elemento de leyenda que contiene el nombre de este campo. Cada elemento de leyenda se conecta a una serie individual del gráfico, a excepción de los gráficos de formas, donde la leyenda se conecta a puntos de datos individuales en lugar de a series individuales.  
  
 En los gráficos de formas, puede cambiar el texto de un elemento de leyenda para mostrar más información sobre los puntos de datos individuales. Por ejemplo, si desea mostrar los valores de los puntos de datos como porcentajes en la leyenda, puede usar una palabra clave como `#PERCENT`. Puede anexar códigos de formato de .NET Framework junto con las palabras clave para aplicar formatos numéricos y de fecha. Para obtener más información sobre las palabras clave, vea [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
 ![Gráfico nítido](../media/sharpchart.png "Gráfico nítido")  
  
 En los gráficos que no son de formas, puede cambiar el texto de un elemento de leyenda. Por ejemplo, si la serie se denomina "Serie1", es posible que desee cambiar el texto por otro más descriptivo como "Ventas para 2008".  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>Para modificar el texto que aparece en la leyenda en un gráfico de formas  
  
1.  Haga clic con el botón derecho en una serie o en un campo del área **Valores** y seleccione **Propiedades de la serie**.  
  
2.  Haga clic en **Leyenda** y, en el cuadro **Texto de leyenda personalizado** , escriba una palabra clave.  
  
 En la tabla siguiente se proporcionan ejemplos de palabras clave específicas de los gráficos que pueden usarse para la propiedad **Texto de leyenda personalizado** . Para obtener más información sobre las palabras clave, vea [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
|Palabra clave|Descripción|El ejemplo de lo que aparece como texto en la leyenda|  
|-------------|-----------------|---------------------------------------------------|  
|`#PERCENT{P1}`|Muestra el porcentaje del valor total con un decimal.|85.0%|  
|`#VALY`|Muestra el valor numérico real del campo de datos.|17000|  
|`#VALY{C2}`|Muestra el valor numérico real del campo de datos con formato monetario y con dos decimales.|$17000.00|  
|`#AXISLABEL (#PERCENT{P0})`|Muestra la representación de texto del campo de categorías, seguida por el porcentaje que cada categoría representa en el gráfico.|Michael Blythe (85%)|  
  
> [!NOTE]  
>  La palabra clave #AXISLABEL solo se puede evaluar en tiempo de ejecución cuando no se especifica ningún campo en el área **Grupos de la serie** .  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-non-shape-chart"></a>Para modificar el texto que aparece en la leyenda en un gráfico que no es de formas  
  
1.  Haga clic con el botón derecho en una serie o en un campo del área **Valores** y seleccione **Propiedades de la serie**.  
  
2.  Haga clic en **Leyenda** y, en el cuadro **Texto de leyenda personalizado** , escriba una etiqueta de leyenda. La serie se actualizada con el texto especificado.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a la leyenda en un gráfico &#40;generador de informes y SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Aplicar formato a los colores de serie de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Ocultar elementos de leyenda en el gráfico &#40;Generador de informes y SSRS&#41;](chart-legend-hide-items-report-builder.md)  
  
  
