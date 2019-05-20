---
title: 'Lección 3: Definir un conjunto de datos para el informe de tabla (Reporting Services) | Microsoft Docs'
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eaa2af570ae363e6a48c8d14e5b73c70e6790b5c
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106030"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lección 3: Definir un conjunto de datos para el informe de tabla (Reporting Services)

Después de definir el origen de datos, necesita definir un conjunto de datos. En [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)], los datos que usa en los informes proceden de un *conjunto de datos*. Un conjunto de datos incluye un puntero a un origen de datos y la consulta que usará para el informe, los campos calculados y las variables.

Use el Diseñador de consultas del Diseñador de informes para definir el conjunto de datos. En este tutorial, va a crear una consulta que recupera la información sobre los pedidos de ventas de la base de datos AdventureWorks2016.

## <a name="define-a-transact-sql-query-for-report-data"></a>Definición de una consulta Transact-SQL para los datos de informe  

1. En el panel **Datos de informe**, seleccione **Nuevo** > **Conjunto de datos...**. El cuadro de diálogo **Propiedades del conjunto de datos** se abre y en él se muestra la sección **Consulta**.

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. En el cuadro de texto **Nombre**, escriba "AdventureWorksDataset".

3. Debajo, seleccione el botón de radio **Usar un conjunto de datos incrustado en el informe**.

4. En el cuadro de texto **Origen de datos**, seleccione AdventureWorks2016.

5. En **Tipo de consulta**, seleccione el botón de radio **Texto**.

6. Escriba o copie y pegue la siguiente consulta de Transact-SQL en el cuadro de texto **Consulta**.

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
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
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. (Opcional) Seleccione el botón **Diseñador de consultas**. La consulta se muestra en el *Diseñador de consultas* basado en texto. Para ver los resultados de la consulta, seleccione el botón ![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png) **Ejecutar** de la barra de herramientas del **Diseñador de consultas**. El conjunto de datos mostrado contiene seis campos de cuatro tablas de la base de datos AdventureWorks2016. La consulta utiliza funcionalidad de Transact-SQL como los alias. Por ejemplo, la tabla SalesOrderHeader se denomina *soh*.

8. Seleccione **Aceptar** para salir del **Diseñador de consultas**.

9. Seleccione **Aceptar** para salir del cuadro de diálogo **Propiedades del conjunto de datos**.

El panel **Datos de informe** muestra el conjunto de datos y los campos de AdventureWorksDataset.

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>Pasos siguientes

Ha especificado correctamente una consulta que recupera datos para su informe. A continuación, va a crear el diseño del informe. Continúe con la [Lección 4: Agregar una tabla al informe &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md).

## <a name="see-also"></a>Vea también

[Herramientas de diseño de consulta &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)
[Tipo de conexión de SQL Server &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[Tutorial: Escribir instrucciones Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
