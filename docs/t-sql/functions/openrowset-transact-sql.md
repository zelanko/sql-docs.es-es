---
title: OPENROWSET (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 26b3b72cf4e3ece0624eb33032e34713695c081c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Contiene toda la información de conexión necesaria para tener acceso a datos remotos desde un origen de datos OLE DB. Es un método alternativo para tener acceso a las tablas de un servidor vinculado y, al mismo tiempo, es un método ad hoc para conectarse y tener acceso a datos remotos utilizando OLE DB. Para obtener referencias más frecuentes a orígenes de datos OLE DB, use, en su lugar, servidores vinculados. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md). Se puede hacer referencia a la función `OPENROWSET` en la cláusula FROM de una consulta como si fuera un nombre de tabla. También se puede hacer referencia a la función `OPENROWSET` como la tabla de destino de una instrucción `INSERT`, `UPDATE` o `DELETE`, según cuál sea la funcionalidad del proveedor OLE DB. Aunque la consulta puede devolver varios conjuntos de resultados, `OPENROWSET` solo devuelve el primero.  
  
 `OPENROWSET` también admite operaciones masivas a través de un proveedor integrado BULK que permite que los datos se lean y se devuelvan como un conjunto de filas.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

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
 '*provider_name*'  
 Es una cadena de caracteres que representa el nombre descriptivo (o PROGID) del proveedor OLE DB según se especifica en el Registro. *provider_name* no tiene valor predeterminado.  
  
 '*datasource*'  
 Es una constante de cadena que corresponde a un origen de datos OLE DB determinado. *datasource* es la propiedad DBPROP_INIT_DATASOURCE que se pasará a la interfaz IDBProperties del proveedor para inicializarlo. Normalmente, esta cadena incluye el nombre del archivo de la base de datos, el nombre del servidor de bases de datos o un nombre comprensible para que el proveedor encuentre las bases de datos.  
  
 '*user_id*'  
 Es una constante de cadena que contiene el nombre de usuario que se pasa al proveedor OLE DB especificado. *user_id* indica el contexto de seguridad para la conexión y se pasa como la propiedad DBPROP_AUTH_USERID para inicializar el proveedor. *user_id* no puede ser un nombre de inicio de sesión de Microsoft Windows.  
  
 '*password*'  
 Es una constante de cadena que contiene la contraseña de usuario que se debe pasar al proveedor OLE DB. *password* se pasa como la propiedad DBPROP_AUTH_PASSWORD cuando el proveedor se inicializa. *password* no puede ser una contraseña de Microsoft Windows.  
  
 '*provider_string*'  
 Es una cadena de conexión específica del proveedor que se pasa como la propiedad DBPROP_INIT_PROVIDERSTRING para inicializar el proveedor OLE DB. Normalmente, *provider_string* encapsula toda la información de conexión necesaria para inicializar el proveedor. Para obtener una lista de palabras clave que el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pueda reconocer, vea [Initialization and Authorization Properties](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md) (Propiedades de inicialización y autorización).  
  
 *catalog*  
 Es el nombre del catálogo o de la base de datos donde reside el objeto especificado.  
  
 *schema*  
 Es el nombre del esquema o propietario del objeto para el objeto especificado.  
  
 *object*  
 Es el nombre del objeto que identifica unívocamente el objeto con el que se va a trabajar.  
  
 '*query*'  
 Es una constante de cadena que se envía al proveedor, quien la ejecuta. La instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no procesa esta consulta, pero sí que procesa los resultados de la consulta devuelta por el proveedor (una consulta de paso a través). Las consultas de paso a través resultan útiles cuando se utilizan en proveedores que no muestran sus datos tabulares a través de nombres de tablas, sino solamente a través de un lenguaje de comandos. El servidor remoto admite las consultas de paso a través siempre y cuando el proveedor de consultas admita el objeto Command de OLE DB y sus interfaces obligatorias. Para más información, vea [Referencia de SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md).  
  
 BULK  
 Utiliza el proveedor de conjuntos de filas BULK para que OPENROWSET lea datos de un archivo. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], OPENROWSET puede leer datos de un archivo sin necesidad de cargarlos en una tabla de destino. Esto le permite utilizar OPENROWSET con una instrucción SELECT simple.  
  
 Los argumentos de la opción BULK le permiten elegir dónde empezar y acabar la lectura de datos, cómo abordar los errores y cómo interpretar los datos. Por ejemplo, puede especificar que el archivo de datos se lea como un conjunto de filas de una sola fila y una sola columna de tipo **varbinary**, **varchar** o **nvarchar**. El comportamiento predeterminado se describe en las descripciones de los argumentos que se muestran a continuación.  
  
 Para obtener información acerca del uso de la opción BULK, vea la sección "Comentarios" más adelante en este tema. Para obtener información acerca de los permisos que necesita la opción BULK, vea la sección "Permisos", más adelante en este tema.  
  
> [!NOTE]  
>  Cuando se utiliza para importar datos con el modelo de recuperación completa, OPENROWSET (BULK ...) no optimiza el registro.  
  
 Para más información sobre cómo preparar datos para importaciones masivas, vea [Preparar los datos para exportar o importar de forma masiva &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 '*data_file*'  
 Es la ruta de acceso completa del archivo de datos cuyos datos se copian en la tabla de destino.   
 **Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, data_file puede estar en Azure Blob Storage. Para ver ejemplos, vea [Ejemplos de acceso masivo a datos en Azure Blob Storage](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
 \<bulk_options>  
 Especifica uno o más argumentos para la opción BULK.  
  
 CODEPAGE = { 'ACP'| 'OEM'| 'RAW'| '*code_page*' }  
 Especifica la página de códigos de los datos incluidos en el archivo de datos. CODEPAGE solo es pertinente si los datos contienen columnas de tipo **char**, **varchar** o **text** con valores de caracteres mayores que 127 o menores que 32.  

> [!IMPORTANT]
> CODEPAGE no es una opción admitida en Linux.

> [!NOTE]  
>  Se recomienda especificar un nombre de intercalación para cada columna en un archivo de formato, excepto cuando quiera que la opción 65001 tenga prioridad sobre la especificación de la página de códigos o la intercalación.  
  
|Valor de CODEPAGE|Description|  
|--------------------|-----------------|  
|ACP|Convierte columnas de los tipos de datos **char**, **varchar** o **text** de la página de códigos ANSI/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (ISO 1252) a la página de códigos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|OEM (valor predeterminado)|Convierte columnas de los tipos de datos **char**, **varchar** o **text** de la página de códigos OEM del sistema a la página de códigos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|RAW|No se realiza ninguna conversión entre páginas de códigos. Ésta es la opción más rápida.|  
|*code_page*|Indica la página de códigos original en la que se codifican los datos de caracteres incluidos en el archivo de datos; por ejemplo, 850.<br /><br /> **\*\* Importante \*\*** Las versiones anteriores a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] no admiten la página de códigos 65001 (codificación UTF-8).|  
  
 ERRORFILE ='*file_name*'  
 Especifica el archivo utilizado para recopilar filas que tienen errores de formato y no pueden convertirse en un conjunto de filas OLE DB. Estas filas se copian en este archivo de errores desde el archivo de datos "tal cual".  
  
 El archivo de errores se crea cuando se inicia la ejecución del comando. Se producirá un error si el archivo ya existe. Además, se crea un archivo de control con la extensión .ERROR.txt. Este archivo hace referencia a cada una de las filas del archivo de errores y proporciona diagnósticos de errores. Tras corregir los errores, pueden cargarse los datos.  
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], `error_file_path` puede estar en Azure Blob Storage. 

'errorfile_data_source_name'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Es un origen de datos externo con nombre que apunta a la ubicación de Azure Blob Storage del archivo de error que contendrá los errores encontrados durante la importación. El origen de datos externo se debe crear con la opción `TYPE = BLOB_STORAGE` que se ha incluido en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para más información, vea [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 FIRSTROW =*first_row*  
 Especifica el número de la primera fila que se va a cargar. El valor predeterminado es 1. Indica la primera fila del archivo de datos especificado. Los números de fila vienen determinados por el recuento de terminadores de fila. FIRSTROW está en base 1.  
  
 LASTROW =*last_row*  
 Especifica el número de la última fila que va a cargarse. El valor predeterminado es 0. Indica la última fila del archivo de datos especificado.  
  
 MAXERRORS =*maximum_errors*  
 Especifica el número máximo de errores de sintaxis o filas no compatibles, tal y como se define en el archivo de formato, que pueden tener lugar antes de que OPENROWSET produzca una excepción. Hasta que se alcance el valor de MAXERRORS, OPENROWSET omite todas las filas erróneas, sin cargarlas, y cuenta cada fila errónea como un error.  
  
 El valor predeterminado de *maximum_errors* es 10.  
  
> [!NOTE]  
>  MAX_ERRORS no se aplica en las restricciones CHECK o para convertir tipos de datos **money** y **bigint**.  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 Especifica el número aproximado de filas de datos del archivo de datos. Este valor debe ser del mismo tipo que el número de filas real.  
  
 OPENROWSET siempre importa un archivo de datos como un solo lote. Con todo, si especifica *rows_per_batch* con un valor > 0, el procesador de consulta usará el valor de *rows_per_batch* como sugerencia para asignar recursos en el plan de consulta.  
  
 De forma predeterminada, el valor de ROWS_PER_BATCH es desconocido. Especificar ROWS_PER_BATCH = 0 es lo mismo que omitir ROWS_PER_BATCH.  
  
 ORDER ( { *column* [ ASC | DESC ] } [ ,... *n* ] [ UNIQUE ] )  
 Sugerencia opcional que especifica la forma en que están ordenados los datos en el archivo. De forma predeterminada, la operación masiva presupone que los datos del archivo no están ordenados. El rendimiento podría mejorar si el optimizador de consultas puede aprovechar el orden especificado para generar un plan de consulta más eficaz. A continuación se citan algunos ejemplos en los que especificar una ordenación puede ser beneficioso:  
  
-   La inserción de filas en una tabla que tiene un índice clúster, donde los datos del conjunto de filas están ordenados en la clave del índice clúster.  
  
-   La combinación del conjunto de filas con otra tabla, donde las columnas de ordenación y combinación coinciden.  
  
-   La agregación de los datos del conjunto de filas por las columnas de ordenación.  
  
-   El uso del conjunto de filas como una tabla de origen en la cláusula FROM de una consulta, donde las columnas de ordenación y combinación coinciden.  
  
 UNIQUE especifica que el archivo de datos no tiene entradas duplicadas.  
  
 Si las filas del archivo de datos no están ordenadas según el orden especificado, o si se ha especificado la sugerencia UNIQUE y hay claves duplicadas, se devuelve un error.  
  
 Se requieren alias de columna cuando se utiliza ORDER. La lista de alias de columna debe hacer referencia a la tabla derivada a la que la cláusula BULK está obteniendo acceso. Los nombres de columna que se especifican en la cláusula ORDER hacen referencia a esta lista de alias de columna. No se pueden especificar columnas con tipos de valor grande (**varchar(max)**, **nvarchar(max)**, **varbinary(max)** y **xml**) ni con tipos de objeto grande (**text**, **ntext** e **image**).  
  
 SINGLE_BLOB  
 Devuelve el contenido de *data_file* como un conjunto de filas de una sola columna y una sola fila de tipo **varbinary(max)**.  
  
> [!IMPORTANT]  
>  Recomendamos que importe los datos XML solo mediante la opción SINGLE_BLOB, en vez de SINGLE_CLOB y SINGLE_NCLOB, ya que solo SINGLE_BLOB admite todas las conversiones de codificación de Windows.  
  
 SINGLE_CLOB  
 Al leer *data_file* como ASCII, el contenido se devuelve como un conjunto de filas de tipo **varchar(max)** de una sola fila y una sola columna, por medio de la intercalación de la base de datos actual.  
  
 SINGLE_NCLOB  
 Al leer *data_file* como UNICODE, el contenido se devuelve como un conjunto de filas de tipo **nvarchar(max)** de una sola fila y una sola columna, por medio de la intercalación de la base de datos actual.  

### <a name="input-file-format-options"></a>Opciones de formato de los archivos de entrada
  
FORMAT **=** 'CSV'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica un archivo de valores separados por comas conforme a la norma [RFC 4180](https://tools.ietf.org/html/rfc4180).

 FORMATFILE ='*format_file_path*'  
 Especifica la ruta de acceso completa de un archivo de formato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite dos tipos de archivos de formato: XML y no XML.  
  
 Es necesario usar un archivo de formato para definir los tipos de columna del conjunto de resultados. La única excepción es cuando se especifica SINGLE_CLOB, SINGLE_BLOB o SINGLE_NCLOB; en este caso, no es necesario usar el archivo de formato.  
  
 Para más información sobre los formatos de archivo, vea [Usar un archivo de formato para importar datos de forma masiva &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, format_file_path puede estar en Azure Blob Storage. Para ver ejemplos, vea [Ejemplos de acceso masivo a datos en Azure Blob Storage](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

FIELDQUOTE **=** 'field_quote'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica un carácter que se usará como carácter de comillas en el archivo CSV. Si no se especifica, se usará el carácter de comillas (") como carácter de comillas, según define la norma [RFC 4180](https://tools.ietf.org/html/rfc4180).

  
## <a name="remarks"></a>Notas  
 `OPENROWSET` se puede usar para tener acceso a datos remotos desde orígenes de datos de OLE DB solo cuando la opción de Registro **DisallowAdhocAccess** está establecida explícitamente en 0 para el proveedor especificado y la opción de configuración avanzada Ad Hoc Distributed Queries está habilitada. Cuando no se establecen estas opciones, el comportamiento predeterminado no permite el acceso ad hoc.  
  
 Al tener acceso remoto a orígenes de datos OLE DB, la identidad de inicio de sesión de las conexiones de confianza no se delegan automáticamente del servidor en el que el cliente se conecta al servidor que se consulta. Debe configurarse la delegación de autenticación.  
  
 Los nombres de catálogo y esquema son necesarios si el proveedor OLE DB admite varios catálogos y esquemas en el origen de datos especificado. Los valores de *catalog* y *schema* se pueden omitir si el proveedor OLE DB no los admite. Si el proveedor solamente admite nombres de esquema, se debe especificar un nombre de dos partes con el formato *esquema ***.*** objeto*. Si el proveedor solamente admite nombres de catálogo, se debe especificar un nombre de tres partes con el formato *catálogo ***.*** esquema ***.*** objeto*. Es necesario especificar nombres de tres partes para las consultas de paso a través que usen el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para más información, vea [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET` no acepta variables para sus argumentos.  
  
 Las llamadas a `OPENDATASOURCE`, `OPENQUERY` o `OPENROWSET` en la cláusula `FROM` se evalúan por separado y de forma independiente de otras llamadas a estas funciones usadas como destino de la actualización, incluso si se han suministrado argumentos idénticos a las dos llamadas. En particular, las condiciones de filtro o combinación aplicadas en el resultado de una de esas llamadas no tienen ningún efecto en los resultados de la otra llamada.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>Utilizar OPENROWSET con la opción BULK  
 Las siguientes mejoras de [!INCLUDE[tsql](../../includes/tsql-md.md)] admiten la función OPENROWSET(BULK…):  
  
-   Las cláusulas FROM que se usan con `SELECT` pueden llamar a `OPENROWSET(BULK...)` en lugar de indicar un nombre de tabla, con toda la funcionalidad de `SELECT`.  
  
     `OPENROWSET` con la opción `BULK` requiere un nombre de correlación en la cláusula `FROM`, que también recibe el nombre de alias o variable de intervalo. Pueden especificarse alias de columna. Si no se especifica una lista de alias de columna, el archivo de formato debe incluir nombres de columna. Al especificar alias de columnas se anulan los nombres de columnas en el archivo de formato:  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    Si `AS <table_alias>` no se puede agregar, se producirá el error:    
>    Mensaje 491, Nivel 16, Estado 1, Línea 20    
>    Debe especificarse un nombre de correlación para el conjunto de filas masivo en la cláusula FROM.    
  
-   Una instrucción `SELECT...FROM OPENROWSET(BULK...)` consulta los datos directamente en el archivo, sin importar los datos a una tabla. Las instrucciones `SELECT…FROM OPENROWSET(BULK...)` también pueden mostrar los alias de las columnas masivas usando un archivo de formato para especificar los nombres de las columnas y también los tipos de datos.  
  
-   Usar `OPENROWSET(BULK...)` como tabla de origen en una instrucción `INSERT` o `MERGE` permite realizar una importación masiva desde un archivo de datos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, vea [Importación en bloque de datos mediante las instrucciones BULK INSERT u OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
-   Cuando se usa la opción `OPENROWSET BULK` BULK con una instrucción `INSERT`, la cláusula BULK admite sugerencias de tabla. Además de las sugerencias de tabla normales, como `TABLOCK`, la cláusula `BULK` puede aceptar las sugerencias de tablas especializadas siguientes: `IGNORE_CONSTRAINTS` (solo pasa por alto las restricciones `CHECK` y `FOREIGN KEY`), `IGNORE_TRIGGERS`, `KEEPDEFAULTS` y `KEEPIDENTITY`. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Para más información sobre cómo usar las instrucciones `INSERT...SELECT * FROM OPENROWSET(BULK...)`, vea [Importar y exportar datos de forma masiva &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). Para obtener más información sobre cuándo se incluyen en el registro de transacciones las operaciones de inserción de filas que se efectúan durante una importación en bloque, vea [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
> [!NOTE]  
>  Cuando use `OPENROWSET`, es importante que entienda el modo en el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controla la suplantación. Para más información sobre las consideraciones de seguridad, vea [Importación en bloque de datos mediante las instrucciones BULK INSERT u OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>Importar de forma masiva datos SQLCHAR, SQLNCHAR o SQLBINARY  
 OPENROWSET(BULK...) presupone que, si no se especifica, la longitud máxima de los datos SQLCHAR, SQLNCHAR o SQLBINARY no supera los 8000 bytes. Si los datos importados están en un campo de datos LOB que incluye cualquier objeto **varchar(max)**, **nvarchar(max)** o **varbinary(max)** que supera los 8000 bytes, debe usar un archivo de formato XML que defina la longitud máxima para el campo de datos. Para especificar la longitud máxima, edite el archivo de formato y declare el atributo MAX_LENGTH.  
  
> [!NOTE]  
>  Un archivo de formato generado automáticamente no especifica la longitud o la longitud máxima de un campo LOB. Sin embargo, es posible editar un archivo de formato y especificar la longitud o la longitud máxima manualmente.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Exportación o importación masiva de documentos SQLXML  
 Para importar o exportar de forma masiva datos SQLXML, utilice uno de los tipos de datos siguientes en el archivo de formato.  
  
|Tipo de datos|Efecto|  
|---------------|------------|  
|SQLCHAR o SQLVARYCHAR|Los datos se envían a la página de códigos del cliente o a la página de códigos implícita por la intercalación.|  
|SQLNCHAR o SQLNVARCHAR|Los datos se envían como datos Unicode.|  
|SQLBINARY o SQLVARYBIN|Los datos se envían sin realizar ninguna conversión.|  
  
## <a name="permissions"></a>Permisos  
 Los permisos de `OPENROWSET` vienen determinados por los permisos del nombre de usuario que se pasa al proveedor OLE DB. Para poder usar la opción `BULK`, se necesita el permiso `ADMINISTER BULK OPERATIONS`.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. Usar OPENROWSET con SELECT y el proveedor OLE DB de SQL Server Native Client  
 En el siguiente ejemplo se usa el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para tener acceso a la tabla `HumanResources.Department` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en el servidor remoto `Seattle1`. (El uso de SQLNCLI y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] redirigirá a la última versión del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client). Se utiliza una instrucción `SELECT` para definir el conjunto de filas devuelto. La cadena de proveedor contiene las palabras clave `Server` y `Trusted_Connection`. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client reconoce estas palabras clave.  
  
```sql  
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
  
```sql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. Usar OPENROWSET y otra tabla en INNER JOIN  
 En el siguiente ejemplo se seleccionan todos los datos de la tabla `Customers` de la instancia local de la base de datos `Northwind` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de la tabla `Orders` de la base de datos `Northwind` de Access que se encuentra en el mismo equipo.  
  
> [!NOTE]  
>  En este ejemplo se supone que está instalado Access. Para ejecutar este ejemplo, debe instalar la base de datos Northwind.  
  
```sql  
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
  
```sql  
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
  
```sql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 El archivo de formato, `values.fmt`, describe las columnas en `values.txt`:  
  
```sql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 Ésta es la consulta que recupera los datos:  
  
```sql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  
  
### <a name="f-specifying-a-format-file-and-code-page"></a>F. Especificar un archivo de formato y una página de códigos  
 En el siguiente ejemplo se muestra cómo usar las opciones de archivo de formato y página de códigos al mismo tiempo.  
  
```sql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. Tener acceso a los datos de un archivo CSV con un archivo de formato  
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
```sql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. Tener acceso a los datos de un archivo CSV sin un archivo de formato

```sql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. Tener acceso a los datos de un archivo almacenado en Azure Blob Storage   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
En el siguiente ejemplo se usa un origen de datos externo que apunta a un contenedor en una cuenta de Azure Storage y una credencial con ámbito de base de datos creada para una firma de acceso compartido.     

```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
Para ver ejemplos completos de `OPENROWSET`, incluido cómo configurar la credencial y el origen de datos externo, vea [Ejemplos de acceso masivo a datos en Azure Blob Storage](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
 
### <a name="additional-examples"></a>Otros ejemplos  
 Para obtener más ejemplos del uso de `INSERT...SELECT * FROM OPENROWSET(BULK...)`, vea los siguientes temas:  
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Ver también  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40;Transact-SQL&#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [Rowset Functions &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
