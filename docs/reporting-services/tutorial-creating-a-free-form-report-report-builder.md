---
title: 'Tutorial: Crear un informe de forma libre (Generador de informes) | Microsoft Docs'
description: Aprenda a crear un informe paginado que actúe como un boletín y donde cada página muestre texto estático, objetos visuales de resumen y datos de ventas de ejemplo detallados.
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b189c494f887faca2b6d3d4bb00253992470132
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247464"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>Tutorial: Creación de un informe de forma libre (Report Builder)
En este tutorial, creará un informe paginado que actúa como un boletín. Cada página muestra texto estático, objetos visuales de resumen y datos de ventas de ejemplo detallados.

![report-builder-free-form-report-complete](../reporting-services/media/report-builder-free-form-report-complete.png)

El informe agrupa la información por territorio y muestra el nombre del administrador de ventas del territorio, así como una información de ventas detallada y sumaria. Comenzará con una región de datos de la lista como la base para el informe de forma libre y, después, agregará un panel decorativo con una imagen, texto estático con datos insertados, una tabla para mostrar información detallada y, opcionalmente, gráficos circulares y de columnas que muestren la información resumida.  
  
Tiempo estimado para completar este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="1-create-a-blank-report-data-source-and-dataset"></a><a name="BlankReport"></a>1. Crear un informe en blanco, un origen de datos y un conjunto de datos  
  
> [!NOTE]  
> En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
### <a name="to-create-a-blank-report"></a>Para crear un informe en blanco  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, asegúrese de que está seleccionada la opción **Nuevo informe** . 
 
3.  En el panel derecho, haga clic en **Informe en blanco**.  
  
### <a name="to-create-a-new-data-source"></a>Para crear un nuevo vista origen de datos  
  
1.  En el panel Datos de informe, haga clic en **Nuevo** > **Origen de datos**.  
  
2.  En el cuadro **Nombre**, escriba: **ListDataSource**  
  
3.  Haga clic en **Usar una conexión incrustada en mi informe**.  
  
4.  Compruebe que el tipo de conexión sea Microsoft SQL Server y, luego, en el cuadro **Cadena de conexión** , escriba: **Origen de datos = \<servername>**  
  
    **\<servername>** , por ejemplo Informe001, especifica un equipo en el que se ha instalado una instancia del motor de base de datos de SQL Server. Dado que los datos del informe no se extraen de una base de datos de SQL Server, no necesita incluir el nombre de una base de datos. Para analizar la consulta se usa la base de datos predeterminada en el servidor especificado.  
  
5.  Haga clic en **Credenciales**e introduzca las credenciales necesarias para conectarse a la instancia del Motor de base de datos de SQL Server.  
  
6.  Haga clic en **OK**.  
  
### <a name="to-create-a-new-dataset"></a>Para crear un nuevo conjunto de datos  
  
1.  En el panel Datos de informe, haga clic en **Nuevo** > **Conjunto de datos**.  
  
2.  En el cuadro **Nombre**, escriba: **ListDataset**.  
  
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
  
7.  Haga clic en el icono **Ejecutar** (!) para ejecutar la consulta.  
  
    Los resultados de la consulta son los datos disponibles para mostrarse en su informe.  
  
    ![report-builder-free-form-tutorial-data](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="2-add-and-configure-a-list"></a><a name="List"></a>2. Agregar y configurar una lista  
En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , la región de datos de lista es perfecta para crear informes de forma libre. Se basa en la región de datos *tablix* , ya que son tablas y matrices. Para obtener más información, consulte [Crear facturas y formularios con listas](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
Usará una lista para mostrar la información de ventas sobre los territorios de ventas en un informe con el formato de un boletín. La información está agrupada por territorio. Agregará un nuevo grupo de filas que agrupa los datos por territorio y, a continuación, eliminará el grupo de filas de detalles integrado.  
  
### <a name="to-add-a-list"></a>Para agregar una lista  
  
1.  En la pestaña **Insertar** > **Regiones de datos** > **Lista**. 

2. Haga clic en el cuerpo del informe (entre las áreas de título y pie de página) y arrastre para crear el cuadro de lista. Haga el cuadro de lista de 7 pulgadas de alto y 6,25 pulgadas de ancho. Para obtener el tamaño exacto, en el panel **Propiedades** en **Posición**, escriba los valores de las propiedades **Ancho** y **Alto** .
  
    > [!NOTE]  
    > Este informe utiliza la Carta de tamaño del papel (8.5 X11) y márgenes de 1 pulgada. Un cuadro de lista más alto de 9 pulgadas o más ancho de 6,5 pulgadas podría generar páginas en blanco.  
  
2.  Haga clic dentro del cuadro de lista, haga clic con el botón derecho en la parte superior de la lista y luego haga clic en **Propiedades de Tablix**.  
  
    ![report-builder-free-form-tablix-properties](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  En la lista desplegable **Nombre del conjunto de datos** , seleccione **ListDataset**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Haga clic con el botón derecho dentro de la lista y luego haga clic en **Propiedades del rectángulo**.  
  
6.  En la pestaña **General** , active la casilla **Agregar un salto de página después** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>Para agregar un nuevo grupo de filas y eliminar el grupo de detalles  
  
1.  En el panel Grupos de filas, haga clic con el botón derecho en el grupo Detalles, seleccione **Agregar grupo**y, después, haga clic en **Grupo primario**.  
  
    ![report-builder-free-form-add-parent-group](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  En la lista **Agrupar por** , seleccione `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Una columna que contiene la celda `[Territory]` se agrega a la lista.
  
4.  Haga clic con el botón derecho en la columna Territory de la lista y, después, seleccione **Eliminar columnas**.  
  
    ![report-builder-free-form-delete-columns](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  Seleccione **Eliminar solo columnas**.  
  
6.  En el panel Grupos de filas, haga clic con el botón derecho en el grupo **Detalles** > **Eliminar grupo**.  
   
7.  Seleccione **Eliminar solo el grupo**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="3-add-graphic-elements"></a><a name="Graphics"></a>3. Agregar elementos gráficos  
Una de las ventajas de las regiones de datos de la lista es que puede agregar en cualquier parte los elementos de informe, como rectángulos y cuadros de texto, en lugar de limitarse a un diseño tabular. Mejorará la apariencia del informe agregando un gráfico (un rectángulo relleno con un color).  
  
### <a name="to-add-graphic-elements-to-the-report"></a>Para agregar elementos gráficos al informe  
  
1.  En la pestaña **Insertar** , seleccione **Rectángulo**. 

2. Haga clic en la esquina superior izquierda de la lista y arrastre para crear el rectángulo de 7 pulgadas de alto y 3,5 pulgadas de ancho. De nuevo, para obtener el tamaño exacto, en el panel **Propiedades** en **Posición**, escriba los valores de **Ancho** y **Alto**.
  
2.  Haga clic con el botón derecho en el rectángulo > **Propiedades del rectángulo**.  
  
3.  Haga clic en la pestaña **Rellenar** .  
  
4.  En **Color de relleno**, seleccione **Gris claro**.  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
La parte izquierda del informe tiene ahora un gráfico vertical compuesto por un rectángulo gris claro, tal y como se muestra en la imagen siguiente.  
  
![report-builder-free-form-gray-rectangle](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="4-add-free-form-text"></a><a name="Text"></a>4. Agregar texto en forma libre  
Puede agregar cuadros de texto para mostrar texto estático que se repite en cada página del informe, así como campos de datos.  
  
### <a name="to-add-text-to-the-report"></a>Para agregar texto al informe  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  En la pestaña **Insertar** > **Cuadro de texto**. Haga clic en la esquina superior izquierda de la lista, dentro del rectángulo que ha agregado anteriormente, y arrastre para crear el cuadro de texto de 3,45 pulgadas de ancho y 5 pulgadas de alto.  
  
3.  Coloque el cursor en el cuadro de texto y escriba: **Boletín para** . Incluya un espacio después de la palabra "para" para separar el texto del campo que se va a agregar en el paso siguiente.   
  
    ![Agregar un texto de encabezado del boletín](../reporting-services/media/tutorial-newsletterfor.png "Agregar un texto de encabezado del boletín")  
  
4.  Arrastre el campo `[Territory]` de ListDataSet en el panel Datos de informe al cuadro de texto y colóquelo después de "Boletín para ".  
  
    ![report-builder-free-form-territory-field](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  Seleccione el texto y el campo `[Territory]` .  
  
6.  En la pestaña **Inicio** > **Fuente**, seleccione: 
  
    *  **Segoe Semibold**.
    *  **20 pt**.
    *  **Tomate**.  
  
9. Coloque el cursor debajo del texto que ha escrito en el paso 3 y escriba: **Hola,** con un espacio después para separar el texto y el campo que se va a agregar en el paso siguiente.  
 
10. Arrastre el campo `[FullName]` de ListDataSet en el panel Datos de informe al cuadro de texto y colóquelo después de "Hola," y luego escriba dos puntos (:).  
   
11. Seleccione el texto que ha agregado en los pasos anteriores.
  
12. En la pestaña **Inicio** > **Fuente**, seleccione: 
  
    *  **Segoe Semibold**.
    *  **16 pt**.
    *  **Negro**.  
   
15. Coloque el cursor debajo del texto que ha agregado en los pasos 9 a 13 y luego copie y pegue el siguiente texto que carece de sentido:  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. Seleccione el texto que acaba de agregar.  
  
17.  En la pestaña **Inicio** > **Fuente**, seleccione: 
  
      *  **Segoe UI**.
      *  **10 pt**.
      *  **Negro**.  
 
20. Coloque el cursor dentro del cuadro de texto, debajo del texto que carece de sentido y escriba: **Felicidades por sus ventas totales de**, con un espacio después de la palabra para separar el texto y el campo que agregará en el paso siguiente. 
  
21. Arrastre el campo Sales hasta el cuadro de texto, colóquelo después del texto que ha escrito en el paso anterior y luego escriba un signo de exclamación (!).  

25. Seleccione el texto y el campo que acaba de agregar.  
  
17.  En la pestaña **Inicio** > **Fuente**, seleccione: 
  
      *  **Segoe Semibold**.
      *  **16 pt**.
      *  **Negro**.  
  
22. Seleccione solo el campo `[Sales]`, haga clic con el botón derecho en el campo > **Expresión**.  
  
23. En el cuadro **Expresión** , cambie la expresión para incluir la función Sum como sigue:  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![report-builder-free-form-text-box](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. Con `[Sum(Sales)]` aún seleccionado, en la pestaña **Inicio** > grupo **Número** > **Moneda**.  
  
30. Haga clic con el botón derecho en el cuadro de texto con el texto "Haga clic para agregar un título" y, después, haga clic en **Eliminar**.  
  
31. Seleccione el cuadro de lista. Seleccione las dos flechas de dos puntas y muévalo a la parte superior de la página.  

    ![report-builder-drag-list](../reporting-services/media/report-builder-drag-list.png)
  
32. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe muestra el texto estático y cada página del informe incluye datos que pertenecen a un territorio. Se da formato a las ventas como moneda.  
  
![report-builder-newsletter-page-preview](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="5-add-a-table-to-show-sales-details"></a><a name="Table"></a>5. Agregar una tabla para mostrar los detalles de ventas  
Utilice el nuevo Asistente para tablas y matrices para agregar una tabla al informe de la forma libre. Después de completar el asistente, agregará manualmente una fila para los totales.  
  
### <a name="to-add-a-table"></a>Para agregar una tabla  
  
1.  En la pestaña **Insertar** > área **Regiones de datos** > **Tabla** > **Asistente para tablas**.  
  
2.  En la página **Elegir un conjunto de datos** , haga clic en **ListDataset** > **Siguiente**.  
  
4.  En la página **Organizar campos** , arrastre el campo Product desde **Campos disponibles** hasta **Valores**.  
  
5.  Repita el paso 3 para SalesDate, Quantity y Sales. Coloque SalesDate bajo Product, Quantity bajo SalesDate y Sales bajo SalesDate.  
  
6.  Haga clic en **Next**.  
  
7.  En la página **Elegir el diseño** , vea el diseño de la tabla.  
  
    La tabla es simple: cinco columnas sin grupos de filas o columnas. Dado que no tiene ningún grupo, las opciones de diseño relacionadas con los grupos no están disponibles. Actualizará manualmente la tabla para incluir un total en una fase posterior del tutorial.  
  
8.  Haga clic en **Next**.  
  
9. Haga clic en **Finalizar**  
  
11. Arrastre la tabla bajo el cuadro de texto que agregó en la lección 4.  
  
    > [!NOTE]  
    > Asegúrese de que la tabla está dentro del cuadro de lista y dentro del rectángulo gris.  
  
12. Con la tabla seleccionada, en el panel **Grupo de filas** , haga clic con el botón derecho en **Detalles** > **Agregar total** > **Después**.  
  
    ![report-builder-free-form-table-totals](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. Seleccione la celda de la columna Product y escriba **Total**.

    ![report-builder-free-form-type-total](../reporting-services/media/report-builder-free-form-type-total.png)

12. Seleccione el campo [SalesDate]. En la pestaña **Inicio** > **Número**, cambie **Valor predeterminado** por **Fecha**.

13. Seleccione los campos [SUM(Sales)]. En la pestaña **Inicio** > **Número**, cambie **Valor predeterminado** por **Moneda**.

Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe muestra una tabla con detalles y totales de ventas.  
  
![report-builder-free-form-with-table](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="6-save-the-report"></a><a name="Save"></a>6. Guardar el informe  
Puede guardar los informes en un servidor de informes, en una biblioteca de SharePoint o en su equipo.  
  
En este tutorial, guarde el informe en un servidor de informes. Si no tiene acceso a un servidor de informes, guarde el informe en su equipo.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
    Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **SalesInformationByTerritory**.  
  
5.  Haga clic en **Save**(Guardar).  
  
El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde desea guardar el informe.  
  
3.  En **Nombre**, reemplace el nombre predeterminado por **SalesInformationByTerritory**.  
  
4.  Haga clic en **Save**(Guardar).  
  
## <a name="7-optional-add-a-line-to-separate-areas-of-the-report"></a><a name="Line"></a>7. (Opcional) Agregar una línea para separar áreas del informe  
Agregue una línea para separar las áreas de editorial y detalles del informe.  
  
### <a name="to-add-a-line"></a>Para agregar una línea  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  En la pestaña **Insertar** > **Elementos de informe** > **Línea**.  
  
3.  Dibuje una línea debajo del cuadro de texto que ha agregado en la lección 4.  
  
4.  Haga clic en la línea y, en la pestaña **Inicio** > **Borde**, seleccione:
     * **Ancho** seleccione **3** pt.
     * **Color** seleccione **Tomate**.  
  
## <a name="8-optional-add-summary-data-visualizations"></a><a name="Visualization"></a>8. (Opcional) Agregar visualizaciones de datos resumidos  
Los rectángulos le ayudan a controlar cómo se representa el informe. Coloque un grafo circular y de columnas dentro de un rectángulo para asegurarse de que el informe se representa del modo que desea.  
  
### <a name="to-add-a-rectangle"></a>Para agregar un rectángulo  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  En la pestaña **Insertar** > **Elementos de informe** >  **Rectángulo**. Arrastre el rectángulo dentro del cuadro de lista a la derecha de la tabla para crear un rectángulo de aproximadamente 2,25 pulgadas de ancho y 7,9 pulgadas de alto.  
  
3.  Con el nuevo rectángulo seleccionado, en el panel Propiedades, haga **BorderColor LightGrey**, **BorderStyle Solid**y **BorderWidth 2 pt**. 

4. Alinee las partes superiores del rectángulo y la tabla.  
  
## <a name="to-add-a-pie-chart"></a>Para agregar un gráfico circular  
  
1.  En la pestaña **Insertar** > **Visualizaciones de datos** > **Gráfico** > **Asistente para gráficos**.  
  
2.  En la página **Elegir un conjunto de datos** , haga clic en **ListDataset** > **Siguiente**.  
  
3.  Haga clic en **Circular** > **Siguiente**.  
  
4.  En la página Organizar campos del gráfico, arrastre Product hasta **Categorías**.  
  
5.  Arrastre Quantity hasta **Valores**y, después, haga clic en **Siguiente**.  
  
6.  Haga clic en **Finalizar**  
  
8.  Cambie el tamaño del gráfico que aparece en la esquina superior izquierda del informe, para que tenga aproximadamente 2,25 pulgadas de ancho y 3,6 de alto.  
  
9. Arrastre el gráfico dentro del rectángulo.  
   
10. Seleccione el título del gráfico y escriba: **Cantidades de producto vendidas**.  
  
12. En la pestaña **Inicio** > **Fuente**, para el título:
    * **Fuente** **Segoe UI Semibold**.
    * **Tamaño** **12 pt**.
    * **Color** **Negro**.  

13. Haga clic con el botón derecho en la leyenda > **Propiedades de la leyenda**.

14. En la pestaña **General** , en **Posición de la leyenda**, seleccione el punto central en la parte inferior. 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. Si es necesario, arrastre para que la región del gráfico sea más alta.

     ![report-builder-free-form-pie](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>Para agregar un gráfico de columnas  
  
1.  En la pestaña **Insertar** > **Visualizaciones de datos** > **Gráfico,**  > **Asistente para gráficos**.  
  
2.  En la página **Elegir un conjunto de datos** , haga clic en **ListDataset**y, después, en **Siguiente**.  
  
3.  Haga clic en **Columna**y, luego, en **Siguiente**.  
  
4.  En la página **Organizar campos del gráfico** , arrastre el campo Product hasta **Categorías**.  
  
5.  Arrastre Sales hasta **Valores** y, después, haga clic en **Siguiente**.  
  
    Valores se muestra en el eje vertical.  
  
6.  Haga clic en **Finalizar**  
  
    Un gráfico de columnas se agrega a la esquina superior izquierda del informe.  
  
8.  Cambie el tamaño del gráfico para que tenga aproximadamente 2,25 pulgadas de ancho y casi 4 pulgadas de alto.  
  
9. Arrastre el gráfico al interior del rectángulo, debajo del gráfico circular.  
   
10. Seleccione el título del gráfico y escriba: **Ventas de producto**.  
  
12. En la pestaña **Inicio** > **Fuente**, para el título:
    * **Fuente** **Segoe UI Semibold**.
    * **Tamaño** **12 pt**.
    * **Color** **Negro**.  
  
15. Haga clic con el botón secundario en la leyenda y, a continuación, haga clic en **Eliminar leyenda**.  
  
    > [!NOTE]  
    > Quitar la leyenda hace que el gráfico sea más legible si el gráfico es pequeño.  
  
    ![report-builder-free-form-column](../reporting-services/media/report-builder-free-form-column.png)

12. Seleccione el eje del gráfico y en la pestaña **Inicio** > **Número** > **Moneda**.

13. Seleccione **Disminuir decimales** dos veces, de modo que el número muestre solo dólares sin centavos.      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>Para comprobar que los gráficos están dentro del rectángulo  

Puede usar rectángulos como contenedores para otros elementos de una página del informe. Obtenga más información sobre [rectángulos como contenedores](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md).
  
1.  Seleccione el rectángulo que ha creado y al que ha agregado los gráficos, anteriormente en esta lección.  
  
    En el panel Propiedades, la propiedad **Name** muestra el nombre del rectángulo.  
  
    ![report-builder-free-form-rectangle-name](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  Haga clic en el gráfico circular.  
  
3.  En el panel **Propiedades** , compruebe que la propiedad **Parent** contiene el nombre del rectángulo.  
  
     ![report-builder-free-form-pie-parent](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  Haga clic en el gráfico de columnas y repita el paso 3.  
  
    > [!NOTE]  
    > Si los gráficos no están dentro del rectángulo, el informe representado no muestra los gráficos juntos.  
  
### <a name="to-make-the-charts-the-same-size"></a>Para que los gráficos sean del mismo tamaño  
  
1.  Seleccione el gráfico circular, pulse la tecla CTRL y, después, seleccione el gráfico de columnas.  
  
2.  Con ambos gráficos seleccionados, haga clic con el botón derecho > **Diseño** > **Igualar ancho**.  
  
    > [!NOTE]  
    > El elemento en el que hace clic primero determina el ancho de todos los elementos seleccionados.  
  
3.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe muestra ahora los datos de ventas resumidos en gráficos circulares y de columnas.  
  

  
## <a name="next-steps"></a>Pasos siguientes  
Esto concluye el tutorial sobre cómo crear un informe de forma libre.  
  
Para obtener más información sobre las listas, consulte: 
* [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [Creación de facturas y formularios con listas](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
Para más información sobre los diseñadores de consultas, vea [Herramientas de diseño de consulta (SSRS)](report-data/query-design-tools-ssrs.md) e [Interfaz de usuario del diseñador de consultas basado en texto &#40;Generador de informes&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Consulte también  
[Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md) 
  

