---
title: 'Lección 3: Definir un conjunto de datos para el informe de tabla (Reporting Services) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bc5ee5a106bf8b412f4096c06255be2e16f90a2f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594844"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lección 3: Definir un conjunto de datos para el informe de tabla (Reporting Services)
Después de definir el origen de datos, necesita definir un conjunto de datos. En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], los datos que usa en los informes proceden de un *conjunto de datos*. Un conjunto de datos incluye un puntero a un origen de datos y la consulta que usará para el informe, así como campos y variables calculados.  
  
Use el diseñador de consultas del Diseñador de informes para diseñar el conjunto de datos. En este tutorial, creará una consulta que recupere información sobre pedidos de ventas de la base de datos [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] .  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>Para definir una consulta de Transact-SQL para los datos de informe  
  
1.  En el panel **Datos de informe** , haga clic en **Nuevo**y, después, haga clic en **Conjunto de datos...**. Se abre el cuadro de diálogo **Propiedades del conjunto de datos** .  
  
2.  En el cuadro **Nombre** , escriba **AdventureWorksDataset**.  
  
3.  Haga clic en **Usar un conjunto de datos insertado en el informe**.  
  
4.  Seleccione el origen de datos que creó en la lección anterior, [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)].   
5. Seleccione **Texto** en el **Tipo de consulta**.  
  
6.  Escriba o copie y pegue la siguiente consulta de Transact-SQL en el cuadro **Consulta** .  
  
    ```  
    SELECT   
       soh.OrderDate AS [Date],   
       soh.SalesOrderNumber AS [Order],   
       pps.Name AS Subcat, pp.Name as Product,    
       SUM(sd.OrderQty) AS Qty,  
       SUM(sd.LineTotal) AS LineTotal  
    FROM Sales.SalesPerson sp   
       INNER JOIN Sales.SalesOrderHeader AS soh   
          ON sp.BusinessEntityID = soh.SalesPersonID  
       INNER JOIN Sales.SalesOrderDetail AS sd   
          ON sd.SalesOrderID = soh.SalesOrderID  
       INNER JOIN Production.Product AS pp   
          ON sd.ProductID = pp.ProductID  
       INNER JOIN Production.ProductSubcategory AS pps   
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID  
       INNER JOIN Production.ProductCategory AS ppc   
          ON ppc.ProductCategoryID = pps.ProductCategoryID  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,   
       soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'  
    ```  
  
7.  (Opcional) Haga clic en el botón **Diseñador de consultas** . La consulta se muestra en el Diseñador de consultas basado en texto. Puede cambiar al diseñador gráfico de consultas si hace clic en **Editar como texto**. Para ver los resultados de la consulta, haga clic en el botón ejecutar ![ssrs_querydesigner_run](../reporting-services/media/ssrs-querydesigner-run.png)  de la barra de herramientas del diseñador de consultas.  
  
    Verá los datos procedentes de seis campos de cuatro tablas distintas de la base de datos [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . La consulta utiliza funcionalidad de Transact-SQL como los alias. Por ejemplo, la tabla SalesOrderHeader se denomina *soh*.  
  
8.  Haga clic en **Aceptar** para salir del diseñador de consultas.  
  
9.  Haga clic en **Aceptar** para salir del cuadro de diálogo **Propiedades del conjunto de datos** .  
  
    El conjunto de datos **AdventureWorksDataset** y los campos aparecen en el panel Datos de informe.  
    ![ssrs_adventureworksdataset](../reporting-services/media/ssrs-adventureworksdataset.png)  
  
## <a name="next-task"></a>Tarea siguiente  
Ha especificado correctamente una consulta que recupera datos para su informe. A continuación, creará el diseño para el informe. Vea [Lección 4: Agregar una tabla al informe &#40;Reporting Services&#41;](../reporting-services/lesson-4-adding-a-table-to-the-report-reporting-services.md).  
  
## <a name="see-also"></a>Ver también  
[Herramientas de diseño de consulta &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)  
[Tipo de conexión de SQL Server &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)  
[Tutorial: Escribir instrucciones Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
  

