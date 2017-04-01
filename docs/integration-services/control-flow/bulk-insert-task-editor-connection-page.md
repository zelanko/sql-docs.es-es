---
title: "Editor de la tarea Inserci&#243;n masiva (p&#225;gina Conexi&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.bulkinserttask.connection.f1"
helpviewer_keywords: 
  - "Inserción masiva, editor de la tarea"
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor de la tarea Inserci&#243;n masiva (p&#225;gina Conexi&#243;n)
  Use la página **Conexión** del cuadro de diálogo **Editor de la tarea Inserción masiva** para especificar el origen y el destino de la operación de inserción masiva y el formato que se debe utilizar.  
  
 Para más información sobre las inserciones masivas, vea [Tarea Inserción masiva](../../integration-services/control-flow/bulk-insert-task.md) y [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## Opciones  
 **Conexión**  
 Seleccione un administrador de conexiones OLE DB de la lista, o bien haga clic en \<**Nueva conexión…**> para crear una conexión.  
  
 **Temas relacionados:** [Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md), [Configurar el administrador de conexiones OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 **Tabla de destino**  
 Escriba el nombre de la tabla o la vista de destino, o seleccione una tabla o una vista de la lista.  
  
 **Formato**  
 Seleccione el origen del formato de la inserción masiva. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Utilizar archivo**|Seleccione un archivo que contenga la especificación de formato. Si se selecciona esta opción, se muestra la opción dinámica **FormatFile**.|  
|**Especificar**|Especifique el formato. Si se selecciona esta opción, se muestran las opciones dinámicas **RowDelimiter** y **ColumnDelimiter**.|  
  
 **Archivo**  
 Seleccione un administrador de conexiones de archivos o archivos planos de la lista, o bien haga clic en \<**Nueva conexión…**> para crear una conexión.  
  
 La ubicación del archivo es relativa al motor de base de datos de SQL Server especificado en el administrador de conexiones para esta tarea. Es preciso que el motor de base de datos de SQL Server tenga acceso al archivo de texto en un disco duro local en el servidor o mediante una unidad compartida o asignada a SQL Server. El tiempo de ejecución de SSIS no tiene acceso al archivo.  
  
 Si obtiene acceso al archivo de origen utilizando el administrador de conexiones de archivos planos, la tarea Inserción masiva no utiliza el formato especificado en el administrador de conexiones de archivos planos. En su lugar, la tarea Inserción masiva usa el formato especificado en un archivo de formato o los valores de las propiedades RowDelimiter y ColumnDelimiter de la tarea.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor del administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager-editor.md), [Administrador de conexiones de archivos planos](../../integration-services/connection-manager/flat-file-connection-manager.md), [Editor del administrador de conexiones de archivos planos &#40;página General&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md), [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md), [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)  
  
 **Actualizar tablas**  
 Actualice la lista de tablas y vistas.  
  
## Opciones dinámicas de formato  
  
### Formato = Utilizar archivo  
 **FormatFile**  
 Escriba la ruta de acceso del archivo de formato, o bien haga clic en el botón de puntos suspensivos (**…**) para buscar el archivo de formato.  
  
### Formato = Especificar  
 **RowDelimiter**  
 Especifique el delimitador de filas en el archivo de origen. El valor predeterminado es **{CR}{LF}**.  
  
 **ColumnDelimiter**  
 Especifique el delimitador de columna en el archivo de origen. El valor predeterminado es **Tab**.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea Inserción masiva &#40;página General&#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)   
 [Editor de la tarea Inserción masiva &#40;página Opciones&#41;](../../integration-services/control-flow/bulk-insert-task-editor-options-page.md)   
 [Página Expresiones](../../integration-services/expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  