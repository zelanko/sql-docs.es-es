---
title: Definir la granularidad de las dimensiones en un grupo de medida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4f079485-9eb4-405c-9a20-81258298b810
author: minewiskan
ms.author: owend
ms.openlocfilehash: 06d1b643ce53be3b263ea493a8594f8db7ff11c9
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542842"
---
# <a name="defining-dimension-granularity-within-a-measure-group"></a>Definir la granularidad de las dimensiones en un grupo de medida
  Los usuarios desearán dimensionar los datos de hechos con una granularidad o especificidad distinta para distintos objetivos. Por ejemplo, los datos de venta para las ventas de proveedor o ventas por Internet pueden registrarse cada día, mientras que es posible que la información sobre cuotas de venta solo exista en el nivel de mes o trimestre. En estos casos, los usuarios desearán una dimensión de tiempo con otra granularidad o un nivel de detalle distinto para cada una de las distintas tablas de hechos. Si bien puede definirse una nueva dimensión de base de datos como una dimensión de tiempo con esta granularidad diferente, hay una forma más fácil de hacerlo con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 De forma predeterminada, cuando en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]se usa una dimensión dentro de un grupo de medida, el nivel de detalle de los datos de esa dimensión se basa en el atributo clave de la dimensión. Por ejemplo, cuando se incluye una dimensión de tiempo en un grupo de medida y el nivel de detalle predeterminado de la dimensión de tiempo es diariamente, el nivel de detalle predeterminado de dicha dimensión dentro del grupo de medida es diariamente. Esto es a menudo muy apropiado, como en el caso de los grupos de medida **Internet Sales** y **Reseller Sales** de este tutorial. No obstante, cuando se incluye una dimensión de este tipo en otros tipos de grupos de medida, como en el grupo de medida de cuotas de venta o de presupuestos, generalmente es más apropiado utilizar un nivel de detalle mensual o trimestral.  
  
 Para especificar un nivel de detalle para una dimensión de cubo que no sea el predeterminado, debe modificar el atributo de granularidad para una dimensión de cubo como se utiliza en un grupo de medida determinado en la pestaña **Uso de dimensiones** del Diseñador de cubos. Si cambia el nivel de detalle de una dimensión de un grupo de medida específico por un atributo distinto del atributo clave de dicha dimensión, debe garantizar que todos los demás atributos del grupo de mensaje estén directa o indirectamente relacionados con el nuevo atributo de granularidad. Para ello, debe especificar las relaciones de atributo entre todos los demás atributos y el atributo que se ha especificado como atributo de granularidad en el grupo de medida. En este caso, se definen relaciones de atributo adicionales en vez de mover relaciones de atributo. El atributo que se especifica como atributo de granularidad se convierte efectivamente en el atributo clave del grupo de medida para el resto de atributos de la dimensión. Si no especifica correctamente las relaciones de atributo, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no podrá agregar los valores de forma correcta, como verá en las tareas de este tema.  
  
 Para obtener más información, consulte [Relaciones de dimensión](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)y [Definir relaciones normales y propiedades de las relaciones normales](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
 En las tareas de este tema, debe agregar un grupo de medida Sales Quotas y definir la granularidad de la dimensión Date en este grupo de modo que sea mensual. Después debe definir las relaciones de atributo existentes entre el atributo de mes y otros atributos de dimensión para asegurarse de que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] agregue los valores correctamente.  
  
## <a name="adding-tables-and-defining-the-sales-quotas-measure-group"></a>Agregar tablas y definir el grupo de medida Sales Quotas  
  
1.  Cambie a la vista del origen de datos **Adventure Works DW 2012** .  
  
2.  Haga clic con el botón secundario en cualquier lugar del panel **organizador de diagramas** , haga clic en **nuevo diagrama**y, a continuación, asigne un nombre al diagrama `Sales Quotas` .  
  
3.  Arrastre el **empleado**, el **territorio de ventas**y `Date` las tablas desde el panel **tablas** hasta el panel **Diagrama** .  
  
4.  Agregue la tabla **FactSalesQuota** al panel **Diagrama** haciendo clic con el botón derecho en cualquier punto del panel **Diagrama** y seleccionando **Agregar o quitar tablas**.  
  
     Observe que la tabla **SalesTerritory** está vinculada a la tabla **FactSalesQuota** a través de la tabla **Employee** .  
  
5.  Revise las columnas de la tabla **FactSalesQuota** y, a continuación, explore los datos de la tabla.  
  
     Observe que el nivel de detalle de los datos de esta tabla es trimestre natural, que es el nivel más bajo de detalle de la tabla FactSalesQuota.  
  
6.  En el diseñador de vistas del origen de datos, cambie la propiedad **FriendlyName** de la tabla **FactSalesQuota** a `SalesQuotas` .  
  
7.  Cambie al cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y haga clic en la pestaña **Estructura de cubo** .  
  
8.  Haga clic con el botón secundario en cualquier lugar del panel **medidas** , haga clic en **nuevo grupo de medida**, haga clic `SalesQuotas` en el cuadro de diálogo **nuevo grupo de medida** y, a continuación, haga clic en **Aceptar**.  
  
     El `Sales Quotas` grupo de medida aparece en el panel **medidas** . En el panel **dimensiones** , observe que `Date` también se define una nueva dimensión de cubo, basada en la dimensión de la `Date` base de datos. Se define una dimensión de cubo nueva relacionada con el tiempo porque [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no sabe qué dimensión de las existentes en el cubo y relacionada con el tiempo debe relacionar con la columna **DateKey** de la tabla de hechos **FactSalesQuota** subyacente del grupo de medida Sales Quotas. Cambiará este valor más adelante en otra tarea de este tema.  
  
9. Expanda el `Sales Quotas` grupo de medida.  
  
10. En el panel **Medidas** , seleccione **Sales Amount Quota**y, a continuación, establezca el valor de la propiedad **FormatString** en **Currency** en la ventana Propiedades.  
  
11. Seleccione la medida **sales Quotas Count** y, a continuación, escriba `#,#` como el valor de la propiedad **FormatString** en el ventana Propiedades.  
  
12. Elimine la medida **Calendar Quarter** del `Sales Quotas` grupo de medida.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ha detectado la columna que subyace en la medida Calendar Quarter como columna que contiene medidas. No obstante, esta columna y la columna CalendarYear contienen los valores que más adelante en este tema utilizará para vincular el grupo de medida Sales Quotas con la dimensión Date.  
  
13. En el panel **medidas** , haga clic con el botón secundario en el `Sales Quotas` grupo de medida y, a continuación, haga clic en **nueva medida**.  
  
     Se abre el cuadro de diálogo **Nueva medida** , que contiene las columnas de origen disponibles para una medida con un tipo de uso **Suma**.  
  
14. En el cuadro de diálogo **nueva medida** , **Seleccione recuento distinto** en la lista **uso** , compruebe que `SalesQuotas` está seleccionado en la lista **tabla de origen** , seleccione **EmployeeKey** en la lista columna de **origen** y, a continuación, haga clic en **Aceptar**.  
  
     Observe que la medida se crea en un grupo de medida nuevo denominado **Sales Quotas 1**. A fin de maximizar el rendimiento del procesamiento, en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se crean medidas de recuento distintas en los grupos de medida correspondientes.  
  
15. Cambie el valor de la propiedad **nombre** de la medida **Employee Key DISTINCT Count** a y, `Sales Person Count` a continuación, escriba `#,#` como el valor de la propiedad **FormatString** .  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Examinar las medidas del grupo de medida Sales Quota por fecha  
  
1.  En el menú **Compilar** , haga clic en **Tutorial de Implementar Analysis Services**.  
  
2.  Cuando la implementación se haya completado correctamente, haga clic en la pestaña **Explorador** del Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, a continuación, haga clic en el botón **Volver a conectar** .  
  
3.  Haga clic en el acceso directo de Excel y, a continuación, haga clic en **Habilitar**.  
  
4.  En la lista de campos de tabla dinámica, expanda el `Sales Quotas` grupo de medida y, a continuación, arrastre la medida **sales amount quota** hasta el área valores.  
  
5.  Expanda la dimensión **Sales Territory** y arrastre la jerarquía definida por el usuario **Sales Territories** hasta las etiquetas de fila.  
  
     Observe que la dimensión de cubo Sales Territory no está relacionada, directa ni indirectamente, con la tabla de hechos Sales Quota, como se muestra en la imagen siguiente.  
  
     ![Dimensión de cubo de territorio de ventas](../../2014/tutorials/media/l5-granularity-2.gif "Dimensión del cubo Sales Territory")  
  
     En la próxima serie de pasos de este tema definirá una relación de dimensión de referencia entre esta dimensión y esta tabla de hechos.  
  
6.  Mueva la jerarquía de usuario **Territorios de ventas** del área Etiquetas de fila al área Etiquetas de columna.  
  
7.  En la lista de campos de tabla dinámica, seleccione la jerarquía definida por el usuario **Sales Territories** y haga clic en la flecha hacia abajo de la derecha.  
  
     ![Jerarquía Sales Territories en la lista de campos](../../2014/tutorials/media/l5-granularity-1a.png "Jerarquía Sales Territories en la lista de campos")  
  
8.  En el filtro, haga clic en la casilla Seleccionar todo para desactivar todas las casillas y elija solo **Norteamérica**.  
  
     ![Panel Filtro para seleccionar North America](../../2014/tutorials/media/l5-granularity-1b.png "Panel Filtro para seleccionar North America")  
  
9. En la lista de campos de tabla dinámica, expanda `Date` .  
  
10. Arrastre la jerarquía de usuario **Date.Fiscal Date** hasta Etiquetas de fila.  
  
11. En la tabla dinámica, haga clic en la flecha hacia abajo que aparece junto a Etiquetas de fila. Desactive todos los años excepto **FY 2008**.  
  
     Observe que solo aparece el miembro **2007 de julio** del nivel **Month** , en lugar de los miembros **julio, 2007**, **agosto, 2007**y **septiembre, 2007** del nivel **Month** , y que solo aparece el miembro de **Julio 1, 2007** del `Date` nivel, en lugar de los 31 días. Este comportamiento se produce porque el nivel de detalle de los datos de la tabla de hechos es el nivel de trimestre y el grano de la `Date` dimensión es el nivel diario. Cambiará este comportamiento en la siguiente tarea de este tema.  
  
     Observe también que el valor de **Sales Amount Quota** para los niveles de mes y día es el mismo valor que aparece en el nivel de trimestre, $13.733.000,00. Esto es así porque el nivel más bajo de datos del grupo de medida Sales Quotas se encuentra en el nivel de trimestre. Cambiará este comportamiento en la lección 6.  
  
     En la imagen siguiente se muestran los valores para **Sales Amount Quota**.  
  
     ![Valores de Sales Amount Quota](../../2014/tutorials/media/l5-granularity-3.png "Valores de Sales Amount Quota")  
  
## <a name="defining-dimension-usage-properties-for-the-sales-quotas-measure-group"></a>Definir las propiedades de uso de dimensiones para el grupo de medida Sales Quotas  
  
1.  Abra el Diseñador de dimensiones para la dimensión **Employee** , haga clic con el botón derecho en **SalesTerritoryKey** en el panel **Vista del origen de datos** y, después, haga clic en **Nuevo atributo de columna**.  
  
2.  En el panel **Atributos** , seleccione **SalesTerritoryKey**y, a continuación, establezca la propiedad **AttributeHierarchyVisible** en **False** en la ventana de propiedades, la propiedad **AttributeHierarchyOptimizedState** en **NotOptimized**y la propiedad **AttributeHierarchyOrdered** en **False**.  
  
     Este atributo es necesario para vincular la dimensión de **territorio de ventas** a los `Sales Quotas` grupos de medida y **sales Quotas 1** como una dimensión a la que se hace referencia.  
  
3.  En el diseñador de cubos para el [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo tutorial de, haga clic en la pestaña **uso de dimensiones** y, a continuación, revise el uso de las dimensiones dentro de los `Sales Quotas` grupos de medida y **cuotas de ventas 1** .  
  
     Observe que las dimensiones **Employee** y `Date` Cube están vinculadas a los grupos de medida **sales Quotasand sales Quotas 1** a través de relaciones normales. Observe también que la dimensión de cubo **Sales Territory** no está vinculada a ninguno de estos grupos de medida.  
  
4.  Haga clic en la celda en la intersección de la dimensión **territorio de ventas** y el `Sales Quotas` grupo de medida y, a continuación, haga clic en el botón Examinar (**...**). Se abre el cuadro de diálogo **definir relación** .  
  
5.  En la lista **Seleccionar tipo de relación** , seleccione **Referenciada**.  
  
6.  En la lista **Dimensión intermedia** , seleccione **Employee**.  
  
7.  En la lista **Atributo de dimensión de referencia** , **Sales Territory Region.**  
  
8.  En la lista **Atributo de dimensión intermedia** , seleccione **Sales Territory Key** (la columna de clave para el atributo Sales Territory Region es la columna SalesTerritoryKey).  
  
9. Compruebe que la casilla **Materializar** está activada.  
  
10. Haga clic en **OK**.  
  
11. Haga clic en la celda en la intersección de la dimensión **territorio de ventas** y el grupo de medida **sales Quotas 1** y, a continuación, haga clic en el botón Examinar (**...**). Se abre el cuadro de diálogo **definir relación** .  
  
12. En la lista **Seleccionar tipo de relación** , seleccione **Referenciada**.  
  
13. En la lista **Dimensión intermedia** , seleccione **Employee**.  
  
14. En la lista **Atributo de dimensión de referencia** , **Sales Territory Region.**  
  
15. En la lista **Atributo de dimensión intermedia** , seleccione **Sales Territory Key** (la columna de clave para el atributo Sales Territory Region es la columna SalesTerritoryKey).  
  
16. Compruebe que la casilla **Materializar** está activada.  
  
17. Haga clic en **OK**.  
  
18. Elimine la `Date` dimensión de cubo.  
  
     En lugar de tener cuatro dimensiones de cubo relacionadas con el tiempo, utilizará la dimensión de cubo **Order Date** del `Sales Quotas` grupo de medida como la fecha en la que se dimensionarán las cuotas de ventas. También utilizará esta dimensión de cubo como dimensión de fecha principal del cubo.  
  
19. En la lista **dimensiones** , cambie el nombre de la dimensión de cubo **Order Date** a `Date` .  
  
     Cambiar el nombre de la dimensión de cubo **Order Date** para `Date` facilitar a los usuarios comprender su rol como dimensión de fecha principal en este cubo.  
  
20. Haga clic en el botón Examinar (**...**) de la celda en la intersección del `Sales Quotas` grupo de medida y la `Date` dimensión.  
  
21. En el cuadro de diálogo **Definir relación** , seleccione **Regular** en la lista **Seleccionar tipo de relación** .  
  
22. En la lista **Atributo de granularidad** , seleccione **Calendar Quarter**.  
  
     Observe que aparece un mensaje de advertencia para notificarle que, puesto que ha seleccionado un atributo sin clave como atributo de granularidad, debe especificar todos los demás atributos como propiedades de miembro para asegurarse de que estén relacionados directa o indirectamente con el atributo de granularidad.  
  
23. En el área **Relación** del cuadro de diálogo **Definir relación** , vincule las columnas de dimensión **CalendarYear** y **CalendarQuarter** de la tabla que subyace en la dimensión de cubo Date con las columnas **CalendarYear** y **CalendarQuarter** de la tabla que subyace en el grupo de medida Sales Quota y, a continuación, haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Calendar Quarter se define como atributo de granularidad de la dimensión de cubo Date en el grupo de medida Sales Quotas, pero el atributo Date sigue siendo el atributo de granularidad para los grupos de medida Internet Sales y Reseller Sales.  
  
24. Repita los cuatro pasos anteriores para el grupo de medida **Sales Quotas 1** .  
  
## <a name="defining-attribute-relationships-between-the-calendar-quarter-attribute-and-the-other-dimension-attributes-in-the-date-dimension"></a>Definir las relaciones de atributo entre el atributo Calendar Quarter y otros atributos de dimensión de la dimensión Date  
  
1.  Cambie al **Diseñador de dimensiones** para la `Date` dimensión y, a continuación, haga clic en la pestaña **relaciones de atributo** .  
  
     Tenga en cuenta que aunque el **año natural** está vinculado al **trimestre natural** a través del atributo **Calendar** Quarter, los atributos del calendario fiscal solo se vinculan entre sí; no se vinculan al atributo **Calendar Quarter** y, por lo tanto, no se agregarán correctamente en el `Sales Quotas` grupo de medida.  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **Calendar Quarter** y seleccione **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Calendar Quarter**. Establezca el **Atributo relacionado** en **Fiscal Quarter**.  
  
4.  Haga clic en **OK**.  
  
     Observe que aparece un mensaje de advertencia que indica que la `Date` dimensión contiene una o varias relaciones de atributo redundantes que pueden impedir que se agreguen datos cuando se usa un atributo sin clave como atributo de granularidad.  
  
5.  Elimine la relación de atributo entre los atributos **Month Name** y **Fiscal Quarter** .  
  
6.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="browsing-the-measures-in-the-sales-quota-measure-group-by-date"></a>Examinar las medidas del grupo de medida Sales Quota por fecha  
  
1.  En el menú **Compilar** , haga clic en **Tutorial de Implementar Analysis Services**.  
  
2.  Cuando la implementación se haya completado correctamente, haga clic en la pestaña **Explorador** del Diseñador de cubos para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, a continuación, haga clic en **Volver a conectar**.  
  
3.  Haga clic en el acceso directo de Excel y, a continuación, haga clic en **Habilitar**.  
  
4.  Arrastre la medida **Sales Amount Quota** hasta el área Valores.  
  
5.  Arrastre la jerarquía de usuario **Territorios de ventas** hasta las Etiquetas de columna y, a continuación, filtre en **Norteamérica**.  
  
6.  Arrastre la jerarquía de usuario **Date.FiscalDate** hasta Etiquetas de fila y, a continuación, haga clic en la flecha hacia abajo que aparece junto a **Etiquetas de fila** en la tabla dinámica y desactive todas las casillas excepto **FY 2008**para mostrar solamente el año fiscal 2008.  
  
7.  Haga clic en Aceptar.  
  
8.  Expanda sucesivamente **FY 2008**, **H1 FY 2008**y **Q1 FY 2008**.  
  
     En la ilustración siguiente se muestra una tabla dinámica para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , con el grupo de medida Sales Quota bien dimensionado.  
  
     Observe que cada miembro del nivel de trimestre fiscal tiene el mismo valor que el nivel de trimestre. Usando **Q1 FY 2008** como ejemplo, la cuota de $9.180.000, 00 para **Q1 FY 2008** es también el valor de cada uno de sus miembros. Este comportamiento se produce porque el nivel de detalle de los datos de la tabla de hechos es el nivel trimestral y el nivel de detalle de la dimensión Date también es el nivel de trimestre. En la lección 6, aprenderá a asignar el importe trimestral proporcionalmente a cada mes.  
  
     ![Grupo de medida Sales Quota con dimensiones correctas](../../2014/tutorials/media/l5-granularity-7.gif "Grupo de medida Sales Quota con dimensiones correctas")  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 6: definir cálculos](lesson-6-defining-calculations.md)  
  
## <a name="see-also"></a>Consulte también  
 [Relaciones de dimensión](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Definir una relación normal y propiedades de relación normal](multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)   
 [Trabajar con diagramas en el Diseñador de vistas del origen de datos &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
