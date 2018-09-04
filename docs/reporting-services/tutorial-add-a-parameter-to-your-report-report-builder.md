---
title: 'Tutorial: Agregar un parámetro a un informe (Generador de informes) | Microsoft Docs'
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0fd54e59c30a03cc918bc080ab64b21db8983ba1
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43278483"
---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>Tutorial: Agregar un parámetro a un informe (Generador de informes)
En este tutorial, agregará un parámetro a un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] para que los lectores del informe puedan filtrar los datos del informe para uno o más valores. 
  
![report-builder-parameter-tutorial](../reporting-services/media/report-builder-parameter-tutorial.png)

Los parámetros del informe se crean automáticamente para cada parámetro de la consulta que incluya en una consulta del conjunto de datos. El tipo de datos de parámetro determina cómo aparece en la barra de herramientas de visualización de informe. 
   
> [!NOTE]  
> En este tutorial, los pasos del asistente se encuentran reunidos en un único procedimiento. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos y crear un conjunto de datos, consulte el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tiempo estimado para completar este tutorial: 25 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Setup"></a>1. Crear un informe de matriz y un conjunto de datos en el Asistente para tabla o matriz  
Cree un informe de matriz, un origen de datos y un conjunto de datos.  
  
> [!NOTE]  
> En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
### <a name="to-create-a-new-matrix-report"></a>Para crear un nuevo informe de matriz  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, asegúrese de que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos** > **Siguiente**.  
  
7.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos de la lista o vaya al servidor de informes y seleccione uno. Seleccione cualquier origen de datos del tipo **SQL Server**.  
      
8.  Haga clic en **Siguiente**.  

    Puede que tenga que escribir sus credenciales.    
     
9. En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
10. Pegue la siguiente consulta en el panel vacío en la parte superior:  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
    Esta consulta combina los resultados de varias instrucciones SELECT de [!INCLUDE[tsql_md](../includes/tsql-md.md)] dentro de una expresión de tabla común para especificar los valores que están basados en datos de ventas simplificados de cámaras de la base de datos de ejemplo Contoso. Las subcategorías son cámaras digitales, cámaras réflex digitales de una sola lente (SLR), cámaras de vídeo y accesorios.  
  
11. En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar** (**!**) para ver los datos.   
  
    El conjunto de resultados consta de 11 filas de datos que muestran la cantidad de elementos vendidos para cada subcategoría de cuatro almacenes en las columnas siguientes: StoreID, Subcategory, Quantity. El nombre del almacén no forma parte del conjunto de resultados. Más adelante en este tutorial, buscará en otro conjunto de datos el nombre del almacén que corresponde al identificador del almacén.  
  
    Esta consulta no contiene parámetros de consulta. Agregará los parámetros de consulta posteriormente en este tutorial.   
  
12. Haga clic en **Siguiente**.  
  
## <a name="CompleteWizard"></a>2. Organizar datos y elegir el diseño en el asistente  
El asistente proporciona un diseño inicial para mostrar los datos. El panel de vista previa del asistente le ayudará a visualizar el resultado de las agrupaciones de datos antes de completar la tabla o el diseño de la matriz.  
  
### <a name="to-organize-data-into-groups"></a>Para organizar los datos en grupos  
  
1.  En la página **Organizar campos** , arrastre Subcategory a **Grupos de filas**.  
  
2.  Arrastre StoreID a **Grupos de columnas**.  
  
3.  Arrastre Quantity a **Valores**.  
  
    Ha organizado los valores de cantidad vendida en filas agrupadas por subcategoría, con una columna para cada almacén.  
  
4.  Haga clic en **Siguiente**.  
  
5.  En la página **Elegir el diseño** , en **Opciones**, asegúrese de que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
    Al ejecutar el informe, la última columna mostrará la cantidad total de cada subcategoría para todos los almacenes y la última fila mostrará la cantidad total para todas las subcategorías de cada almacén.  
  
6.  Haga clic en **Siguiente**.  
  
8.  Haga clic en **Finalizar**.  
  
    La matriz se agrega a la superficie de diseño. La matriz muestra tres columnas y tres filas. El contenido de las celdas de la primera fila es Subcategory, [StoreID] y Total. El contenido de las celdas de la segunda fila muestra expresiones que representan la subcategoría, la cantidad de artículos vendidos de cada almacén y el total de cada subcategoría de todos los almacenes. Las celdas de la última fila muestran los totales de cada almacén.  
      
    ![ssRB_ParamTut_Design](../reporting-services/media/ssrb-paramtut-design.png)  
  
9. Haga clic en la matriz, mantenga el mouse sobre el borde de la primera columna, agarre el controlador y expanda el ancho de la columna.  
  
   ![ssRB_ParamTut_Drag](../reporting-services/media/ssrb-paramtut-drag.png)  
  
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El informe se ejecuta en el servidor de informes y muestra el título y la hora en que tuvo lugar el procesamiento del informe.  

![ssRB_ParamTut__Preview1](../reporting-services/media/ssrb-paramtut-preview1.png)
  
Hasta el momento, los encabezados de columna muestran el identificador del almacén, pero no su nombre. Más adelante agregará una expresión para buscar el nombre del almacén en un conjunto de datos que contiene pares identificador/nombre de almacén.  
  
## <a name="Query"></a>3. Agregar un parámetro de consulta para crear un parámetro de informe  
Al agregar un parámetro de consulta a una consulta, el Generador de informes crea automáticamente un parámetro de informe de un solo valor con propiedades predeterminadas para el nombre, mensaje y tipo de datos.  
  
### <a name="to-add-a-query-parameter"></a>Para agregar un parámetro de consulta  
  
1.  Haga clic en **Diseño** para volver a cambiar a la vista Diseño.  
  
2.  En el panel Datos de informe, expanda la carpeta **Conjuntos de datos** , haga clic con el botón derecho en **DataSet1**y haga clic en **Consulta**.  
  
3.  Agregue la siguiente cláusula [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** clause as the last line in the query:  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
    Se abre el cuadro de diálogo **de** limita los datos recuperados al identificador del almacén que se especifica mediante el parámetro de consulta *@StoreID*.  
  
4.  En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar** (**!**). Se abre el cuadro de diálogo **Definir parámetros de consulta** y se le pide un valor para el parámetro de consulta *@StoreID*.  
  
5.  En **Valor de parámetro**, escriba **200**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    El conjunto de resultados muestra las cantidades vendidas de accesorios, cámaras de vídeo y cámaras digitales SLR para el identificador de almacén **200**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  En el panel Datos de informe, expanda la carpeta **Parámetros** .  
  
Tenga en cuenta que ahora hay un parámetro de informe denominado *@StoreID*y un panel Parámetros donde puede diseñar los parámetros del informe.   
  
![ssRB_ParamPane](../reporting-services/media/ssrb-parampane.png)  
  
¿No ve un panel Parámetros? En el menú **Ver** , seleccione **Parámetros**.  
  
## <a name="ChangeDefaultProperties"></a>4. Cambiar el tipo de datos predeterminado y otras propiedades de un parámetro de informe  
Después de crear un parámetro de informe, puede ajustar los valores predeterminados de las propiedades.  
  
### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>Para cambiar el tipo de datos predeterminado para un parámetro de informe  
  
De manera predeterminada, el parámetro que ha creado tiene el tipo de datos **Texto**. Como el identificador de almacén es un entero, puede cambiar el tipo de datos a Entero.  
  
1.  En el panel Datos de informe debajo del nodo **Parámetros** , haga clic con el botón derecho en *@StoreID*y luego haga clic en **Propiedades del parámetro**.  
  
2.  En **Pedir datos**, escriba **¿Identificador del almacén?** Este texto aparece en la barra de herramientas del visor de informes al ejecutar el informe.  
  
3.  En **Tipo de datos**, en la lista desplegable, seleccione **Entero**.  
  
4.  Acepte los valores predeterminados restantes del cuadro de diálogo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe. El visor de informes muestra **Store Identifier?** para *@StoreID*.  
  
7.  En la barra de herramientas del visor de informes, al lado de Store ID, escriba **200**y, después, haga clic en **Ver informe**.  
  
![SSRB_ParamTutStoreID](../reporting-services/media/ssrb-paramtutstoreid.png)  
  
## <a name="AddDataset"></a>4a. Agregar un conjunto de datos para proporcionar los valores disponibles y nombres para mostrar  
Para asegurarse de que los lectores del informe solo pueden escribir valores válidos para un parámetro, puede crear una lista desplegable de valores entre los que elegir. Los valores pueden proceder de un conjunto de datos o de una lista que se especifique. Se deben proporcionar valores disponibles de un conjunto de datos con una consulta que no contenga una referencia al parámetro.  
  
### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>Para crear un conjunto de datos para los valores válidos de un parámetro  
  
1.  Haga clic en **Diseño** para cambiar a la vista Diseño.  
  
2.  En el panel Datos de informe, haga clic con el botón derecho en la carpeta **Conjuntos de datos** y, después, haga clic en **Agregar conjunto de datos**.  
  
3.  En **Nombre**, escriba **Almacenes**.  
  
4.  Seleccione **Usar un conjunto de datos insertado en el informe**.  
  
5.  En **Origen de datos**, en la lista desplegable, elija el origen de datos que ha usado en el primer procedimiento.  
  
6.  En **Tipo de consulta**, compruebe que la opción **Texto** está seleccionada.  
  
7.  En **Consulta**, pegue el texto siguiente:  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    El panel Datos de informe muestra los campos StoreID y StoreName bajo el nodo de conjunto de datos **Almacenes** .  
  
## <a name="AvailableValues"></a>4b. Especificar valores disponibles para mostrar en una lista 
Después de crear un conjunto de datos para proporcionar los valores disponibles, cambie las propiedades de informe para especificar qué conjunto de datos y qué campo usar para rellenar la lista desplegable de valores válidos de la barra de herramientas del visor de informes.  
  
### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>Para proporcionar los valores disponibles para un parámetro desde un conjunto de datos  
  
1.  En el panel Datos de informe, haga clic con el botón derecho en el parámetro *@StoreID*y luego haga clic en **Propiedades del parámetro**.  
  
2.  Haga clic en **Valores disponibles**y luego haga clic en **Obtener valores de una consulta**.  
  
3.  En **Conjunto de datos**, haga clic en **Almacenes**en la lista desplegable.  
  
4.  En **Campo de valor**, en la lista desplegable, haga clic en StoreID.  
  
5.  En **Campo de etiqueta**, en la lista desplegable, haga clic en StoreName. El campo de etiqueta especifica el nombre para mostrar del valor.  
  
6.  Haga clic en **General**.  
  
7.  En **Pedir datos**, cambie **¿Identificador del almacén?** a **¿Nombre del almacén?**  
  
    Los lectores del informe seleccionarán ahora entre una lista de nombres de almacén en lugar de entre los identificadores de almacén. Observe que el tipo de datos de parámetro sigue siendo **Entero** , porque el parámetro está basado en el identificador del almacén, no el nombre del almacén.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Obtenga una vista previa del informe.  
  
    En la barra de herramientas del visor de informes, el cuadro de texto del parámetro es ahora una lista desplegable que muestra **Seleccionar un valor**.  
  
10. En la lista desplegable, seleccione Contoso Catalog Store y, después, haga clic en **Ver informe**.  
  
El informe muestra la cantidad vendida de accesorios, cámaras de vídeo y cámaras digitales SLR para el identificador de almacén **200**.  
  
## <a name="DefaultValues"></a>4c. Especificar un valor predeterminado 
Puede especificar un valor predeterminado para cada parámetro de modo que el informe se ejecute automáticamente.  
  
### <a name="to-specify-a-default-value-from-a-dataset"></a>Para especificar un valor predeterminado de un conjunto de datos  
  
1.  Cambie a la vista de diseño.  
  
2.  En el panel Datos de informe, haga clic con el botón derecho en *@StoreID*y luego haga clic en **Propiedades del parámetro**.  
  
3.  Haga clic en **Valores predeterminados**y, después, haga clic en **Obtener valores de una consulta**.  
  
4.  En **Conjunto de datos**, haga clic en **Almacenes**en la lista desplegable.  
  
5.  En **Campo de valor**, en la lista desplegable, haga clic en StoreID.  
  
6.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)]  
  
7.  Obtenga una vista previa del informe.  
  
For *@StoreID*, el visor de informes muestra el valor "Contoso North America Online Store", porque es el primer valor del conjunto de resultados del conjunto de datos **Almacenes**. El informe muestra la cantidad vendida de cámaras digitales para el identificador del almacén **199**.  
  
### <a name="to-specify-a-custom-default-value"></a>Para especificar un valor predeterminado personalizado  
  
1.  Cambie a la vista de diseño.  
  
2.  En el panel Datos de informe, haga clic con el botón derecho en *@StoreID*y haga clic en **Propiedades del parámetro**.  
  
3.  Haga clic en **Valores predeterminados** > **Especificar valores** > **Agregar**. Se agrega una nueva fila de valor.  
  
4.  En **Valor**, escriba **200**.  
  
5.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)] 
  
6.  Obtenga una vista previa del informe.  
  
For *@StoreID*, el visor de informes muestra "Contoso Catalog Store", porque es el nombre para mostrar del identificador de almacén **200**. El informe muestra la cantidad vendida de accesorios, cámaras de vídeo y cámaras digitales SLR para el identificador de almacén **200**.  
  
## <a name="NameValue"></a>4d. Buscar un par Nombre/Valor  
Un conjunto de datos podría contener el identificador y el campo de nombre correspondiente. Si solo tiene un identificador, puede buscar el nombre correspondiente en un conjunto de datos que haya creado y que tenga pares de nombre/valor.  
  
### <a name="to-look-up-a-value-from-a-dataset"></a>Para buscar un valor de un conjunto de datos  
  
1.  Cambie a la vista de diseño.  
  
2.  En la superficie de diseño, en la matriz, en el encabezado de columna de la primera fila, haga clic con el botón derecho en `[StoreID]` y, después, haga clic en **Expresión**.  
  
3.  En el panel de expresión, elimine todo el texto excepto el **signo igual** (=) inicial.  
  
4.  En **Categoría**, expanda **Funciones comunes**y haga clic en **Varios**. El panel de elementos muestra un conjunto de funciones.  
  
5.  En Elemento, haga doble clic en **Búsqueda**. En el panel de expresión se muestra `=Lookup(`. En el panel de ejemplo se muestra un ejemplo de sintaxis de búsqueda.  
  
6.  Escriba la siguiente expresión: 

    ```  
    =Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")      
    ```  
  
    La función de búsqueda toma el valor de StoreID, lo busca en el conjunto de datos "Almacenes" y devuelve el valor de StoreName.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    El encabezado de columna del almacén contiene el texto para mostrar de una expresión compleja: **Expr**.  
  
8.  Obtenga una vista previa del informe.  
  
El encabezado de columna de la parte superior de cada columna muestra el nombre del almacén en lugar del identificador del almacén.  
  
## <a name="Expression"></a>5. Mostrar el valor de parámetro seleccionado en el informe  
Si los lectores del informe tienen preguntas sobre un informe, resulta útil saber qué valores de parámetro han elegido. Puede conservar los valores seleccionados por el usuario para cada parámetro del informe. Una forma de hacerlo es mostrar los parámetros en un cuadro de texto en el pie de página.  
  
### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>Para mostrar el valor del parámetro seleccionado y etiquetarlo en un pie de página  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic con el botón derecho en el pie de página > **Insertar** > **Cuadro de texto**. Arrastre el cuadro de texto junto al cuadro de texto que tiene la marca de tiempo. Agarre el controlador lateral del cuadro de texto y expanda el ancho.  
  
3.  En el panel Datos de informe, arrastre el parámetro *@StoreID* al cuadro de texto. El cuadro de texto presenta `[@StoreID]`.  
  
4.  Para mostrar la etiqueta de parámetro, haga clic en el cuadro de texto hasta que el cursor de inserción aparezca después de la expresión existente, escriba un espacio y, a continuación, arrastre otra copia del parámetro en el panel Datos de informe al cuadro de texto. El cuadro de texto presenta `[@StoreID] [@StoreID]`.  
  
5.  Haga clic con el botón derecho en el primer `[@StoreID]` y haga clic en **Expresión**. Se abre el cuadro de diálogo **Expresión** . Reemplace el texto `Value` con `Label`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    El texto indica: `[@StoreID.Label] [@StoreID]`.  
  
7.  Obtenga una vista previa del informe.  
  
## <a name="Filter"></a>6. Utilizar el parámetro de informe en un filtro  
Los filtros ayudan a controlar qué datos se deben usar en un informe una vez que se han recuperado de un origen de datos externo. Para permitir que los lectores del informe controlen los datos que quieren ver, puede incluir el parámetro de informe en un filtro para la matriz.  
  
### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>Para especificar un parámetro en un filtro de la matriz  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic con el botón derecho en una fila o identificador del encabezado de columna de la matriz y, después, haga clic en **Propiedades de Tablix**.  
  
3.  Haga clic en **Filtros**y luego en **Agregar**. Aparece una nueva fila de filtro.  
  
4.  En **Expresión**, en la lista desplegable, seleccione el StoreId del campo de conjunto de datos. El tipo de datos indica **Entero**. Cuando el valor de expresión es un campo de un conjunto de datos, el tipo de datos se establece automáticamente.  
  
5.  En **Operador**, compruebe que está seleccionado **signo igual** (=).  
  
6.  En **Valor**, escriba `[@StoreID]`. 

    `[@StoreID]` es la sintaxis de expresión simple que representa `=Parameters!StoreID.Value`.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Obtenga una vista previa del informe.  
  
    La matriz solo muestra los datos de "Contoso Catalog Store".  
  
9. En la barra de herramientas del visor de informes, para **¿Nombre del almacén?**, seleccione **Contoso Asia Online Store**y, después, haga clic en **Ver informe**.  
  
La matriz muestra los datos correspondientes al almacén que había seleccionado.  
  
## <a name="Multivalued"></a>7. Cambiar el parámetro de informe a fin de que acepte varios valores  
Para cambiar un parámetro de un solo valor a varios valores, debe cambiar la consulta y todas las expresiones que contienen una referencia al parámetro, incluidos los filtros. Un parámetro de varios valores es una matriz de valores. En una consulta de conjunto de datos, la sintaxis de la consulta debe comprobar la inclusión de un valor en un conjunto de valores. En una expresión de informe, la sintaxis de la expresión debe tener acceso a una matriz de valores y no a un valor individual.  
  
### <a name="to-change-a-parameter-from-single-to-multivalued"></a>Para cambiar un parámetro de un solo valor a varios valores  
  
1.  Cambie a la vista de diseño.  
  
2.  En el panel Datos de informe, haga clic con el botón derecho en *@StoreID*y haga clic en **Propiedades del parámetro**.  
  
3.  Seleccione **Permitir varios valores**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  En el panel Datos de informe, expanda la carpeta **Conjuntos de datos** , haga clic con el botón derecho en **DataSet1**y haga clic en **Consulta**.  
  
6.  Cambie el **signo igual** (=) por **IN** en la cláusula [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** clause en la cláusula last line en la cláusula query:  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
    El operador **IN** prueba un valor para su inclusión en un conjunto de valores.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Haga clic con el botón derecho en una fila o identificador del encabezado de columna de la matriz y, después, haga clic en **Propiedades de Tablix**.  
  
9. Haga clic en **Filtros**.  
  
10. En **Operador**, seleccione **In**.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. En el cuadro de texto que muestra el parámetro en el pie de página, elimine todo el texto.  
  
13. Haga clic con el botón derecho en el cuadro y, después, haga clic en **Expresión**. Escriba la siguiente expresión: `=Join(Parameters!StoreID.Label, ", ")`  
  
    Esta expresión concatena todos los nombres de almacén seleccionados por el usuario, separados por una coma y un espacio.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. Haga clic en el cuadro de texto que hay delante de la expresión que acaba de crear y, a continuación, escriba lo siguiente: 

    **Valores de parámetro seleccionados:** 
  
16. Obtenga una vista previa del informe.  
  
17. Haga clic en la lista desplegable al lado de ¿Nombre del almacén?  
  
    Cada valor válido aparece al lado de una casilla.  
  
18. Haga clic en **Seleccionar todo**y, después, en **Ver informe**.  
  
    El informe muestra la cantidad vendida para todas las subcategorías en todos los almacenes.  
  
19. En la lista desplegable, haga clic en **Seleccionar todo** para borrar la lista, haga clic en "Contoso Catalog Store" y en "Contoso Asia Online Store" y luego haga clic en **Ver informe**.  

    ![report-builder-parameter-multiselect](../reporting-services/media/report-builder-parameter-multiselect.png)
  
 
## <a name="Boolean"></a>8. Agregar un parámetro booleano para obtener visibilidad condicional  
  
### <a name="to-add-a-boolean-parameter"></a>Para agregar un parámetro booleano  
  
1.  En la superficie de diseño, en el panel Datos de informe, haga clic con el botón derecho en **Parámetros**y haga clic en **Agregar parámetro**.  
  
2.  En **Nombre**, escriba ShowSelections.  
  
3.  En **Pedir datos**, escriba ¿Mostrar selecciones?  
  
4.  En **Tipo de datos**, haga clic en **Booleano**.  
  
5.  Haga clic en **Valores predeterminados**.  
  
6.  Haga clic en **Especificar valor**y, después, haga clic en **Agregar**.  
  
7.  En **Valor**, escriba **False**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>Para establecer la visibilidad en función de un parámetro booleano  
  
1.  En la superficie de diseño, haga clic con el botón derecho en el cuadro de texto del pie de página que muestra los valores de parámetro y luego haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en **Visibilidad**.  
  
3.  Seleccione la opción **Mostrar u ocultar en función de una expresión**y, después, haga clic en el botón de expresión **Fx**.  
  
4.  Escriba la siguiente expresión: `=Not Parameters!ShowSelections.Value`  
  
    La propiedad Hidden controla la opción Visibilidad del cuadro de texto. Aplique el operador **Not** para que cuando el parámetro esté seleccionado, la propiedad Hidden sea false y, así, se mostrará el cuadro de texto.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Obtenga una vista previa del informe.  
  
    El cuadro de texto que muestra las opciones de parámetro en el pie de página no aparece.  
  
8.  En la barra de herramientas del visor de informes, al lado de **Show selections**(Mostrar selecciones), haga clic en **True** > **Ver informe**.  
  
    El cuadro de texto del pie de página aparece y muestra todos los nombres de almacén que haya seleccionado.  
  
## <a name="Title"></a>9. Agregar un título de informe  
  
### <a name="to-add-a-report-title"></a>Para agregar un título de informe  

1.  Cambie a la vista de diseño.  
   
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba Parameterized Product Sales y, a continuación, haga clic fuera del cuadro de texto.  
  
## <a name="Save"></a>10. Guardar el informe  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
    Aparece el mensaje **Conectándose al servidor de informes**. Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por Ventas de productos con parámetros.  
  
5.  Haga clic en **Guardar**.  
  
El informe se guarda en el servidor de informes. El servidor de informes al que está conectado aparece en la barra de estado en la parte inferior de la ventana.  
  
## <a name="next-steps"></a>Next Steps  
De esta forma se concluye el tutorial sobre cómo agregar un parámetro a un informe. Para obtener más información sobre los parámetros, consulte [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Ver también  
* [Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)
* [Generador de informes en SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
*  [Función Lookup](../reporting-services/report-design/report-builder-functions-lookup-function.md)   
