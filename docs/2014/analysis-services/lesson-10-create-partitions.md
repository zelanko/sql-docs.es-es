---
title: 'Lección 11: Creación de particiones | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0817db540c9db8f17fbc71da68f43cc68645190
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729484"
---
# <a name="lesson-11-create-partitions"></a>Lección 11: Crear particiones
  En esta lección, creará particiones para dividir la tabla Internet Sales en piezas lógicas más pequeñas que puedan procesarse (actualizarse) independientemente de otras particiones. De forma predeterminada, cada tabla que se incluye en el modelo tiene una partición que incluye todas las columnas y filas de la tabla. Para la tabla Internet Sales, queremos dividir los datos por año; una partición para cada uno de cinco años de la tabla.  Cada partición se podrá procesar entonces independientemente. Para obtener más información, consulte [Particiones &#40;SSAS tabular&#41;](tabular-models/partitions-ssas-tabular.md).  
  
 Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 10: Crear jerarquías](lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Crear particiones  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>Para crear particiones en la tabla Internet Sales  
  
1.  En el diseñador de modelos, haga clic en la tabla **Internet Sales** , haga clic en el menú **Tabla** y luego en **Particiones**.  
  
     Se abrirá el cuadro de diálogo **Administrador de partición** .  
  
2.  En el **Partition Manager** cuadro de diálogo **particiones**, haga clic en el **Internet Sales** partición.  
  
3.  En **nombre de la partición**, cambie el nombre a `Internet Sales 2005`.  
  
    > [!TIP]  
    >  Antes de continuar con el paso siguiente, observe que los nombres de columna de la ventana Vista previa de la tabla muestran las columnas incluidas (activadas) en la tabla del modelo con los nombres de columna del origen. Esto es porque la ventana Vista previa de la tabla muestra las columnas de la tabla de origen, no de la tabla del modelo.  
  
4.  Seleccione el botón **Editor de consultas** situado sobre el margen derecho de la ventana de vista previa.  
  
     Como desea que la partición solo incluya las filas de un determinado período, debe incluir una cláusula WHERE. Solo puede crear una cláusula WHERE usando una instrucción SQL.  
  
5.  En el campo **Instrucción SQL** , pegue la instrucción siguiente para reemplazar la instrucción existente:  
  
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
    WHERE (([OrderDate] >= N'2005-01-01 00:00:00') AND ([OrderDate] < N'2006-01-01 00:00:00'))  
    ```  
  
     Esta instrucción especifica que la partición debe incluir todos los datos de las filas en las que OrderDate corresponda al año del calendario 2005, tal como se especifica en la cláusula WHERE.  
  
6.  Haga clic en **Validar**.  
  
     Observe que se muestra una advertencia en la que se indica que algunas columnas no existen en el origen. Esto es porque en [lección 3: Cambiar el nombre de las columnas](rename-columns.md), cambió el nombre de las columnas de la tabla de ventas por Internet en el modelo sea distinto de las columnas en el origen.  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>Para crear una partición para el año 2006 en la tabla de ventas por Internet  
  
1.  En el **Partition Manager** cuadro de diálogo **particiones**, haga clic en el `Internet Sales 2005` partición que acaba de crear y, a continuación, **copia**.  
  
2.  En **nombre de la partición**, tipo `Internet Sales 2006`.  
  
3.  En la instrucción SQL, en orden para la partición incluya solamente las filas del año 2006, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>Para crear una partición para el año 2007 en la tabla de ventas por Internet  
  
1.  En el cuadro de diálogo **Administrador de partición** , haga clic en **Copiar**.  
  
2.  En **nombre de la partición**, tipo `Internet Sales 2007`.  
  
3.  En **cambiar a**, seleccione **Editor de consultas**.  
  
4.  En la instrucción SQL, en orden para la partición incluya solamente las filas del año 2007, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>Para crear una partición para el año 2008 en la tabla de ventas por Internet  
  
1.  En el cuadro de diálogo **Administrador de partición** , haga clic en **Nuevo**.  
  
2.  En **nombre de la partición**, tipo `Internet Sales 2008`.  
  
3.  En **cambiar a**, seleccione **Editor de consultas**.  
  
4.  En la instrucción SQL, en orden para la partición incluya solamente las filas del año 2008, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>Para crear una partición para el año 2009 en la tabla Internet Sales  
  
1.  En el cuadro de diálogo **Administrador de partición** , haga clic en **Nuevo**.  
  
2.  En **nombre de la partición**, tipo `Internet Sales 2009`.  
  
3.  En **cambiar a**, seleccione **Editor de consultas**.  
  
4.  En la instrucción SQL, para que la partición incluya solamente las filas del año 2009, reemplace la cláusula WHERE por lo siguiente:  
  
    ```  
    WHERE (([OrderDate] >= N'2009-01-01 00:00:00') AND ([OrderDate] < N'2010-01-01 00:00:00'))  
    ```  
  
## <a name="process-partitions"></a>Procesar particiones  
 En el cuadro de diálogo **Administrador de partición** , observe el asterisco (**\***) situado junto a los nombres de particiones de cada una de las nuevas particiones que acaba de crear. Este asterisco indica que la partición no se ha procesado (actualizado). Cuando crea nuevas particiones, debe ejecutar una operación Procesar particiones o Procesar tabla para actualizar los datos de esas particiones.  
  
#### <a name="to-process-internet-sales-partitions"></a>Para procesar particiones de Internet Sales  
  
1.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Administrador de partición** .  
  
2.  En el diseñador de modelos, haga clic en la tabla **Internet Sales** , después haga clic en el menú **Modelo** , elija **Procesar** (actualizar) y, después, haga clic en **Procesar las particiones**.  
  
3.  En el cuadro de diálogo **Procesar las particiones** , compruebe que **Modo** está establecido en **Proceso predeterminado**.  
  
4.  Active la casilla de la columna **Procesar** para cada una de las cinco particiones que ha creado y haga clic en **Aceptar**.  
  
     Si se le piden credenciales de suplantación, especifique el nombre de usuario y la contraseña de Windows que especificó en la lección 2, paso 6.  
  
     El **proceso datos** , a continuación, aparecerá el cuadro de diálogo y muestra los detalles del proceso para cada partición. Observe que se ha transferido un número diferente de filas para cada partición. Esto es porque cada partición incluye solamente las filas del año especificado en la cláusula WHERE de la instrucción SQL. No hay datos para el año 2010.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: Lección: [Lección 12: Crear Roles](lesson-11-create-roles.md).  
  
  
