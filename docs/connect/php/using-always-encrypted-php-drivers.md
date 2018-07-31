---
title: Uso de Always Encrypted con los controladores PHP para SQL Server | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 12f0427b4ff23452f244c830c9116913dfb03968
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174972"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>Uso de Always Encrypted con los controladores PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>Aplicable a
 -   Controladores de Microsoft 5.2 para PHP para SQL Server
 
## <a name="introduction"></a>Introducción

Este artículo proporciona información sobre cómo desarrollar aplicaciones de PHP con [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y [PHP Driver for SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md).

Always Encrypted permite a las aplicaciones cliente cifrar la información confidencial y nunca revelar los datos ni las claves de cifrado en SQL Server o Azure SQL Database. Un Always Encrypted habilitado el controlador, como ODBC Driver for SQL Server, de forma transparente cifra y descifra los datos confidenciales en la aplicación cliente. El controlador determina automáticamente qué parámetros de consulta corresponden a columnas de bases de datos confidenciales (protegidas mediante Always Encrypted) y cifra los valores de esos parámetros antes de pasar los datos a SQL Server o Azure SQL Database. De forma similar, el controlador descifra de manera transparente los datos que se han recuperado de las columnas de bases de datos cifradas de los resultados de la consulta. Para obtener más información, vea [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Los controladores de PHP para SQL Server usan el controlador ODBC para SQL Server cifrar datos confidenciales.

## <a name="prerequisites"></a>Prerequisites

 -   Configure Always Encrypted en su base de datos. Esta configuración implica el aprovisionamiento de las claves Always Encrypted y la configuración del cifrado para las columnas de las bases de datos seleccionadas. Si todavía no tiene una base de datos configurada con Always Encrypted, siga las instrucciones de [Introducción a Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). En concreto, la base de datos debe contener las definiciones de metadatos para una clave maestra de columna (CMK), una clave de cifrado de columna (CEK) y una tabla que contiene una o varias columnas cifradas mediante ese CEK.
 -   Asegúrese de que el controlador ODBC para SQL Server versión 17 o posterior está instalado en el equipo de desarrollo. Para obtener más información, consulte [ODBC Driver para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="enabling-always-encrypted-in-a-php-application"></a>Habilitar Always Encrypted en una aplicación PHP

Establecer el valor de la palabra clave de cadena de conexión `ColumnEncryption` en `Enabled` es la manera más sencilla de habilitar el cifrado de parámetros que tienen como destino las columnas cifradas y el descifrado de los resultados de la consulta. Los siguientes son ejemplos de la habilitación de Always Encrypted en los controladores de SQLSRV y PDO_SQLSRV:

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

Habilitar Always Encrypted no es suficiente para el cifrado o descifrado se realice correctamente; También deberá asegurarse de que:
 -   La aplicación tiene los permisos de base de datos VIEW ANY COLUMN MASTER KEY DEFINITION y VIEW ANY COLUMN ENCRYPTION KEY DEFINITION, que se requieren para tener acceso a los metadatos sobre las claves Always Encrypted de la base de datos. Para obtener más información, consulte [permiso de base de datos](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
 -   La aplicación puede tener acceso a la CMK que protege el CEK para las columnas cifradas consultadas. Este requisito depende de que el proveedor de almacén de claves que almacena la CMK. Para obtener más información, consulte [trabajar con almacenes de claves maestras de columna](#working-with-column-master-key-stores).

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperar y modificar los datos de las columnas cifradas

Una vez que habilite Always Encrypted en una conexión, puede usar las API de SQLSRV estándar (consulte [referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)) o las API PDO_SQLSRV (consulte [referencia de API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)) para recuperar o modificar datos en las columnas de la base de datos cifrada. Suponiendo que la aplicación tiene los permisos de base de datos necesarios y puede tener acceso a la clave maestra de columna, el controlador cifra los parámetros de consulta que como destino las columnas cifradas y descifrar los datos recuperados de columnas cifradas, que se comporta de forma transparente a la aplicación como si no se cifran las columnas.

Si Always Encrypted no está habilitado, se produce un error en las consultas con parámetros que tengan como destino las columnas cifradas. Las datos todavía se pueden recuperar de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas. Sin embargo, el controlador no intenta realizar cualquier descifrado y la aplicación recibe los datos binarios cifrados (como matrices de bytes).

En la tabla siguiente se resume el comportamiento de las consultas, dependiendo de si Always Encrypted está habilitado o no:

|Característica de las consultas|Always Encrypted está habilitado y la aplicación puede tener acceso a las claves y a los metadatos de clave|Always Encrypted está habilitado y la aplicación no puede tener acceso a las claves ni a los metadatos de clave|Always Encrypted está deshabilitado|
|---|---|---|---|
|Parámetros que se dirigen a columnas cifradas.|Los valores de parámetro se cifran de manera transparente.|Error|Error|
|Recuperación de datos de las columnas cifradas, sin parámetros que tengan como destino las columnas cifradas.|Los resultados de las columnas cifradas se descifran de manera transparente. La aplicación recibe valores de columna de texto simple. |Error|Los resultados de las columnas cifradas no se descifran. La aplicación recibe valores cifrados como matrices de bytes.|
 
En el siguiente ejemplo se ilustra la recuperación y la modificación de datos en las columnas cifradas. Los ejemplos supone una tabla con el siguiente esquema. Las columnas SSN y BirthDate están cifradas.
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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>Ejemplo de inserción de datos

Los ejemplos siguientes muestran cómo usar los controladores de SQLSRV y PDO_SQLSRV para insertar una fila en la tabla paciente. Tenga en cuenta lo siguiente:
 -   No existe nada específico al cifrado en el código de ejemplo. El controlador detecta automáticamente y cifra los valores de los parámetros de SSN y BirthDate, que se dirigen a columnas cifradas. Este mecanismo hace que el cifrado se realice de manera transparente en la aplicación.
 -   Los valores que se insertan en las columnas de bases de datos, incluidas las columnas cifradas, se pasan como parámetros enlazados. Aunque el uso de parámetros es opcional al enviar valores a las columnas no cifradas (aunque es altamente recomendable porque ayuda a evitar la inyección de código SQL), es necesario para los valores que tienen como destino las columnas cifradas. Si los valores insertados en las columnas SSN o BirthDate se pasan como literales incrustados en la instrucción de consulta, la consulta produciría un error porque el controlador no intenta cifrar o procesar de otro modo, los literales en consultas. Como resultado, el servidor los rechazará considerándolos incompatibles con las columnas cifradas.
 -   Cuando se insertan valores con parámetros de enlace, se debe pasar un tipo SQL que es idéntico al tipo de datos de la columna de destino o cuya conversión al tipo de datos de la columna de destino es compatible para la base de datos. Este requisito es porque Always Encrypted admite algunas conversiones de tipo (para obtener más información, consulte [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). Los dos controladores PHP de SQLSRV y PDO_SQLSRV, cada uno tiene un mecanismo para ayudar al usuario determinar el tipo SQL del valor. Por lo tanto, el usuario no tiene que proporcionar explícitamente el tipo de SQL.
  -   Para el controlador SQLSRV, el usuario tiene dos opciones:
   -   Se basan en el controlador PHP para determinar y establecer el tipo correcto de SQL. En este caso, el usuario debe usar `sqlsrv_prepare` y `sqlsrv_execute` para ejecutar una consulta con parámetros.
   -   Establecer explícitamente el tipo SQL.
  -   Para el controlador PDO_SQLSRV, el usuario no tiene la opción para establecer explícitamente el tipo SQL de un parámetro. El controlador PDO_SQLSRV automáticamente ayuda al usuario determinar el tipo SQL al enlazar un parámetro.
 -   Para que los controladores determinar el tipo SQL, se aplican algunas limitaciones:
  -   Controlador SQLSRV:
   -   Si el usuario desea que el controlador para determinar los tipos SQL para las columnas cifradas, el usuario debe usar `sqlsrv_prepare` y `sqlsrv_execute`.
   -   Si `sqlsrv_query` es preferido, el usuario es responsable de especificar los tipos de SQL para todos los parámetros. El tipo SQL especificado debe incluir la longitud de cadena para tipos de cadena y la escala y precisión de los tipos decimal.
  -   Controlador PDO_SQLSRV:
   -   El atributo de instrucción `PDO::SQLSRV_ATTR_DIRECT_QUERY` no se admite en una consulta parametrizada.
   -   El atributo de instrucción `PDO::ATTR_EMULATE_PREPARES` no se admite en una consulta parametrizada.
   
Controlador SQLSRV y [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

Controlador SQLSRV y [sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

Controlador PDO_SQLSRV y [PDO:: Prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>Ejemplo de recuperación de datos de texto simple

Los ejemplos siguientes muestran datos filtrados según valores cifrados y la recuperación de datos de texto simple de las columnas cifradas con los controladores de SQLSRV y PDO_SQLSRV. Tenga en cuenta lo siguiente:
 -   El valor utilizado en la cláusula WHERE para filtrar según la columna SSN necesita pasarse mediante el parámetro de enlace, por lo que el controlador puede cifrarlo de manera transparente antes de enviarlo al servidor.
 -   Al ejecutar una consulta con parámetros enlazados, los controladores PHP determina automáticamente el tipo SQL para el usuario a menos que el usuario especifica explícitamente el tipo SQL al usar el controlador SQLSRV.
 -   Todos los valores impresos por el programa están en texto sin formato, ya que el controlador descifra de forma transparente los datos recuperados de las columnas SSN y BirthDate.
 
Nota: Las consultas pueden realizar comparaciones de igualdad en las columnas cifradas solo si el cifrado es determinista. Para obtener más información, vea la sección [Selección del cifrado determinista o aleatorio](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>Ejemplo de recuperación de datos de texto cifrado

Si Always Encrypted no está habilitado, una consulta todavía puede recuperar datos de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas.

Los ejemplos siguientes ilustran recuperar datos binarios cifrados de las columnas cifradas con los controladores de SQLSRV y PDO_SQLSRV. Tenga en cuenta lo siguiente:
 -   Como Always Encrypted no está habilitado en la cadena de conexión, la consulta devuelve valores cifrados de SSN y BirthDate como matrices de bytes (el programa convierte los valores en cadenas).
 -   Una consulta que recupera datos de columnas cifradas con Always Encrypted deshabilitado puede tener parámetros, siempre y cuando ninguno de ellos tenga como destino una columna cifrada. La siguiente consulta filtra por LastName, que no está cifrado en la base de datos. Si la consulta filtra por SSN o BirthDate, esta producirá un error.
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitar problemas comunes al consultar columnas cifradas

En esta sección se describen las categorías comunes de errores al consultar columnas cifradas de aplicaciones PHP y algunas instrucciones sobre cómo evitarlos.

#### <a name="unsupported-data-type-conversion-errors"></a>Errores de conversión de tipos de datos no compatibles

Always Encrypted admite algunas conversiones para los tipos de datos cifrados. Vea [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obtener una lista detallada de las conversiones de tipos compatibles. Para evitar los errores de conversión de tipo de datos, haga lo siguiente:
 -   Cuando se usa el controlador SQLSRV con `sqlsrv_prepare` y `sqlsrv_execute` se determina automáticamente el tipo SQL, junto con el tamaño de columna y el número de dígitos decimales del parámetro.
 -   Cuando se usa el controlador PDO_SQLSRV para ejecutar una consulta, automáticamente se determina el tipo SQL con el tamaño de columna y el número de dígitos decimales del parámetro
 -   Cuando se usa el controlador SQLSRV con `sqlsrv_query` para ejecutar una consulta:
  -   El tipo SQL del parámetro o es exactamente el mismo que el tipo de la columna de destino o se admite la conversión de tipo SQL al tipo de la columna.
  -   La precisión y la escala de los parámetros que tienen como destino columnas de los tipos de datos `decimal` y `numeric` de SQL Server debe ser la misma que la precisión y la escala configurada para la columna de destino.
  -   La precisión de los parámetros que tienen como destino las columnas de tipos de datos `datetime2`, `datetimeoffset` o `time` de SQL Server no debe ser superior a la precisión de la columna de destino, en las consultas que modifiquen la columna de destino.
 -   No utilice los atributos de instrucción PDO_SQLSRV `PDO::SQLSRV_ATTR_DIRECT_QUERY` o `PDO::ATTR_EMULATE_PREPARES` en una consulta parametrizada
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errores debidos a pasar texto sin formato en lugar de valores cifrados

Cualquier valor que tenga como destino una columna cifrada necesita cifrarse antes de enviarse al servidor. Un intento para insertar, modificar o filtrar por un valor de texto simple en el resultado de un error en una columna cifrada. Para evitar dichos errores, asegúrese de que:
 -   Always Encrypted esté habilitado (en la cadena de conexión, establezca el `ColumnEncryption` palabra clave para `Enabled`).
 -   Usa un parámetro de enlace para enviar datos que tengan como destino las columnas cifradas. El ejemplo siguiente muestra una consulta que filtra de manera incorrecta mediante un literal o constante en una columna cifrada (SSN):
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Controlar el impacto en el rendimiento de Always Encrypted

Como Always Encrypted es una tecnología de cifrado del lado cliente, la mayoría de las sobrecargas de rendimiento se observan en el lado cliente y no en la base de datos. Además del costo de las operaciones de cifrado y descifrado, los demás orígenes de las sobrecargas de rendimiento en el lado cliente son:
 -   Ciclos de ida y vuelta adicionales a la base de datos para recuperar metadatos para los parámetros de consulta.
 -   Llamadas a un almacén de claves maestras de columna para tener acceso a una clave maestra de columna.
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>Ciclos de ida y vuelta para recuperar metadatos para los parámetros de consulta

De forma predeterminada, si Always Encrypted está habilitado para una conexión, ODBC Driver llamará a [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta con parámetros, al pasar la instrucción de consulta (sin ningún valor de parámetro) a SQL Server. Este procedimiento almacenado analiza la instrucción de consulta para averiguar si algún parámetro necesita cifrarse y, si es así, se devuelve la información relacionada con el cifrado para cada parámetro permitir que el controlador cifrarlos.

Puesto que los controladores PHP permiten al usuario enlazar un parámetro en una instrucción preparada sin proporcionar el código SQL, escriba, al enlazar un parámetro en una conexión habilitado para Always Encrypted, llame los controladores de PHP [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) en el parámetro para obtener el tipo SQL, el tamaño de columna y dígitos decimales. Los metadatos, a continuación, se usan para llamar a [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md). Estos adicional `SQLDescribeParam` llamadas no requieren de ida y vuelta adicional a la base de datos como el controlador ODBC ya ha almacenado la información del cliente cuando `sys.sp_describe_parameter_encryption` llamó.

Los comportamientos anteriores garantizan un alto nivel de transparencia para la aplicación cliente (y el desarrollador de aplicaciones) no necesita tener en cuenta qué consultas acceden a las columnas cifradas, siempre y cuando los valores que se dirigen a columnas cifradas se pasan al controlador en parámetros.

A diferencia de ODBC Driver for SQL Server, habilitar Always Encrypted en el nivel de instrucción o consulta no todavía admite los controladores PHP. 

### <a name="column-encryption-key-caching"></a>Almacenamiento en memoria caché de claves de cifrado de columnas

Para reducir el número de llamadas a un almacén de claves maestras de columna para descifrar las claves de cifrado de columna (CEK), el controlador almacena en caché el CEK de texto simple en la memoria. Después de recibir la CEK cifrada (ECEK) de metadatos de la base de datos, en primer lugar el controlador ODBC intenta encontrar la CEK de texto simple correspondiente al valor de clave cifrado en la memoria caché. El controlador llama al almacén de claves que contiene la CMK solo si no encuentra el CEK de texto sin formato correspondiente en la memoria caché.

Nota: En el controlador ODBC para SQL Server, las entradas de la memoria caché se expulsan después de un tiempo de espera de dos horas. Este comportamiento significa que para un determinado ECEK, el controlador se pone en contacto el almacén de claves solo una vez durante la vigencia de la aplicación o cada dos horas, lo que sea menor.

## <a name="working-with-column-master-key-stores"></a>Trabajar con almacenes de claves maestras de columna

Para cifrar o descifrar los datos, el controlador necesita obtener una CEK que esté configurada para la columna de destino. Las CEK se almacenan en formato cifrado (ECEKs) en los metadatos de la base de datos. Cada CEK tiene una CMK correspondiente que se usó para cifrarlo. El [los metadatos de la base de datos](../../t-sql/statements/create-column-master-key-transact-sql.md) no almacena la CMK sí; solo contiene el nombre del almacén de claves e información que puede usar el almacén de claves para buscar la CMK.

Para obtener el valor de texto simple de un ECEK, el controlador obtiene los metadatos acerca de la CEK y su CMK correspondiente y, a continuación, usa esta información para ponerse en contacto con el almacén de claves que contiene la CMK y lo solicita descifrar ECEK. El controlador se comunica con un almacén de claves mediante un proveedor de almacén de claves.

Microsoft Driver 5.3.0 para PHP para SQL Server, se admiten sólo Windows Certificate Store Provider y Azure Key Vault. Aún no se admite el otro proveedor de almacén de claves compatibles con el controlador ODBC (proveedor de almacén de claves personalizado).

### <a name="using-the-windows-certificate-store-provider"></a>Mediante el proveedor de Windows Certificate Store

El controlador ODBC para SQL Server en Windows incluye un proveedor de almacén de claves maestras de columna integrada para el Store de certificados de Windows denominado `MSSQL_CERTIFICATE_STORE`. (Este proveedor no está disponible en macOS o Linux). Con este proveedor, la CMK se almacena localmente en el equipo cliente y no es necesaria para usarlo con el controlador de ninguna configuración adicional por parte de la aplicación. Sin embargo, la aplicación debe tener acceso al certificado y su clave privada en el almacén. Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

### <a name="using-azure-key-vault"></a>Con Azure Key Vault

Azure Key Vault ofrece una forma de almacenar las claves de cifrado, contraseñas y otros secretos con Azure y puede usarse para almacenar las claves de Always Encrypted. El controlador ODBC para SQL Server (versión 17 y versiones posterior) incluye un proveedor de almacén de claves maestra integrado para Azure Key Vault. Las siguientes opciones de conexión controlan la configuración de Azure Key Vault: `KeyStoreAuthentication`, `KeyStorePrincipalId`, y `KeyStoreSecret`. 
 -   `KeyStoreAuthentication` puede tomar uno de dos posibles valores de cadena: `KeyVaultPassword` y `KeyVaultClientSecret`. Estos valores controlan qué tipo de credenciales de autenticación se utilizan con las otras dos palabras clave.
 -   `KeyStorePrincipalId` toma una cadena que representa un identificador de la cuenta que buscan tener acceso a Azure Key Vault. 
     -   Si `KeyStoreAuthentication` está establecido en `KeyVaultPassword`, a continuación, `KeyStorePrincipalId` debe ser el nombre de un usuario de Azure Active Directory.
     -   Si `KeyStoreAuthentication` está establecido en `KeyVaultClientSecret`, a continuación, `KeyStorePrincipalId` debe ser un identificador de aplicación cliente.
 -   `KeyStoreSecret` toma una cadena que representa un secreto de credencial. 
     -   Si `KeyStoreAuthentication` está establecido en `KeyVaultPassword`, a continuación, `KeyStoreSecret` debe ser la contraseña del usuario. 
     -   Si `KeyStoreAuthentication` está establecido en `KeyVaultClientSecret`, a continuación, `KeyStoreSecret` debe ser el secreto de aplicación asociado con el identificador de aplicación cliente.

Las tres opciones deben estar presentes en la cadena de conexión para usar Azure Key Vault. Además, `ColumnEncryption` debe establecerse en `Enabled`. Si `ColumnEncryption` está establecido en `Disabled` pero están presentes las opciones de Azure Key Vault, la secuencia de comandos continuará sin errores, pero no se realizará cifrado.

Los ejemplos siguientes muestran cómo conectarse a SQL Server con Azure Key Vault.

SQLSRV:

Con una cuenta de Azure Active Directory:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreAuthentication"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Uso de un identificador de cliente de aplicación de Azure y un secreto:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreAuthentication"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV: Uso de una cuenta de Azure Active Directory:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreAuthentication = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Uso de un identificador de cliente de aplicación de Azure y un secreto:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreAuthentication = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Limitaciones de los controladores PHP cuando se usa Always Encrypted

SQLSRV y PDO_SQLSRV:
 -   Linux y macOS no admiten Windows Certificate Store Provider
 -   Forzar el cifrado de parámetros
 -   Habilitar Always Encrypted en el nivel de instrucción 
 -   Al utilizar los escenarios de característica y que no sean UTF8 Always Encrypted en Linux y macOS (por ejemplo, "en_US. ISO-8859-1 "), insertar datos null o una cadena vacía en una columna char cifrada puede no funcionar a menos que la página de códigos 1252 se ha instalado en el sistema
 
Solo SQLSRV:
 -   Uso de `sqlsrv_query` para el parámetro de enlace sin especificar el tipo de SQL
 -   Uso de `sqlsrv_prepare` para enlazar parámetros en un lote de instrucciones SQL  
 
Sólo PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` atributo de instrucción especificado en una consulta parametrizada
 -   `PDO::ATTR_EMULATE_PREPARE` atributo de instrucción especificado en una consulta parametrizada
 -   enlace de parámetros en un lote de instrucciones SQL
 
Los controladores PHP también heredan las limitaciones impuestas por el controlador ODBC para SQL Server y la base de datos. Consulte [limitaciones del controlador ODBC cuando se usa Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) y [siempre cifrados detalles de la característica](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details).  
  
## <a name="see-also"></a>Ver también  
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referencia de API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
