---
title: "Configurar una salida de error en un componente de flujo de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "errores [Integration Services], componentes de flujo de datos"
  - "componentes [Integration Services], flujo de datos"
  - "salidas de errores [Integration Services]"
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# Configurar una salida de error en un componente de flujo de datos
  Un gran número de componentes de flujo de datos admiten salidas de errores y, dependiendo del componente, el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] proporciona diferentes maneras de configurar una salida de error. Además de configurar una salida de error, también puede configurar sus columnas correspondientes. Esto incluye configurar las columnas **ErrorCode** y **ErrorColumn** agregadas por el componente.  
  
## Configurar una salida de error  
 Para configurar una salida de error, tiene dos opciones:  
  
-   Utilice el cuadro de diálogo **Configurar la salida de errores** . Puede usar este cuadro de diálogo para configurar una salida de error en cualquier componente de flujo de datos que la admita.  
  
-   Utilice el cuadro de diálogo del editor para el componente. Algunos componentes permiten configurar directamente salidas de errores en el cuadro de diálogo de su editor. Sin embargo, no se pueden configurar salidas de errores en el cuadro de diálogo del editor para el origen de ADO NET, la transformación Importar columna, la transformación Comando de OLE DB o el destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Los procedimientos siguientes describen cómo utilizar estos cuadros de diálogo para configurar salidas de errores.  
  
#### Para configurar una salida de error mediante el cuadro de diálogo Configurar la salida de errores  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de datos** .  
  
4.  Arrastre la salida de error, representada por una flecha roja, del componente de origen de los errores a otro componente de flujo de datos.  
  
5.  En el cuadro de diálogo **Configurar la salida de errores** , seleccione una acción de las columnas **Error** y **Truncamiento** para cada columna de la entrada de componentes.  
  
6.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
#### Para agregar una salida de error mediante el cuadro de diálogo del editor para el componente  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de datos** .  
  
4.  Haga doble clic en los componentes de flujo de datos en los que desee configurar una salida de error y, en función del componente, realice una de las siguientes acciones:  
  
    -   Haga clic en **Configurar la salida de errores**.  
  
    -   Haga clic en **Salida de error**.  
  
5.  Establezca la opción **Error** para cada columna.  
  
6.  Establezca la opción **Truncamiento** para cada columna.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## Configurar columnas de salida de error  
 Para configurar columnas de salida de error, tiene que utilizar la pestaña **Propiedades de entrada y salida** del cuadro de diálogo **Editor avanzado** .  
  
#### Para configurar columnas de salida de error  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de datos** .  
  
4.  Haga clic con el botón derecho en el componente cuyas columnas de salida de error quiere configurar y haga clic en **Mostrar editor avanzado**.  
  
5.  Haga clic en la pestaña **Propiedades de entrada y salida** y expanda **Salida de error de \<nombre de componente>** y, después, expanda **Columnas de salida**.  
  
6.  Haga clic en una columna y actualice sus propiedades.  
  
    > [!NOTE]  
    >  La lista de columnas incluye las columnas de la entrada de componentes, las columnas **ErrorCode** y **ErrorColumn** agregadas por salidas de errores previas, y las columnas **ErrorCode** y **ErrorColumn** agregadas por este componente.  
  
7.  Haga clic en **Aceptar.**  
  
8.  Para guardar el paquete actualizado, en el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
## Vea también  
 [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md)  
  
  