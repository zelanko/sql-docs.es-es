---
title: "Editor de origen de ODBC (p&#225;gina Salida de error) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.odbcsource.errorhandling.f1"
ms.assetid: b2f6866c-db07-4cb3-9f38-889f8d2b03e6
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor de origen de ODBC (p&#225;gina Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de origen de ODBC** para seleccionar las opciones de control de errores.  
  
 Para obtener más información acerca del origen de ODBC, vea [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Lista de tareas  
 **Para abrir la página Salida de error del Editor de origen de ODBC**  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
-   En la pestaña **Flujo de datos**, haga doble clic en el origen ODBC.  
  
-   En el **Editor de origen de ODBC**, haga clic en **Salida de error**.  
  
## Opciones  
  
### Entrada/salida  
 Muestra el nombre del origen de datos.  
  
### Columna  
 No se usa.  
  
### Error  
 Seleccione la forma en la que el origen de ODBC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### Truncamiento  
 Seleccione la forma en la que el origen de ODBC debe controlar el truncamiento en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### Description  
 No se usa.  
  
### Establecer este valor en las celdas seleccionadas  
 Seleccione cómo el origen de ODBC va a controlar todas las celdas seleccionadas cuando se produzca un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### Aplicar  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
## Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el origen de ODBC controla errores y truncamientos.  
  
### Error de componente  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Éste es el comportamiento predeterminado.  
  
### Omitir error  
 Se omite el error o el truncamiento.  
  
### Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del origen de ODBC. Para más información, consulte [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Vea también  
 [Editor de orígenes ODBC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Editor de orígenes ODBC &#40;página Columnas&#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)  
  
  