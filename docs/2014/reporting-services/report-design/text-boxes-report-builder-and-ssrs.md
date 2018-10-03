---
title: Cuadros de texto (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10134"
- sql12.rtp.rptdesigner.textproperties.general.f1
- "10120"
- sql12.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 19c2f599a00548ed85853720c0aad86d38950c74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222525"
---
# <a name="text-boxes-report-builder-and-ssrs"></a>Cuadros de texto (Generador de informes y SSRS)
  Al pensar en un cuadro de texto, probablemente se imagina un cuadro independiente que contiene el texto en una superficie como la de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint. En el Generador de informes algunos cuadros de texto son así y pueden mostrar el texto literal de títulos, descripciones y etiquetas, o texto dinámico basado en expresiones. Además, todas las celdas de una tabla o una matriz (región de datos de Tablix) contienen un cuadro de texto, al que se puede dar formato de la misma manera que a los cuadros de texto independientes de un informe.  
  
> [!NOTE]  
>  Si arrastra un valor de campo de un conjunto de datos de informe directamente hasta la superficie de diseño del informe, o hasta un cuadro de texto situado en la superficie de diseño del informe, al ejecutar el informe solamente verá el primer valor del conjunto de resultados. Para ver todos los valores de un campo, deberá arrastrar dicho campo hasta una celda de una tabla o matriz. Así, al ejecutar el informe, verá todos los valores en ese campo.  
  
 Para mostrar texto repetido en un diseño de forma libre, coloque un cuadro de texto en una región de datos de la lista. Use una lista si desea repetir un formato para varios valores, por ejemplo, un formato de factura de cliente que se repite una vez para cada cliente. Para obtener más información, consulte [enumera &#40;generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
 Use un contenedor de rectángulo si desea controlar el diseño del cuadro de texto y los espacios en blanco que aparecen debajo del último cuadro de texto. Para más información, vea [Rectángulos y líneas &#40;Generador de informes y SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md).  
  
 La expresión de un cuadro de texto puede incluir texto literal, apuntar a un campo de la base de datos o calcular datos. Todas las expresiones se muestran como texto de marcador de posición para que pueda dar formato a los números, colores y otras propiedades de aspecto. También puede combinar marcadores de posición con texto literal en el mismo cuadro de texto.  
  
 Puede dar formato al texto de cada uno de los cuadros de texto con variedad de fuentes, colores, estilos y acciones. Para más información, vea [Formatting Text and Placeholders &#40;Report Builder and SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a> Aumentar y disminuir el tamaño de un cuadro de texto  
 De manera predeterminada, los cuadros de texto tienen un tamaño fijo. Puede permitir que un cuadro de texto se reduzca o se expanda verticalmente según su contenido. Para obtener más información, consulte [permitir que un cuadro de texto aumente o disminuya &#40;generador de informes y SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md).  
  
## <a name="orienting-a-text-box"></a>Orientar un cuadro de texto  
 Orientar los cuadros de texto puede ayudarle a crear informes más legibles, permitir una orientación del texto específica de la configuración regional, ajustar más columnas en un informe impreso a tamaño de página fijo y crear informes con más atractivo gráfico. Un cuadro de texto se puede orientar en direcciones diferentes: horizontal, vertical o girado 270 grados. La opción vertical se suele utilizar más para los idiomas de Asia oriental que se escriben de arriba abajo. En la mayoría de los representadores, la opción vertical controla la propiedad de giro de glifo para que el texto se escriba de arriba abajo, pero los caracteres no estén en los lados. Para otros idiomas, el texto de las opciones vertical y girado 270 grados se escribe de lado.  
  
 Puede aplicar la orientación a los cuadros de texto que contienen texto literal, campos de un conjunto de datos de informe o datos calculados. El cuadro de texto puede ser independiente en el cuerpo del informe, en una tabla o matriz, o en un encabezado y pie de página del informe.  
  
 La siguiente imagen muestra tres versiones de un informe de la tabla que agrupa los datos por mes. El cuadro de texto que contiene el valor del mes utiliza una orientación diferente.  
  
 ![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 La orientación se establece en el cuadro de texto y se aplica a todo el texto del cuadro. No puede especificar una orientación diferente para las partes del cuadro de texto.  
  
 Para empezar rápidamente con el cambio de orientación del texto, vea la sección sobre cómo girar texto en el [Tutorial: dar formato al texto &#40;Report Builder&#41;](../tutorial-format-text-report-builder.md). Para obtener más información, consulte [establecer orientación del cuadro de texto &#40;generador de informes y SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md).  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 [Agregar, mover o eliminar un cuadro de texto &#40;generador de informes y SSRS&#41;](add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [Dar formato al texto en un cuadro de texto &#40;generador de informes y SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [Establecer la orientación del cuadro de texto &#40;generador de informes y SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [Permitir que un cuadro de texto aumente o disminuya &#40;generador de informes y SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a texto y marcadores de posición &#40;generador de informes y SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Aplicar formato a números y fechas &#40;generador de informes y SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
