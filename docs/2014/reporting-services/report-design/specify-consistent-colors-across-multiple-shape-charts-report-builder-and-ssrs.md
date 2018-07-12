---
title: Especificar colores coherentes en varios gráficos de formas (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 588df3c7dae6d5d2a96a3662123af5eca20398f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200725"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>Especificar colores coherentes en varios gráficos de formas (Generador de informes y SSRS)
  En los gráficos que no son de formas, se selecciona un nuevo color de la paleta en función del índice de series del gráfico. Por ejemplo, la primera serie del gráfico se asignará al primer color de la paleta. Sin embargo, este comportamiento difiere para los gráficos de formas. En los gráficos de formas, cada color de la paleta se asigna a un punto de datos del conjunto de datos. Por ejemplo, el punto de datos 1 se asigna al primer color de la paleta, el punto de datos 2 se asigna al segundo color de la paleta, etc.  
  
 Si un punto de datos no tiene ningún valor, se omite de la presentación en un gráfico de formas. Esto significa que el punto de datos no se colorea. Por ejemplo, si el punto 2 tiene un valor de cero, el punto 1 se asignará al primer color de la paleta y el punto 3 se asignará al segundo color de la paleta. Este método resulta útil porque los puntos vacíos del conjunto de datos de un gráfico circular no usan innecesariamente un color de la paleta cuando no es necesario dibujar el punto vacío.  
  
 Como efecto secundario, cuando se muestran varios gráficos circulares en un informe, dichos gráficos pueden mostrar colores diferentes para puntos de datos que tienen la misma agrupación de categoría. Para solucionarlo, debe definir colores individuales que se asignen a un grupo de categorías en lugar de a valores de datos individuales. Cómo lo haga depende de si los gráficos de formas son minigráficos en una tabla o matriz, o son gráficos de formas en el propio informe.  
  
 La leyenda está conectada a la serie, de modo que cualquier color que especifique para ésta se mostrará automáticamente en la leyenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>Para especificar colores coherentes en varios gráficos de formas que son minigráficos en una tabla o matriz  
  
1.  Haga clic en el gráfico para mostrar el panel Datos del gráfico.  
  
2.  En el área **Grupos de categorías** , haga clic con el botón derecho en una categoría y, después, haga clic en **Propiedades del grupo de categorías**.  
  
3.  En la pestaña General, en el cuadro **Sincronizar grupos en** , haga clic en el nombre de la categoría cuyos colores desea sincronizar y, a continuación, haga clic en **Aceptar**.  
  
### <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>Para especificar colores coherentes en varios gráficos de formas  
  
1.  Haga clic con el botón derecho fuera del cuerpo del informe y seleccione **Propiedades del informe**.  
  
2.  En **Código**, escriba el código siguiente en el cuadro de texto.  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  Deberá reemplazar las cadenas de "Color1" por sus propios colores. Puede usar colores con nombre, por ejemplo "Rojo", o un valor hexadecimal de seis dígitos que represente el color, como "#FFFFFF" para el negro. Si ha definido más de tres colores, deberá extender la matriz de colores para que el número de colores de la matriz coincida con el número de puntos del gráfico de formas. Puede agregar nuevos colores a la matriz especificando una lista de valores de cadena separada por comas que contenga colores con nombre o representaciones hexadecimales de los colores.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Haga clic con el botón derecho en el gráfico de formas y seleccione **Propiedades de la serie**.  
  
5.  En **Relleno**, haga clic en el botón **Expresión** (*fx*) para editar la expresión de la propiedad **Color** .  
  
6.  Escriba la expresión siguiente, donde "MyCategoryField" es el campo que se muestra en el área **Grupos de categorías** :  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a los colores de serie de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Agregar estilos con bisel, relieve y textura a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Definir los colores de un gráfico mediante una paleta &#40;Generador de informes y SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Agregar puntos vacíos al gráfico &#40;generador de informes y SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos de formas &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Vincular varias regiones de datos al mismo conjunto de datos &#40;Generador de informes y SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Anidar regiones de datos &#40;Generador de informes y SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)   
 [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
