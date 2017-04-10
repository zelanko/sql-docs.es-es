---
title: "Configurar el registro utilizando un archivo de configuraci&#243;n guardado | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contenedores [Integration Services], registros"
  - "registros [Integration Services], contenedores"
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Configurar el registro utilizando un archivo de configuraci&#243;n guardado
  Este procedimiento describe cómo configurar el registro para los contenedores nuevos de un paquete, cargando un archivo de configuración de registro previamente guardado.  
  
 De manera predeterminada, todos los contenedores de un paquete utilizan la misma configuración de registro que el contenedor principal. Por ejemplo, las tareas de un bucle ForEach utilizan la misma configuración de registro que el bucle ForEach.  
  
### Para configurar el registro para un contenedor  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el menú **SSIS** , haga clic en **Registro**.  
  
3.  Expanda la vista de árbol del paquete y seleccione el contenedor que desee configurar.  
  
4.  En la pestaña **Proveedores y registros** , seleccione los registros que desee utilizar para el contenedor.  
  
    > [!NOTE]  
    >  Solo puede crear registros en el nivel de paquete. Para más información, vea [Habilitar el registro de paquetes en SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md).  
  
5.  Haga clic en la pestaña **Detalles** y, a continuación, en **Cargar**.  
  
6.  Localice el archivo de configuración del registro que desee utilizar y haga clic en **Abrir**.  
  
7.  También puede seleccionar una entrada diferente del registro al activar la casilla correspondiente en la columna **Eventos** . Haga clic en **Avanzadas** para seleccionar el tipo de información que se debe registrar para esta entrada.  
  
    > [!NOTE]  
    >  El nuevo contenedor puede incluir entradas de registro adicionales que no estén disponibles para el contenedor utilizado originalmente para crear la configuración del registro. Es necesario seleccionar manualmente estas entradas adicionales para que se registren.  
  
8.  Para guardar la versión actualizada de la configuración de registro, haga clic en **Guardar**.  
  
9. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## Vea también  
 [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  