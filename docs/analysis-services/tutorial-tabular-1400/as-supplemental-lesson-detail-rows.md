---
title: 'Lección complementaria tutorial de Analysis Services: filas de detalles | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0518cdd7707c5973bfd055af997a75c9b67d7479
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38017798"
---
# <a name="supplemental-lesson---detail-rows"></a>Lección complementaria: filas de detalles

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección complementaria, usará el Editor de DAX para definir una expresión personalizada de las filas de detalle. Una expresión de filas de detalles es una propiedad en una medida, que proporciona a los usuarios finales más información acerca de los resultados agregados de una medida. 
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo de la lección complementaria forma parte de un tutorial de modelado tabular. Antes de realizar las tareas de esta lección complementaria, debe haber completado todas las lecciones anteriores o tiene un proyecto de modelos de ejemplo Adventure Works Internet Sales completado.  
  
## <a name="whats-the-issue"></a>¿Cuál es el problema?

Echemos un vistazo a los detalles de la medida InternetTotalSales, antes de agregar una expresión de filas de detalle.

1.  En SSDT, haga clic en el **modelo** menú > **analizar en Excel** para abrir Excel y crear una tabla dinámica en blanco.
  
2.  En **PivotTable Fields**, agregue el **InternetTotalSales** medida desde la tabla FactInternetSales a **valores**, **CalendarYear** desde la tabla DimDate a **columnas**, y **EnglishCountryRegionName** a **filas**. La tabla dinámica proporciona ahora resultados agregados de la medida InternetTotalSales por regiones y año. 

    ![como-lección-detalle-filas de tabla dinámica](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. En la tabla dinámica, haga doble clic en un valor agregado para un año y un nombre de región. Aquí se hace doble clic en el valor de Australia y el año 2014. Que contiene datos, pero los datos no resultan de utilidad, se abre una hoja nueva.

    ![como-lección-detalle-filas de tabla dinámica](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
Lo que queremos ver aquí es una tabla que contiene columnas y filas de datos que contribuyan al resultado agregado de la medida InternetTotalSales. Para ello, podemos agregar una expresión de filas de detalles como una propiedad de la medida.

## <a name="add-a-detail-rows-expression"></a>Agregar una expresión de filas de detalles

#### <a name="to-create-a-detail-rows-expression"></a>Para crear una expresión de filas de detalles 
  
1. En la cuadrícula de medidas de la tabla FactInternetSales, haga clic en el **InternetTotalSales** medida. 

2. En **propiedades** > **expresión de filas de detalle**, haga clic en el botón del editor para abrir el Editor de DAX.

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

    Esta expresión especifica nombres de columnas, y se devuelven los resultados de la medida de la tabla FactInternetSales y las tablas relacionadas cuando un usuario hace doble clic en un resultado agregado en una tabla dinámica o informe.

4. En Excel, elimine la hoja creada en el paso 3, a continuación, haga doble clic en un valor agregado. Esta vez, con una propiedad de expresión de filas de detalles definida para la medida, nuevo abre una hoja que contiene los datos mucho más útiles.

    ![como-lección-detalle-filas-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. Volver a implementar el modelo.

  
## <a name="see-also"></a>Vea también  

[Función SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[Lección complementaria: Seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Lección complementaria: Jerarquías desiguales](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
