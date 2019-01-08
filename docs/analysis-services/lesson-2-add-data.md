---
title: 'Lección 2: Agregar datos | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 22ee688f6ef1036c63cd3bf878ccf2fce869115f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52401640"
---
# <a name="lesson-2-add-data"></a>Lección 2: Agregar datos
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, usará al Asistente para importación de tablas en SSDT para conectarse a la base de datos SQL AdventureWorksDW, seleccionar datos, obtener una vista previa y filtrar los datos y, a continuación, importar los datos en el área de trabajo del modelo.  
  
Con el Asistente para importación de tabla, puede importar datos desde una variedad de orígenes relacionales: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata y mucho más. El procedimiento para importar los datos de cada uno de estos orígenes relacionales es muy similar al que se describe a continuación. También se pueden seleccionar datos mediante un procedimiento almacenado. Para más información sobre la importación de datos y los diferentes tipos de orígenes de datos puede importar desde, consulte [orígenes de datos](../analysis-services/tabular-models/data-sources-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 1: Cree un nuevo proyecto de modelo Tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Crear una conexión  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>Para crear una conexión a una base de datos de AdventureWorksDW2014  
  
1.  En el Explorador de modelos tabulares, haga clic en **orígenes de datos** > **importar desde el origen de datos**.  
  
    Esto inicia al Asistente para importación de tablas, que le guiará a través de una conexión a un origen de datos. Si no ve el Explorador de modelos tabulares, haga doble clic en **Model.bim** en **el Explorador de soluciones** para abrir el modelo en el diseñador. 
    
    ![como-tabular-lesson2-tme](../analysis-services/media/as-tabular-lesson2-tme.png) 

    Nota: Si va a crear el modelo en el nivel de compatibilidad 1400, verá la nueva experiencia de obtener datos en lugar el Asistente para importación de tablas. Los cuadros de diálogo se mostrará un poco diferentes de los pasos siguientes, pero aún podrá seguir el tutorial. 
  
2.  En el Asistente para importación de tablas, en **bases de datos relacionales**, haga clic en **Microsoft SQL Server** > **siguiente**.  
  
3.  En la página **Conectarse a una base de datos de Microsoft SQL Server** , en **Nombre descriptivo de la conexión**, escriba **BD de Adventure Works de SQL**.  
  
4.  En **nombre del servidor**, escriba el nombre del servidor donde instaló la base de datos AdventureWorksDW.  
  
5.  En el **nombre de base de datos** campos, seleccione **AdventureWorksDW**y, a continuación, haga clic en **siguiente**.  
  
    ![como-tabular-lesson2-tiw-name](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  En la página **Información de suplantación** , tendrá que especificar las credenciales que usará Analysis Services para conectar con el origen de datos al importar y procesar los datos. Compruebe que **Nombre de usuario y contraseña específicos de Windows** está seleccionado y, en **Nombre de usuario** y **Contraseña**, especifique las credenciales de inicio de sesión de Windows y haga clic en **Siguiente**.  
  
    > [!NOTE]  
    > El uso de una cuenta de usuario y una contraseña de Windows es el método más seguro de conexión a un origen de datos. Para obtener más información, consulte [suplantación](../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
7.  En la página **Elegir cómo importar los datos** , compruebe que la opción **Seleccionar de una lista de tablas y vistas para elegir los datos para importar** está seleccionada. Tendrá que seleccionar valores de una lista de tablas y vistas, así que haga clic en **Siguiente** para mostrar una lista de todas las tablas de origen de la base de datos de origen.  
  
8.  En el **seleccionar tablas y vistas** , seleccione la casilla de verificación para las siguientes tablas: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, y **FactInternetSales**.  
  
    **NO** haga clic en **Finalizar**.  
  
## <a name="FilterData"></a>Filter the table data  
La tabla DimCustomer que va a importar desde la base de datos de ejemplo contiene un subconjunto de los datos de la base de datos de Adventure Works de SQL Server original. Filtrará algunas más de las columnas de la tabla DimCustomer que no son necesarias cuando se importan en el modelo. Cuando sea posible, desea filtrar los datos que no se utilicen para ahorrar espacio en memoria que usa el modelo.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Para filtrar los datos de las tablas antes de importar  
  
1.  Seleccione la fila de la **DimCustomer** de tabla y, a continuación, haga clic en **vista previa y filtro**. La ventana **Vista previa de la tabla seleccionada** se abre con todas las columnas de la tabla de origen DimCustomer mostradas.  
  
2.  Desactive la casilla situada sobre las siguientes columnas: **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**. 

    ![como-tabular-lesson2-tiw-clear](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    Puesto que los valores de estas columnas no son pertinentes para el análisis de ventas por Internet, no hay necesidad de importarlas. Eliminación de columnas innecesarias hará que el modelo más pequeño y eficaz.  
  
3.  Compruebe que el resto de las columnas estén activadas y después haga clic **Aceptar**.  
  
    Tenga en cuenta las palabras **filtros aplicados** se muestran ahora en el **detalles del filtro** columna en el **DimCustomer** fila; si hace clic en ese vínculo, verá una descripción textual de la filtros que recién aplicados.  
    
    ![como-tabular-lesson2--filtros aplicados](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  Filtre las tablas restantes desactivando las casillas de las columnas siguientes en cada tabla:  
    
    **DimDate**
    
      |columna|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |columna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |columna|  
      |-----------|  
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
  
    **DimProductCategory**
  
      |columna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |columna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |columna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
Ahora que ha muestra una vista previa y filtrar los datos innecesarios, puede importar el resto de los datos que desee. El asistente importa los datos de la tabla junto con todas las relaciones entre las tablas. Se crean nuevas tablas y columnas en el modelo y no se importarán los datos filtrados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar los datos de las columnas y las tablas seleccionadas  
  
1.  Revise las opciones seleccionadas. Si todo parece correcto, haga clic en **finalizar**.  
  
    Mientras importa los datos, el asistente muestra cuántas filas se han capturado. Cuando se hayan importado todos los datos, se muestra un mensaje para indicarlo.  
    
    ![como-tabular-lesson2-success](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > Para ver las relaciones que se han creado automáticamente entre las tablas importadas, en la fila **Preparación de datos** , haga clic en **Detalles**. 
  
2.  Haga clic en **Cerrar**.  
  
    El asistente se cierra y el Diseñador de modelos muestra ahora las tablas importadas. 
  
## <a name="save-your-model-project"></a>Guarde el proyecto de modelo  
Es importante que guarde frecuentemente el proyecto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para guardar el proyecto de modelo  
  
-   Click **Archivo** > **Guardar todo**.  
  
## <a name="whats-next"></a>¿Qué sigue?
Vaya a la lección siguiente: [Lección 3: Marcar como tabla de fechas](../analysis-services/lesson-3-mark-as-date-table.md).

  
  
