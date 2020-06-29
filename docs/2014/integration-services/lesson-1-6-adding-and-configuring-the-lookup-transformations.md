---
title: 'Paso 6: Agregar y configurar transformaciones de búsqueda | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3798dd0632522cf68b1b73976b7f4b932b257c0f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440692"
---
# <a name="step-6-adding-and-configuring-the-lookup-transformations"></a>Paso 6: Adición y configuración de transformaciones de búsqueda
  Tras configurar el origen de archivo plano para extraer datos del archivo de origen, la siguiente tarea consiste en definir las transformaciones de búsqueda necesarias para obtener los valores para las claves **CurrencyKey** y **DateKey**. Una transformación Búsqueda realiza una búsqueda combinando datos de la columna de entrada especificada en una columna de un conjunto de datos de referencia. El conjunto de datos de referencia puede ser una tabla o una vista existente, una tabla nueva o el resultado de una instrucción SQL. En este tutorial, la transformación Búsqueda utiliza un administrador de conexiones OLE DB para conectar con la base de datos que contiene los datos que constituyen el origen del conjunto de datos de referencia.  
  
> [!NOTE]  
>  También puede configurar la transformación de Búsqueda para conectar con una caché que contiene el conjunto de datos de referencia. Para obtener más información, vea [lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
 Para este tutorial, agregará y configurará los dos componentes de la transformación Búsqueda en el paquete:  
  
-   Una transformación para realizar una búsqueda de valores de la columna **CurrencyKey** de la tabla de dimensiones **DimCurrency** basada en la coincidencia de valores de la columna **CurrencyID** del archivo plano.  
  
-   Una transformación para realizar una búsqueda de valores de la columna **DateKey** de la tabla de dimensiones **DimDate** basada en la coincidencia de valores de la columna **CurrencyDate** del archivo plano.  
  
 En ambos casos, la transformación de búsqueda usará el administrador de conexiones OLE DB creado anteriormente.  
  
### <a name="to-add-and-configure-the-lookup-currency-key-transformation"></a>Para agregar y configurar la transformación Lookup Currency Key  
  
1.  En el **cuadro de herramientas de SSIS**, expanda **común**y arrastre **búsqueda** en la superficie de diseño de la pestaña **flujo de datos** . Coloque la búsqueda directamente debajo del origen de **datos Extract Sample Currency** .  
  
2.  Haga clic en el origen de archivo plano **Extract Sample Currency Data** y arrastre la flecha verde a la transformación **Búsqueda** que acaba de agregar para conectar los dos componentes.  
  
3.  En la superficie de diseño **Flujo de datos** , haga clic en **Búsqueda** en la transformación **Búsqueda** y cambie el nombre por **Lookup Currency Key**.  
  
4.  Haga doble clic en la transformación **Lookup CurrencyKey** para mostrar el Editor de transformación Búsqueda.  
  
5.  En la página **General** , realice las selecciones siguientes:  
  
    1.  Seleccione **Caché completa**.  
  
    2.  En el área **Tipo de conexión** , seleccione **Administrador de conexiones OLE DB**.  
  
6.  En la página **Conexión** , realice las selecciones siguientes:  
  
    1.  En el cuadro de diálogo **Administrador de conexiones OLE DB** , asegúrese de que se muestra **localhost.AdventureWorksDW2012** .  
  
    2.  Seleccione **Usar los resultados de una consulta SQL**y, a continuación, escriba o copie la instrucción SQL siguiente:  
  
        ```  
        select * from (select * from [dbo].[DimCurrency]) as refTable  
        where [refTable].[CurrencyAlternateKey] = 'ARS'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'AUD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'BRL'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CAD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'CNY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'DEM'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'EUR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'FRF'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'GBP'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'JPY'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'MXN'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'SAR'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'USD'  
        OR  
        [refTable].[CurrencyAlternateKey] = 'VEB'  
        ```  
  
7.  En la página **Columnas** , realice las selecciones siguientes:  
  
    1.  En el panel **Columnas de entrada disponibles** , arrastre **CurrencyID** al panel **Columnas de búsqueda disponibles** y suéltelo en **CurrencyAlternateKey**.  
  
    2.  En la lista **Columnas de búsqueda disponibles** , active la casilla situada a la izquierda de **CurrencyKey**.  
  
8.  Haga clic en **Aceptar** para volver a la superficie de diseño **Flujo de datos** .  
  
9. Haga clic con el botón derecho en la transformación Lookup Currency Key y haga clic en **Propiedades**.  
  
10. En el ventana Propiedades, compruebe que la `LocaleID` propiedad está establecida en **inglés (Estados Unidos)** y que la propiedad **DefaultCodePage** está establecida en **1252**.  
  
### <a name="to-add-and-configure-the--lookup-datekey-transformation"></a>Para agregar y configurar la transformación Lookup Date Key  
  
1.  En el **cuadro de herramientas de SSIS**, arrastre **Búsqueda** a la superficie de diseño **Flujo de datos** . Coloque Búsqueda justo debajo de la transformación **Lookup Currency Key** .  
  
2.  Haga clic en la transformación **Lookup Currency Key** y arrastre la flecha verde hasta la transformación **Búsqueda** que acaba de agregar para conectar los dos componentes.  
  
3.  En el cuadro de diálogo **Selección de entrada y salida** , en el cuadro de lista **Salida** , haga clic en **Salida de entradas coincidentes de búsqueda** y, a continuación, haga clic en **Aceptar**.  
  
4.  En la superficie de diseño **Flujo de datos** , haga clic en **Búsqueda** en la transformación **Búsqueda** recién agregada y cambie el nombre por **Lookup Date Key**.  
  
5.  Haga doble clic en la transformación **Lookup Date Key** .  
  
6.  En la página **General** , seleccione **Caché parcial**.  
  
7.  En la página **Conexión** , realice las selecciones siguientes:  
  
    1.  En el cuadro de diálogo **Administrador de conexiones OLEDB** , asegúrese de que se muestra **localhost.AdventureWorksDW2012** .  
  
    2.  En el cuadro **Usar una tabla o vista** , escriba o seleccione **[dbo].[DimDate]**.  
  
8.  En la página **Columnas** , realice las selecciones siguientes:  
  
    1.  En el panel **Columnas de entrada disponibles** , arrastre **CurrencyDate** al panel **Columnas de búsqueda disponibles** y suéltelo en **FullDateAlternateKey**.  
  
    2.  En la lista **Columnas de búsqueda disponibles** , active la casilla situada a la izquierda de **DateKey**.  
  
9. En la página **Avanzadas** , revise las opciones de almacenamiento en memoria caché.  
  
10. Haga clic en **Aceptar** para volver a la superficie de diseño **Flujo de datos** .  
  
11. Haga clic con el botón derecho en la transformación Lookup Date Key y haga clic en **Propiedades.**  
  
12. En el ventana Propiedades, compruebe que la `LocaleID` propiedad está establecida en **inglés (Estados Unidos)** y que la propiedad **DefaultCodePage** está establecida en **1252**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 7: Adición y configuración del destino de OLE DB](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>Consulte también  
 [Transformación Búsqueda](data-flow/transformations/lookup-transformation.md)  
  
  
