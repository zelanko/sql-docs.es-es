---
title: 'Tutorial: Creación de un informe de forma libre (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aaa5729c47c66e40b62cddc6bfcef1ba2ec84bdf
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175026"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>Tutorial: Creación de un informe de forma libre (Report Builder)
  Este tutorial le enseña a crear un informe de forma libre de SSRS que se asemeja a una carta de formularios. Puede organizar los elementos de informe para crear un formulario con cuadros de texto, imágenes y otras regiones de datos.

 El informe que creará en este tutorial se basa en los datos de ventas de ejemplo que se incluyen en el tutorial. El informe agrupa la información por territorio y muestra el nombre del administrador de ventas del territorio, así como una información de ventas detallada y sumaria. Utilizará la región de datos de la lista como la base para el informe de la forma libre y, a continuación, agregará un panel decorativo con una imagen, texto estático con datos insertados, una tabla para mostrar información detallada y, opcionalmente, gráficos circulares y de columnas que muestren la información resumida.

##  <a name="BackToTop"></a>Qué aprenderá
 En este tutorial, aprenderá los siguientes procedimientos:

-   [Crear un informe en blanco, un origen de datos y un conjunto de datos](#BlankReport)

-   [Agregar y configurar una lista](#List)

-   [Agregar gráficos](#Graphics)

-   [Agregar texto en forma libre](#Text)

-   [Agregar una tabla para mostrar detalles](#Table)

-   [Dar formato a datos](#Format)

-   [Guardar el informe](#Save)

### <a name="other-optional-steps"></a>Otros pasos opcionales

-   [Agregar una línea para separar áreas de informe](#Line)

-   [Agregar visualización de datos resumidos](#Visualization)

 Tiempo estimado para completar este tutorial: 20 minutos.

## <a name="requirements"></a>Requisitos
 Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).

##  <a name="BlankReport"></a>1. crear un informe en blanco, un origen de datos y un conjunto de datos

> [!NOTE]
>  En este tutorial, la consulta contiene los valores de los datos, de forma que el informe no necesite un origen de datos externo. Es muy útil usar este tipo de datos internos para el aprendizaje, pero el método hace que la consulta sea larga. .

#### <a name="to-create-a-blank-report"></a>Para crear un informe en blanco

1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.

    > [!NOTE]
    >  Debería aparecer el cuadro de diálogo **Introducción** . Si no hace, en el botón Generador de informes haga clic **Nuevo**.

2.  En el panel izquierdo del cuadro de diálogo **Introducción** , compruebe que **Nuevo informe** está seleccionado.

3.  En el panel derecho, haga clic en **Informe en blanco**.

#### <a name="to-create-a-new-data-source"></a>Para crear un nuevo vista origen de datos

1.  En el panel datos de informe, haga clic en **nuevo**y, a continuación, haga clic en **origen de datos**.

2.  En el `Name` cuadro, escriba: **ListDataSource**

3.  Haga clic en **Usar una conexión incrustada en mi informe**.

4.  Compruebe que el tipo de conexión es Microsoft SQL Server y luego en el cuadro **Cadena de conexión**, escriba: **Origen de datos = \<nombre de servidor>**.

     \<ServerName>, por ejemplo Report001, especifica un equipo en el que se ha instalado una instancia del Motor de base de datos de SQL Server. Dado que los datos del informe no se extraen de una base de datos de SQL Server, no necesita incluir el nombre de una base de datos. Para analizar la consulta se utiliza la base de datos predeterminada en el servidor especificado.

5.  Haga clic en **Credenciales**e introduzca las credenciales necesarias para conectarse a la instancia del Motor de base de datos de SQL Server.

6.  Haga clic en **OK**.

#### <a name="to-create-a-new-dataset"></a>Para crear un nuevo conjunto de datos

1.  En el panel datos de informe, haga clic en **nuevo**y, a continuación, en **conjunto**de datos.

2.  En el `Name` cuadro, escriba: **ListDataset.**

3.  Haga clic en **Usar un conjunto de datos insertado en el informe**y compruebe que el origen de datos es **ListDataSource**.

4.  Compruebe que el tipo de consulta **Texto** está seleccionado, y, a continuación, haga clic en **Diseñador de consultas**.

5.  Haga clic en **Editar como texto**.

6.  Copie y pegue la siguiente consulta en el panel de consulta:

    ```
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity
    ```

7.  Haga clic en el icono Ejecutar para ejecutar la consulta.

     Los resultados de la consulta son los datos disponibles para mostrarse en su informe.

     ![Diseñador de consultas](../../2014/tutorials/media/tutorial-querydesigner.png "Diseñador de consultas")

8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

##  <a name="List"></a>2. agregar y configurar una lista
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona tres plantillas de región de datos: tabla, matriz y lista. Todas estas plantillas se basan en una región de datos Tablix.

 En este tutorial, utilizará una lista para mostrar la información de ventas de los territorios de ventas de un informe similar a un boletín. La información está agrupada por territorio. Agregará un nuevo grupo de filas que agrupa los datos por territorio y, a continuación, eliminará el grupo de filas de detalles integrado. La plantilla de lista es perfecta para crear informes de forma libre. Para obtener más información, vea [las listas &#40;generador de informes y SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).

> [!NOTE]
>  Este informe utiliza la Carta de tamaño del papel (8.5 X11) y márgenes de 1 pulgada. Una página de informe más alta de 9 pulgadas o más ancha de 6 1/2 pulgadas podría generar páginas en blanco.

#### <a name="to-add-a-list"></a>Para agregar una lista

1.  En la pestaña **Insertar** de la cinta de opciones, en el área **Regiones de datos** , haga clic en **Lista** y, a continuación, arrastre la lista dentro del cuerpo del informe. Haga la lista de 7 pulgadas de alto y 6,25 pulgadas de ancho.

2.  Haga clic dentro de la lista, haga clic con el botón secundario en la parte superior de la lista y luego haga clic en **Propiedades de Tablix**.

     ![Añadir lista](../../2014/tutorials/media/tutorial-addinglistwithnumbers.png "Añadir lista")

3.  En la lista desplegable **Nombre del conjunto de datos** , seleccione **ListDataset**.

4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

5.  Haga clic con el botón derecho dentro de la lista y luego haga clic en **Propiedades del rectángulo**.

     ![Comando de las propiedades del rectángulo](../../2014/tutorials/media/tutorial-rectanglepropertiescommand.png "Comando de las propiedades del rectángulo")

6.  En la pestaña **General** , active la casilla **Agregar un salto de página después** .

7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

#### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>Para agregar un nuevo grupo de filas y eliminar el grupo de detalles

1.  En el panel Grupos de filas, haga clic con el botón derecho en el grupo Detalles, seleccione **Agregar grupo**y, después, haga clic en **Grupo primario**.

     ![Comando de grupo primario](../../2014/tutorials/media/tutorial-parentgroupcommand.png "Comando de grupo primario")

2.  En la lista desplegable, seleccione `[Territory].`

3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

     Se agregará una nueva columna a la lista. La columna contiene la celda `[Territory].`.

4.  Haga clic con el botón derecho en la columna Territory de la lista y, después, seleccione **Eliminar columnas**.

     ![Eliminar columnas](../../2014/tutorials/media/tutorial-deletecolumnscommand.png "Eliminar columnas")

5.  Haga clic en **Eliminar solo columnas**.

     ![Eliminar columnas (cuadro de diálogo)](../../2014/tutorials/media/tutorial-deletecolumnsdialog.png "Eliminar columnas, cuadro de diálogo")

6.  En el panel Grupos de filas, haga clic con el botón secundario en el grupo **Detalles** y, luego, haga clic en **Eliminar grupo**.

     ![Eliminar grupo de detalles](../../2014/tutorials/media/tutorial-deletedetailsgroup.png "Eliminar grupo de detalles")

7.  Haga clic en **eliminar solo el grupo**.

8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

##  <a name="Graphics"></a>3. agregar gráficos
 Uno de las ventajas de utilizar una región de datos de la lista es que puede agregar en cualquier parte los elementos de informe, como rectángulos y cuadros de texto, en lugar de limitarse a un diseño tabular. Mejorará la apariencia del informe agregando un gráfico (un rectángulo relleno con un color).

#### <a name="to-add-graphic-elements-to-the-report"></a>Para agregar elementos gráficos al informe

1.  En la pestaña **Insertar** de la cinta de opciones, haga clic en **rectángulo**y, a continuación, arrastre un rectángulo hacia la esquina superior izquierda de la lista. Haga el rectángulo de 7 pulgadas de alto y 1 de ancho.

2.  Haga clic con el botón secundario en el rectángulo y, a continuación, haga clic en **Propiedades del rectángulo**.

3.  Haga clic en la pestaña **Rellenar** .

4.  En la lista desplegable **Color de relleno** , haga clic en **Más colores**y, luego, seleccione el color **GrisOscuro** .

     ![Seleccionar el color de relleno](../../2014/tutorials/media/tutorial-selectfillcolorwithnumbers.png "Seleccionar el color de relleno")

5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.

 La parte izquierda del informe incorpora ahora un gráfico vertical compuesto por un rectángulo gris pizarra.

##  <a name="Text"></a>4. agregar texto de forma libre
 Un cuadro de texto contiene texto estático que se repite en cada página del informe, así como campos de datos.

#### <a name="to-add-text-to-the-report"></a>Para agregar texto al informe

1.  Haga clic en **Diseño** para volver a la vista de diseño.

2.  En la pestaña **Insertar** de la cinta de opciones, haga clic en **Cuadro de texto**y, después, arrastre un cuadro de texto hacia la esquina superior izquierda de la lista, pero dentro del rectángulo que agregó previamente. Haga el cuadro de texto de unas 3 pulgadas de alto y 5 de ancho.

3.  Coloque el cursor en la parte superior del cuadro de texto y, a continuación, escriba: **Boletín para** .

     ![Añadir un texto de encabezado del boletín](../../2014/tutorials/media/tutorial-newsletterfor.png "Añadir un texto de encabezado del boletín")

    > [!NOTE]
    >  Asegúrese de incluir el espacio adicional después de la palabra "para". El espacio separa el texto y el campo que agregará en el paso siguiente.

4.  Arrastre el campo Territory hasta el cuadro de texto y colóquelo después de que el texto que escribió en el paso 3.

     ![Añadir campo territorial](../../2014/tutorials/media/tutorial-addterritorialfield.png "Añadir campo territorial")

5.  Seleccione todo el texto, haga clic con el botón secundario y, a continuación, haga clic en **Propiedades de texto**.

6.  Haga clic en la pestaña **Fuente** .

7.  En la lista **Fuente** , seleccione **Times New Roman**; en **Tamaño** seleccione **20 pto**, en **Color** seleccione **Rojo**.

     ![Propiedades de texto](../../2014/tutorials/media/tutorial-textpropertieswithnumbers.png "Propiedades de texto")

8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

9. Coloque el cursor debajo del texto que escribió en el paso 3 y escriba: **Hola** .

    > [!NOTE]
    >  Asegúrese de incluir el espacio adicional después de la palabra "Hola". El espacio separa el texto y el campo que agregará en el paso siguiente.

10. Arrastre el campo FullName hasta el cuadro de texto y colóquelo después del el texto que escribió en el paso 9 y, a continuación, escribe una coma (,).

     ![Añadir campo de nombre completo](../../2014/tutorials/media/tutorial-addfullnamefield.png "Añadir campo de nombre completo")

11. Seleccionar el texto que agregó en los pasos 9 y 10, haga clic con el botón secundario y, a continuación, haga clic en **Propiedades de texto**

12. Haga clic en la pestaña **Fuente** .

13. En la lista **Fuente** , seleccione **Times New Roman**; en **Tamaño** seleccione **16 pto**, en **Color** seleccione **Negro** .

14. [!INCLUDE[clickOK](../includes/clickok-md.md)]

15. Coloque el cursor debajo del texto que agregó en los pasos 9 a 13, y, a continuación, copie y pegue el siguiente texto de "lorem ipsum":

    ```
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque. 
    Nulla facilisi. Proin ligula enim, porta ut tincidunt id, adipiscing sit amet eros. Ut purus sem, bibendum et vulputate sit amet, facilisis eget magna. Sed aliquam erat non erat eleifend hendrerit. Ut a ligula est, sit amet eleifend enim. Ut et nisl enim, sit amet adipiscing augue. Vivamus eu arcu ac libero posuere elementum. Integer condimentum bibendum venenatis. Integer odio tellus, feugiat in pellentesque semper, interdum nec sem. Sed cursus euismod sem, ut elementum sapien placerat vel. 
    ```

16. Seleccionar el texto que agregó en el paso 15, haga clic con el botón secundario y, a continuación, haga clic en **Propiedades de texto**

17. Haga clic en la pestaña **Fuente** .

18. En la lista **Fuente** , seleccione **Arial**; en **Tamaño** seleccione **10 pto**, en **Color** seleccione **Negro**.

19. [!INCLUDE[clickOK](../includes/clickok-md.md)]

     ![Añadir texto al boletín](../../2014/tutorials/media/tutorial-newslettertext.png "Añadir texto al boletín")

20. Coloque el cursor debajo del texto que pegó en el paso 15, y, a continuación, escriba: **Felicidades por sus ventas totales de** .

    > [!NOTE]
    >  Asegúrese de incluir el espacio adicional después de la palabra "de". El espacio separa el texto y el campo que agregará en el paso siguiente.

21. Arrastre el campo Sales hasta el cuadro de texto, colóquelo después del texto que escribió en el paso 20 y, a continuación, escriba un signo de admiración (!).

22. Resalte el campo ventas, haga clic con el botón secundario en el campo y, a continuación, haga clic en **expresión**.

23. En el cuadro de expresión, cambie la expresión para incluir la función Sum como sigue:

    ```
    =Sum(Fields!Sales.value)
    ```

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]

     ![Añadir una expresión al campo de ventas](../../2014/tutorials/media/tutorial-addexpressiontosalesfield.png "Añadir una expresión al campo de ventas")

25. Seleccionar el texto que agregó en los pasos 20 a 23, haga clic con el botón secundario y, a continuación, haga clic en **Propiedades de texto**

26. Haga clic en la pestaña **Fuente** .

27. En la lista **Fuente** , seleccione **Times New Roman**; en **Tamaño** seleccione **16 pto**, en **Color** seleccione **Rojo**.

28. [!INCLUDE[clickOK](../includes/clickok-md.md)]

29. Seleccione `[Sum(Sales)]` y en la pestaña **Inicio** , en el grupo **Número** , haga clic en el botón **Moneda** .

     ![Añadir símbolo de moneda](../../2014/tutorials/media/tutorial-addcurrencysymbol.png "Añadir símbolo de moneda")

30. Haga clic con el botón derecho en el cuadro de texto con el texto "Haga clic para agregar un título" y, después, haga clic en **Eliminar**.

31. Seleccione el cuadro de lista y utilizando las teclas de dirección, muévalo a la parte superior de la página.

32. Haga clic en **Ejecutar** para obtener la vista previa del informe.

 El informe muestra el texto estático y cada página del informe incluye datos que pertenecen a un territorio. Se da formato a las ventas como moneda.

 ![Vista previa de boletín](../../2014/tutorials/media/tutorial-newsletters.png "Vista previa de boletín")

##  <a name="Table"></a>5. agregar una tabla para mostrar los detalles de ventas
 Utilice el nuevo Asistente para tablas y matrices para agregar una tabla al informe de la forma libre. Después de completar el asistente, agregará manualmente una fila para los totales.

#### <a name="to-add-a-table"></a>Para agregar una tabla

1.  En la pestaña **Insertar** de la cinta de opciones, en el área **Regiones de datos** , haga clic en **Tabla**y, a continuación, haga clic en **Asistente para tablas**.

2.  En la página Elegir un conjunto de datos, haga clic en **ListDataset**.

3.  Haga clic en **Next**.

4.  En la página **Organizar campos** , arrastre el campo Product desde **Campos disponibles** hasta **Valores**.

5.  Repita el paso 4 para SalesDate, Quantity y Sales. Coloque SalesDate bajo Product, Quantity bajo SalesDate y Sales bajo SalesDate.

6.  Haga clic en **Next**.

7.  En la página **Elegir el diseño** , vea el diseño de la tabla.

     La tabla es muy simple. Se compone de cinco columnas y no tiene ningún grupo de filas o columnas. Dado que no tiene ningún grupo, las opciones de diseño relacionadas con los grupos no están disponibles. Actualizará manualmente la tabla para incluir un total en una fase posterior del tutorial.

8.  Haga clic en **Next**.

9. En la página **Elegir un estilo** , en el panel **Estilos** , seleccione **Pizarra**.

10. Haga clic en **Finalizar**

11. Arrastre la tabla bajo el cuadro de texto que agregó en la lección 4.

    > [!NOTE]
    >  Asegúrese de que la tabla está dentro de la lista.

12. Confirme que la tabla está seleccionada y, en el panel Grupo de filas, haga clic con el botón secundario en Detalles, seleccione **Agregar total**y, luego, haga clic en **Después**.

     ![Añadir total del informe](../../2014/tutorials/media/tutorial-addtotal.png "Añadir total del informe")

13. Haga clic en **Ejecutar** para obtener la vista previa del informe.

 El informe muestra una tabla con detalles y totales de ventas.

 ![Totales de ventas en el informe](../../2014/tutorials/media/tutorial-reportsalestotals.png "Totales de ventas en el informe")

##  <a name="Format"></a>6. dar formato a los datos
 Dar formato a datos numéricos como moneda y a fechas como día y hora solamente.

#### <a name="to-format-fields-table"></a>Para dar formato a la tabla de campos

1.  Haga clic en **diseño** para cambiar a la vista Diseño.

2.  Haga clic en las celdas de la tabla que contienen `[Sum(SalesSales)]` y en la pestaña **Inicio** del grupo **Número** haga clic en el botón **Moneda** .

     ![Añadir símbolo de moneda a la suma de las ventas](../../2014/tutorials/media/tutorial-sumsales-currencysymbol.png "Añadir símbolo de moneda a la suma de las ventas")

3.  Haga clic en la celda que contiene `[SalesDate]` y en el grupo **Número** , en la lista desplegable, seleccione **Fecha**.

4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.

 El informe muestra ahora datos dados con formato y es más fácil de leer.

 ![Formatear totales de ventas en el informe](../../2014/tutorials/media/tutorial-reportsalestotals-formatted.png "Formatear totales de ventas en el informe")

##  <a name="Save"></a>7. guardar el informe
 Puede guardar los informes en un servidor de informes, en una biblioteca de SharePoint o en su equipo. También puede exportar el informe en diversos formatos, como Word y PDF: para ello, ejecute el informe y seleccione el formato en el menú **Exportar** .

 En este tutorial, guarde el informe en un servidor de informes. Si no tiene acceso a un servidor de informes, guarde el informe en su equipo.

#### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes

1.  En el botón **generador de informes** , haga clic en **Guardar como**.

2.  Haga clic en **Sitios y servidores recientes**.

3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.

     Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.

4.  En `Name`, reemplace el nombre predeterminado por **SalesInformationByTerritory**.

5.  Haga clic en **Save**(Guardar).

 El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.

#### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo

1.  En el botón **generador de informes** , haga clic en **Guardar como**.

2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde desea guardar el informe.

3.  En `Name`, reemplace el nombre predeterminado por **SalesInformationByTerritory**.

4.  Haga clic en **Save**(Guardar).

##  <a name="Line"></a>8. (opcional) agregar una línea para separar áreas del informe
 Agregue una línea para separar las áreas de editorial y detalles del informe.

#### <a name="to-add-a-line"></a>Para agregar una línea

1.  Haga clic en **Diseño** para volver a la vista de diseño.

2.  En la pestaña **Insertar** de la cinta de opciones, en el área **Elementos de informe** , haga clic en **Línea.**

3.  Dibuje una línea debajo del cuadro de texto de forma libre que agregó en la lección 4.

4.  Haga clic en la línea.

5.  Haga clic en la pestaña **Inicio** .

6.  En el área **Borde** , para el ancho seleccione **4 1/2** pto y para el color seleccione **Rojo**.

     ![Añadir línea al informe](../../2014/tutorials/media/tutorial-reportwithline.png "Añadir línea al informe")

##  <a name="Visualization"></a>9. (opcional) agregar visualización de datos resumidos
 Los rectángulos le ayudan a controlar cómo se representa el informe. Coloque un grafo circular y de columnas dentro de un rectángulo para asegurarse de que el informe se representa del modo que desea.

#### <a name="to-add-a-rectangle"></a>Para agregar un rectángulo

1.  Haga clic en **Diseño** para volver a la vista de diseño.

2.  En la pestaña **Insertar** de la cinta de opciones, en el área **Elementos de informe** haga clic en **Rectángulo**y, a continuación, arrastre el rectángulo dentro de la lista, a la derecha de la tabla. Haga el rectángulo de 2 pulgadas de alto y 4 de ancho.

3.  Alinee las partes superiores del rectángulo y la tabla.

#### <a name="to-add-a-pie-chart"></a>Para agregar un gráfico circular

1.  En la pestaña **Insertar** de la cinta de opciones, en el área **Visualizaciones de datos** , haga clic en **Gráfico** y después haga clic en **Asistente para gráficos**.

2.  En la página Elegir un conjunto de datos, haga clic en **ListDataset**y, después, en **Siguiente**.

3.  Haga clic en **Circular**y, a continuación, en **Siguiente**.

4.  En la página Organizar campos del gráfico, arrastre Product hasta **Categorías**.

5.  Arrastre quantity hasta **valores**y, a continuación, haga clic en **siguiente**.

6.  En la página **Elegir un estilo** , en el panel **Estilos** , seleccione **Pizarra**.

7.  Haga clic en **Finalizar**

8.  Cambie el tamaño del gráfico que aparece en la esquina superior izquierda del informe, para que tenga 1 1/2 pulgadas de alto y 2 de ancho.

9. Arrastre el gráfico dentro del rectángulo.

     ![Añadir gráfico circular](../../2014/tutorials/media/tutorial-addpiechart.png "Añadir gráfico circular")

10. Haga clic con el botón secundario en el título del gráfico y luego haga clic en **Propiedades del título**.

11. En el cuadro de diálogo **Propiedades del título del gráfico** , en texto de título, escriba: **Cantidades de producto vendidas**.

12. Haga clic en la pestaña **Fuente** y en la lista **Tamaño** haga clic en **10 pto**.

13. [!INCLUDE[clickOK](../includes/clickok-md.md)]

#### <a name="to-add-a-column-chart"></a>Para agregar un gráfico de columnas

1.  En la pestaña **Insertar** de la cinta de opciones, en el área **Visualizaciones de datos** , haga clic en **Gráfico** y después haga clic en **Asistente para gráficos**.

2.  En la página **elegir un conjunto** de los, haga clic en **ListDataset**y, a continuación, en **siguiente**.

3.  Haga clic en **Columna**y, a continuación, en **Siguiente**.

4.  En la página organizar campos del gráfico, arrastre el campo Product hasta **categorías**.

5.  Arrastre Sales hasta **Valores** y, después, haga clic en **Siguiente**.

     Valores se muestra en el eje vertical.

6.  En la página **Elegir un estilo** , en el panel **Estilos** , seleccione **Pizarra**.

7.  Haga clic en **Finalizar**

     Un gráfico de columnas se agrega a la esquina superior izquierda del informe.

8.  Cambie el tamaño del gráfico para que tenga 2 pulgadas de ancho y 2 de alto.

9. Arrastre el gráfico al interior del rectángulo, debajo del gráfico circular.

     ![Agregar gráfico de columnas](../../2014/tutorials/media/tutorial-addcolumnchart.png "Agregar gráfico de columnas")

10. Haga clic con el botón secundario en el título del gráfico y después haga clic en **propiedades del título**.

11. En el cuadro de diálogo **Propiedades del título del gráfico** , en texto de título, escriba: **Ventas de producto**.

12. Haga clic en la pestaña **Fuente** y, en la lista **Tamaño** , haga clic en **10 pto**y luego en **Aceptar**.

13. En el gráfico de columnas, haga clic con el botón secundario en el eje vertical y después anule la selección de **Mostrar título del eje**.

14. Repita el paso 13 para el eje horizontal.

15. Haga clic con el botón secundario en la leyenda y, a continuación, haga clic en **Eliminar leyenda**.

    > [!NOTE]
    >  Quitar los títulos y la leyenda de un eje vuelve el gráfico más legible cuando es un tamaño pequeño.

 ![Cambiar los títulos del gráfico y eliminar el título del eje](../../2014/tutorials/media/tutorial-columnchart-newtitle-noaxistitle.png "Cambiar los títulos del gráfico y eliminar el título del eje")

#### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>Para comprobar que los gráficos están dentro del rectángulo

1.  Haga clic en el rectángulo que agregó anteriormente en esta lección.

     En el panel Propiedades, la propiedad `Name` muestra el nombre del rectángulo.

     ![Nombre del rectángulo](../../2014/tutorials/media/tutorial-rectanglename.png "Nombre del rectángulo")

2.  Haga clic en el gráfico circular.

3.  En el panel **propiedades** , compruebe que la `Parent` propiedad contiene el nombre del rectángulo.

     ![Propiedad primaria del gráfico circular](../../2014/tutorials/media/tutorial-piechart-parentproperty.png "Propiedad primaria del gráfico circular")

4.  Haga clic en el gráfico de columnas y repita los pasos 2 y 3.

    > [!NOTE]
    >  Si los gráficos no están dentro del rectángulo, el informe representado no muestra los gráficos juntos.

#### <a name="to-make-the-charts-the-same-size"></a>Para que los gráficos sean del mismo tamaño

1.  Haga clic en el gráfico circular, presione la tecla CTRL y, a continuación, haga clic en el gráfico de columnas.

2.  Con ambos gráficos seleccionados, haga clic con el botón secundario para seleccionar **Diseño**y, a continuación, haga clic en **Igualar ancho**.

     ![Igualar los anchos de los gráficos](../../2014/tutorials/media/tutorial-makechartssamewidth.png "Igualar los anchos de los gráficos")

    > [!NOTE]
    >  El elemento en el que hace clic primero determina el ancho de todos los elementos seleccionados.

3.  Haga clic en **Ejecutar** para obtener la vista previa del informe.

 El informe muestra ahora los datos de ventas resumidos en gráficos circulares y de columnas.

 ![Tutorial de SSRS, informe con formato libre](../../2014/tutorials/media/tutorial-reportfinal.png "Tutorial de SSRS, informe con formato libre")

## <a name="more-information"></a>Más información
 Para obtener más información acerca de las listas, consulte [tablas, matrices y listas &#40;generador de informes y ssrs&#41;](report-design/tables-matrices-and-lists-report-builder-and-ssrs.md), [enumera &#40;Generador de informes y SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md), áreas de la [región de datos Tablix &#40;generador de informes y SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md)y [celdas, filas y columnas de la región de datos Tablix &#40;generador de informes&#41; y SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).

 Para más información sobre los diseñadores de consultas, vea [Diseñadores de consultas &#40;Generador de informes&#41;](../../2014/reporting-services/query-designers-report-builder.md) e [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](report-data/text-based-query-designer-user-interface-report-builder.md).

## <a name="see-also"></a>Consulte también
 [Tutoriales &#40;Generador de informes&#41;](report-builder-tutorials.md) [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)


