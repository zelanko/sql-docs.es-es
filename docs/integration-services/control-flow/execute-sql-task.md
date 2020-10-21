---
description: Tarea Ejecutar SQL
title: Tarea Ejecutar SQL
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0b8155db361eeffd3b84ba1aadf313ecef4652e9
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196547"
---
# <a name="execute-sql-task"></a>Tarea Ejecutar SQL

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  La tarea Ejecutar SQL ejecuta instrucciones SQL o procedimientos almacenados de un paquete. La tarea puede contener una sola instrucción SQL o múltiples instrucciones SQL que se ejecutarán de forma secuencial. Puede usar la tarea Ejecutar SQL para los siguientes fines:  
  
-   Truncar una tabla o vista en preparación para insertar datos.  
  
-   Crear, modificar y quitar objetos de base de datos, como tablas y vistas.  
  
-   Volver a crear tablas de hechos y tablas de dimensiones antes de cargar datos en ellas.  
  
-   Ejecutar procedimientos almacenados. Si la instrucción SQL invoca un procedimiento almacenado que devuelve resultados de una tabla temporal, use la opción WITH RESULT SETS para definir los metadatos del conjunto de resultados.  
  
-   Guardar en una variable el conjunto de filas devuelto por una consulta.  
  
 La tarea Ejecutar SQL puede usarse en combinación con los contenedores de bucles Foreach y For para ejecutar varias instrucciones SQL. Estos contenedores implementan flujos de control que se repiten en un paquete y pueden ejecutar repetidamente la tarea Ejecutar SQL. Por ejemplo, un paquete puede usar el contenedor de bucles Foreach para enumerar los archivos de una carpeta y ejecutar una tarea Ejecutar SQL repetidamente con el fin de ejecutar la instrucción SQL almacenada en cada archivo.  
  
## <a name="connect-to-a-data-source"></a>Conectarse a un origen de datos  
 La tarea Ejecutar SQL puede usar distintos tipos de administradores de conexión para conectar con el origen de datos en el que se ejecuta la instrucción SQL o el procedimiento almacenado. La tarea puede usar los tipos de conexión mostrados en la tabla siguiente.  
  
|Tipo de conexión|Administrador de conexiones|  
|---------------------|------------------------|  
|EXCEL|[Administrador de conexiones de Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>Crear instrucciones SQL  
 El origen de las instrucciones SQL usadas por esta tarea puede ser una propiedad de tarea que contiene una instrucción, una conexión con un archivo que contiene una o varias instrucciones, o el nombre de una variable que contiene una instrucción. Debe escribirlas en el dialecto del sistema de administración de bases de datos (DBMS) de origen. Para más información, vea [Consultas de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Si las instrucciones SQL se almacenan en un archivo, la tarea utiliza un administrador de conexiones de archivos para conectar con el archivo. Para obtener más información, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede utilizar el cuadro de diálogo **Editor de la tarea Ejecutar SQL** para escribir instrucciones SQL, o utilizar el **Generador de consultas**, una interfaz gráfica de usuario para crear consultas SQL. 
  
> [!NOTE]  
>  Es posible que la tarea Ejecutar SQL no pueda analizar correctamente instrucciones SQL válidas escritas fuera de dicha tarea.  
  
> [!NOTE]  
>  La tarea Ejecutar SQL usa el valor de enumeración de ParseMode **RecognizeAll** . Para obtener más información, vea [Espacio de nombres ManagedBatchParser](/dotnet/api/managedbatchparser).  
  
## <a name="send-multiple-statements-in-a-batch"></a>Enviar varias instrucciones en un lote  
 Si incluye varias instrucciones en una tarea Ejecutar SQL, puede agruparlas y ejecutarlas como un lote. Para indicar el final de un lote, utilice el comando GO. Todas las instrucciones SQL entre dos comandos GO se envían en un lote al proveedor OLE DB para que se ejecuten. El comando SQL puede incluir varios lotes separados por comandos GO.  
  
 Hay restricciones respecto a los tipos de instrucciones SQL que se pueden agrupar en un lote. Para más información, consulte [Batches of Statements](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Si la tarea Ejecutar SQL ejecuta un lote de instrucciones SQL, se aplicarán las reglas siguientes al lote:  
  
-   Solo una instrucción puede devolver un conjunto de resultados y debe ser la primera instrucción del lote.  
  
-   Si el conjunto de resultados usa enlaces de resultados, las consultas deben devolver el mismo número de columnas. Si las consultas devuelven un número distinto de columnas, la tarea no se completará correctamente. Sin embargo, aunque la tarea no se complete correctamente, se completarán correctamente las consultas que ejecute, como DELETE o INSERT.  
  
-   Si los enlaces de resultados usan nombres de columna, la consulta debe devolver columnas que tengan los mismos nombres que los nombres de los conjuntos de resultados que se utilizan en la tarea. Si faltan columnas, la tarea no se completa correctamente.  
  
-   Si la tarea utiliza enlace de parámetros, todas las consultas del lote deberán tener el mismo número de parámetros y estos deberán ser del mismo tipo.  
  
## <a name="run-parameterized-sql-commands"></a>Ejecutar comandos SQL con parámetros  
 Las instrucciones SQL y los procedimientos almacenados suelen usar parámetros de entrada, parámetros de salida y códigos de retorno. La tarea Ejecutar SQL admite los tipos de parámetros **Input**, **Output**y **ReturnValue** . Utilice el tipo **Input** para parámetros de entrada, **Output** para parámetros de salida y **ReturnValue** para códigos de retorno.  
  
> [!NOTE]  
>  Solo puede usar parámetros en una tarea Ejecutar SQL si el proveedor de datos los admite.  
  
## <a name="specify-a-result-set-type"></a>Especificar un tipo de conjunto de resultados  
 En función del tipo de comando SQL, la tarea Ejecutar SQL puede devolver o no un conjunto de resultados. Por ejemplo, una instrucción SELECT suele devolver un conjunto de resultados; en cambio, una instrucción INSERT no lo devuelve. El conjunto de resultados de una instrucción SELECT puede contener cero filas, una fila o muchas filas. Los procedimientos almacenados también pueden devolver un valor entero, denominado código de retorno, que indica el estado de ejecución del procedimiento. En tal caso, el conjunto de resultados constará de una fila individual.  
  
## <a name="configure-the-execute-sql-task"></a>Configurar la tarea Ejecutar SQL  
 Puede configurar la tarea Ejecutar SQL de las maneras siguientes:  
  
-   Especificar el tipo de administrador de conexiones que se va a utilizar para conectar con una base de datos.  
  
-   Especificar el tipo de conjunto de resultados que devolverá la instrucción SQL.  
  
-   Especificar un tiempo de espera para las instrucciones SQL.  
  
-   Especificar el origen de la instrucción SQL.  
  
-   Indicar si la tarea omite la fase de preparación para la instrucción SQL.  
  
-   Si utiliza el tipo de conexión ADO, debe indicar si la instrucción SQL es un procedimiento almacenado. Para otros tipos de conexión, esta propiedad es de solo lectura y su valor siempre es **false**.  
  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  

## <a name="general-page---execute-sql-task-editor"></a>Página general: Editor de la tarea Ejecutar SQL
 Use la página **General** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para configurar la tarea Ejecutar SQL y proporcionar la instrucción SQL de ejecución de la tarea.  

Para más información sobre el lenguaje de consultas Transact-SQL y su sintaxis, vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](../../t-sql/language-reference.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Nombre**  
 Escriba un nombre único para la tarea Ejecutar SQL en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describa la tarea Ejecutar SQL. Como práctica recomendada, describa la tarea en función de su objetivo para que los paquetes se autodocumenten y su mantenimiento resulte sencillo.  
  
 **TimeOut**  
 Especifique la duración máxima en segundos de la ejecución de la tarea antes de exceder el tiempo de espera. Un valor de 0 indica un tiempo infinito. El valor predeterminado es 0.  
  
> [!NOTE]  
>  En los procedimientos almacenados no se excederá el tiempo de espera si imitan la funcionalidad de espera al proporcionar un tiempo para la realización de conexiones y finalización de las transacciones superior al número de segundos especificado en **TimeOut**. Sin embargo, los procedimientos almacenados que ejecutan consultas siempre están sujetos a la restricción de tiempo especificada en **TimeOut**.  
  
 **CodePage**  
 Especifique la página de códigos que desea utilizar para traducir los valores Unicode a variables. El valor predeterminado es la página de códigos del equipo local.  
  
> [!NOTE]  
>  Cuando la tarea Ejecutar SQL utiliza un administrador de conexiones ADO u ODBC, la propiedad **CodePage** no está disponible. Si la solución requiere el uso de una página de códigos, utilice un administrador de conexiones OLE DB o ADO.NET con la tarea Ejecutar SQL.  
  
 **TypeConversionMode**  
 Cuando establece esta propiedad en **Allowed**, la tarea Ejecutar SQL intentará convertir el parámetro de salida y los resultados de la consulta al tipo de datos de la variable a la que se asignan los resultados. Esto se aplica al tipo de conjunto de resultados de **Fila única** .  
  
 **ResultSet**  
 Especifique el tipo de resultados esperado tras la ejecución de la instrucción SQL. Elija **Fila única**, **Conjunto de resultados completo**, **XML**o **Ninguno**.  
  
 **ConnectionType**  
 Elija el tipo de administrador de conexiones que desea utilizar para conectarse al origen de datos. Entre los tipos de conexión disponibles se encuentran **OLE DB**, **ODBC**, **ADO**, **ADO.NET** y **SQLMOBILE**.  
  
 **Temas relacionados:** [Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md), [Administrador de conexiones ODBC](../../integration-services/connection-manager/odbc-connection-manager.md), [Administrador de conexiones ADO](../../integration-services/connection-manager/ado-connection-manager.md), [Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md), [Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Connection**  
 Elija la conexión en la lista de administradores de conexión definidos. Para crear una conexión nueva, seleccione \<**New connection...**>.  
  
 **SQLSourceType**  
 Seleccione el tipo de origen de la instrucción SQL que ejecuta la tarea.  
  
 Dependiendo del tipo de administrador de conexiones que utiliza la tarea Ejecutar SQL, debe utilizar marcadores de parámetros específicos en instrucciones SQL con parámetros.    
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen para una instrucción Transact-SQL. Si selecciona este valor, se mostrará la opción dinámica **SQLStatement**.|  
|**Conexión de archivos**|Seleccione un archivo que contenga una instrucción Transact-SQL. Si selecciona esta opción, se mostrará la opción dinámica **FileConnection**.|  
|**Variable**|Establezca el origen a una variable que defina la instrucción Transact-SQL. Si selecciona este valor, se mostrará la opción dinámica **SourceVariable**.|  
  
 **QueryIsStoredProcedure**  
 Indica que la instrucción SQL especificada es un procedimiento almacenado. Esta propiedad es de solo lectura/escritura si la tarea utiliza el administrador de conexiones ADO. En caso contrario, la propiedad es de solo lectura y su valor es **false**.  
  
 **BypassPrepare**  
 Indique si la instrucción SQL está preparada.  **true** omite la preparación; **false** prepara la instrucción SQL antes de ejecutarla. Esta opción solo estará disponible con las conexiones OLE DB que admiten la preparación.  
  
 **Temas relacionados:**  [Ejecución preparada](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Browse**  
 Busque un archivo que contenga una instrucción SQL en el cuadro de diálogo **Abrir** . Seleccione el archivo en el que desea copiar el contenido del archivo como una instrucción SQL en la propiedad **SQLStatement** .  
  
 **Generar consulta**  
 Cree una instrucción SQL con el cuadro de diálogo **Generador de consultas** , una herramienta gráfica usada para crear consultas. Esta opción estará disponible si la opción **SQLSourceType** se establece en **Entrada directa**.  
  
 **Analizar consulta**  
 Valide la sintaxis de la instrucción SQL.  
  
### <a name="sqlsourcetype-dynamic-options"></a>Opciones dinámicas de SQLSourceType  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Entrada directa  
 **SQLStatement**  
 Escriba la instrucción SQL que quiere ejecutar en el cuadro de opción, o bien haga clic en el botón Examinar […] para escribir la instrucción SQL en el cuadro de diálogo **Escribir consulta SQL**; también puede hacer clic en **Generar consulta** para escribir la instrucción en el cuadro de diálogo **Generador de consultas**.  
  
 **Temas relacionados:** [Generador de consultas](../integration-services-ssis-queries.md)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = Conexión de archivos  
 **FileConnection**  
 Seleccione un administrador de conexiones de archivos existente o haga clic en \<**New connection...**> para crear uno nuevo.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../connection-manager/file-connection-manager.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variable  
 **SourceVariable**  
 Seleccione una variable existente o haga clic en \<**New variable...**> para crear una nueva.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](../integration-services-ssis-variables.md)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>Página Asignación de parámetros: Editor de la tarea Ejecutar SQL
Use la página **Asignación de parámetros** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para asignar variables a los parámetros de la instrucción SQL.  
  
### <a name="options"></a>Opciones  
 **Nombre de variable**  
 Tras hacer clic en **Agregar** para agregar una asignación de parámetros, seleccione en la lista una variable del sistema o definida por el usuario, o haga clic en \<**New variable...**> para agregar una nueva variable mediante el cuadro de diálogo **Agregar variable**.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 **Dirección**  
 Permite seleccionar la dirección del parámetro. Asigne cada variable a un parámetro de entrada o de salida, o bien a un código de retorno.  
  
 **Tipo de datos**  
 Seleccione el tipo de datos del parámetro. La lista de tipos de datos disponibles es específica del proveedor seleccionado en el administrador de conexiones utilizado por la tarea.  
  
 **Nombre de parámetro**  
 Proporcione un nombre de parámetro.  
  
 Dependiendo del tipo de administrador de conexiones que utiliza la tarea, se utilizarán números o nombres de parámetro. Algunos tipos de administradores de conexión requieren que el primer carácter del nombre del parámetro sea el signo \@, nombres específicos como \@Param1 o nombres de columnas como nombres de parámetro.  
  
 **Tamaño del parámetro**  
 Proporcione el tamaño de los parámetros que tienen longitud variable, como cadenas y campos binarios.  
  
 Este valor garantiza que el proveedor asigna el espacio suficiente para los valores de parámetro de longitud variable.  
  
 **Add (Agregar)**  
 Haga clic para agregar una asignación de parámetros.  
  
 **Remove**  
 Seleccione una asignación de parámetros de la lista y después haga clic en **Quitar**.  
 
## <a name="result-set-page---execute-sql-task-editor"></a>Página Conjunto de resultados: Editor de la tarea Ejecutar SQL
Utilice la página **Conjunto de resultados** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para asignar el resultado de la instrucción SQL a variables nuevas o existentes. Las opciones de este cuadro de diálogo están deshabilitadas si se define **Conjunto de resultados** de la página General como **Ninguno**.  
  
### <a name="options"></a>Opciones  
 **Nombre del resultado**  
 Después de hacer clic en **Agregar**y de agregar un conjunto de asignaciones de conjuntos de resultados, asigne un nombre al resultado. Deberá utilizar nombres de resultados específicos dependiendo del tipo de conjunto de resultados.  
  
 Si el tipo de conjunto de resultados es **Fila única**, puede utilizar el nombre de una columna devuelta por la consulta o el número que representa la posición de una columna en la lista de columnas de una de las columnas devueltas por la consulta.  
  
 Si el tipo de conjunto de resultados es **Conjunto de resultados completo** o **XML**, debe utilizar 0 como nombre del conjunto de resultados.  
 
  
 **Nombre de variable**  
 Para asignar el conjunto de resultados a una variable, seleccione una variable o haga clic en \<**New variable...**> para agregar una variable nueva con el cuadro de diálogo **Agregar variable**.  
  
 **Add (Agregar)**  
 Haga clic para agregar una asignación de conjuntos de resultados.  
  
 **Remove**  
 Seleccione de la lista una asignación de conjuntos de resultados y, después, haga clic en **Quitar**.  
 
## <a name="parameters-in-the-execute-sql-task"></a>Parámetros en la tarea Ejecutar SQL
Las instrucciones SQL y los procedimientos almacenados suelen usar parámetros de **input** , parámetros de **output** entrada y códigos de retorno. En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], la tarea Ejecutar SQL admite los tipos de parámetros **Input**, **Output**y **ReturnValue** . Utilice el tipo **Input** para parámetros de entrada, **Output** para parámetros de salida y **ReturnValue** para códigos de retorno.  
  
> [!NOTE]  
>  Solo puede usar parámetros en una tarea Ejecutar SQL si el proveedor de datos los admite.  
  
 Los parámetros de los comandos SQL, incluidas las consultas y los procedimientos almacenados, se asignan a las variables definidas por el usuario que se crean dentro del ámbito de la tarea Ejecutar SQL, un contenedor primario o dentro del ámbito del paquete. Los valores de las variables pueden establecerse en tiempo de diseño o rellenarse dinámicamente en tiempo de ejecución. También se pueden asignar parámetros a las variables del sistema. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) y [Variables del sistema](../../integration-services/system-variables.md).  
  
 Sin embargo, trabajar con parámetros y códigos de retorno en una tarea Ejecutar SQL implica algo más que simplemente saber qué tipos de parámetros admite la tarea y cómo se asignarán. Hay requisitos de uso adicionales e instrucciones que se deben seguir para utilizar correctamente los parámetros y códigos de retorno en la tarea Ejecutar SQL. El resto de este tema abarca estos requisitos de uso e instrucciones:  
  
-   [Usar nombres y marcadores de parámetros](#Parameter_names_and_markers)  
  
-   [Usar parámetros con tipos de datos de fecha y hora](#Date_and_time_data_types)  
  
-   [Usar parámetros en cláusulas WHERE](#WHERE_clauses)  
  
-   [Usar parámetros con procedimientos almacenados](#Stored_procedures)  
  
-   [Obtener valores de códigos de retorno](#Return_codes)    
  
###  <a name="parameter-names-and-markers"></a><a name="Parameter_names_and_markers"></a> Nombres y marcadores de parámetros  
 En función del tipo de conexión que utiliza la tarea Ejecutar SQL, la sintaxis del comando SQL usa marcadores de parámetros diferentes. Por ejemplo, el tipo de administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] necesita que el comando SQL use un marcador de parámetro con el formato **\@varParameter**, mientras que el tipo de conexión OLE DB necesita el signo de interrogación (?) como marcador de parámetro.  
  
 Los nombres que puede utilizar como nombres de parámetros en las asignaciones entre variables y parámetros también varían según el tipo de Administrador de conexiones. Por ejemplo, el tipo de Administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] utiliza un nombre definido por el usuario con el prefijo \@, mientras que el tipo de Administrador de conexiones OLE DB requiere que se utilice el valor numérico de un ordinal basado en 0 como nombre de parámetro.  
  
 La tabla siguiente resume los requisitos de los comandos SQL para los tipos de Administrador de conexiones que puede utilizar la tarea Ejecutar SQL.  
  
|Tipo de conexión|Marcador de parámetro|Nombre de parámetro|Comando SQL (ejemplo)|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|\@\<parameter name>|\@\<parameter name>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL y OLE DB|?|0, 1, 2, 3…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>Usar parámetros con administradores de conexiones ADO.NET y ADO  
 Los administradores de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] y ADO tienen requisitos concretos para los comandos SQL que utilizan parámetros:  
  
-   Los administradores de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] requieren que el comando SQL utilice nombres de parámetros como marcadores de parámetros. Esto significa que las variables se pueden asignar directamente a los parámetros. Por ejemplo, la variable `@varName` se asigna al parámetro denominado `@parName` y proporciona un valor al parámetro `@parName`.  
  
-   Los administradores de conexiones ADO requieren que el comando SQL utilice signos de interrogación (?) como marcadores de parámetros. Sin embargo, puede utilizar cualquier nombre definido por el usuario, salvo valores enteros, como nombres de parámetro.  
  
 Para proporcionar valores a los parámetros, se asignan variables a los nombres de parámetro. Después, la tarea Ejecutar SQL utiliza el valor ordinal del nombre del parámetro de la lista de parámetros para cargar los valores de las variables en los parámetros.  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Usar parámetros con administradores de conexiones en EXCEL, ODBC y OLE DB  
 Los administradores de conexiones de Excel, ODBC y OLE DB requieren que el comando SQL utilice signos de interrogación (?) como marcadores de parámetros y valores numéricos basados en 0 o en 1 como nombres de los parámetros. Si la tarea Ejecutar SQL utiliza el Administrador de conexiones ODBC, el nombre de parámetro que se asigna al primer parámetro en la consulta se denomina 1; de lo contrario, el parámetro se denomina 0. Para los parámetros siguientes, el valor numérico del nombre de parámetro indica el parámetro en el comando SQL al que se asigna el nombre de parámetro. Por ejemplo, el parámetro denominado 3 se asigna al tercer parámetro, que se representa con un signo de interrogación (?) en el comando SQL.  
  
 Para proporcionar valores a los parámetros, se asignan variables a los nombres de parámetros y la tarea Ejecutar SQL utiliza el valor ordinal del nombre del parámetro para cargar valores de variables a parámetros.  
  
 En función del proveedor que utiliza el Administrador de conexiones, es posible que no se acepten algunos tipos de datos OLE DB. Por ejemplo, el controlador de Excel reconoce solo un conjunto limitado de tipos de datos. Para obtener más información sobre el comportamiento del proveedor Jet con el controlador de Excel, vea [Excel Source](../../integration-services/data-flow/excel-source.md).  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>Usar parámetros con administradores de conexiones OLE DB  
 Cuando la tarea Ejecutar SQL usa el Administrador de conexiones OLE DB, está disponible la propiedad BypassPrepare de la tarea. Debería establecer esta propiedad en **true** si la tarea Ejecutar SQL utiliza instrucciones SQL con parámetros.  
  
 Cuando se usa un Administrador de conexiones OLE DB, no se pueden utilizar subconsultas con parámetros, ya que la tarea Ejecutar SQL no puede derivar la información de los parámetros a través del proveedor OLE DB. Sin embargo, puede utilizar una expresión para concatenar los valores de los parámetros en la cadena de consulta y establecer la propiedad SqlStatementSource de la tarea.  
  
###  <a name="use-parameters-with-date-and-time-data-types"></a><a name="Date_and_time_data_types"></a> Usar parámetros con tipos de datos de fecha y hora  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Usar parámetros de fecha y hora con administradores de conexiones ADO y ADO.NET  
 Al leer datos de los tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( **time** y **datetimeoffset**), una tarea Ejecutar SQL que usa el Administrador de conexiones ADO o [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tiene los requisitos adicionales siguientes:  
  
-   Para los datos de **time** , un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] necesita que estos datos se almacenen en un parámetro cuyo tipo sea **Input** o **Output**, y cuyo tipo de datos sea **string**.  
  
-   Con los datos de **datetimeoffset** , un administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] necesita que estos datos estén almacenados en uno de los parámetros siguientes:  
  
    -   Un parámetro cuyo tipo de parámetro es **Input** y cuyo tipo de datos es **string**.  
  
    -   Un parámetro cuyo tipo de parámetro es **Output** o **ReturnValue**, y cuyo tipo de datos es **datetimeoffset**, **string**o **datetime2**. Si selecciona un parámetro cuyo tipo de datos es **string** o **datetime2**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] convierte los datos a string o datetime2.  
  
-   Un administrador de conexiones ADO requiere que los datos de tipo **time** o **datetimeoffset** estén almacenados en un parámetro cuyo tipo de parámetro sea **Input** o **Output**, y cuyo tipo de datos sea **adVarWchar**.  
  
 Para más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo se asignan a los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) y [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>Usar parámetros de fecha y hora con administradores de conexiones OLE DB  
 Al usar el administrador de conexiones OLE DB, una tarea Ejecutar SQL tiene requisitos de almacenamiento específicos para los datos de los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **date**, **time**, **datetime**, **datetime2**y **datetimeoffset**. Debe almacenar estos datos en uno de los tipos de parámetros siguientes:  
  
-   Un parámetro de entrada del tipo de datos NVARCHAR.  
  
-   Un parámetro de salida del tipo de datos adecuado, tal y como se enumera en la tabla siguiente.  
  
    |Tipo de parámetro**Output**|Tipo de datos de fecha|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**, **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 Si los datos no están almacenados en el parámetro de entrada o de salida adecuado, se produce un error en el paquete.  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>Usar parámetros de fecha y hora con administradores de conexiones ODBC  
 Al usar el administrador de conexiones ODBC, una tarea Ejecutar SQL tiene requisitos de almacenamiento específicos para los datos de uno de los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **date**, **time**, **datetime**, **datetime2**o **datetimeoffset**. Debe almacenar estos datos en uno de los tipos de parámetros siguientes:  
  
-   Un parámetro de **entrada** del tipo de datos SQL_WVARCHAR  
  
-   Un parámetro **output** del tipo de datos adecuado, tal y como se enumera en la tabla siguiente.  
  
    |Tipo de parámetro**Output**|Tipo de datos de fecha|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> O bien<br /><br /> SQL_TIMESTAMP|**datetime**, **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 Si los datos no están almacenados en el parámetro de entrada o de salida adecuado, se produce un error en el paquete.  
  
###  <a name="use-parameters-in-where-clauses"></a><a name="WHERE_clauses"></a> Usar parámetros en cláusulas WHERE  
 Los comandos SELECT, INSERT, UPDATE y DELETE suelen incluir cláusulas WHERE para especificar filtros que definen las condiciones que debe cumplir cada fila de las tablas de origen con el fin de satisfacer los requisitos de un comando SQL. Los parámetros proporcionan los valores de filtro en las cláusulas WHERE.  
  
 Puede utilizar marcadores de parámetros para proporcionar valores de parámetros de forma dinámica. Las reglas para los marcadores y nombres de parámetros que se pueden utilizar en la instrucción SQL dependen del tipo de Administrador de conexiones que utiliza la tarea Ejecutar SQL.  
  
 La tabla siguiente enumera ejemplos del comando SELECT por tipo de Administrador de conexiones. Las instrucciones INSERT, UPDATE y DELETE son similares. Los ejemplos utilizan el comando SELECT para devolver los productos de la tabla **Product** de [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] que tienen un valor de **ProductID** mayor y menor que los valores especificados por dos parámetros.  
  
|Tipo de conexión|Sintaxis de SELECT|  
|---------------------|-------------------|  
|EXCEL, ODBC y OLE DB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 Los ejemplos necesitarán parámetros que tengan los siguientes nombres:  
  
-   Los administradores de conexión en EXCEL y OLED DB utilizan los nombres de parámetro 0 y 1. El tipo de conexión ODBC utiliza 1 y 2.  
  
-   El tipo de conexión ADO podría utilizar cualquier par de nombres de parámetros, como Param1 y Param2, pero los parámetros deben asignarse por su posición ordinal en la lista de parámetros.  
  
-   El tipo de conexión de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] utiliza los nombres de parámetros \@parmMinProductID y \@parmMaxProductID.  
  
###  <a name="use-parameters-with-stored-procedures"></a><a name="Stored_procedures"></a> Usar parámetros con procedimientos almacenados  
 Los comandos SQL que ejecutan procedimientos almacenados también pueden usar la asignación de parámetros. Las reglas sobre el uso de marcadores y nombres de parámetros dependen del tipo de Administrador de conexiones que utiliza la tarea Ejecutar SQL, del mismo modo que sucede con las consultas con parámetros.  
  
 La tabla siguiente enumera ejemplos del comando EXEC por tipo de Administrador de conexiones. Los ejemplos ejecutan el procedimiento almacenado **uspGetBillOfMaterials** en [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]. El procedimiento almacenado usa los parámetros de **entrada** `@StartProductID` y `@CheckDate`.  
  
|Tipo de conexión|Sintaxis de EXEC|  
|---------------------|-----------------|  
|EXCEL y OLE DB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Para obtener más información sobre la sintaxis de la llamada ODBC, consulte el tema sobre [Parámetros de procedimientos](../../odbc/reference/develop-app/procedure-parameters.md), en la Referencia del programador de ODBC de MSDN Library.|  
|ADO|Si IsQueryStoredProcedure se establece en **False**, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Si IsQueryStoredProcedure se establece en **True**, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Si IsQueryStoredProcedure se establece en **False**, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Si IsQueryStoredProcedure se establece en **True**, `uspGetBillOfMaterials`|  
  
 Para utilizar parámetros de salida, la sintaxis requiere que la palabra clave OUTPUT siga a cada marcador de parámetro. Por ejemplo, la sintaxis del parámetro de salida siguiente es correcta: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Para más información sobre el uso de parámetros de entrada y salida con procedimientos almacenados de Transact-SQL, vea [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
 
### <a name="map-query-parameters-to-variables"></a>Asignar parámetros de consulta a variables
En esta sección se describe cómo utilizar una instrucción SQL con parámetros en la tarea Ejecutar SQL, y crear asignaciones entre las variables y los parámetros en la instrucción SQL.  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Si el paquete no incluye en ese momento una tarea Ejecutar SQL, agregue una al flujo de control del paquete. Para más información, vea [Agregar o eliminar tareas o contenedores en un flujo de control](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Haga doble clic en la tarea Ejecutar SQL.  
  
6.  Proporcione un comando SQL con parámetros en una de las siguientes maneras:  
  
    -   Use entrada directa y escriba el comando SQL en la propiedad SQLStatement.  
  
    -   Use entrada directa, haga clic en **Generar consulta**y luego cree un comando SQL mediante las herramientas gráficas proporcionadas por el Generador de consultas.  
  
    -   Use una conexión de archivo y luego haga referencia al archivo que contiene el comando SQL.  
  
    -   Use una variable y luego haga referencia a la variable que contiene el comando SQL.  
  
     Los marcadores de parámetros que utiliza en las instrucciones SQL con parámetros dependen del tipo de conexión que utiliza la tarea Ejecutar SQL.  
  
    |Tipo de conexión|Marcador de parámetro|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET y SQLMOBILE|\@\<parameter name>|  
    |ODBC|?|  
    |EXCEL y OLE DB|?|  
  
     La tabla siguiente enumera ejemplos del comando SELECT por tipo de Administrador de conexiones. Los parámetros proporcionan los valores de filtro en las cláusulas WHERE. Los ejemplos utilizan el comando SELECT para devolver los productos de la tabla **Product** de [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] que tienen un valor de **ProductID** mayor y menor que los valores especificados por dos parámetros.  
  
    |Tipo de conexión|Sintaxis de SELECT|  
    |---------------------|-------------------|  
    |EXCEL, ODBC y OLE DB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  Haga clic en **Asignación de parámetros**.  
  
8.  Para agregar una asignación de parámetros, haga clic en **Agregar**.  
  
9. Escriba un nombre en el cuadro **Nombre de parámetro** .  
  
     Los nombres de parámetros que utiliza dependen del tipo de conexión que utiliza la tarea Ejecutar SQL.  
  
    |Tipo de conexión|Nombre de parámetro|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2…|  
    |ADO.NET y SQLMOBILE|\@\<parameter name>|  
    |ODBC|1, 2, 3…|  
    |EXCEL y OLE DB|0, 1, 2, 3…|  
  
10. En la lista **Nombre de variable** , seleccione una variable. Para más información, vea [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../integration-services-ssis-variables.md).  
  
11. En la lista **Dirección** , especifique si el parámetro es una entrada, una salida o un valor devuelto.  
  
12. En la lista **Tipo de datos** , seleccione el tipo de datos del parámetro.  
  
    > [!IMPORTANT]  
    >  El tipo de datos del parámetro debe ser compatible con el tipo de datos de la variable.  
  
13. Repita los pasos del 8 al 11 para cada parámetro en la instrucción SQL.  
  
    > [!IMPORTANT]  
    >  El orden de las asignaciones de parámetros debe ser el mismo que el orden en que aparecen los parámetros en la instrucción SQL.  
  
14. Haga clic en **OK**.  

##  <a name="get-the-values-of-return-codes"></a><a name="Return_codes"></a> Obtener los valores de códigos de retorno  
 Un procedimiento almacenado puede devolver un valor entero, denominado código de retorno, para indicar el estado de ejecución de un procedimiento. Para implementar códigos de retorno en la tarea Ejecutar SQL, debe utilizar los parámetros del tipo **ReturnValue** .  
  
 La tabla siguiente enumera, por tipo de conexión, algunos ejemplos de comandos EXEC que implementan códigos de retorno. Todos los ejemplos utilizan un parámetro de **input** . Las reglas del uso de marcadores y nombres de parámetros son las mismas para todos los tipos de parámetros: **Input**, **Output** y **ReturnValue**.  
  
 Algunas sintaxis no admiten literales en los parámetros. En tal caso, debe proporcionar el valor del parámetro mediante una variable.  
  
|Tipo de conexión|Sintaxis de EXEC|  
|---------------------|-----------------|  
|EXCEL y OLE DB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Para obtener más información sobre la sintaxis de la llamada ODBC, consulte el tema sobre [Parámetros de procedimientos](../../odbc/reference/develop-app/procedure-parameters.md), en la Referencia del programador de ODBC de MSDN Library.|  
|ADO|Si IsQueryStoreProcedure se establece en **False**, `EXEC ? = myStoredProcedure 1`<br /><br /> Si IsQueryStoreProcedure se establece en **True**, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Establecer IsQueryStoreProcedure en **True**.<br /><br /> `myStoredProcedure`|  
  
 En la sintaxis mostrada en la tabla anterior, la tarea Ejecutar SQL utiliza el tipo de origen **Entrada directa** para ejecutar el procedimiento almacenado. La tarea Ejecutar SQL también puede utilizar el tipo de origen **Conexión de archivos** para ejecutar un procedimiento almacenado. Con independencia de si la tarea Ejecutar SQL utiliza el tipo de origen **Entrada directa** o **Conexión de archivos** , use un parámetro del tipo **ReturnValue** para implementar el código de retorno.
  
 Para más información sobre el uso de códigos de retorno con procedimientos almacenados de Transact-SQL, vea [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md).  
  
## <a name="result-sets-in-the-execute-sql-task"></a>Conjuntos de resultados en la tarea Ejecutar SQL
 En un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , el hecho de que se devuelva un conjunto de resultados a la tarea Ejecutar SQL depende del tipo de comando SQL que use la tarea. Por ejemplo, una instrucción SELECT suele devolver un conjunto de resultados; en cambio, una instrucción INSERT no lo devuelve.  
  
 El contenido del conjunto de resultados también varía en función del comando SQL. Por ejemplo, el conjunto de resultados de una instrucción SELECT puede contener cero filas, una fila o muchas filas. Sin embargo, el conjunto de resultados de una instrucción SELECT que devuelve un recuento o suma contiene exclusivamente una fila.  
  
 Trabajar con conjuntos de resultados en una tarea Ejecutar SQL es algo más que saber si el comando SQL devuelve un conjunto de resultados y cuál es el contenido de este. Existen requisitos de uso e instrucciones adicionales para usar correctamente los conjuntos de resultados en la tarea Ejecutar SQL. El resto de este tema abarca estos requisitos de uso e instrucciones:  
  
-   [Especificar un tipo de conjunto de resultados](#Result_set_type)  
  
-   [Rellenar una variable con un conjunto de resultados](#Populate_variable_with_result_set)  
  
###  <a name="specify-a-result-set-type"></a><a name="Result_set_type"></a> Especificar un tipo de conjunto de resultados  
 La tarea Ejecutar SQL admite los siguientes tipos de conjuntos de resultados:  
  
-   El conjunto de resultados **Ninguno** se usa cuando la consulta no devuelve ningún resultado. Por ejemplo, este conjunto de resultados se utiliza para consultas que agregan, cambian y eliminan registros de una tabla.  
  
-   El conjunto de resultados **Fila única** se usa cuando la consulta devuelve una sola fila. Por ejemplo, este conjunto de resultados se utiliza en una instrucción SELECT que devuelve un recuento o suma.  
  
-   El conjunto de resultados **Conjunto de resultados completo** se usa cuando la consulta devuelve múltiples filas. Por ejemplo, este conjunto de resultados se usa para una instrucción SELECT que recupera todas las filas de una tabla.  
  
-   El conjunto de resultados **XML** se usa cuando la consulta devuelve un conjunto de resultados en formato XML. Por ejemplo, este conjunto de resultados se usa para una instrucción SELECT que incluya una cláusula FOR XML.  
  
 Si la tarea Ejecutar SQL utiliza el conjunto de resultados **Conjunto de resultados completo** y la consulta devuelve varios conjuntos de filas, la tarea solo devuelve el primero de ellos. Si el primer conjunto de filas genera un error, la tarea lo notifica. Si otros conjuntos de filas generan errores, la tarea no los notifica.  
  
###  <a name="populate-a-variable-with-a-result-set"></a><a name="Populate_variable_with_result_set"></a> Rellenar una variable con un conjunto de resultados  
 Puede enlazar el conjunto de resultados devuelto por una consulta con una variable definida por el usuario si el tipo del conjunto de resultados es una fila individual, un conjunto de filas o XML.  
  
 Si el tipo de conjunto de resultados es **Fila única**, puede enlazar una columna del resultado devuelto a una variable utilizando el nombre de la columna como nombre del conjunto de resultados, o puede utilizar la posición ordinal de la columna en la lista de columnas como dicho nombre. Por ejemplo, el nombre del conjunto de resultados para la consulta `SELECT Color FROM Production.Product WHERE ProductID = ?` puede ser **Color** o **0**. Si la consulta devuelve varias columnas y desea obtener acceso a los valores de todas ellas, debe enlazar cada columna a una variable distinta. Si asigna columnas a variables utilizando números como nombre de los conjuntos de resultados, los números reflejan el orden de aparición de las columnas en la lista de columnas de la consulta. Por ejemplo, en la consulta `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`, puede utilizar 0 para la columna **Color** y 1 para la columna **ListPrice** . La capacidad de utilizar un nombre de columna como nombre del conjunto de resultados dependerá del proveedor para el que se haya configurado la tarea. No todos los proveedores ponen los nombres de columna a disposición.  
  
 Es posible que algunas consultas que devuelven un valor único no incluyan nombres de columnas. Por ejemplo, la instrucción `SELECT COUNT (*) FROM Production.Product` no devuelve un nombre de columna. Puede tener acceso al resultado devuelto utilizando la posición ordinal 0 como nombre del resultado. Para tener acceso al resultado devuelto por nombre de columna, la consulta debe incluir una cláusula AS \<alias name> para proporcionar un nombre de columna. La instrucción `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`proporciona la columna **CountOfProduct** . Luego puede tener acceso al resultado devuelto utilizando el nombre de la columna **CountOfProduct** o la posición ordinal 0.  
  
 Si el tipo de conjunto de resultados es **Conjunto de resultados completo** o **XML**, debe utilizar 0 como nombre del conjunto de resultados.  
  
 Cuando se asigna una variable a un conjunto de resultados con el tipo de conjunto de resultados **Fila única** , la variable debe tener un tipo de datos que sea compatible con el tipo de datos de la columna contenida en el conjunto de resultados. Por ejemplo, un conjunto de resultados que contiene una columna con un tipo de datos **String** no se puede asignar a una variable con un tipo de datos numérico. Cuando establece la propiedad **TypeConversionMode** en **Allowed**, la tarea Ejecutar SQL intentará convertir el parámetro de salida y los resultados de la consulta al tipo de datos de la variable a la que se han asignado los resultados.  
  
 Un conjunto de resultados XML solamente se puede asignar a una variable con el tipo de datos **String** o **Object** . Si la variable tiene el tipo de datos **String** , la tarea Ejecutar SQL devuelve una cadena y el origen XML puede consumir los datos XML. Si la variable tiene el tipo de datos **Object** , la tarea Ejecutar SQL devuelve un objeto del modelo de objetos de documento (DOM).  
  
 Un **Conjunto de resultados completo** se debe asignar a una variable del tipo de datos **Object** . El resultado devuelto es un objeto de conjunto de filas. Puede usar un contenedor de bucle Foreach para extraer los valores de las filas de una tabla almacenados en la variable Object y almacenarlos en las variables de paquete y, entonces, utilizar una tarea Script para escribir los datos almacenados en variables de paquetes en un archivo. Para ver una demostración de cómo usar un contenedor de bucle Foreach y una tarea Script, consulte el ejemplo en CodePlex, [Ejecutar parámetros SQL y conjuntos de resultados](https://go.microsoft.com/fwlink/?LinkId=157863), en msftisprodsamples.codeplex.com.  
  
 En la tabla siguiente se resumen los tipos de datos de variables que se pueden asignar a conjuntos de resultados.  
  
|Tipo de conjunto de resultados|Tipo de datos de variable|Tipo de objeto|  
|---------------------|---------------------------|--------------------|  
|Fila única|Cualquier tipo que sea compatible con la columna de tipo del conjunto de resultados.|No aplicable|  
|Conjunto de resultados completo|**Object**|Si la tarea usa un administrador de conexiones nativo, incluidos los administradores de conexiones ADO, OLE DB, Excel y ODBC, el objeto devuelto es un **Recordset**de ADO.<br /><br /> Si la tarea usa un administrador de conexiones administrado, como el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , el objeto devuelto es un objeto **System.Data.DataSet**.<br /><br /> Puede utilizar una tarea Script para tener acceso al objeto **System.Data.DataSet** , tal como se muestra en el ejemplo siguiente.<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**String**|**String**|  
|XML|**Object**|Si la tarea usa un administrador de conexiones nativo, incluidos los administradores de conexiones ADO, OLE DB, Excel y ODBC, el objeto devuelto es un objeto **MSXML6.IXMLDOMDocument**.<br /><br /> Si la tarea usa un administrador de conexiones administrado, como el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , el objeto devuelto es un objeto **System.Xml.XmlDocument**.|  
  
 La variable puede definirse en el ámbito de la tarea Ejecutar SQL o en el ámbito del paquete. Si la variable tiene ámbito de paquete, el conjunto de resultados estará disponible para otras tareas y otros contenedores del paquete, así como para cualquier paquete ejecutado por la tarea Ejecutar paquete o Ejecutar paquete DTS 2000.  
  
 Cuando se asigna una variable a un conjunto de resultados de **fila única** , los valores que no son de cadena devueltos por la instrucción SQL se convierten en cadenas cuando se cumplen las condiciones siguientes:  
  
-   La propiedad **TypeConversionMode** se establece en True. Establezca el valor de propiedad en la ventana Propiedades o mediante el **Editor de la tarea Ejecutar SQL**.  
  
-   La conversión no producirá el truncamiento de datos.  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>asignar conjuntos de resultados a variables en una tarea Ejecutar SQL
En esta sección se describe cómo crear una asignación entre un conjunto de resultados y una variable en una tarea Ejecutar SQL. La asignación de un conjunto de resultados a una variable hace que el conjunto de resultados esté disponible para otros elementos del paquete. Por ejemplo, un script de la tarea Script puede leer la variable y luego utilizar los valores del conjunto de resultados, o un origen XML puede consumir el conjunto de resultados almacenados en una variable. Si un paquete primario genera el conjunto de resultados, este conjunto de resultados se puede poner a disposición de un paquete secundario llamado por la tarea Ejecutar paquete asignando el conjunto de resultados a una variable del paquete primario, y luego creando una configuración de variable de paquete primario en el paquete secundario a fin de almacenar el valor de la variable primaria.  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el **Explorador de soluciones**, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Si el paquete no incluye en ese momento una tarea Ejecutar SQL, agregue una al flujo de control del paquete. Para más información, vea [Agregar o eliminar tareas o contenedores en un flujo de control](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Haga doble clic en la tarea Ejecutar SQL.  
  
6.  En el cuadro de diálogo **Editor de la tarea Ejecutar SQL** , en la página **General** , seleccione el tipo de conjunto de resultados **Fila única**, **Conjunto de resultados completo**o **XML** .  

7.  Haga clic en **Conjunto de resultados**.  
  
8.  Para agregar una asignación de conjunto de resultados, haga clic en **Agregar**.  
  
9. En la lista **Nombre de variable** , seleccione una variable o cree una variable nueva. Para más información, vea [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../integration-services-ssis-variables.md).  
  
10. En la lista **Nombre del resultado** , opcionalmente, modifique el nombre del conjunto de resultados.  
  
     En general, puede usar el nombre de columna como nombre del conjunto de resultados, o puede usar la posición ordinal de la columna en la lista de columnas como conjunto de resultados. La posibilidad de usar un nombre de columna como el nombre del conjunto de resultados depende del proveedor para el que se haya configurado la tarea. No todos los proveedores ponen los nombres de columna a disposición.  
  
11. Haga clic en **OK**.  

## <a name="troubleshoot-the-execute-sql-task"></a>Solucionar problemas de la tarea Ejecutar SQL  
 Puede registrar las llamadas que realiza la tarea Ejecutar SQL a proveedores de datos externos. Puede usar esta capacidad de registro para solucionar problemas relacionados con los comandos SQL que ejecuta la tarea Ejecutar SQL. Para registrar las llamadas realizadas por la tarea Ejecutar SQL a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 A veces, un procedimiento almacenado o comando SQL devuelve varios conjuntos de resultados. Estos conjuntos de resultados no solo incluyen los conjuntos de filas resultantes de consultas **SELECT** , sino valores únicos generados por errores de las instrucciones **RAISERROR** o **PRINT** . El hecho de que la tarea omita errores en los conjuntos de resultados que se producen después del primer conjunto de resultados depende del tipo de administrador de conexiones que se use:  
  
-   Si utiliza los administradores de conexiones ADO y OLE DB, la tarea omite los conjuntos de resultados que se producen después del primer conjunto de resultados. Por consiguiente, con estos administradores de conexiones la tarea omite un error devuelto por un procedimiento almacenado o comando SQL cuando el error no forma parte del primer conjunto de resultados.  
  
-   Si utiliza los administradores de conexiones ODBC y ADO.NET, la tarea no omite los conjuntos de resultados que se producen después del primer conjunto de resultados. Con estos administradores de conexiones, la tarea producirá un error cuando un conjunto de resultados distinto del primer conjunto de resultados contenga un error.  
  
### <a name="custom-log-entries"></a>Entradas del registro personalizadas  
 La siguiente tabla contiene la entrada del registro personalizada para la tarea Ejecutar SQL. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Proporciona información sobre las fases de ejecución de la instrucción SQL. Las entradas de registro se escriben cuando la tarea adquiere una conexión con la base de datos, cuando la tarea comienza a preparar la instrucción SQL y una vez que se completa la ejecución de la instrucción SQL. La entrada del registro para la fase de preparación incluye la instrucción SQL que utiliza la tarea.|