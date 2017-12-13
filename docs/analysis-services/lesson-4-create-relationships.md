---
title: "Lección 5: Crear relaciones | Documentos de Microsoft"
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 53cfcc73f8bca771607425ac69eff021b8e6a00c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-4-create-relationships"></a>Lección 4: Crear relaciones
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección se comprobará las relaciones que se crearon automáticamente cuando importó los datos y agregar nuevas relaciones entre tablas diferentes. Una relación es una conexión entre dos tablas de datos que establece cómo se deben poner en correlación los datos de esas tablas. Por ejemplo, la tabla DimProduct y la tabla DimProductSubcategory tienen una relación basada en el hecho que cada producto pertenece a una subcategoría. Para obtener más información, consulte [relaciones](../analysis-services/tabular-models/relationships-ssas-tabular.md).
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 3: marcar como tabla de fechas](../analysis-services/lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Examinar las relaciones existentes y agregar nuevas relaciones  
Cuando importa datos utilizando el Asistente para importación de tablas, tenemos siete tablas de la base de datos AdventureWorksDW. Por lo general, al importar datos desde un origen relacional, las relaciones existentes se importan automáticamente junto con los datos. Sin embargo, para poder crear el modelo debe comprobar que esas relaciones entre las tablas se crearon correctamente. En este tutorial, agregará también tres relaciones nuevas.  
  
#### <a name="to-review-existing-relationships"></a>Para revisar las relaciones existentes  
  
1.  Haga clic en el **modelo** menú > **vista de modelo** > **vista de diagrama**.  

    El diseñador de modelos se muestra ahora en la vista de diagrama, un formato gráfico que muestra todas las tablas que importó con líneas entre ellas. Las líneas entre las tablas indican las relaciones que se crearon automáticamente cuando importó los datos.
    
    ![como-tabular-lesson4-diagrama](../analysis-services/media/as-tabular-lesson4-diagram.png)
  
    Use los controles de minimapa de la esquina inferior derecha del diseñador de modelos para ajustar la vista e incluir tantas tablas como sea posible. También puede hacer clic y arrastrar las tablas a ubicaciones diferentes, aunando las tablas o colocándolas en un orden determinado. El movimiento de las tablas no afecta a las relaciones existentes entre ellas. Para ver todas las columnas de una determinada tabla, haga clic y arrastre un borde de la tabla para expandirla o reducirla.  
  
2.  Haga clic en la línea sólida entre la **DimCustomer** tabla y la **DimGeography** tabla. La línea sólida entre estas dos tablas muestra que esta relación está activa, es decir, se utiliza de forma predeterminada al calcular fórmulas DAX.  
  
    Observe el **GeographyKey** columna en el **DimCustomer** tabla y la **GeographyKey** columna en el **DimGeography** ahora aparecen dentro de un cuadro de tabla. Esto indica que esas son las columnas usadas en la relación. Las propiedades de la relación aparecen ahora también en la ventana **Propiedades** .  
  
    > [!TIP]  
    > Además de utilizar el Diseñador de modelos en la vista de diagrama, también puede usar el cuadro de diálogo Administrar relaciones para mostrar las relaciones entre todas las tablas en un formato de tabla. Haga clic en **relaciones** en el Explorador de modelos tabulares y, a continuación, haga clic en **administrar relaciones**. El cuadro de diálogo Administrar relaciones muestra las relaciones que se crearon automáticamente cuando importó los datos.  
  
3.  Usar el Diseñador de modelos en la vista de diagrama o el cuadro de diálogo Administrar relaciones, para comprobar que se crearon las siguientes relaciones cuando se importó cada una de las tablas de la base de datos AdventureWorksDW:  
  
    |Activo|Tabla|Tabla de búsqueda relacionada|  
    |----------|---------|------------------------|  
    |Sí|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sí|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sí|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sí|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sí|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Si falta cualquiera de las relaciones en la tabla anterior, compruebe que el modelo incluye las siguientes tablas: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory y FactInternetSales. Si las tablas de la misma conexión del origen de datos se importan en momentos distintos, no se creará ninguna relación entre estas tablas y las relaciones deberán crearse manualmente.  

### <a name="take-a-closer-look"></a>Fijémonos con más atención
En la vista de diagrama, observará una flecha, un asterisco y un número en las líneas que muestran la relación entre tablas.

![como-tabular-lesson4-line](../analysis-services/media/as-tabular-lesson4-line.png)

La flecha muestra la dirección del filtro, que el asterisco muestra esta tabla es el lado "varios" en la cardinalidad de la relación y el 1 muestra que esta tabla es el uno lado de la relación. Si tiene que modificar una relación; Por ejemplo, cambiar la dirección del filtro de la relación y cardinalidad, haga doble clic en la línea de relación en la vista de diagrama para abrir el cuadro de diálogo Editar relación.

![como tabulares-lesson4-editar](../analysis-services/media/as-tabular-lesson4-edit.png)

Probablemente, nunca necesitará modificar una relación. Estas características están diseñadas para modelado de datos avanzados y están fuera del ámbito de este tutorial. Para obtener más información, consulte [bidireccional entre los filtros para los modelos tabulares en SQL Server 2016 Analysis Services](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).

En algunos casos, tal vez necesite crear relaciones adicionales entre las tablas de su modelo para permitir una determinada lógica empresarial. Para este tutorial, debe crear tres relaciones adicionales entre la tabla FactInternetSales y la tabla DimDate.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para agregar nuevas relaciones entre las tablas  
  
1.  En el Diseñador de modelos en el **FactInternetSales** de tabla, haga clic y mantenga el **OrderDate** columna, a continuación, arrastre el cursor hasta el **fecha** columna en el  **DimDate** de tabla y, a continuación, la versión.  

    Aparece una línea sólida que indica que ha creado una relación activa entre el **OrderDate** columna en el **venta por Internet** tabla y la **fecha** columna en el **Fecha** tabla. 
  
      ![como tabulares-lesson4-nuevo](../analysis-services/media/as-tabular-lesson4-new.png) 
  
    > [!NOTE]  
    > Al crear relaciones, se selecciona automáticamente la dirección del filtro y cardinalidad entre la tabla principal y la tabla de búsqueda relacionada.  
  
2.  En el **FactInternetSales** de tabla, haga clic y mantenga el **DueDate** columna, a continuación, arrastre el cursor hasta el **fecha** columna en el **DimDate** de tabla y, a continuación, suelte.  
  
    Aparecerá una línea punteada que indica que ha creado una relación inactiva entre la **DueDate** columna en el **FactInternetSales** tabla y la **fecha** columna en el  **DimDate** tabla. Puede haber varias relaciones entre las tablas, pero solo una puede estar activa cada vez.  
  
3.  Por último, cree una relación más; en el **FactInternetSales** de tabla, haga clic y mantenga el **ShipDate** columna, a continuación, arrastre el cursor hasta el **fecha** columna en el **DimDate** tabla y suelte el botón.  
    
     ![como-tabular-lesson4-newinactive](../analysis-services/media/as-tabular-lesson4-newinactive.png)
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?
Vaya a la siguiente lección: [lección 5: crear columnas calculadas](../analysis-services/lesson-5-create-calculated-columns.md).
  
  
  
