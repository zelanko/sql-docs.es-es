---
title: 'Tutorial: Crear un informe de matriz (generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86bffd9c3cf98732da253e511287a9c9e722f4a7
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033126"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>Tutorial: Crear un informe de matriz (generador de informes)
  Este tutorial enseña a crear un informe de matriz básico de acuerdo con los datos de ventas de ejemplo. La matriz ha anidado en grupos de filas y de columnas, así como en un grupos de columnas adyacente. También aprenderá a dar formato a las columnas y a girar el texto. En la siguiente ilustración se muestra un informe similar al que creará.  
  
 ![rs_CreateMatixReportTutorial](../../2014/tutorials/media/rs-creatematixreporttutorial.gif "rs_CreateMatixReportTutorial")  
  
 Una versión mejorada del informe que creará en este tutorial está disponible como ejemplo en el informe del Generador de informes de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obtener más información acerca de cómo descargar este ejemplo y otros informes, vea [informe del generador de informes de ejemplo](https://go.microsoft.com/fwlink/?LinkId=184851).  
  
##  <a name="BackToTop"></a> Qué aprenderá  
 En este tutorial, aprenderá a:  
  
1.  [Crear un informe de matriz y un conjunto de datos de la nueva tabla o el Asistente para matrices](#CreateMatrix)  
  
2.  [Organizar datos y elegir el diseño y estilo de la nueva tabla o el Asistente para matrices](#Groups)  
  
3.  [Formato de datos](#FormatData)  
  
4.  [Agregar grupo de columnas adyacente](#AdjacentGroup)  
  
5.  [Cambiar el ancho de columna](#Width)  
  
6.  [Combinar celdas de la matriz](#MergeCells)  
  
7.  [Agregar un encabezado de informe y el título del informe](#HeaderTitle)  
  
8.  [Guardar el informe](#Save)  
  
### <a name="other-optional-step"></a>Otro paso opcional  
  
1.  [Girar texto 270 grados el cuadro](#RotateTextBox)  
  
 Tiempo estimado para completar este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="CreateMatrix"></a> 1. Crear un informe de matriz y un conjunto de datos desde el nuevo Asistente para tablas o matrices  
 Desde el **Introducción** cuadro de diálogo Generador de informes, elija un origen de datos compartido, crear un conjunto de datos incrustado y, a continuación, muestre los datos de una matriz.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene ya los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-create-a-new-matrix"></a>Para crear una nueva matriz  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
    > [!NOTE]  
    >  Debería aparecer el cuadro de diálogo **Introducción** . Si no es así, en el botón Generador de informes, haga clic en **New**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y, a continuación, seleccione un origen de datos. Si no hay disponible ningún origen de datos o no tiene acceso a un servidor de informes, puede utilizar un origen de datos incrustados en su lugar. Para obtener más información acerca de cómo crear un origen de datos incrustados, vea [Tutorial: Creación de un informe de tabla básico &#40;generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
9. Copie y pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. Haga clic en **Siguiente**.  
  
##  <a name="Groups"></a> 2. Organizar datos y elegir el diseño y el estilo desde el nuevo Asistente para tablas o matrices  
 Utilice el asistente para proporcionar un diseño inicial en el que mostrar los datos. El panel de vista previa del asistente le ayudará a visualizar el resultado de las agrupaciones de datos antes de completar el diseño de la matriz.  
  
#### <a name="to-organize-data-into-groups-and-choose-a-layout-and-style"></a>Para organizar los datos en grupos y elegir un diseño y un estilo  
  
1.  En la página **Organizar campos** , arrastre Territory desde **Campos disponibles** a **Grupos de filas**.  
  
2.  Arrastre SalesDate hasta **Grupos de filas** y colóquelo debajo de Territory.  
  
     El orden en el que se enumeran los campos en **Grupos de filas** define la jerarquía de grupos. Los pasos 1 y 2 organizan los valores de los campos primero por territorio y, después, por la fecha de las ventas.  
  
3.  Arrastre Subcategory a **Grupos de columnas**.  
  
4.  Arrastre Product hasta **grupos de columnas,** y, a continuación, coloque abajo Subcategory.  
  
     El orden en el que se enumeran los campos en **grupos de columnas** define la jerarquía de grupos.  
  
     Los pasos 3 y 4 organizan los valores de los campos primero por subcategoría y, después, por producto.  
  
5.  Arrastre Sales a **Valores**.  
  
     El campo Sales se resume con la función Sum, que es la función predeterminada para resumir campos numéricos.  
  
6.  Arrastre Quantity a **Valores**.  
  
     El campo Quantity se resume con la función Sum.  
  
     Los pasos 5 y 6 especifican los datos que deben mostrarse en las celdas de datos de la matriz.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página Elegir el diseño, en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
9. Compruebe que esté seleccionada la opción **Bloqueado, subtotal abajo** .  
  
10. Compruebe que la opción **Expandir o contraer grupos** está seleccionada.  
  
11. Haga clic en **Siguiente**.  
  
12. En la página Elegir un estilo, en el panel Estilos, seleccione **Pizarra**.  
  
13. Haga clic en **Finalizar**.  
  
     La matriz se agrega a la superficie de diseño. El panel de grupos de filas muestra dos grupos de filas: Territory y SalesDate. El panel de grupos de columnas muestra dos grupos de columnas: Subcategoría y producto. Los datos detallados son todos los datos recuperados por la consulta del conjunto de datos.  
  
14. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 Para cada producto que se vende en una fecha concreta, la matriz muestra la subcategoría a la que pertenece el producto y el territorio de las ventas.  
  
##  <a name="FormatData"></a> 3. Dar formato a datos  
 De forma predeterminada, los datos de resumen para el campo Sales muestran un número general y el campo SalesDate muestra información de fecha y de hora. Dé formato al campo Sales para mostrar el número como moneda y el campo SalesDate para mostrar solo la fecha. Alterne **Estilos de marcador de posición** para mostrar los cuadros de texto con formato y el texto de marcador de posición como valores de ejemplo.  
  
#### <a name="to-format-fields"></a>Para dar formato a los campos  
  
1.  Haga clic en **Diseño** para cambiar a la vista de diseño.  
  
2.  Presione la tecla CTRL y, a continuación, seleccione las nueve celdas que contienen `[Sum(Sales)]`.  
  
3.  En la pestaña **Inicio** , en el grupo **Número** , haga clic en el botón **Moneda**. Las celdas cambian para mostrar la moneda con formato.  
  
     Si la configuración regional es Inglés (Estados Unidos), el texto de ejemplo predeterminado es [**$12,345.00**]. Si no ve un valor de moneda de ejemplo, haga clic en **estilos de marcador de posición** en el **números** de grupo y, a continuación, haga clic en **valores de ejemplo**.  
  
4.  Haga clic en la celda que contiene `[SalesDate]`.  
  
5.  En el **número** grupo, en la lista desplegable, seleccione **fecha**.  
  
     La celda muestra la fecha de ejemplo **[1/31/2000]**. Si no ve un valor de fecha de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** y, después, haga clic en **Valores de ejemplo**.  
  
6.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 Los valores de fecha solo muestran fechas y los valores de ventas se muestran como moneda.  
  
##  <a name="AdjacentGroup"></a> 4. Agregar grupo de columnas adyacente  
 Puede anidar grupos de filas y de columnas en relaciones de elemento primarias o adyacentes en relaciones del mismo nivel.  
  
 Agregue un grupo de columnas que es adyacente al grupo de columnas de Subcategory, copie las celdas para rellenar el nuevo grupo de columnas y, a continuación, utilice una expresión para crear el valor del encabezado de grupo de columnas.  
  
#### <a name="to-add-an-adjacent-column-group"></a>Para agregar un grupo de columnas adyacente  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic con el botón derecho en la celda que contiene `[Subcategory]`, señale **Agregar grupo**y luego haga clic en **Adyacente a la derecha**.  
  
     Se abre el cuadro de diálogo **Grupo de Tablix** .  
  
3.  En la lista **Agrupar por** , seleccione SalesDate y, después, haga clic en **Aceptar**.  
  
     Un nuevo grupo de columnas se agrega a la izquierda del grupo de columnas de Subcategory.  
  
4.  Haga clic con el botón derecho en la celda del nuevo grupo de columnas que contiene `[SalesDate],` y luego haga clic en **Expresión**.  
  
5.  Copie la siguiente expresión en el cuadro de diálogo de expresión.  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
     Esta expresión extrae el nombre del día de la semana de la fecha de ventas. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md).  
  
6.  Haga clic con el botón derecho en la celda del grupo de columnas de Subcategory que contiene Total y luego haga clic en **Copiar**.  
  
7.  Haga clic con el botón derecho en la celda situada inmediatamente debajo de la celda que contiene la expresión que ha creado en el paso 5 y haga clic en **Pegar**.  
  
8.  Presione la tecla CTRL.  
  
9. En el grupo Subcategory, haga clic en el encabezado de columna Sales y las tres celdas debajo de él, haga clic con el botón derecho y, después, haga clic en **Copiar**.  
  
10. Pegue las cuatro celdas en las cuatro celdas vacías en el nuevo grupo de columnas.  
  
11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El informe incluye columnas denominadas Monday y Tuesday. El conjunto de datos solo contiene los datos de estos dos días.  
  
> [!NOTE]  
>  Si los datos incluyeran otros días, el informe también incluiría las columnas correspondientes. Cada columna tiene el encabezado de columna, `Sales`y los totales de ventas por territorio.  
  
##  <a name="Width"></a> 5. Cambiar el ancho de columna  
 Un informe que incluye una matriz normalmente se expande horizontalmente así como verticalmente cuando se ejecuta. Controlar la expansión horizontal es particularmente importante si piensa exportar el informe a los formatos como Microsoft Word o Adobe PDF, que se utilizan para los informes impresos. Si el informe se expande horizontalmente por varias páginas, el informe impreso es difícil de entender. Para minimizar la expansión horizontal, puede cambiar el tamaño de las columnas para que tengan solo el ancho necesario para mostrar los datos sin ajustar. También puede cambiar el nombre de las columnas para que sus títulos con el ancho necesario para mostrar los datos.  
  
#### <a name="to-rename-and-resize-the-columns"></a>Cambiar el nombre y el tamaño de las columnas  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Seleccione el texto de la columna Quantity situada más a la izquierda y, después, escriba **QTY**.  
  
     El título de la columna es ahora QTY.  
  
3.  Repita el paso 2 en las otras columnas denominadas Quantity. Hay dos de ellas.  
  
4.  Haga clic en la matriz para que los identificadores de columna y de fila aparezcan encima y al lado de la matriz.  
  
     Las barras grises situadas en la parte superior y en el lado de la tabla son los identificadores de fila y de columna.  
  
5.  Para cambiar el tamaño de la columna QTY situada más a la izquierda, seleccione la línea entre los identificadores de columna para que el cursor cambie a una flecha doble. Arrastre la columna hacia la izquierda hasta que el ancho sea de 1/2 pulgada.  
  
     Un ancho de columna de 1/2 pulgada es adecuado para mostrar la cantidad.  
  
6.  Repita el paso 5 en las otras columnas denominadas QTY.  
  
7.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 Las columnas del informe que contiene las cantidades se denominan ahora QTY y son más estrechas.  
  
##  <a name="MergeCells"></a> 6. Combinar las celdas de la matriz  
 El área de la esquina está en la esquina superior izquierda de la matriz Dependiendo del número de grupos de filas y columnas de la matriz, el número de celdas en el área de la esquina varía. La matriz generada en este tutorial tiene cuatro celdas en su área de esquina. Las celdas se disponen en dos filas y dos columnas, reflejando la profundidad de las jerarquías de grupos de filas y columnas. Las cuatro celdas no se utilizan en este informe y los combinará en una.  
  
#### <a name="to-merge-matrix-cells"></a>Para combinar las celdas de la matriz  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la matriz para que los identificadores de columna y de fila aparezcan encima y al lado de la matriz.  
  
3.  Presione la tecla CTRL y, a continuación, seleccione las cuatro celdas de la esquina.  
  
4.  Haga clic en las celdas y, a continuación, haga clic en **combinar celdas**.  
  
5.  Haga clic en la celda de esquina y, a continuación, haga clic en **propiedades de cuadro de texto**.  
  
6.  Haga clic en la pestaña **Rellenar** .  
  
7.  Haga clic en el (***fx***) botón **color de relleno**.  
  
8.  Copie y pegue la expresión siguiente en el cuadro de diálogo de expresión.  
  
    ```  
    #96a4b2  
    ```  
  
     Es el valor hexadecimal de RGB para un color del azul deshabilitado utilizado en el estilo Pizarra.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 La matriz de la esquina superior es una celda única y tiene el mismo color que las celdas del grupo de filas y columnas.  
  
##  <a name="HeaderTitle"></a> 7. Agregar un encabezado y un título del informe  
 Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. En este tutorial, quitará el cuadro de texto de la parte superior del informe y agregará un título al encabezado.  
  
#### <a name="to-add-a-report-header-and-report-title"></a>Para agregar un encabezado y un título del informe  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en el cuadro de texto en la parte superior del cuerpo del informe que contiene **haga clic aquí para agregar un título**y, a continuación, presione la tecla SUPR.  
  
3.  En el **insertar** pestaña de la cinta de opciones, haga clic en **encabezado** y, a continuación, haga clic en **agregar encabezado**.  
  
     Se agrega un encabezado a la parte superior del cuerpo del informe.  
  
4.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**y luego arrastre un cuadro de texto al encabezado del informe. Haga un cuadro de texto de aproximadamente 6 pulgadas de largo y 3/4 de pulgada de alto, y colóquelo en el lado izquierdo del encabezado del informe.  
  
5.  En el cuadro de texto, escriba **Ventas por territorio, Subcategoría y Día**.  
  
6.  Seleccione el texto que escribió, con el botón secundario y, a continuación, haga clic en **propiedades de texto**.  
  
    > [!NOTE]  
    >  Para dar formato al mismo tiempo a los caracteres, deben ser contiguos.  
  
7.  En el **propiedades de texto** cuadro de diálogo, haga clic en **fuente**.  
  
8.  En el **fuente** lista, seleccione **Times New Roman**; en **tamaño** seleccione **24 pt**, en **Color** seleccione  **Granate**y en **estilo** seleccione **cursiva**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El informe incluye un título de informe en el encabezado del informe.  
  
##  <a name="Save"></a> 8. Guardar el informe  
 Puede guardar los informes en un servidor de informes, en una biblioteca de SharePoint o en su equipo.  
  
 En este tutorial, guarde el informe en un servidor de informes. Si no tiene acceso a un servidor de informes, guarde el informe en su equipo.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
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
  
##  <a name="RotateTextBox"></a> 9. (Opcional) Girar 270 grados el cuadro de texto  
 Un informe con matrices se puede expandir horizontal y verticalmente cuando se ejecuta. Girando los cuadros de texto verticalmente o 270 grados, puede ahorrar espacio horizontal. El informe representado se hace más estrecho y, si se exporta a un formato como Microsoft Word, tendrá más posibilidades de ajustar en una página impresa.  
  
 Un cuadro de texto también puede mostrar el texto como horizontal o como, vertical (de arriba abajo). Para más información, vea [Cuadros de texto &#40;Generador de informes y SSRS&#41;](report-design/text-boxes-report-builder-and-ssrs.md).  
  
#### <a name="to-rotate-text-box-270-degrees"></a>Para girar el cuadro de texto 270 grados  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la celda que contiene `[Territory].`.  
  
3.  En el panel Propiedades, busque la propiedad WritingMode y en su lista desplegable, seleccione **Rotate270**.  
  
     Si el panel Propiedades no está abierto, haga clic en la pestaña **Ver** de la cinta de opciones y seleccione **Propiedades**.  
  
4.  Compruebe que la propiedad CanGrow está establecida en `True`.  
  
5.  Cambie el tamaño de la columna Territory para que tenga un ancho de 1/2 pulgada y elimine el título de columna.  
  
6.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 El nombre del territorio se escribe verticalmente, de arriba abajo. El alto del grupo de fila de Territory varía por la longitud del nombre del territorio.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Concluye así el tutorial para sobre el modo de crear un informe de matriz. Para obtener más información sobre matrices, vea [tablas, Matrices y listas &#40;generador de informes y SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md), [Matrices &#40;generador de informes y SSRS&#41;](report-design/create-a-matrix-report-builder-and-ssrs.md), [ Áreas de la región de datos Tablix &#40;generador de informes y SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md), y [columnas, filas y celdas de la región de datos Tablix &#40;generador de informes&#41; y SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
