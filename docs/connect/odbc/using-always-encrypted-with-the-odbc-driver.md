---
title: Uso de Always Encrypted with the ODBC Driver 13.1 para SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
caps.latest.revision: 3
ms.author: v-chojas
manager: jhubbard
author: MightyPen
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e02c46bc1e068d75d9a67413f45b303616ccd82b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-always-encrypted-with-the-odbc-driver-131-for-sql-server"></a>Uso de Always Encrypted with the ODBC Driver 13.1 para SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

Este artículo proporciona información sobre cómo desarrollar aplicaciones de ODBC mediante [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx) y [ODBC Driver 13.1 para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

Always Encrypted permite a las aplicaciones cliente cifrar la información confidencial y nunca revelar los datos ni las claves de cifrado en SQL Server o Azure SQL Database. Un Always Encrypted habilitado el controlador, como ODBC Driver 13.1 para SQL Server, consigue esto al cifrar y descifrar datos confidenciales en la aplicación cliente de forma transparente. El controlador determina automáticamente qué parámetros de consulta corresponden a columnas de bases de datos confidenciales (protegidas mediante Always Encrypted) y cifra los valores de esos parámetros antes de pasar los datos a SQL Server o Azure SQL Database. De forma similar, el controlador descifra de manera transparente los datos que se han recuperado de las columnas de bases de datos cifradas de los resultados de la consulta. Para obtener más información, vea [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx).

### <a name="prerequisites"></a>Requisitos previos

Configure Always Encrypted en su base de datos. Esto implica el aprovisionamiento de las claves Always Encrypted y la configuración del cifrado para las columnas de las bases de datos seleccionadas. Si todavía no tiene una base de datos configurada con Always Encrypted, siga las instrucciones de [Introducción a Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). En concreto, la base de datos debe contener las definiciones de metadatos para una clave maestra de columna (CMK) y una clave de cifrado de columna (CEK), una tabla que contiene una o varias columnas que se cifra mediante ese CEK.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Habilitar Always Encrypted en una aplicación ODBC

Es la manera más fácil de habilitar el cifrado de parámetro y el descifrado de columna de conjunto de resultados que se cifran al establecer el valor de la `ColumnEncryption` palabra clave de cadena de conexión a **habilitado**. El siguiente es un ejemplo de una cadena de conexión que habilita Always Encrypted:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Always Encrypted también estar habilitado en la configuración de DSN, con la misma clave y valor (lo que serán reemplazada por el valor de cadena de conexión, si está presente), o mediante programación con el `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo anterior a la conexión. Si se establece este modo, invalida el valor establecido en la cadena de conexión o DSN:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Una vez habilitada para la conexión, se puede ajustar el comportamiento de Always Encrypted para consultas individuales. Vea [controlar el rendimiento de impacto de Always Encrypted](#controlling-the-performance-impact-of-always-encrypted) a continuación para obtener más información.

Tenga en cuenta que habilitar Always Encrypted no es suficiente para el cifrado o descifrado se realicen correctamente; También debe asegurarse de:

- La aplicación tiene los permisos de base de datos *VIEW ANY COLUMN MASTER KEY DEFINITION* y *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , que se requieren para tener acceso a los metadatos sobre las claves Always Encrypted de la base de datos. Para obtener más información, consulte [permisos de base de datos](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- La aplicación puede tener acceso a la CMK que protege el CEK de las columnas cifradas consultadas. Se trata depende del proveedor de almacén de claves que almacena la CMK. Vea [trabajar con almacenes de claves maestras de columna](#working-with-column-master-key-stores) para obtener más información.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperar y modificar los datos de las columnas cifradas

Una vez que habilite Always Encrypted en una conexión, puede usar la API de ODBC estándar (vea [código de ejemplo ODBC](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) o [referencia del programador de ODBC](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) para recuperar o modificar datos en las columnas de la base de datos cifrada. Suponiendo que la aplicación tiene los permisos de base de datos y puede tener acceso a la clave maestra de columna, el controlador cifrará cualquier parámetro de consulta que destino las columnas cifradas y descifrar los datos recuperados de columnas cifradas, que se comporta de forma transparente para el aplicación como si las columnas no se cifran.

Si Always Encrypted no está habilitado, se producirá un error en las consultas con parámetros que se dirigen a columnas cifradas. Todavía se pueden recuperar datos de las columnas cifradas, siempre y cuando la consulta no tiene ningún parámetro dirigidos a columnas cifradas. Sin embargo, el controlador no intentará cualquier descifrado y la aplicación recibirá los datos binarios cifrados (como matrices de bytes).

En la tabla siguiente se resume el comportamiento de las consultas, dependiendo de si Always Encrypted está habilitado o no:

|Característica de las consultas | Always Encrypted está habilitado y la aplicación puede tener acceso a las claves y a los metadatos de clave|Always Encrypted está habilitado y la aplicación no puede tener acceso a las claves ni a los metadatos de clave | Always Encrypted está deshabilitado|
|:---|:---|:---|:---|
| Parámetros que se dirigen a columnas cifradas. | Los valores de parámetro se cifran de manera transparente. | Error | Error|
| Recuperar datos de las columnas cifradas, sin parámetros que se dirigen a columnas cifradas.| Los resultados de las columnas cifradas se descifran de manera transparente. La aplicación recibe valores de columna de texto simple. | Error | Los resultados de las columnas cifradas no se descifran. La aplicación recibe valores cifrados como matrices de bytes.

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

- No existe nada específico al cifrado en el código de ejemplo. El controlador detecta automáticamente y cifra los valores de los parámetros de fecha y número de seguridad social, que se dirigen a columnas cifradas. Esto hace que el cifrado se realice de manera transparente en la aplicación.

- Los valores insertados en las columnas de base de datos, incluidas las columnas cifradas, se pasan como parámetros enlazados (vea [función SQLBindParameter](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Mientras que el uso de parámetros es opcional al enviar valores a columnas no cifradas (aunque se recomienda porque ayuda a evitar la inyección de código SQL), es necesario para los valores que se dirigen a columnas cifradas. Si los valores insertados en las columnas SSN o BirthDate se pasan como literales incrustados en la instrucción de consulta, la consulta produciría un error porque el controlador no intenta cifrar o procesar de otro modo literales en las consultas. Como resultado, el servidor los rechazará considerándolos incompatibles con las columnas cifradas.

- El tipo SQL del parámetro que se inserta en la columna SSN se establece en SQL_CHAR, que se asigna a la **char** tipo de datos de SQL Server (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Si el tipo del parámetro se establece a SQL_WCHAR, que se asigna al **nchar**, la consulta producirá, ya que Always Encrypted no admite conversiones de servidor de valores cifrados de nchar a valores cifrados char. Vea [referencia del programador de ODBC: tipos de datos de apéndice D:](https://msdn.microsoft.com/library/ms713607.aspx) para obtener información acerca de las asignaciones de tipos de datos.

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

- El valor que se utiliza en la cláusula WHERE para filtrar según la columna SSN necesita pasarse mediante SQLBindParameter, por lo que el controlador puede cifrarlo de manera transparente antes de enviarlo al servidor.

- Todos los valores impresos por el programa estarán en texto sin formato, ya que el controlador descifrar de forma transparente los datos recuperados de las columnas SSN y BirthDate.

> [!NOTE]
> Las consultas pueden realizar comparaciones de igualdad en las columnas cifradas solo si el cifrado es determinista. Para obtener más información, consulte [cifrado seleccionando determinista o aleatorio](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

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

En el ejemplo siguiente se muestra la recuperación de datos binarios cifrados de las columnas cifradas. Observe lo siguiente:

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

Esta sección describen las categorías comunes de errores al consultar columnas cifradas entre las aplicaciones de ODBC y algunas instrucciones sobre cómo evitarlos.

##### <a name="unsupported-data-type-conversion-errors"></a>Errores de conversión de tipos de datos no compatibles

Always Encrypted admite algunas conversiones para los tipos de datos cifrados. Vea [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx) para obtener una lista detallada de las conversiones de tipos compatibles. Para evitar errores de conversión de tipo de datos, asegúrese de que observe los siguientes puntos al utilizar SQLBindParameter con parámetros que se dirigen a columnas cifradas:

- El tipo SQL del parámetro sea exactamente el mismo que el tipo de la columna de destino o se admite la conversión del tipo de SQL para el tipo de la columna.

- La precisión y la escala de los parámetros que tienen como destino columnas de la `decimal` y `numeric` tipos de datos de SQL Server es el mismo que la precisión y escala configurada para la columna de destino.

- La precisión de los parámetros que tienen como destino columnas de `datetime2`, `datetimeoffset`, o `time` tipos de datos de SQL Server no es mayor que la precisión de la columna de destino, en las consultas que modifican la columna de destino.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errores debidos a pasar texto sin formato en lugar de valores cifrados

Cualquier valor que tenga como destino una columna cifrada necesita cifrarse antes de enviarse al servidor. Intenta insertar, modificar o filtrar por un valor de texto simple en una columna cifrada producirá un error. Para evitar estos errores, asegúrese de:

- Always Encrypted está habilitado (en el DSN, la cadena de conexión antes conexión estableciendo la `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo de conexión para una conexión específica, o la `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo de instrucción para una instrucción concreta).

- Utilice SQLBindParameter para enviar datos dirigidos a columnas cifradas. En el ejemplo siguiente se muestra una consulta que filtra de manera incorrecta mediante un literal o constante en una columna cifrada (SSN), en lugar de pasar el literal como argumento a SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Precauciones al usar SQLSetPos y SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

El `SQLSetPos` API permite que una aplicación actualizar filas en un conjunto de resultados con búferes que se enlazaron con SQLBindCol y en qué fila de datos se ha capturado previamente. Debido al comportamiento de relleno asimétrica de tipos de longitud fija cifrados, es posible modificar inesperadamente los datos de estas columnas al realizar actualizaciones en las demás columnas de la fila. Con AE, se rellenarán los valores de caracteres de longitud fija si el valor es menor que el tamaño de búfer.

Para mitigar este comportamiento, use la `SQL_COLUMN_IGNORE` marca para omitir las columnas que no se actualizarán como parte de `SQLBulkOperations` y al usar `SQLSetPos` para cursor según las actualizaciones.  Se deben ignorar todas las columnas que no se están modificando directamente por la aplicación, tanto para el rendimiento y para evitar el truncamiento de columnas que están enlazados a un búfer *menor* que su tamaño real de (DB). Para obtener más información, consulte [referencia a la función SQLSetPos](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

Programas de aplicación pueden llamar a [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) para devolver los metadatos acerca de las columnas en instrucciones preparadas.  Cuando se habilita Always Encrypted, una llamada a `SQLMoreResults` *antes de* al llamar a `SQLDescribeCol` hace [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) para llamar, que no correctamente devuelve el texto sin formato metadatos de las columnas cifradas. Para evitar este problema, llame a `SQLDescribeCol` en instrucciones preparadas *antes de* al llamar a `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controlar el impacto de rendimiento de Always Encrypted

Como Always Encrypted es una tecnología de cifrado en el cliente, la mayor parte de la sobrecarga de rendimiento se observa en el lado de cliente, no en la base de datos. Además del costo de las operaciones de cifrado y descifrado, los otros orígenes de sobrecarga de rendimiento en el lado del cliente son:

- Ciclos de ida y vuelta adicionales a la base de datos para recuperar metadatos para los parámetros de consulta.

- Llamadas a un almacén de claves maestras de columna para tener acceso a una clave maestra de columna.

En esta sección se describe las optimizaciones de rendimiento integrados en ODBC Driver 13.1 para SQL Server y cómo se puede controlar el impacto de los dos factores anteriores en el rendimiento.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Control de ida y vuelta para recuperar los metadatos para los parámetros de consulta

Si Always Encrypted está habilitado para una conexión, ODBC Driver 13.1 para SQL Server, de forma predeterminada, llame a [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx) para cada consulta con parámetros, pasar la instrucción de consulta (sin ningún parámetro los valores) a SQL Server. Este procedimiento almacenado se analiza la instrucción de consulta para averiguar si algún parámetro necesita cifrarse y si es así, se devuelve la información relacionada con el cifrado para cada parámetro para permitir que el controlador cifrarlos. El comportamiento anterior garantiza un alto nivel de transparencia para la aplicación cliente: la aplicación (y el programador de aplicaciones) no necesitan ser consciente de las consultas que acceden a columnas cifradas, siempre y cuando se pasan los valores que se dirigen a columnas cifradas a el controlador de parámetros.

### <a name="per-statement-always-encrypted-behavior"></a>Por cada instrucción Always Encrypted comportamiento

Para controlar el impacto en el rendimiento de recuperación de metadatos de cifrado para las consultas parametrizadas, puede modificar el comportamiento de Always Encrypted para consultas individuales si se ha habilitado en la conexión. De esta manera, puede asegurarse de que `sys.sp_describe_parameter_encryption` se invoca únicamente para las consultas que sabe que tienen parámetros que se dirigen a columnas cifradas. Sin embargo, tenga en cuenta que al hacerlo, se reduce la transparencia del cifrado: si se cifran columnas adicionales en la base de datos, deberá cambiar el código de la aplicación para alinearlo con los cambios de esquema.

Para controlar el comportamiento de Always Encrypted de una instrucción, llame a SQLSetStmtAttr para establecer el `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo de instrucción a uno de los siguientes valores:

|Valor|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|Always Encrypted está deshabilitado para la instrucción|
|`SQL_CE_RESULTSETONLY` (1)|Solo el descifrado. Conjuntos de resultados y valores devueltos se descifran y parámetros no están cifrados|
|`SQL_CE_ENABLED` (3) | Always Encrypted está habilitada y usada para parámetros y resultados|

Identificadores de instrucciones nuevo creados a partir de una conexión con Always Encrypted habilitado de forma predeterminada SQL_CE_ENABLED. Esos creado a partir de una conexión con él deshabilitado de forma predeterminada SQL_CE_DISABLED (y no es posible habilitar Always Encrypted en ellos.)

Si la mayoría de las consultas de una aplicación cliente tener acceso a las columnas cifradas, se recomienda lo siguiente:

- Establecer el `ColumnEncryption` palabra clave de cadena de conexión a `Enabled`.

- Establecer el `SQL_SOPT_SS_COLUMN_ENCRYPTION` atribuir a `SQL_CE_DISABLED` en las instrucciones que no puedan acceder a ninguna columna cifrada. Esto deshabilitará ambos llamada `sys.sp_describe_parameter_encryption` , así como los intentos de descifrar cualquier valor en el resultado establecido.
    
- Establecer el `SQL_SOPT_SS_COLUMN_ENCRYPTION` atribuir a `SQL_CE_RESULTSETONLY` en las instrucciones que no tiene ningún parámetro que requiera cifrado, pero recuperen datos de las columnas cifradas. Esto deshabilitará la llamada `sys.sp_describe_parameter_encryption` y cifrado de parámetros. Los resultados que contienen columnas cifradas continuarán puede descifrar.

## <a name="always-encrypted-security-settings"></a>Cifra siempre la configuración de seguridad

### <a name="force-column-encryption"></a>Forzar el cifrado de columna

Para forzar el cifrado de un parámetro, establezca el `SQL_CA_SS_FORCE_ENCRYPT` campo descriptor de parámetro de implementación (IPD) a través de una llamada a la función SQLSetDescField. Un valor distinto de cero hace que el controlador devolver un error cuando no se devuelven metadatos de cifrado para el parámetro asociado.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Si SQL Server indica al controlador que no es necesario cifrar el parámetro, se producirá un error en las consultas que utilizan ese parámetro. Esto proporciona protección adicional contra los ataques de seguridad que implican a un servidor SQL Server comprometido que proporciona metadatos de cifrado incorrectos al cliente, que puede provocar la divulgación de datos.

### <a name="column-encryption-key-caching"></a>Almacenamiento en caché de clave de cifrado de columna

Para reducir el número de llamadas a un almacén de claves maestras de columna para descifrar las claves de cifrado de columna, el controlador almacena en caché el CEK de texto simple en la memoria. Después de recibir el ECEK de metadatos de la base de datos, primero el controlador intenta encontrar la CEK de texto simple correspondiente al valor de clave de cifrado en la memoria caché. El controlador llama al almacén de claves que contiene la CMK solo si no encuentra el CEK de texto sin formato correspondiente en la memoria caché.

> [!NOTE]
> En ODBC Driver 13.1 para SQL Server, las entradas de la memoria caché se desalojan después de un tiempo de espera de dos horas. Esto significa que para una ECEK determinada, el controlador se pone en contacto el almacén de claves sólo una vez durante la duración de la aplicación o cada dos horas, lo que sea menor.

## <a name="working-with-column-master-key-stores"></a>Trabajar con almacenes de claves maestras de columna

Para cifrar o descifrar los datos, el controlador debe obtener una CEK que está configurada para la columna de destino. Las CEK se almacenan en formato cifrado (ECEKs) en los metadatos de la base de datos. Cada CEK tiene una CMK correspondiente que se utilizó para cifrarlo. El [metadatos de base de datos](../../t-sql/statements/create-column-master-key-transact-sql.md) no almacena la CMK sí; solo contiene el nombre del almacén de claves e información que puede utilizar el almacén de claves para buscar la CMK.

Para obtener el valor de texto simple de un ECEK, el controlador obtiene los metadatos de la CEK y su correspondiente CMK en primer lugar y, a continuación, utiliza esta información para ponerse en contacto con el almacén de claves que contiene la CMK y lo solicita para descifrar el ECEK. El controlador se comunica con un almacén de claves mediante un proveedor de almacén de claves.

### <a name="built-in-keystore-providers"></a>Proveedores de almacén de claves integradas

ODBC Driver 13.1 para SQL Server incluye los siguientes proveedores de almacén de claves integradas:

| Nombre | Description | Nombre del proveedor (metadatos) |Disponibilidad|
|:---|:---|:---|:---|
|Azure Key Vault |Almacenes CMK en un almacén de claves de Azure | `AZURE_KEY_VAULT` |Windows, Mac OS, Linux|
|Almacén de certificados de Windows|Almacena CMK localmente en el almacén de claves de Windows| `MSSQL_CERTIFICATE_STORE`|Windows|

- Usted (o su DBA) debe asegurarse de que el nombre del proveedor, configurado en los metadatos de clave maestra de columna es correcto y la ruta de acceso de clave maestra de columna cumple con el formato de ruta de la clave para el proveedor en cuestión. Se recomienda que configure las claves mediante herramientas como SQL Server Management Studio, que genera automáticamente las rutas de acceso a la clave y los nombres de proveedor válidos al emitir la instrucción [CREATE COLUMN MASTER KEY](https://msdn.microsoft.com/library/mt146393.aspx) (Transact-SQL).

- Debe asegurarse de que su aplicación puede tener acceso a la clave en el almacén de claves. Esto puede conllevar la concesión de la aplicación tenga acceso a la clave o el almacén de claves, según el almacén de claves, o realizar otros pasos de configuración específicos de almacén de claves. Por ejemplo, para tener acceso a un almacén de claves de Azure, debe proporcionar las credenciales correctas para el almacén de claves.

### <a name="using-the-azure-key-vault-provider"></a>Mediante el proveedor de almacén de claves de Azure

El Almacén de claves de Azure es una opción adecuada para almacenar y administrar claves maestras de columna para Always Encrypted (especialmente si sus aplicaciones se hospedan en Azure). ODBC Driver 13.1 for SQL Server en Linux, Mac OS y Windows incluye un proveedor de almacén de claves maestras de columna integrada para el almacén de claves de Azure. Vea [almacén de claves de Azure: paso a paso](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [Introducción al almacén de claves](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), y [crear claves maestras de columna en el almacén de claves de Azure](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) para obtener más información acerca de cómo configurar una clave de Azure Almacén de Always Encrypted.

El controlador admite la autenticación en el almacén de claves de Azure mediante los siguientes tipos de credencial:

- Nombre de usuario/contraseña: con este método, las credenciales son el nombre de un usuario de Active Directory de Azure y su contraseña.

- Id. de cliente/secreto: con este método, las credenciales son un identificador de cliente de la aplicación y un secreto de aplicación.

Para permitir que el controlador debe usar CMK almacenada en claves para cifrado de columnas, utilice las siguientes palabras clave de cadena de conexión solo:

|Tipo de credencial| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Nombre de usuario/contraseña| `KeyVaultPassword`|Nombre Principal de usuario|Contraseña|
|Id. de cliente/secreto| `KeyVaultClientSecret`|Id. de cliente|Secreto|

#### <a name="example-connection-strings"></a>Cadenas de conexión de ejemplo

Las cadenas de conexión siguientes muestran cómo autenticar al almacén de claves de Azure con los dos tipos de credencial:

**ClientID/secreto**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Nombre de usuario/contraseña**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Ningún otro cambio de aplicación de ODBC es necesarios para usar claves para el almacenamiento CMK.

### <a name="using-the-windows-certificate-store-provider"></a>Mediante el proveedor de almacén de certificados de Windows

ODBC Driver 13.1 for SQL Server en Windows incluye un proveedor de almacén de claves maestras de columna integrada para el almacén de certificados de Windows, denominado `MSSQL_CERTIFICATE_STORE`. (Este proveedor no está disponible en Mac OS o Linux). Con este proveedor, la CMK se almacena localmente en el equipo cliente y no es necesaria para usar con el controlador ninguna configuración adicional por la aplicación. Sin embargo, la aplicación debe tener acceso al certificado y su clave privada en el almacén. Vea [Create and Store Column Master Keys (Always Encrypted)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted) para obtener más información.

### <a name="using-custom-keystore-providers"></a>Usar proveedores de almacén de claves personalizados

ODBC Driver 13.1 para SQL Server también admite los proveedores de almacén de claves personalizados de terceros mediante la interfaz CEKeystoreProvider. Esto permite que una aplicación cargar la consulta y configurar los proveedores de almacén de claves de modo que pueden ser usados por el controlador para tener acceso a las columnas cifradas. Las aplicaciones pueden interactuar directamente con un proveedor de almacén de claves con el fin de cifrar las CEK para su almacenamiento en SQL Server y realizar tareas más allá de tener acceso a las columnas cifradas con ODBC; Para obtener más información, consulte [proveedores de almacén de claves personalizados](../../connect/odbc/custom-keystore-providers.md).

Dos atributos de conexión se utilizan para interactuar con proveedores de almacén de claves personalizados. Estas sobrecargas son:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

El primero se usa para cargar y enumerar los proveedores de almacén de claves cargado, mientras que el segundo permite la comunicación de proveedor de la aplicación. Estos atributos de conexión pueden utilizarse en cualquier momento, antes o después de establecer una conexión, puesto que la interacción con el proveedor de la aplicación no requiere comunicación con SQL Server. Sin embargo, porque todavía no ha cargado el controlador, establecer y obtener estos atributos antes de conectar hará que se procesan mediante el Administrador de controladores y no, pueden obtener los resultados esperados.

#### <a name="loading-a-keystore-provider"></a>Cargar un proveedor de almacén de claves

Establecer el `SQL_COPT_SS_CEKEYSTOREPROVIDER` atributo de conexión permite a una aplicación cliente para cargar una biblioteca de proveedor, pasa a estar disponible para su uso los proveedores de almacén de claves contenidos en ella.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde todos los demás en el mismo proceso.|
|`Attribute`|[Entrada] Atributo que se establecerá: el `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Entrada] Puntero a una cadena de caracteres terminadas en null que especifica el nombre de archivo de la biblioteca del proveedor. Para SQLSetConnectAttrA, se trata de una cadena (multibyte) de ANSI. Para SQLSetConnectAttrW, se trata de una cadena Unicode (wchar_t).|
|`StringLength`|[Entrada] La longitud de la cadena de ValuePtr o SQL_NTS.|

El controlador intenta cargar la biblioteca identificada por el parámetro ValuePtr mediante la biblioteca dinámica definido por la plataforma carga mecanismo (`dlopen()` en Linux y macOS, `LoadLibrary()` en Windows), y agrega los proveedores definidos en ellas a la lista de proveedores de sabe que el controlador. Pueden producirse los siguientes errores:

| Error | Description |
|:--|:--|
|`CE203`|No se pudo cargar la biblioteca dinámica.|
|`CE203`|No se encontró el símbolo "CEKeyStoreProvider" Exportar en la biblioteca.|
|`CE203`|Uno o varios proveedores en la biblioteca ya están cargados.|

`SQLSetConnectAttr`Devuelve el error habitual o valores correctos e información adicional está disponible para los errores que se ha producido a través del mecanismo de diagnóstico estándar de ODBC.

> [!NOTE]
> El programador de la aplicación debe asegurarse de que los proveedores personalizados se cargan antes de enviar cualquier consulta que se les solicita a través de las conexiones. Si no se hace así, se producirá el error:

| Error | Description |
|:--|:--|
|`CE200`|Proveedor de almacén de claves %1 que no se encuentra. Asegúrese de que se ha cargado la biblioteca del proveedor de almacén de claves adecuado.|

> [!NOTE]
> Los implementadores de proveedor de almacén de claves deben evitar el uso de `MSSQL` en el nombre de sus proveedores personalizados. Este término se reserva exclusivamente para uso de Microsoft y puede provocar conflictos con futuras proveedores integrados. Usar este término en el nombre de un proveedor personalizado puede dar lugar a una advertencia de ODBC.

#### <a name="getting-the-list-of-loaded-providers"></a>Obtener la lista de proveedores cargados

Obtener el atributo de conexión permite a una aplicación de cliente determinar los proveedores de almacén de claves cargados actualmente en el controlador (incluidos los integrados). Solo puede realizarse después de conectarse.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde todos los demás en el mismo proceso.|
|`Attribute`|[Entrada] Atributo para recuperar: el `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Salida] Un puntero a la memoria en el que se va a devolver el siguiente nombre de proveedor cargado.|
|`BufferLength`|[Entrada] La longitud del búfer ValuePtr.|
|`StringLengthPtr`|[Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (sin incluir el carácter de terminación null) disponible para devolver en \*ValuePtr. Si ValuePtr es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponible para devolver es mayor que BufferLength menos la longitud de la terminación null de caracteres, los datos de \*ValuePtr se trunca a BufferLength menos la longitud de la carácter de terminación NULL y termina en null el controlador.|

Para permitir la recuperación de la lista completa, cada operación Get devuelve el nombre del proveedor actual e incrementa un contador interno a la siguiente. Una vez que este contador llega al final de la lista, una cadena vacía ("") se devuelve, y se restablece el contador; operaciones Get sucesivas, continúe nuevo desde el principio de la lista.

### <a name="communicating-with-keystore-providers"></a>Comunicación con proveedores de almacén de claves

El `SQL_COPT_SS_CEKEYSTOREDATA` atributo de conexión permite a una aplicación de cliente para comunicarse con los proveedores de almacén de claves cargado para configurar parámetros adicionales, incrustación de material, etcetera. La comunicación entre una aplicación cliente y un proveedor sigue un protocolo simple de solicitud-respuesta, en función de Get y Set solicita mediante el atributo de conexión. Se inicia la comunicación solo por la aplicación cliente.

> [!NOTE]
> Debido a la naturaleza de ODBC llama responden del CEKeyStoreProvider a (SQLGet/SetConnectAttr), ODBC admite la interfaz sola establecer datos en la resolución del contexto de conexión.

La aplicación se comunica con los proveedores de almacén de claves mediante el controlador a través de la estructura de CEKeystoreData:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| Argumento | Description |
|:---|:---|
|`name`|[Entrada] En conjunto, el nombre del proveedor al que se envían los datos. Se omite en Get. Cadena terminada en null, en caracteres anchos.|
|`dataSize`|[Entrada] El tamaño de la matriz de datos después de la estructura.|
|`data`|[Entrada] En conjunto, los datos que se enviarán al proveedor. Esto puede ser datos arbitrarios; el controlador no realizará ningún intento para interpretarlo. En Get, leer el búfer para recibir los datos del proveedor.|

#### <a name="writing-data-to-a-provider"></a>Escribir datos en un proveedor

A `SQLSetConnectAttr` llama mediante el `SQL_COPT_SS_CEKEYSTOREDATA` atributo escribe un "paquete" de datos en el proveedor de almacén de claves especificado.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`| [Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde todos los demás en el mismo proceso.|
|`Attribute`|[Entrada] Atributo que se establecerá: el `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Entrada] Puntero a una estructura CEKeystoreData. El campo de nombre de la estructura identifica el proveedor para el que los datos se usan.|
|`StringLength`|[Entrada] Constante SQL_IS_POINTER|

Información adicional detallada del error puede obtenerse a través de [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> El proveedor puede utilizar el identificador de conexión para asociar los datos escritos en una conexión específica, si lo desea. Esto es útil para implementar la configuración de cada conexión. También puede pasar por alto el contexto de conexión y tratar los datos de forma idéntica independientemente de la conexión usada para enviar los datos. Vea [asociación contexto](../../connect/odbc/custom-keystore-providers.md#context-association) para obtener más información.

#### <a name="reading-data-from-a-provider"></a>Leer datos de un proveedor

Una llamada a `SQLGetConnectAttr` mediante la `SQL_COPT_SS_CEKEYSTOREDATA` atributo lee un "paquete" de datos de *el último-escrito-to* proveedor. Si no hay ninguno, se produce un Error de secuencia de función. Los implementadores de proveedor de almacén de claves se recomienda para admitir "ficticia escribe" de 0 bytes como una manera de seleccionar el proveedor para las operaciones de lectura sin provocar otros efectos secundarios, si tiene sentido hacerlo.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexión. Debe ser un identificador de conexión válida, pero los proveedores de carga mediante el identificador de una conexión son accesibles desde todos los demás en el mismo proceso.|
|`Attribute`|[Entrada] Atributo para recuperar: el `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Salida] Un puntero a una estructura de CEKeystoreData en la que se colocan los datos leídos desde el proveedor.|
|`BufferLength`|[Entrada] Constante SQL_IS_POINTER|
|`StringLengthPtr`|[Salida] Un puntero a un búfer en el que se va a devolver BufferLength. Si * ValuePtr no es un puntero nulo, se devuelve ninguna longitud.|

El llamador debe asegurarse de que se asigna un búfer de longitud suficiente siguiendo la estructura CEKEYSTOREDATA para que el proveedor escribir en. Tras la devolución, su campo dataSize se actualiza con la longitud real de los datos leídos desde el proveedor. Información adicional detallada del error puede obtenerse a través de [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Esta interfaz no impone ningún requisito adicional sobre el formato de datos que se transfieren entre una aplicación y un proveedor de almacén de claves. Cada proveedor pueden definir su propio formato de protocolo o datos, dependiendo de sus necesidades.

Para obtener un ejemplo de la implementación de su propio proveedor de almacén de claves, consulte [proveedores de almacén de claves personalizados](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Limitaciones del controlador ODBC cuando se usa Always Encrypted

### <a name="bulk-copy-function-usage"></a>Uso de funciones de copia masiva
El uso de la [funciones de copia masiva de SQL](https://msdn.microsoft.com/library/ms130792.aspx) no se admite cuando se usa el controlador ODBC con Always Encrypted. No se producirá ningún cifrado/descifrado transparente en las columnas cifradas que se usan con las funciones de copia masiva de SQL.

### <a name="asynchronous-operations"></a>Operaciones asincrónicas
Mientras que el controlador ODBC permitirá el uso de [operaciones asincrónicas](https://msdn.microsoft.com/library/ms131658.aspx) con Always Encrypted, hay un impacto en el rendimiento en las operaciones cuando se habilita Always Encrypted. La llamada a `sys.sp_describe_parameter_encryption` para determinar los metadatos de cifrado para la instrucción está bloqueando y hará que el controlador de espera para que el servidor devolver los metadatos antes de devolver `SQL_STILL_EXECUTING`.

## <a name="always-encrypted-api-summary"></a>Resumen de la API de Always Encrypted

### <a name="connection-string-keywords"></a>Palabras clave de cadena de conexión

|Nombre|Description|  
|----------|-----------------|  
|`ColumnEncryption`|Valores aceptados son `Enabled` / `Disabled`.<br>`Enabled`--habilita la funcionalidad de Always Encrypted para la conexión.<br>`Disabled`--deshabilitar la funcionalidad de Always Encrypted para la conexión. <br><br>El valor predeterminado es `Disabled`.|  
|`KeyStoreAuthentication` | Valores válidos: `KeyVaultPassword`,`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Cuando `KeyStoreAuthentication`  =  `KeyVaultPassword`, establezca este valor en un nombre Principal de usuario de Active Directory de Azure válido. <br>Cuando `KeyStoreAuthetication`  =  `KeyVaultClientSecret` establezca este valor en un Azure Active Directory aplicación cliente identificador válido |
|`KeyStoreSecret` | Cuando `KeyStoreAuthentication`  =  `KeyVaultPassword` establezca este valor en la contraseña para el nombre de usuario correspondiente. <br>Cuando `KeyStoreAuthentication`  =  `KeyVaultClientSecret` establezca este valor en el secreto de aplicación asociados con un Azure Active Directory aplicación cliente identificador válido|

### <a name="connection-attributes"></a>Atributos de conexión

|Nombre|Tipo|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Antes de conectar|`SQL_COLUMN_ENCRYPTION_DISABLE`(0): deshabilitar Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE`(1): habilitar Always Encrypted|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Después de conectar|[Establecido] Intente cargar CEKeystoreProvider<br>[Obtener] Devuelve un nombre de CEKeystoreProvider|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Después de conectar|[Establecido] Escribir datos en CEKeystoreProvider<br>[Obtener] Leer datos de CEKeystoreProvider|

### <a name="statement-attributes"></a>Atributos de instrucción

|Nombre|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED`(0): always Encrypted está deshabilitado para la instrucción <br>`SQL_CE_RESULTSETONLY`(1): solo el descifrado. Conjuntos de resultados y valores devueltos se descifran y parámetros no están cifrados <br>`SQL_CE_ENABLED`(3): always Encrypted está habilitado y usada para parámetros y resultados|

### <a name="descriptor-fields"></a>Campos de descriptor

|Campo IPD|Tipo de tamaño /|Valor predeterminado|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 bytes)|0|Cuando 0 (valor predeterminado): decisión para cifrar este parámetro está determinado por la disponibilidad de los metadatos de cifrado.<br><br>Si es distinto de cero: si hay metadatos de cifrado para este parámetro, se cifra. En caso contrario, produce un error en la solicitud con error [CE300] cifrado obligatorio [Microsoft] [ODBC Driver 13 for SQL Server] se especificó para un parámetro pero no hay metadatos de cifrado se proporcionan el servidor.|

## <a name="see-also"></a>Vea también

- [Always Encrypted (motor de base de datos)](https://msdn.microsoft.com/library/mt163865.aspx)
- [Blog de Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)


