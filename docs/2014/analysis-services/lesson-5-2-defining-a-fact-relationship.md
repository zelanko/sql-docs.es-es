---
title: Definir una relación de hechos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 4b49a078-6848-4286-bc71-cf4862d29064
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b66614a40176a0c6ee0ac4b0b9283fc0415ecc1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728727"
---
# <a name="defining-a-fact-relationship"></a>Definir una relación de hechos
  A veces, los usuarios desean poder dimensionar las medidas según los elementos de datos que se encuentran en la tabla de hechos o realizar consultas en la tabla de hechos sobre determinada información relacionada adicional, como números de factura o números de pedidos de compra relacionados con hechos de venta específicos. Cuando se define una dimensión basada en un elemento de tabla de hechos de este tipo, la dimensión se conoce como *dimensión de hechos*. Las dimensiones de hechos también se denominan dimensiones degeneradas. Las dimensiones de hechos son útiles para agrupar filas de tablas de hechos relacionadas, como todas las filas que están relacionadas con un número de factura determinado. Aunque esta información puede colocarse en una tabla de dimensiones independiente de la base de datos relacional, crear una tabla de dimensiones independiente para la información no supone ninguna ventaja, ya que la tabla de dimensiones crecerá al mismo ritmo que la tabla de hechos, y simplemente crearía datos duplicados y una complejidad innecesaria.  
  
 En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede determinar si los datos de las dimensiones de hechos deben duplicarse en una estructura de dimensiones MOLAP para incrementar el rendimiento de las consultas o si es necesario definir una dimensión de hechos como dimensión ROLAP para ahorrar espacio a costa del rendimiento de las consultas. Cuando se almacena una dimensión en modo de almacenamiento MOLAP, todos los miembros de la dimensión se almacenan en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en una estructura MOLAP muy comprimida, además de almacenarse en las particiones del grupo de medida. Al almacenar una dimensión con el modo de almacenamiento ROLAP, se almacena la definición de la dimensión en el MOLAP miembros de estructura de la dimensión propiamente dichos se consultan de la tabla de hechos relacionales subyacente en tiempo de consulta. El modo de almacenamiento adecuado se decide en función de la frecuencia con la que se consultan las dimensiones de hechos, el número de filas que devuelve una consulta típica, el rendimiento de la consulta y el costo de procesamiento. Para definir una dimensión como ROLAP, no es necesario almacenar todos los cubos que utilizan la dimensión con el mismo modo de almacenamiento ROLAP. El modo de almacenamiento de cada dimensión se puede configurar independientemente.  
  
 Cuando define una dimensión de hechos, puede definir la relación entre la dimensión de hechos y el grupo de medida como relación de hechos. Las relaciones de hechos presentan estas limitaciones:  
  
-   El atributo de granularidad debe encontrarse en la columna de clave de la dimensión, que crea una relación uno a uno entre la dimensión y los hechos de la tabla de hechos.  
  
-   Una dimensión puede tener una relación de hechos con un solo grupo de medida.  
  
> [!NOTE]  
>  Las dimensiones de hechos deben actualizarse de forma incremental después de cada actualización realizada en el grupo de medida al que hace referencia la relación de hechos.  
  
 Para obtener más información, consulte [Relaciones de dimensión](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)y [Definir relaciones de hechos y propiedades de las relaciones de hechos](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
 En las tareas de este tema, debe agregar una nueva dimensión de cubo basada en la columna **CustomerPONumber** de la tabla de hechos **FactInternetSales** . Después debe definir la relación entre esta nueva dimensión de cubo y el grupo de medida **Internet Sales** como relación de hechos.  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>Definir la dimensión de hechos de los pedidos de ventas por Internet  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en **Dimensiones**y, después, haga clic en **Nueva dimensión**.  
  
2.  En la página **Asistente para dimensiones** , haga clic en **Siguiente**.  
  
3.  En la página **Seleccionar método de creación** , compruebe que la opción **Usar una tabla existente** está seleccionada y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página **Especificar información de origen** , compruebe que la vista del origen de datos **Adventure Works DW 2012** está seleccionada.  
  
5.  En la lista **Tabla principal** , seleccione **InternetSales**.  
  
6.  Compruebe que aparecen **SalesOrderNumber** y **SalesOrderLineNumber** en la lista **Columnas de clave** .  
  
7.  En la lista **Columna de nombre** , seleccione **SalesOrderLineNumber**.  
  
8.  Haga clic en **Siguiente**.  
  
9. En la página **Seleccionar tablas relacionadas** , desactive las casillas que aparecen al lado de todas las tablas y, después, haga clic en **Siguiente**.  
  
10. En la página **Seleccionar los atributos de la dimensión** , haga clic dos veces en la casilla del encabezado para desactivar todas las casillas. El atributo **Sales Order Number** seguirá seleccionado porque es el atributo clave.  
  
11. Seleccione el atributo **Customer PO Number** y, después, haga clic en **Siguiente**.  
  
12. En la página **Finalización del asistente** , cambie el nombre por **Internet Sales Order Details** y, después, haga clic en **Finalizar** para completar el asistente.  
  
13. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
14. En el **atributos** panel del Diseñador de dimensiones para la **Internet Sales Order Details** dimensión, seleccione **Sales Order Number**y, a continuación, cambie el  **Nombre** propiedad en la ventana Propiedades para `Item Description.`  
  
15. En el **NameColumn** propiedad de celda, haga clic en el botón Examinar **(...)** . En el cuadro de diálogo **Columna de nombre** , seleccione **Product** en la lista **Tabla de origen** , seleccione **EnglishProductName** en **Columna de origen**y, después, haga clic en **Aceptar**.  
  
16. Agregue el atributo **Sales Order Number** a la dimensión arrastrando la columna **SalesOrderNumber** de la tabla **InternetSales** del panel **Vista del origen de datos** al panel **Atributos** .  
  
17. Cambiar el **nombre** propiedad del nuevo **Sales Order Number** atribuir a `Order Number`y cambie el **OrderBy** propiedad **clave**.  
  
18. En el **jerarquías** panel, cree un **Internet Sales Orders** jerarquía de usuario que contiene el `Order Number` y **Item Description** niveles, en ese orden.  
  
19. En el panel **Atributos** , seleccione **Internet Sales Order Details**y luego revise el valor de la propiedad **StorageMode** en la ventana Propiedades.  
  
     Observe que, de forma predeterminada, esta dimensión está almacenada como dimensión MOLAP. Aunque cambiar el modo de almacenamiento por ROLAP supondrá un ahorro de tiempo de procesamiento y espacio de almacenamiento, esto es así a costa del rendimiento de las consultas. Para este tutorial, utilizará MOLAP como modo de almacenamiento.  
  
20. Para agregar la dimensión que acaba de crear al cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como una dimensión de cubo, cambie al **Diseñador de cubos**. En la pestaña **Estructura de cubo** , haga clic con el botón derecho en el panel **Dimensiones** y seleccione **Agregar dimensión de cubo**.  
  
21. En el cuadro de diálogo **Agregar dimensión de cubo**, seleccione **Internet Sales Order Details** y, después, haga clic en **Aceptar**.  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>Definir una relación de hechos para la dimensión de hechos  
  
1.  En el Diseñador de cubos del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , haga clic en la pestaña **Uso de dimensiones** .  
  
     Observe que la dimensión de cubo **Internet Sales Order Details** está configurada automáticamente con una relación de hechos, como indica el icono único.  
  
2.  Haga clic en el botón Examinar (**...** ) en el **Item Description** celda en la intersección de la **Internet Sales** grupo de medida y la **Internet Sales Order Details** dimensión, Revise las propiedades de relación de hechos.  
  
     Se abre el cuadro de diálogo **Definir relación** . Observe que no puede configurar ninguna de las propiedades.  
  
     En la imagen siguiente se muestran las propiedades de la relación de hechos en el cuadro de diálogo **Definir relación** .  
  
     ![Cuadro de diálogo Definir relación](../../2014/tutorials/media/l5-factrelationship-2.gif "cuadro de diálogo Definir relación")  
  
3.  Haga clic en **Cancelar**.  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>Examinar el cubo utilizando la dimensión de hecho  
  
1.  En el menú **Generar** , haga clic en **Implementar tutorial de Analysis Services** para implementar los cambios realizados en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y procesar la base de datos.  
  
2.  Cuando la implementación se haya completado correctamente, haga clic en la pestaña **Explorador** del Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, después, haga clic en el botón **Volver a conectar** .  
  
3.  Borre todas las medidas y las jerarquías del panel de datos y, después, agregue la medida **Internet Sales-Sales Amount** al área de datos de dicho panel.  
  
4.  En el panel de metadatos, expanda sucesivamente **Customer**, **Location**, **Customer Geography**, **Members**, **All Customers**, **Australia**, **Queensland**, **Brisbane**, **4000**, haga clic con el botón derecho en **Adam Powell**y, después, haga clic en **Agregar a filtro**.  
  
     La aplicación de un filtro para limitar los pedidos de venta que se devuelven a un único cliente permite al usuario obtener detalles en una tabla de hechos de gran tamaño sin tener que sufrir una notable pérdida en el rendimiento de las consultas.  
  
5.  Agregue la jerarquía definida por el usuario **Internet Sales Orders** de la dimensión **Internet Sales Order Details** al área de filas del panel de datos.  
  
     Observe que en el panel de datos aparecen los números de pedidos de venta y los importes correspondientes de ventas por Internet para Adam Powell.  
  
     En la imagen siguiente se muestra el resultado de los pasos anteriores.  
  
     ![El dimensionamiento de Internet Sales-Sales Amount](../../2014/tutorials/media/l5-factrelationship-3.gif "acotación de Internet Sales-Sales Amount")  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Definir una relación de varios a varios](../analysis-services/lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>Vea también  
 [Relaciones de dimensión](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Definir relaciones de hechos y propiedades de las relaciones de hechos](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
