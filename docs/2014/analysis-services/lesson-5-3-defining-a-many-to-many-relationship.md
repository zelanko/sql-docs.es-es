---
title: Definir una relación de varios a varios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b7b091c6e963af043533bfe362a801d7d4c91f2
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2019
ms.locfileid: "69493875"
---
# <a name="defining-a-many-to-many-relationship"></a>Definir una relación de varios a varios
  Generalmente, cuando se define una dimensión cada hecho se combina con un único miembro de dimensión, mientras que un mismo miembro puede estar asociado a varios hechos distintos. Por ejemplo, cada cliente puede tener varios pedidos, pero cada pedido pertenece a un solo cliente. En terminología de bases de datos relacionales, esto se conoce como *relación uno a varios*. No obstante, algunas veces un único hecho puede combinarse con varios miembros de dimensión. En terminología de bases de datos relacionales, esto se conoce como *relación de varios a varios*. Por ejemplo, un cliente puede tener varios motivos para realizar una compra, y un motivo de compra puede estar asociado a varias compras. Para definir los motivos de venta que se relacionan con cada compra, se utiliza una tabla de combinación. Una dimensión de motivo de venta creada a partir de relaciones de este tipo tendría varios miembros que estarían relacionados a una única transacción de venta. Las dimensiones de varios a varios amplían el modelo dimensional más allá del esquema de estrella y admiten análisis complejos cuando las dimensiones no están directamente relacionadas con una tabla de hechos.  
  
 En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], para definir una relación de varios a varios entre una dimensión y un grupo de medida se especifica una tabla de hechos intermedia que está combinada con la tabla de dimensiones. Una tabla de hechos intermedia, a su vez, se combina con una tabla de dimensiones intermedia con la que la tabla de hechos está combinada. Las relaciones de varios a varios entre la tabla de hechos intermedia y las tablas de dimensiones de la relación y la dimensión intermedia crean las relaciones de varios a varios entre los miembros de dimensión primaria y las medidas del grupo de medida especificado por la relación. Para definir una relación de varios a varios entre una dimensión y un grupo de medida a través de un grupo de medida intermedio, el grupo de medida intermedio debe compartir una o varias dimensiones con el grupo de medida original.  
  
 Con una dimensión de varios a varios, los valores distintos se suman, lo que significa que no se agregan más de una vez al miembro Todos.  
  
> [!NOTE]  
>  Para admitir una relación de dimensión de varios a varios, se debe definir una relación de clave principal y clave externa en la vista del origen de datos entre todas las tablas implicadas. De lo contrario, no podrá seleccionar el grupo de medida intermedio correcto cuando establezca la relación en la pestaña **Uso de dimensiones** del Diseñador de cubos.  
  
 Para obtener más información, consulte [Relaciones de dimensión](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)y [Definir una relación de varios a varios y las propiedades de las relaciones de varios a varios](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
 En las tareas de este tema, debe definir la dimensión Sales Reasons y el grupo de medida Sales Reasons, y definir una relación de varios a varios entre la dimensión Sales Reasons y el grupo de medida Internet Sales a través del grupo de medida Sales Reasons.  
  
## <a name="adding-required-tables-to-the-data-source-view"></a>Agregar tablas necesarias a la vista del origen de datos  
  
1.  Abra el Diseñador de vistas del origen de datos para la vista del origen de datos **Adventure Works DW 2012** .  
  
2.  Haga clic con el botón secundario en cualquier lugar del panel **organizador de diagramas** , `Internet Sales Order Reasons` haga clic en **nuevo diagrama**y especifique como nombre de este nuevo diagrama.  
  
3.  Arrastre la tabla **InternetSales** al panel **Diagrama** desde el panel **Tablas** .  
  
4.  Haga clic con el botón derecho en cualquier punto del panel **Diagrama** y luego haga clic en **Agregar o quitar tablas**.  
  
5.  En el cuadro de diálogo **Agregar o quitar tablas** , agregue la tabla **DimSalesReason** y la tabla **FactInternetSalesReason** a la lista **Objetos incluidos** y haga clic en **Aceptar**.  
  
     Observe que las relaciones de clave principal y clave externa entre las tablas implicadas se establecen automáticamente porque dichas relaciones se definen en la base de datos relacional subyacente. Si dichas relaciones no se hubiesen definido en la base de datos relacional subyacente, tendría que definirlas en la vista del origen de datos.  
  
6.  En el menú **Formato** , seleccione **Diseño automático**y haga clic en **Diagrama**.  
  
7.  En el ventana Propiedades, cambie la propiedad **FriendlyName** de la tabla **DimSalesReason** a `SalesReason`y, a continuación, cambie la propiedad **FriendlyName** de la tabla `InternetSalesReason` **FactInternetSalesReason** a.  
  
8.  En el panel **Tablas** , expanda **InternetSalesReason (dbo.FactInternetSalesReason)** , haga clic en **SalesOrderNumber**y luego revise la propiedad **DataType** para esta columna de datos en la ventana Propiedades.  
  
     Observe que el tipo de datos para la columna **SalesOrderNumber** es un tipo de datos de cadena.  
  
9. Revise los tipos de datos de las demás columnas de `InternetSalesReason` la tabla.  
  
     Observe que los datos de las otras dos columnas de esta tabla son de tipo numérico.  
  
10. En el panel **Tablas** , haga clic con el botón derecho en **InternetSalesReason (dbo.FactInternetSalesReason)** y seleccione **Explorar datos**.  
  
     Observe que, para cada número de línea de cada pedido, un valor clave identifica el motivo de venta para la compra del artículo de la línea, como se muestra en la imagen siguiente.  
  
     ![Valor de clave para identificar el motivo de venta para las compras](../../2014/tutorials/media/l5-many-to-many-1.gif "Valor de clave para identificar el motivo de venta para las compras")  
  
## <a name="defining-the-intermediate-measure-group"></a>Definir el grupo de medida intermedio  
  
1.  Cambie al Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y haga clic en la pestaña **Estructura de cubo** .  
  
2.  Haga clic con el botón derecho en cualquier punto del panel **Medidas** y, después, haga clic en **Nuevo grupo de medida**. Para obtener más información, consulte [Crear medidas y grupos de medida en modelos multidimensionales](multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md).  
  
3.  En el cuadro de diálogo **nuevo grupo** de medida `InternetSalesReason` , seleccione en la lista **Seleccione una tabla de la vista del origen de datos** y, a continuación, haga clic en **Aceptar**.  
  
     Observe que el grupo de medida **Internet Sales Reason** ahora aparece en el panel **Medidas** .  
  
4.  Expanda el grupo de medida **Internet Sales Reason** .  
  
     Como puede observar, solo hay una medida definida para este nuevo grupo de medida, la medida **Internet Sales Reason Count** .  
  
5.  Seleccione **Internet Sales Reason Count** y revise las propiedades de esta medida en la ventana Propiedades.  
  
     Observe que la propiedad **AggregateFunction** para esta medida está definida como **Recuento** en lugar de como **Suma**. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionó **Recuento** porque el tipo de datos subyacente es un tipo de datos de cadena. Las otras dos columnas de la tabla de hechos subyacente no estaban seleccionadas como medias porque [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] las detectó como claves numéricas y no como medidas reales. Para obtener más información, consulte [Definir el comportamiento de suma parcial](multidimensional-models/define-semiadditive-behavior.md).  
  
6.  En la ventana Propiedades, cambie la propiedad **Visible** de la medida **Internet Sales Reason Count** a **False**.  
  
     Esta medida solo podrá utilizarse para combinar la dimensión Sales Reason que definirá junto al grupo de medida Internet Sales. Los usuarios no examinarán esta medida directamente.  
  
     En la ilustración siguiente se muestran las propiedades de la medida **Internet Sales Reason Count** .  
  
     ![Propiedades de la medida Internet sales Reason Count](../../2014/tutorials/media/l5-many-to-many-2.gif "Propiedades de la medida Internet sales Reason Count")  
  
## <a name="defining-the-many-to-many-dimension"></a>Definir la dimensión de varios a varios  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en **Dimensiones**y, después, haga clic en **Nueva dimensión**.  
  
2.  En la página **Asistente para dimensiones** , haga clic en **Siguiente**.  
  
3.  En la página **Seleccionar método de creación** , compruebe que la opción **Usar una tabla existente** está seleccionada y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página **Especificar información de origen** , compruebe que la vista del origen de datos [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 está seleccionada.  
  
5.  En la lista **tabla principal** , seleccione `SalesReason`.  
  
6.  En la lista **Columnas de clave** , compruebe que aparece **SalesReasonKey** .  
  
7.  En la lista **Columna de nombre** , seleccione **SalesReasonName**.  
  
8.  Haga clic en **Siguiente**.  
  
9. En la página **Seleccionar los atributos de la dimensión** , el atributo **Sales Reason Key** se selecciona automáticamente porque es el atributo clave. Active la casilla situada junto al atributo **sales Reason Reason Type** , cambie su nombre a `Sales Reason Type`y, a continuación, haga clic en **siguiente**.  
  
10. En la página **Finalización del asistente** , haga clic en **Finalizar** para crear la dimensión Sales Reason.  
  
11. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
12. En el panel **atributos** del diseñador de dimensiones para la dimensión **sales Reason** , seleccione **sales Reason Key**y, a continuación, cambie la propiedad **Name** en el ventana Propiedades a`Sales Reason.`  
  
13. En el panel **jerarquías** del diseñador de dimensiones, cree una jerarquía de usuario **sales reasons** que `Sales Reason Type` contenga el nivel y el nivel **sales Reason** , en ese orden.  
  
14. En el ventana Propiedades, defina `All Sales Reasons` como el valor de la propiedad **AllMemberName** de la jerarquía sales reasons.  
  
15. Defina `All Sales Reasons` como el valor de la propiedad **AttributeAllMemberName** de la dimensión sales Reason.  
  
16. Para agregar la dimensión que acaba de crear al cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como una dimensión de cubo, cambie al **Diseñador de cubos**. En la pestaña **Estructura de cubo** , haga clic con el botón derecho en el panel **Dimensiones** y seleccione **Agregar dimensión de cubo**.  
  
17. En el cuadro de diálogo **Agregar dimensión de cubo** , seleccione **Sales Reason** y, a continuación, haga clic en **Aceptar**.  
  
18. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-the-many-to-many-relationship"></a>Definir la relación de varios a varios  
  
1.  Cambie al Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y haga clic en la pestaña **Uso de dimensiones** .  
  
     Observe que la dimensión **Sales Reason** tiene una relación regular definida con el grupo de medida **Internet Sales Reason** , pero no tiene ninguna relación definida con los grupos de medida **Internet Sales** ni **Reseller Sales** . Observe también que la dimensión **Internet Sales Order Details** tiene una relación normal definida con la dimensión **Internet Sales Reason** , que a su vez tiene una **relación de hechos** con el grupo de medida **Internet Sales** . Si esta dimensión no estaba presente (u otra dimensión con una relación con **Internet Sales Reason** y el grupo de medida **Internet Sales** no estaban presentes), no se podría definir la relación de varios a varios.  
  
2.  Haga clic en la celda en la intersección del grupo de medida **Internet Sales** y la dimensión **Sales Reasons** y, después, haga clic en el botón Examinar ( **…** ).  
  
3.  En el cuadro de diálogo **Definir relación** , seleccione **Varios a varios** en la lista **Seleccionar tipo de relación** .  
  
     Debe definir el grupo de medida intermedio que conecta la dimensión Sales Reason al grupo de medida Internet Sales.  
  
4.  En la lista **Grupo de medida intermedio** , seleccione **Internet Sales Reason**.  
  
     En la imagen siguiente se muestran los cambios realizados en el cuadro de diálogo **Definir relación** .  
  
     ![Definir relación (cuadro de diálogo)](../../2014/tutorials/media/l5-many-to-many-3.gif "Definir relación (cuadro de diálogo)")  
  
5.  Haga clic en **Aceptar**.  
  
     Observe el icono de varios a varios que representa la relación existente entre la dimensión Sales Reason y el grupo de medida Internet Sales.  
  
## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>Examinar el cubo y la dimensión de varios a varios  
  
1.  En el menú **Compilar** , haga clic en **Tutorial de Implementar Analysis Services**.  
  
2.  Cuando la implementación se haya completado correctamente, cambie a la pestaña **Explorador** del Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, a continuación, haga clic en **Volver a conectar**.  
  
3.  Agregue la medida **Internet Sales-Sales Amount** al área de datos del panel de datos.  
  
4.  Agregue la jerarquía definida por el usuario **Sales Reason** de la dimensión **Sales Reason** al área de filas del panel de datos.  
  
5.  En el panel de metadatos, expanda sucesivamente **Customer**, **Location**, **Customer Geography**, **Members**, **All Customers**y **Australia**, haga clic con el botón derecho en **Queensland**y, después, haga clic en **Agregar a filtro**.  
  
6.  Expanda cada miembro del `Sales Reason Type` nivel para revisar los valores en dólares que están asociados a cada razón que un cliente de Queensland dio por su compra [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] de un producto a través de Internet.  
  
     Observe que los totales que están asociados con cada motivo de ventas se suman y dan lugar a un valor superior a las ventas totales. Esto es así porque algunos clientes citaron varios motivos para su compra.  
  
     En la imagen siguiente se muestran los paneles **Filtro** y **Datos** del Diseñador de cubos.  
  
     ![Paneles de filtros y datos del diseñador de cubos](../../2014/tutorials/media/l5-many-to-many-5.gif "Paneles de filtros y datos del diseñador de cubos")  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Definir la granularidad de las dimensiones en un grupo de medida](lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con diagramas en el Diseñador de vistas del origen de datos &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [Relaciones de dimensión](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Definir una relación de varios a varios y las propiedades de las relaciones de varios a varios](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)  
  
  
