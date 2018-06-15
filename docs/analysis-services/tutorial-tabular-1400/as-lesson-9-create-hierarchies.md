---
title: 'Lección tutorial de Analysis Services 9: crear jerarquías | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
ms.openlocfilehash: df99d05373d4d3087ef1d5fa5324ec645bf000b6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34042979"
---
# <a name="create-hierarchies"></a>Crear jerarquías

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará jerarquías. Las jerarquías son grupos de columnas dispuestas en niveles. Por ejemplo, una jerarquía geografía puede tener subniveles para país, estado, provincia y ciudad. Las jerarquías pueden aparecer por separado de otras columnas en una lista de campos de la aplicación cliente de informes, lo que facilita la navegación de los usuarios del cliente y su inclusión en un informe. Para obtener más información, consulte [jerarquías](../tabular-models/hierarchies-ssas-tabular.md)
  
Para crear jerarquías, use el Diseñador de modelos en *vista de diagrama*. Crear y administrar jerarquías no se admiten en la vista de datos.  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 8: crear perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Crear jerarquías  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>Para crear una jerarquía de categorías de la tabla DimProduct  
  
1.  En el Diseñador de modelos (vista de diagrama), haga clic en el **DimProduct** tabla > **crear jerarquía**. Aparece una nueva jerarquía en la parte inferior de la ventana de tabla. Cambiar el nombre de la jerarquía **categoría**.  
  
2.  Haga clic y arrastre la **ProductCategoryName** columna a la nueva **categoría** jerarquía.  
  
3.  En el **categoría** jerarquía, haga clic en **ProductCategoryName** > **cambiar el nombre de**y, a continuación, escriba **categoría**.  
  
    > [!NOTE]  
    > Al cambiar el nombre de una columna de la jerarquía no se cambia el nombre de esa columna en la tabla. Una columna de una jerarquía es simplemente una representación de la columna de la tabla.  
  
4.  Haga clic y arrastre la **ProductSubcategoryName** columna a la **categoría** jerarquía. Cámbiele el nombre **subcategoría**. 
  
5.  Haga clic en el **ModelName** columna > **agregar a jerarquía**y, a continuación, seleccione **categoría**. Cámbiele el nombre **modelo**.

6.  Por último, agregue **EnglishProductName** a la jerarquía de categorías. Cámbiele el nombre **producto**.  

    ![categoría como lesson9](../tutorial-tabular-1400/media/as-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Para crear jerarquías en la tabla DimDate  
  
1.  En el **DimDate** de tabla, cree una jerarquía denominada **calendario**.  
  
3.  Agregue el columnas siguientes en el orden:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  En el **DimDate** de tabla, cree un **Fiscal** jerarquía. Incluir el columnas siguientes en el orden:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por último, en la **DimDate** de tabla, cree un **ProductionCalendar** jerarquía. Incluir el columnas siguientes en el orden:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>¿Qué sigue?

[Lección 10: Crear particiones](../tutorial-tabular-1400/as-lesson-10-create-partitions.md). 
  
  
