---
title: Editor de transformación búsqueda aproximada (pestaña columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.columns.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 74608af46f2b76a2df69d2fc7b522948bd858f7a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966295"
---
# <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>Editor de transformación Búsqueda aproximada (pestaña Columnas)
  Use la pestaña **Columnas** del cuadro de diálogo **Editor de transformación Búsqueda aproximada** para especificar las propiedades de las columnas de entrada y salida.  
  
 Para obtener más información acerca de la transformación Búsqueda aproximada, vea [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Arrastre las columnas de entrada para conectarlas a las columnas de búsqueda disponibles. Las columnas deben poseer tipos de datos coincidentes y compatibles. Seleccione una línea de asignación y haga clic con el botón derecho para editar las asignaciones en el cuadro de diálogo [Crear relaciones](data-flow/transformations/create-relationships.md) .  
  
 **Nombre**  
 Muestra los nombres de las columnas de entrada disponibles.  
  
 **Paso a través**  
 Especifique si desea incluir las columnas de entrada en la salida de transformación.  
  
 **Columnas de búsqueda disponibles**  
 Use las casillas para seleccionar las columnas en las que se realizarán operaciones de búsqueda aproximada.  
  
 **columna de búsqueda**  
 Seleccione las columnas de búsqueda en la lista de columnas de tabla de referencia disponibles. Sus selecciones se reflejan en las casillas en la tabla **Columnas de búsqueda disponibles** . Seleccione una columna en la tabla **Columnas de búsqueda disponibles** para crear una columna de salida que contenga el valor de la columna de la tabla de referencia para cada fila coincidente devuelta.  
  
 **Alias de salida**  
 Escriba un alias para la salida de cada columna de búsqueda. El nombre predeterminado es el de la columna de búsqueda con un valor de índice numérico anexado, pero puede elegir cualquier nombre descriptivo único.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación búsqueda aproximada &#40;pestaña tabla de referencia&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de transformación Búsqueda aproximada &#40;pestaña Avanzadas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
