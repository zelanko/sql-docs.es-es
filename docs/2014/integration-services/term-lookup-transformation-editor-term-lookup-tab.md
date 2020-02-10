---
title: Editor de transformación búsqueda de términos (pestaña búsqueda de términos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookup.termlookup.f1
helpviewer_keywords:
- Term Lookup Transformation Editor
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2939d160773d60944a2e8a786e5495cea366edb1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055132"
---
# <a name="term-lookup-transformation-editor-term-lookup-tab"></a>Editor de transformación Búsqueda de términos (pestaña Búsqueda de términos)
  Use la pestaña **Búsqueda de términos** del cuadro de diálogo **Editor de transformación Búsqueda de términos** para asignar una columna de entrada a una columna de búsqueda en una tabla de referencia y para proporcionar un alias a cada columna de salida.  
  
 Para obtener más información acerca de la transformación Búsqueda de términos, vea [Term Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Con las casillas, seleccione las columnas de entrada que se van a pasar directamente a la salida sin cambios. Arrastre una columna de entrada a la lista **Columnas de referencia disponibles** para asignarla a una columna de búsqueda en la tabla de referencia. Las columnas de entrada y búsqueda deben coincidir en los tipos de datos admitidos, DT_NTEXT o DT_WSTR. Seleccione una línea de asignación y haga clic con el botón derecho para editar las asignaciones en el cuadro de diálogo [Crear relaciones](data-flow/transformations/create-relationships.md) .  
  
 **Columnas de referencia disponibles**  
 Vea las columnas disponibles en la tabla de referencia. Elija la columna que contiene la lista de términos que coincidirán.  
  
 **Columna de paso a través**  
 Seleccione las columnas de entrada disponibles de la lista. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de columna de salida**  
 Escriba un alias para cada columna de salida. El valor predeterminado es el nombre de la columna; no obstante, puede elegir un nombre descriptivo exclusivo.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) para especificar las opciones de control de errores de las filas que provocan errores.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación búsqueda de términos &#40;pestaña tabla de referencia&#41;](../../2014/integration-services/term-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de transformación búsqueda de términos &#40;pestaña avanzadas&#41;](../../2014/integration-services/term-lookup-transformation-editor-advanced-tab.md)   
 [Extracción de términos, transformación](data-flow/transformations/term-extraction-transformation.md)  
  
  
