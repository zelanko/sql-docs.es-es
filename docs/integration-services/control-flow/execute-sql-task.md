---
title: "Tarea Ejecutar SQL | Microsoft Docs"
ms.custom: 
  - "ssisdev020617"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.executesqltask.f1"
  - "sql13.dts.designer.executesqltask.general.f1"
  - "sql13.dts.designer.executesqltask.parametermapping.f1"
  - "sql13.dts.designer.executesqltask.resultset.f1"
helpviewer_keywords: 
  - "instrucciones Transact-SQL, SSIS"
  - "instrucciones [Integration Services]"
  - "lotes [Integration Services]"
  - "Ejecutar SQL, tarea [Integration Services]"
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
caps.latest.revision: 115
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 113
---
# Tarea Ejecutar SQL
  La tarea Ejecutar SQL ejecuta instrucciones SQL o procedimientos almacenados de un paquete. La tarea puede contener una sola instrucción SQL o múltiples instrucciones SQL que se ejecutarán de forma secuencial. Puede usar la tarea Ejecutar SQL para los siguientes fines:  
  
-   Truncar una tabla o vista en preparación para insertar datos.  
  
-   Crear, modificar y quitar objetos de base de datos, como tablas y vistas.  
  
-   Volver a crear tablas de hechos y tablas de dimensiones antes de cargar datos en ellas.  
  
-   Ejecutar procedimientos almacenados. Si la instrucción SQL invoca un procedimiento almacenado que devuelve resultados de una tabla temporal, use la opción WITH RESULT SETS para definir los metadatos del conjunto de resultados.  
  
-   Guardar en una variable el conjunto de filas devuelto por una consulta.  
  
 La tarea Ejecutar SQL puede usarse en combinación con los contenedores de bucles Foreach y For para ejecutar varias instrucciones SQL. Estos contenedores implementan flujos de control que se repiten en un paquete y pueden ejecutar repetidamente la tarea Ejecutar SQL. Por ejemplo, un paquete puede usar el contenedor de bucles Foreach para enumerar los archivos de una carpeta y ejecutar una tarea Ejecutar SQL repetidamente con el fin de ejecutar la instrucción SQL almacenada en cada archivo.  
  
## Conectar con un origen de datos  
 La tarea Ejecutar SQL puede usar distintos tipos de administradores de conexión para conectar con el origen de datos en el que se ejecuta la instrucción SQL o el procedimiento almacenado. La tarea puede usar los tipos de conexión mostrados en la tabla siguiente.  
  
|Tipo de conexión|Administrador de conexiones|  
|---------------------|------------------------|  
|EXCEL|[Administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## Crear instrucciones SQL  
 El origen de las instrucciones SQL usadas por esta tarea puede ser una propiedad de tarea que contiene una instrucción, una conexión con un archivo que contiene una o varias instrucciones, o el nombre de una variable que contiene una instrucción. Debe escribirlas en el dialecto del sistema de administración de bases de datos (DBMS) de origen. Para más información, vea [Consultas de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Si las instrucciones SQL se almacenan en un archivo, la tarea utiliza un administrador de conexiones de archivos para conectar con el archivo. Para más información, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede utilizar el cuadro de diálogo **Editor de la tarea Ejecutar SQL** para escribir instrucciones SQL, o utilizar el **Generador de consultas**, una interfaz gráfica de usuario para crear consultas SQL. Para más información, vea [Editor de la tarea Ejecutar SQL &#40;página General&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(General%20Page\).md) y [Generador de consultas](../Topic/Query%20Builder.md).  
  
> [!NOTE]  
>  Es posible que la tarea Ejecutar SQL no pueda analizar correctamente instrucciones SQL válidas escritas fuera de dicha tarea.  
  
> [!NOTE]  
>  La tarea Ejecutar SQL usa el valor de enumeración de ParseMode **RecognizeAll** . Para obtener más información, vea [Espacio de nombres ManagedBatchParser](http://go.microsoft.com/fwlink/?LinkId=223617).  
  
## Enviar varias instrucciones en un lote  
 Si incluye varias instrucciones en una tarea Ejecutar SQL, puede agruparlas y ejecutarlas como un lote. Para indicar el final de un lote, utilice el comando GO. Todas las instrucciones SQL entre dos comandos GO se envían en un lote al proveedor OLE DB para que se ejecuten. El comando SQL puede incluir varios lotes separados por comandos GO.  
  
 Hay restricciones respecto a los tipos de instrucciones SQL que se pueden agrupar en un lote. Para más información, consulte [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Si la tarea Ejecutar SQL ejecuta un lote de instrucciones SQL, se aplicarán las reglas siguientes al lote:  
  
-   Solo una instrucción puede devolver un conjunto de resultados y debe ser la primera instrucción del lote.  
  
-   Si el conjunto de resultados usa enlaces de resultados, las consultas deben devolver el mismo número de columnas. Si las consultas devuelven un número distinto de columnas, la tarea no se completará correctamente. Sin embargo, aunque la tarea no se complete correctamente, se completarán correctamente las consultas que ejecute, como DELETE o INSERT.  
  
-   Si los enlaces de resultados usan nombres de columna, la consulta debe devolver columnas que tengan los mismos nombres que los nombres de los conjuntos de resultados que se utilizan en la tarea. Si faltan columnas, la tarea no se completa correctamente.  
  
-   Si la tarea utiliza enlace de parámetros, todas las consultas del lote deberán tener el mismo número de parámetros y estos deberán ser del mismo tipo.  
  
## Ejecutar comandos SQL con parámetros  
 Las instrucciones SQL y los procedimientos almacenados suelen usar parámetros de entrada, parámetros de salida y códigos de retorno. La tarea Ejecutar SQL admite los tipos de parámetros **Input**, **Output**y **ReturnValue** . Utilice el tipo **Input** para parámetros de entrada, **Output** para parámetros de salida y **ReturnValue** para códigos de retorno.  
  
> [!NOTE]  
>  Solo puede usar parámetros en una tarea Ejecutar SQL si el proveedor de datos los admite.  
  
 Para más información sobre el uso de parámetros y códigos de retorno en la tarea Ejecutar SQL, vea [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md).  
  
## Especificar un tipo de conjunto de resultados  
 En función del tipo de comando SQL, la tarea Ejecutar SQL puede devolver o no un conjunto de resultados. Por ejemplo, una instrucción SELECT suele devolver un conjunto de resultados; en cambio, una instrucción INSERT no lo devuelve. El conjunto de resultados de una instrucción SELECT puede contener cero filas, una fila o muchas filas. Los procedimientos almacenados también pueden devolver un valor entero, denominado código de retorno, que indica el estado de ejecución del procedimiento. En tal caso, el conjunto de resultados constará de una fila individual.  
  
 Para más información sobre cómo recuperar conjuntos de resultados de comandos SQL en la tarea Ejecutar SQL, vea [Conjuntos de resultados en la tarea Ejecutar SQL](../Topic/Result%20Sets%20in%20the%20Execute%20SQL%20Task.md).  
  
## Solucionar problemas de la tarea Ejecutar SQL  
 Puede registrar las llamadas que realiza la tarea Ejecutar SQL a proveedores de datos externos. Puede usar esta capacidad de registro para solucionar problemas relacionados con los comandos SQL que ejecuta la tarea Ejecutar SQL. Para registrar las llamadas realizadas por la tarea Ejecutar SQL a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 A veces, un procedimiento almacenado o comando SQL devuelve varios conjuntos de resultados. Estos conjuntos de resultados no solo incluyen los conjuntos de filas resultantes de consultas **SELECT** , sino valores únicos generados por errores de las instrucciones **RAISERROR** o **PRINT** . El hecho de que la tarea omita errores en los conjuntos de resultados que se producen después del primer conjunto de resultados depende del tipo de administrador de conexiones que se use:  
  
-   Si utiliza los administradores de conexiones ADO y OLE DB, la tarea omite los conjuntos de resultados que se producen después del primer conjunto de resultados. Por consiguiente, con estos administradores de conexiones la tarea omite un error devuelto por un procedimiento almacenado o comando SQL cuando el error no forma parte del primer conjunto de resultados.  
  
-   Si utiliza los administradores de conexiones ODBC y ADO.NET, la tarea no omite los conjuntos de resultados que se producen después del primer conjunto de resultados. Con estos administradores de conexiones, la tarea producirá un error cuando un conjunto de resultados distinto del primer conjunto de resultados contenga un error.  
  
### Entradas del registro personalizadas  
 La siguiente tabla contiene la entrada del registro personalizada para la tarea Ejecutar SQL. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Proporciona información sobre las fases de ejecución de la instrucción SQL. Las entradas de registro se escriben cuando la tarea adquiere una conexión con la base de datos, cuando la tarea comienza a preparar la instrucción SQL y una vez que se completa la ejecución de la instrucción SQL. La entrada del registro para la fase de preparación incluye la instrucción SQL que utiliza la tarea.|  
  
## Configurar la tarea Ejecutar SQL  
 Puede configurar la tarea Ejecutar SQL de las maneras siguientes:  
  
-   Especificar el tipo de administrador de conexiones que se va a utilizar para conectar con una base de datos.  
  
-   Especificar el tipo de conjunto de resultados que devolverá la instrucción SQL.  
  
-   Especificar un tiempo de espera para las instrucciones SQL.  
  
-   Especificar el origen de la instrucción SQL.  
  
-   Indicar si la tarea omite la fase de preparación para la instrucción SQL.  
  
-   Si utiliza el tipo de conexión ADO, debe indicar si la instrucción SQL es un procedimiento almacenado. Para otros tipos de conexión, esta propiedad es de solo lectura y su valor siempre es **false**.  
  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Ejecutar SQL &#40;página General&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(General%20Page\).md)  
  
-   [Editor de la tarea Ejecutar SQL &#40;página Asignación de parámetros&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(Parameter%20Mapping%20Page\).md)  
  
-   [Editor de la tarea Ejecutar SQL &#40;página Conjunto de resultados&#41;](../Topic/Execute%20SQL%20Task%20Editor%20\(Result%20Set%20Page\).md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Configurar la tarea Ejecutar SQL mediante programación  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## Tareas relacionadas  
  
-   [asignar parámetros de consulta a variables en una tarea Ejecutar SQL](../Topic/Map%20Query%20Parameters%20to%20Variables%20in%20an%20Execute%20SQL%20Task.md)  
  
-   [asignar conjuntos de resultados a variables en una tarea Ejecutar SQL](../Topic/Map%20Result%20Sets%20to%20Variables%20in%20an%20Execute%20SQL%20Task.md)  
  
## Contenido relacionado  
  
-   [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md)  
  
-   [Conjuntos de resultados en la tarea Ejecutar SQL](../Topic/Result%20Sets%20in%20the%20Execute%20SQL%20Task.md)  
  
-   [Referencia de Transact-SQL &#40;motor de base de datos&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
-   Entrada de blog, [Nuevas funciones de fecha y hora en SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=239783), en mssqltips.com.  
  
  