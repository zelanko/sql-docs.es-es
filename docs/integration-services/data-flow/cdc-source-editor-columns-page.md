---
title: "Editor de origen de CDC (p&#225;gina Columnas) | Microsoft Docs"
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
  - "sql13.ssis.designer.cdcsource.columns.f1"
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Editor de origen de CDC (p&#225;gina Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de origen de CDC** para asignar una columna de salida a cada columna externa (origen).  
  
 Para obtener más información acerca del origen de CDC, vea [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## Lista de tareas  
 **Para abrir la página Columnas del Editor de origen de CDC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de CDC.  
  
2.  En la pestaña **Flujo de datos**, haga doble clic en el origen de CDC.  
  
3.  En el **Editor de origen de CDC**, haga clic en **Columnas**.  
  
## Opciones  
 **Columnas externas disponibles**  
 Lista de las columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas. Seleccione las columnas que se van a usar en el origen. Las columnas seleccionadas se agregan a la lista **Columna externa** en el orden en que se seleccionan.  
  
 **Columna externa**  
 Vista de las columnas externas (origen) en el orden en que se verán cuando configure componentes que usen datos del origen de CDC. Para cambiar este orden, en primer lugar borre las columnas seleccionadas en la lista **Columnas externas disponibles** y, a continuación, seleccione las columnas externas en la lista en un orden diferente. Las columnas seleccionadas se agregan a la lista **Columna externa** en el orden en que las haya seleccionado.  
  
 **Columna de salida**  
 Especifique un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir cualquier nombre único y descriptivo. El nombre especificado se muestra en el Diseñador de SSIS.  
  
## Vea también  
 [Editor de origen de CDC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Editor de origen de CDC &#40;página Salida de error&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  