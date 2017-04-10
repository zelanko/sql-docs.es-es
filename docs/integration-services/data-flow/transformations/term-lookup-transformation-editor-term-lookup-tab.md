---
title: "Editor de transformaci&#243;n B&#250;squeda de t&#233;rminos (pesta&#241;a B&#250;squeda de t&#233;rminos) | Microsoft Docs"
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
  - "sql13.dts.designer.termlookup.termlookup.f1"
helpviewer_keywords: 
  - "Búsqueda de términos, editor de transformación "
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor de transformaci&#243;n B&#250;squeda de t&#233;rminos (pesta&#241;a B&#250;squeda de t&#233;rminos)
  Use la pestaña **Búsqueda de términos** del cuadro de diálogo **Editor de transformación Búsqueda de términos** para asignar una columna de entrada a una columna de búsqueda en una tabla de referencia y para proporcionar un alias a cada columna de salida.  
  
 Para obtener más información acerca de la transformación Búsqueda de términos, vea [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
## Opciones  
 **Columnas de entrada disponibles**  
 Con las casillas, seleccione las columnas de entrada que se van a pasar directamente a la salida sin cambios. Arrastre una columna de entrada a la lista **Columnas de referencia disponibles** para asignarla a una columna de búsqueda en la tabla de referencia. Las columnas de entrada y búsqueda deben coincidir en los tipos de datos admitidos, DT_NTEXT o DT_WSTR. Seleccione una línea de asignación y haga clic con el botón derecho para editar las asignaciones en el cuadro de diálogo [Crear relaciones](../../../integration-services/data-flow/transformations/create-relationships.md).  
  
 **Columnas de referencia disponibles**  
 Vea las columnas disponibles en la tabla de referencia. Elija la columna que contiene la lista de términos que coincidirán.  
  
 **Columna de paso a través**  
 Seleccione las columnas de entrada disponibles de la lista. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de columna de salida**  
 Escriba un alias para cada columna de salida. El valor predeterminado es el nombre de la columna; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](../Topic/Configure%20Error%20Output.md) para especificar las opciones de control de errores de las filas que provocan errores.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Búsqueda de términos &#40;pestaña Tabla de referencia&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de transformación Búsqueda de términos &#40;pestaña Avanzadas&#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-advanced-tab.md)   
 [Transformación Extracción de términos](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
  