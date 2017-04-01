---
title: "Lecci&#243;n 5: Crear relaciones | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 5: Crear relaciones
En esta lección, comprobará las relaciones que se han creado de forma automática al importar datos y agregará nuevas relaciones entre tablas diferentes. Una relación es una conexión entre dos tablas de datos que establece cómo se deben poner en correlación los datos de esas tablas. Por ejemplo, la tabla Product y la tabla Product Subcategory tienen una relación basada en el hecho de que cada producto pertenece a una subcategoría. Para obtener más información, consulte [Relaciones &#40;SSAS tabular&#41;](../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 3: Cambiar el nombre de las columnas](../analysis-services/lesson-3-rename-columns.md).  
  
## Examinar las relaciones existentes y agregar nuevas relaciones  
Cuando importó los datos mediante el Asistente para la importación de tablas, importó siete tablas de la base de datos AdventureWorksDW. Normalmente, si importa datos de un origen relacional, las relaciones existentes se importan automáticamente junto con los datos. Sin embargo, para poder crear el modelo debe comprobar que esas relaciones entre las tablas se crearon correctamente. En este tutorial, agregará también tres relaciones nuevas.  
  
#### Para revisar las relaciones existentes  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo**, elija **Vista de modelo** y haga clic en **Vista de diagrama**.  
  
    El diseñador de modelos se muestra ahora en la vista de diagrama, un formato gráfico que muestra todas las tablas que importó con líneas entre ellas. Las líneas entre las tablas indican las relaciones que se crearon automáticamente cuando importó los datos.  
  
    Use los controles de minimapa de la esquina inferior derecha del diseñador de modelos para ajustar la vista e incluir tantas tablas como sea posible. También puede hacer clic y arrastrar las tablas a ubicaciones diferentes, aunando las tablas o colocándolas en un orden determinado. El movimiento de las tablas no afecta a las relaciones existentes entre ellas. Para ver todas las columnas de una determinada tabla, haga clic y arrastre un borde de la tabla para expandirla o reducirla.  
  
2.  Haga clic en la línea sólida entre la tabla **Customer** y la tabla **Geography**. La línea sólida entre estas dos tablas muestra que esta relación está activa, es decir, se utiliza de forma predeterminada al calcular fórmulas DAX.  
  
    Observe que la columna **Geography Id** de la tabla **Customer** y la columna **Geography Id** de la tabla **Geography** aparecen ahora dentro de un cuadro. Esto indica que esas son las columnas usadas en la relación. Las propiedades de la relación aparecen ahora también en la ventana **Propiedades**.  
  
    > [!TIP]  
    > Además de usar el diseñador de modelos en la vista de diagrama, puede usar también el cuadro de diálogo **Administrar relaciones** para mostrar las relaciones entre todas las tablas en un formato de tabla. Haga clic en el menú **Tabla** y, después, haga clic en **Administrar relaciones**. El cuadro de diálogo **Administrar relaciones** muestra las relaciones que se han creado de forma automática al importar los datos.  
  
3.  Use el diseñador de modelos en la vista de diagrama o el cuadro de diálogo **Administrar relaciones** para comprobar que se han creado las siguientes relaciones al importar cada una de las tablas de la base de datos AdventureWorksDW:  
  
    |Activo|Table|Tabla de búsqueda relacionada|  
    |----------|---------|------------------------|  
    |Sí|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |Sí|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |Sí|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |Sí|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |Sí|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
Si falta alguna de las relaciones en la tabla, compruebe que el modelo incluye las tablas siguientes: Customer, Date, Geography, Product, Product Category, Product Subcategory y Internet Sales. Si las tablas de la misma conexión del origen de datos se importan en momentos distintos, no se creará ninguna relación entre estas tablas y las relaciones deberán crearse manualmente.  
  
En algunos casos, tal vez necesite crear relaciones adicionales entre las tablas de su modelo para permitir una determinada lógica empresarial. En este tutorial, tendrá que crear tres relaciones adicionales entre la tabla Internet Sales y la tabla Date.  
  
#### Para agregar nuevas relaciones entre las tablas  
  
1.  En el diseñador de modelos, en la tabla **Internet Sales**, haga clic y mantenga seleccionada la columna **Order Date**, arrastre el cursor hasta la columna **Date** de la tabla **Date** y suéltelo.  
  
    Aparece una línea sólida que indica que ha creado una relación activa entre la columna **Order Date** de la tabla **Internet Sales** y la columna **Date** de la tabla **Date**.  
  
    > [!NOTE]  
    > Al crear relaciones, el orden entre la tabla primaria y la tabla de búsqueda relacionada se fija de manera correcta automáticamente.  
  
2.  En la tabla **Internet Sales**, haga clic y mantenga seleccionada la columna **Due Date**, arrastre el cursor hasta la columna **Date** de la tabla **Date** y suéltelo.  
  
    Aparece una línea de puntos que indica que ha creado una relación inactiva entre la columna **Due Date** de la tabla **Internet Sales** y la columna **Date** de la tabla **Date**. Puede haber varias relaciones entre las tablas, pero solo una puede estar activa cada vez.  
  
3.  Por último, cree una relación más; en la tabla **Internet Sales**, haga clic y mantenga seleccionada la columna **Ship Date**, arrastre el cursor hasta la columna **Date** de la tabla **Date** y suéltelo.  
  
    Aparece una línea de puntos que indica que ha creado una relación inactiva entre la columna **Ship Date** de la tabla **Internet Sales** y la columna **Date** de la tabla **Date**.  
  
## Paso siguiente  
Para continuar esta lección, vaya a la lección siguiente: [Lección 6: Crear columnas calculadas](../analysis-services/lesson-6-create-calculated-columns.md).  
  
  
  
