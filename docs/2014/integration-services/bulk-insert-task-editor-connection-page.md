---
title: Editor de la tarea inserción masiva (página conexión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.connection.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6834a2a4cd75e70de253419cc42ec5904ce0793
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061221"
---
# <a name="bulk-insert-task-editor-connection-page"></a>Editor de la tarea Inserción masiva (página Conexión)
  Use la página **Conexión** del cuadro de diálogo **Editor de la tarea Inserción masiva** para especificar el origen y el destino de la operación de inserción masiva y el formato que se debe utilizar.  
  
 Para más información sobre las inserciones masivas, vea [Tarea Inserción masiva](control-flow/bulk-insert-task.md) y [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="options"></a>Opciones  
 **Connection**  
 Seleccione un administrador de conexiones OLE DB de la lista, o bien haga clic en \<**Nueva conexión…**> para crear una conexión.  
  
 **Temas relacionados:** [OLE DB administrador de conexiones](connection-manager/ole-db-connection-manager.md), [configurar OLE DB administrador de conexiones](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **Destino**  
 Escriba el nombre de la tabla o la vista de destino, o seleccione una tabla o una vista de la lista.  
  
 **Aplique**  
 Seleccione el origen del formato de la inserción masiva. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Usar archivo**|Seleccione un archivo que contenga la especificación de formato. Si se selecciona esta opción, se muestra la opción dinámica **FormatFile**.|  
|**Especificar**|Especifique el formato. Al seleccionar esta opción se muestran las opciones `RowDelimiter` dinámicas, y `ColumnDelimiter`.|  
  
 **Archivo**  
 Seleccione un administrador de conexiones de archivos o archivos planos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear una conexión.  
  
 La ubicación del archivo es relativa al motor de base de datos de SQL Server especificado en el administrador de conexiones para esta tarea. Es preciso que el motor de base de datos de SQL Server tenga acceso al archivo de texto en un disco duro local en el servidor o mediante una unidad compartida o asignada a SQL Server. El tiempo de ejecución de SSIS no tiene acceso al archivo.  
  
 Si obtiene acceso al archivo de origen utilizando el administrador de conexiones de archivos planos, la tarea Inserción masiva no utiliza el formato especificado en el administrador de conexiones de archivos planos. En su lugar, la tarea Inserción masiva usa el formato especificado en un archivo de formato o los valores de las propiedades RowDelimiter y ColumnDelimiter de la tarea.  
  
 **Temas relacionados:** [Administrador](connection-manager/file-connection-manager.md)de conexiones de archivos, [Editor del administrador de conexiones](../../2014/integration-services/file-connection-manager-editor.md)de archivos, administrador de conexiones de [archivos](connection-manager/flat-file-connection-manager.md)planos, editor del administrador de [conexiones de archivos planos &#40;página general&#41;](general-page-of-integration-services-designers-options.md), [editor del administrador de conexiones de archivos planos &#40;página columnas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md), [Editor del administrador de conexiones de archivos planos &#40;página avanzadas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)  
  
 **Actualizar tablas**  
 Actualice la lista de tablas y vistas.  
  
## <a name="format-dynamic-options"></a>Opciones dinámicas de formato  
  
### <a name="format--use-file"></a>Formato = Utilizar archivo  
 **FormatFile**  
 Escriba la ruta de acceso del archivo de formato, o bien haga clic en el botón de puntos suspensivos (**…**) para buscar el archivo de formato.  
  
### <a name="format--specify"></a>Formato = Especificar  
 `RowDelimiter`  
 Especifique el delimitador de filas en el archivo de origen. El valor predeterminado es **{CR} {LF}**.  
  
 `ColumnDelimiter`  
 Especifique el delimitador de columna en el archivo de origen. El valor predeterminado es **Tab**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea inserción masiva &#40;página general&#41;](../../2014/integration-services/bulk-insert-task-editor-general-page.md)   
 [Editor de la tarea inserción masiva &#40;página Opciones&#41;](../../2014/integration-services/bulk-insert-task-editor-options-page.md)   
 [Página Expresiones](expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Flujo de control](control-flow/control-flow.md)  
  
  
