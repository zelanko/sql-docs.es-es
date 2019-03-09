---
title: 'Analysis Services lección del tutorial 2: Obtención de datos | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 01bf31c3d4f89b77ebdceae2e69d4054a578b03f
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685322"
---
# <a name="get-data"></a>Obtener datos

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, usará **obtener datos** para conectarse a la base de datos de ejemplo AdventureWorksDW, seleccionar datos, la vista previa y filtrar y, a continuación, importar en el área de trabajo del modelo.  
  
Internamente, obtener datos es Power Query, que proporciona una amplia gama de herramientas para la conexión y cambiar la forma de datos para el modelado y análisis. Para obtener más información, consulte [documentación de Power Query](https://docs.microsoft.com/power-query/). 

> [!NOTE]
> Tareas y las imágenes en este tutorial se muestran conectarse a una base de datos de AdventureWorksDW2014 en un servidor local. En algunos casos, una base de datos AdventureWorksDW en Azure SQL Data Warehouse puede mostrar objetos diferentes; No obstante, fundamentalmente son iguales.
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 1: Cree un nuevo proyecto de modelo tabular](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Crear una conexión  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>Para crear una conexión a la base de datos AdventureWorksDW  
  
1.  En **Explorador de modelos tabulares**, haga clic en **orígenes de datos** > **importar desde el origen de datos**.  
  
    Esto inicia **obtener datos**, que le guiará a través de conectarse a un origen de datos. Si no ve el Explorador de modelos tabulares, en **el Explorador de soluciones**, haga doble clic en **Model.bim** para abrir el modelo en el diseñador. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  Obtener los datos, haga clic en **base de datos** > **base de datos de SQL Server** > **Connect**.  
  
3.  En el **base de datos de SQL Server** cuadro de diálogo, en **Server**, escriba el nombre del servidor donde instaló la base de datos AdventureWorksDW y, a continuación, haga clic en **Connect**.  

4.  Cuando se le pida que escriba las credenciales, deberá especificar las credenciales que Analysis Services usa para conectarse al origen de datos al importar y procesar datos. En **modo de suplantación**, seleccione **suplantar cuenta**, a continuación, escriba las credenciales y, a continuación, haga clic en **Connect**. Se recomienda que usar una cuenta que la contraseña no caduca.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > El uso de una cuenta de usuario y una contraseña de Windows es el método más seguro de conexión a un origen de datos.
  
5.  En el navegador, seleccione el **AdventureWorksDW** de base de datos y, a continuación, haga clic en **Aceptar**. Esto crea la conexión a la base de datos. 
  
6.  En el navegador, seleccione la casilla de verificación para las siguientes tablas: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, y **FactInternetSales**.  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
Tras hacer clic en Aceptar, se abre el Editor de consultas. En la sección siguiente, seleccione solo los datos que desea importar.

  
## <a name="filter-the-table-data"></a>Filtrar los datos de tabla  

Tablas de la base de datos de ejemplo AdventureWorksDW tienen datos que no es necesarios incluir en el modelo. Cuando sea posible, desea filtrar los datos para ahorrar espacio en memoria que usa el modelo. Filtre algunas de las columnas de tablas por lo que no se importen en la base de datos del área de trabajo o la base de datos de modelo una vez que se haya implementado. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Para filtrar los datos de la tabla antes de importar  
  
1.  En el Editor de consultas, seleccione el **DimCustomer** tabla. Aparece una vista de la tabla DimCustomer en el origen de datos (la base de datos de ejemplo AdventureWorksDW). 
  
2.  Realice una selección múltiple (Ctrl + clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, a continuación, Haga clic en y, a continuación, haga clic en **quitar columnas**. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    Puesto que los valores de estas columnas no son pertinentes para el análisis de ventas por Internet, no hay necesidad de importarlas. Eliminación de columnas innecesarias, el modelo más pequeño y eficaz.  

    > [!TIP]
    > Si comete un error, puede hacer una copia mediante la eliminación de un paso en **pasos aplicados**.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  Filtrar las tablas restantes mediante la eliminación de las siguientes columnas en cada tabla:  
    
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
  
      No se quitan columnas.
  
## <a name="Import"></a>Import the selected tables and column data  

Ahora que ha muestra una vista previa y filtrar los datos innecesarios, puede importar el resto de los datos que desee. El asistente importa los datos de la tabla junto con todas las relaciones entre las tablas. Se crean nuevas tablas y columnas en el modelo y no se importarán los datos filtrados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar los datos de las columnas y las tablas seleccionadas  
  
1.  Revise las opciones seleccionadas. Si todo parece correcto, haga clic en **importación**. El cuadro de diálogo de procesamiento de datos muestra el estado de los datos que se va a importar desde el origen de datos a la base de datos del área de trabajo.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  Haga clic en **Cerrar**.  

  
## <a name="save-your-model-project"></a>Guarde el proyecto de modelo  

Es importante que guarde frecuentemente el proyecto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para guardar el proyecto de modelo  
  
-   Click **Archivo** > **Guardar todo**.  
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 3: Marcar como tabla de fechas](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md).

  
  
