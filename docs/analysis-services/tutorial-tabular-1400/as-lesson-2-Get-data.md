---
title: 'Lección de Analysis Services tutorial 2: obtener datos | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb7c9b19950036baff8dbe4dd52447040cd9a571
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="get-data"></a>Obtener datos

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, utiliza **obtener datos** para conectarse a la base de datos de ejemplo AdventureWorksDW, seleccionar datos, la vista previa y filtrar y, a continuación, importar el área de trabajo del modelo.  
  
Si usa obtener datos, puede importar datos desde una gran variedad de orígenes. También se pueden consultar los datos mediante una expresión de la fórmula de Power Query M o [expresión de consulta SQL nativo](../tabular-models/ssas-import-query.md).

> [!NOTE]
> Las tareas y las imágenes en este tutorial muestran cómo establecer una conexión a una base de datos de AdventureWorksDW2014 en un servidor local. En algunos casos, una base de datos AdventureWorksDW en almacenamiento de datos de SQL Azure puede mostrar diferentes objetos; Sin embargo, fundamentalmente son iguales.
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 1: crear un nuevo proyecto de modelo tabular](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Crear una conexión  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>Para crear una conexión a la base de datos AdventureWorksDW  
  
1.  En **Explorador de modelos tabulares**, haga clic en **orígenes de datos** > **importar desde el origen de datos**.  
  
    Esto inicia **obtener datos**, que le guiará a través de conectarse a un origen de datos. Si no ve el Explorador de modelos tabulares, en **el Explorador de soluciones**, haga doble clic en **Model.bim** para abrir el modelo en el diseñador. 
    
    ![getdata como lesson2](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  En obtener datos, haga clic en **base de datos** > **base de datos de SQL Server** > **conectar**.  
  
3.  En el **base de datos de SQL Server** cuadro de diálogo, en **Server**, escriba el nombre del servidor donde instaló la base de datos AdventureWorksDW y, a continuación, haga clic en **conectar**.  

4.  Cuando se le pida que escriba las credenciales, debe especificar las credenciales de que Analysis Services se utiliza para conectarse al origen de datos al importar y procesar datos. En **modo de suplantación**, seleccione **suplantar a la cuenta**, a continuación, escriba las credenciales y, a continuación, haga clic en **conectar**. Se recomienda que usar una cuenta que la contraseña no caduca.

    ![lesson2-cuenta](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > El uso de una cuenta de usuario y una contraseña de Windows es el método más seguro de conexión a un origen de datos.
  
5.  En el navegador, seleccione la **AdventureWorksDW** la base de datos y, a continuación, haga clic en **Aceptar**. Esto crea la conexión con la base de datos. 
  
6.  En el navegador, active la casilla de verificación para las siguientes tablas: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, y **FactInternetSales**.  

    ![como-lesson2-seleccione-tablas](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
Tras hacer clic en Aceptar, se abre el Editor de consultas. En la sección siguiente, seleccione sólo los datos que desea importar.

  
## <a name="filter-the-table-data"></a>Filtrar los datos de tabla  

Tablas de la base de datos de ejemplo AdventureWorksDW tienen datos que no es necesarios incluir en el modelo. Cuando sea posible, en el que desea filtrar los datos innecesarios para ahorrar espacio en la memoria utilizada por el modelo. Filtra algunas de las columnas de tablas por lo que no está importados en la base de datos del área de trabajo o la base de datos de modelo una vez que se haya implementado. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Para filtrar los datos de la tabla antes de importar  
  
1.  En el Editor de consultas, seleccione la **DimCustomer** tabla. Aparece una vista de la tabla DimCustomer en el origen de datos (la base de datos de ejemplo AdventureWorksDW). 
  
2.  Realice una selección múltiple (Ctrl + clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, a continuación, menú contextual y, a continuación, haga clic en **quitar columnas**. 

    ![como-lesson2-remove-columnas](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    Puesto que los valores de estas columnas no son pertinentes para el análisis de ventas por Internet, no hay necesidad de importarlas. Eliminación de columnas innecesarias hace que el modelo más pequeño y eficaz.  

    > [!TIP]
    > Si comete un error, puede hacer una copia mediante la eliminación de un paso en **pasos aplicados**.   
    
    ![como-lesson2-remove-columnas](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  Filtre las tablas restantes mediante la eliminación de las siguientes columnas en cada tabla:  
    
    **DimDate**
    
      |Columna|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Columna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Columna|  
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
  
      |Columna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Columna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      No se quitan columnas.
  
## <a name="Import"></a>Import the selected tables and column data  

Ahora que ha obtenido una vista previa y filtran los datos innecesarios, puede importar el resto de los datos que desea. El asistente importa los datos de la tabla junto con todas las relaciones entre las tablas. Se crean nuevas tablas y columnas en el modelo y datos que filtró no se importará.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar los datos de las columnas y las tablas seleccionadas  
  
1.  Revise las opciones seleccionadas. Si todo parece correcto, haga clic en **importación**. El cuadro de diálogo de procesamiento de datos muestra el estado de los datos que se va a importar desde el origen de datos en la base de datos del área de trabajo.
  
    ![éxito como lesson2](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  Haga clic en **Cerrar**.  

  
## <a name="save-your-model-project"></a>Guarde el proyecto de modelo  

Es importante que guarde frecuentemente el proyecto de modelos.  
  
#### <a name="to-save-the-model-project"></a>Para guardar el proyecto de modelo  
  
-   Click **Archivo** > **Guardar todo**.  
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 3: Marcar como tabla de fechas](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md).

  
  
