---
title: "Lección 6: Crear columnas calculadas | Documentos de Microsoft"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c59e137942d45cbe6c20a71b9fa785988b9876fa
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-5-create-calculated-columns"></a>Lección 5: Crear columnas calculadas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección creará nuevos datos en el modelo agregando columnas calculadas. Una columna calculada está basada en datos que ya existen en el modelo. Para obtener más información, consulte [columnas calculadas](../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
Creará cinco columnas calculadas nuevas en tres tablas diferentes. Los pasos son ligeramente diferentes para cada tarea. Esto es así para mostrarle que hay varias formas de crear nuevas columnas, cambiarles el nombre y colocarlas en distintos lugares de una tabla.  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 4: crear relaciones](../analysis-services/lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Crear columnas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Crear una columna calculada MonthCalendar en la tabla DimDate  
  
1.  Haga clic en el **modelo** menú > **vista de modelo** > **vista de datos**.  
  
    Las columnas calculadas solo se pueden crear mediante el diseñador de modelos en la Vista de datos.  
  
2.  En el Diseñador de modelos, haga clic en el **DimDate** tabla (pestaña).  
  
3.  Haga clic en el **CalendarQuarter** encabezado de columna y, a continuación, haga clic en **Insertar columna**.  
  
    Una nueva columna denominada **Columna calculada 1** se inserta a la izquierda de la columna **Calendar Quarter** .  
  
4.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula. Autocompletar sirve de ayuda para escribir los nombres completos de columnas y tablas, y enumera las funciones que están disponibles.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Después, los valores se rellenan para todas las filas de la columna calculada. Si se desplaza hacia abajo por la tabla, verá que las filas pueden tener valores diferentes para esta columna, en función de los datos que haya en cada fila.    
  
5.  Cambiar el nombre de esta columna para **MonthCalendar**. 

    ![como-tabular-lesson5-nuevacolumna](../analysis-services/media/as-tabular-lesson5-newcolumn.png) 
  
MonthCalendar calcula la columna proporciona un nombre que se puede ordenar por mes.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Crear una columna calculada DayOfWeek en la tabla DimDate  
  
1.  Con el **DimDate** sigue activa, haga clic en el **columna** menú y, a continuación, haga clic en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Cuando haya terminado de crear la fórmula, presione ENTRAR. Se agrega la columna nueva a la derecha de la tabla.  
  
3.  Cambiar el nombre de la columna a **DayOfWeek**.  
  
4.  Haga clic en el encabezado de columna y, a continuación, arrastre la columna entre la **EnglishDayNameOfWeek** columna y la **DayNumberOfMonth** columna.  
  
    > [!TIP]  
    > El movimiento de columnas en la tabla simplifica la navegación.  
  
El DayOfWeek calcula la columna proporciona un nombre ordenable del día de la semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Crear una columna calculada ProductSubcategoryName en la tabla DimProduct  
  
  
1.  En el **DimProduct** tabla, desplácese hasta el extremo derecho de la tabla. Observe que la columna situada más a la derecha se denomina **Agregar columna** (en cursiva); haga clic en el encabezado de columna.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente.  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Cambiar el nombre de la columna a **ProductSubcategoryName**.  
  
La columna calculada ProductSubcategoryName se utiliza para crear una jerarquía en la tabla DimProduct que incluye datos de la columna EnglishProductSubcategoryName en la tabla DimProductSubcategory. Las jerarquías no pueden abarcar más de una tabla. Creará jerarquías más adelante en la lección 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Crear una columna calculada ProductCategoryName en la tabla DimProduct  
  
1.  Con el **DimProduct** tabla sigue activa, haga clic el **columna** menú y, a continuación, haga clic en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Cambiar el nombre de la columna a **ProductCategoryName**.  
  
La columna calculada ProductCategoryName se utiliza para crear una jerarquía en la tabla DimProduct que incluye datos de la columna EnglishProductCategoryName en la tabla DimProductCategory. Las jerarquías no pueden abarcar más de una tabla.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Crear una columna calculada margen en la tabla FactInternetSales  
  
1.  En el Diseñador de modelos, seleccione la **FactInternetSales** tabla.  
  
2.  Agregue una nueva columna.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Cambie el nombre de la columna a **Margen**.  
  
5.  Arrastre la columna entre la **SalesAmount** columna y la **TaxAmt** columna. 
 
      ![como-tabular-lesson5-newmargin](../analysis-services/media/as-tabular-lesson5-newmargin.png)
      
    La columna calculada margen se utiliza para analizar los márgenes de beneficios de cada venta.  
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?
Vaya a la siguiente lección: [lección 6: crear medidas](../analysis-services/lesson-6-create-measures.md).
  
  
  

