---
title: Cambios de última hora a la base de datos del motor de características de SQL Server 2014 | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
caps.latest.revision: 143
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 25ba18ecc13f25e3a7b438afb1a3b27b23e443f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198294"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2014"></a>Cambios recientes en las características del Motor de base de datos de SQL Server 2014
  En este tema se describen los cambios recientes en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] y versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
##  <a name="SQL14"></a> Cambios recientes en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 No hay ningún problema nuevo.  
  
##  <a name="Denali"></a> Cambios recientes en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Seleccionar en columnas o tablas denominadas NEXT|Las secuencias utilizan la función NEXT VALUE FOR del estándar ANSI. Si una tabla o una columna se denomina NEXT y la tabla o columna tiene un alias como valor, y el estándar ANSI AS se omite, la instrucción resultante puede producir un error. Para evitar el problema, incluya la palabra clave AS del estándar ANSI. Por ejemplo, `SELECT NEXT VALUE FROM Table` se debería reescribir como `SELECT NEXT AS VALUE FROM Table` y `SELECT Col1 FROM NEXT VALUE` se debería reescribir como `SELECT Col1 FROM NEXT AS VALUE`.|  
|Operador PIVOT|El operador PIVOT no está permitido en una consulta de expresión de tabla común recursiva (CTE) cuando el nivel de compatibilidad está establecido en 110. Vuelva a escribir la consulta o cambie el nivel de compatibilidad a 100 o un valor inferior. Con PIVOT en una consulta CTE se producen resultados incorrectos cuando hay varias filas individuales por agrupación.|  
|sp_setapprole y sp_unsetapprole|El parámetro `OUTPUT` de la cookie para `sp_setapprole` está documentado actualmente como `varbinary(8000)`, que es la longitud máxima correcta. Sin embargo, la implementación actual devuelve `varbinary(50)`. Las aplicaciones deben seguir reservando `varbinary(8000)` para que la aplicación siga funcionando correctamente si el tamaño de retorno de la cookie aumenta en una versión futura. Para obtener más información, vea [sp_setapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql).|  
|EXECUTE AS|El parámetro OUTPUT de la cookie para EXECUTE AS está documentado actualmente como `varbinary(8000)`, que es la longitud máxima correcta. Sin embargo, la implementación actual devuelve `varbinary(100)`. Las aplicaciones deben seguir reservando `varbinary(8000)` para que la aplicación siga funcionando correctamente si el tamaño de retorno de la cookie aumenta en una versión futura. Para obtener más información, vea [EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql).|  
|sys.fn_get_audit_file función|Dos columnas adicionales (**user_defined_event_id** y **user_defined_information**) se agregaron para admitir eventos de auditoría definido por el usuario. Las aplicaciones que no seleccionan columnas por nombre pueden devolver más columnas de las previstas. Seleccione las columnas por nombre o ajuste la aplicación para aceptar estas columnas adicionales.|  
|Palabra clave reservada WITHIN|WITHIN ahora es una palabra clave reservada. Se producirán errores en las referencias a objetos o columnas que se denominen "within". Cambie el nombre del objeto o de la columna, o bien delimite el nombre con corchetes o comillas.  Por ejemplo, `SELECT * FROM [within]`.|  
|Operaciones CAST y CONVERT en columnas calculadas de tipo `time` o `datetime2`|En versiones anteriores a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el estilo predeterminado de las operaciones CAST y CONVERT en tipos de datos `time` y `datetime2` es 121, a menos que se utilice otro tipo en una expresión de columna calculada. Para las columnas calculadas, el estilo predeterminado es 0. Este comportamiento afecta a las columnas calculadas cuando se crean, cuando se utilizan en las consultas que implican parametrización automática o cuando se usan en definiciones de restricciones.<br /><br /> Bajo el nivel de compatibilidad 110, el estilo predeterminado de las operaciones CAST y CONVERT en los tipos de datos `time` y `datetime2` es siempre 121. Si su consulta se basa en el comportamiento anterior, use un nivel de compatibilidad menor de 110, o especifique explícitamente el estilo 0 en la consulta correspondiente.<br /><br /> Actualizar la base de datos al nivel de compatibilidad 110 no cambiará los datos de usuario que se hayan almacenado en disco. Debe corregir manualmente estos datos según convenga. Por ejemplo, si utilizara SELECT INTO para crear una tabla de un origen que contuviera una expresión de columna calculada como la descrita anteriormente, se almacenarían los datos (si se usa el estilo 0) en lugar de la propia definición de columna calculada. Debería actualizar manualmente estos datos para que coincidieran con el estilo 121.|  
|ALTER TABLE|La instrucción ALTER TABLE solo permite nombres de tabla de dos partes (esquema.objeto). Especifica el nombre de una tabla con los siguientes formatos ahora produce un error en tiempo de compilación con el error 117:<br /><br /> servidor.baseDeDatos.esquema.tabla<br /><br /> .baseDeDatos.esquema.tabla<br /><br /> ..esquema.tabla<br /><br /> En versiones anteriores, al especificar el formato servidor.baseDeDatos.esquema.tabla se devolvía el error 4902. La especificación del formato .baseDeDatos.esquema.tabla o ..esquema.tabla se realizaba correctamente. Para resolver el problema, quite el uso de un prefijo de 4 partes.|  
|Examinar los metadatos|Al consultar una vista con FOR BROWSE o SET NO_BROWSETABLE ON, ahora se devuelven los metadatos de la vista, no los metadatos del objeto subyacente. Este comportamiento ahora se corresponde al de otros métodos de examinar los metadatos.|  
|SOUNDEX|Bajo el nivel 110 de la compatibilidad de la base de datos, la función SOUNDEX implementa las nuevas reglas que pueden causar que los valores computados por la función sean diferentes que los valores computados bajo niveles anteriores de compatibilidad. Después de actualizar al nivel de compatibilidad 110, es posible que tenga que regenerar los índices, los montones o las restricciones CHECK que usan la función SOUNDEX. Para más información, vea [SOUNDEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/soundex-transact-sql).
 .|  
|Mensaje de recuento de filas para las instrucciones DML con error|En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], [!INCLUDE[ssDE](../includes/ssde-md.md)] devolverá continuamente el token TDS DONE con RowCount: 0 a los clientes cuando se produzca un error en la instrucción DML. En versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se enviaba un valor incorrecto de -1 al cliente cuando la instrucción DML con error se encontraba en un bloque TRY-CATCH y tenía parámetros automáticos con [!INCLUDE[ssDE](../includes/ssde-md.md)] o el bloque TRY-CATCH no estaba en el mismo nivel que la instrucción con el error. Por ejemplo, si un bloque de TRY-CATCH llama a un procedimiento almacenado y se produce un error en una instrucción DML del procedimiento, el cliente recibirá incorrectamente un valor de -1.<br /><br /> Se producirán errores en las aplicaciones que se basen en este comportamiento incorrecto.|  
|SERVERPROPERTY (‘Edition’)|Edición de producto instalada de la instancia de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Utilice el valor de esta propiedad para determinar las características y los límites, como por ejemplo el número máximo de CPU admitidas por el producto instalado.<br /><br /> En función de la edición Enterprise instalada, puede devolver ‘Enterprise Edition’ o ‘Enterprise Edition: licencia basada en núcleo’. Las ediciones Enterprise se diferencian en la capacidad de proceso máxima de una sola instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información sobre los límites de capacidad de cálculo en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], consulte [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).|  
|CREATE LOGIN|El `CREATE LOGIN WITH PASSWORD = '` *contraseña* `' HASHED` opción no se puede utilizar con valores hash creados con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7 o anterior.|  
|Operaciones CAST y CONVERT para `datetimeoffset`|Los únicos estilos que se admiten al convertir de tipos de fecha y hora a `datetimeoffset` son 0 o 1. Todos los demás estilos de conversión devuelven el error 9809. Por ejemplo, el código siguiente genera un error 9809.<br /><br /> `SELECT CONVERT(date, CAST('7070-11-25 16:25:01.00986 -02:07' as datetimeoffset(5)), 107);`|  
  
### <a name="dynamic-management-views"></a>Vistas de administración dinámica  
  
|Ver|Descripción|  
|----------|-----------------|  
|sys.dm_exec_requests|La columna de comandos cambia de `nvarchar(16)` a `nvarchar(32)`.|  
|Sys.dm_os_memory_cache_counters|Se ha cambiado el nombre de las columnas siguientes:<br /><br /> single_pages_kb es ahora: <br />                          pages_kb<br /><br /> multi_pages_kb<br />                           Ahora es: pages_in_use_kb|  
|Sys.dm_os_memory_cache_entries|La columna pages_allocated_count columna ha sido pages_kb cuyo nombre ha cambiado.|  
|Sys.dm_os_memory_clerks|Se ha quitado la columna multi_pages_kb.<br /><br /> La columna single_pages_kb columna ha sido pages_kb cuyo nombre ha cambiado.|  
|sys.dm_os_memory_nodes|Se ha cambiado el nombre de las columnas siguientes:<br /><br /> single_pages_kb es ahora: <br />                            pages_kb<br /><br /> multi_pages_kb es ahora: <br />                            foreign_committed_kb|  
|Sys.dm_os_memory_objects|Se ha cambiado el nombre de las siguientes columnas.<br /><br /> pages_allocated_count es ahora:<br />                            pages_in_bytes<br /><br /> max_pages_allocated_count es ahora: max_pages_in_bytes|  
|sys.dm_os_sys_info|Se ha cambiado el nombre de las columnas siguientes:<br /><br /> physical_memory_in_bytes es ahora: <br />                            physical_memory_kb<br /><br /> valor de bpool_commit_target es ahora: <br />                            committed_target_kb<br /><br /> bpool_visible es ahora: <br />                            visible_target_kb<br /><br /> virtual_memory_in_bytes es ahora: <br />                            virtual_memory_kb<br /><br /> bpool_commited es ahora:<br />                            committed_kb|  
|Sys.dm_os_workers|La columna regional se ha quitado.|  
  
### <a name="catalog-views"></a>Vistas de catálogo  
  
|Ver|Descripción|  
|----------|-----------------|  
|sys.data_spaces<br /><br /> sys.partition_schemes<br /><br /> sys.filegroups<br /><br /> sys.partition_functions|Se ha agregado la nueva columna is_system a sys.data_spaces y sys.partition_functions. (sys.partition_schemes y sys.filegroups heredan las columnas de sys.data_spaces.)<br /><br /> Un valor de 1 en esta columna indica que el objeto se usa para fragmentos de índice de texto completo.<br /><br /> En sys.partition_functions, sys.partition_schemes y sys.filegroups, la nueva columna no es la última. Revise las consultas existentes que se basan en el orden de las columnas devueltas desde estas vistas de catálogo.|  
  
### <a name="sql-clr-data-types-geometry-geography-and-hierarchyid"></a>Tipos de datos CLR de SQL (geometry, geography y hierarchyid)  
 El ensamblado **Microsoft.SqlServer.Types.dll**, que contiene los tipos de datos espaciales y el tipo hierarchyid, se ha actualizado de la versión 10.0 a la versión 11.0. Cuando se cumplan las siguientes condiciones, se puede producir un error en las aplicaciones personalizadas que hacen referencia a este ensamblado.  
  
-   Al mover una aplicación personalizada de un equipo en el que [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] se instala en un equipo en el que solo [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] está instalado, la aplicación se producirá un error porque la versión 10.0 que se hace referencia de la **SqlTypes** ensamblado no está presente. Puede aparecer este mensaje de error: `“Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified.”`  
  
-   Cuando se hace referencia el **SqlTypes** versión 11.0 del ensamblado y también está instalada la versión 10.0, puede aparecer este mensaje de error: `“System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'.”`  
  
-   Cuando se hace referencia el **SqlTypes** versión 11.0 del ensamblado desde una aplicación personalizada que tenga como destino .NET 3.5, 4 o 4.5, la aplicación producirá un error porque SqlClient, por diseño carga la versión 10.0 del ensamblado. Este error se produce cuando la aplicación llama a uno de los siguientes métodos:  
  
    -   método `GetValue` de la clase `SqlDataReader`  
  
    -   método `GetValues` de la clase `SqlDataReader`  
  
    -   operador de índice de corchete [] de la clase `SqlDataReader`  
  
    -   método `ExecuteScalar` de la clase `SqlCommand`  
  
 Puede solucionar este problema si usa uno de los métodos siguientes:  
  
-   Puede solucionar este problema en el código si llama al método `GetSqlBytes`, en lugar de los métodos Get enumerados anteriormente, para recuperar los tipos de sistema [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de CLR, tal como se muestra en el siguiente ejemplo:  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   Puede solucionar este problema mediante el redireccionamiento de ensamblado en el archivo de configuración de la aplicación, tal como se muestra en el siguiente ejemplo:  
  
    ```xml  
    <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    <runtime>  
    ```  
  
-   Puede solucionar esta problema en la cadena de conexión si especifica el valor "SQL Server 2012" para el atributo "Type System Version" para forzar que SqlClient cargue la versión 11.0 del ensamblado. Este atributo de cadena de conexión solo está disponible en .NET 4.5 y posterior.  
  
-   La etiqueta `assemblyBinding` debe ajustarse debajo de la etiqueta `runtime`.  
  
### <a name="support-for-awe"></a>Compatibilidad con AWE  
 Ya no se incluye la compatibilidad con las extensiones de ventana de dirección (AWE) de 32 bits. Esto puede dar lugar a un rendimiento más lento en sistemas operativos de 32 bits. En el caso de instalaciones que usen grandes cantidades de memoria, migre a un sistema operativo de 64 bits.  
  
### <a name="xquery-functions-are-surrogate-aware"></a>Las funciones XQuery detectan los caracteres suplentes  
 La recomendación de W3C para las funciones y los operadores de XQuery requiere contar un par suplente que represente un carácter Unicode de nivel alto como un solo glifo en codificación UTF-16. No obstante, en versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], las funciones de cadena no reconocían los pares suplentes como un solo carácter. Algunas operaciones de cadena, como los cálculos de longitud de cadena y las extracciones de subcadenas, devolvían resultados incorrectos. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ahora admite UTF-16 por completo y la administración correcta de los pares suplentes.  
  
 El tipo de datos XML de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] solo permite los pares suplentes con formato correcto. No obstante, es posible que algunas funciones sigan devolviendo resultados indefinidos o inesperados en determinadas circunstancias, ya que es posible pasar pares suplentes no válidos o parciales a las funciones XQuery como valores de cadena. Tenga en cuenta los siguientes métodos para generar valores de cadena al usar XQuery en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Proporcionar un valor de cadena constante como valor binario. Al usar este método, sigue siendo posible pasar pares suplentes no válidos o parciales.  
  
-   Proporcionar un valor de cadena constante al proporcionar entidades de caracteres. Al usar este método, no es posible pasar pares suplentes no válidos. Las funciones XQuery requieren una sola entidad de caracteres para el carácter de alto nivel. Estas funciones producen un error si se proporcionan las entidades de caracteres para los caracteres de pares suplentes.  
  
-   Importar valores externos mediante **SQL: column** o **SQL: variable**. Al usar estos métodos, sigue siendo posible incorporar pares suplentes no válidos o parciales.  
  
#### <a name="affected-xquery-functions-and-operators"></a>Funciones y operadores de XQuery afectados  
 Las funciones y los operadores de XQuery siguientes ahora administran los pares suplentes UTF-16 correctamente en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]:  
  
-   **fn: longitud**. Sin embargo, si se pasa un par suplente no válido o parcial como argumento, el comportamiento de **longitud de la cadena** no está definido.  
  
-   **fn:substring**.  
  
-   **fn: contiene**. Sin embargo, si se pasa un par suplente parcial como un valor, **contiene** puede devolver resultados inesperados, ya que puede encontrar el par suplente parcial incluido en el par suplente con formato correcto.  
  
-   **fn:concat**. Sin embargo, si se pasa un par suplente parcial como un valor, **concat** puede producir pares suplentes incorrectos o parciales.  
  
-   Operadores de comparación y el **se ordena por** cláusula. Operadores de comparación son +, \<, >, \<=, > =, `eq`, `lt`, `gt`, `le`, y `ge`.  
  
#### <a name="distributed-query-calls-to-a-system-procedure"></a>Llamadas de consulta distribuida a un procedimiento de sistema  
 Las llamadas de consulta distribuida a través de `OPENQUERY` a algunos procedimientos del sistema generarán un error cuando se llama desde un servidor de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] a otro. Esto sucede cuando [!INCLUDE[ssDE](../includes/ssde-md.md)] no puede detectar metadatos para un procedimiento. Por ejemplo, `SELECT * FROM OPENQUERY(..., 'EXEC xp_loginfo')`.  
  
#### <a name="isolation-level-and-spresetconnection"></a>Nivel de aislamiento y sp_reset_connection  
 El nivel de aislamiento para las conexiones se gestiona por controladores de clientes de la siguiente manera:  
  
-   Todos los controladores nativos (SNAC, MDAC y ODBC) establecen el nivel de aislamiento (según la configuración de la aplicación) basándose en sp_reset_connection.  
  
-   Para ADO.NET, básicamente obtendrá un nivel de aislamiento aleatorio que dependerá de la conexión que se obtiene del grupo (y si la aplicación usa un nivel de aislamiento diferente). Puesto que el grupo ADO.NET puede reciclar conexiones de manera interna y transparente, usted no puede predecir qué lanzará el grupo.  
  
-   Para el controlador JDBC, obtiene el mismo comportamiento que ADO.NET  
  
     La aplicación siempre debe establecer de forma explícita el nivel de aislamiento después de abrir la conexión para obtener lo que quiere.  
  
     Se puede agrupar la conexión JDBC, por lo que la aplicación puede obtener un nivel de aislamiento aleatorio y no saberlo.  
  
 Para conservar la compatibilidad con versiones anteriores, este nuevo comportamiento solo se aplica a clientes recientes a partir de TDS 7.4.  
  
#### <a name="backward-compatibility"></a>Backward Compatibility  
 **Nuevo comportamiento depende del nivel de compatibilidad**  
  
 Las funciones y los operadores siguientes demuestran el nuevo comportamiento descrito anteriormente solo cuando el nivel de compatibilidad es 110 o superior:  
  
-   **fn: contiene**.  
  
-   **fn:concat**.  
  
-   operadores de comparación y **se ordena por** cláusula  
  
 **Nuevo comportamiento depende del espacio de nombres predeterminado URI para las funciones**  
  
 Las siguientes funciones demuestran el nuevo comportamiento descrito anteriormente solo cuando el URI del espacio de nombres predeterminado corresponde al espacio de nombres en la recomendación final, es decir, [ http://www.w3.org/2005/xpath-functions ](http://www.w3.org/2005/xpath-functions). Cuando el nivel de compatibilidad es 110 o superior, de forma predeterminada, [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] enlaza el espacio de nombres de función predeterminado a este espacio de nombres. No obstante, estas funciones demuestran el nuevo comportamiento cuando se usa este espacio de nombres independientemente del nivel de compatibilidad.  
  
-   **fn-longitud**  
  
-   **fn:substring**  
  
##  <a name="KJKatmai"></a> Cambios importantes en SQL Server 2008 y SQL Server 2008 R2  
 Esta sección contiene los principales cambios presentados en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. En [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] no se presentó ningún cambio.  
  
### <a name="collations"></a>Intercalaciones  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Nuevas intercalaciones|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] presenta nuevas intercalaciones que se ajustan totalmente con las que proporciona Windows Server 2008. Estas 80 nuevas intercalaciones han mejorado la precisión lingüística, y para distinguirlas se ha usado *_100 en el nombre de la versión. Si elige una nueva intercalación para el servidor o la base de datos, tenga presente que es posible que los clientes que dispongan de controladores de clientes antiguos no la reconozcan. Las intercalaciones no reconocidas pueden provocar errores en la aplicación. Considere las soluciones siguientes:<br /><br /> Actualice el sistema operativo del cliente para que se actualicen las intercalaciones del sistema subyacentes.<br /><br /> Si el cliente tiene instalado software de cliente de base de datos, plantéese la posibilidad de aplicar una actualización de servicio a dicho software.<br /><br /> Elija una intercalación existente que se corresponda con una página de códigos del cliente.|  
  
### <a name="common-language-runtime-clr"></a>Common Language Runtime (CLR)  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Ensamblados CLR|Cuando se actualiza una base de datos a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], automáticamente se instala el ensamblado `Microsoft.SqlServer.Types` para admitir los nuevos tipos de datos. Las reglas del Asesor de actualizaciones detectan los tipos de usuarios o los ensamblados con nombres problemáticos. El Asesor de actualizaciones aconsejará el cambio de nombre de los ensamblados problemáticos, y en cuanto a los tipos problemáticos, aconsejará el cambio de nombre o el uso de nombres que consten de dos partes en el código para hacer referencia al tipo de usuario existente.<br /><br /> Si una actualización de la base de datos detecta un ensamblado del usuario con un nombre problemático, automáticamente cambiará el nombre de dicho ensamblado y colocará la base de datos en modo de sospecha.<br /><br /> Si durante la actualización se encuentra un tipo de usuario con un nombre problemático, no se llevará a cabo ningún procedimiento especial. Después de la actualización, existirán tanto el tipo de usuario anterior como el nuevo tipo de sistema. El tipo de usuario solo estará disponible a través de nombres de dos partes.|  
|Ensamblados CLR|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] instala .NET Framework 3.5 SP1, que se encarga de actualizar las bibliotecas de la memoria caché de ensamblados global (GAC). Si tiene bibliotecas no admitidas registradas en una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], es posible que la aplicación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deje de funcionar después de realizar la actualización a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. El motivo es que cuando se da servicio o se actualizan bibliotecas de la GAC, no se actualizan los ensamblados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si un ensamblado existe en una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y en la GAC, las dos copias del ensamblado deben coincidir exactamente. Si no coinciden, se producirá un error cuando la integración CLR de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] use el ensamblado. Para obtener más información, consulte [bibliotecas de .NET Framework admite](../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).<br /><br /> Después de actualizar la base de datos, dé servicio o actualice la copia del ensamblado situada en las bases de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la instrucción ALTER ASSEMBLY. Para obtener más información, consulte [el artículo de Knowledge Base 949080](http://go.microsoft.com/fwlink/?LinkId=154563).<br /><br /> Para saber si está usando una biblioteca de .NET Framework no admitida en la aplicación, ejecute la consulta siguiente en la base de datos.<br /><br /> `SELECT name FROM sys.assemblies WHERE clr_name LIKE '%publickeytoken=b03f5f7f11d50a3a,%';`|  
|Rutinas de CLR|El uso de la suplantación en las funciones CLR definidas por el usuario, los agregados definidos por el usuario o los tipos definidos por el usuario (UDT) puede provocar el error 6522 en la aplicación después de la actualización a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. La actualización se realiza correctamente en los escenarios de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] siguientes, pero no así en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Se proporcionan soluciones para cada escenario.<br /><br /> Una función definida por el usuario CLR, el agregado definido por el usuario o el método UDT que utiliza la suplantación tiene un parámetro de tipo `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, `ntext`, `text`, `image`, o un tipo UDT grande y no tiene el  **DataAccessKind.Read** atributo en el método. Para resolver este problema, agregue el **DataAccessKind.Read** del atributo en el método, vuelva a compilar el ensamblado y volver a implementar la rutina y el ensamblado.<br /><br /> Una función con valores de tabla CLR que tiene una **Init** método que realiza la suplantación. Para resolver este problema, agregue el **DataAccessKind.Read** del atributo en el método, vuelva a compilar el ensamblado y volver a implementar la rutina y el ensamblado.<br /><br /> Una función con valores de tabla CLR que tiene un **FillRow** método que realiza la suplantación. Para resolver este problema, quite la suplantación de la **FillRow** método. No tener acceso a recursos externos mediante el **FillRow** método. En su lugar, tener acceso a recursos externos desde el **Init** método.|  
  
### <a name="dynamic-management-views"></a>Vistas de administración dinámica  
  
|Ver|Descripción|  
|----------|-----------------|  
|sys.dm_os_sys_info|Se quitan las columnas sqlserver_start_time_cpu_ticks y cpu_ticks_in_ms.|  
|Sys.dm_exec_query_resource_semaphoressys.dm_exec_query_memory_grants|La columna resource_semaphore_id no es un identificador único en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Este cambio puede afectar a la solución de problemas de ejecución de consultas. Para obtener más información, consulte [sys.dm_exec_query_resource_semaphores &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
  
### <a name="errors-and-events"></a>Errores y eventos  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Errores de inicio de sesión|En [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], se devuelve el error 18452 cuando se usa un inicio de sesión de SQL para conectar con un servidor que está configurado para usar únicamente la autenticación de Windows. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], se devuelve el error 18456 en su lugar.|  
  
### <a name="showplan"></a>Plan de presentación  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Esquema XML del plan de presentación|Un nuevo **SeekPredicateNew** elemento se agrega el esquema de Showplan XML y la secuencia de xsd envolvente (**SqlPredicatesType**) se convierte en una  **\<xsd: choice >** elemento. En lugar de uno o varios **SeekPredicate** elementos, uno o varios **SeekPredicateNew** elementos pueden aparecer ahora en Showplan XML. Estos dos elementos se excluyen mutuamente. **SeekPredicate** se mantiene en el esquema de Showplan XML para hacia atrás compatibilidad; sin embargo, planes de consulta creados en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] puede contener el **SeekPredicateNew** elemento. Las aplicaciones que esperan para recuperar solo el **SeekPredicate** secundarios del nodo ShowPlanXML/BatchSequence/lote/instrucciones/StmtSimple/QueryPlan/RelOp/IndexScan/seekpredicates se pueden producir un error si el  **SeekPredicate** el elemento no existe. Vuelva a escribir la aplicación para que espere el **SeekPredicate** o **SeekPredicateNew** elemento de este nodo. Para obtener más información, consulte el elemento .|  
|Esquema XML del plan de presentación|Un nuevo **IndexKind** atributo se agrega a la **ObjectType** tipo complejo en el esquema de Showplan XML. En las aplicaciones que validen de forma estricta los planes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el esquema de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] se producirá un error.|  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Evento ALTER_AUTHORIZATION_DATABASE DDL|En [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], cuando se desencadena el evento ALTER_AUTHORIZATION_DATABASE de DDL, el valor 'object' se devuelve en el **ObjectType** elemento del xml EVENTDATA para este evento cuando la entidad de tipo de elemento protegible en la definición de datos operación de DDL (lenguaje) es un objeto. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], se devuelve el tipo real (por ejemplo, 'table' o 'function').|  
|CONVERT|Si se pasa un estilo no válido a la función CONVERT, se devuelve un error cuando el tipo de conversión es de binario a carácter o de carácter a binario. En las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se establece un estilo no válido como estilo predeterminado para las conversiones de binario a carácter y de carácter a binario.|  
|GRANT/DENY/REVOKE EXECUTE en ensamblados|No se puede conceder, denegar ni revocar el permiso EXECUTE a los ensamblados. Este permiso no tiene ningún efecto y ahora produce un error. En su lugar, conceda, deniegue o revoque el permiso EXECUTE para los procedimientos almacenados o para las funciones que hacen referencia al método de ensamblado.|  
|Permisos GRANT/DENY/REVOKE para los tipos del sistema|No se pueden conceder, denegar ni revocar permisos a los tipos del sistema. En versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], estas instrucciones se ejecutaban correctamente, pero no tenían ningún efecto. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], se devuelve un error.|  
|GROUP BY|La cláusula GROUP BY no puede contener ninguna subconsulta en una expresión usada para la lista de agrupación. En las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se permitía. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], se devuelve el error 144.<br /><br /> Por ejemplo, el código siguiente se ejecutará correctamente en SQL Server 2005 y producirá un error en SQL Server 2008.<br /><br /> `DECLARE @Test TABLE(a int NOT NULL);` <br /> `INSERT INTO @Test SELECT 1 union ALL SELECT 2;` <br /> `SELECT COUNT(*)` <br /> `FROM @Test` <br /> `GROUP BY CASE WHEN a IN (SELECT t.a FROM @Test AS t)` <br /> `THEN 1 ELSE 0` <br /> `END;`|  
|Cláusula OUTPUT|Para evitar un comportamiento no determinista, la cláusula OUTPUT no puede hacer referencia a una columna desde una vista o una función insertada con valores de tabla si dicha tabla se ha definido mediante uno de los métodos siguientes:<br /><br /> Una subconsulta.<br /><br /> Una función definida por el usuario que obtiene acceso a datos de usuario o del sistema, o que se asume que obtiene dicho acceso.<br /><br /> Una columna calculada que contiene en su definición una función definida por el usuario que obtiene acceso a datos de usuario o del sistema.<br /><br /> <br /><br /> Cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] detecta este tipo de columna en la cláusula OUTPUT, se produce el error 4186. Para obtener más información, consulte [MSSQLSERVER_4186](../relational-databases/errors-events/mssqlserver-4186-database-engine-error.md).|  
|Cláusula OUTPUT INTO|La tabla de destino de la cláusula OUTPUT INTO no puede tener desencadenadores habilitados.|  
|Opción precompute rank de nivel de servidor|Esta opción no se admite en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Modifique las aplicaciones que actualmente utilizan esta característica lo antes posible.|  
|READPAST, sugerencia de tabla|No puede especificar la sugerencia de READPAST con aislamiento de instantáneas.<br /><br /> La sugerencia de READPAST se omite cuando se activa la opción de base de datos READ_COMMITED_SNAPSHOT o ALLOW_SNAPSHOT_ISOLATION. Sin embargo, si combina la sugerencia de READPAST con READCOMMITTEDLOCK, el comportamiento de READPAST será igual que con la sugerencia de READCOMMITTED de bloqueo.|  
|sp_helpuser|Los siguientes nombres de columna que se devuelven en el conjunto de resultados del procedimiento almacenado sp_helpuser han cambiado:<br /><br /> GroupName es ahora:<br />                            RoleName<br /><br /> Nombre_grupo es ahora:<br />                            Role_name<br /><br /> Group_id es ahora:<br />                            Role_id<br /><br /> Users_in_group es ahora:<br />                            Users_in_role|  
|Cifrado de datos transparente|El cifrado de datos transparente (TDE) se realiza en el nivel de E/S: la estructura de la página está sin cifrar en la memoria y solo se cifra cuando la página se escribe en el disco. Se cifran tanto los archivos de base de datos como los archivos de registro. En las aplicaciones de terceros que omitan el mecanismo habitual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para tener acceso a las páginas (por ejemplo, examinando los datos o los archivos de registro directamente), se producirá un error si una base de datos emplea TDE debido a que los datos están cifrados en los archivos. Estas aplicaciones pueden aprovechar la API criptográfica de Windows para desarrollar una solución que permita descifrar los datos desde fuera de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
### <a name="xquery"></a>XQuery  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Compatibilidad con la fecha y la hora|En [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], los tipos de datos `xs:time`, `xs:date`, y `xs:dateTime` no tiene compatibilidad de zona horaria. Los datos de la zona horaria se asignan a la zona horaria UTC. [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] tiene el comportamiento de compatibilidad estándar, lo que se traduce en los cambios siguientes:<br /><br /> Se validan los valores sin zona horaria.<br /><br /> Se conserva la zona horaria proporcionada o la ausencia de zona horaria.<br /><br /> Se modifica la representación del almacenamiento interno.<br /><br /> Se aumenta la resolución de los valores almacenados.<br /><br /> No se permiten los años negativos.<br /><br /> <br /><br /> Nota: Modificar las aplicaciones y las expresiones XQuery para tener en cuenta para los nuevos valores de tipo.|  
|Expresiones de XQuery y XPath|En [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], los pasos de una expresión XQuery o XPath que comienzan por un signo de dos puntos (': ') se permiten. Por ejemplo, la instrucción siguiente contiene una prueba del nombre (`CTR02)` dentro de la expresión de ruta de acceso que comienza con dos puntos.<br /><br /> `SELECT FileContext.query('for n$ in //CTR return <C>{data )(n$/:CTR02)} </C>) AS Files FROM dbo.MyTable;`<br /><br /> En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], este uso se rechaza porque no cumple los estándares de XML. Se devuelve el error 9341. Quite el signo de dos puntos inicial o especifique un prefijo para la prueba del nombre, por ejemplo (n$/p1:CTR02) o (n$/CTR02).|  
  
### <a name="connecting"></a>Connecting  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Conectarse desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client mediante SSL|Al conectarse con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client, las aplicaciones que usan "SERVER=shortname; FORCE ENCRYPTION=true" con un certificado cuyos asuntos especifiquen nombres de dominio completos (FQDN) se han conectado antes debido a una validación poco minuciosa. SQL Server 2008 R2 mejora la seguridad aplicando asuntos de FQDN a los certificados. Las aplicaciones que se basan en una validación poco minuciosa deben tomar una de las siguientes acciones:<br /><br /> Usar el FQDN en la cadena de conexión.<br /><br /> : Esta opción no requiere volver a compilar la aplicación si la palabra clave SERVER de la cadena de conexión se configura fuera de la aplicación.<br /><br /> : Esta opción no funciona para las aplicaciones que tienen codificadas sus cadenas de conexión.<br /><br /> : Esta opción no funciona para las aplicaciones que utilizan la creación de reflejo de base de datos desde el servidor reflejado responde con un nombre simple.|  
||Agregue un alias para asignar shortname al FQDN.<br /><br /> -Esta opción funciona incluso para las aplicaciones que tienen codificadas sus cadenas de conexión.<br /><br /> : Esta opción no funciona para las aplicaciones que utilizan la creación de reflejo de base de datos ya que los proveedores no buscan los alias para nombres de asociado de conmutación por error recibidos.|  
||Haga que se emita un certificado para shortname.<br /><br /> -Esta opción funciona para todas las aplicaciones.|  
  
##  <a name="Yukon"></a> Cambios importantes en SQL Server 2005  
 Para obtener una lista de los principales cambios introducidos en [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], consulte [cambios recientes en las características del motor de base de datos en SQL Server 2005](http://msdn.microsoft.com/library/ms143179\(SQL.90\).aspx).  
  
## <a name="see-also"></a>Vea también  
 [Características del motor de base de datos en desuso en SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md)   
 [Cambios de comportamiento en las características del motor de base de datos en SQL Server 2014](../../2014/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](sql-server-database-engine-backward-compatibility.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
