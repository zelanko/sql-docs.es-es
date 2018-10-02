---
title: 'Tutorial: Dar formato a texto (Generador de informes) | Microsoft Docs'
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1c1af1b9b6e1e9f78469522a90cf589f484f2964
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741513"
---
# <a name="tutorial-format-text-report-builder"></a>Tutorial: Dar formato a texto (Generador de informes)

En este tutorial, puede practicar el proceso de dar formato al texto de varias maneras en un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . Puede experimentar con diferentes formatos. 

Después de configurar el informe en blanco con el origen de datos y el conjunto de datos, puede elegir los formatos que quiere explorar. En la siguiente ilustración se muestra un informe similar al que creará.  
  
![informe-generar-formato-informe](../reporting-services/media/report-build-format-report.png) 
  
En un paso puede cometer un error voluntario para ver por qué es un error. A continuación, corrija el error para lograr el efecto deseado.  
    
Tiempo estimado para completar este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="CreateReport"></a>Crear un Informe en blanco con un origen de datos y un conjunto de datos  
  
### <a name="to-create-a-blank-report"></a>Para crear un informe en blanco  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
 
2.  En el panel izquierdo del cuadro de diálogo **Introducción** , compruebe que **Nuevo informe** está seleccionado.  
  
3.  En el panel derecho, haga clic en **Informe en blanco**.  
  
### <a name="to-create-a-data-source"></a>Para crear un origen de datos  
  
1.  En el panel Datos de informe, haga clic en **Nuevo** > **Origen de datos**.  

    Si no ve el panel **Datos de informe** , en la pestaña **Ver** haga clic en **Datos de informe**.
  
2.  En el cuadro **Nombre** , escriba: **TextDataSource**  
  
3.  Haga clic en **Usar una conexión incrustada en mi informe**.  
  
4.  Compruebe que el tipo de conexión sea Microsoft SQL Server y, luego, en el cuadro **Cadena de conexión** , escriba: `Data Source = <servername>`  
  
    > [!NOTE]  
    > La expresión `<servername>`, por ejemplo Report001, especifica un equipo en el que se ha instalado una instancia del motor de SQL Server Database. Para este tutorial no se necesitan datos concretos, solo una conexión a una base de datos de SQL Server. Si ya tiene una conexión a un origen de datos enumerada bajo **Conexiones de origen de datos**, puede seleccionarla e ir al procedimiento siguiente, "Para crear un conjunto de datos". Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-dataset"></a>Para crear un conjunto de datos  
  
1.  En el panel Datos de informe, haga clic en **Nuevo** > **Conjunto de datos**.  
  
2.  Compruebe que el origen de datos es **TextDataSource**.  
  
3.  En el cuadro **Nombre** , escriba: **TextDataset.**  
  
4.  Compruebe que el tipo de consulta **Texto** está seleccionado, y, a continuación, haga clic en **Diseñador de consultas**.  
  
5.  Haga clic en **Editar como texto**.  
  
6.  Pegue la siguiente consulta en el panel de consulta:  

    > [!NOTE]  
    > En este tutorial, la consulta contiene ya los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Install Report Builder' as LinkText, 'http://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Report Builder in SQL Server' as Link, 'http://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Reporting Services (SSRS)' as Link, 'http://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  Haga clic en Ejecutar (**!**) para ejecutar la consulta.  
  
    Los resultados de la consulta son los datos disponibles para mostrarse en su informe.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

9.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="AddField"></a>Agregar un campo a la superficie de diseño del informe  
Si desea que un campo del conjunto de datos aparezca en un informe, su primer impulso puede ser arrastrarlo hasta la superficie de diseño directamente. En este ejercicio se describe por qué eso no funciona y lo que se ha de hacer en su lugar.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>Para agregar un campo al informe (y obtener el resultado incorrecto)  
  
1.  Arrastre el campo **FullName** desde el panel Datos de informe hasta la superficie de diseño.  
  
    El Generador de informes crea un cuadro de texto con una expresión en él, representada como `<Expr>`.  
  
2.  Haga clic en **Ejecutar**.  
  
    Observe que solo hay un registro, **Fernando Ross**, que es alfabéticamente el primer registro en la consulta. El campo no se repite para mostrar los otros registros de ese campo.  
  
3.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
4.  Seleccione la expresión `<Expr>` en el cuadro de texto.  
  
5.  En el panel Propiedades, para la propiedad **Value** verá lo siguiente (si no ve el panel Propiedades, en la pestaña **Ver** active **Propiedades**):  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
    La función `First` está diseñada para recuperar solo el primer valor de un campo y es lo que ha hecho.  
  
    Al arrastrar el campo hacia la superficie de diseño directamente, se creó un cuadro de texto. Por sí mismos, los cuadros de texto no son regiones de datos, de modo que no muestran datos de un conjunto de datos de informe. Los cuadros de texto de las regiones de datos, como tablas, matrices y listas, muestran datos.  
  
6.  Seleccione el cuadro de texto (si tiene la expresión seleccionada, presione ESC para seleccionarlo) y presione la tecla SUPRIMIR.  
  
### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>Para agregar un campo al informe (y obtener el resultado correcto)  
  
1.  En la pestaña **Insertar** de la cinta de opciones, en el área **Regiones de datos** , haga clic en **Lista**. Haga clic en la superficie de diseño y, a continuación, arrástrela para crear un cuadro que tenga aproximadamente dos pulgadas de ancho y una de alto.  
  
2.  Arrastre el campo **FullName** desde el panel Datos de informe hasta el cuadro de lista.  
  
    Esta vez el Generador de informes crea un cuadro de texto con la expresión `[FullName]` en él.  
  
3.  Haga clic en **Ejecutar**.  
  
    Tenga en cuenta que esta vez el cuadro se repite para mostrar todos los registros de la consulta.  
  
4.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
5.  Seleccione la expresión en el cuadro de texto.  
  
6.  En el panel Propiedades, para la propiedad **Value** , ve lo siguiente:  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
    Arrastrando el cuadro de texto hasta la región de datos de la lista, muestra los datos que hay en ese campo del conjunto de datos.  
  
7.  Seleccione el cuadro de lista y presione la tecla ELIMINAR.  
  
## <a name="AddTable"></a>Agregar un tabla a la superficie de diseño del informe  
Cree esta tabla para tener un lugar donde colocar los hipervínculos y el texto girado.   
  
1.  En la pestaña **Insertar** > **Tabla** > **Asistente para tablas**.  
  
2.  En la página **Elegir un conjunto de datos** del nuevo Asistente para tablas o matrices, haga clic en **Elegir un conjunto de datos existente en este informe o un conjunto de datos compartido** > **TextDataset (en este Informe)** > **Siguiente**.  
  
3.  En la página **Organizar campos** , arrastre los campos **Territory**, **LinkText**y **Product** hasta **Grupos de filas**, arrastre el campo **Sales** hasta **Valores**y después haga clic en **Siguiente**.  

    ![generador-de-informes-organizar-campos-de-texto](../reporting-services/media/report-builder-text-arrange-fields.png)
  
4.  En la página **Elegir el diseño** , desactive la casilla **Expandir o contraer grupos** de modo que pueda ver la tabla entera, y,después, haga clic en **Siguiente**. 
  
5.  Haga clic en **Finalizar**.  
  
6.  Haga clic en **Ejecutar**.  
  
    La tabla parece correcta, pero tiene dos filas con el título Total. La columna **LinkText** no necesita una fila Total.  
    
    ![generador-de-informes-formato-2-totales](../reporting-services/media/report-builder-format-2-totals.png)
  
8.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
9. Seleccione la celda **Total** de la columna **LinkText** y, después, mantenga presionada la tecla MAYÚS y seleccione las dos celdas a su derecha: la celda vacía de la columna **Product** y la celda `[Sum(Sales)]` de la columna **Sales** .  
  
11. Con esas tres celdas seleccionadas, haga clic con el botón secundario en uno de esas celdas y haga clic en **Eliminar filas**.  

    ![generador-de-informes-formato-eliminar-filas](../reporting-services/media/report-builder-format-delete-rows.png)
  
12. Haga clic en **Ejecutar**.  

    Ahora tiene una única fila Total.
    
    ![generador-de-informes-formato-un-total](../reporting-services/media/report-builder-format-one-total.png)
  
## <a name="AddHyperlink"></a>Agregar un hipervínculo al informe  
En esta sección, agrega un hipervínculo al texto de la tabla desde la sección anterior.  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic con el botón secundario en la celda que contiene `[LinkText]`y haga clic en **Propiedades de cuadro de texto**.  
  
3.  En la pestaña **Acción** , haga clic en **Ir a dirección URL**.  
  
5.  En el cuadro **Seleccionar dirección URL** , haga clic en **[URL]** y después en **Aceptar**.  
  
6.  Observe que el texto no parece diferente. Necesita que se parezca al texto del vínculo.  
  
7.  Seleccione `[LinkText]`.  
  
8.  En la pestaña **Inicio** > **Fuente**, seleccione **Subrayado** y cambie **Color** a **Azul**.  
  
9. Haga clic en **Ejecutar**.  
  
    Ahora el texto parece un vínculo.  
    
    ![generador-de-informes-formato-hipervínculo](../reporting-services/media/report-builder-format-hyperlink.png)
  
10. Haga clic en un vínculo. Si el equipo está conectado a Internet, un explorador abrirá a un tema de la Ayuda del Generador de informes.  
  
## <a name="RotateText"></a>Girar texto en el informe  
En esta sección, girará parte del texto de la tabla de las secciones anteriores.  
 
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la celda que contiene `[Territory].`  
  
3.  En la pestaña **Inicio** , en la sección **Fuente** , haga clic en el botón **Negrita** .  
  
4.  Si el panel de propiedades no está abierto, en la pestaña **Ver** active la casilla **Propiedades** .  
  
5.  Busque la propiedad WritingMode en el panel Propiedades y cámbiela de **Default** a **Rotate270**.  
 
    > [!NOTE]  
    > Cuando las propiedades del panel de propiedades se organizan en categorías, WritingMode está en la categoría **Localización** . Asegúrese de haber seleccionado la celda y no el texto. WritingMode es una propiedad del cuadro de texto, no del texto.  

    ![report-builder-select-territory-cell](../reporting-services/media/report-builder-select-territory-cell.png)
   
6.  En la pestaña **Inicio**, sección **Párrafo**, seleccione **Centro** y **Centrar** para colocar el texto en el centro de la celda tanto vertical como horizontalmente.  
  
8.  Haga clic en Ejecutar (**!**).  
  
Ahora el texto de la celda `[Territory]` está situado verticalmente desde la parte inferior a la parte superior de las celdas.  

![generador-de-informes-formato-girar-270](../reporting-services/media/report-builder-format-rotate-270.png)

## <a name="FormatCurrency"></a>Dar formato a moneda  
  
1.  Haga clic en **Diseño** para cambiar a la vista de diseño.  
  
2.  Haga clic en la celda de la tabla superior que contiene `[Sum(Sales)]`, mantenga presionada la tecla MAYÚS y haga clic en la celda de la tabla inferior que contiene `[Sum(Sales)]`.  
  
3.  En la pestaña **Inicio** > grupo **Número** > botón **Moneda**.  
  
4.  (Opcional)     Si la configuración regional es Inglés (Estados Unidos), el texto de ejemplo predeterminado es [**$12,345.00**]. Si no ve un valor de moneda de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** > **Valores de ejemplo**.  

    ![generador-de-informes-botón-valor-marcador-de-posición](../reporting-services/media/report-builder-placeholder-value-button.png)
  
5.  (Opcional) En la pestaña **Inicio** , en el grupo **Número** , haga clic dos veces en el botón **Disminuir decimales** para mostrar las cifras en dólares sin centavos.  
  
6.  Haga clic en Ejecutar (**!**) para obtener la vista previa del informe.  
  
El informe muestra ahora datos dados con formato y es más fácil de leer.  

![informe-generar-formato-informe](../reporting-services/media/report-build-format-report.png)
    
## <a name="FormatHTML"></a>Mostrar texto con formato HTML  
  
1.  Haga clic en **Diseño** para cambiar a la vista de diseño.  
  
2.  En la pestaña **Insertar** , haga clic en **Cuadro de texto**y, después, en la superficie de diseño, haga clic y arrastre para crear un cuadro de texto bajo la tabla, aproximadamente de cuatro pulgadas de ancho y tres de alto.  
  
3.  Copie este texto y péguelo en el cuadro de texto:  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  Arrastre el borde inferior del cuadro de texto para que queda todo el texto. Observe que la superficie de diseño aumenta a medida que realiza la acción de arrastrar.

5. Seleccione todo el texto del cuadro de texto.  
  
5.  Haga clic con el botón secundario en todo el texto seleccionado y, después, haga clic en **Propiedades del texto**.  
  
    Esta es una propiedad del texto, no del cuadro de texto, por lo que en un cuadro de texto puede tener una mezcla de texto sin formato y texto que usa etiquetas HTML como estilos.  
  
6.  En la pestaña **General** , bajo **Tipo de marcado**, haga clic en **HTML: interpretar etiquetas HTML como estilos**.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Haga clic en Ejecutar (**!**) para obtener la vista previa del informe.  
  
El texto del cuadro de texto se muestra como un encabezado, párrafo y lista con viñetas.  
  
![generador-de-informes-formato-html](../reporting-services/media/report-builder-format-html.png)

## <a name="Save"></a>Guardar el informe  
Puede guardar los informes en un servidor de informes, en una biblioteca de SharePoint o en su equipo.  
  
En este tutorial, guarde el informe en un servidor de informes. Si no tiene acceso a un servidor de informes, guarde el informe en su equipo.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
    Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por un nombre de su elección.

5.  Haga clic en **Guardar**.  
  
El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde desea guardar el informe.  
  
3.  En **Nombre**, reemplace el nombre predeterminado por un nombre de su elección. 
  
4.  Haga clic en **Guardar**.  

## <a name="next-steps"></a>Next Steps

Existen numerosas formas de dar formato al texto en el Generador de informes. [Tutorial: Crear un informe de forma libre](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md) contiene más ejemplos.  

[Tutoriales del Generador de informes ](../reporting-services/report-builder-tutorials.md) 
[Aplicar formato a elementos de informe](../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
[Generador de informes en SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
