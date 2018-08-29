---
title: 'Lección del tutorial de Analysis Services 6: crear medidas | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9b466a703dd04a53c6ebf7c6fac624476abcc52
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43093968"
---
# <a name="create-measures"></a>Crear medidas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará medidas para incluirlas en el modelo. Al igual que las columnas calculadas que creó, una medida es un cálculo creado usando una fórmula DAX. Sin embargo, a diferencia de las columnas calculadas, las medidas se evalúan en función de un usuario seleccionado *filtro*. Por ejemplo, una columna en particular o una segmentación de datos que se agrega al campo etiquetas de fila en una tabla dinámica. A continuación, la medida aplicada calcula un valor para cada celda del filtro. Las medidas son cálculos eficaces y flexibles que se van a incluir en casi todos los modelos tabulares para realizar cálculos dinámicos sobre datos numéricos. Para obtener más información, consulte [medidas](../tabular-models/measures-ssas-tabular.md).
  
Para crear medidas, utilice la *cuadrícula de medidas*. De forma predeterminada, cada tabla tiene una cuadrícula de medidas vacía; Sin embargo, normalmente no creará medidas para todas las tablas. La cuadrícula de medidas aparece debajo de una tabla en el diseñador de modelos en la vista de datos. Para mostrar u ocultar la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y en **Mostrar cuadrícula de medidas**.  
  
Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas y, a continuación, escribiendo una fórmula DAX en la barra de fórmulas. Cuando haga clic en ENTRAR para completar la fórmula, la medida, a continuación, aparece en la celda. También puede crear medidas usando una función de agregación estándar haciendo clic en una columna y, a continuación, haga clic en el botón Autosuma (**∑**) en la barra de herramientas. Las medidas creadas mediante la característica Autosuma aparecen en la celda de cuadrícula de medidas directamente debajo de la columna, pero se pueden mover.  
  
En esta lección, creará medidas especificando una fórmula DAX en la barra de fórmulas y usando la característica Autosuma.  
  
Tiempo estimado para completar esta lección: **30 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 5: crear columnas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Crear medidas  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Para crear una medida DaysCurrentQuarterToDate en la tabla DimDate  
  
1.  En el Diseñador de modelos, haga clic en el **DimDate** tabla.  
  
2.  En la cuadrícula de medidas, haga clic en la celda vacía superior izquierda.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Observe que la celda superior izquierda ahora contiene un nombre de medida, **DaysCurrentQuarterToDate**, seguido del resultado, **92**. El resultado no es relevante en este momento porque no se ha aplicado ningún filtro de usuario.
    
      ![newmeasure como lesson6](../tutorial-tabular-1400/media/as-lesson6-newmeasure.png) 
    
    A diferencia de las columnas calculadas, con las fórmulas de medidas puede escribir el nombre de medida, seguido de dos puntos, seguido por la expresión de la fórmula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Para crear una medida DaysInCurrentQuarter en la tabla DimDate  
  
1.  Con el **DimDate** tabla activa en el Diseñador de modelos, en la cuadrícula de medidas, haga clic en la celda vacía situada debajo de la medida que creó.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Al crear una relación de comparación entre un período incompleto y el período anterior. La fórmula debe calcular la proporción del período que ha transcurrido y compararla con la misma proporción del período anterior. En este caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] proporciona la proporción transcurrida del período actual.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Para crear una medida InternetDistinctCountSalesOrder en la tabla FactInternetSales  
  
1.  Haga clic en el **FactInternetSales** tabla.   
  
2.  Haga clic en el **SalesOrderNumber** encabezado de columna.  
  
3.  En la barra de herramientas, haga clic en la flecha abajo situada junto al botón de autosuma (**∑**) y, después, seleccione **DistinctCount**.  
  
    La característica de autosuma crea automáticamente una medida para la columna seleccionada usando la fórmula estándar de agregación DistinctCount.  
    
       ![newmeasure2 como lesson6](../tutorial-tabular-1400/media/as-lesson6-newmeasure2.png)
  
4.  En la cuadrícula de medidas, haga clic en la nueva medida y, a continuación, en el **propiedades** ventana, en **nombre de medida**, cambiar el nombre de la medida a **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Para crear medidas adicionales en la tabla FactInternetSales  
  
1.  Con la característica de autosuma, cree y asigne un nombre a las medidas siguientes:  

    |columna|Nombre de medida|Autosuma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=CountA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|SUM|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|SUM|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|SUM|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|SUM|=SUM([SalesAmount])|  
    |Margen|InternetTotalMargin|SUM|=SUM([Margen])|  
    |TaxAmt|InternetTotalTaxAmt|SUM|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|SUM|=SUM([Cargos])|  
  
2.  Al hacer clic en una celda vacía de la cuadrícula de medidas y mediante el uso de la barra de fórmulas, cree las siguientes medidas personalizadas en orden:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Las medidas creadas para la tabla FactInternetSales pueden utilizarse para analizar datos financieros críticos como ventas, costos y margen de beneficio de los elementos definidos por el filtro seleccionado del usuario.  
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 7: Crear indicadores clave de rendimiento](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  

  
