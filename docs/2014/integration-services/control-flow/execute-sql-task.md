---
title: Tarea Ejecutar SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe677e6b2fb13c3a158c78e0416142b7b15ce975
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204825"
---
# <a name="execute-sql-task"></a>Tarea Ejecutar SQL
  La tarea Ejecutar SQL ejecuta instrucciones SQL o procedimientos almacenados de un paquete. La tarea puede contener una sola instrucción SQL o múltiples instrucciones SQL que se ejecutarán de forma secuencial. Puede usar la tarea Ejecutar SQL para los siguientes fines:  
  
-   Truncar una tabla o vista en preparación para insertar datos.  
  
-   Crear, modificar y quitar objetos de base de datos, como tablas y vistas.  
  
-   Volver a crear tablas de hechos y tablas de dimensiones antes de cargar datos en ellas.  
  
-   Ejecutar procedimientos almacenados. Si la instrucción SQL invoca un procedimiento almacenado que devuelve resultados de una tabla temporal, use la opción WITH RESULT SETS para definir los metadatos del conjunto de resultados.  
  
-   Guardar en una variable el conjunto de filas devuelto por una consulta.  
  
 La tarea Ejecutar SQL puede usarse en combinación con los contenedores de bucles Foreach y For para ejecutar varias instrucciones SQL. Estos contenedores implementan flujos de control que se repiten en un paquete y pueden ejecutar repetidamente la tarea Ejecutar SQL. Por ejemplo, un paquete puede usar el contenedor de bucles Foreach para enumerar los archivos de una carpeta y ejecutar una tarea Ejecutar SQL repetidamente con el fin de ejecutar la instrucción SQL almacenada en cada archivo.  
  
## <a name="connecting-to-a-data-source"></a>Conectar con un origen de datos  
 La tarea Ejecutar SQL puede usar distintos tipos de administradores de conexión para conectar con el origen de datos en el que se ejecuta la instrucción SQL o el procedimiento almacenado. La tarea puede usar los tipos de conexión mostrados en la tabla siguiente.  
  
|Tipo de conexión|Administrador de conexiones|  
|---------------------|------------------------|  
|EXCEL|[Administrador de conexiones de Excel](../connection-manager/excel-connection-manager.md)|  
|OLE DB|[Administrador de conexiones OLE DB](../connection-manager/ole-db-connection-manager.md)|  
|ODBC|[Administrador de conexiones ODBC](../connection-manager/odbc-connection-manager.md)|  
|ADO|[Administrador de conexiones ADO](../connection-manager/ado-connection-manager.md)|  
|ADO.NET|[Administrador de conexiones ADO.NET](../connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[Administrador de conexiones con SQL Server Compact Edition](../connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="creating-sql-statements"></a>Crear instrucciones SQL  
 El origen de las instrucciones SQL usadas por esta tarea puede ser una propiedad de tarea que contiene una instrucción, una conexión con un archivo que contiene una o varias instrucciones, o el nombre de una variable que contiene una instrucción. Debe escribirlas en el dialecto del sistema de administración de bases de datos (DBMS) de origen. Para más información, vea [Consultas de Integration Services &#40;SSIS&#41;](../integration-services-ssis-queries.md).  
  
 Si las instrucciones SQL se almacenan en un archivo, la tarea utiliza un administrador de conexiones de archivos para conectar con el archivo. Para obtener más información, consulte [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede utilizar el cuadro de diálogo **Editor de la tarea Ejecutar SQL** para escribir instrucciones SQL, o utilizar el **Generador de consultas**, una interfaz gráfica de usuario para crear consultas SQL. Para más información, vea [Editor de la tarea Ejecutar SQL &#40;página General&#41;](../execute-sql-task-editor-general-page.md) y [Generador de consultas](../query-builder.md).  
  
> [!NOTE]  
>  Es posible que la tarea Ejecutar SQL no pueda analizar correctamente instrucciones SQL válidas escritas fuera de dicha tarea.  
  
> [!NOTE]  
>  La tarea Ejecutar SQL usa el valor de enumeración de ParseMode `RecognizeAll`. Para obtener más información, vea [Espacio de nombres ManagedBatchParser](http://go.microsoft.com/fwlink/?LinkId=223617).  
  
## <a name="sending-multiple-statements-in-a-batch"></a>Enviar varias instrucciones en un lote  
 Si incluye varias instrucciones en una tarea Ejecutar SQL, puede agruparlas y ejecutarlas como un lote. Para indicar el final de un lote, utilice el comando GO. Todas las instrucciones SQL entre dos comandos GO se envían en un lote al proveedor OLE DB para que se ejecuten. El comando SQL puede incluir varios lotes separados por comandos GO.  
  
 Hay restricciones respecto a los tipos de instrucciones SQL que se pueden agrupar en un lote. Para más información, consulte [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Si la tarea Ejecutar SQL ejecuta un lote de instrucciones SQL, se aplicarán las reglas siguientes al lote:  
  
-   Solo una instrucción puede devolver un conjunto de resultados y debe ser la primera instrucción del lote.  
  
-   Si el conjunto de resultados usa enlaces de resultados, las consultas deben devolver el mismo número de columnas. Si las consultas devuelven un número distinto de columnas, la tarea no se completará correctamente. Sin embargo, aunque la tarea no se complete correctamente, se completarán correctamente las consultas que ejecute, como DELETE o INSERT.  
  
-   Si los enlaces de resultados usan nombres de columna, la consulta debe devolver columnas que tengan los mismos nombres que los nombres de los conjuntos de resultados que se utilizan en la tarea. Si faltan columnas, la tarea no se completa correctamente.  
  
-   Si la tarea utiliza enlace de parámetros, todas las consultas del lote deberán tener el mismo número de parámetros y estos deberán ser del mismo tipo.  
  
## <a name="running-parameterized-sql-commands"></a>Ejecutar comandos SQL con parámetros  
 Las instrucciones SQL y los procedimientos almacenados suelen usar parámetros de entrada, parámetros de salida y códigos de retorno. La tarea Ejecutar SQL admite el `Input`, `Output`, y `ReturnValue` tipos de parámetro. Usa el `Input` tipo para parámetros de entrada, `Output` para parámetros de salida y `ReturnValue` para códigos de retorno.  
  
> [!NOTE]  
>  Solo puede usar parámetros en una tarea Ejecutar SQL si el proveedor de datos los admite.  
  
 Para más información sobre el uso de parámetros y códigos de retorno en la tarea Ejecutar SQL, vea [Parámetros y códigos de retorno en la tarea Ejecutar SQL](execute-sql-task.md).  
  
## <a name="specifying-a-result-set-type"></a>Especificar un tipo de conjunto de resultados  
 En función del tipo de comando SQL, la tarea Ejecutar SQL puede devolver o no un conjunto de resultados. Por ejemplo, una instrucción SELECT suele devolver un conjunto de resultados; en cambio, una instrucción INSERT no lo devuelve. El conjunto de resultados de una instrucción SELECT puede contener cero filas, una fila o muchas filas. Los procedimientos almacenados también pueden devolver un valor entero, denominado código de retorno, que indica el estado de ejecución del procedimiento. En tal caso, el conjunto de resultados constará de una fila individual.  
  
 Para más información sobre cómo recuperar conjuntos de resultados de comandos SQL en la tarea Ejecutar SQL, vea [Conjuntos de resultados en la tarea Ejecutar SQL](../result-sets-in-the-execute-sql-task.md).  
  
## <a name="troubleshooting-the-execute-sql-task"></a>Solucionar problemas de la tarea Ejecutar SQL  
 Puede registrar las llamadas que realiza la tarea Ejecutar SQL a proveedores de datos externos. Puede usar esta capacidad de registro para solucionar problemas relacionados con los comandos SQL que ejecuta la tarea Ejecutar SQL. Para registrar las llamadas realizadas por la tarea Ejecutar SQL a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 A veces, un procedimiento almacenado o comando SQL devuelve varios conjuntos de resultados. Estos conjuntos de resultados incluyen no solo los conjuntos de filas que son el resultado de `SELECT` consultas, sino valores únicos que son el resultado de errores de `RAISERROR` o `PRINT` instrucciones. El hecho de que la tarea omita errores en los conjuntos de resultados que se producen después del primer conjunto de resultados depende del tipo de administrador de conexiones que se use:  
  
-   Si utiliza los administradores de conexiones ADO y OLE DB, la tarea omite los conjuntos de resultados que se producen después del primer conjunto de resultados. Por consiguiente, con estos administradores de conexiones la tarea omite un error devuelto por un procedimiento almacenado o comando SQL cuando el error no forma parte del primer conjunto de resultados.  
  
-   Si utiliza los administradores de conexiones ODBC y ADO.NET, la tarea no omite los conjuntos de resultados que se producen después del primer conjunto de resultados. Con estos administradores de conexiones, la tarea producirá un error cuando un conjunto de resultados distinto del primer conjunto de resultados contenga un error.  
  
### <a name="custom-log-entries"></a>Entradas del registro personalizadas  
 La siguiente tabla contiene la entrada del registro personalizada para la tarea Ejecutar SQL. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../custom-messages-for-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|Proporciona información sobre las fases de ejecución de la instrucción SQL. Las entradas de registro se escriben cuando la tarea adquiere una conexión con la base de datos, cuando la tarea comienza a preparar la instrucción SQL y una vez que se completa la ejecución de la instrucción SQL. La entrada del registro para la fase de preparación incluye la instrucción SQL que utiliza la tarea.|  
  
## <a name="configuring-the-execute-sql-task"></a>Configurar la tarea Ejecutar SQL  
 Puede configurar la tarea Ejecutar SQL de las maneras siguientes:  
  
-   Especificar el tipo de administrador de conexiones que se va a utilizar para conectar con una base de datos.  
  
-   Especificar el tipo de conjunto de resultados que devolverá la instrucción SQL.  
  
-   Especificar un tiempo de espera para las instrucciones SQL.  
  
-   Especificar el origen de la instrucción SQL.  
  
-   Indicar si la tarea omite la fase de preparación para la instrucción SQL.  
  
-   Si utiliza el tipo de conexión ADO, debe indicar si la instrucción SQL es un procedimiento almacenado. Para otros tipos de conexión, esta propiedad es de solo lectura y su valor es siempre `false`.  
  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Ejecutar el Editor de la tarea SQL &#40;página General&#41;](../execute-sql-task-editor-general-page.md)  
  
-   [Ejecutar el Editor de la tarea SQL &#40;página asignación de parámetros&#41;](../execute-sql-task-editor-parameter-mapping-page.md)  
  
-   [Ejecutar el Editor de la tarea SQL &#40;página conjunto de resultados&#41;](../execute-sql-task-editor-result-set-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="configuring-the-execute-sql-task-programmatically"></a>Configurar la tarea Ejecutar SQL mediante programación  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Asignar parámetros de consulta a variables en una tarea Ejecutar SQL](../map-query-parameters-to-variables-in-an-execute-sql-task.md)  
  
-   [Asignar conjuntos de resultados a variables en una tarea Ejecutar SQL](../map-result-sets-to-variables-in-an-execute-sql-task.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Parámetros y códigos de retorno en la tarea Ejecutar SQL](execute-sql-task.md)  
  
-   [Conjuntos de resultados en la tarea Ejecutar SQL](../result-sets-in-the-execute-sql-task.md)  
  
-   [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference)  
  
-   Entrada de blog, [Nuevas funciones de fecha y hora en SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=239783), en mssqltips.com.  
  
  
