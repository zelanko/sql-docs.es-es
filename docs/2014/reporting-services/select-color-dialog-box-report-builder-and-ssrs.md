---
title: Seleccione el cuadro de diálogo Color (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.selectcolor.f1
- "10090"
helpviewer_keywords:
- Select Color dialog box
ms.assetid: ac7089a3-5c7b-4f53-8348-180610e86da2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6bcbbe828da811ace5df4feea5cfdf888e1e6ca5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101382"
---
# <a name="select-color-dialog-box-report-builder-and-ssrs"></a>Cuadro de diálogo Seleccionar color (Generador de informes y SSRS)
  Use el cuadro de diálogo **Seleccionar color** para especificar las opciones de color para el fondo de una o varias celdas de una región de datos o un cuadro de texto de un gráfico.  
  
## <a name="options"></a>Opciones  
 **Selector de colores**  
 Elija una de las tres opciones para especificar cómo desea seleccionar los colores:  
  
-   **Selector - Círculo de colores:** elija un color con los valores HSB (matiz/saturación/luminosidad).  
  
-   **Selector - Cuadrado de colores:** elija un color con los valores RGB (rojo/verde/azul).  
  
-   **Paleta - Colores estándar:** elija un color de una lista predefinida de valores de color.  
  
 **Círculo de colores**  
 Se usa para los colores HSB porque los valores HSB se asignan a un sistema de coordenadas cilíndrico. El matiz es el color propiamente dicho, la saturación es la pureza del color y la luminosidad es su luminosidad u oscuridad relativa.  
  
 Cuando se elige un color, el centro del círculo determina el color. Use el control deslizante de color para cambiar el matiz. Las coordenadas x e y representan los valores de saturación y luminosidad, respectivamente.  
  
 **Cuadrado de colores**  
 Se usa para los colores RGB porque los valores RGB se asignan a un sistema de coordenadas cartesiano. R es el valor para el rojo, G es el valor para el verde y B es el valor para el azul.  
  
 Cuando se elige un color, el centro del cuadrado determina el color. Use el control deslizante de color para cambiar la gama del color elegido. Las coordenadas x e y representan los otros dos colores. Por ejemplo, si elige el color verde, el control deslizante muestra la gama de valores de verde, y las coordenadas x e y representan los valores para el rojo y el azul, respectivamente.  
  
 **Paleta de colores estándar**  
 Uso de colores con nombre desde el [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] `KnownColor` enumeración.  
  
 **Sistema de colores**  
 Especifique si desea colores RGB o HSB. Esta opción cambia la presentación para mostrar valores RGB o HSB que se actualizan interactivamente cuando se utiliza un círculo o un cuadrado de colores para el **Selector de colores**.  
  
 El valor **Alpha** se muestra para algunas propiedades cuando un color puede incluir un valor de transparencia. Por ejemplo, el relleno para las series del gráfico. Para las propiedades que no admiten la transparencia, este valor está deshabilitado.  
  
 **Rojo**  
 El valor decimal para la parte roja del color RGB. Use el cuadro de número para cambiar el valor o escriba un valor entre 0 y 255.  
  
 **Verde**  
 El valor decimal para la parte verde del color RGB. Use el cuadro de número para cambiar el valor o escriba un valor entre 0 y 255.  
  
 **Blue**  
 El valor decimal para la parte azul del color RGB. Use el cuadro de número para cambiar el valor o escriba un valor entre 0 y 255.  
  
 **Alpha**  
 El valor decimal para alfa o la transparencia del color. Cuando este valor está habilitado, puede usar el control deslizante para ajustar el grado de transparencia que desee.  
  
 **Matiz**  
 El valor decimal para el matiz del color HSB. Use el cuadro de número para cambiar el valor o escriba un valor entre 0 y 255.  
  
 **Saturación**  
 El valor decimal para la saturación del color HSB. Use el cuadro de número para cambiar el valor o escriba un valor entre 0 y 255.  
  
 **Brillo**  
 El valor decimal para la luminosidad del color HSB. Use el cuadro de número para cambiar el valor o escriba un valor entre 0 y 255.  
  
 **Ejemplo de color**  
 Muestra el color actual en la mitad izquierda del panel e interactivamente muestra el nuevo color que se está eligiendo en la mitad derecha del panel. Si no hay ningún color predeterminado, la mitad izquierda del panel es blanca. La mayoría de las propiedades RDL no tienen ningún color predeterminado.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a los elementos de informe &#40;Generador de informes y SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Aplicar formato a texto y a marcadores de posición &#40;Generador de informes y SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
