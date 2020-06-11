---
title: 'Lección 5: crear relaciones | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 63fe9b7d83eea026a9a0f61213e2ccd30bba3591
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542913"
---
# <a name="lesson-5-create-relationships"></a>Lección 5: Crear relaciones
  En esta lección, comprobará las relaciones que se han creado de forma automática al importar datos y agregará nuevas relaciones entre tablas diferentes. Una relación es una conexión entre dos tablas de datos que establece cómo se deben poner en correlación los datos de esas tablas. Por ejemplo, la tabla Product y la tabla Product Subcategory tienen una relación basada en el hecho de que cada producto pertenece a una subcategoría. Para obtener más información, consulte [Relaciones &#40;SSAS tabular&#41;](tabular-models/relationships-ssas-tabular.md).  
  
 Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 3: Cambiar el nombre de las columnas](rename-columns.md).  
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Examinar las relaciones existentes y agregar nuevas relaciones  
 Cuando importó los datos mediante el Asistente para la importación de tablas, importó siete tablas de la base de datos AdventureWorksDW. Normalmente, si importa datos de un origen relacional, las relaciones existentes se importan automáticamente junto con los datos. Sin embargo, antes de continuar creando el modelo, debe comprobar que las relaciones entre tablas se crearon correctamente. En este tutorial, agregará también tres relaciones nuevas.  
  
#### <a name="to-review-existing-relationships"></a>Procedimiento para revisar las relaciones existentes  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** , elija **Vista de modelo**y haga clic en **Vista de diagrama**.  
  
     El diseñador de modelos se muestra ahora en la vista de diagrama, un formato gráfico que muestra todas las tablas que importó con líneas entre ellas. Las líneas entre las tablas indican las relaciones que se crearon automáticamente cuando importó los datos.  
  
     Utilice los controles de minimapa de la esquina superior derecha del diseñador de modelos para ajustar la vista e incluir tantas tablas como sea posible. También puede hacer clic y arrastrar las tablas a ubicaciones diferentes, aunando las tablas o colocándolas en un orden determinado. El movimiento de las tablas no afecta a las relaciones existentes entre ellas. Para ver todas las columnas de una determinada tabla, haga clic y arrastre un borde de la tabla para expandirla o reducirla.  
  
2.  Haga clic en la línea sólida entre la tabla **Customer** y la tabla **Geography** . La línea sólida entre estas dos tablas muestra que esta relación está activa, es decir, se utiliza de forma predeterminada al calcular fórmulas DAX.  
  
     Observe que la columna **Geography Id** de la tabla **Customer** y la columna **Geography Id** de la tabla **Geography** aparecen ahora dentro de un cuadro. Esto indica que esas son las columnas utilizadas en la relación. Las propiedades de la relación aparecen ahora también en la ventana **propiedades** .  
  
    > [!TIP]  
    >  Además de utilizar el diseñador de modelos en la vista de diagrama, también puede utilizar el cuadro de diálogo **administrar relaciones** para mostrar las relaciones entre todas las tablas en un formato de tabla. Haga clic en el menú **Tabla** y, después, haga clic en **Administrar relaciones**. El cuadro de diálogo **Administrar relaciones** muestra las relaciones que se han creado de forma automática al importar los datos.  
  
3.  Use el diseñador de modelos en la vista de diagrama o el cuadro de diálogo **Administrar relaciones** para comprobar que se han creado las siguientes relaciones al importar cada una de las tablas de la base de datos AdventureWorksDW:  
  
    |Activo|Tabla|Tabla de búsqueda relacionada|  
    |------------|-----------|--------------------------|  
    |Sí|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |Sí|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |Sí|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |Sí|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |Sí|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
 Si falta alguna de las relaciones en la tabla, compruebe que el modelo incluye las tablas siguientes: Customer, Date, Geography, Product, Product Category, Product Subcategory y Internet Sales. Si las tablas de la misma conexión de origen de datos se importaron en momentos distintos, las relaciones entre esas tablas no se crearán y tendrá que crearlas manualmente.  
  
 En algunos casos, debe crear relaciones adicionales entre las tablas del modelo para admitir una determinada lógica de negocios. En este tutorial, tendrá que crear tres relaciones adicionales entre la tabla Internet Sales y la tabla Date.  
  
#### <a name="to-add-new-relationships-between-tables"></a>Para agregar nuevas relaciones entre las tablas  
  
1.  En el diseñador de modelos, en la tabla **Internet Sales** , haga clic y mantenga seleccionada la columna **Order Date** , arrastre el cursor hasta la columna **Date** de la tabla **Date** y suéltelo.  
  
     Aparece una línea sólida que indica que ha creado una relación activa entre la columna **Order Date** de la tabla **Internet Sales** y la columna **Date** de la tabla **Date** .  
  
    > [!NOTE]  
    >  Al crear relaciones, el orden entre la tabla primaria y la tabla de búsqueda relacionada se fija de manera correcta automáticamente.  
  
2.  En la tabla **Internet Sales** , haga clic y mantenga seleccionada la columna **Due Date** , arrastre el cursor hasta la columna **Date** de la tabla **Date** y suéltelo.  
  
     Aparece una línea de puntos que indica que ha creado una relación inactiva entre la columna **Due Date** de la tabla **Internet Sales** y la columna **Date** de la tabla **Date** . Puede tener varias relaciones entre tablas, pero solo una relación puede estar activa simultáneamente.  
  
3.  Por último, cree una relación más; en la tabla **Internet Sales** , haga clic y mantenga seleccionada la columna **Ship Date** , arrastre el cursor hasta la columna **Date** de la tabla **Date** y suéltelo.  
  
     Aparece una línea de puntos que indica que ha creado una relación inactiva entre la columna **Ship Date** de la tabla **Internet Sales** y la columna **Date** de la tabla **Date** .  
  
## <a name="next-step"></a>siguiente paso  
 Para continuar esta lección, vaya a la lección siguiente: [Lección 6: Crear columnas calculadas](lesson-5-create-calculated-columns.md).  
  
  
