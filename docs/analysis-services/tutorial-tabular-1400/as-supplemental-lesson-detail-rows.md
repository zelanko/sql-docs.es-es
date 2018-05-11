---
title: 'Lección complementaria de Analysis Services tutorial: filas de detalles | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 69a962bcb518040c88763b65004a89f5277546c5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="supplemental-lesson---detail-rows"></a>Lección complementaria - filas de detalles

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección complementaria, se utiliza el Editor de DAX para definir una expresión personalizada de filas de detalle. Una expresión de filas de detalles es una propiedad en una medida, proporciona más información acerca de los resultados agregados de una medida de los usuarios finales. 
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo de lección complementaria forma parte de un tutorial de modelado tabular. Antes de realizar las tareas de esta lección complementaria, deberá haber finalizado todas las lecciones anteriores o tiene un proyecto de modelo de ejemplo Adventure Works Internet Sales completado.  
  
## <a name="whats-the-issue"></a>¿Cuál es el problema?

Echemos un vistazo a los detalles de la medida InternetTotalSales, antes de agregar una expresión de filas de detalle.

1.  En SSDT, haga clic en el **modelo** menú > **analizar en Excel** para abrir Excel y cree una tabla dinámica en blanco.
  
2.  En **PivotTable Fields**, agregue el **InternetTotalSales** medida de la tabla FactInternetSales y **valores**, **CalendarYear** de la tabla DimDate para **columnas**, y **Spanishcountryregionname** a **filas**. La tabla dinámica le proporciona los resultados de un agregado de la medida InternetTotalSales por regiones y año. 

    ![como-lección-detalle-filas de tabla dinámica](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. En la tabla dinámica, haga doble clic en un valor agregado para un año y un nombre de región. A continuación se hace doble clic en el valor para el año 2014 y Australia. Una nueva hoja abre que contiene datos, pero los datos no resultan de utilidad.

    ![como-lección-detalle-filas de tabla dinámica](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
Lo que queremos ver aquí es una tabla que contiene columnas y filas de datos que contribuyen al resultado de la medida InternetTotalSales agregado. Para ello, podemos agregar una expresión de filas de detalles como una propiedad de la medida.

## <a name="add-a-detail-rows-expression"></a>Agregar una expresión de filas de detalle

#### <a name="to-create-a-detail-rows-expression"></a>Para crear una expresión de filas de detalle 
  
1. En la cuadrícula de medidas de la tabla FactInternetSales, haga clic en el **InternetTotalSales** medida. 

2. En **propiedades** > **expresión de filas de detalle**, haga clic en el botón de editor para abrir el Editor de DAX.

    ![como-lección-detalle-filas-elipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. En el Editor de DAX, escriba la siguiente expresión:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Esta expresión especifica nombres de columnas, y se devuelven resultados de medida de la tabla FactInternetSales y las tablas relacionadas cuando un usuario hace doble clic en un resultado agregado en una tabla dinámica o informe.

4. En Excel, elimine la hoja que creó en el paso 3, a continuación, haga doble clic en un valor agregado. Esta vez, con una propiedad de expresión de filas de detalle definida para la medida, una nueva hoja abre que contienen datos mucho más útiles.

    ![como-lección-detalle-filas-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. Volver a implementar el modelo.

  
## <a name="see-also"></a>Vea también  

[Función SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[Lección complementaria: Seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lección complementaria: Jerarquías desiguales](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
