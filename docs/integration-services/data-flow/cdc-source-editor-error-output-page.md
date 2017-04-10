---
title: "Editor de origen de CDC (p&#225;gina Salida de error) | Microsoft Docs"
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
  - "sql13.ssis.designer.cdcsource.errorhandling.f1"
ms.assetid: 8a4c2cb8-fd2f-4c45-824f-b93473a8981e
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor de origen de CDC (p&#225;gina Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de origen de CDC** para seleccionar las opciones de control de errores.  
  
 Para obtener más información acerca del origen de CDC, vea [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Lista de tareas  
 **Para abrir la página Salida de error del Editor de origen de CDC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de CDC.  
  
2.  En la pestaña **Flujo de datos**, haga doble clic en el origen de CDC.  
  
3.  En el **Editor de origen de CDC**, haga clic en **Salida de error**.  
  
## Opciones  
 **Entrada/salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Muestra las columnas externas (origen) que se han seleccionado en la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de CDC**.  
  
 **Error**  
 Seleccione la forma en la que el origen de CDC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Truncamiento**  
 Seleccione la forma en la que el origen de CDC debe controlar el truncamiento en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Description**  
 No se usa.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Seleccione la forma en la que el origen de CDC controla todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
## Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el origen de CDC controla errores y truncamientos.  
  
 **Error de componente**  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Éste es el comportamiento predeterminado.  
  
 **Omitir error**  
 El error o el truncamiento se omite y la fila de datos se dirige a la salida de origen de CDC.  
  
 **Redirigir fila**  
 La fila de datos de error o truncamiento se dirige a la salida de error del origen de CDC. En este caso, se usa el control de errores de origen de CDC. Para más información, consulte [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Vea también  
 [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Editor de origen de CDC &#40;página Columnas&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
  