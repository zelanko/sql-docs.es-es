---
title: "Lección 10: Crear jerarquías | Documentos de Microsoft"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 003cf0dbb536397f1bebd4811a8d15c99a8211f5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-9-create-hierarchies"></a>Lección 9: Crear jerarquías
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, creará jerarquías. Las jerarquías son grupos de columnas dispuestas en niveles; por ejemplo, una jerarquía Geografía puede tener subniveles para País, Provincia y Ciudad. Las jerarquías pueden aparecer por separado de otras columnas en una lista de campos de la aplicación cliente de informes, lo que facilita la navegación de los usuarios del cliente y su inclusión en un informe. Para obtener más información, consulte [jerarquías](../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
Para crear jerarquías, deberá usar el Diseñador de modelos en *vista de diagrama*. Crear y administrar jerarquías no se admiten en la vista de datos.  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 8: crear perspectivas](../analysis-services/lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Crear jerarquías  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>Para crear una jerarquía de categorías de la tabla DimProduct  
  
1.  En el Diseñador de modelos (vista de diagrama), haga clic en el **DimProduct** tabla > **crear jerarquía**. Aparece una nueva jerarquía en la parte inferior de la ventana de tabla. Cambiar el nombre de la jerarquía **categoría**.  
  
2.  Haga clic y arrastre la **ProductCategoryName** columna a la nueva **categoría** jerarquía.  
  
3.  En el **categoría** jerarquía, haga clic en el **ProductCategoryName** > **cambiar el nombre de**y, a continuación, escriba **categoría**.  
  
    > [!NOTE]  
    > Al cambiar el nombre de una columna de la jerarquía no se cambia el nombre de esa columna en la tabla. Una columna de una jerarquía es simplemente una representación de la columna de la tabla.  
  
4.  Haga clic y arrastre la **ProductSubcategoryName** columna a la **categoría** jerarquía. Cámbiele el nombre **subcategoría**. 
  
5.  Haga clic en el **ModelName** columna > **agregar a jerarquía**y, a continuación, seleccione **categoría**. Haga lo mismo **EnglishProductName**. Cambiar el nombre de estas columnas en la jerarquía **modelo** y **producto**.  

    ![como-tabular-lesson9-categoría](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Para crear jerarquías en la tabla DimDate  
  
1.  En el **DimDate** de tabla, cree una nueva jerarquía denominada **calendario**.  
  
3.  Agregue el columnas siguientes en el orden:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  En el **DimDate** de tabla, cree un **Fiscal** jerarquía. Incluir las columnas siguientes:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por último, en la **DimDate** de tabla, cree un **ProductionCalendar** jerarquía. Incluir las columnas siguientes:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>¿Qué debe hacer a continuación?
Vaya a la siguiente lección: [lección 10: crear particiones](../analysis-services/lesson-10-create-partitions.md). 
  
  

