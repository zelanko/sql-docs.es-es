---
title: 'Tutorial: Introducción a las expresiones | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79563abac2c6a9ed64dff93667ff3d3966b70bc5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098845"
---
# <a name="tutorial-introducing-expressions"></a>Tutorial: Introducción a las expresiones
  Las expresiones ayudan a crear informes eficaces y flexibles. Este tutorial enseña a crear e implementar expresiones que usen operadores y funciones comunes. Usará el **expresión** cuadro de diálogo para escribir expresiones que concatenan valores de nombres, buscan valores en un conjunto de datos independiente, mostrar diferentes imágenes según los valores de campo y así sucesivamente.  
  
 Se trata de un informe con barras y colores de filas que alternan entre el blanco y un color. El informe incluye un parámetro para seleccionar el color de las filas que no son blancas.  
  
 En la siguiente ilustración se muestra un informe similar al que creará.  
  
 ![rs_ExpressionsTutorial](../../2014/tutorials/media/rs-expressionstutorial.gif "rs_ExpressionsTutorial")  
  
##  <a name="BackToTop"></a> Qué aprenderá  
 En este tutorial, aprenderá a realizar las siguientes tareas:  
  
1.  [Crear un informe de tabla y el conjunto de datos de la tabla o el Asistente para matrices](#Setup)  
  
2.  [Actualizar nombres predeterminados de los datos de origen y conjunto de datos](#UpdateNames)  
  
3.  [Nombre, iniciales y apellido nombre para mostrar](#Concatenate)  
  
4.  [Usar imágenes para mostrar el sexo](#Gender)  
  
5.  [Buscar nombre CountryRegion](#Lookup)  
  
6.  [Recuento de días desde la última compra](#Count)  
  
7.  [Usar un indicador para mostrar la comparación de ventas](#Indicator)  
  
8.  [Hacer que el informe que notificar una "barra verde"](#GreenBar)  
  
### <a name="other-optional-steps"></a>Otros pasos opcionales  
  
-   [Columna de fecha de formato](#DateFormat)  
  
-   [Agregar un título de informe](#Title)  
  
-   [Guardar el informe](#Save)  
  
 Tiempo estimado para completar este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Setup"></a> 1. Crear un informe de tabla y un conjunto de datos con el asistente para tablas o matrices  
 Cree un informe de tabla, un origen de datos y un conjunto de datos. Cuando distribuya la tabla, incluirá solo unos cuantos campos. Después de completar el asistente, agregará manualmente las columnas. El asistente facilita la distribución de la tabla y la aplicación de un estilo.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
> [!NOTE]  
>  En este tutorial, los pasos del asistente se encuentran reunidos en un único procedimiento. Para instrucciones paso a paso sobre cómo desplazarse hasta un servidor de informes, elegir un origen de datos y crear un conjunto de datos, consulte el primer tutorial de esta serie: [Tutorial: Creación de un informe de tabla básico &#40;generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
#### <a name="to-create-a-new-table-report"></a>Para crear un nuevo informe de tabla  
  
1.  Haga clic en **iniciar**, apunte a **programas**, haga clic en [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **Report Builder**y, a continuación, haga clic en **Report Builder**.  
  
     Aparecerá el cuadro de diálogo **Introducción** .  
  
    > [!NOTE]  
    >  Si el **Introducción** no aparece el cuadro de diálogo, desde el **Report Builder** botón, haga clic en **New**.  
  
    > [!NOTE]  
    >  Si prefiere usar la versión ClickOnce del generador de informes, abra el Administrador de informes y haga clic en **Report Builder**, o vaya a un sitio de SharePoint en los servicios de informes de los tipos de contenido como informes están habilitados y haga clic en  **Informe del generador** en el **nuevo documento** menú en el **documentos** pestaña de una biblioteca de documentos compartida.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Elegir una conexión a un origen de datos**, seleccione un origen de datos del tipo **SQL Server**. Seleccione un origen de datos en la lista o vaya al servidor de informes para seleccionar uno.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
9. Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Unknown' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2010-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2010-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2010-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2010-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2010-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2010-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2010-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2010-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2010-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2010-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2010-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2010-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2010-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2010-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2010-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2010-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2010-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    ```  
  
     La consulta especifica los nombres de columna que incluyen una fecha de nacimiento, un nombre, un apellido, el estado o provincia, el identificador de país o región, el sexo y compras anuales.  
  
10. En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar** (**!**). El conjunto de resultados muestra 20 filas de datos e incluye las siguientes columnas: FirstName, LastName, StateProvince, CountryRegionID, Gender, YTDPurchase y LastPurchase.  
  
11. Haga clic en **Siguiente**.  
  
12. En la página **Organizar campos** , arrastre los campos siguientes, en el orden especificado, desde la lista **Campos disponibles** a la lista **Valores** .  
  
    -   StateProvince  
  
    -   CountryRegionID  
  
    -   LastPurchase  
  
    -   YTDPurchase  
  
     Dado que CountryRegionID e YTDPurchase contienen datos numéricos, el agregado SUM se aplica a ellos de forma predeterminada.  
  
    > [!NOTE]  
    >  Los campos FirstName y LastName no están incluidos. Los agregará en un paso posterior.  
  
13. En el **valores** lista, haga clic en `CountryRegionID` y haga clic en el **suma** opción.  
  
     La suma ya no se aplica a CountryRegionID.  
  
14. En la lista **Valores** , haga clic con el botón derecho en **YTDPurchase** y en la opción **Sumar** .  
  
     La suma ya no se aplica a YTDPurchase.  
  
15. Haga clic en **Siguiente**.  
  
16. En la página **Elegir el diseño**, haga clic en **Siguiente**.  
  
17. En el **elegir un estilo** página, haga clic en **Pizarra**y, a continuación, haga clic en **finalizar**.  
  
##  <a name="UpdateNames"></a> 2. Actualizar nombres predeterminados del origen de datos y el conjunto de datos  
  
#### <a name="to-update-the-default-name-of-the-data-source"></a>Para actualizar el nombre predeterminado del origen de datos  
  
1.  En el panel Datos de informe, expanda **Orígenes de datos**.  
  
2.  Haga clic con el botón derecho en **OrigenDeDatos1** y, después, haga clic en **Propiedades del origen de datos.**  
  
3.  En el cuadro **Nombre** , escriba **ExpressionsDataSource**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-update-the-default-name-of-the-dataset"></a>Para actualizar el nombre predeterminado del conjunto de datos  
  
1.  En el panel Datos de informe, expanda **Conjuntos de datos**.  
  
2.  Haga clic con el botón derecho en **ConjuntoDeDatos1** y haga clic en **Propiedades del conjunto de datos.**  
  
3.  En el cuadro **Nombre** , escriba **Expresiones**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Concatenate"></a> 3. Mostrar First Name, Initial y Last Name  
 Use la función **Izquierda** y el operador **Concatenar** (**&**) en una expresión que da como resultado un nombre que incluye una inicial y un apellido. Puede compilar la expresión paso a paso o avanzar en el procedimiento y copiar y pegar la expresión desde el tutorial al cuadro de diálogo **Expresión**.  
  
#### <a name="to-add-the-name-column"></a>Para agregar la columna Nombre  
  
1.  Haga clic con el botón derecho en la columna **StateProvince**, seleccione **Insertar columna** y haga clic en **Izquierda**.  
  
     Se agrega una columna nueva a la izquierda de la columna **StateProvince**.  
  
2.  Haga clic en el título de la nueva columna y escriba **Nombre**  
  
3.  Haga clic con el botón derecho en la celda de datos de la columna **Nombre** y haga clic en **Expresión**.  
  
4.  En el cuadro de diálogo **Expresión** , expanda **Funciones comunes**y haga clic en **Texto**.  
  
5.  En la lista **Elemento** , haga doble clic en **Izquierda**.  
  
     La función **Izquierda** se agrega a la expresión.  
  
6.  En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
7.  En la lista **Valores** , haga doble clic en **FirstName**.  
  
8.  Escriba **, 1)**  
  
     Esta expresión extrae un carácter del valor **FirstName**, contando desde la izquierda.  
  
9. Escriba **&" "&**  
  
10. En la lista **Valores** , haga doble clic en **LastName**.  
  
     La expresión completa es la siguiente: `=Left(Fields!FirstName.Value, 1) &" "& Fields!LastName.Value`  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="Gender"></a> 4. Usar imágenes para mostrar el sexo  
 Use imágenes para mostrar el sexo de una persona e identifique el sexo desconocido usando una tercera imagen. Agregará al informe tres imágenes ocultas y una nueva columna para mostrar las imágenes y después determinará la imagen que aparece en la columna según el valor del campo Gender.  
  
 Para aplicar un color a la celda de la tabla que contiene la imagen, cuando convierta el informe en un informe con barras, agregará un rectángulo y después agregará la imagen al mismo. Tiene que usar un rectángulo porque puede aplicar un color de fondo a un rectángulo, pero no a una imagen.  
  
 El tutorial usa las imágenes que se instalan con Windows, pero puede usar cualquier imagen de que disponga. Usará imágenes incrustadas y no es necesario que estén instaladas en el equipo local ni en el servidor de informes.  
  
#### <a name="to-add-images-to-the-report-body"></a>Para agregar imágenes al cuerpo del informe  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  En la pestaña **Insertar** de la cinta de opciones, haga clic en **Imagen** y, después, haga clic en el cuerpo del informe, debajo de la tabla.  
  
     Se abrirá el cuadro de diálogo **Propiedades de la imagen**.  
  
3.  Haga clic en **Importar** y navegue hasta C:\Users\Public\Public Pictures\Sample Pictures.  
  
4.  Haga clic en Penguins.JPG y en **Abrir**.  
  
     En el cuadro de diálogo **Propiedades de la imagen** haga clic en **Visibilidad** y, después, en la opción **Ocultar**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Repita los pasos 2 a 5, pero elija ahora Koala.JPG.  
  
7.  Repita los pasos 2 a 5, pero elija ahora Tulips.JPG.  
  
#### <a name="to-add-the-gender-column"></a>Para agregar la columna Gender  
  
1.  Haga clic con el botón derecho en la columna **Nombre**, seleccione **Insertar columna** y haga clic en **Derecha**.  
  
     Se agrega una columna nueva a la derecha de la columna **Nombre**.  
  
2.  Haga clic en el título de la nueva columna y escriba **Gender**  
  
#### <a name="to-add-a-rectangle"></a>Para agregar un rectángulo  
  
-   En la pestaña **Insertar** de la cinta de opciones, haga clic en **Rectángulo** y, después, haga clic en la celda de datos de la columna **Gender**.  
  
     Se agregará un rectángulo a la celda.  
  
#### <a name="to-add-an-image-to-the-rectangle"></a>Para agregar una imagen al rectángulo  
  
1.  Haga clic con el botón derecho en el rectángulo, seleccione **Insertar** y haga clic en **Imagen**.  
  
2.  En el cuadro de diálogo **Propiedades de la imagen**, haga clic en la flecha abajo junto a **Usar esta imagen** y seleccione una de las imágenes que agregó, por ejemplo, Penguins.JPG.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-use-images-to-show-gender"></a>Para usar imágenes para mostrar el sexo  
  
1.  Haga clic con el botón derecho en la imagen en la celda de datos de la columna **Gender** y haga clic en **Propiedades de la imagen**.  
  
2.  En el cuadro de diálogo **Propiedades de la imagen** haga clic en el botón **fx** de la expresión junto al cuadro de texto **Usar esta imagen**.  
  
3.  En el cuadro de diálogo **Expresión**, expanda **Funciones comunes** y, después, haga clic en **Flujo de programa**.  
  
4.  En la lista **Elemento** , haga doble clic en **Cambiar**.  
  
5.  En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
6.  En la lista **Valores** , haga doble clic en **Gender**.  
  
7.  Escriba **="Male", "Koala",**  
  
8.  En la lista **Valores** , haga doble clic en **Gender**.  
  
9. Escriba **="Female", "Penguins",**  
  
10. En la lista **Valores**, haga doble clic en **Gender**.  
  
11. Escriba **="Unknown", "Tulips")**  
  
     La expresión completa es la siguiente: `=Switch(Fields!Gender.Value ="Male", "Koala",Fields!Gender.Value ="Female","Penguins",Fields!Gender.Value ="Unknown","Tulips")`  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Haga clic en **Aceptar** de nuevo para cerrar el cuadro de diálogo **Propiedades de la imagen**.  
  
14. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="Lookup"></a> 5. Buscar el nombre CountryRegion  
 Cree el conjunto de datos CountryRegion y use la función **Búsqueda** para mostrar el nombre de un país o región en lugar del identificador del mismo.  
  
#### <a name="to-create-the-countryregion-dataset"></a>Para crear el conjunto de datos CountryRegion  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  En el panel Datos de informe, haga clic en **Nuevo** y, después, en **Conjunto de datos**.  
  
3.  Haga clic en **Usar un conjunto de datos insertado en el informe**.  
  
4.  En la lista **Origen de datos**, seleccione ExpressionsDataSource.  
  
5.  En el cuadro **Nombre** , escriba **CountryRegion**  
  
6.  Compruebe que el tipo de consulta **Texto** está seleccionado y haga clic en **Diseñador de consultas**.  
  
7.  Haga clic en **Editar como texto**.  
  
8.  Copie y pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. Haga clic en **Ejecutar** (**!**) para ejecutar la consulta.  
  
     Los resultados de la consulta son los identificadores del país o región y los nombres.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Haga clic en **Aceptar** de nuevo para cerrar el cuadro de diálogo **Propiedades del conjunto de datos**.  
  
#### <a name="to-look-up-values-in-the-countryregion-dataset"></a>Para buscar valores en el conjunto de datos CountryRegion  
  
1.  Haga clic en el **Country Region ID** título de columna y elimine el texto: ID.  
  
2.  Haga clic con el botón derecho en la celda de datos de la columna **Country Region** y haga clic en **Expresión**.  
  
3.  Elimine la expresión excepto el signo igual (=) inicial.  
  
     El resto de la expresión es: `=`  
  
4.  En el cuadro de diálogo **Expresión**, expanda **Funciones comunes** y, después, haga clic en **Varios**.  
  
5.  En la lista **Elemento**, haga doble clic en **Búsqueda**.  
  
6.  En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
7.  En el **valores** lista, haga doble clic en `CountryRegionID`.  
  
8.  Si el cursor no está ya inmediatamente después de `CountryRegionID.Value`, colóquelo ahí.  
  
9. Elimine el paréntesis de cierre y escriba **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**  
  
     La expresión completa es la siguiente: `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
     La sintaxis de la función **Búsqueda** especifica una búsqueda entre CountryRegionID e ID en el conjunto de datos CountryRegion que devuelve el valor CountryRegion, que también está en el conjunto de datos CountryRegion.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="Count"></a> 6. Recuento de días desde la última compra  
 Agregar una columna y, a continuación, usar el **ahora** función o el `ExecutionTime` variable global integrada para calcular el número de días desde hoy que una persona última compra.  
  
#### <a name="to-add-the-days-ago-column"></a>Para agregar la columna Días transcurridos  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic con el botón derecho en la columna **Last Purchase** , seleccione **Insertar columna**y haga clic en **Derecha**.  
  
     Se agrega una columna nueva a la derecha de la columna **Last Purchase** .  
  
3.  En el encabezado de columna, escriba **Días transcurridos**  
  
4.  Haga clic con el botón derecho en la celda de datos de la columna **Días transcurridos** y haga clic en **Expresión**.  
  
5.  En el cuadro de diálogo **Expresión**, expanda **Funciones comunes** y haga clic en **Fecha y hora**.  
  
6.  En la lista **Elemento**, haga doble clic en **DateDiff**.  
  
7.  Si el cursor no está ya inmediatamente después de `DateDiff(`, colóquelo ahí.  
  
8.  Escriba **"d",**  
  
9. En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
10. En la lista **Valores**, haga doble clic en **LastPurchase**.  
  
11. Si el cursor no está ya inmediatamente después de `Fields!LastPurchase.Value`, colóquelo ahí.  
  
12. Escriba **,**  
  
13. En la lista de **Categoría**, haga clic de nuevo en **Fecha y hora**.  
  
14. En la lista **Elemento**, haga doble clic en **Ahora**.  
  
    > [!WARNING]  
    >  En los informes de producción no debe usar la función **Ahora** en las expresiones que se evalúan varias veces como representadores de informes (por ejemplo, en las filas de detalle de un informe). El valor de **Ahora** cambia de una fila a otra y los diferentes valores afectan a los resultados de evaluación de las expresiones, lo que conduce a resultados ligeramente incoherentes. En su lugar, debe usar la variable global `ExecutionTime` que proporciona [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
15. Si el cursor no está ya inmediatamente después de `Now(`, colóquelo ahí.  
  
16. Elimine el paréntesis de apertura y escriba **)**  
  
     La expresión completa es la siguiente: `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Indicator"></a> 7. Usar un indicador para mostrar la comparación de ventas  
 Agregue una nueva columna y usar un indicador para mostrar si una persona año hasta la fecha (año actual) están por encima o por debajo del promedio de que compras hasta la fecha. La función **Redondear** quita los decimales de los valores.  
  
 La configuración del indicador y sus estados requiere muchos pasos. Si lo desea, en el procedimiento "para configurar el indicador", puede avanzar y copiar y pegar las expresiones completas de este tutorial en el **expresión** cuadro de diálogo.  
  
#### <a name="to-add-the--or---avg-sales-column"></a>Para agregar la columna Promedio + o -  
  
1.  Haga clic con el botón derecho en la columna **YTD Purchase** , seleccione **Insertar columna**y haga clic en **Derecha**.  
  
     Se agrega una columna nueva a la derecha de la columna **YTD Purchase**.  
  
2.  Haga clic en el título de la columna y escriba **Ventas promedio + o -**  
  
#### <a name="to-add-an-indicator"></a>Para agregar un indicador  
  
1.  En la pestaña **Insertar** de la cinta de opciones, haga clic en **Indicador** y, después, haga clic en la celda de datos de la columna **Ventas promedio + o -**.  
  
     Se abrirá el cuadro de diálogo **Seleccionar tipo de indicador**.  
  
2.  En el grupo **Direccional** de los conjuntos de iconos, haga clic en el conjunto de tres flechas grises.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-configure-the-indicator"></a>Para configurar el indicador  
  
1.  Haga clic con el botón derecho en el indicador, haga clic en **Propiedades de indicador**y, después, en **Valor y estados**.  
  
2.  Haga clic en el botón de expresión **fx** situado junto al cuadro de texto **Valor** .  
  
3.  En el cuadro de diálogo **Expresión** , expanda **Funciones comunes**y haga clic en **Matemáticas**.  
  
4.  En la lista **Elemento**, haga doble clic en **Redondear**.  
  
5.  En la lista **Categoría**, haga clic en **Campos (Expresiones)**.  
  
6.  En la lista **Valores**, haga doble clic en **YTDPurchase**.  
  
7.  Si el cursor no está ya inmediatamente después de `Fields!YTDPurchase.Value`, colóquelo ahí.  
  
8.  Escriba **-**  
  
9. Expanda **Funciones comunes** de nuevo y haga clic en **Agregado**.  
  
10. En la lista **Elemento**, haga doble clic en **Promedio**.  
  
11. En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
12. En la lista **Valores**, haga doble clic en **YTDPurchase**.  
  
13. Si el cursor no está ya inmediatamente después de `Fields!YTDPurchase.Value`, colóquelo ahí.  
  
14. Escriba **, "Expressions"))**  
  
     La expresión completa es la siguiente: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. En el cuadro **Unidad de medida de estados** , seleccione **Numérico**.  
  
17. En la fila con la flecha hacia abajo, haga clic en el botón **fx** a la derecha del cuadro de texto del valor **Inicio**.  
  
18. En el cuadro de diálogo **Expresión**, expanda **Funciones comunes** y haga clic en **Matemáticas**.  
  
19. En la lista **Elemento**, haga doble clic en **Redondear**.  
  
20. En la lista **Categoría**, haga clic en **Campos (Expresiones)**.  
  
21. En la lista **Valores**, haga doble clic en **YTDPurchase**.  
  
22. Si el cursor no está ya inmediatamente después de `Fields!YTDPurchase.Value`, colóquelo ahí.  
  
23. Escriba **-**  
  
24. Expanda **Funciones comunes** de nuevo y haga clic en **Agregado**.  
  
25. En la lista **Elemento**, haga doble clic en **Promedio**.  
  
26. En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
27. En la lista **Valores**, haga doble clic en **YTDPurchase**.  
  
28. Si el cursor no está ya inmediatamente después de `Fields!YTDPurchase.Value`, colóquelo ahí.  
  
29. Escriba **, "Expressions")) < 0**  
  
     La expresión completa es la siguiente: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. En el cuadro de texto del valor **Final** , escriba **0**  
  
32. Haga clic en la fila con la flecha horizontal y haga clic en **Eliminar**.  
  
33. En la fila con la flecha hacia arriba, en el cuadro **Inicio**, escriba **0**  
  
34. Haga clic en el botón **fx** a la derecha del cuadro de texto del valor **Final** .  
  
35. En el **expresión** diálogo cuadro, cree la expresión: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. Haga clic en **Aceptar** de nuevo para cerrar el cuadro de diálogo **Propiedades de indicador** .  
  
38. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="GreenBar"></a> 8. Hacer que el informe que notificar una "barra verde"  
 Use un parámetro para especificar el color que se aplicará a filas alternativas del informe, convirtiéndolo en un informe con barras.  
  
#### <a name="to-add-a-parameter"></a>Para agregar un parámetro  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  En el panel **Datos de informe**, haga clic con el botón derecho en **Parámetros** y haga clic en **Agregar parámetro**.  
  
     Se abrirá el cuadro de diálogo **Propiedades de parámetro de informe** .  
  
3.  En **Pedir datos**, escriba **Elegir color**  
  
4.  En **Nombre**, escriba **RowColor**  
  
5.  En el panel izquierdo, haga clic en **Valores disponibles**.  
  
6.  Haga clic en **Especificar valores**.  
  
7.  Haga clic en **Agregar**.  
  
8.  En el **etiqueta** , escriba: **Amarillo**  
  
9. En el cuadro **Valor** , escriba **Amarillo**  
  
10. Haga clic en **Agregar**.  
  
11. En el cuadro **Etiqueta** , escriba **Verde**  
  
12. En el cuadro **Valor** , escriba **VerdePálido**  
  
13. Haga clic en **Agregar**.  
  
14. En el cuadro **Etiqueta** , escriba **Azul**  
  
15. En el cuadro **Valor** , escriba **AzulClaro**  
  
16. Haga clic en **Agregar**.  
  
17. En el cuadro **Etiqueta** , escriba **Rosa**  
  
18. En el cuadro **Valor** , escriba **Rosa**  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-apply-alternating-colors-to-detail-rows"></a>Para aplicar colores alternativos a las filas de detalle.  
  
1.  Haga clic en la pestaña **Vista** de la cinta de opciones y compruebe que está seleccionado **Propiedades**.  
  
2.  Haga clic en la celda de datos de la columna **Nombre** y pulse la tecla Mayús.  
  
3.  Una a una, haga clic en el resto de celdas de la fila.  
  
4.  En el panel Propiedades, haga clic en **BackgroundColor**.  
  
     Si en el panel Propiedades se muestran las propiedades según la categoría, encontrará **BackgroundColor** en la categoría **Relleno**.  
  
5.  Haga clic en la flecha hacia abajo y, después, en **Expresión**.  
  
6.  En el cuadro de diálogo **Expresión**, expanda **Funciones comunes** y, después, haga clic en **Flujo de programa**.  
  
7.  En la lista **Elemento**, haga doble clic en **SiInm**.  
  
8.  Expanda **Funciones comunes** y haga clic en **Agregado**.  
  
9. En la lista **Elemento**, haga doble clic en **RunningValue**.  
  
10. En la lista **Categoría** , haga clic en **Campos (Expresiones)**.  
  
11. En la lista **Valores**, haga doble clic en **FirstName**.  
  
12. Si el cursor no está ya inmediatamente después de `Fields!FirstName.Value`, colóquelo ahí y escriba **,**  
  
13. Expanda **Funciones comunes** y haga clic en **Agregado**.  
  
14. En la lista **Elemento**, haga doble clic en **Recuento**.  
  
15. Si el cursor no está ya inmediatamente después de `Count(`, colóquelo ahí.  
  
16. Elimine el paréntesis de apertura y, a continuación, escriba **, "Expressions")**  
  
    > [!NOTE]  
    >  Expressions es el nombre del conjunto de datos en el que contabilizar las filas de datos.  
  
17. Expanda **Operadores** y haga clic en **Aritméticos**.  
  
18. En la lista **Elemento**, haga doble clic en **Resto**.  
  
19. Si el cursor no está ya inmediatamente después de `Mod`, colóquelo ahí.  
  
20. Escriba **2 =0,**  
  
    > [!IMPORTANT]  
    >  Asegúrese de incluir un espacio antes de escribir el número 2.  
  
21. Haga clic en **Parámetros** y en la lista **Valores**, haga doble clic en **RowColor**.  
  
22. Si el cursor no está ya inmediatamente después de `Parameters!RowColor.Value`, colóquelo ahí.  
  
23. Escriba **, "White")**  
  
     La expresión completa es la siguiente: `=IIf(RunningValue(Fields!FirstName.Value,Count, "Expressions") Mod 2 =0, Parameters!RowColor.Value, "White")`  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="run-the-report"></a>Ejecutar el informe  
  
1.  Si no está en la pestaña **Inicio**, haga clic en **Inicio** para volver a la vista de diseño.  
  
2.  Haga clic en **Ejecutar**.  
  
3.  En la lista desplegable **Elegir color**, seleccione el color de las barras que no son blancas del informe.  
  
4.  Haga clic en **Ver informe**.  
  
     Los representadores de informes y las filas alternativas tienen el fondo que elija.  
  
##  <a name="DateFormat"></a> (opcional) Columna de fecha de formato  
 Dé formato a la columna **Last Purchase**, que contiene fechas.  
  
#### <a name="to-format-date-column"></a>Para dar formato a la columna de fecha  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic con el botón derecho en la celda de datos de **Última compra** y haga clic en **Propiedades de cuadro de texto**.  
  
3.  En el cuadro de diálogo **Propiedades de cuadro de texto** haga clic en **Número**, haga clic en **Fecha**, y, después, en el tipo **\*31/1/2000**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Title"></a> (opcional) Agregar un título de informe  
 Agregue un título al informe.  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Resumen de comparación de ventas** y, después, haga clic fuera del cuadro de texto.  
  
3.  Haga clic con el botón derecho en el cuadro de texto que contiene **Resumen de comparación de ventas** y haga clic en **Propiedades de cuadro de texto**.  
  
4.  En el cuadro de diálogo **Propiedades de cuadro de texto**, haga clic en **Fuente**.  
  
5.  En la lista **Tamaño**, seleccione **18pt**.  
  
6.  En la lista **Color**, seleccione **Gris**.  
  
7.  Seleccione **Negrita** y **Cursiva**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> (opcional) Guardar el informe  
 Puede guardar los informes en un servidor de informes, en una biblioteca de SharePoint o en su equipo. Para obtener más información, consulte [Guardar informes &#40;Generador de informes&#41;](report-builder/saving-reports-report-builder.md).  
  
 En este tutorial, guarde el informe en un servidor de informes. Si no tiene acceso a un servidor de informes, guarde el informe en su equipo.  
  
#### <a name="to-save-the-report-to-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
     Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, verá el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **Resumen de comparación de ventas**.  
  
5.  Haga clic en **Guardar**.  
  
 El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
#### <a name="to-save-the-report-to-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde desea guardar el informe.  
  
3.  En **Nombre**, reemplace el nombre predeterminado por **Resumen de comparación de ventas**.  
  
4.  Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Los indicadores &#40;generador de informes y SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)   
 [Imágenes, cuadros de texto, rectángulos y líneas &#40;Generador de informes y SSRS&#41;](report-design/rectangles-and-lines-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
