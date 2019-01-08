---
title: Modificar la dimensión Product | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 430ac56191fcfc2c601c50f9f31de128d5d58368
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523327"
---
# <a name="modifying-the-product-dimension"></a>Modificar la dimensión Product
  En las tareas de este tema, usará un cálculo con nombre para proporcionar nombres más descriptivos a las líneas de producto, definir una jerarquía en la dimensión Product y especificar el nombre de miembro (Todos) para dicha jerarquía. También agrupará los atributos en carpetas para mostrar.  
  
## <a name="adding-a-named-calculation"></a>Agregar un cálculo con nombre  
 Puede agregar un cálculo con nombre a una tabla de una vista del origen de datos. En la tarea siguiente, creará un cálculo con nombre que mostrará el nombre completo de la línea de producto.  
  
#### <a name="to-add-a-named-calculation"></a>Para agregar un cálculo con nombre  
  
1.  Para abrir la vista del origen de datos **Adventure Works DW 2012** , haga doble clic en **Adventure Works DW 2012** en la carpeta **Vistas del origen de datos** del Explorador de soluciones.  
  
2.  Al final de panel de diagrama, haga clic con el botón derecho en el encabezado de tabla **Product** y, después, haga clic en **Nuevo cálculo con nombre**.  
  
3.  En el **crear cálculo con nombre** cuadro de diálogo, escriba `ProductLineName` en el **nombre de columna** cuadro.  
  
4.  En el cuadro **Expresión** , escriba o copie y pegue la siguiente instrucción **CASE** :  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
     Esta instrucción **CASE** crea nombres descriptivos para cada línea de producto del cubo.  
  
5.  Haga clic en **Aceptar** para crear el `ProductLineName` cálculo con nombre. Es posible que tenga que esperar.  
  
6.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>Modificar la propiedad NameColumn de un atributo  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>Para modificar el valor de la propiedad NameColumn de un atributo  
  
1.  Cambie a la dimensión Product en el Diseñador de dimensiones. Para ello, haga doble clic en la dimensión **Product** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , seleccione **Product Line**.  
  
3.  En la ventana Propiedades en el lado derecho de la pantalla, haga clic en el **NameColumn** propiedad de campo en la parte inferior de la ventana y, a continuación, haga clic en el (**...** ) para abrir el **nombre de columna** cuadro de diálogo. (Es posible que tenga que hacer clic en la pestaña **Propiedades** a la derecha de la pantalla para abrir la ventana Propiedades).  
  
4.  Seleccione `ProductLineName` en la parte inferior de la **columna de origen** lista y, a continuación, haga clic en **Aceptar**.  
  
     El campo NameColumn contiene ahora el texto **Product.ProductLineName (WChar)**. Los miembros de la jerarquía de atributo **Product Line** mostrarán el nombre completo de la línea de producto en lugar de un nombre abreviado de la misma.  
  
5.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , seleccione **Product Key**.  
  
6.  En la ventana Propiedades, haga clic en el **NameColumn** propiedad de campo y, a continuación, haga clic en el botón de puntos suspensivos (**...** ) para abrir el **nombre de columna** cuadro de diálogo.  
  
7.  Seleccione **EnglishProductName** en la lista **Columna de origen** y, después, haga clic en **Aceptar**.  
  
     El campo NameColumn contiene ahora el texto **Product.EnglishProductName (WChar)**.  
  
8.  En la ventana Propiedades, desplácese hacia arriba, haga clic en el **nombre** campo de propiedad y, a continuación, escriba `Product Name`.  
  
## <a name="creating-a-hierarchy"></a>Creación de una jerarquía  
  
#### <a name="to-create-a-hierarchy"></a>Para crear una jerarquía  
  
1.  Arrastre el atributo **Product Line** del panel **Atributos** al panel **Jerarquías** .  
  
2.  Arrastre el **Model Name** de atributo de la **atributos** panel en el  **\<nuevo nivel >** de celda en el **jerarquías** panel, debajo del **Product Line** nivel.  
  
3.  Arrastre el `Product Name` de atributo de la **atributos** panel en el  **\<nuevo nivel >** de celda en la **jerarquías** panel debajo el  **Nombre del modelo** nivel. (Cambió el nombre Product Key a Nombre del producto en la sección anterior).  
  
4.  En el **jerarquías** panel de la **estructura de dimensión** pestaña, haga clic en la barra de título de la **jerarquía** jerarquía, haga clic en **cambiar el nombre de** y, a continuación, escriba `Product Model Lines`.  
  
     El nombre de la jerarquía es ahora `Product Model Lines`.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="specifying-folder-names-and-all-member-names"></a>Especificar los nombres de carpeta y el nombre de todos los miembros  
  
#### <a name="to-specify-the-folder-and-member-names"></a>Para especificar los nombres de carpeta y de los miembros  
  
1.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Clase**  
  
    -   **Color**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **Tamaño**  
  
    -   **Size Range**  
  
    -   **Estilo**  
  
    -   **Weight**  
  
2.  En el **AttributeHierarchyDisplayFolder** campo de propiedad en la ventana Propiedades, escriba `Stocking`.  
  
     Ahora ha agrupado estos atributos en una única carpeta para mostrar.  
  
3.  En el panel **Atributos** , seleccione los atributos siguientes:  
  
    -   **Dealer Price**  
  
    -   **List Price**  
  
    -   **Standard Cost**  
  
4.  En el **AttributeHierarchyDisplayFolder** celda de la propiedad en la ventana Propiedades, escriba `Financial`.  
  
     Ahora ha agrupado estos atributos en una segunda carpeta para mostrar.  
  
5.  En el panel **Atributos** , seleccione los atributos siguientes:  
  
    -   **End Date**  
  
    -   **Fecha de inicio**  
  
    -   **Estado**  
  
6.  En el **AttributeHierarchyDisplayFolder** celda de la propiedad en la ventana Propiedades, escriba `History`.  
  
     Ahora ha agrupado estos atributos en una tercera carpeta para mostrar.  
  
7.  Seleccione el `Product Model Lines` jerarquía en la **jerarquías** panel y, a continuación, cambie el **AllMemberName** propiedad en la ventana Propiedades para `All Products`.  
  
8.  Haga clic en un área abierta de la **jerarquías** panel y, a continuación, cambie el **AttributeAllMemberName** propiedad en la parte superior de la ventana Propiedades para `All Products`.  
  
     Hacer clic en un área abierta permite modificar las propiedades de la dimensión Product propiamente dicha. También puede hacer clic en **Product** en la parte superior de la lista de atributos del panel **Atributos** .  
  
9. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-attribute-relationships"></a>Definición de relaciones de atributo  
 Si los datos subyacentes lo permiten, debería definir relaciones de atributo entre atributos. La definición de relaciones de atributo acelera el procesamiento de las dimensiones, las particiones y las consultas. Para obtener más información, consulte [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md) y [Relaciones de atributo](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relaciones de atributo  
  
1.  En el **Diseñador de dimensiones** , para la dimensión Product, haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **Model Name** y haga clic en **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo**, el **Atributo de origen** es **Model Name**. Establezca el **Atributo relacionado** en **Product Line**.  
  
     En la lista **Tipo de relación** , deje establecido el tipo de relación en **Flexible** , ya que las relaciones entre los miembros pueden cambiar con el tiempo. Por ejemplo, un modelo de producto podría moverse a otra línea de producto.  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="reviewing-product-dimension-changes"></a>Revisar los cambios de la dimensión Product  
  
#### <a name="to-review-the-product-dimension-changes"></a>Para revisar los cambios de la dimensión Product  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Después de que aparezca el mensaje **La implementación finalizó correctamente** , haga clic en la pestaña **Explorador** del **Diseñador de dimensiones** para la dimensión **Product** y, luego, haga clic en el botón Volver a conectar de la barra de herramientas del diseñador.  
  
3.  Compruebe que `Product Model Lines` está seleccionado en el **jerarquía** lista y, a continuación, expanda `All Products`.  
  
     Tenga en cuenta que el nombre de la **todas** miembro aparece como `All Products`. Esto es debido a que cambió la **AllMemberName** propiedad para la jerarquía para `All Products` anteriormente en esta lección. Además, los miembros del nivel **Product Line** ahora tienen nombres descriptivos, en lugar de abreviaturas de una sola letra.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar la dimensión Date](lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>Vea también  
 [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [Crear jerarquías definidas por el usuario](multidimensional-models/user-defined-hierarchies-create.md)   
 [Configurar el nivel &#40;All&#41; para las jerarquías de atributo](multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
