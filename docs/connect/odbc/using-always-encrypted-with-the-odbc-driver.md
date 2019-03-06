---
title: Uso de Always Encrypted con ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: 1ba94395acad1aec8717c570cc4b6e30ed7a12a4
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662859"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>Uso de Always Encrypted con ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>Aplicable a

- Controlador ODBC 13.1 para SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>Introducción

Este artículo proporciona información sobre cómo desarrollar aplicaciones de ODBC con [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y [ODBC Driver para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

Always Encrypted permite a las aplicaciones cliente cifrar la información confidencial y nunca revelar los datos ni las claves de cifrado en SQL Server o Azure SQL Database. Un controlador habilitado para Always Encrypted, como ODBC Driver for SQL Server, consigue esto al cifrar y descifrar de manera transparente la información confidencial en la aplicación cliente. El controlador determina automáticamente qué parámetros de consulta corresponden a columnas de bases de datos confidenciales (protegidas mediante Always Encrypted) y cifra los valores de esos parámetros antes de pasar los datos a SQL Server o Azure SQL Database. De forma similar, el controlador descifra de manera transparente los datos que se han recuperado de las columnas de bases de datos cifradas de los resultados de la consulta. Para obtener más información, vea [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

### <a name="prerequisites"></a>Prerequisites

Configure Always Encrypted en su base de datos. Esto implica el aprovisionamiento de las claves Always Encrypted y la configuración del cifrado para las columnas de las bases de datos seleccionadas. Si todavía no tiene una base de datos configurada con Always Encrypted, siga las instrucciones de [Introducción a Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). En concreto, la base de datos debe contener las definiciones de metadatos para una clave maestra de columna (CMK), una clave de cifrado de columna (CEK) y una tabla que contiene una o varias columnas cifradas mediante ese CEK.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Habilitar Always Encrypted en una aplicación ODBC

La manera más fácil de habilitar el parámetro cifrado y descifrado de columna cifrada del conjunto de resultados está estableciendo el valor de la `ColumnEncryption` palabra clave de cadena de conexión a **habilitado**. A continuación se muestra un ejemplo de una cadena de conexión que habilita Always Encrypted:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Always Encrypted también estar habilitado en la configuración de DSN, utilizando la misma clave y valor (que serán reemplazada por el valor de cadena de conexión, si está presente), o mediante programación con el `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo anterior a la conexión. Si se establece este modo reemplaza al valor establecido en la cadena de conexión o DSN:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Una vez habilitada para la conexión, se puede ajustar el comportamiento de Always Encrypted para consultas individuales. Para más información, consulte [Controlar el impacto en el rendimiento de Always Encrypted](#controlling-the-performance-impact-of-always-encrypted).

Tenga en cuenta que habilitar Always Encrypted no es suficiente para el cifrado o descifrado se realice correctamente; También deberá asegurarse de que:

- La aplicación tiene los permisos de base de datos *VIEW ANY COLUMN MASTER KEY DEFINITION* y *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , que se requieren para tener acceso a los metadatos sobre las claves Always Encrypted de la base de datos. Para obtener más información, consulte [permisos de base de datos](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- La aplicación puede tener acceso a la CMK que protege el CEK para las columnas cifradas consultadas. Esto depende del proveedor de almacén de claves que almacena la CMK. Consulte [trabajar con almacenes de claves maestras de columna](#working-with-column-master-key-stores) para obtener más información.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperar y modificar los datos de las columnas cifradas

Una vez que habilite Always Encrypted en una conexión, puede usar las API de ODBC estándar (consulte [código de ejemplo ODBC](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) o [referencia del programador de ODBC](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) para recuperar o modificar datos en columnas de la base de datos cifrada. Suponiendo que la aplicación tiene los permisos de base de datos y puede tener acceso a la clave maestra de columna, el controlador cifrará los parámetros de consulta que como destino las columnas cifradas y descifrar los datos recuperados de columnas cifradas, se comporta de forma transparente a la aplicación como si no se cifran las columnas.

Si Always Encrypted no está habilitado, se producirá un error en las consultas con parámetros que tengan como destino las columnas cifradas. Las datos todavía se pueden recuperar de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas. Sin embargo, el controlador no intentará cualquier descifrado y la aplicación recibirá los datos binarios cifrados (como matrices de bytes).

En la tabla siguiente se resume el comportamiento de las consultas, dependiendo de si Always Encrypted está habilitado o no:

|Característica de las consultas | Always Encrypted está habilitado y la aplicación puede tener acceso a las claves y a los metadatos de clave|Always Encrypted está habilitado y la aplicación no puede tener acceso a las claves ni a los metadatos de clave | Always Encrypted está deshabilitado|
|:---|:---|:---|:---|
| Parámetros que se dirigen a columnas cifradas. | Los valores de parámetro se cifran de manera transparente. | Error | Error|
| Recuperación de datos de las columnas cifradas, sin parámetros que tengan como destino las columnas cifradas.| Los resultados de las columnas cifradas se descifran de manera transparente. La aplicación recibe valores de columna de texto simple. | Error | Los resultados de las columnas cifradas no se descifran. La aplicación recibe valores cifrados como matrices de bytes.

En el siguiente ejemplo se ilustra la recuperación y la modificación de datos en las columnas cifradas. Los ejemplos supone una tabla con el siguiente esquema. Tenga en cuenta que las columnas SSN y BirthDate están cifradas.

```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>Ejemplo de inserción de datos

En este ejemplo se inserta una fila en la tabla Patients. Observe lo siguiente:

- No existe nada específico al cifrado en el código de ejemplo. El controlador detecta automáticamente y cifra los valores de los parámetros de SSN y fecha, que se dirigen a columnas cifradas. Esto hace que el cifrado se realice de manera transparente en la aplicación.

- Los valores que se insertan en las columnas de bases de datos, incluidas las columnas cifradas, se pasan como parámetros enlazados (consulte [Función SQLBindParameter](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Aunque el uso de parámetros es opcional al enviar valores a las columnas no cifradas (aunque es altamente recomendable porque ayuda a evitar la inyección de código SQL), es necesario para los valores que tienen como destino las columnas cifradas. Si los valores insertados en las columnas SSN o BirthDate se pasan como literales incrustados en la instrucción de consulta, la consulta produciría un error porque el controlador no intenta cifrar o procesar de otro modo, los literales en consultas. Como resultado, el servidor los rechazará considerándolos incompatibles con las columnas cifradas.

- El tipo SQL del parámetro insertado en la columna SSN se establece en SQL_CHAR, que se asigna a la **char** tipo de datos de SQL Server (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Si el tipo del parámetro se estableció en SQL_WCHAR, que se asigna a **nchar**, la consulta producirá, ya que Always Encrypted no admite conversiones de servidor de los valores cifrados de nchar a valores cifrados char. Consulte [referencia del programador de ODBC: Apéndice D: tipos de datos](https://msdn.microsoft.com/library/ms713607.aspx) para obtener información acerca de las asignaciones de tipos de datos.

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>Ejemplo de recuperación de datos de texto simple

En el siguiente ejemplo se muestra el filtrado de datos basándose en valores cifrados, así como la recuperación de datos de texto sin formato de las columnas cifradas. Observe lo siguiente:

- El valor que se ha usado en la cláusula WHERE para filtrar por la columna SSN necesita pasarse con SQLBindParameter, de forma que el controlador pueda cifrarlo de manera transparente antes de enviarlo al servidor.

- Todos los valores impresos por el programa estarán en texto sin formato, ya que el controlador descifrará los datos que se han recuperado de las columnas SSN y BirthDate de manera transparente.

> [!NOTE]
> Las consultas pueden realizar comparaciones de igualdad en las columnas cifradas solo si el cifrado es determinista. Para obtener más información, vea la sección [Selección del cifrado determinista o aleatorio](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>Ejemplo de recuperación de datos de texto cifrado

Si Always Encrypted no está habilitado, una consulta todavía puede recuperar datos de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas.

En el siguiente ejemplo se ilustra la recuperación de datos binarios cifrados de las columnas cifradas. Observe lo siguiente:

- Como Always Encrypted no está habilitado en la cadena de conexión, la consulta devolverá valores cifrados de SSN y BirthDate como matrices de bytes (el programa convierte los valores en cadenas).
- Una consulta que recupera datos de columnas cifradas con Always Encrypted deshabilitado puede tener parámetros, siempre y cuando ninguno de ellos tenga como destino una columna cifrada. La consulta anterior filtra por LastName, que no está cifrado en la base de datos. Si la consulta ha filtrado por SSN o BirthDate, esta producirá un error.


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitar problemas comunes al consultar columnas cifradas

En esta sección se describen las categorías comunes de errores al consultar columnas cifradas de aplicaciones ODBC y algunas instrucciones sobre cómo evitarlos.

##### <a name="unsupported-data-type-conversion-errors"></a>Errores de conversión de tipos de datos no compatibles

Always Encrypted admite algunas conversiones para los tipos de datos cifrados. Vea [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obtener una lista detallada de las conversiones de tipos compatibles. Para evitar errores de conversión de tipo de datos, asegúrese de observar los siguientes puntos cuando se usa SQLBindParameter con parámetros que tienen como destino columnas cifradas:

- El tipo SQL del parámetro o es exactamente el mismo que el tipo de la columna de destino o se admite la conversión de tipo SQL al tipo de la columna.

- La precisión y la escala de los parámetros que tienen como destino columnas de los tipos de datos `decimal` y `numeric` de SQL Server debe ser la misma que la precisión y la escala configurada para la columna de destino.

- La precisión de los parámetros que tienen como destino las columnas de tipos de datos `datetime2`, `datetimeoffset` o `time` de SQL Server no debe ser superior a la precisión de la columna de destino, en las consultas que modifiquen la columna de destino.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errores debidos a pasar texto sin formato en lugar de valores cifrados

Cualquier valor que tenga como destino una columna cifrada necesita cifrarse antes de enviarse al servidor. Un intento para insertar, modificar o filtrar mediante un valor de texto sin formato en una columna cifrada producirá un error. Para evitar dichos errores, asegúrese de que:

- Always Encrypted esté habilitado (en el DSN, la cadena de conexión conecta antes estableciendo el `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo de conexión para una conexión específica, o la `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo de instrucción de una instrucción específica).

- Usa SQLBindParameter para enviar datos que tengan como destino las columnas cifradas. En el ejemplo siguiente se muestra una consulta que filtra de manera incorrecta mediante un literal o constante por una columna cifrada (SSN), en lugar de pasar el literal como un argumento a SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Precauciones al usar SQLSetPos y SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

El `SQLSetPos` API permite que una aplicación actualizar filas en un conjunto de resultados con los búferes que se enlazaron con SQLBindCol y en qué fila se capturan previamente los datos. Debido al comportamiento de relleno asimétrico de tipos de longitud fija cifrados, es posible alterar los datos de estas columnas al realizar actualizaciones en las demás columnas de la fila de forma inesperada. Con AE, se rellenarán los valores de caracteres de longitud fija si el valor es menor que el tamaño del búfer.

Para mitigar este comportamiento, utilice el `SQL_COLUMN_IGNORE` marca para omitir las columnas que no se actualizará como parte de `SQLBulkOperations` y cuando se usa `SQLSetPos` para el cursor en función de las actualizaciones.  Se deben omitir todas las columnas que no se están modificando directamente por la aplicación, tanto para el rendimiento y para evitar el truncamiento de columnas que están enlazados a un búfer *menor* que su tamaño real de (DB). Para obtener más información, consulte [referencia a la función SQLSetPos](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

Pueden llamar los programas de aplicación [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) para devolver metadatos sobre las columnas en instrucciones preparadas.  Cuando se habilita Always Encrypted, una llamada a `SQLMoreResults` *antes de* una llamada a `SQLDescribeCol` hace [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) se debe llamar, que no correctamente devuelve el texto sin formato metadatos de las columnas cifradas. Para evitar este problema, llame a `SQLDescribeCol` en instrucciones preparadas *antes* una llamada a `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controlar el impacto en el rendimiento de Always Encrypted

Como Always Encrypted es una tecnología de cifrado del lado cliente, la mayoría de las sobrecargas de rendimiento se observan en el lado cliente y no en la base de datos. Además del costo de las operaciones de cifrado y descifrado, los demás orígenes de las sobrecargas de rendimiento en el lado cliente son:

- Ciclos de ida y vuelta adicionales a la base de datos para recuperar metadatos para los parámetros de consulta.

- Llamadas a un almacén de claves maestras de columna para tener acceso a una clave maestra de columna.

En esta sección se describen las optimizaciones integradas de rendimiento en ODBC Driver for SQL Server y la forma en que puede controlar el impacto de los dos factores anteriores en el rendimiento.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlar los ciclos de ida y vuelta para recuperar metadatos para los parámetros de consulta

De forma predeterminada, si Always Encrypted está habilitado para una conexión, el controlador llamará a [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta con parámetros, al pasar la instrucción de consulta (sin ningún valor de parámetro) a SQL Server. Este procedimiento almacenado analiza la instrucción de consulta para averiguar si algún parámetro necesita cifrarse y, si es así, se devuelve la información relacionada con el cifrado para cada parámetro permitir que el controlador cifrarlos. El comportamiento anterior garantiza un alto nivel de transparencia a la aplicación cliente: la aplicación (y el desarrollador de aplicaciones) que no deberá tener en cuenta qué consultas acceden a las columnas cifradas, siempre y cuando se pasan los valores que se dirigen a columnas cifradas a el controlador de parámetros.

### <a name="per-statement-always-encrypted-behavior"></a>Por cada instrucción Always Encrypted comportamiento

Para controlar el impacto de rendimiento de recuperación de metadatos de cifrado para las consultas parametrizadas, puede modificar el comportamiento de Always Encrypted para consultas individuales si se ha habilitado en la conexión. De este modo, puede asegurarse de que `sys.sp_describe_parameter_encryption` se invoca solo para las consultas que sabe que tienen parámetros que se dirigen a columnas cifradas. Pero tenga en cuenta que haciendo esto reduce la transparencia del cifrado: si cifra columnas adicionales en la base de datos, puede que necesite cambiar el código de la aplicación para alinearlo con los cambios de esquema.

Para controlar el comportamiento de Always Encrypted de una instrucción, llame a SQLSetStmtAttr para establecer el `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo de instrucción a uno de los siguientes valores:

|Valor|Descripción|
|-|-|
|`SQL_CE_DISABLED` (0)|Always Encrypted está deshabilitado para la instrucción|
|`SQL_CE_RESULTSETONLY` (1)|Solo el descifrado. Los conjuntos de resultados y valores devueltos se descifran y los parámetros no están cifrados|
|`SQL_CE_ENABLED` (3) | Siempre Encrypted está habilitado y se usa para los parámetros y resultados|

Identificadores de instrucción nuevo creados a partir de una conexión con Always Encrypted habilitado de forma predeterminada SQL_CE_ENABLED. Esos creado a partir de una conexión con él deshabilitado de forma predeterminada SQL_CE_DISABLED (y no es posible habilitar Always Encrypted en ellas.)

Si la mayoría de las consultas de una aplicación cliente tener acceso a las columnas cifradas, se recomienda lo siguiente:

- Establezca la palabra clave de cadena de conexión `ColumnEncryption` en `Enabled`.

- Establecer el `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo `SQL_CE_DISABLED` en las instrucciones que no tienen acceso a ninguna columna cifrada. Esto deshabilitará ambos llamada `sys.sp_describe_parameter_encryption` , así como los intentos para descifrar los valores en el resultado establecido.
    
- Establecer el `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo `SQL_CE_RESULTSETONLY` en las instrucciones que no tiene ningún parámetro que requiera cifrado, pero que recuperen datos de las columnas cifradas. Esto deshabilitará la llamada `sys.sp_describe_parameter_encryption` y cifrado de parámetros. Los resultados que contienen columnas cifradas continuará para descifrarla.

## <a name="always-encrypted-security-settings"></a>Always Encrypted configuración de seguridad

### <a name="force-column-encryption"></a>Forzar el cifrado de columna

Para forzar el cifrado de un parámetro, establezca el `SQL_CA_SS_FORCE_ENCRYPT` campo descriptor de parámetro de implementación (IPD) mediante una llamada a la función SQLSetDescField. Un valor distinto de cero hace que el controlador devolverá un error cuando no se devuelve ningún metadato de cifrado para el parámetro asociado.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Si SQL Server indica al controlador que no hace falta cifrar el parámetro, las consultas que utilice este último generarán un error. Esto confiere una protección adicional frente a ataques contra la seguridad que utilice un servidor SQL Server comprometido que proporcione metadatos de cifrado incorrectos al cliente, lo cual podría provocar la divulgación de datos.

### <a name="column-encryption-key-caching"></a>Almacenamiento en memoria caché de claves de cifrado de columnas

Para reducir el número de llamadas a un almacén de claves maestras de columna para descifrar las claves de cifrado de columna, el controlador almacena en caché el CEK de texto simple en la memoria. La caché de la CEK es global para el controlador y no están asociados con una conexión de prueba. Después de recibir ECEK de metadatos de la base de datos, en primer lugar el controlador intenta encontrar la CEK de texto simple correspondiente al valor de clave cifrado en la memoria caché. El controlador llama al almacén de claves que contiene la CMK solo si no encuentra el CEK de texto sin formato correspondiente en la memoria caché.

> [!NOTE]
> En el controlador ODBC para SQL Server, las entradas de la memoria caché se expulsan después de un tiempo de espera de dos horas. Esto significa que para un determinado ECEK, el controlador se pone en contacto el almacén de claves solo una vez durante la vigencia de la aplicación o cada dos horas, lo que sea menor.

A partir del 17.1 del controlador ODBC para SQL Server, el tiempo de espera de caché CEK puede ajustarse mediante el `SQL_COPT_SS_CEKCACHETTL` atributo de conexión, que especifica el número de segundos que una CEK permanecerá en la memoria caché. Dada la naturaleza global de la memoria caché, este atributo se puede ajustar de cualquier identificador de conexión válida para el controlador. Cuando la memoria caché se reduce el TTL, las CEK existentes que se superaría el nuevo valor de TTL también se expulsan. Si es 0, no las CEK se almacenan en caché.

### <a name="trusted-key-paths"></a>Rutas de acceso de claves de confianza

A partir de la 17.1 del controlador ODBC para SQL Server, el `SQL_COPT_SS_TRUSTEDCMKPATHS` atributo de conexión permite que una aplicación requerir que las operaciones de Always Encrypted solo usen una lista especificada de CMK, identificados por sus rutas de acceso de claves. De forma predeterminada, este atributo es NULL, lo que significa que el controlador acepta cualquier ruta de acceso de clave. Para usar esta característica, establezca `SQL_COPT_SS_TRUSTEDCMKPATHS` para que apunte a una cadena de caracteres anchos delimitada por valores null, terminada en null que se enumera las rutas de acceso de clave permitidos. La memoria a la que señala a este atributo debe seguir siendo válida durante las operaciones de cifrado o descifrado con el identificador de conexión en el que se establece---en el que el controlador comprobará si la ruta de acceso CMK según lo especificado por los metadatos del servidor es entre mayúsculas y minúsculas en este lista. Si la ruta de acceso CMK no está en la lista, se produce un error en la operación. La aplicación puede cambiar el contenido de la memoria que este atributo señala, cambiar su lista de confianza CMK, sin tener que establecer el atributo nuevo.

## <a name="working-with-column-master-key-stores"></a>Trabajar con almacenes de claves maestras de columna

Para cifrar o descifrar los datos, el controlador necesita obtener una CEK que esté configurada para la columna de destino. Las CEK se almacenan en formato cifrado (ECEKs) en los metadatos de la base de datos. Cada CEK tiene una CMK correspondiente que se usó para cifrarlo. El [los metadatos de la base de datos](../../t-sql/statements/create-column-master-key-transact-sql.md) no almacena la CMK sí; solo contiene el nombre del almacén de claves y la información que puede usar el almacén de claves para buscar la CMK.

Para obtener el valor de texto simple de un ECEK, el controlador obtiene los metadatos acerca de la CEK y su CMK correspondiente y, a continuación, usa esta información para ponerse en contacto con el almacén de claves que contiene la CMK y lo solicita descifrar ECEK. El controlador se comunica con un almacén de claves mediante un proveedor de almacén de claves.

### <a name="built-in-keystore-providers"></a>Proveedores de almacén de claves integrada

El controlador ODBC para SQL Server incluye los siguientes proveedores de almacén de claves integrada:

| Nombre | Descripción | Nombre del proveedor (metadatos) |Disponibilidad|
|:---|:---|:---|:---|
|Azure Key Vault |Almacenes CMK en Azure Key Vault | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Almacén de certificados de Windows|Almacena CMK localmente en el almacén de claves de Windows| `MSSQL_CERTIFICATE_STORE`|Windows|

- Usted (o su DBA) necesita asegurarse de que el nombre de proveedor, configurado en los metadatos de clave maestra de columna, sea correcto y que la ruta de acceso de la clave maestra de columna cumpla con un formato de ruta de acceso de la clave para un proveedor determinado. Se recomienda que configure las claves mediante herramientas como SQL Server Management Studio, que genera automáticamente las rutas de acceso a la clave y los nombres de proveedor válidos al emitir la instrucción [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) (Transact-SQL).

- Necesita asegurarse de que la aplicación pueda tener acceso a la clave del almacén de claves. Esto puede suponer conceder a la aplicación el acceso a la clave o al almacén de claves, dependiendo de este, o realizar cualquier otro paso de configuración específico del almacén de claves. Por ejemplo, para tener acceso a una instancia de Azure Key Vault, deberá proporcionar las credenciales correctas para el almacén de claves.

### <a name="using-the-azure-key-vault-provider"></a>Usar el proveedor de Azure Key Vault

El Almacén de claves de Azure es una opción adecuada para almacenar y administrar claves maestras de columna para Always Encrypted (especialmente si sus aplicaciones se hospedan en Azure). El controlador ODBC para SQL Server en Linux, macOS y Windows incluye un proveedor de almacén de claves maestras de columna integrada para Azure Key Vault. Consulte [Azure Key Vault - paso a paso](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [Introducción a Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), y [crear claves maestras de columna en Azure Key Vault](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) para obtener más información sobre cómo configurar una clave de Azure Almacén de Always Encrypted.

> [!NOTE]
> En Linux y macOS, para la versión 17.2 y versiones posterior, del controlador `libcurl` es necesario utilizar este proveedor, pero no es una dependencia explícita, ya que otras operaciones con el controlador no lo necesita. Si se produce un error referente a `libcurl`, asegúrese de está instalado.

El controlador admite la autenticación en Azure Key Vault mediante los siguientes tipos de credencial:

- Nombre de usuario/contraseña - con este método, las credenciales son el nombre de un usuario de Azure Active Directory y su contraseña.

- Id. de cliente/secreto: con este método, las credenciales son un identificador de cliente de aplicación y un secreto de aplicación.

- -La identidad de servicio administrada con este método, son las credenciales de identidad asignada por el sistema o la identidad asignada por el usuario. Para la identidad asignada por el usuario, UID se establece en el identificador de objeto de la identidad del usuario.

Para permitir que el controlador use CMK almacenada en AKV para el cifrado de columna, utilice las siguientes palabras clave de cadena de conexión solo:

|Tipo de credencial| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Nombre de usuario y contraseña| `KeyVaultPassword`|Nombre principal del usuario|Contraseña|
|Id. o el secreto de cliente| `KeyVaultClientSecret`|Id. de cliente|Secreto|

#### <a name="example-connection-strings"></a>Ejemplos de cadena de conexión

Las cadenas de conexión siguiente muestran cómo autenticarse en Azure Key Vault con los dos tipos de credenciales:

**ClientID o secreto**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Nombre de usuario y contraseña**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Ningún otro cambio de la aplicación ODBC deben usar Azure Key VAULT para el almacenamiento CMK.

### <a name="using-the-windows-certificate-store-provider"></a>Uso del proveedor para el Almacén de certificados de Windows

El controlador ODBC para SQL Server en Windows incluye un proveedor de almacén de claves maestras de columna integrada para el Store de certificados de Windows denominado `MSSQL_CERTIFICATE_STORE`. (Este proveedor no está disponible en macOS o Linux). Con este proveedor, la CMK se almacena localmente en el equipo cliente y no es necesaria para usarlo con el controlador de ninguna configuración adicional por parte de la aplicación. Sin embargo, la aplicación debe tener acceso al certificado y su clave privada en el almacén. Vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted) para obtener más información.

### <a name="using-custom-keystore-providers"></a>Usar proveedores de almacén de claves personalizados

El controlador ODBC para SQL Server también admite proveedores de almacén de claves personalizados de terceros mediante la interfaz CEKeystoreProvider. Esto permite que una aplicación cargar, la consulta y configurar los proveedores de almacén de claves de modo que puede usar el controlador para tener acceso a las columnas cifradas. Las aplicaciones pueden interactuar directamente con un proveedor de almacén de claves con el fin de cifrar las CEK para el almacenamiento en SQL Server y realizar tareas más allá de obtener acceso a las columnas cifradas con ODBC; Para obtener más información, consulte [proveedores de almacén de claves personalizados](../../connect/odbc/custom-keystore-providers.md).

Dos atributos de conexión se usan para interactuar con proveedores de almacén de claves personalizados. Estas sobrecargas son:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

El primero se usa para cargar y enumerar los proveedores cargados del almacén de claves, mientras que la última habilita a las comunicaciones del proveedor de la aplicación. Estos atributos de conexión pueden utilizarse en cualquier momento, antes o después de establecer una conexión, puesto que la interacción con el proveedor de la aplicación no requiere comunicación con SQL Server. Sin embargo, porque aún no se ha cargado el controlador, establecer y obtener estos atributos antes de conectar hará que se procesan mediante el Administrador de controladores y es posible que no muestra los resultados esperados.

#### <a name="loading-a-keystore-provider"></a>Cargar un proveedor de almacén de claves

Establecer el `SQL_COPT_SS_CEKEYSTOREPROVIDER` atributo de conexión permite que una aplicación cliente cargar una biblioteca de proveedores, hacer que estén disponibles para su uso los proveedores de almacén de claves contenidos en ella.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| Argumento | Descripción |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde cualquier otro en el mismo proceso.|
|`Attribute`|[Entrada] Atributo que se establecerá: el `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Entrada] Puntero a una cadena de caracteres terminada en null que se especifica el nombre de archivo de la biblioteca del proveedor. Para SQLSetConnectAttrA, se trata de una cadena (multibyte) de ANSI. Para SQLSetConnectAttrW, esto es una cadena Unicode (wchar_t).|
|`StringLength`|[Entrada] La longitud de la cadena ValuePtr o SQL_NTS.|

El controlador intenta cargar la biblioteca identificada por el parámetro ValuePtr mediante la biblioteca dinámica definido por la plataforma de mecanismo de carga (`dlopen()` en Linux y macOS, `LoadLibrary()` en Windows), y agrega todos los proveedores definidos en ellas a la lista de proveedores que sabe que el controlador. Pueden producirse los errores siguientes:

| Error | Descripción |
|:--|:--|
|`CE203`|No se pudo cargar la biblioteca dinámica.|
|`CE203`|No se encontró el símbolo "CEKeyStoreProvider" exportado en la biblioteca.|
|`CE203`|Uno o varios proveedores en la biblioteca ya están cargados.|

`SQLSetConnectAttr` Devuelve el error habitual o valores correctos e información adicional está disponible para los errores que se ha producido a través del mecanismo de diagnóstico ODBC estándar.

> [!NOTE]
> El programador de la aplicación debe asegurarse de que todos los proveedores personalizados se cargan antes de cualquier consulta exigirles que se envía a través de cualquier conexión. Si no lo hace, se producirá el siguiente error:

| Error | Descripción |
|:--|:--|
|`CE200`|Proveedor de almacén de claves %1 no encontrado. Asegúrese de que se ha cargado la biblioteca del proveedor de almacén de claves adecuado.|

> [!NOTE]
> Los implementadores de proveedor de almacén de claves deben evitar el uso de `MSSQL` en el nombre de sus proveedores personalizados. Este término se reserva exclusivamente para uso de Microsoft y puede provocar conflictos con futuras proveedores integrados. Uso de este término en el nombre de un proveedor personalizado puede producir una advertencia de ODBC.

#### <a name="getting-the-list-of-loaded-providers"></a>Obtener la lista de proveedores cargados

Obtener el atributo de conexión permite que una aplicación cliente determinar los proveedores de almacén de claves cargados actualmente en el controlador (incluidas aquellas creadas). Solo puede realizarse después de conectarse.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| Argumento | Descripción |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde cualquier otro en el mismo proceso.|
|`Attribute`|[Entrada] Atributo para recuperar: el `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Salida] Un puntero a la memoria en el que se va a devolver el siguiente nombre de proveedor cargado.|
|`BufferLength`|[Entrada] La longitud del búfer ValuePtr.|
|`StringLengthPtr`|[Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (excluido el carácter de terminación null) disponibles para devolver en \*ValuePtr. Si ValuePtr es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponible para devolver es mayor que BufferLength menos la longitud de la terminación null de caracteres, los datos de \*ValuePtr se trunca a BufferLength menos la longitud de la carácter de terminación NULL y termina en null por el controlador.|

Para permitir la recuperación de toda la lista, cada operación Get devuelve el nombre del proveedor actual e incrementa un contador interno a la siguiente. Una vez que este contador llega al final de la lista, una cadena vacía ("") se devuelve, y se restablece el contador; operaciones Get sucesivas, a continuación, continuar nuevo desde el principio de la lista.

### <a name="communicating-with-keystore-providers"></a>Comunicación con proveedores de almacén de claves

El `SQL_COPT_SS_CEKEYSTOREDATA` atributo de conexión permite que una aplicación cliente para comunicarse con los proveedores de almacén de claves de carga para configurar parámetros adicionales, la incrustación de material, etcetera. La comunicación entre una aplicación cliente y un proveedor sigue un protocolo simple de solicitud-respuesta, en función de Get y Set solicita mediante el atributo de conexión. Se inicia la comunicación solo por la aplicación cliente.

> [!NOTE]
> Debido a la naturaleza de ODBC llama a responder de CEKeyStoreProvider a (SQLGet/SetConnectAttr), ODBC admite la interfaz sola establecer datos en la resolución del contexto de conexión.

La aplicación se comunica con los proveedores de almacén de claves a través del controlador a través de la estructura CEKeystoreData:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```

| Argumento | Descripción |
|:---|:---|
|`name`|[Entrada] En conjunto, el nombre del proveedor al que se envían los datos. Se omite en Get. Cadena terminada en null, en caracteres anchos.|
|`dataSize`|[Entrada] El tamaño de la matriz de datos siguiendo la estructura.|
|`data`|[Entrada] En conjunto, los datos que se envía al proveedor. Esto puede ser datos arbitrarios; el controlador hace que intenta interpretarla. Tras la Get, leer el búfer para recibir los datos del proveedor.|

#### <a name="writing-data-to-a-provider"></a>Escribir datos en un proveedor

Un `SQLSetConnectAttr` llamar mediante el `SQL_COPT_SS_CEKEYSTOREDATA` atributo escribe un "paquete" de datos en el proveedor de almacén de claves especificado.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| Argumento | Descripción |
|:---|:---|
|`ConnectionHandle`| [Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde cualquier otro en el mismo proceso.|
|`Attribute`|[Entrada] Atributo que se establecerá: el `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Entrada] Puntero a una estructura CEKeystoreData. El campo de nombre de la estructura identifica el proveedor que se dirige los datos.|
|`StringLength`|[Entrada] Constante SQL_IS_POINTER|

Información detallada del error adicional puede obtenerse a través de [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> El proveedor puede usar el identificador de conexión para asociar los datos escritos en una conexión específica, si así lo desea. Esto es útil para implementar la configuración de cada conexión. También puede pasar por alto el contexto de conexión y tratar los datos de forma idéntica independientemente de la conexión usada para enviar los datos. Consulte [asociación contexto](../../connect/odbc/custom-keystore-providers.md#context-association) para obtener más información.

#### <a name="reading-data-from-a-provider"></a>Leer datos de un proveedor

Una llamada a `SQLGetConnectAttr` utilizando el `SQL_COPT_SS_CEKEYSTOREDATA` atributo lee un "paquete" de datos de *el último escrito-a* proveedor. Si no hay ninguna, se produce un Error de secuencia de función. Los implementadores de proveedor de almacén de claves se recomienda para admitir dummy "escritura" de 0 bytes como una manera de seleccionar el proveedor para las operaciones de lectura sin provocar otros efectos secundarios, si tiene sentido hacerlo.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| Argumento | Descripción |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde cualquier otro en el mismo proceso.|
|`Attribute`|[Entrada] Atributo para recuperar: el `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Salida] Un puntero a una estructura CEKeystoreData en la que se colocan los datos leídos desde el proveedor.|
|`BufferLength`|[Entrada] Constante SQL_IS_POINTER|
|`StringLengthPtr`|[Salida] Un puntero a un búfer en el que se va a devolver BufferLength. Si * ValuePtr no es un puntero nulo, se devuelve ninguna longitud.|

El llamador debe asegurarse de que se asigna un búfer de longitud suficiente siguiendo la estructura CEKEYSTOREDATA que escribir en el proveedor. Cuando se devuelve, su campo dataSize se actualiza con la longitud real de los datos leídos desde el proveedor. Información detallada del error adicional puede obtenerse a través de [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Esta interfaz no impone ningún requisito adicional sobre el formato de datos transferidos entre una aplicación y un proveedor de almacén de claves. Cada proveedor puede definir su propio formato de datos del protocolo, según sus necesidades.

Para obtener un ejemplo de la implementación de su propio proveedor de almacén de claves, consulte [proveedores de almacén de claves personalizados](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Limitaciones del controlador ODBC cuando se usa Always Encrypted

### <a name="asynchronous-operations"></a>Operaciones asincrónicas
Mientras que el controlador ODBC permitirá el uso de [operaciones asincrónicas](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) con Always Encrypted, hay un impacto en el rendimiento en las operaciones cuando Always Encrypted está habilitado. La llamada a `sys.sp_describe_parameter_encryption` para determinar los metadatos de cifrado de la instrucción está bloqueando y hará que el controlador de espera para que el servidor devolver los metadatos antes de devolver `SQL_STILL_EXECUTING`.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>Recuperar datos de partes con SQLGetData
Antes de cifrar ODBC Driver 17 for SQL Server, las columnas binarias y carácter no se puede recuperar en partes con SQLGetData. Sólo una llamada a SQLGetData puede realizarse con un búfer de longitud suficiente para contener los datos de la columna completa.

### <a name="send-data-in-parts-with-sqlputdata"></a>Enviar datos de partes con SQLPutData
No se puede enviar datos de inserción o de comparación en partes con SQLPutData. Puede realizar solo una llamada a SQLPutData, con un búfer que contiene todos los datos. Para insertar datos long en columnas cifradas, use la API de copia masiva, se describe en la sección siguiente, con un archivo de datos de entrada.

### <a name="encrypted-money-and-smallmoney"></a>Smallmoney y money cifrada
Cifrado **dinero** o **smallmoney** parámetros no pueden tener como destino las columnas, ya que no específicos para el que se asigna a esos tipos, lo que produce errores de conflicto de tipo de operando de tipo de datos ODBC.

## <a name="bulk-copy-of-encrypted-columns"></a>Copia masiva de las columnas cifradas

El uso de la [funciones de copia masiva de SQL](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) y **bcp** utilidad es compatible con Always Encrypted desde ODBC Driver 17 for SQL Server. Texto simple (cifrada en inserción y recuperación descifrada en) y texto cifrado (transferida literalmente) se pueden insertar y recuperar mediante la copia masiva (bcp_&#42;) API y la **bcp** utilidad.

- Para recuperar el texto cifrado en formato varbinary (max) (por ejemplo, para la carga masiva en una base de datos diferente), conectarse sin el `ColumnEncryption` opción (o establézcalo en `Disabled`) y realizar una operación BCP OUT.

- Para insertar y recuperar el texto simple y dejar que el controlador de forma transparente realizar el cifrado y descifrado como la configuración necesaria, `ColumnEncryption` a `Enabled` es suficiente. En caso contrario, se modifica la funcionalidad de la API de BCP.

- Para insertar texto cifrado en formato varbinary (max) (p. ej., como recuperados anteriormente), establezca el `BCPMODIFYENCRYPTED` opción en TRUE y realizar una operación BCP IN. En el orden de los datos resultantes se decryptable, asegúrese de que el destino CEK de la columna es igual que desde el que se ha obtenido originalmente el texto cifrado.

Cuando se usa el **bcp** utilidad: controlar la `ColumnEncryption` establecer, use la opción -D y especifique un DSN que contiene el valor deseado. Para insertar texto cifrado, asegúrese del `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` está habilitada la configuración del usuario.

En la tabla siguiente proporciona un resumen de las acciones cuando se trabaja en una columna cifrada:

|`ColumnEncryption`|Dirección BCP|Descripción|
|----------------|-------------|-----------|
|`Disabled`|OUT (al cliente)|Recupera el texto cifrado. Es el tipo de datos observada **varbinary (max)**.|
|`Enabled`|OUT (al cliente)|Recupera texto simple. El controlador descifrará los datos de columna.|
|`Disabled`|IN (en el servidor)|Inserta el texto cifrado. Esto se pretende de manera opaca mover los datos cifrados sin necesidad de se pueden descifrar. La operación dará error si el `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` opción no está establecida en el usuario o BCPMODIFYENCRYPTED no está establecida en el identificador de conexión. Para obtener más información, vea lo siguiente.|
|`Enabled`|IN (en el servidor)|Inserta texto simple. El controlador cifrará los datos de columna.|

### <a name="the-bcpmodifyencrypted-option"></a>La opción BCPMODIFYENCRYPTED

Para evitar daños en los datos, el servidor normalmente no permite insertar texto cifrado directamente en una columna cifrada, y, por tanto, se producirá un error si intenta hacerlo; Sin embargo, para la carga masiva de datos cifrados mediante la API de BCP, establecer el `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) opción en TRUE permite texto cifrado para insertarse directamente y reduce el riesgo de dañar los datos cifrados a través de la configuración de la `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` opción en la cuenta de usuario. Sin embargo, las claves deben coincidir con los datos y resulta una buena idea realizar algunas comprobaciones de solo lectura de los datos insertados después de la inserción masiva y antes de usarlo.

Vea [Migración de datos confidenciales protegidos mediante Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md) para obtener más información.

## <a name="always-encrypted-api-summary"></a>Resumen de la API de Always Encrypted

### <a name="connection-string-keywords"></a>Palabras clave de cadena de conexión

|Nombre|Descripción|  
|----------|-----------------|  
|`ColumnEncryption`|Valores aceptados son `Enabled` / `Disabled`.<br>`Enabled`: habilita o deshabilita la funcionalidad de Always Encrypted para la conexión.<br>`Disabled`: deshabilita la funcionalidad de Always Encrypted para la conexión. <br><br>El valor predeterminado es `Disabled`.|  
|`KeyStoreAuthentication` | Valores válidos: `KeyVaultPassword`, `KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Cuando `KeyStoreAuthentication`  =  `KeyVaultPassword`, establezca este valor en un nombre válido de entidad de usuario de Active Directory de Azure. <br>Cuando `KeyStoreAuthetication`  =  `KeyVaultClientSecret` establezca este valor en un Azure Active Directory aplicación cliente identificador válido |
|`KeyStoreSecret` | Cuando `KeyStoreAuthentication`  =  `KeyVaultPassword` establezca este valor en la contraseña para el nombre de usuario correspondiente. <br>Cuando `KeyStoreAuthentication`  =  `KeyVaultClientSecret` establezca este valor en el secreto de aplicación asociados con un Azure Active Directory aplicación cliente identificador válido |


### <a name="connection-attributes"></a>Atributos de conexión

|Nombre|Tipo|Descripción|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Antes de conectar|`SQL_COLUMN_ENCRYPTION_DISABLE` (0): deshabilitar Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1): habilitar Always Encrypted|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Después de conectar|[Establecer] Intenta cargar CEKeystoreProvider<br>[Obtener] Devolver un nombre CEKeystoreProvider|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Después de conectar|[Establecer] Escribir datos en CEKeystoreProvider<br>[Obtener] Leer datos de CEKeystoreProvider|
|`SQL_COPT_SS_CEKCACHETTL`|Después de conectar|[Establecer] Establecer la memoria caché CEK TTL<br>[Obtener] Obtener la caché actual de la CEK TTL|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|Después de conectar|[Establecer] Establecer el puntero de rutas de acceso CMK confianza<br>[Obtener] Obtener el puntero de rutas de acceso CMK de confianza actual|

### <a name="statement-attributes"></a>Atributos de instrucción

|Nombre|Descripción|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0): always Encrypted está deshabilitado para la instrucción <br>`SQL_CE_RESULTSETONLY` (1): solo el descifrado. Los conjuntos de resultados y valores devueltos se descifran y los parámetros no están cifrados <br>`SQL_CE_ENABLED` (3): always Encrypted está habilitado y se utiliza para los parámetros y los resultados|

### <a name="descriptor-fields"></a>Campos de descriptor

|Campo IPD|Tipo y tamaño|Valor predeterminado|Descripción|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 bytes)|0|Cuando 0 (valor predeterminado): la decisión para cifrar este parámetro viene determinada por la disponibilidad de los metadatos de cifrado.<br><br>Cuando es distinto de cero: si los metadatos de cifrado están disponible para este parámetro, se cifra. En caso contrario, produce un error en la solicitud con error [CE300] cifrado obligatorio [Microsoft] [ODBC Driver 13 para SQL Server] se ha especificado para un parámetro pero no hay metadatos de cifrado proporcionada por el servidor.|

### <a name="bcpcontrol-options"></a>bcp_control opciones

|Nombre de la opción|Valor predeterminado|Descripción|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|Cuando es TRUE, permite valores varbinary (max) va a insertar en una columna cifrada. Cuando sea FALSE, impide la inserción a menos que se proporcionen los metadatos de cifrado y el tipo correcto.|

## <a name="see-also"></a>Consulte también

- [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Blog de Always Encrypted](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

