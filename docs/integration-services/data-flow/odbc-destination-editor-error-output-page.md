---
title: "Editor de destinos de ODBC (p&#225;gina Salida de error) | Microsoft Docs"
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
  - "sql13.ssis.designer.odbcdest.errorhandling.f1"
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Editor de destinos de ODBC (p&#225;gina Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de destinos de ODBC** para seleccionar las opciones de control de errores.  
  
 Para obtener más información acerca del destino de ODBC, vea [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).  
  
 **Para abrir la página Salida de error del Editor de destinos de ODBC**  
  
## Lista de tareas  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el destino de ODBC.  
  
-   En la pestaña **Flujo de datos**, haga doble clic en el destino de ODBC.  
  
-   En el **Editor de destinos de ODBC**, haga clic en **Salida de error**.  
  
## Opciones  
  
### Entrada/salida  
 Muestra el nombre del origen de datos.  
  
### Columna  
 No se usa.  
  
### Error  
 Seleccione la forma en la que el destino de ODBC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### Truncamiento  
 Seleccione la forma en la que el destino de ODBC debe controlar los truncamientos en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### Description  
 Muestra una descripción del error.  
  
### Establecer este valor en las celdas seleccionadas  
 Seleccione la forma en la que el destino de ODBC controla todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
### Aplicar  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
## Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el destino de ODBC controla errores y truncamientos.  
  
### Error de componente  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Éste es el comportamiento predeterminado.  
  
### Omitir error  
 Se omite el error o el truncamiento.  
  
### Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del destino de ODBC. Para obtener más información, vea Destino de ODBC.  
  
## Vea también  
 [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [Editor de destino de ODBC &#40;página Asignaciones&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
  