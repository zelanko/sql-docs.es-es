---
title: "Establecer un valor m&#237;nimo o m&#225;ximo en un medidor (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b4c260c0-5a88-4f30-8977-eb5cc78fc146
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Establecer un valor m&#237;nimo o m&#225;ximo en un medidor (Generador de informes y SSRS)
  A diferencia de los gráficos de un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], donde se definen varios grupos, los medidores muestran un solo valor. Puesto que el Generador de informes y el Diseñador de informes determinan el contexto o la importancia relativa del valor que se está intentando mostrar en el medidor, se deberán definir los valores mínimo y máximo de la escala.   
    
  Por ejemplo, si los valores de datos son clasificaciones entre 0 y 10, le interesará establecer el mínimo en 0 y el máximo en 10. Los números del intervalo se calculan automáticamente en función de los valores mínimo y máximo especificados. De forma predeterminada, los valores mínimo y máximo están establecidos en 0 y 100, pero estos son valores arbitrarios que conviene cambiar. La aplicación no calcula el valor como un porcentaje.  
  
 Si el intervalo de valores es grande, por ejemplo de 0 a 10000, considere la posibilidad de usar un multiplicador para reducir el número de ceros en el medidor. El multiplicador únicamente reducirá la escala de los números en el medidor, no el valor en sí mismo.  
  
 Puede utilizar las expresiones para establecer los valores de las opciones **Mínimo** y **Máximo** . Para obtener más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## Para establecer los valores mínimo y máximo en el medidor  
  
1.  Haga clic con el botón derecho en la escala y seleccione **Propiedades de escala**. Aparece el cuadro de diálogo **Propiedades de escala** .  
  
2.  En **General**, especifique un valor para **Mínimo**. De forma predeterminada, este valor es 0. Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece el valor de la opción.  
  
3.  Especifique un valor **Máximo**. De forma predeterminada, este valor es 100. Si quiere, haga clic en el botón **Expresión** (*fx*) para modificar la expresión que establece el valor de la opción.  
  
4.  (Opcional) Si los valores mínimo y máximo son grandes, especifique un valor para la opción **Multiplicar etiquetas de escala por**. Para especificar un multiplicador que reduzca la escala, use un número decimal. Por ejemplo, si tiene una escala de 0 a 1000, puede especificar un valor de multiplicador de 0,01 para que se vea de 0 a 10.  
  
## Vea también  
 [Aplicar formato a las escalas de un medidor &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Aplicar formato a los punteros de un medidor &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  