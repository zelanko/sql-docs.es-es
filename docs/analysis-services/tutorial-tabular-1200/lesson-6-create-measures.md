---
title: 'Lección 6: Crear medidas | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f8ad53f78acb862101ff633f663ea03198825ab
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404667"
---
# <a name="lesson-6-create-measures"></a>Lección 6: Crear medidas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, creará medidas para incluirlas en su modelo. Al igual que las columnas calculadas que creó en la lección anterior, una medida es un cálculo creado usando una fórmula DAX. Sin embargo, a diferencia de las columnas calculadas, las medidas se evalúan en función de un *filtro*seleccionado por el usuario; por ejemplo, una columna o una segmentación de datos determinada agregada al campo Etiquetas de filas en una tabla dinámica. A continuación, la medida aplicada calcula un valor para cada celda del filtro. Las medidas son cálculos eficaces y flexibles que desea incluir en casi todos los modelos tabulares para realizar cálculos dinámicos sobre datos numéricos. Para obtener más información, consulte [medidas](../tabular-models/measures-ssas-tabular.md).  
  
Para crear medidas, usará el *cuadrícula de medidas*. De manera predeterminada, cada tabla tiene una cuadrícula de medidas vacía, pero normalmente no creará medidas para todas las tablas. La cuadrícula de medidas aparece debajo de una tabla en el diseñador de modelos en la vista de datos. Para mostrar u ocultar la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y en **Mostrar cuadrícula de medidas**.  
  
Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas y escribiendo después una fórmula DAX en la barra de fórmulas. Al hacer clic en ENTRAR para completar la fórmula, la medida aparecerá en la celda. También puede crear medidas mediante una función de agregación estándar. Para ello, haga clic en una columna y, después, en el botón de autosuma (**∑**) en la barra de herramientas. Las medidas creadas mediante la característica de Autosuma aparecerán en la celda de cuadrícula de medidas directamente debajo de la columna, pero se pueden mover.  
  
En esta lección, creará medidas escribiendo una fórmula DAX en la barra de fórmulas y usando la característica de autosuma.  
  
Tiempo estimado para completar esta lección: **30 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 5: Crear columnas calculadas](lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Crear medidas  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a>Para crear una medida DaysCurrentQuarterToDate en la tabla DimDate  
  
1.  En el Diseñador de modelos, haga clic en el **DimDate** tabla.  
  
2.  En la cuadrícula de medidas, haga clic en la celda vacía superior izquierda.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Observe que la celda superior izquierda ahora contiene un nombre de medida, **DaysCurrentQuarterToDate**, seguido del resultado, **92**.
    
      ![as-tabular-lesson6-newmeasure](media/as-tabular-lesson6-newmeasure.png) 
    
    A diferencia de las columnas calculadas, con las fórmulas de medidas puede escribir el nombre de medida, seguido por una coma, seguida por la expresión de la fórmula.

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a>Para crear una medida DaysInCurrentQuarter en la tabla DimDate  
  
1.  Con el **DimDate** tabla activa en el Diseñador de modelos, en la cuadrícula de medidas, haga clic en la celda vacía situada debajo de la medida que acaba de crear.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Al crear un coeficiente de comparación entre un período incompleto y el período anterior, la fórmula debe tener en cuenta la parte del período que ha transcurrido y compararla con la misma parte del período anterior. En este caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] proporciona la proporción transcurrida del período actual.  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a>Para crear una medida InternetDistinctCountSalesOrder en la tabla FactInternetSales  
  
1.  Haga clic en el **FactInternetSales** tabla.   
  
2.  Haga clic en el **SalesOrderNumber** encabezado de columna.  
  
3.  En la barra de herramientas, haga clic en la flecha abajo situada junto al botón de autosuma (**∑**) y, después, seleccione **DistinctCount**.  
  
    La característica de autosuma crea automáticamente una medida para la columna seleccionada usando la fórmula estándar de agregación DistinctCount.  
    
       ![as-tabular-lesson6-newmeasure2](media/as-tabular-lesson6-newmeasure2.png)
  
4.  En la cuadrícula de medidas, haga clic en la nueva medida y, a continuación, en el **propiedades** ventana, en **nombre de medida**, cambiar el nombre de la medida a **InternetDistinctCountSalesOrder**. 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a>Para crear medidas adicionales en la tabla FactInternetSales  
  
1.  Con la característica de autosuma, cree y asigne un nombre a las medidas siguientes:  
  
    |Nombre de medida|columna|Autosuma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |InternetOrderLinesCount|SalesOrderLineNumber|Count|=COUNTA([SalesOrderLineNumber])|  
    |InternetTotalUnits|OrderQuantity|Sum|=SUM([OrderQuantity])|  
    |InternetTotalDiscountAmount|DiscountAmount|Sum|=SUM([DiscountAmount])|  
    |InternetTotalProductCost|TotalProductCost|Sum|=SUM([TotalProductCost])|  
    |InternetTotalSales|SalesAmount|Sum|=SUM([SalesAmount])|  
    |InternetTotalMargin|Margen|Sum|=SUM([Margen])|  
    |InternetTotalTaxAmt|TaxAmt|Sum|=SUM([TaxAmt])|  
    |InternetTotalFreight|Freight|Sum|=SUM([Cargos])|  
  
2.  Al hacer clic en una celda vacía de la cuadrícula de medidas y mediante el uso de la barra de fórmulas, cree y asigne el nombre de las siguientes medidas en orden:  
  
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
Vaya a la lección siguiente: [Lección 7: Creación de indicadores clave de rendimiento](lesson-7-create-key-performance-indicators.md).  

  
