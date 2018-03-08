---
title: "Lección de Analysis Services tutorial 4: crear relaciones | Documentos de Microsoft"
description: "Describe cómo crear relaciones en el proyecto de tutorial de Analysis Services."
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 2776649b049254e27851a9d4ce95e8d6dea81067
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="create-relationships"></a>Crear relaciones

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, compruebe las relaciones que se crearon automáticamente cuando importó los datos y agregar nuevas relaciones entre tablas diferentes. Una relación es una conexión entre dos tablas de datos que establece cómo se deben poner en correlación los datos de esas tablas. Por ejemplo, la tabla DimProduct y la tabla DimProductSubcategory tienen una relación basada en el hecho que cada producto pertenece a una subcategoría. Para obtener más información, consulte [relaciones](../tabular-models/relationships-ssas-tabular.md).
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 3: marcar como tabla de fechas](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Examinar las relaciones existentes y agregar nuevas relaciones  

Cuando importa datos mediante obtener datos, tenemos siete tablas de la base de datos AdventureWorksDW. Por lo general, al importar datos desde un origen relacional, las relaciones existentes se importan automáticamente junto con los datos. Fin de obtener datos crear automáticamente relaciones en el modelo de datos, debe haber relaciones entre tablas en el origen de datos.

Antes de continuar con el modelo de creación, debe comprobar las relaciones entre tablas se crearon correctamente. Para este tutorial, agregará también tres relaciones nuevas.  

  
#### <a name="to-review-existing-relationships"></a>Para revisar las relaciones existentes  
  
1.  Haga clic en el **modelo** menú > **vista de modelo** > **vista de diagrama**.  

    El Diseñador de modelos aparece ahora en la vista de diagrama, un formato gráfico para mostrar todas las tablas que importó con líneas entre ellos. Las líneas entre las tablas indican las relaciones que se crearon automáticamente cuando importó los datos.
    
    ![diagrama como lesson4](../tutorial-tabular-1400/media/as-lesson4-diagram.png)
  
    > [!NOTE]
    > Si no ve las relaciones entre tablas, se deberá probablemente significa que no hay ninguna relación entre esas tablas en el origen de datos.

    Incluir como muchas de las tablas como sea posible mediante el uso de controles de minimapa situados en la esquina inferior derecha del Diseñador de modelos. También puede hacer clic y arrastrar las tablas a ubicaciones diferentes, aunando las tablas o colocándolas en un orden determinado. Mover tablas no afecta a las relaciones entre las tablas. Para ver todas las columnas en una tabla determinada, haga clic y arrastre un borde de la tabla para expandir o reducir el tamaño.  
  
2.  Haga clic en la línea sólida entre la **DimCustomer** tabla y la **DimGeography** tabla. La línea sólida entre estas dos tablas se muestra que esta relación está activa, es decir, se utiliza de forma predeterminada al calcular las fórmulas de DAX.  
  
    Observe el **GeographyKey** columna en el **DimCustomer** tabla y la **GeographyKey** columna en el **DimGeography** ahora aparecen dentro de un cuadro de tabla. Estas columnas se utilizan en la relación. Las propiedades de la relación aparecen ahora también en la ventana **Propiedades** .  
  
    > [!TIP]  
    > También puede usar el cuadro de diálogo Administrar relaciones para mostrar las relaciones entre todas las tablas en un formato de tabla. En el Explorador de modelos tabulares, haga clic en **relaciones** > **administrar relaciones**.
  
3.  Compruebe que se crearon las siguientes relaciones cuando se importó cada una de las tablas de la base de datos AdventureWorksDW:  
  
    |Activo|Tabla|Tabla de búsqueda relacionada|  
    |----------|---------|------------------------|  
    |Sí|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sí|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sí|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sí|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sí|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Si falta cualquiera de las relaciones, compruebe que el modelo incluye las siguientes tablas: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory y FactInternetSales. Si las tablas de la misma conexión de origen de datos se importan en momentos, las relaciones entre distintos dichas tablas no se crean y se deben crear manualmente. Si no aparece ninguna relación, significa que no hay ninguna relación en el origen de datos. Puede crearlos manualmente en el modelo de datos.

### <a name="take-a-closer-look"></a>Fijémonos con más atención

En la vista de diagrama, tenga en cuenta una flecha, un asterisco y un número en las líneas que muestran la relación entre tablas.

![como en línea lesson4](../tutorial-tabular-1400/media/as-lesson4-line.png)

La flecha muestra la dirección del filtro. El asterisco muestra esta tabla es la *muchos* lado en la cardinalidad de la relación y la muestra esta tabla es la *una* lado de la relación. Si tiene que modificar una relación; Por ejemplo, cambiar la dirección del filtro de la relación y cardinalidad, haga doble clic en la línea de relación para abrir el cuadro de diálogo Editar relación.

![as-lesson4-edit](../tutorial-tabular-1400/media/as-lesson4-edit.png)

Estas características están diseñadas para modelado de datos avanzados y están fuera del ámbito de este tutorial. Para obtener más información, consulte [bidireccional entre los filtros para modelos tabulares de Analysis Services](../tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

En algunos casos, tal vez necesite crear relaciones adicionales entre las tablas de su modelo para permitir una determinada lógica empresarial. Para este tutorial, debe crear tres relaciones adicionales entre la tabla FactInternetSales y la tabla DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para agregar nuevas relaciones entre las tablas  
  
1.  En el Diseñador de modelos, en la **FactInternetSales** de tabla, haga clic y mantenga el **OrderDate** columna, a continuación, arrastre el cursor hasta el **fecha** columna en el **DimDate** de tabla y, a continuación, suelte.  

    Aparece una línea sólida que indica que ha creado una relación activa entre el **OrderDate** columna en el **venta por Internet** tabla y el **fecha** columna en el **fecha** tabla. 
  
      ![como lesson4-nuevo](../tutorial-tabular-1400/media/as-lesson4-new.png) 
  
    > [!NOTE]  
    > Al crear relaciones, se selecciona automáticamente la dirección del filtro y cardinalidad entre la tabla principal y la tabla de búsqueda relacionada.  
  
2.  En el **FactInternetSales** de tabla, haga clic y mantenga el **DueDate** columna, a continuación, arrastre el cursor hasta el **fecha** columna en el **DimDate** de tabla y, a continuación, suelte.  
  
    Aparecerá una línea punteada que indica que ha creado una relación inactiva entre la **DueDate** columna en el **FactInternetSales** tabla y el **fecha** columna en el **DimDate** tabla. Puede haber varias relaciones entre las tablas, pero solo una puede estar activa cada vez. Las relaciones inactivas pueden hacerse activas para realizar agregaciones especial en expresiones de DAX personalizadas.  
  
3.  Finalmente, cree una relación más. En el **FactInternetSales** de tabla, haga clic y mantenga el **ShipDate** columna, a continuación, arrastre el cursor hasta el **fecha** columna en el **DimDate** de tabla y, a continuación, suelte.  
    
     ![as-lesson4-newinactive](../tutorial-tabular-1400/media/as-lesson4-newinactive.png)
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 5: Crear columnas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md).
  
  
  
