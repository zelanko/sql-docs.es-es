---
title: Los parámetros y códigos de retorno en la tarea Ejecutar SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f0899922eb2cdec88e73901f14ebeb6dfe953622
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367218"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>Parámetros y códigos de retorno en la tarea Ejecutar SQL
  Las instrucciones SQL y los procedimientos almacenados suelen usar parámetros de `input`, parámetros de `output` entrada y códigos de retorno. En [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], la tarea Ejecutar SQL admite los tipos de parámetros `Input`, `Output` y `ReturnValue`. Utilice el tipo `Input` para parámetros de entrada, `Output` para parámetros de salida y `ReturnValue` para códigos de retorno.  
  
> [!NOTE]  
>  Solo puede usar parámetros en una tarea Ejecutar SQL si el proveedor de datos los admite.  
  
 Los parámetros de los comandos SQL, incluidas las consultas y los procedimientos almacenados, se asignan a las variables definidas por el usuario que se crean dentro del ámbito de la tarea Ejecutar SQL, un contenedor primario o dentro del ámbito del paquete. Los valores de las variables pueden establecerse en tiempo de diseño o rellenarse dinámicamente en tiempo de ejecución. También se pueden asignar parámetros a las variables del sistema. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) y [Variables del sistema](system-variables.md).  
  
 Sin embargo, trabajar con parámetros y códigos de retorno en una tarea Ejecutar SQL implica algo más que simplemente saber qué tipos de parámetros admite la tarea y cómo se asignarán. Hay requisitos de uso adicionales e instrucciones que se deben seguir para utilizar correctamente los parámetros y códigos de retorno en la tarea Ejecutar SQL. El resto de este tema abarca estos requisitos de uso e instrucciones:  
  
-   [Usar nombres y marcadores de parámetros](#Parameter_names_and_markers)  
  
-   [Usar parámetros con tipos de datos de fecha y hora](#Date_and_time_data_types)  
  
-   [Usar parámetros en cláusulas WHERE](#WHERE_clauses)  
  
-   [Usar parámetros con procedimientos almacenados](#Stored_procedures)  
  
-   [Obtener valores de códigos de retorno](#Return_codes)  
  
-   [Configurar parámetros y códigos de retorno en el Editor de tareas de ejecución SQL](#Configure_parameters_and_return_codes)  
  
##  <a name="Parameter_names_and_markers"></a> Usar nombres de parámetros y marcadores  
 En función del tipo de conexión que utiliza la tarea Ejecutar SQL, la sintaxis del comando SQL usa marcadores de parámetros diferentes. Por ejemplo, el tipo de administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] necesita que el comando SQL use un marcador de parámetro con el formato **\@varParameter**, mientras que el tipo de conexión OLE DB necesita el signo de interrogación (?) como marcador de parámetro.  
  
 Los nombres que puede utilizar como nombres de parámetros en las asignaciones entre variables y parámetros también varían según el tipo de Administrador de conexiones. Por ejemplo, el tipo de Administrador de conexiones de [!INCLUDE[vstecado](../includes/vstecado-md.md)] utiliza un nombre definido por el usuario con el prefijo \@, mientras que el tipo de Administrador de conexiones OLE DB requiere que se utilice el valor numérico de un ordinal basado en 0 como nombre de parámetro.  
  
 La tabla siguiente resume los requisitos de los comandos SQL para los tipos de Administrador de conexiones que puede utilizar la tarea Ejecutar SQL.  
  
|Tipo de conexión|Marcador de parámetro|Nombre del parámetro|Comando SQL (ejemplo)|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|\@\<nombre de parámetro>|\@\<nombre de parámetro>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL y OLE DB|?|0, 1, 2, 3…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>Usar parámetros con ADO.NET y administradores de conexión ADO  
 Los administradores de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] y ADO tienen requisitos concretos para los comandos SQL que utilizan parámetros:  
  
-   Los administradores de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] requieren que el comando SQL utilice nombres de parámetros como marcadores de parámetros. Esto significa que las variables se pueden asignar directamente a los parámetros. Por ejemplo, la variable `@varName` se asigna al parámetro denominado `@parName` y proporciona un valor al parámetro `@parName`.  
  
-   Los administradores de conexiones ADO requieren que el comando SQL utilice signos de interrogación (?) como marcadores de parámetros. Sin embargo, puede utilizar cualquier nombre definido por el usuario, salvo valores enteros, como nombres de parámetro.  
  
 Para proporcionar valores a los parámetros, se asignan variables a los nombres de parámetro. Después, la tarea Ejecutar SQL utiliza el valor ordinal del nombre del parámetro de la lista de parámetros para cargar los valores de las variables en los parámetros.  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Usar parámetros con administradores de conexión en EXCEL, ODBC y OLE DB  
 Los administradores de conexiones de Excel, ODBC y OLE DB requieren que el comando SQL utilice signos de interrogación (?) como marcadores de parámetros y valores numéricos basados en 0 o en 1 como nombres de los parámetros. Si la tarea Ejecutar SQL utiliza el Administrador de conexiones ODBC, el nombre de parámetro que se asigna al primer parámetro en la consulta se denomina 1; de lo contrario, el parámetro se denomina 0. Para los parámetros siguientes, el valor numérico del nombre de parámetro indica el parámetro en el comando SQL al que se asigna el nombre de parámetro. Por ejemplo, el parámetro denominado 3 se asigna al tercer parámetro, que se representa con un signo de interrogación (?) en el comando SQL.  
  
 Para proporcionar valores a los parámetros, se asignan variables a los nombres de parámetros y la tarea Ejecutar SQL utiliza el valor ordinal del nombre del parámetro para cargar valores de variables a parámetros.  
  
 En función del proveedor que utiliza el Administrador de conexiones, es posible que no se acepten algunos tipos de datos OLE DB. Por ejemplo, el controlador de Excel reconoce solo un conjunto limitado de tipos de datos. Para obtener más información sobre el comportamiento del proveedor Jet con el controlador de Excel, vea [Excel Source](data-flow/excel-source.md).  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>Usar parámetros con administradores de conexión OLE DB  
 Cuando la tarea Ejecutar SQL usa el Administrador de conexiones OLE DB, está disponible la propiedad BypassPrepare de la tarea. Debería establecer esta propiedad en `true` si la tarea Ejecutar SQL utiliza instrucciones SQL con parámetros.  
  
 Cuando se usa un Administrador de conexiones OLE DB, no se pueden utilizar subconsultas con parámetros, ya que la tarea Ejecutar SQL no puede derivar la información de los parámetros a través del proveedor OLE DB. Sin embargo, puede utilizar una expresión para concatenar los valores de los parámetros en la cadena de consulta y establecer la propiedad SqlStatementSource de la tarea.  
  
##  <a name="Date_and_time_data_types"></a> Usar parámetros con tipos de fecha y hora  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Usar parámetros de fecha y hora con administradores de conexión ADO y ADO.NET  
 Al leer datos de los tipos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `time` y `datetimeoffset`, una tarea Ejecutar SQL que utiliza el Administrador de conexiones ADO o [!INCLUDE[vstecado](../includes/vstecado-md.md)] tiene los requisitos adicionales siguientes:  
  
-   Para `time` datos, un [!INCLUDE[vstecado](../includes/vstecado-md.md)] connection manager requiere estos datos se almacenen en un parámetro cuyo tipo sea `Input` o `Output`, y cuyo tipo de datos es `string`.  
  
-   Con los datos `datetimeoffset`, un Administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] requiere que estos datos estén almacenados en uno de los parámetros siguientes:  
  
    -   Un parámetro cuyo tipo de parámetro es `Input` y cuyo tipo de datos es `string`.  
  
    -   Un parámetro cuyo tipo de parámetro es `Output` o `ReturnValue`, y cuyo tipo de datos es `datetimeoffset`, `string` o `datetime2`. Si selecciona un parámetro cuyo tipo de datos es `string` o `datetime2`, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] convierte los datos en string o datetime2.  
  
-   Un administrador de conexiones ADO requiere que los datos de tipo `time` o `datetimeoffset` estén almacenados en un parámetro cuyo tipo de parámetro sea `Input` o `Output`, y cuyo tipo de datos sea `adVarWchar`.  
  
 Para más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y cómo se asignan a los tipos de datos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vea [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) y [Tipos de datos de Integration Services](data-flow/integration-services-data-types.md).  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>Usar parámetros de fecha y hora con administradores de conexión OLE DB  
 Al utilizar un Administrador de conexiones OLE DB, una tarea Ejecutar SQL tiene requisitos de almacenamiento concretos para los datos de los tipos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `date`, `time`, `datetime`, `datetime2` y `datetimeoffset`. Debe almacenar estos datos en uno de los tipos de parámetros siguientes:  
  
-   Un parámetro de entrada del tipo de datos NVARCHAR.  
  
-   Un parámetro de salida del tipo de datos adecuado, tal y como se enumera en la tabla siguiente.  
  
    |Tipo de parámetro `Output`|Tipo de datos de fecha|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`, `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 Si los datos no están almacenados en el parámetro de entrada o de salida adecuado, se produce un error en el paquete.  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>Usar parámetros de fecha y hora con administradores de conexión ODBC  
 Al utilizar un Administrador de conexiones ODBC, una tarea Ejecutar SQL tiene requisitos de almacenamiento concretos para uno de los datos de los tipos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `date`, `time`, `datetime`, `datetime2` o `datetimeoffset`. Debe almacenar estos datos en uno de los tipos de parámetros siguientes:  
  
-   Un parámetro de `input` del tipo de datos SQL_WVARCHAR  
  
-   Un parámetro `output` del tipo de datos adecuado, tal y como se enumera en la tabla siguiente.  
  
    |Tipo de parámetro `Output`|Tipo de datos de fecha|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -o bien-<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 Si los datos no están almacenados en el parámetro de entrada o de salida adecuado, se produce un error en el paquete.  
  
##  <a name="WHERE_clauses"></a> Usar parámetros en dónde cláusulas  
 Los comandos SELECT, INSERT, UPDATE y DELETE suelen incluir cláusulas WHERE para especificar filtros que definen las condiciones que debe cumplir cada fila de las tablas de origen con el fin de satisfacer los requisitos de un comando SQL. Los parámetros proporcionan los valores de filtro en las cláusulas WHERE.  
  
 Puede utilizar marcadores de parámetros para proporcionar valores de parámetros de forma dinámica. Las reglas para los marcadores y nombres de parámetros que se pueden utilizar en la instrucción SQL dependen del tipo de Administrador de conexiones que utiliza la tarea Ejecutar SQL.  
  
 La tabla siguiente enumera ejemplos del comando SELECT por tipo de Administrador de conexiones. Las instrucciones INSERT, UPDATE y DELETE son similares. Los ejemplos utilizan el comando SELECT para devolver los productos de la tabla **Product** de [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] que tienen un valor de **ProductID** mayor y menor que los valores especificados por dos parámetros.  
  
|Tipo de conexión|Sintaxis de SELECT|  
|---------------------|-------------------|  
|EXCEL, ODBC y OLE DB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 Los ejemplos necesitarán parámetros que tengan los siguientes nombres:  
  
-   Los administradores de conexión en EXCEL y OLED DB utilizan los nombres de parámetro 0 y 1. El tipo de conexión ODBC utiliza 1 y 2.  
  
-   El tipo de conexión ADO podría utilizar cualquier par de nombres de parámetros, como Param1 y Param2, pero los parámetros deben asignarse por su posición ordinal en la lista de parámetros.  
  
-   El tipo de conexión de [!INCLUDE[vstecado](../includes/vstecado-md.md)] utiliza los nombres de parámetros \@parmMinProductID y \@parmMaxProductID.  
  
##  <a name="Stored_procedures"></a> Usar parámetros con procedimientos almacenados  
 Los comandos SQL que ejecutan procedimientos almacenados también pueden usar la asignación de parámetros. Las reglas sobre el uso de marcadores y nombres de parámetros dependen del tipo de Administrador de conexiones que utiliza la tarea Ejecutar SQL, del mismo modo que sucede con las consultas con parámetros.  
  
 La tabla siguiente enumera ejemplos del comando EXEC por tipo de Administrador de conexiones. Los ejemplos ejecutan el procedimiento almacenado **uspGetBillOfMaterials** en [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]. El procedimiento almacenado usa el `@StartProductID` y `@CheckDate` `input` parámetros.  
  
|Tipo de conexión|Sintaxis de EXEC|  
|---------------------|-----------------|  
|EXCEL y OLE DB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Para obtener más información sobre la sintaxis de la llamada ODBC, consulte el tema sobre [Parámetros de procedimientos](https://go.microsoft.com/fwlink/?LinkId=89462), en la Referencia del programador de ODBC de MSDN Library.|  
|ADO|Si IsQueryStoredProcedure se establece en `False`, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Si IsQueryStoredProcedure se establece en `True`, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Si IsQueryStoredProcedure se establece en `False`, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Si IsQueryStoredProcedure se establece en `True`, `uspGetBillOfMaterials`|  
  
 Para utilizar parámetros de salida, la sintaxis requiere que la palabra clave OUTPUT siga a cada marcador de parámetro. Por ejemplo, la sintaxis del parámetro de salida siguiente es correcta: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Para más información sobre el uso de parámetros de entrada y salida con procedimientos almacenados de Transact-SQL, vea [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
##  <a name="Return_codes"></a> Obtener valores de los códigos de retorno  
 Un procedimiento almacenado puede devolver un valor entero, denominado código de retorno, para indicar el estado de ejecución de un procedimiento. Para implementar códigos de retorno en la tarea Ejecutar SQL, debe utilizar los parámetros del tipo `ReturnValue`.  
  
 La tabla siguiente enumera, por tipo de conexión, algunos ejemplos de comandos EXEC que implementan códigos de retorno. Todos los ejemplos utilizan un parámetro de `input`. Las reglas de cómo usar marcadores de parámetros y los nombres de parámetro son los mismos para todos los tipos de parámetro:`Input`, `Output`, y `ReturnValue`.  
  
 Algunas sintaxis no admiten literales en los parámetros. En tal caso, debe proporcionar el valor del parámetro mediante una variable.  
  
|Tipo de conexión|Sintaxis de EXEC|  
|---------------------|-----------------|  
|EXCEL y OLE DB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Para obtener más información sobre la sintaxis de la llamada ODBC, consulte el tema sobre [Parámetros de procedimientos](https://go.microsoft.com/fwlink/?LinkId=89462), en la Referencia del programador de ODBC de MSDN Library.|  
|ADO|Si IsQueryStoreProcedure se establece en `False`, `EXEC ? = myStoredProcedure 1`<br /><br /> Si IsQueryStoreProcedure se establece en `True`, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Establecer IsQueryStoreProcedure se establece en `True`.<br /><br /> `myStoredProcedure`|  
  
 En la sintaxis mostrada en la tabla anterior, la tarea Ejecutar SQL utiliza el tipo de origen **Entrada directa** para ejecutar el procedimiento almacenado. La tarea Ejecutar SQL también puede utilizar el tipo de origen **Conexión de archivos** para ejecutar un procedimiento almacenado. Independientemente de si la tarea Ejecutar SQL utiliza el **entrada directa** o **de conexiones de archivos** tipo de origen, use un parámetro de la `ReturnValue` tipo para implementar el código de retorno. Para más información sobre cómo configurar el tipo de origen de la instrucción SQL que ejecuta la tarea Ejecutar SQL, vea [Editor de la tarea Ejecutar SQL &#40;página General&#41;](general-page-of-integration-services-designers-options.md).  
  
 Para más información sobre el uso de códigos de retorno con procedimientos almacenados de Transact-SQL, vea [RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql).  
  
##  <a name="Configure_parameters_and_return_codes"></a> Configurar parámetros y códigos de retorno en la tarea Ejecutar SQL  
 Para obtener más información acerca de las propiedades de los parámetros y códigos de devolución que puede establecer en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Ejecutar el Editor de la tarea SQL &#40;página asignación de parámetros&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de tareas o contenedores](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada de blog, [Procedimientos almacenados con parámetros de salida](https://go.microsoft.com/fwlink/?LinkId=157786)(en inglés), en blogs.msdn.com  
  
-   Ejemplo CodePlex, [Ejecutar conjuntos de resultados y parámetros de SQL](https://go.microsoft.com/fwlink/?LinkId=157863)(en inglés), en msftisprodsamples.codeplex.com  
  
## <a name="see-also"></a>Vea también  
 [Tarea Ejecutar SQL](control-flow/execute-sql-task.md)   
 [Conjuntos de resultados en la tarea Ejecutar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
