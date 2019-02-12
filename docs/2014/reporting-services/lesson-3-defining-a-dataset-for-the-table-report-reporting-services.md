---
title: 'Lección 3: Definir un conjunto de datos para el informe de tabla (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3f57ec59753e7539107c652d60f7a00959f95cbb
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56009677"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lección 3: Definir un conjunto de datos para el informe de tabla (Reporting Services)
  Después de definir el origen de datos, necesita definir un conjunto de datos. En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], los datos que usa en los informes proceden de un *conjunto de datos*. Un conjunto de datos incluye un puntero a un origen de datos y la consulta que usará para el informe, así como campos y variables calculados.  
  
 Puede usar el Diseñador de consultas del Diseñador de informes para diseñar la consulta. Para este tutorial, creará una consulta que recupera información de pedido de ventas desde la [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] **2008** base de datos.  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>Para definir una consulta de Transact-SQL para los datos de informe  
  
1.  En el panel **Datos de informe**, haga clic en **Nuevo** y después en **Conjunto de datos...**. Se abre el cuadro de diálogo **Propiedades del conjunto de datos** .  
  
2.  En el cuadro **Nombre** , escriba **AdventureWorksDataset**.  
  
3.  Haga clic en **Usar un conjunto de datos insertado en el informe**.  
  
4.  Asegúrese de que el nombre del origen de datos, AdventureWorks2012, está en el **origen de datos** cuadro de texto y que la **tipo de consulta** es **texto**.  
  
5.  Escriba o copie y pegue la siguiente consulta de Transact-SQL en el cuadro **Consulta** .  
  
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
  
6.  (Opcional) Haga clic en el botón **Diseñador de consultas** . La consulta se muestra en el Diseñador de consultas basado en texto. Puede cambiar al diseñador gráfico de consultas si hace clic en **Editar como texto**. Ver los resultados de la consulta haciendo clic en la ejecución **(!)**  botón en la barra de herramientas Diseñador de consultas.  
  
     Verá los datos procedentes de seis campos de cuatro tablas distintas de la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . La consulta utiliza funcionalidad de Transact-SQL como los alias. Por ejemplo, la tabla SalesOrderHeader se denomina soh.  
  
     Haga clic en **Aceptar** para salir del diseñador de consultas.  
  
7.  Haga clic en **Aceptar** para salir del cuadro de diálogo **Propiedades del conjunto de datos** .  
  
     El conjunto de datos **AdventureWorksDataset** y los campos aparecen en el panel Datos de informe.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha especificado correctamente una consulta que recupera datos para su informe. A continuación, creará el diseño para el informe. Consulte [lección 4: Agregar una tabla al informe &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de diseño de herramientas de datos del servidor de informes SQL Diseñador de consultas &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [Tipo de conexión de SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [Tutorial: Escribir instrucciones Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
