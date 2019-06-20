---
title: 'Analysis Services lección 5 del tutorial: Crear columnas calculadas | Microsoft Docs'
ms.date: 04/25/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: b56fe07237faa6570fd4b8c1adb31d3cce8e4540
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "64776072"
---
# <a name="create-calculated-columns"></a>Crear columnas calculadas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, crear los datos en el modelo agregando columnas calculadas. Puede crear columnas calculadas (como columnas personalizadas) cuando se usa obtener datos, mediante el Editor de consultas, o más adelante en el tipo de diseñador modelo hace aquí. Para obtener más información, consulte [columnas calculadas](../tabular-models/ssas-calculated-columns.md).
  
Creará cinco columnas calculadas en tres tablas diferentes. Los pasos son ligeramente diferentes para cada tarea que muestra varias maneras para crear columnas, cambiarles el nombre y colocarlas en ubicaciones diferentes en una tabla.  

En esta lección también es donde se utilizar expresiones de análisis de datos (DAX). DAX es un lenguaje especial para crear expresiones de fórmula altamente personalizables para los modelos tabulares. En este tutorial, usará DAX para crear columnas calculadas, medidas y filtros de rol. Para obtener más información, consulte [DAX en modelos tabulares](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md). 
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 4: Crear relaciones](../tutorial-tabular-1400/as-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Crear columnas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Crear una columna calculada MonthCalendar en la tabla DimDate  
  
1.  Haga clic en el **modelo** menú > **vista de modelo** > **vista datos**.  
  
    Las columnas calculadas solo se pueden crear mediante el diseñador de modelos en la Vista de datos.  
  
2.  En el Diseñador de modelos, haga clic en el **DimDate** tabla (pestaña).  
  
3.  Haga clic en el **CalendarQuarter** encabezado de columna y, a continuación, haga clic en **Insertar columna**.  
  
    Una nueva columna denominada **Columna calculada 1** se inserta a la izquierda de la columna **Calendar Quarter** .  
  
4.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula DAX: Autocompletar le ayuda a escribir el nombres completos de columnas y tablas y enumera las funciones que están disponibles.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Después, los valores se rellenan para todas las filas de la columna calculada. Si desplaza hacia abajo por la tabla, verá las filas pueden tener valores diferentes para esta columna, en función de los datos de cada fila.    
  
5.  Cambiar el nombre de esta columna a **MonthCalendar**. 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
La columna calculada MonthCalendar proporciona un nombre ordenable del mes.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Crear una columna calculada DayOfWeek en la tabla DimDate  
  
1.  Con el **DimDate** tabla sigue activa, haga clic la **columna** menú y, a continuación, haga clic en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Cuando haya terminado de crear la fórmula, presione ENTRAR. Se agrega la columna nueva a la derecha de la tabla.  
  
3.  Cambiar el nombre de la columna a **DayOfWeek**.  
  
4.  Haga clic en el encabezado de columna y, a continuación, arrastre la columna entre la **EnglishDayNameOfWeek** columna y el **DayNumberOfMonth** columna.  
  
    > [!TIP]  
    > El movimiento de columnas en la tabla simplifica la navegación.  
  
La columna calculada DayOfWeek proporciona un nombre ordenable del día de semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Crear una columna calculada ProductSubcategoryName en la tabla DimProduct  
  
  
1.  En el **DimProduct** tabla, desplácese hasta el extremo derecho de la tabla. Observe que la columna más a la derecha se denomina ***Agregar columna***, haga clic en el encabezado de columna.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Cambiar el nombre de la columna a **ProductSubcategoryName**.  
  
La columna calculada ProductSubcategoryName se usa para crear una jerarquía en la tabla DimProduct que incluye datos de la columna EnglishProductSubcategoryName en la tabla DimProductSubcategory. Las jerarquías no pueden abarcar más de una tabla. Crear jerarquías más adelante en la lección 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Crear una columna calculada ProductCategoryName en la tabla DimProduct  
  
1.  Con el **DimProduct** tabla sigue activa, haga clic la **columna** menú y, a continuación, haga clic en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Cambiar el nombre de la columna a **ProductCategoryName**.  
  
La columna calculada ProductCategoryName se usa para crear una jerarquía en la tabla DimProduct que incluye datos de la columna EnglishProductCategoryName en la tabla DimProductCategory. Las jerarquías no pueden abarcar más de una tabla.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Crear una columna calculada margen en la tabla FactInternetSales  
  
1.  En el Diseñador de modelos, seleccione la **FactInternetSales** tabla.  
  
2.  Crear una nueva columna calculada entre la **SalesAmount** columna y el **TaxAmt** columna.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Cambie el nombre de la columna a **Margen**.  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    La columna calculada margen se utiliza para analizar los márgenes de beneficios de cada venta.  
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 6: Crear medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md).
  
  
  
