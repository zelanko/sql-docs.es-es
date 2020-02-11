---
title: Modificar la dimensión Product | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff912ed43048e00f0ed77989a46b3b7d0b111cff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078839"
---
# <a name="modifying-the-product-dimension"></a>Modificar la dimensión Product
  En las tareas de este tema, usará un cálculo con nombre para proporcionar nombres más descriptivos a las líneas de producto, definir una jerarquía en la dimensión Product y especificar el nombre de miembro (Todos) para dicha jerarquía. También agrupará los atributos en carpetas para mostrar.  
  
## <a name="adding-a-named-calculation"></a>Agregar un cálculo con nombre  
 Puede agregar un cálculo con nombre a una tabla de una vista del origen de datos. En la tarea siguiente, creará un cálculo con nombre que mostrará el nombre completo de la línea de producto.  
  
#### <a name="to-add-a-named-calculation"></a>Para agregar un cálculo con nombre  
  
1.  Para abrir la vista del origen de datos **Adventure Works DW 2012** , haga doble clic en **Adventure Works DW 2012** en la carpeta **Vistas del origen de datos** del Explorador de soluciones.  
  
2.  Al final de panel de diagrama, haga clic con el botón derecho en el encabezado de tabla **Product** y, después, haga clic en **Nuevo cálculo con nombre**.  
  
3.  En el cuadro de diálogo **crear cálculo con nombre** , escriba `ProductLineName` en el cuadro **nombre de columna** .  
  
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
  
5.  Haga clic en **Aceptar** para `ProductLineName` crear el cálculo con nombre. Es posible que tenga que esperar.  
  
6.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>Modificar la propiedad NameColumn de un atributo  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>Para modificar el valor de la propiedad NameColumn de un atributo  
  
1.  Cambie a la dimensión Product en el Diseñador de dimensiones. Para ello, haga doble clic en la dimensión **Product** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , seleccione **Product Line**.  
  
3.  En el ventana Propiedades en el lado derecho de la pantalla, haga clic en el campo de la propiedad **NameColumn** situado en la parte inferior de la ventana y, a continuación, haga clic en el botón Examinar (**...**) para abrir el cuadro de diálogo **columna de nombre** . (Es posible que tenga que hacer clic en la pestaña **Propiedades** a la derecha de la pantalla para abrir la ventana Propiedades).  
  
4.  Seleccione `ProductLineName` en la parte inferior de la lista **columna de origen** y, a continuación, haga clic en **Aceptar**.  
  
     El campo NameColumn contiene ahora el texto **Product.ProductLineName (WChar)**. Los miembros de la jerarquía de atributo **Product Line** mostrarán el nombre completo de la línea de producto en lugar de un nombre abreviado de la misma.  
  
5.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , seleccione **Product Key**.  
  
6.  En el ventana Propiedades, haga clic en el campo de la propiedad **NameColumn** y, a continuación, haga clic en el botón de puntos suspensivos (**...**) para abrir el cuadro de diálogo **columna de nombre** .  
  
7.  Seleccione **EnglishProductName** en la lista **Columna de origen** y, después, haga clic en **Aceptar**.  
  
     El campo NameColumn contiene ahora el texto **Product.EnglishProductName (WChar)**.  
  
8.  En el ventana Propiedades, desplácese hacia arriba, **** haga clic en el campo de la `Product Name`propiedad nombre y, a continuación, escriba.  
  
## <a name="creating-a-hierarchy"></a>Creación de una jerarquía  
  
#### <a name="to-create-a-hierarchy"></a>Para crear una jerarquía  
  
1.  Arrastre el atributo **Product Line** del panel **Atributos** al panel **Jerarquías** .  
  
2.  Arrastre el atributo **Model Name** desde el panel **atributos** a la ** \<celda nuevo nivel>** del panel **jerarquías** , debajo del nivel **Product line** .  
  
3.  Arrastre el `Product Name` atributo desde el panel **atributos** a la ** \<celda nuevo nivel>** del panel **jerarquías** , debajo del nivel **nombre del modelo** . (Cambió el nombre Product Key a Nombre del producto en la sección anterior).  
  
4.  En el panel **jerarquías** de la pestaña **estructura de dimensión** , haga clic con el botón secundario en la barra de título de la jerarquía jerarquía, haga clic en **cambiar nombre**y, a continuación, escriba `Product Model Lines`. ****  
  
     El nombre de la jerarquía es ahora `Product Model Lines`.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="specifying-folder-names-and-all-member-names"></a>Especificar los nombres de carpeta y el nombre de todos los miembros  
  
#### <a name="to-specify-the-folder-and-member-names"></a>Para especificar los nombres de carpeta y de los miembros  
  
1.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Clase**  
  
    -   **Color**  
  
    -   **Días de fabricación**  
  
    -   **Reordenar punto**  
  
    -   **Nivel de seguridad de existencias**  
  
    -   **Tamaño**  
  
    -   **Intervalo de tamaño**  
  
    -   **Estilo**  
  
    -   **Media**  
  
2.  En el campo de la propiedad **AttributeHierarchyDisplayFolder** en el ventana propiedades `Stocking`, escriba.  
  
     Ahora ha agrupado estos atributos en una única carpeta para mostrar.  
  
3.  En el panel **Atributos** , seleccione los atributos siguientes:  
  
    -   **Precio del distribuidor**  
  
    -   **Precio de lista**  
  
    -   **Costo estándar**  
  
4.  En la celda de la propiedad **AttributeHierarchyDisplayFolder** del ventana Propiedades, `Financial`escriba.  
  
     Ahora ha agrupado estos atributos en una segunda carpeta para mostrar.  
  
5.  En el panel **Atributos** , seleccione los atributos siguientes:  
  
    -   **Fecha de finalización**  
  
    -   **Fecha de inicio**  
  
    -   **Estado**  
  
6.  En la celda de la propiedad **AttributeHierarchyDisplayFolder** del ventana Propiedades, `History`escriba.  
  
     Ahora ha agrupado estos atributos en una tercera carpeta para mostrar.  
  
7.  Seleccione la `Product Model Lines` jerarquía en el panel **jerarquías** y, a continuación, cambie la propiedad **AllMemberName** de la `All Products`ventana Propiedades a.  
  
8.  Haga clic en un área abierta del panel **jerarquías** y, a continuación, cambie la propiedad **AttributeAllMemberName** en la parte superior `All Products`de la ventana Propiedades a.  
  
     Hacer clic en un área abierta permite modificar las propiedades de la dimensión Product propiamente dicha. También puede hacer clic en **Product** en la parte superior de la lista de atributos del panel **Atributos** .  
  
9. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-attribute-relationships"></a>Definición de relaciones de atributo  
 Si los datos subyacentes lo permiten, debería definir relaciones de atributo entre atributos. La definición de relaciones de atributo acelera el procesamiento de las dimensiones, las particiones y las consultas. Para obtener más información, consulte [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md) y [Relaciones de atributo](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relaciones de atributo  
  
1.  En el **Diseñador de dimensiones** , para la dimensión Product, haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **Model Name** y haga clic en **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Model Name**. Establezca el **Atributo relacionado** en **Product Line**.  
  
     En la lista **Tipo de relación** , deje establecido el tipo de relación en **Flexible** , ya que las relaciones entre los miembros pueden cambiar con el tiempo. Por ejemplo, un modelo de producto podría moverse a otra línea de producto.  
  
4.  Haga clic en **OK**.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="reviewing-product-dimension-changes"></a>Revisar los cambios de la dimensión Product  
  
#### <a name="to-review-the-product-dimension-changes"></a>Para revisar los cambios de la dimensión Product  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Después de que aparezca el mensaje **La implementación finalizó correctamente** , haga clic en la pestaña **Explorador** del **Diseñador de dimensiones** para la dimensión **Product** y, luego, haga clic en el botón Volver a conectar de la barra de herramientas del diseñador.  
  
3.  Compruebe que `Product Model Lines` está seleccionado en la lista **jerarquía** y, a continuación `All Products`, expanda.  
  
     Observe que el nombre del miembro **todos** aparece como `All Products`. Esto se debe a que ha cambiado la propiedad **AllMemberName** de la `All Products` jerarquía a anteriormente en la lección. Además, los miembros del nivel **Product Line** ahora tienen nombres descriptivos, en lugar de abreviaturas de una sola letra.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar la dimensión Date](lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>Consulte también  
 [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [Crear jerarquías definidas por el usuario](multidimensional-models/user-defined-hierarchies-create.md)   
 [Configurar el nivel de&#41; &#40;para las jerarquías de atributo](multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
