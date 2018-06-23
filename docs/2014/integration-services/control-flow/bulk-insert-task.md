---
title: Tarea Inserción masiva| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.bulkinserttask.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 62
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 62cc927e4beb15666940f30cd063d5618fd2a038
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199495"
---
# <a name="bulk-insert-task"></a>Inserción masiva, tarea
  La tarea Inserción masiva proporciona una forma muy eficaz de copiar grandes cantidades de datos a una tabla o vista de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, suponga que su empresa almacena una lista de productos de un millón de filas en un sistema central, pero el sistema de comercio electrónico de la empresa usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para rellenar páginas web. Debe actualizar la tabla de productos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todas las noches con la lista maestra de productos del gran sistema. Para ello, debe guardar la lista de productos con un formato delimitado por tabuladores y utilizar la tarea Inserción masiva para copiar los datos directamente a la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para garantizar que la copia de datos se realice a gran velocidad, no se permite la aplicación de transformaciones a los datos mientras se mueven desde el archivo de origen a la tabla o la vista.  
  
## <a name="usage-considerations"></a>Consideraciones de uso  
 Antes de utilizar la tarea Inserción masiva, tenga en cuenta que:  
  
-   La tarea Inserción masiva solo puede transferir datos de un archivo de texto a una tabla o una vista de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para usar la tarea Inserción masiva para transferir datos de otros sistemas de administración de bases de datos (DBMS), debe exportar los datos del origen a un archivo de texto y después importar los datos del archivo de texto en una tabla o vista de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   El destino debe ser una tabla o una vista de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si la tabla o vista de destino ya contiene datos, los datos nuevos se anexarán a los datos existentes cuando se ejecute la tarea Inserción masiva. Si desea reemplazar los datos, antes de ejecutar la tarea Inserción masiva, debe ejecutar una tarea Ejecutar SQL que ejecute una instrucción DELETE o TRUNCATE. Para más información, consulte [Execute SQL Task](execute-sql-task.md).  
  
-   Puede utilizar un archivo de formato en el objeto de tarea Inserción masiva. Si tiene un archivo de formato creado con la utilidad **bcp** , puede especificar su ruta de acceso en la tarea Inserción masiva. La tarea Inserción masiva admite tanto archivos XML como archivos con otros formatos. Para obtener más información sobre archivos de formato, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Solo los miembros del rol fijo de servidor sysadmin pueden ejecutar un paquete que contiene una tarea Inserción masiva.  
  
## <a name="bulk-insert-task-with-transactions"></a>Tarea Inserción masiva en las transacciones  
 Si el tamaño de un lote no está establecido, la operación completa de copia masiva se trata como una transacción. Si el tamaño del lote es **0** , significa que los datos se insertan en un lote. Si se ha establecido un tamaño de lote, cada lote constituye una transacción que será confirmada cuando finalice la ejecución del lote.  
  
 El comportamiento de la tarea Inserción masiva en lo que se refiere a las transacciones dependerá de si la tarea se combina con la transacción del paquete. Si la tarea Inserción masiva no se combina con la transacción de paquete, se confirmará cada lote sin errores como una unidad antes de procesar el siguiente lote. Si se combina la tarea de inserción masiva con la transacción del paquete, los lotes sin errores permanecerán en la transacción tras la finalización de la tarea. Estos lotes están sujetos a las operaciones para confirmar o revertir del paquete.  
  
 Un error en la tarea Inserción masiva no revierte automáticamente los lotes cargados correctamente; de forma similar, si la tarea se completa correctamente, los lotes no se confirman automáticamente. Solo se realizan operaciones para confirmar o revertir en respuesta a valores de propiedades de un paquete y un flujo de trabajo.  
  
## <a name="source-and-destination"></a>Origen y destino  
 Si se especifica la ubicación del archivo de origen de texto, tenga en cuenta los siguientes aspectos:  
  
-   El servidor debe tener permiso de acceso al archivo y a la base de datos de destino.  
  
-   El servidor ejecuta la tarea Inserción masiva. Por tanto, cualquier archivo de formato utilizado por la tarea debe encontrarse en el servidor.  
  
-   El archivo de código fuente que carga la tarea Inserción masiva puede estar en el mismo servidor que la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se van a insertar los datos o en un servidor remoto. Si el archivo está en un servidor remoto, debe especificar el nombre de archivo en la ruta mediante un nombre conforme con la convención de nomenclatura universal (UNC).  
  
## <a name="performance-optimization"></a>Optimización del rendimiento  
 Para optimizar el rendimiento, tenga en cuenta que:  
  
-   Si el archivo de texto se encuentra en el mismo equipo que la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se van a insertar los datos, la operación de copia se producirá aun más rápido, ya que no hay que mover los datos por la red.  
  
-   La tarea de inserción masiva no registrará las filas que produzcan errores. Si tiene que capturar esta información, use las salidas de error de componentes de flujo de datos para capturar las filas que provocan errores en un archivo de excepciones.  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>Entradas del registro personalizadas disponibles en la tarea Inserción masiva  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Inserción masiva. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`BulkInsertTaskBegin`|Indica que se inició la inserción masiva.|  
|`BulkInsertTaskEnd`|Indica que finalizó la inserción masiva.|  
|`BulkInsertTaskInfos`|Proporciona información descriptiva sobre la tarea.|  
  
## <a name="bulk-insert-task-configuration"></a>Configuración de la tarea Inserción masiva  
 Puede configurar la tarea Inserción masiva de las maneras siguientes:  
  
-   Especificar el administrador de conexiones OLE DB para conectar con la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino y la tabla o la vista en la que se insertarán los datos. La tarea Inserción masiva solo admite conexiones de OLE DB para la base de datos de destino.  
  
-   Especifique el archivo o administrador de conexiones de archivos planos para tener acceso al archivo de origen. La tarea Inserción masiva solo utiliza el administrador de conexiones para la ubicación del archivo de destino. La tarea omite otras opciones seleccionadas en el editor de administrador de conexiones.  
  
-   Definir el formato usado por la tarea Inserción masiva mediante un archivo de formato o definiendo la columna y los delimitadores de filas de los datos de origen. Si utiliza un archivo de formato, especifique el administrador de conexiones de archivos para tener acceso al archivo de formato.  
  
-   Especificar acciones que se deben realizar en la tabla o la vista de destino cuando la tarea inserta los datos. Entre las opciones figuran restricciones CHECK, habilitar inserciones de identidad, conservar valores NULL, activar desencadenadores y bloquear la tabla.  
  
-   Proporcionar información acerca del lote de datos que se va a insertar, como el tamaño del lote, la primera y la última fila del archivo que se va a insertar, el número de errores de inserción que se pueden producir antes de que la tarea deje de insertar filas y los nombres de las columnas que se van a ordenar.  
  
 Si la tarea Inserción masiva utiliza un administrador de conexiones de archivos planos para obtener acceso al archivo de origen, la tarea no utiliza el formato especificado en dicho administrador. En su lugar, la tarea Inserción masiva usa el formato especificado en un archivo de formato o los valores de las propiedades RowDelimiter y ColumnDelimiter de la tarea.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea de inserción de forma masiva &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea de inserción de forma masiva &#40;página de conexión&#41;](../bulk-insert-task-editor-connection-page.md)  
  
-   [Editor de la tarea de inserción de forma masiva &#40;página de opciones&#41;](../bulk-insert-task-editor-options-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>Configuración mediante programación de la tarea Inserción masiva  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico, sobre la [posible aparición del error "No se puede preparar la inserción masiva de SSIS para la inserción de datos" en sistemas habilitados para UAC](http://go.microsoft.com/fwlink/?LinkId=233693), en support.microsoft.com.  
  
-   Artículo técnico, [The Data Loading Performance Guide](http://go.microsoft.com/fwlink/?LinkId=233700), en msdn.microsoft.com.  
  
-   Artículo técnico sobre cómo [usar SQL Server Integration Services para la carga masiva de datos](http://go.microsoft.com/fwlink/?LinkId=233701), en simple-talk.com.  
  
  