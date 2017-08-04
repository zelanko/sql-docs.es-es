---
title: "Editor de transformación Búsqueda de términos (pestaña búsqueda de términos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termlookup.termlookup.f1
helpviewer_keywords:
- Term Lookup Transformation Editor
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79e7f405e9418b47985efd7bcc8bb13b14f20ec6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="term-lookup-transformation-editor-term-lookup-tab"></a>Editor de transformación Búsqueda de términos (pestaña Búsqueda de términos)
  Use la pestaña **Búsqueda de términos** del cuadro de diálogo **Editor de transformación Búsqueda de términos** para asignar una columna de entrada a una columna de búsqueda en una tabla de referencia y para proporcionar un alias a cada columna de salida.  
  
 Para obtener más información acerca de la transformación Búsqueda de términos, vea [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Con las casillas, seleccione las columnas de entrada que se van a pasar directamente a la salida sin cambios. Arrastre una columna de entrada a la lista **Columnas de referencia disponibles** para asignarla a una columna de búsqueda en la tabla de referencia. Las columnas de entrada y búsqueda deben coincidir en los tipos de datos admitidos, DT_NTEXT o DT_WSTR. Seleccione una línea de asignación y haga clic con el botón derecho para editar las asignaciones en el cuadro de diálogo [Crear relaciones](../../../integration-services/data-flow/transformations/create-relationships.md) .  
  
 **Columnas de referencia disponibles**  
 Vea las columnas disponibles en la tabla de referencia. Elija la columna que contiene la lista de términos que coincidirán.  
  
 **Columna de paso a través**  
 Seleccione las columnas de entrada disponibles de la lista. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de columna de salida**  
 Escriba un alias para cada columna de salida. El valor predeterminado es el nombre de la columna; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores de las filas que provocan errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Búsqueda de términos &#40; Pestaña tabla de referencia &#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de transformación Búsqueda de términos &#40; Ficha Opciones avanzadas &#41;](../../../integration-services/data-flow/transformations/term-lookup-transformation-editor-advanced-tab.md)   
 [Transformación extracción de términos](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
  
