---
title: 'Tutorial: Crear un informe de matriz (Generador de informes) | Microsoft Docs'
ms.custom: 
ms.date: 06/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
caps.latest.revision: "15"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ee61088e30c0c2be4caa7a6989e56812c77fe0e3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>Tutorial: Crear un informe de matriz (Generador de informes)
Este tutorial le enseña a crear un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] con una matriz de datos de ventas de ejemplo en los grupos anidados de filas y columnas. 

También creará un grupo de columnas adyacente, dará formato a columnas y girará el texto. En la siguiente ilustración se muestra un informe similar al que creará.  
  
![report-builder-matrix-tutorial](../reporting-services/media/report-builder-matrix-tutorial.png)
   
Tiempo estimado para completar este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener información sobre los requisitos, consulte [Requisitos previos para los tutoriales](../reporting-services/prerequisites-for-tutorials-report-builder.md). 
  
## <a name="CreateMatrix"></a>1. Crear un informe de matriz y un conjunto de datos desde el nuevo Asistente para tablas o matrices  
En esta sección, elegirá un origen de datos compartido, creará un conjunto de datos insertado y, después, mostrará los datos en una matriz.  
  
> [!NOTE]  
> En este tutorial, la consulta contiene ya los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
### <a name="to-create-a-matrix"></a>Para crear una matriz  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos. Si no hay disponible ningún origen de datos o no tiene acceso a un servidor de informes, puede utilizar un origen de datos incrustados en su lugar. Para más información sobre cómo crear un origen de datos insertado, vea [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
9. Copie y pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. (opcional) Haga clic en el icono Ejecutar (!) para ejecutar la consulta y ver los datos.

11. Haga clic en **Siguiente**.  
  
## <a name="Groups"></a>2. Organizar datos y elegir el diseño desde el Asistente para nueva tabla o matriz  
Utilice el asistente para proporcionar un diseño inicial en el que mostrar los datos. El panel de vista previa del asistente le ayudará a visualizar el resultado de las agrupaciones de datos antes de completar el diseño de la matriz.  
  
1.  En la página **Organizar campos** , arrastre Territory desde **Campos disponibles** a **Grupos de filas**.  
  
2.  Arrastre SalesDate hasta **Grupos de filas** y colóquelo debajo de Territory.  
  
    El orden en el que se enumeran los campos en **Grupos de filas** define la jerarquía de grupos. Los pasos 1 y 2 organizan los valores de los campos primero por territorio y, después, por la fecha de las ventas.  
  
3.  Arrastre Subcategory a **Grupos de columnas**.  
  
4.  Arrastre Product a **Grupos de columnas** y colóquelo debajo de Subcategory.  
  
    De nuevo, el orden en el que se enumeran los campos en **Grupos de columnas** define la jerarquía de grupos. Los pasos 3 y 4 organizan los valores de los campos primero por subcategoría y, después, por producto.  
  
5.  Arrastre Sales a **Valores**.  
  
    El campo Sales se resume con la función Sum, que es la función predeterminada para resumir campos numéricos.  
  
6.  Arrastre Quantity a **Valores**.  
  
    El campo Quantity se resume con la función Sum.  
  
    Los pasos 5 y 6 especifican los datos que deben mostrarse en las celdas de datos de la matriz.
    
    ![report-builder-arrange-fields-report-wizard](../reporting-services/media/report-builder-arrange-fields-report-wizard.png)  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página Elegir el diseño, en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
9. Compruebe que esté seleccionada la opción **Bloqueado, subtotal abajo** .  
  
10. Compruebe que la opción **Expandir o contraer grupos** está seleccionada.  
  
11. Haga clic en **Siguiente**.  
  
13. Haga clic en **Finalizar**.  
  
    La matriz se agrega a la superficie de diseño. El panel Grupos de filas muestra dos grupos de filas: Territory y SalesDate. El panel Grupos de columnas muestra dos grupos de columnas: Subcategory y Product. Los datos detallados son todos los datos recuperados por la consulta del conjunto de datos.  
    
    ![report-builder-row-and-column-groups](../reporting-services/media/report-builder-row-and-column-groups.png)
  
14. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
    Para cada producto que se vende en una fecha concreta, la matriz muestra la subcategoría a la que pertenece el producto y el territorio de las ventas.  

14. Expanda una subcategoría. Puede ver que el informe se amplía de forma rápida.

![report-builder-expand-matrix](../reporting-services/media/report-builder-expand-matrix.png)
  
## <a name="FormatData"></a>3. Dar formato a datos  
De forma predeterminada, los datos de resumen para el campo Sales muestran un número general y el campo SalesDate muestra información de fecha y de hora. En esta sección, dará formato al campo Sales para mostrar el número como moneda y al campo SalesDate para mostrar solo la fecha. Alterne **Estilos de marcador de posición** para mostrar los cuadros de texto con formato y el texto de marcador de posición como valores de ejemplo.  
  
### <a name="to-format-fields"></a>Para dar formato a los campos  
  
1.  Haga clic en **Diseño** para cambiar a la vista de diseño.  
  
2.  Presione la tecla CTRL y, a continuación, seleccione las nueve celdas que contienen `[Sum(Sales)]`.  
  
3.  En la pestaña **Inicio** > **Número** > **Moneda**. Las celdas cambian para mostrar la moneda con formato.  
  
    Si la configuración regional es Inglés (Estados Unidos), el texto de ejemplo predeterminado es [**$12,345.00**]. Si no ve un valor de moneda de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** > **Valores de ejemplo**.  
    
    ![report-builder-placeholder-value](../reporting-services/media/report-builder-placeholder-value.png)
  
4.  Haga clic en la celda que contiene `[SalesDate]`.  
  
5.  En el grupo **Número** > **Fecha**.  
  
    La celda muestra la fecha de ejemplo **[1/31/2000]**. Si no ve un valor de fecha de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** y, después, haga clic en **Valores de ejemplo**.  
  
6.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
Los valores de fecha solo muestran fechas y los valores de ventas se muestran como moneda.  
  
## <a name="AdjacentGroup"></a>4. Agregar grupo de columnas adyacente  
Puede anidar grupos de filas y de columnas en relaciones de elementos primarios y secundarios o adyacentes en relaciones del mismo nivel.  
  
En esta sección, agregará un grupo de columnas adyacente al grupo de columnas de Subcategory, copiará las celdas para rellenar el nuevo grupo de columnas y, después, usará una expresión para crear el valor del encabezado de grupo de columnas.  
  
### <a name="to-add-an-adjacent-column-group"></a>Para agregar un grupo de columnas adyacente  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic con el botón derecho en la celda que contiene `[Subcategory]`, señale **Agregar grupo**y luego haga clic en **Adyacente a la derecha**.  
  
    Se abre el cuadro de diálogo **Grupo de Tablix** .  
  
3.  En la lista **Agrupar por** , seleccione SalesDate y, después, haga clic en **Aceptar**.  
  
    Se agrega un nuevo grupo de columnas a la derecha del grupo de columnas de Subcategory.  
  
4.  Haga clic con el botón derecho en la celda del nuevo grupo de columnas que contiene `[SalesDate],` y luego haga clic en **Expresión**.  
  
5.  Copie la siguiente expresión en el cuadro de expresión.  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
    Esta expresión extrae el nombre del día de la semana de la fecha de ventas. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
6.  Haga clic con el botón derecho en la celda del grupo de columnas de Subcategory que contiene Total y luego haga clic en **Copiar**.  
  
7.  Haga clic con el botón derecho en la celda situada inmediatamente debajo de la celda que contiene la expresión que ha creado en el paso 5 y haga clic en **Pegar**.  
  
8.  Presione la tecla CTRL.  
  
9. En el grupo Subcategory, haga clic en el encabezado de columna Sales y las tres celdas debajo de él, haga clic con el botón derecho y, después, haga clic en **Copiar**.  
  
10. Pegue las cuatro celdas en las cuatro celdas vacías en el nuevo grupo de columnas.  
  
11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe incluye columnas denominadas Monday y Tuesday. El conjunto de datos solo contiene los datos de estos dos días.  

![report-builder-matrix-weekdays](../reporting-services/media/report-builder-matrix-weekdays.png)
  
> [!NOTE]  
> Si los datos incluyeran otros días, el informe también incluiría las columnas correspondientes. Cada columna tiene el encabezado de columna **Sales**y los totales de ventas por territorio.  
  
## <a name="Width"></a>5. Cambiar el ancho de columna  
Un informe que incluye una matriz normalmente se expande horizontalmente así como verticalmente cuando se ejecuta. Controlar la expansión horizontal es particularmente importante si piensa exportar el informe a los formatos como Microsoft Word o Adobe PDF, que se utilizan para los informes impresos. Si el informe se expande horizontalmente por varias páginas, el informe impreso es difícil de entender. Para minimizar la expansión horizontal, puede cambiar el tamaño de las columnas para que tengan solo el ancho necesario para mostrar los datos sin ajustar. También puede cambiar el nombre de las columnas para que sus títulos con el ancho necesario para mostrar los datos.  
  
### <a name="to-rename-and-resize-the-columns"></a>Cambiar el nombre y el tamaño de las columnas  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Seleccione el texto de la columna Quantity situada más a la izquierda y, después, escriba **QTY**.  
  
    El título de la columna es ahora QTY.  
  
3.  Repita el paso 2 en las otras dos columnas denominadas Quantity.
  
4.  Haga clic en la matriz para que los identificadores de columna y de fila aparezcan encima y al lado de la matriz.  
  
    Las barras grises situadas en la parte superior y en el lado de la tabla son los identificadores de fila y de columna.  
    
    ![report-builder-column-handles](../reporting-services/media/report-builder-column-handles.png)
  
5.  Para cambiar el tamaño de la columna QTY más alejada de la izquierda, seleccione la línea entre los identificadores de columna para que el cursor cambie a una flecha doble. Arrastre la columna hacia la izquierda hasta que el ancho sea de 1/2 pulgada.  
  
    Un ancho de columna de 1/2 pulgada es adecuado para mostrar la cantidad.  
  
6.  Repita el paso 5 en las otras columnas denominadas QTY.  
  
7.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
Las columnas que contienen cantidades son ahora más estrechas y se denominan QTY.  
  
## <a name="MergeCells"></a>6. Combinar las celdas de la matriz  
El área de la esquina está en la esquina superior izquierda de la matriz Dependiendo del número de grupos de filas y columnas de la matriz, el número de celdas en el área de la esquina varía. La matriz generada en este tutorial tiene cuatro celdas en su área de esquina. Las celdas se disponen en dos filas y dos columnas, reflejando la profundidad de las jerarquías de grupos de filas y columnas. Las cuatro celdas no se utilizan en este informe y los combinará en una.  
  
### <a name="to-merge-matrix-cells"></a>Para combinar las celdas de la matriz  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la matriz para que los identificadores de columna y de fila aparezcan encima y al lado de la matriz.  
  
3.  Pulse la tecla CTRL y seleccione las cuatro celdas de la esquina.  
  
4.  Haga clic con el botón derecho en las celdas y, después, en **Combinar celdas**.  
  
5.  Haga clic con el botón derecho en la nueva celda combinada y haga clic en **Propiedades de cuadro de texto**.  
  
6.  En la pestaña **Borde** > **Valores predeterminados** > **Ninguno**.
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
La celda en la esquina superior de la matriz ya no está visible. 
  
## <a name="HeaderTitle"></a>7. Agregar un encabezado y un título del informe  
Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. En este tutorial, quitará el cuadro de texto de la parte superior del informe y agregará un título al encabezado.  
  
### <a name="to-add-a-report-header-and-report-title"></a>Para agregar un encabezado y un título del informe  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Seleccione el cuadro de texto de la parte superior del cuerpo del informe que contiene **Haga clic para agregar un título**y, después, pulse la tecla Suprimir.  
  
3.  En la pestaña **Insertar** > **Encabezado** > **Agregar encabezado**.  
  
    Se agrega un encabezado a la parte superior del cuerpo del informe.  
  
4.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**y luego arrastre un cuadro de texto al encabezado del informe. Haga un cuadro de texto de aproximadamente 6 pulgadas de largo y 3/4 de pulgada de alto, y colóquelo en el lado izquierdo del encabezado del informe.  
  
5.  En el cuadro de texto, escriba **Ventas por territorio, Subcategoría y Día**.  
  
6.  Seleccione el texto que ha escrito, en la pestaña **Inicio** > **Fuente**:
    * **Tamaño 24 pt**
    * **Color Rojo oscuro**
 
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe incluye un título de informe en el encabezado del informe.  
  
## <a name="Save"></a>8. Guardar el informe  
Puede guardar los informes en un servidor de informes, en una biblioteca de SharePoint o en su equipo.  
  
En este tutorial, guarde el informe en un servidor de informes. Si no tiene acceso a un servidor de informes, guarde el informe en su equipo.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
    Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, verá el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **SalesByTerritorySubcategory**.  
  
5.  Haga clic en **Guardar**.  
  
El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde desea guardar el informe.  
  
3.  En **Nombre**, reemplace el nombre predeterminado por **SalesByTerritorySubcategory**.  
  
4.  Haga clic en **Guardar**.  
  
## <a name="RotateTextBox"></a>9. (Opcional) Girar 270 grados el cuadro de texto  
Un informe con matrices se puede expandir horizontal y verticalmente cuando se ejecuta. Girando los cuadros de texto verticalmente o 270 grados, puede ahorrar espacio horizontal. El informe representado se hace más estrecho y, si se exporta a un formato como Microsoft Word, tendrá más posibilidades de ajustar en una página impresa.  
  
Un cuadro de texto también puede mostrar el texto como horizontal o como, vertical (de arriba abajo). Para más información, vea [Cuadros de texto &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md).  
  
### <a name="to-rotate-text-box-270-degrees"></a>Para girar el cuadro de texto 270 grados  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Seleccione la celda que contiene `[Territory].` 

    >**Nota**: Seleccione la celda, no el texto. La propiedad WritingMode solo está disponible para la celda.
    
     ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
  
3.  En el panel Propiedades, busque la propiedad WritingMode y cámbiela de **Default** a **Rotate270**.  
  
    Si el panel Propiedades no está abierto, haga clic en la pestaña **Ver** de la cinta de opciones y seleccione **Propiedades**.  
  
4.  Compruebe que la propiedad CanGrow está establecida en **True**.  
  
5.  En la pestaña **Inicio**, sección **Párrafo**, seleccione **Centro** y **Centrar** para colocar el texto en el centro de la celda tanto vertical como horizontalmente.  
 
6. Cambie el tamaño de la columna Territory para que tenga un ancho de 1/2 pulgada y elimine el título de columna.  
6.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
El nombre del territorio se escribe verticalmente, de arriba abajo. El alto del grupo de fila de Territory varía por la longitud del nombre del territorio.  
  
## <a name="next-steps"></a>Pasos siguientes  
Concluye así el tutorial para sobre el modo de crear un informe de matriz. Para obtener más información sobre matrices, consulte: 
-    [Tablas, matrices y listas](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)
-    [Crear una matriz](../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)
-    [Describir las áreas de la región de datos Tablix](../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md) 
-    [Celdas, filas y columnas de la región de datos Tablix](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
[Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)  
[Generador de informes en SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

