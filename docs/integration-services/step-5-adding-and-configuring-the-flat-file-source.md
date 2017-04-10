---
title: "Paso 5: Agregar y configurar el origen de archivo plano | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Paso 5: Agregar y configurar el origen de archivo plano
En esta tarea, agregará un origen de archivo plano al paquete y configurará dicho origen. Un origen de archivo plano es un componente de flujo de datos que utiliza metadatos definidos por un administrador de conexiones de archivo plano para especificar el formato y la estructura de los datos que deben extraerse del archivo plano mediante un proceso de transformación. El origen de archivo plano puede configurarse para extraer datos de un único archivo plano utilizando la definición de formato de archivo proporcionada por el administrador de conexiones de archivo plano.  
  
Para este tutorial, configurará el origen de archivo plano para utilizar el administrador de conexiones **Sample Flat File Source Data** creado con anterioridad.  
  
### Para agregar un componente de origen de archivo plano  
  
1.  Abra el diseñador **Flujo de datos** haciendo doble clic en la tarea de flujo de datos **Extract Sample Currency Data** o haciendo clic en la **pestaña Flujo de datos**.  
  
2.  En el **cuadro de herramientas de SSIS**, expanda **Otros orígenes** y, después, arrastre un **Origen de archivo plano** a la superficie de diseño de la pestaña **Flujo de datos**.  
  
3.  En la superficie de diseño **Flujo de datos**, haga clic con el botón derecho en el **Origen de archivo plano** que acaba de agregar, haga clic en **Cambiar nombre** y cambie el nombre por **Extract Sample Currency Data**.  
  
4.  Haga doble clic en el origen del archivo plano para abrir el cuadro de diálogo Editor de origen de archivos planos.  
  
5.  En el cuadro **Administrador de conexiones de archivos planos** , seleccione **Sample Flat File Source Data**.  
  
6.  Haga clic en **Columnas** y compruebe que los nombres de las columnas son correctos.  
  
7.  Haga clic en **Aceptar**.  
  
8.  Haga clic con el botón derecho en el origen del archivo plano y haga clic en **Propiedades**.  
  
9. En la ventana Propiedades, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos)**.  
  
## Siguiente tarea de la lección  
[Paso 6: Agregar y configurar transformaciones de búsqueda](../integration-services/step-6-adding-and-configuring-the-lookup-transformations.md)  
  
## Vea también  
[Origen de archivo plano](../integration-services/data-flow/flat-file-source.md)  
[Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
  
  
