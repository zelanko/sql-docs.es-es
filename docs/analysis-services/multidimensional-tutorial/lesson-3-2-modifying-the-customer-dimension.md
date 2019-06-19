---
title: Modificar la dimensión Customer | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bbe4fbfc2cad2df41a1d9bd14fcb2620e2dec5c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403647"
---
# <a name="lesson-3-2---modifying-the-customer-dimension"></a>Lección 3-2: modificar la dimensión Customer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Existen varios métodos para hacer que las dimensiones de un cubo sean más fáciles de usar y tengan más funciones. En las tareas de este tema, debe modificar la dimensión Customer.  
  
## <a name="renaming-attributes"></a>Cambiar el nombre de los atributos  
Use la pestaña **Estructura de dimensión** del Diseñador de dimensiones para cambiar los nombres de los atributos.  
  
#### <a name="to-rename-an-attribute"></a>Para cambiar el nombre de un atributo  
  
1.  Cambie al **Diseñador de dimensiones** para la dimensión Customer en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en la dimensión **Customer** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  En el panel **Atributos** , haga clic con el botón derecho en **English Country Region Name**y haga clic en **Cambiar nombre**. Cambie el nombre del atributo por **Country-Region**.  
  
3.  Cambie los nombres de los atributos siguientes del mismo modo:  
  
    -   **English Education** atributos: cambiar a **educación**  
  
    -   **English Occupation** atributos: cambiar a **ocupación**  
  
    -   **State Province Name** atributos: cambiar a **State-Province**  
  
4.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="creating-a-hierarchy"></a>Creación de una jerarquía  
Puede crear una nueva jerarquía si arrastra un atributo desde el panel **Atributos** hasta el panel **Jerarquías** .  
  
#### <a name="to-create-a-hierarchy"></a>Para crear una jerarquía  
  
1.  Arrastre el atributo **Country-Region** desde el panel **Atributos** al panel **Jerarquías** .  
  
2.  Arrastre el atributo **State-Province** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **Country-Region** .  
  
3.  Arrastre el atributo **City** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **State-Province** .  
  
4.  En el panel **Jerarquías** de la pestaña **Estructura de dimensión** , haga clic con el botón derecho en la barra de título de la jerarquía **Jerarquía** , seleccione **Cambiar nombre**y escriba **Customer Geography**.  
  
    El nombre de esta jerarquía es ahora **Customer Geography**.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="adding-a-named-calculation"></a>Agregar un cálculo con nombre  
Puede agregar un cálculo con nombre, que es una expresión SQL representada como columna calculada en una tabla de la vista del origen de datos. Aparece la expresión y se comporta como columna en la tabla. Los cálculos con nombre permiten ampliar el esquema relacional de las tablas existentes de la vista del origen de datos sin modificar la tabla en el origen de datos subyacente. Para obtener más información, consulte [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>Para agregar un cálculo con nombre  
  
1.  Abra la vista del origen de datos **[!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW 2012** haciendo doble clic en ella en la carpeta **Vistas de origen de datos** del Explorador de soluciones.  
  
2.  En el panel **Tablas** , haga clic con el botón derecho en **Customer**y, después, haga clic en **Nuevo cálculo con nombre**.  
  
3.  En el cuadro de diálogo **Crear cálculo con nombre** , escriba **FullName** en el cuadro **Nombre de columna** y, después, escriba o copie y pegue la siguiente instrucción **CASE** en el cuadro **Expresión** :  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
    La instrucción **CASE** concatena las columnas **FirstName**, **MiddleName**y **LastName** en una única columna que se usará en la dimensión Customer como nombre mostrado para el atributo **Customer** .  
  
4.  Haga clic en **Aceptar**y expanda **Customer** en el panel **Tablas** .  
  
    Aparece el cálculo con nombre **FullName** en la lista de columnas de la tabla Customer, con un icono que indica que se trata de un cálculo con nombre.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
6.  En el panel **Tablas** , haga clic con el botón derecho en **Customer**y haga clic en **Explorar datos**.  
  
7.  Revise la última columna de la vista **Explorar la tabla Customer** .  
  
    Observe que la columna **FullName** aparece en la vista del origen de datos, concatenando correctamente los datos de varias columnas del origen de datos subyacente sin modificar el origen de datos original.  
  
8.  Cierre la pestaña **Explorar la tabla Customer** .  
  
## <a name="using-the-named-calculation-for-member-names"></a>Usar el cálculo con nombre para los nombres de miembro  
Una vez que ha creado un cálculo con nombre en la vista del origen de datos, puede usar ese cálculo como propiedad de un atributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Para utilizar el cálculo con nombre para los nombres de miembro  
  
1.  Pase al Diseñador de dimensiones para la dimensión Customer.  
  
2.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , haga clic en el atributo **Customer Key** .  
  
3.  Abra la ventana Propiedades y haga clic en el botón **Ocultar automáticamente** de la barra de título para que permanezca abierta.  
  
4.  En el campo de la propiedad **Name** , escriba **Full Name**.  
  
5.  Haga clic en el **NameColumn** propiedad de campo en la parte inferior y, a continuación, haga clic en el ( **...** ) para abrir el **nombre de columna** cuadro de diálogo.  
  
6.  Seleccione **FullName** al final de la lista **Columna de origen** y haga clic en **Aceptar**.  
  
7.  En la pestaña Estructura de dimensiones, arrastre el atributo **Full Name** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **City** .  
  
8.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-display-folders"></a>Definir carpetas para mostrar  
Puede utilizar carpetas para mostrar para agrupar jerarquías de usuario y de atributo en estructuras de carpeta con el fin de facilitar el uso de dichas estructuras.  
  
#### <a name="to-define-display-folders"></a>Para definir carpetas para mostrar  
  
1.  Abra la pestaña **Estructura de dimensión** para la dimensión Customer.  
  
2.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **City**  
  
    -   **Country-Region**  
  
    -   **Código postal**  
  
    -   **State-Province**  
  
3.  En la ventana Propiedades, haga clic en el campo de la propiedad **AttributeHierarchyDisplayFolder** situado en la parte superior (es posible que tenga que seleccionarlo para ver el nombre completo) y, después, escriba **Location**.  
  
4.  En el panel **Jerarquías** , haga clic en **Customer Geography**y, en la ventana Propiedades de la derecha, seleccione **Location** como valor de la propiedad **DisplayFolder** .  
  
5.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Commute Distance**  
  
    -   **Education**  
  
    -   **Gender**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   **Occupation**  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  En la ventana Propiedades, haga clic en el campo de la propiedad **AttributeHierarchyDisplayFolder** situado en la parte superior y escriba **Demographic**.  
  
7.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Email Address**  
  
    -   **Teléfono**  
  
8.  En la ventana Propiedades, haga clic en el campo de la propiedad **AttributeHierarchyDisplayFolder** situado en la parte superior y escriba **Contacts**.  
  
9. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-composite-keycolumns"></a>Definir KeyColumns compuestas  
La propiedad **KeyColumns** contiene la columna o columnas que representan la clave para el atributo. En esta lección, debe crear una clave compuesta para los atributos **City** y **State-Province** . Las claves compuestas pueden resultar de utilidad cuando necesite identificar un atributo de forma inequívoca. Por ejemplo, cuando defina relaciones de atributo más adelante en este tutorial, un atributo **City** deberá identificar de forma exclusiva un atributo **State-Province** . Sin embargo, podrían existir varias ciudades con el mismo nombre en estados diferentes. Por este motivo, deberá crear una clave compuesta formada por las columnas **StateProvinceName** y **City** para el atributo **City** . Para más información, vea [Modificar la propiedad KeyColumns de un atributo](../multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>Para definir KeyColumns compuestas para el atributo City  
  
1.  Abra la pestaña **Estructura de dimensión** para la dimensión Customer.  
  
2.  En el panel **Atributos** , haga clic en el atributo **City** .  
  
3.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** junto a la parte final y, después, haga clic en el botón Examinar ( **...** ).  
  
4.  En el cuadro de diálogo **Columnas de clave** , en la lista **Columnas disponibles** , seleccione la columna **StateProvinceName**y, después, haga clic en el botón **>** .  
  
    Las columnas **City** y **StateProvinceName** se muestran ahora en la lista **Columnas de clave** .  
  
5.  Haga clic en **Aceptar**.  
  
6.  Para establecer la propiedad **NameColumn** del atributo **City** , haga clic en el campo **NameColumn** en la ventana Propiedades y, después, haga clic en el botón Examinar ( **...** ).  
  
7.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **City**y, después, haga clic en **Aceptar**.  
  
8.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>Para definir KeyColumns compuestas para el atributo State-Province  
  
1.  Asegúrese de que la pestaña **Estructura de dimensión** para la dimensión Customer está abierta.  
  
2.  En el panel **Atributos** , haga clic en el atributo **State-Province** .  
  
3.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** y, después, haga clic en el botón Examinar ( **...** ).  
  
4.  En el cuadro de diálogo **Columnas de clave** , en la lista **Columnas disponibles** , seleccione la columna **EnglishCountryRegionName**y, después, haga clic en el botón **>** .  
  
    Las columnas **EnglishCountryRegionName** y **StateProvinceName** se muestran ahora en la lista **Columnas de clave** .  
  
5.  Haga clic en **Aceptar**.  
  
6.  Para establecer la propiedad **NameColumn** del atributo **State-Province** , haga clic en el campo **NameColumn** en la ventana Propiedades y, después, haga clic en el botón Examinar ( **...** ).  
  
7.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **StateProvinceName**y, después, haga clic en **Aceptar**.  
  
8.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-attribute-relationships"></a>Definición de relaciones de atributo  
Si los datos subyacentes lo permiten, debería definir relaciones de atributo entre atributos. La definición de relaciones de atributo acelera el procesamiento de las dimensiones, las particiones y las consultas. Para obtener más información, consulte [Definir relaciones de atributo](../multidimensional-models/attribute-relationships-define.md) y [Relaciones de atributo](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relaciones de atributo  
  
1.  En el **Diseñador de dimensiones** para la dimensión Customer, haga clic en la pestaña **Relaciones de atributo** . Es posible que tenga que esperar.  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **City** y haga clic en **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **City**. Establezca el **Atributo relacionado** en **State-Province**.  
  
4.  En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
    El tipo de relación es **Rígida** porque las relaciones entre los miembros no cambiarán con el tiempo. Por ejemplo, es poco habitual que una ciudad pase a formar parte de otro estado o provincia.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  En el diagrama, haga clic con el botón derecho en el atributo **State-Province** y seleccione **Nueva relación de atributo**.  
  
7.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **State-Province**. Establezca el **Atributo relacionado** en **Country-Region**.  
  
8.  En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
9. Haga clic en **Aceptar**.  
  
10. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>Implementar cambios, procesar los objetos y ver los cambios  
Una vez que ha cambiado los atributos y las jerarquías, debe implementar los cambios y procesar de nuevo los objetos relacionados antes de ver los cambios.  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>Para implementar los cambios, procesar los objetos y ver los cambios  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Después de que aparezca el mensaje **La implementación finalizó correctamente** , haga clic en la pestaña **Explorador** del Diseñador de dimensiones para la dimensión Customer y, después, haga clic en el botón Volver a conectar en el lado izquierdo de la barra de herramientas del diseñador.  
  
3.  Compruebe que **Customer Geography** aparece seleccionado en la lista **Jerarquía** y, después, en el panel del explorador, expanda **All**, **Australia**, **New South Wales**y, por último, **Coffs Harbour**.  
  
    El explorador muestra los clientes de la ciudad.  
  
4.  Cambie al **Diseñador de cubos** para el cubo Tutorial de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para ello, haga doble clic en el cubo **Tutorial de Analysis Services** en el nodo **Cubos** del **Explorador de soluciones**.  
  
5.  Haga clic en la pestaña **Explorador** y haga clic en el botón Volver a conectar en la barra de herramientas del diseñador.  
  
6.  En el panel **Grupo de medida** , expanda **Customer**.  
  
    Observe que, en lugar de una lista larga de atributos, debajo de Customer solamente aparecen las carpetas para mostrar y los atributos que no tienen valores de carpeta para mostrar.  
  
7.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Modificar la dimensión Product](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>Vea también  
[Referencia de las propiedades de los atributos de dimensión](../multidimensional-models/dimension-attribute-properties-reference.md)  
[Quitar un atributo de una dimensión](../multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)  
[Cambiar el nombre de un atributo](../multidimensional-models/attribute-properties-rename-an-attribute.md)  
[Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
