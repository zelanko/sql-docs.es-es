---
title: "Lecci&#243;n 11: Crear particiones | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 11: Crear particiones
En esta lección, creará particiones para dividir la tabla Internet Sales en piezas lógicas más pequeñas que puedan procesarse (actualizarse) independientemente de otras particiones. De forma predeterminada, cada tabla que incluye en el modelo tiene una partición que incluye todas las columnas y filas de la tabla. Para las tabla Internet Sales, queremos dividir los datos por año, una partición para cada uno de los cinco años de la tabla.  Cada partición se podrá procesar entonces independientemente. Para obtener más información, consulte [Particiones &#40;SSAS tabular&#41;](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 10: Crear jerarquías](../analysis-services/lesson-10-create-hierarchies.md).  
  
## Crear particiones  
  
#### Para crear particiones en la tabla Internet Sales  
  
1.  En el diseñador de modelos, haga clic en la tabla **Internet Sales**, haga clic en el menú **Tabla** y luego en **Particiones**.  
  
    Se abrirá el cuadro de diálogo **Administrador de partición**.  
  
2.  En el cuadro de diálogo **Administrador de partición**, en la lista de particiones, haga clic en la partición **Internet Sales**.  
  
3.  En **Nombre de la partición**, cambie el nombre a **Ventas por Internet 2010**.  
  
    > [!TIP]  
    > Antes de continuar con el paso siguiente, observe que los nombres de columna de la ventana Vista previa de la tabla muestran las columnas incluidas (activadas) en la tabla del modelo con los nombres de columna del origen. Esto es porque la ventana Vista previa de la tabla muestra las columnas de la tabla de origen, no de la tabla del modelo.  
  
4.  Seleccione el botón **Editor de consultas** situado sobre el margen derecho de la ventana de vista previa.  
  
    Como desea que la partición solo incluya las filas de un determinado período, debe incluir una cláusula WHERE. Solo puede crear una cláusula WHERE usando una instrucción SQL.  
  
5.  En el campo **Instrucción SQL**, pegue la instrucción siguiente para reemplazar la instrucción existente:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    Esta instrucción especifica que la partición debe incluir todos los datos de las filas en las que OrderDate corresponda al año del calendario 2010, tal y como se especifica en la cláusula WHERE.  
  
6.  Haga clic en **Validar**.  
  
  
#### Para crear una partición para el año 2011  
  
1.  En la lista de particiones, haga clic en la partición **Ventas por Internet 2010** que acaba de crear y haga clic en **Copiar**.  
  
2.  En **Nombre de la partición**, escriba **Ventas por Internet 2011**.  
  
3.  En la instrucción SQL, para que la partición incluya solamente las filas del año 2011, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### Para crear una partición para el año 2012  
  
1.  En el cuadro de diálogo **Administrador de partición**, haga clic en **Copiar**.  
  
2.  En **Nombre de la partición**, escriba **Ventas por Internet 2012**.  
  
3.  En la instrucción SQL, para que la partición incluya solamente las filas del año 2012, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### Para crear una partición para el año 2013  
  
1.  En el cuadro de diálogo **Administrador de partición**, haga clic en **Nuevo**.  
  
2.  En **Nombre de la partición**, escriba **Ventas por Internet 2013**.  
  
3.  En la instrucción SQL, para que la partición incluya solamente las filas del año 2013, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### Para crear una partición para el año 2014 en la tabla Internet Sales  
  
1.  En el cuadro de diálogo **Administrador de partición**, haga clic en **Nuevo**.  
  
2.  En **Nombre de la partición**, escriba **Ventas por Internet 2014**.  
  
3.  En la instrucción SQL, para que la partición incluya solamente las filas del año 2014, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  
  
## Procesar particiones  
En el cuadro de diálogo **Administrador de partición**, observe el asterisco (**\***) situado junto a los nombres de particiones de cada una de las nuevas particiones que acaba de crear. Este asterisco indica que la partición no se ha procesado (actualizado). Cuando crea nuevas particiones, debe ejecutar una operación Procesar particiones o Procesar tabla para actualizar los datos de esas particiones.  
  
#### Para procesar particiones de Internet Sales  
  
1.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Administrador de partición**.  
  
2.  En el diseñador de modelos, haga clic en la tabla **Internet Sales**, después haga clic en el menú **Modelo**, elija **Procesar** (actualizar) y, después, haga clic en **Procesar las particiones**.  
  
3.  En el cuadro de diálogo **Procesar las particiones**, compruebe que **Modo** está establecido en **Proceso predeterminado**.  
  
4.  Active la casilla de la columna **Procesar** para cada una de las cinco particiones que ha creado y haga clic en **Aceptar**.  
  
    Si se le piden credenciales de suplantación, especifique el nombre de usuario y la contraseña de Windows que especificó en la lección 2, paso 6.  
  
    Aparece el cuadro de diálogo **Procesamiento de datos** con los detalles del proceso de cada partición. Observe que se ha transferido un número diferente de filas para cada partición. Esto es porque cada partición incluye solamente las filas del año especificado en la cláusula WHERE de la instrucción SQL. Cuando finalice el procesamiento, continúe y cierre el cuadro de diálogo Procesamiento de datos.  
  
  
  
## Pasos siguientes  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 12: Crear roles](../analysis-services/lesson-12-create-roles.md).  
  
  
  
