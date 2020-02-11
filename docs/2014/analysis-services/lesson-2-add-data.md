---
title: 'Lección 2: agregar datos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 370e368843fa1e9584cc341397853fcdad26922a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078971"
---
# <a name="lesson-2-add-data"></a>Lección 2: Agregar datos
  En esta lección usará el Asistente para la importación de tablas de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para conectarse a la base de datos SQL AdventureWorksDW, seleccionar datos, obtener una vista previa, filtrar los datos e importarlos al área de trabajo del modelo.  
  
 Con el Asistente para importación de tabla, puede importar datos desde una variedad de orígenes relacionales: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata y mucho más. El procedimiento para importar los datos de cada uno de estos orígenes relacionales es muy similar al que se describe a continuación. Asimismo, los datos se pueden seleccionar mediante un procedimiento almacenado.  
  
 Para obtener más información sobre la importación de datos y los diferentes tipos de orígenes de datos de los que puede realizar la importación, vea [Orígenes de datos &#40;SSAS tabular&#41;](data-sources-ssas-tabular.md).  
  
 Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 1: crear un nuevo proyecto de modelo tabular](lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Crear una conexión  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2012-database"></a>Para crear una conexión con la base de datos AdventureWorksDW2012  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y, a continuación, haga clic en **Importar desde el origen de datos**.  
  
     De esta forma se inicia el Asistente para la importación de tablas, que le guía a través del proceso para establecer una conexión a un origen de datos. Si **Importar desde el origen de datos** está atenuado, haga doble clic en **Model.bim** en **Explorador de soluciones** para abrir el modelo en el diseñador.  
  
2.  En el **Asistente para la importación de tablas**, bajo **Bases de datos relacionales**, haga clic en **Microsoft SQL Server**y después en **Siguiente**.  
  
3.  En la página **conectar a una base de datos de Microsoft SQL Server** , en **nombre descriptivo**de la conexión, escriba `Adventure Works DB from SQL`.  
  
4.  En **Nombre del servidor**, escriba el nombre del servidor en el que instaló la base de datos AdventureWorksDW.  
  
5.  En el campo **Nombre de la base de datos** , haga clic en la flecha abajo y seleccione **AdventureWorksDW**; a continuación, haga clic en **Siguiente**.  
  
6.  En la página **Información de suplantación** , tendrá que especificar las credenciales que usará Analysis Services para conectar con el origen de datos al importar y procesar los datos. Compruebe que **Nombre de usuario y contraseña específicos de Windows** está seleccionado y, en **Nombre de usuario** y **Contraseña**, especifique las credenciales de inicio de sesión de Windows y haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  El uso de una cuenta de usuario y contraseña de Windows proporciona el método más seguro de conectarse a un origen de datos. Para más información, vea [Suplantación &#40;SSAS tabular&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
7.  En la página **Elegir cómo importar los datos** , compruebe que la opción **Seleccionar de una lista de tablas y vistas para elegir los datos para importar** está seleccionada. Tendrá que seleccionar valores de una lista de tablas y vistas, así que haga clic en **Siguiente** para mostrar una lista de todas las tablas de origen de la base de datos de origen.  
  
8.  En la página **Seleccionar tablas y vistas** , active la casilla para las siguientes tablas: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**y **FactInternetSales**.  
  
9. Vamos a asignar nombres fáciles de identificar a las tablas del modelo. Haga clic en la celda de la columna **Nombre descriptivo** de **DimCustomer**. Cambie el nombre de la tabla quitando "DIM" de DimCustomer.  
  
10. Cambie el nombre de las demás tablas:  
  
    |Nombre de origen|Nombre descriptivo|  
    |-----------------|-------------------|  
    |DimDate|Date|  
    |DimGeography|Geography|  
    |DimProduct|Producto|  
    |DimProductCategory|Categoría de productos|  
    |DimProductSubcategory|Product Subcategory|  
    |FactInternetSales|Internet Sales|  
  
     **No** haga clic en **Finalizar**.  
  
 Ahora que se ha conectado a la base de datos, ha seleccionado las tablas que se importarán y ha asignado nombres descriptivos a las tablas, vaya a la siguiente sección, [Filtrar los datos de la tabla antes de importar](#FilterData).  
  
##  <a name="FilterData"></a>Filtrar los datos de la tabla  
 La tabla DimCustomer que va a importar de la base de datos contiene un subconjunto de los datos de la base de datos Adventure original de SQL Server. Filtrará algunas de las columnas de la tabla DimCustomer que no son necesarias. Cuando sea posible, querrá filtrar los datos que no se utilicen para ahorrar espacio en memoria usado por el modelo.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Para filtrar los datos de las tablas antes de importar  
  
1.  Seleccione la fila de la tabla **Customer** y luego haga clic en **Vista previa y filtro**. La ventana **Vista previa de la tabla seleccionada** se abre con todas las columnas de la tabla de origen DimCustomer mostradas.  
  
2.  Desactive la casilla situada sobre las siguientes columnas:  
  
    |Customer|  
    |--------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
     Dado que los valores de estas columnas no son pertinentes para el análisis de ventas por Internet, no es necesario importar estas columnas. La eliminación de columnas innecesarias reducirá el tamaño de su modelo.  
  
3.  Compruebe que el resto de las columnas estén activadas y después haga clic **Aceptar**.  
  
     Observe que las palabras **filtros aplicados** se muestran ahora en la columna **detalles del filtro** en la fila **Customer** ; Si hace clic en ese vínculo, verá una descripción de texto de los filtros que acaba de aplicar.  
  
4.  Filtre las tablas restantes desactivando las casillas de las columnas siguientes en cada tabla:  
  
    |Date|  
    |----------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |Geography|  
    |---------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |Producto|  
    |-------------|  
    |**SpanishProductName**|  
    |**FrenchProductName**|  
    |**FrenchDescription**|  
    |**ChineseDescription**|  
    |**ArabicDescription**|  
    |**HebrewDescription**|  
    |**ThaiDescription**|  
    |**GermanDescription**|  
    |**JapaneseDescription**|  
    |**TurkishDescription**|  
  
    |Categoría de productos|  
    |----------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |Product Subcategory|  
    |-------------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |--------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
 Ahora que ha obtenido una vista previa de los datos innecesarios y los ha filtrado, puede importar los datos. Vaya a la siguiente sección, **Importar los datos de las columnas y las tablas seleccionadas**.  
  
##  <a name="Import"></a>Importar las tablas y los datos de columna seleccionados  
 Ahora puede importar los datos seleccionados. El asistente importa los datos de las tablas junto con las relaciones entre las tablas. Las nuevas tablas y columnas se crean en el modelo con los nombres descriptivos que especificó, y los datos que filtró no se importan.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar las tablas y los datos de columna seleccionados  
  
1.  Revise lo que ha seleccionado. Si todo parece correcto, haga clic en **Finalizar**.  
  
     Mientras importa los datos, el asistente muestra cuántas filas se han capturado. Cuando se hayan importado todos los datos, se muestra un mensaje para indicarlo.  
  
    > [!TIP]  
    >  Para ver las relaciones que se han creado automáticamente entre las tablas importadas, en la fila **Preparación de datos** , haga clic en **Detalles**.  
  
2.  Haga clic en **Cerrar**.  
  
     El asistente se cierra y aparece el diseñador de modelos. Cada tabla se ha agregado como una nueva pestaña en el diseñador de modelos.  
  
## <a name="save-the-model-project"></a>Guardar el proyecto de modelo  
 Es importante que guarde frecuentemente el proyecto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para guardar el proyecto de modelo  
  
-   En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Archivo** y luego en **Guardar todo**.  
  
## <a name="next-step"></a>siguiente paso  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 3: Cambiar el nombre de las columnas](rename-columns.md).  
  
  
