---
title: Establecer un valor mínimo o máximo en un medidor (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d13b0b0c9fd55a6de3dfca7a07b913711828887e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215234"
---
# <a name="set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs"></a>Establecer un valor mínimo o máximo en un medidor (Generador de informes y SSRS)
  A diferencia del gráfico, donde se definen varios grupos, el medidor solo muestra un valor. Puesto que el Generador de informes y el Diseñador de informes determinan el contexto o la importancia relativa del valor que se está intentando mostrar en el medidor, se deberán definir los valores mínimo y máximo de la escala. Por ejemplo, si los valores de datos son clasificaciones entre 0 y 10, le interesará establecer el mínimo en 0 y el máximo en 10. Los números del intervalo se calculan automáticamente en función de los valores mínimo y máximo especificados. De forma predeterminada, los valores mínimo y máximo están establecidos en 0 y 100, pero estos son valores arbitrarios que conviene cambiar. La aplicación no calcula el valor como un porcentaje.  
  
 Si el intervalo de valores es grande, por ejemplo de 0 a 10000, considere la posibilidad de usar un multiplicador para reducir el número de ceros en el medidor. El multiplicador únicamente reducirá la escala de los números en el medidor, no el valor en sí mismo.  
  
 Puede utilizar las expresiones para establecer los valores de las opciones **Mínimo** y **Máximo** . Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-minimum-and-maximum-on-the-gauge"></a>Para establecer los valores mínimo y máximo en el medidor  
  
1.  Haga clic con el botón derecho en la escala y seleccione **Propiedades de escala**. Aparece el cuadro de diálogo **Propiedades de escala** .  
  
2.  En **General**, especifique un valor para **Mínimo**. De forma predeterminada, este valor es 0. Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece el valor de la opción.  
  
3.  Especifique un valor **Máximo**. De forma predeterminada, este valor es 100. Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece el valor de la opción.  
  
4.  (Opcional) Si los valores mínimo y máximo son grandes, especifique un valor para la opción **Multiplicar etiquetas de escala por** . Para especificar un multiplicador que reduzca la escala, use un número decimal. Por ejemplo, si tiene una escala de 0 a 1000, puede especificar un valor de multiplicador de 0,01 para que se vea de 0 a 10.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las escalas de un medidor &#40;Generador de informes y SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Aplicar formato a los punteros de un medidor &#40;Generador de informes y SSRS&#41;](formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
