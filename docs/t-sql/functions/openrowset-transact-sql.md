---
title: OPENROWSET (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
caps.latest.revision: 130
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c23ec85299af595305a5f6d5141dbbf3ffab96d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene toda la información de conexión necesaria para tener acceso a datos remotos desde un origen de datos OLE DB. Es un método alternativo para tener acceso a las tablas de un servidor vinculado y, al mismo tiempo, es un método ad hoc para conectarse y tener acceso a datos remotos utilizando OLE DB. Para obtener referencias más frecuentes a orígenes de datos OLE DB, use, en su lugar, servidores vinculados. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md). El `OPENROWSET` función puede hacer referencia en la cláusula FROM de una consulta como si fuera un nombre de tabla. El `OPENROWSET` también se puede hacer referencia a función como la tabla de destino de un `INSERT`, `UPDATE`, o `DELETE` (instrucción), sujeto a las capacidades del proveedor OLE DB. Aunque la consulta puede devolver varios conjuntos de resultados, `OPENROWSET` devuelve solo la primera de ellas.  
  
 `OPENROWSET`También es compatible con operaciones masivas a través de un proveedor integrado BULK que permite que los datos de un archivo para ser leído y se devuelve como un conjunto de filas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENROWSET   
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'   
   | 'provider_string' }   
   , {   [ catalog. ] [ schema. ] object   
       | 'query'   
     }   
   | BULK 'data_file' ,   
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]  
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }  
} )   
  
<bulk_options> ::=  
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]  
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ , FIRSTROW = first_row ]   
   [ , LASTROW = last_row ]   
   [ , MAXERRORS = maximum_errors ]   
   [ , ROWS_PER_BATCH = rows_per_batch ]  
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]   
```

  
## <a name="arguments"></a>Argumentos  
 '*NombreProveedor*'  
 Es una cadena de caracteres que representa el nombre descriptivo (o PROGID) del proveedor OLE DB según se especifica en el Registro. *NombreProveedor* no tiene ningún valor predeterminado.  
  
 '*datasource*'  
 Es una constante de cadena que corresponde a un origen de datos OLE DB determinado. *origen de datos* es la propiedad DBPROP_INIT_DATASOURCE que se pasan a la interfaz IDBProperties del proveedor para inicializar el proveedor. Normalmente, esta cadena incluye el nombre del archivo de la base de datos, el nombre del servidor de bases de datos o un nombre comprensible para que el proveedor encuentre las bases de datos.  
  
 '*user_id*'  
 Es una constante de cadena que contiene el nombre de usuario que se pasa al proveedor OLE DB especificado. *USER_ID* especifica el contexto de seguridad para la conexión y se pasa como la propiedad DBPROP_AUTH_USERID para inicializar el proveedor. *USER_ID* no puede ser un nombre de inicio de sesión de Microsoft Windows.  
  
 '*contraseña*'  
 Es una constante de cadena que contiene la contraseña de usuario que se debe pasar al proveedor OLE DB. *contraseña* se pasa como la propiedad DBPROP_AUTH_PASSWORD cuando se inicializa el proveedor. *contraseña* no puede ser una contraseña de Microsoft Windows.  
  
 '*provider_string*'  
 Es una cadena de conexión específica del proveedor que se pasa como la propiedad DBPROP_INIT_PROVIDERSTRING para inicializar el proveedor OLE DB. *provider_string* normalmente encapsula toda la información de conexión necesaria para inicializar el proveedor. Para obtener una lista de palabras clave que son reconocidos por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB, vea [propiedades de inicialización y autorización](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 *catálogo*  
 Es el nombre del catálogo o de la base de datos donde reside el objeto especificado.  
  
 *esquema*  
 Es el nombre del esquema o propietario del objeto para el objeto especificado.  
  
 *objeto*  
 Es el nombre del objeto que identifica unívocamente el objeto con el que se va a trabajar.  
  
 '*consulta*'  
 Es una constante de cadena que se envía al proveedor, quien la ejecuta. La instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no procesa esta consulta, pero sí que procesa los resultados de la consulta devuelta por el proveedor (una consulta de paso a través). Las consultas de paso a través resultan útiles cuando se utilizan en proveedores que no muestran sus datos tabulares a través de nombres de tablas, sino solamente a través de un lenguaje de comandos. Se admiten consultas de paso a través en el servidor remoto, siempre que el proveedor de consultas admita el objeto de comando de OLE DB y sus interfaces obligatorias. Para obtener más información, vea [SQL Server Native Client &#40; OLE DB &#41; Referencia](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md).  
  
 BULK  
 Utiliza el proveedor de conjuntos de filas BULK para que OPENROWSET lea datos de un archivo. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], OPENROWSET puede leer datos de un archivo sin necesidad de cargarlos en una tabla de destino. Esto le permite utilizar OPENROWSET con una instrucción SELECT simple.  
  
 Los argumentos de la opción BULK le permiten elegir dónde empezar y acabar la lectura de datos, cómo abordar los errores y cómo interpretar los datos. Por ejemplo, puede especificar que el archivo de datos se lea como un conjunto de filas de fila única y una sola columna de tipo **varbinary**, **varchar**, o **nvarchar**. El comportamiento predeterminado se describe en las descripciones de los argumentos que se muestran a continuación.  
  
 Para obtener información acerca del uso de la opción BULK, vea la sección "Comentarios" más adelante en este tema. Para obtener información acerca de los permisos que necesita la opción BULK, vea la sección "Permisos", más adelante en este tema.  
  
> [!NOTE]  
>  Cuando se utiliza para importar datos con el modelo de recuperación completa, OPENROWSET (BULK ...) no optimiza el registro.  
  
 Para obtener información sobre cómo preparar datos para la importación masiva, vea [preparar los datos para la exportación masiva o importar &#40; SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 '*data_file*'  
 Es la ruta de acceso completa del archivo de datos cuyos datos se copian en la tabla de destino.   
 **Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, que puede ser el data_file en almacenamiento de blobs de Azure. Para obtener ejemplos, vea [ejemplos de forma masiva acceso a los datos en almacenamiento de blobs de Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
 \<bulk_options >  
 Especifica uno o más argumentos para la opción BULK.  
  
 PÁGINA DE CÓDIGOS = {'ACP' | "OEM" | "SIN PROCESAR" | *página_de_códigos*'}  
 Especifica la página de códigos de los datos incluidos en el archivo de datos. CODEPAGE solo es pertinente si los datos contienen **char**, **varchar**, o **texto** columnas con valores de caracteres mayores que 127 o menores que 32.  
  
> [!NOTE]  
>  Se recomienda especificar un nombre de intercalación para cada columna en un archivo de formato, excepto cuando quiera que la opción 65001 tenga prioridad sobre la especificación de la página de código o la intercalación.  
  
|Valor de CODEPAGE|Description|  
|--------------------|-----------------|  
|ACP|Convierte columnas de **char**, **varchar**, o **texto** tipo de datos de ANSI /[!INCLUDE[msCoName](../../includes/msconame-md.md)] página de códigos de Windows (ISO 1252) a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de códigos.|  
|OEM (valor predeterminado)|Convierte columnas de **char**, **varchar**, o **texto** tipo de datos desde la página de códigos OEM del sistema a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de códigos.|  
|RAW|Se produce ninguna conversión desde una página de códigos a otra. Ésta es la opción más rápida.|  
|*code_page*|Indica la página de códigos original en la que se codifican los datos de caracteres incluidos en el archivo de datos; por ejemplo, 850.<br /><br /> **\*\*Importante \* \***  versiones anteriores a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] no son compatibles con la página de códigos 65001 (codificación UTF-8).|  
  
 ERRORFILE ='*file_name*'  
 Especifica el archivo utilizado para recopilar filas que tienen errores de formato y no pueden convertirse en un conjunto de filas OLE DB. Estas filas se copian en este archivo de errores desde el archivo de datos "tal cual".  
  
 El archivo de errores se crea cuando se inicia la ejecución del comando. Se producirá un error si el archivo ya existe. Además, se crea un archivo de control con la extensión .ERROR.txt. Este archivo hace referencia a cada una de las filas del archivo de errores y proporciona diagnósticos de errores. Tras corregir los errores, pueden cargarse los datos.  
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], el `error_file_path` puede estar en el almacenamiento de blobs de Azure. 

'errorfile_data_source_name'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Un origen de datos externo con nombre apunta a la ubicación de almacenamiento de blobs de Azure del archivo de error que contendrá los errores encontrados durante la importación. El origen de datos externo debe crearse con el `TYPE = BLOB_STORAGE` opción se ha agregado en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP. Para obtener más información, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 FIRSTROW =*first_row*  
 Especifica el número de la primera fila que se va a cargar. El valor predeterminado es 1. Indica la primera fila del archivo de datos especificado. Los números de fila vienen determinados por el recuento de terminadores de fila. FIRSTROW está en base 1.  
  
 LASTROW =*last_row*  
 Especifica el número de la última fila que va a cargarse. El valor predeterminado es 0. Indica la última fila del archivo de datos especificado.  
  
 MAXERRORS =*maximum_errors*  
 Especifica el número máximo de errores de sintaxis o filas no compatibles, tal y como se define en el archivo de formato, que pueden tener lugar antes de que OPENROWSET produzca una excepción. Hasta que se alcance el valor de MAXERRORS, OPENROWSET omite todas las filas erróneas, sin cargarlas, y cuenta cada fila errónea como un error.  
  
 El valor predeterminado de *maximum_errors* es 10.  
  
> [!NOTE]  
>  MAX_ERRORS no se aplica a las restricciones CHECK, o para convertir **dinero** y **bigint** tipos de datos.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 Especifica el número aproximado de filas de datos del archivo de datos. Este valor debe ser del mismo tipo que el número de filas real.  
  
 OPENROWSET siempre importa un archivo de datos como un solo lote. Sin embargo, si especifica *rows_per_batch* con un valor > 0, el procesador de consultas utiliza el valor de *rows_per_batch* como una sugerencia para asignar recursos en el plan de consulta.  
  
 De forma predeterminada, el valor de ROWS_PER_BATCH es desconocido. Especificar ROWS_PER_BATCH = 0 es lo mismo que omitir ROWS_PER_BATCH.  
  
 ORDEN ({ *columna* [ASC | DESC]} [,... *n*  ] [UNIQUE])  
 Sugerencia opcional que especifica la forma en que están ordenados los datos en el archivo. De forma predeterminada, la operación masiva presupone que los datos del archivo no están ordenados. El rendimiento podría mejorar si el optimizador de consultas puede aprovechar el orden especificado para generar un plan de consulta más eficaz. A continuación se citan algunos ejemplos en los que especificar una ordenación puede ser beneficioso:  
  
-   La inserción de filas en una tabla que tiene un índice clúster, donde los datos del conjunto de filas están ordenados en la clave del índice clúster.  
  
-   La combinación del conjunto de filas con otra tabla, donde las columnas de ordenación y combinación coinciden.  
  
-   La agregación de los datos del conjunto de filas por las columnas de ordenación.  
  
-   El uso del conjunto de filas como una tabla de origen en la cláusula FROM de una consulta, donde las columnas de ordenación y combinación coinciden.  
  
 UNIQUE especifica que el archivo de datos no tiene entradas duplicadas.  
  
 Si las filas del archivo de datos no están ordenadas según el orden especificado, o si se ha especificado la sugerencia UNIQUE y hay claves duplicadas, se devuelve un error.  
  
 Se requieren alias de columna cuando se utiliza ORDER. La lista de alias de columna debe hacer referencia a la tabla derivada a la que la cláusula BULK está obteniendo acceso. Los nombres de columna que se especifican en la cláusula ORDER hacen referencia a esta lista de alias de columna. Tipos de valores grandes (**varchar (max)**, **nvarchar (max)**, **varbinary (max)**, y **xml**) y los tipos de objetos grandes (LOB) (**texto**, **ntext**, y **imagen**) no se pueden especificar columnas.  
  
 SINGLE_BLOB  
 Devuelve el contenido de *data_file* como un conjunto de filas de fila única y una sola columna de tipo **varbinary (max)**.  
  
> [!IMPORTANT]  
>  Recomendamos que importe los datos XML solo mediante la opción SINGLE_BLOB, en vez de SINGLE_CLOB y SINGLE_NCLOB, ya que solo SINGLE_BLOB admite todas las conversiones de codificación de Windows.  
  
 SINGLE_CLOB  
 Leyendo *data_file* como ASCII, se devuelve el contenido como un conjunto de filas de fila única y una sola columna de tipo **varchar (max)**, mediante la intercalación de la base de datos actual.  
  
 SINGLE_NCLOB  
 Leyendo *data_file* como UNICODE, se devuelve el contenido como un conjunto de filas de fila única y una sola columna de tipo **nvarchar (max)**, mediante la intercalación de la base de datos actual.  

### <a name="input-file-format-options"></a>Opciones de formato de archivo de entrada
  
FORMATO  **=**  'CSV'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica un archivo de valores separados por comas conforme a la [RFC 4180](https://tools.ietf.org/html/rfc4180) estándar.

 FORMATFILE ='*format_file_path*'  
 Especifica la ruta de acceso completa de un archivo de formato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite dos tipos de archivos de formato: XML y no XML.  
  
 Es necesario usar un archivo de formato para definir los tipos de columna del conjunto de resultados. La única excepción es cuando se especifica SINGLE_CLOB, SINGLE_BLOB o SINGLE_NCLOB; en este caso, no es necesario usar el archivo de formato.  
  
 Para obtener información acerca de los archivos de formato, vea [utilizar un archivo de formato para la importación masiva de datos &#40; SQL Server &#41; ](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, que puede ser el format_file_path en almacenamiento de blobs de Azure. Para obtener ejemplos, vea [ejemplos de forma masiva acceso a los datos en almacenamiento de blobs de Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

FIELDQUOTE  **=**  'field_quote'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica un carácter que se usará como el carácter de comillas en el archivo CSV. Si no se especifica, se utilizará el carácter de comillas (") como el carácter de comilla como se define en el [RFC 4180](https://tools.ietf.org/html/rfc4180) estándar.

  
## <a name="remarks"></a>Comentarios  
 `OPENROWSET`Puede utilizar para tener acceso a datos remotos de OLE DB orígenes de datos solo cuando la **DisallowAdhocAccess** opción del registro se establece explícitamente en 0 para el proveedor especificado y es el Ad Hoc Distributed Queries opción de configuración avanzada habilitado. Cuando no se establecen estas opciones, el comportamiento predeterminado no permite el acceso ad hoc.  
  
 Al tener acceso remoto a orígenes de datos OLE DB, la identidad de inicio de sesión de las conexiones de confianza no se delegan automáticamente del servidor en el que el cliente se conecta al servidor que se consulta. Debe configurarse la delegación de autenticación.  
  
 Los nombres de catálogo y esquema son necesarios si el proveedor OLE DB admite varios catálogos y esquemas en el origen de datos especificado. Los valores para *catálogo* y *esquema* pueden omitirse si no es compatible con el proveedor OLE DB. Si el proveedor admite solo los nombres de esquema, un nombre de dos partes del formulario *esquema***.** *objeto* debe especificarse. Si el proveedor admite solo los nombres de catálogo, un nombre de tres partes del formulario *catálogo***.** *esquema***.** *objeto* debe especificarse. Se deben especificar nombres de tres partes para las consultas de paso a través que use la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB. Para obtener más información, vea [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET`no acepta variables como argumentos.  
  
 Todas las llamadas a `OPENDATASOURCE`, `OPENQUERY`, o `OPENROWSET` en el `FROM` cláusula se evalúa por separado y de forma independiente de las llamadas a estas funciones se usan como el destino de la actualización, incluso si se han suministrado argumentos idénticos para las dos llamadas. En particular, las condiciones de filtro o combinación aplicadas en el resultado de una de esas llamadas no tienen ningún efecto en los resultados de la otra llamada.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>Utilizar OPENROWSET con la opción BULK  
 Las siguientes mejoras de [!INCLUDE[tsql](../../includes/tsql-md.md)] admiten la función OPENROWSET(BULK…):  
  
-   Una cláusula FROM que se utiliza con `SELECT` puede llamar a `OPENROWSET(BULK...)` en lugar de un nombre de tabla completo `SELECT` funcionalidad.  
  
     `OPENROWSET`con el `BULK` opción requiere un nombre de correlación, también conocido como una variable de intervalo o alias, en la `FROM` cláusula. Pueden especificarse alias de columna. Si no se especifica una lista de alias de columna, el archivo de formato debe incluir nombres de columna. Al especificar alias de columnas se anulan los nombres de columnas en el archivo de formato:  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    Error al agregar el `AS <table_alias>` se producirá el error:    
>    Mensaje 491, nivel 16, estado 1, línea 20    
>    Debe especificarse un nombre de correlación para el conjunto de filas masivo en la cláusula FROM.    
  
-   Un `SELECT...FROM OPENROWSET(BULK...)` instrucción consulta los datos en un archivo directamente, sin importar los datos en una tabla. `SELECT…FROM OPENROWSET(BULK...)`las instrucciones también pueden mostrar alias de columnas masivas utilizando un archivo de formato para especificar nombres de columna y también tipos de datos.  
  
-   Usar `OPENROWSET(BULK...)` como una tabla de origen en un `INSERT` o `MERGE` una importación masiva de instrucción desde un archivo de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. Para obtener más información, vea [importación masiva de datos mediante el uso de BULK INSERT u OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) .  
  
-   Cuando el `OPENROWSET BULK` opción se utiliza con un `INSERT` instrucción, la cláusula BULK admite sugerencias de tabla. Además de regular sugerencias de tabla, como `TABLOCK`, `BULK` cláusula puede aceptar las sugerencias de tablas especializadas siguientes: `IGNORE_CONSTRAINTS` (omite solo el `CHECK` y `FOREIGN KEY` restricciones), `IGNORE_TRIGGERS`, `KEEPDEFAULTS`, y `KEEPIDENTITY`. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Para obtener información sobre cómo usar `INSERT...SELECT * FROM OPENROWSET(BULK...)` , vea [importación en bloque y exportar datos &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). Para obtener más información sobre cuándo se incluyen en el registro de transacciones las operaciones de inserción de filas que se efectúan durante una importación en bloque, vea [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
> [!NOTE]  
>  Cuando usas `OPENROWSET`, es importante entender cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controla la suplantación. Para obtener información acerca de las consideraciones de seguridad, consulte [importación masiva de datos mediante el uso de BULK INSERT u OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>Importar de forma masiva datos SQLCHAR, SQLNCHAR o SQLBINARY  
 OPENROWSET(BULK...) presupone que, si no se especifica, la longitud máxima de los datos SQLCHAR, SQLNCHAR o SQLBINARY no supera los 8000 bytes. Si los datos que se va a importar están en un campo de datos LOB que incluye cualquier **varchar (max)**, **nvarchar (max)**, o **varbinary (max)** objetos que superan los 8000 bytes, debe usar un Archivo de formato XML que define la longitud máxima del campo de datos. Para especificar la longitud máxima, edite el archivo de formato y declare el atributo MAX_LENGTH.  
  
> [!NOTE]  
>  Un archivo de formato generado automáticamente no especifica la longitud o la longitud máxima de un campo LOB. Sin embargo, es posible editar un archivo de formato y especificar la longitud o la longitud máxima manualmente.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportación o importación masiva de documentos SQLXML  
 Para importar o exportar de forma masiva datos SQLXML, utilice uno de los tipos de datos siguientes en el archivo de formato.  
  
|Tipo de datos|Efecto|  
|---------------|------------|  
|SQLCHAR o SQLVARYCHAR|Los datos se envían a la página de códigos del cliente o a la página de códigos implícita por la intercalación.|  
|SQLNCHAR o SQLNVARCHAR|Los datos se envían como datos Unicode.|  
|SQLBINARY o SQLVARYBIN|Los datos se envían sin realizar ninguna conversión.|  
  
## <a name="permissions"></a>Permissions  
 `OPENROWSET`permisos están determinados por los permisos del nombre de usuario que se pasa al proveedor OLE DB. Para usar el `BULK` opción requiere `ADMINISTER BULK OPERATIONS` permiso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. Usar OPENROWSET con SELECT y el proveedor OLE DB de SQL Server Native Client  
 En el ejemplo siguiente se usa el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB para tener acceso a la `HumanResources.Department` tabla el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos en el servidor remoto `Seattle1`. (El uso de SQLNCLI y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] redirigirá a la última versión del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client). Se utiliza una instrucción `SELECT` para definir el conjunto de filas devuelto. La cadena de proveedor contiene las palabras clave `Server` y `Trusted_Connection`. Estas palabras clave son reconocidas por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB.  
  
```tsql  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>B. Usar el proveedor Microsoft OLE DB para Jet  
 En el siguiente ejemplo se obtiene acceso a la tabla `Customers` de la base de datos `Northwind` de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access a través del proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet.  
  
> [!NOTE]  
>  En este ejemplo se supone que está instalado Access. Para ejecutar este ejemplo, debe instalar la base de datos Northwind.  
  
```tsql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. Usar OPENROWSET y otra tabla en INNER JOIN  
 En el ejemplo siguiente se seleccionan todos los datos de la `Customers` tabla a partir de la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` base de datos desde y hacia el `Orders` tabla al acceso de `Northwind` base de datos almacenada en el mismo equipo.  
  
> [!NOTE]  
>  En este ejemplo se supone que está instalado Access. Para ejecutar este ejemplo, debe instalar la base de datos Northwind.  
  
```tsql  
USE Northwind  ;  
GO  
SELECT c.*, o.*  
FROM Northwind.dbo.Customers AS c   
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',   
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)      
   AS o   
   ON c.CustomerID = o.CustomerID ;  
GO  
```  
  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. Usar OPENROWSET para insertar de forma masiva datos de archivo en una columna varbinary(max)  
 En el ejemplo siguiente se crea una tabla pequeña como ejemplo y se insertan datos de archivo desde un archivo llamado `Text1.txt` ubicado en el directorio raíz `C:` en una columna `varbinary(max)`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable(FileName nvarchar(60),   
  FileType nvarchar(60), Document varbinary(max));  
GO  
  
INSERT INTO myTable(FileName, FileType, Document)   
   SELECT 'Text1.txt' AS FileName,   
      '.txt' AS FileType,   
      * FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;  
GO  
```  
  
### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. Usar el proveedor OPENROWSET BULK con un archivo de formato para recuperar filas de un archivo de texto  
 En el ejemplo siguiente se utiliza un archivo de formato para recuperar filas de un archivo de texto delimitado por tabuladores, `values.txt`, que contiene los datos siguientes:  
  
```tsql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 El archivo de formato, `values.fmt`, describe las columnas en `values.txt`:  
  
```tsql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 Ésta es la consulta que recupera los datos:  
  
```tsql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  
  
### <a name="f-specifying-a-format-file-and-code-page"></a>F. Especificar una página de códigos y el archivo de formato  
 En el ejemplo siguiente se muestra cómo utilizar tanto el archivo y el código página Opciones de formato al mismo tiempo.  
  
```tsql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. Acceso a datos desde un archivo CSV con un archivo de formato  
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
```tsql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. Acceso a datos desde un archivo CSV sin un archivo de formato

```tsql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. Acceso a datos desde un archivo almacenado en almacenamiento de blobs de Azure   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
En el ejemplo siguiente se usa un origen de datos externo que apunta a un contenedor en una cuenta de almacenamiento de Azure y una credencial de ámbito de la base de datos creadas para una firma de acceso compartido.     

```tsql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
Para completar `OPENROWSET` ejemplos, incluida la configuración de la credencial y el origen de datos externo, vea [ejemplos de forma masiva acceso a los datos en almacenamiento de blobs de Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
 
### <a name="additional-examples"></a>Otros ejemplos  
 Para obtener ejemplos adicionales que muestran el uso de `INSERT...SELECT * FROM OPENROWSET(BULK...)`, vea los temas siguientes:  
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40; Transact-SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [Funciones de conjunto de filas &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

