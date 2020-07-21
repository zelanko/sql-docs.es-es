---
title: Modificar la dimensión Customer | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 63cfc1fc4b5bcc3e1c468bbb456a660587757f2b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543447"
---
# <a name="modifying-the-customer-dimension"></a>Modificar la dimensión Customer
  Existen varios métodos para hacer que las dimensiones de un cubo sean más fáciles de usar y tengan más funciones. En las tareas de este tema, debe modificar la dimensión Customer.  
  
## <a name="renaming-attributes"></a>Cambiar el nombre de los atributos  
 Use la pestaña **Estructura de dimensión** del Diseñador de dimensiones para cambiar los nombres de los atributos.  
  
#### <a name="to-rename-an-attribute"></a>Para cambiar el nombre de un atributo  
  
1.  Cambie al **Diseñador de dimensiones** para la dimensión Customer en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en la dimensión **Customer** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  En el panel **Atributos** , haga clic con el botón derecho en **English Country Region Name**y haga clic en **Cambiar nombre**. Cambie el nombre del atributo a `Country-Region` .  
  
3.  Cambie los nombres de los atributos siguientes del mismo modo:  
  
    -   Atributo de **educación en inglés** : cambiar a`Education`  
  
    -   Atributo de **ocupación en inglés** : cambiar a`Occupation`  
  
    -   Atributo de **nombre de provincia de estado** : cambiar a`State-Province`  
  
4.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="creating-a-hierarchy"></a>Creación de una jerarquía  
 Puede crear una nueva jerarquía si arrastra un atributo desde el panel **Atributos** hasta el panel **Jerarquías** .  
  
#### <a name="to-create-a-hierarchy"></a>Para crear una jerarquía  
  
1.  Arrastre el `Country-Region` atributo desde el panel **atributos** al panel **jerarquías** .  
  
2.  Arrastre el `State-Province` atributo desde el panel **atributos** a la **\<new level>** celda del panel **jerarquías** , debajo del `Country-Region` nivel.  
  
3.  Arrastre el atributo **City** desde el panel **atributos** a la **\<new level>** celda del panel **jerarquías** , debajo del `State-Province` nivel.  
  
4.  En el panel **jerarquías** de la pestaña **estructura de dimensión** , haga clic con el botón secundario en la barra de título de la jerarquía jerarquía, seleccione **cambiar nombre**y, a continuación, escriba **Hierarchy** `Customer Geography` .  
  
     El nombre de la jerarquía es ahora `Customer Geography` .  
  
5.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="adding-a-named-calculation"></a>Agregar un cálculo con nombre  
 Puede agregar un cálculo con nombre, que es una expresión SQL representada como columna calculada en una tabla de la vista del origen de datos. Aparece la expresión y se comporta como columna en la tabla. Los cálculos con nombre permiten ampliar el esquema relacional de las tablas existentes de la vista del origen de datos sin modificar la tabla en el origen de datos subyacente. Para obtener más información, vea [definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>Para agregar un cálculo con nombre  
  
1.  Abra la vista del origen de datos ** [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** haciendo doble clic en ella en la carpeta **vistas del origen de datos** en explorador de soluciones.  
  
2.  En el panel **Tablas** , haga clic con el botón derecho en **Customer**y, después, haga clic en **Nuevo cálculo con nombre**.  
  
3.  En el cuadro de diálogo **crear cálculo con nombre** , escriba `FullName` en el cuadro **nombre de columna** y, a continuación, escriba o copie y pegue la siguiente `CASE` instrucción en el cuadro **expresión** :  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
     La `CASE` instrucción concatena las columnas **FirstName**, **MiddleName**y **LastName** en una única columna que se usará en la dimensión Customer como el nombre mostrado para el atributo **Customer** .  
  
4.  Haga clic en **Aceptar**y expanda **Customer** en el panel **Tablas** .  
  
     El `FullName` cálculo con nombre aparece en la lista de columnas de la tabla Customer, con un icono que indica que se trata de un cálculo con nombre.  
  
5.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
6.  En el panel **Tablas** , haga clic con el botón derecho en **Customer**y haga clic en **Explorar datos**.  
  
7.  Revise la última columna de la vista **Explorar la tabla Customer** .  
  
     Observe que la `FullName` columna aparece en la vista del origen de datos, concatenando correctamente los datos de varias columnas del origen de datos subyacente y sin modificar el origen de datos original.  
  
8.  Cierre la pestaña **Explorar la tabla Customer** .  
  
## <a name="using-the-named-calculation-for-member-names"></a>Usar el cálculo con nombre para los nombres de miembro  
 Una vez que ha creado un cálculo con nombre en la vista del origen de datos, puede usar ese cálculo como propiedad de un atributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Para utilizar el cálculo con nombre para los nombres de miembro  
  
1.  Pase al Diseñador de dimensiones para la dimensión Customer.  
  
2.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , haga clic en el atributo **Customer Key** .  
  
3.  Abra la ventana Propiedades y haga clic en el botón **Ocultar automáticamente** de la barra de título para que permanezca abierta.  
  
4.  En el campo de la propiedad **nombre** , escriba `Full Name` .  
  
5.  Haga clic en el campo de la propiedad **NameColumn** situado en la parte inferior y, a continuación, haga clic en el botón Examinar (**...**) para abrir el cuadro de diálogo **columna de nombre** .  
  
6.  Seleccione `FullName` en la parte inferior de la lista **columna de origen** y, a continuación, haga clic en **Aceptar**.  
  
7.  En la pestaña estructura de dimensiones, arrastre el `Full Name` atributo desde el panel **atributos** a la **\<new level>** celda del panel **jerarquías** , debajo del nivel **City** .  
  
8.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="defining-display-folders"></a>Definir carpetas para mostrar  
 Puede utilizar carpetas para mostrar para agrupar jerarquías de usuario y de atributo en estructuras de carpeta con el fin de facilitar el uso de dichas estructuras.  
  
#### <a name="to-define-display-folders"></a>Para definir carpetas para mostrar  
  
1.  Abra la pestaña **Estructura de dimensión** para la dimensión Customer.  
  
2.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Ciudad**  
  
    -   `Country-Region`  
  
    -   **Código postal**  
  
    -   `State-Province`  
  
3.  En el ventana Propiedades, haga clic en el campo de la propiedad **AttributeHierarchyDisplayFolder** en la parte superior (puede que tenga que apuntar para ver el nombre completo) y, a continuación, escriba `Location` .  
  
4.  En el panel **jerarquías** , haga clic en `Customer Geography` y, en el ventana Propiedades de la derecha, seleccione `Location` como el valor de la propiedad **DisplayFolder** .  
  
5.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Commute Distance**  
  
    -   `Education`  
  
    -   **Sexo**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   `Occupation`  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  En el ventana Propiedades, haga clic en el campo de la propiedad **AttributeHierarchyDisplayFolder** en la parte superior y, a continuación, escriba `Demographic` .  
  
7.  En el panel **Atributos** , mantenga pulsada la tecla CTRL mientras hace clic en cada uno de los atributos siguientes para seleccionarlos:  
  
    -   **Dirección de correo electrónico**  
  
    -   **Teléfono**  
  
8.  En el ventana Propiedades, haga clic en el campo de la propiedad **AttributeHierarchyDisplayFolder** y escriba `Contacts` .  
  
9. En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="defining-composite-keycolumns"></a>Definir KeyColumns compuestas  
 La propiedad **KeyColumns** contiene la columna o columnas que representan la clave para el atributo. En esta lección, creará una clave compuesta para la **ciudad** y `State-Province` los atributos. Las claves compuestas pueden resultar de utilidad cuando necesite identificar un atributo de forma inequívoca. Por ejemplo, al definir las relaciones de atributo más adelante en este tutorial, un atributo **City** debe identificar de forma única un `State-Province` atributo. Sin embargo, podrían existir varias ciudades con el mismo nombre en estados diferentes. Por este motivo, deberá crear una clave compuesta formada por las columnas **StateProvinceName** y **City** para el atributo **City** . Para más información, vea [Modificar la propiedad KeyColumns de un atributo](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>Para definir KeyColumns compuestas para el atributo City  
  
1.  Abra la pestaña **Estructura de dimensión** para la dimensión Customer.  
  
2.  En el panel **Atributos** , haga clic en el atributo **City** .  
  
3.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** junto a la parte final y, después, haga clic en el botón Examinar (**...**).  
  
4.  En el cuadro de diálogo **Columnas de clave** , en la lista **Columnas disponibles** , seleccione la columna **StateProvinceName**y, después, haga clic en el botón **>** .  
  
     Las columnas **City** y **StateProvinceName** se muestran ahora en la lista **Columnas de clave** .  
  
5.  Haga clic en **OK**.  
  
6.  Para establecer la propiedad **NameColumn** del atributo **City** , haga clic en el campo **NameColumn** en la ventana Propiedades y, después, haga clic en el botón Examinar (**...**).  
  
7.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **City**y, después, haga clic en **Aceptar**.  
  
8.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>Para definir KeyColumns compuestas para el atributo State-Province  
  
1.  Asegúrese de que la pestaña **Estructura de dimensión** para la dimensión Customer está abierta.  
  
2.  En el panel **atributos** , haga clic en el `State-Province` atributo.  
  
3.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** y, después, haga clic en el botón Examinar (**...**).  
  
4.  En el cuadro de diálogo **Columnas de clave** , en la lista **Columnas disponibles** , seleccione la columna **EnglishCountryRegionName**y, después, haga clic en el botón **>** .  
  
     Las columnas **EnglishCountryRegionName** y **StateProvinceName** se muestran ahora en la lista **Columnas de clave** .  
  
5.  Haga clic en **OK**.  
  
6.  Para establecer la propiedad **NameColumn** del `State-Province` atributo, haga clic en el campo **NameColumn** en el ventana Propiedades y, a continuación, haga clic en el botón Examinar (**...**).  
  
7.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **StateProvinceName**y, después, haga clic en **Aceptar**.  
  
8.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="defining-attribute-relationships"></a>Definición de relaciones de atributo  
 Si los datos subyacentes lo permiten, debería definir relaciones de atributo entre atributos. La definición de relaciones de atributo acelera el procesamiento de las dimensiones, las particiones y las consultas. Para obtener más información, consulte [Definir relaciones de atributo](multidimensional-models/attribute-relationships-define.md) y [Relaciones de atributo](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relaciones de atributo  
  
1.  En el **Diseñador de dimensiones** para la dimensión Customer, haga clic en la pestaña **relaciones de atributo** . Es posible que tenga que esperar.  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **City** y haga clic en **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **City**. Establezca el **atributo relacionado** en `State-Province` .  
  
4.  En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
     El tipo de relación es **Rígida** porque las relaciones entre los miembros no cambiarán con el tiempo. Por ejemplo, es poco habitual que una ciudad pase a formar parte de otro estado o provincia.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  En el diagrama, haga clic con el botón secundario en el `State-Province` atributo y seleccione **nueva relación de atributo**.  
  
7.  En el cuadro de diálogo **crear relación de atributo** , el **atributo de origen** es `State-Province` . Establezca el **atributo relacionado** en `Country-Region` .  
  
8.  En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
9. Haga clic en **OK**.  
  
10. En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>Implementar cambios, procesar los objetos y ver los cambios  
 Una vez que ha cambiado los atributos y las jerarquías, debe implementar los cambios y procesar de nuevo los objetos relacionados antes de ver los cambios.  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>Para implementar los cambios, procesar los objetos y ver los cambios  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Después de que aparezca el mensaje **La implementación finalizó correctamente** , haga clic en la pestaña **Explorador** del Diseñador de dimensiones para la dimensión Customer y, después, haga clic en el botón Volver a conectar en el lado izquierdo de la barra de herramientas del diseñador.  
  
3.  Compruebe que `Customer Geography` está seleccionado en la lista **jerarquía** y, a continuación, en el panel explorador, expanda **todo**, **Australia**, **Nueva Gales del sur**y, a continuación, expanda **Coffs**.  
  
     El explorador muestra los clientes de la ciudad.  
  
4.  Cambie al **Diseñador de cubos** para el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para ello, haga doble clic en el cubo **Tutorial de Analysis Services** en el nodo **Cubos** del **Explorador de soluciones**.  
  
5.  Haga clic en la pestaña **Explorador** y haga clic en el botón Volver a conectar en la barra de herramientas del diseñador.  
  
6.  En el panel **Grupo de medida** , expanda **Customer**.  
  
     Observe que, en lugar de una lista larga de atributos, debajo de Customer solamente aparecen las carpetas para mostrar y los atributos que no tienen valores de carpeta para mostrar.  
  
7.  En el menú **Archivo**, haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar la dimensión Product](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de propiedades de atributo de dimensión](multidimensional-models/dimension-attribute-properties-reference.md)   
 [Quitar un atributo de una dimensión](multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)   
 [Cambiar el nombre de un atributo](multidimensional-models/attribute-properties-rename-an-attribute.md)   
 [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
