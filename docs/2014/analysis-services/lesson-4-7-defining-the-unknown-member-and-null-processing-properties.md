---
title: Definir el miembro desconocido y propiedades de procesamiento de valores Null | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d9abb09c-9bfa-4e32-b530-8590e4383566
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5982bd49a5b7847cb8c09a7e46ca077bbe0e2d2b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521616"
---
# <a name="defining-the-unknown-member-and-null-processing-properties"></a>Definir las propiedades de miembro desconocido y de procesamiento de valores NULL
  Cuando [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] procesa una dimensión, todos los valores distintos de las columnas subyacentes de las tablas o las vistas de la vista del origen de datos rellenan los atributos de la dimensión. Si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encuentra una valor NULL durante el procesamiento, de forma predeterminada, convierte este valor NULL en un cero en las columnas numéricas o en una cadena vacía en las columnas de cadena. Puede modificar estas opciones predeterminadas o convertir los valores NULL en el proceso de extracción, transformación y carga (si existe) del almacenamiento de datos relacional subyacente. También puede hacer que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] convierta el valor NULL en un valor determinado configurando tres propiedades: las propiedades **UnknownMember** y **UnknownMemberName** de la dimensión y la propiedad **NullProcessing** del atributo clave de la dimensión.  
  
 El Asistente para dimensiones y el Asistente para cubos habilitarán estas propiedades dependiendo de si el atributo clave de una dimensión admite valores NULL o si el atributo del elemento raíz de una dimensión de copo de nieve se basa en una columna que puede admitir valores NULL. En estos casos, la propiedad **NullProcessing** del atributo clave se establecerá en **UnknownMember** y la propiedad **UnknownMember** se establecerá en **Visible**.  
  
 Pero al crear dimensiones de copo de nieve incrementalmente, como se hace con la dimensión Product en este tutorial, o al definir dimensiones con el Diseñador de dimensiones y, después, incorporar estas dimensiones existentes en un cubo, es posible que tenga que establecer manualmente las propiedades **UnknownMember** y **NullProcessing** .  
  
 En las tareas de este tema, agregará los atributos de categoría de producto y subcategoría de producto en la dimensión Product de las tablas de copo de nieve que agregará a la vista del origen de datos [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW. Después habilitará la **UnknownMember** propiedad para la dimensión Product, especifique `Assembly Components` como el valor de la **UnknownMemberName** propiedad, se relacionan con el `Subcategory` y `Category`atributos al producto atributo name y, a continuación, defina el atributo clave de miembro que vincula las tablas de copo de nieve control de errores personalizado.  
  
> [!NOTE]  
>  Si ha agregado los atributos Subcategory y Category al definir originalmente el cubo del Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con el Asistente para cubos, estos pasos deberían haberse ejecutado automáticamente.  
  
## <a name="reviewing-error-handling-and-unknown-member-properties-in-the-product-dimension"></a>Revisar las propiedades de control de errores y de miembro desconocido en la dimensión Product  
  
1.  Cambie al Diseñador de dimensiones para la dimensión **Product** , haga clic en la pestaña **Estructura de dimensión** y, después, seleccione **Product** en el panel **Atributos** .  
  
     De este modo, podrá ver y modificar las propiedades de la dimensión propiamente dicha.  
  
2.  En la ventana Propiedades, revise las propiedades **UnknownMember** y **UnknownMemberName** .  
  
     Observe que la propiedad **UnknownMember** no está habilitada, porque su valor está establecido en **Ninguno** en lugar de **Visible** u **Oculto**, y que no se ha especificado ningún nombre para la propiedad **UnknownMemberName** .  
  
3.  En la ventana Propiedades, seleccione **(personalizada)** en la celda de la propiedad **ErrorConfiguration** y luego expanda la colección de propiedades **ErrorConfiguration** .  
  
     Establecer la propiedad **ErrorConfiguration** en **(personalizada)** permite ver los valores de configuración de errores predeterminados, no se cambia ningún valor.  
  
4.  Revise las propiedades de configuración de error de clave y clave NULL, pero no realice ningún cambio.  
  
     Observe que, de forma predeterminada, cuando se convierten las claves NULL en el miembro desconocido, el error de procesamiento asociado con esta conversión se omite.  
  
     En la imagen siguiente se muestran los parámetros de propiedad para la colección de propiedades **ErrorConfiguration** .  
  
     ![Colección de propiedades ErrorConfiguration](../../2014/tutorials/media/l4-productdimensionerrorconfig-1.gif "colección de propiedades ErrorConfiguration")  
  
5.  Haga clic en el **explorador** , compruebe que **Product Model Lines** está seleccionado en el **jerarquía** lista y, a continuación, expanda `All Products`.  
  
     Observe los cinco miembros del nivel Product Line.  
  
6.  Expanda **Components**y, después, expanda el miembro sin etiqueta del nivel **Model Name** .  
  
     Este nivel contiene los componentes de ensamblado que se usan al crear otros componentes, empezando por el producto **Adjustable Race** , como se muestra en la imagen siguiente.  
  
     ![Componentes del ensamblado usados para generar otros componentes](../../2014/tutorials/media/l4-productdimensionerrorconfig-2.gif "componentes del ensamblado usados para generar otros componentes")  
  
## <a name="defining-attributes-from-snowflaked-tables-and-a-product-category-user-defined-hierarchy"></a>Definir los atributos de tablas de copo de nieve y una jerarquía definida por el usuario Product Category  
  
1.  Abra el Diseñador de vistas del origen de datos para la vista del origen de datos [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW, seleccione **Reseller Sales** en el panel **Organizador de diagramas** y, después, haga clic en **Agregar o quitar objetos** en el menú **Vista del origen de datos** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
     Se abre el cuadro de diálogo **Agregar o quitar tablas** .  
  
2.  En la lista **Objetos incluidos** seleccione **DimProduct (dbo)** y, después, haga clic en **Agregar tablas relacionadas**.  
  
     Se agregarán tanto **DimProductSubcategory (dbo)** como **FactProductInventory (dbo)** . Quite **FactProductInventory (dbo)** de modo que solo se agregue la tabla **DimProductSubcategory (dbo)** a la lista **Objetos incluidos** .  
  
3.  Con la tabla **DimProductSubcategory (dbo)** seleccionada de forma predeterminada como tabla que se agrega con más frecuencia, haga clic de nuevo en **Agregar tablas relacionadas** .  
  
     La tabla **DimProductCategory (dbo)** se agrega a la lista **Objetos incluidos** .  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el menú **Formato** de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], seleccione **Diseño automático**y haga clic en **Diagrama**.  
  
     Observe que la tabla **DimProductSubcategory (dbo)** y la tabla **DimProductCategory (dbo)** están vinculadas entre sí y también a la tabla **ResellerSales** a través de la tabla **Product** .  
  
6.  Cambie al Diseñador de dimensiones para la dimensión **Product** y haga clic en la pestaña **Estructura de dimensión** .  
  
7.  Haga clic con el botón derecho en el panel **Vista del origen de datos** y luego haga clic en **Mostrar todas las tablas**.  
  
8.  En el panel **Vista del origen de datos** , busque la tabla **DimProductCategory** , haga clic con el botón derecho en **ProductCategoryKey** en dicha tabla y, luego, haga clic en **Nuevo atributo de columna**.  
  
9. En el **atributos** panel, cambie el nombre de este nuevo atributo por `Category`.  
  
10. En la ventana Propiedades, haga clic en el **NameColumn** propiedad de campo y, a continuación, haga clic en el (**...** ) para abrir el **nombre de columna** cuadro de diálogo.  
  
11. Seleccione **EnglishProductCategoryName** en la lista **Columna de origen** y haga clic en **Aceptar**.  
  
12. En el panel **Vista del origen de datos** , busque la tabla **DimProductSubcategory** , haga clic con el botón derecho en **ProductSubcategoryKey** en dicha tabla y, luego, haga clic en **Nuevo atributo de columna**.  
  
13. En el **atributos** panel, cambie el nombre de este nuevo atributo por `Subcategory`.  
  
14. En la ventana Propiedades, haga clic en el **NameColumn** propiedad de campo y, a continuación, haga clic en el **(...)**  botón para abrir el **nombre de columna** cuadro de diálogo.  
  
15. Seleccione **EnglishProductSubcategoryName** en la lista **Columna de origen** y haga clic en **Aceptar**.  
  
16. Crear una nueva jerarquía definida por el usuario denominada **categorías de producto** con los niveles siguientes, en orden de arriba a abajo: `Category`, `Subcategory`, y **Product Name**.  
  
17. Especificar `All Products` como el valor de la **AllMemberName** propiedad de la jerarquía de categorías de producto definido por el usuario.  
  
## <a name="browsing-the-user-defined-hierarchies-in-the-product-dimension"></a>Examinar las jerarquías definidas por el usuario en la dimensión Product  
  
1.  En la barra de herramientas de la pestaña **Estructura de dimensión** del **Diseñador de dimensiones** para la dimensión **Product** , haga clic en **Procesar**.  
  
2.  Haga clic en **Sí** para crear e implementar el proyecto y, después, haga clic en **Ejecutar** para procesar la dimensión **Product** .  
  
3.  Cuando el proceso se haya ejecutado correctamente, expanda **Procesamiento de dimensión 'Product' finalizó correctamente** en el cuadro de diálogo **Progreso del proceso** , expanda **Procesamiento de atributo de dimensión 'Product Name' finalizó correctamente**y, después expanda **Consultas SQL 1**.  
  
4.  Haga clic en la consulta SELECT DISTINCT y, después, en **Ver detalles**.  
  
     Observe que se ha agregado una cláusula WHERE a la cláusula SELECT DISTINCT que elimina los productos que no tienen ningún valor en la columna ProductSubcategoryKey, como se muestra en la imagen siguiente.  
  
     ![Cláusula SELECT DISTINCT que muestra la cláusula WHERE](../../2014/tutorials/media/l4-productnametraceline-1.gif "cláusula SELECT DISTINCT que muestra la cláusula WHERE")  
  
5.  Haga clic en **Cerrar** tres veces para cerrar todos los cuadros de diálogo de procesamiento.  
  
6.  Haga clic en la pestaña **Explorador** en el Diseñador de dimensiones para la dimensión **Product** y, después, haga clic en **Volver a conectar**.  
  
7.  Compruebe que **Product Model Lines** aparece en el **jerarquía** lista, expanda `All Products`y, a continuación, expanda **componentes**.  
  
8.  Seleccione **categorías de producto** en el **jerarquía** lista, expanda `All Products`y, a continuación, expanda **componentes**.  
  
     Observe que no aparece ningún componente de ensamblado.  
  
 Para modificar el comportamiento que se mencionan en la tarea anterior, habilitará la **UnknownMember** propiedad de la dimensión Products, establezca un valor para el **UnknownMemberName** establecer la propiedad, el  **NullProcessing** propiedad para el `Subcategory` y **Model Name** atributos a **UnknownMember**, definir el `Category` atributo como un atributo relacionado de el `Subcategory` atributo y, a continuación, defina el **Product Line** atributo como atributo relacionado de la **Model Name** atributo. Estos pasos harán que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use el valor de nombre de miembro desconocido para cada producto que no tenga ningún valor para la columna **SubcategoryKey** , como verá en la tarea siguiente.  
  
## <a name="enabling-the-unknown-member-defining-attribute-relationships-and-specifying-custom-processing-properties-for-nulls"></a>Habilitar el miembro desconocido, definir las relaciones de atributo y especificar propiedades de procesamiento personalizadas para valores NULL  
  
1.  Haga clic en la pestaña **Estructura de dimensión** del Diseñador de dimensiones para la dimensión **Product** y, después, seleccione **Product** en el panel **Atributos** .  
  
2.  En el **propiedades** ventana, cambie el **UnknownMember** propiedad **Visible**y, a continuación, cambie el valor de la **UnknownMemberName**propiedad `Assembly Components`.  
  
     Al cambiar la propiedad **UnknownMember** por **Visible** u **Oculto** se habilita la propiedad **UnknownMember** para la dimensión.  
  
3.  Haga clic en la pestaña **Relación de atributo** .  
  
4.  En el diagrama, haga clic en el `Subcategory` atributo y, a continuación, seleccione **nueva relación de atributo**.  
  
5.  En el **Crear relación de atributo** cuadro de diálogo, el **atributo de origen** es `Subcategory`. Establecer el **atributo relacionado** a `Category`. Deje establecido el tipo de relación en **Flexible**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  En el panel **Atributos** , seleccione **Subcategory.**  
  
8.  En la ventana Propiedades, expanda la propiedad **KeyColumns** y, después, expanda la propiedad **DimProductSubcategory.ProductSubcategoryKey (Integer)** .  
  
9. Cambie la propiedad **NullProcessing** por **UnknownMember**.  
  
10. En el panel **Atributos** , seleccione **Model Name**.  
  
11. En la ventana Propiedades, expanda la propiedad **KeyColumns** y, después, expanda la propiedad **Product.ModelName (WChar)** .  
  
12. Cambie la propiedad **NullProcessing** por **UnknownMember**.  
  
     Debido a estos cambios, cuando [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encuentra un valor null para el `Subcategory` atributo o la **Model Name** atributo durante el procesamiento, el valor del miembro desconocido se sustituirá como el valor de clave y el jerarquías definidas por el usuario se generarán correctamente.  
  
## <a name="browsing-the-product-dimension-again"></a>Examinar de nuevo la dimensión Product  
  
1.  En el menú **Compilar** , haga clic en **Tutorial de Implementar Analysis Services**.  
  
2.  Cuando la implementación haya finalizado correctamente, haga clic en la pestaña **Explorador** del Diseñador de dimensiones para la dimensión **Product** y luego haga clic en **Reconnect**.  
  
3.  Compruebe que **categorías de producto** está seleccionado en el **jerarquía** lista y, a continuación, expanda `All Products`.  
  
     Observe que aparece Assembly Components como nuevo miembro del nivel Category.  
  
4.  Expanda el `Assembly Components` miembro de la `Category` nivel y, a continuación, expanda el `Assembly Components` miembro de la `Subcategory` nivel.  
  
     Observe que todos los componentes de ensamblado ahora aparecen en el nivel **Product Name** , como se muestra en la ilustración siguiente.  
  
     ![Nivel Product Name, que muestra los componentes de ensamblado](../../2014/tutorials/media/l4-assemblycomponents-1.gif "nivel Product Name que muestra los componentes de ensamblado")  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 5: Definir relaciones entre dimensiones y grupos de medida](../analysis-services/lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)  
  
  
