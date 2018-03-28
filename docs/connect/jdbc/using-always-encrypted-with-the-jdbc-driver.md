---
title: Con Always Encrypted con el controlador JDBC | Documentos de Microsoft
ms.custom: ''
ms.date: 3/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 425f965c37e1d148a267566bd1980eb345cadfc6
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Uso de Always Encrypted con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Esta página proporciona información sobre cómo desarrollar aplicaciones de Java mediante [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y Microsoft JDBC Driver 6.0 (o posterior) para SQL Server.

Always Encrypted permite a los clientes cifrar información confidencial y nunca revelar los datos o las claves de cifrado en SQL Server o base de datos de SQL Azure. Un Always Encrypted habilitado controlador, por ejemplo, Microsoft JDBC Driver 6.0 (o superior) para SQL Server, se logra este comportamiento al cifrar y descifrar datos confidenciales en la aplicación cliente de forma transparente. El controlador determina automáticamente qué consulta parámetros corresponden a las columnas de base de datos de Always Encrypted y cifra los valores de esos parámetros antes de que envía a SQL Server o base de datos de SQL Azure. De forma similar, el controlador descifra de manera transparente los datos que se han recuperado de las columnas de bases de datos cifradas de los resultados de la consulta. Para obtener más información, consulte [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Requisitos previos
- Asegúrese de que Microsoft JDBC Driver 6.0 (o posterior) para SQL Server está instalado en el equipo de desarrollo. 
- Descargue e instale los archivos de Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy.  Asegúrese de leer el archivo Léame incluido en el archivo zip para obtener instrucciones de instalación y detalles pertinentes sobre problemas de exportación/importación posibles.  

    - Si usa el mssql-jdbc-X.X.X.jre7.jar o sqljdbc41.jar, los archivos de directivas pueden descargarse desde [descargarán archivos de directiva de Java Cryptography Extension (JCE) Unlimited intensidad jurisdicción 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Si usa el mssql-jdbc-X.X.X.jre8.jar o sqljdbc42.jar, los archivos de directivas pueden descargarse desde [descargarán archivos de directiva de Java Cryptography Extension (JCE) Unlimited intensidad jurisdicción 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Si usa el X.X.X.jre9.jar de jdbc mssql, ningún archivo de directivas tiene que ser descargados. La directiva de la jurisdicción en Java 9 el valor predeterminado es un número ilimitado nivel de cifrado.

## <a name="working-with-column-master-key-stores"></a>Trabajar con almacenes de clave maestra de columna
Para cifrar o descifrar los datos en las columnas cifradas, SQL Server mantiene las claves de cifrado de columna. Las claves de cifrado de columna se almacenan en un formato cifrado en los metadatos de la base de datos. Cada clave de cifrado de columnas tiene una clave maestra de columna correspondiente que se utiliza para cifrar la clave de cifrado de columna. Los metadatos de la base de datos no contienen las claves maestras de columna. Esas claves solo se mantienen en el cliente. Sin embargo los metadatos de la base de datos contienen información sobre dónde se almacenan las claves maestras de columna en relación con el cliente. Por ejemplo, los metadatos de la base de datos pueden decir el almacén de claves que contiene una clave maestra de columna es el almacén de certificados de Windows y el certificado específico utilizado para cifrar y descifrar se encuentra en una ruta de acceso específica en el almacén de certificados de Windows. Si el cliente tiene acceso a ese certificado en el almacén de certificados de Windows, puede obtener el certificado. El certificado, a continuación, puede utilizarse para descifrar la clave de cifrado de columna. A continuación, esa clave de cifrado puede utilizarse para descifrar ni cifrar datos en las columnas cifradas que utilizan esa clave de cifrado de columna.

El controlador JDBC de Microsoft para SQL Server se comunica con un almacén de claves mediante un proveedor de almacén de claves maestras de columna, que es una instancia de una clase derivado de **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Usar proveedores integrados de almacenamiento de claves maestras de columna
El controlador JDBC de Microsoft para SQL Server incluye los siguientes proveedores de almacenes de clave maestra de columna integrada. Algunos de estos proveedores se registran previamente con los nombres de proveedor específico (utilizados para buscar el proveedor) y algunos requieren credenciales adicionales o registro explícito.

| Clase | Description | Nombre del proveedor (búsqueda) |¿Se ha registrado previamente?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Un proveedor para un almacén de claves para el almacén de claves de Azure.| AZURE_KEY_VAULT|no|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Un proveedor para el almacén de certificados de Windows.|MSSQL_CERTIFICATE_STORE|Sí
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Un proveedor para el almacén de claves de Java|MSSQL_JAVA_KEYSTORE|Sí|

Para los proveedores de almacén de claves registrados previamente, no necesita realizar ningún cambio de código de aplicación para usar estos proveedores pero tenga en cuenta los siguientes elementos:

- Usted (o su DBA) necesita para asegurarse de que el nombre del proveedor configurado en los metadatos de clave maestra de columna sea correcto y la ruta de acceso de clave maestra de columna cumple con el formato de ruta de la clave es válido para un proveedor determinado. Se recomienda que configure las claves mediante herramientas como SQL Server Management Studio, que genera automáticamente los nombres de proveedor y las rutas de acceso de claves cuando se emite la instrucción CREATE COLUMN MASTER KEY (Transact-SQL).
- Asegúrese de que la aplicación puede tener acceso a la clave en el almacén de claves. Esta tarea puede implicar la concesión de la aplicación tenga acceso a la clave o el almacén de claves, según el almacén de claves, o realizar otros pasos de configuración específicos de almacén de claves. Por ejemplo, para usar el SQLServerColumnEncryptionJavaKeyStoreProvider, debe proporcionar la ubicación y la contraseña del almacén de claves en las propiedades de conexión. 

Todos estos proveedores de almacén de claves se describen con más detalle en las secciones siguientes. Sólo debe implementar un proveedor de almacén de claves para usar Always Encrypted.

### <a name="using-azure-key-vault-provider"></a>Usar el proveedor de Azure Key Vault
Almacén de claves de Azure es una opción adecuada para almacenar y administrar claves maestras de columna para Always Encrypted (especialmente si la aplicación se hospeda en Azure). El controlador JDBC de Microsoft para SQL Server incluye un proveedor integrado, SQLServerColumnEncryptionAzureKeyVaultProvider, las aplicaciones que tienen claves almacenadas en el almacén de claves de Azure. El nombre de este proveedor es AZURE_KEY_VAULT. Para poder usar el proveedor de almacenamiento de almacén de claves de Azure, un desarrollador de aplicaciones debe crear el almacén y las claves en el almacén de claves de Azure y crear un registro de una aplicación en Azure Active Directory. La aplicación registrada debe ser concedido obtener, descifrar, cifrar, clave Unwrap, clave ajustar y comprobar permisos en las directivas de acceso definidas para el almacén de claves que se crea para su uso con Always Encrypted. Para obtener más información acerca de cómo configurar el almacén de claves y crear una clave maestra de columna, vea [almacén de claves de Azure: paso a paso](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) y [crear claves maestras de columna en el almacén de claves de Azure](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Para los ejemplos en esta página, si ha creado un almacén de claves de Azure basados en la clave maestra de columna y la clave de cifrado de columna mediante el uso de SQL Server Management Studio, el script de T-SQL para volver a crearlos después puede ser similar a este ejemplo con su propio valor concreto **KEY_ Ruta de acceso** y **ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

Para usar el almacén de claves de Azure, las aplicaciones cliente se necesitan crear una instancia de la SQLServerColumnEncryptionAzureKeyVaultProvider y registrarlo con el controlador.

Este es un ejemplo de inicialización de SQLServerColumnEncryptionAzureKeyVaultProvider:  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** es el identificador de aplicación de un registro de una aplicación en una instancia de Azure Active Directory. **clientKey** se registra una contraseña de clave en esa aplicación, que proporciona acceso de API para el almacén de claves de Azure.

Después de que la aplicación crea una instancia de SQLServerColumnEncryptionAzureKeyVaultProvider, la aplicación debe registrar la instancia con el controlador mediante el método Sqlserverconnection.registercolumnencryptionkeystoreproviders (). Se recomienda encarecidamente que la instancia está registrada con el nombre de búsqueda predeterminado, AZURE_KEY_VAULT, que se puede obtener mediante una llamada a la API SQLServerColumnEncryptionAzureKeyVaultProvider.getName(). El nombre predeterminado, podrá usar herramientas como SQL Server Management Studio o PowerShell para aprovisionar y administrar claves de Always Encrypted (las herramientas usan el nombre predeterminado para generar el objeto de metadatos para la clave maestra de columna). El ejemplo siguiente muestra el registro del proveedor de almacén de claves de Azure. Para obtener más información sobre el método Sqlserverconnection.registercolumnencryptionkeystoreproviders (), consulte [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Si utiliza el proveedor de almacén de claves de almacén de claves de Azure, la implementación de almacén de claves de Azure del controlador JDBC tiene dependencias en estas bibliotecas (desde GitHub) que se deben incluidas con la aplicación:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Para obtener un ejemplo de cómo incluir estas dependencias en un proyecto de Maven, consulte [descargar ADAL4J y claves dependencias con Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Mediante el proveedor de almacén de certificados de Windows
La SQLServerColumnEncryptionCertificateStoreProvider puede utilizarse para almacenar claves maestras de columna en el almacén de certificados de Windows. Use el Asistente para Always Encrypted SQL Server Management Studio (SSMS) u otras herramientas compatibles para crear definiciones de clave de la clave maestra de columna y el cifrado de columna en la base de datos. Puede utilizarse el mismo Asistente para generar un certificado autofirmado en el almacén de certificados de Windows que puede utilizarse como una clave maestra de columna para los datos siempre cifrados. Para obtener más información sobre la clave maestra de columna y la sintaxis de T-SQL de clave de cifrado de columna, vea [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) y [CREATE COLUMN ENCRPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) respectivamente.

El nombre de la SQLServerColumnEncryptionCertificateStoreProvider es MSSQL_CERTIFICATE_STORE y puede ser consultado por la API de getName() del objeto de proveedor. Se registra automáticamente el controlador y se puede utilizar sin problemas sin ningún cambio de la aplicación.

Para los ejemplos en esta página, si ha creado un almacén de certificados de Windows basados en la clave maestra de columna y la clave de cifrado de columna mediante el uso de SQL Server Management Studio, el script de T-SQL para volver a crearlos después puede ser similar a este ejemplo con su propio concreto **KEY_PATH** y **ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> Mientras que los otros proveedores de almacén de claves en este artículo están disponibles en todas las plataformas compatibles con el controlador, la implementación de SQLServerColumnEncryptionCertificateStoreProvider del controlador JDBC está disponible en sistemas operativos Windows únicamente. Tiene una dependencia en el sqljdbc_auth.dll que está disponible en el paquete de controladores. Para utilizar este proveedor, copie el archivo sqljdbc_auth.dll en un directorio en la ruta de acceso del sistema de Windows en el equipo donde está instalado el controlador JDBC. Alternativamente, puede especificar la propiedad del sistema java.libary.path para especificar el directorio de sqljdbc_auth.dll. Si está ejecutando una máquina virtual Java de (JVM, Java Virtual Machine) 32 bits, utilice el archivo sqljdbc_auth.dll en la carpeta x86, aun cuando la versión del sistema operativo sea la x64. Si está ejecutando una JVM de 64 bits en un procesador x64, utilice el archivo sqljdbc_auth.dll de la carpeta x64. Por ejemplo, si usas la JVM de 32 bits y el controlador JDBC está instalado en el directorio predeterminado, puede especificar la ubicación del archivo DLL mediante el siguiente argumento de la máquina virtual (VM) cuando se inicia la aplicación de Java: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Mediante el proveedor de almacén de claves de Java
El controlador JDBC incluye una implementación de proveedor de almacén de claves integradas para el almacén de claves de Java. Si el **keyStoreAuthentication** propiedad cadena de conexión está presente en la cadena de conexión y se establece en "JavaKeyStorePassword", el controlador que automáticamente crea y registra el proveedor de almacén de claves de Java de. El nombre del proveedor de almacén de claves de Java es MSSQL_JAVA_KEYSTORE. Este nombre también se puede consultar mediante la API de SQLServerColumnEncryptionJavaKeyStoreProvider.getName(). 

Hay tres propiedades de cadena de conexión que permiten a una aplicación cliente especificar las credenciales que el controlador necesita para autenticarse en el almacén de claves de Java. El controlador inicializa el proveedor en función de los valores de estas tres propiedades en la cadena de conexión.

**keyStoreAuthentication:** identifica el almacén de claves de Java para usar. Con Microsoft JDBC Driver 6.0 y versiones posterior para SQL Server, se puede autenticar en el almacén de claves de Java sólo a través de esta propiedad. Para el almacén de claves de Java, el valor de esta propiedad debe ser `JavaKeyStorePassword`.

**keyStoreLocation:** la ruta de acceso del archivo de almacén de claves de Java que almacena la clave maestra de columna. La ruta de acceso incluye el nombre de archivo de almacén de claves.

**keyStoreSecret:** el secreto y la contraseña que se utilizará para el almacén de claves, así como para la clave. Para usar el almacén de claves de Java, el almacén de claves y la contraseña de la clave deben ser el mismo.

Este es un ejemplo de proporcionar estas credenciales en la cadena de conexión:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

También puede obtener o establecer estas opciones mediante el objeto SQLServerDataSource. Para obtener más información, consulte [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

El controlador JDBC crea automáticamente una instancia el SQLServerColumnEncryptionJavaKeyStoreProvider cuando estas credenciales están presentes en las propiedades de conexión.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Crear una clave maestra de columna para el almacén de claves de Java
La SQLServerColumnEncryptionJavaKeyStoreProvider puede utilizarse con tipos de almacén de claves de almacén JKS o PKCS12. Para crear o importar una clave para usarla con este proveedor utiliza el Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) utilidad. La clave debe tener la misma contraseña que el almacén de claves. Este es un ejemplo de cómo crear una clave pública y su clave privada asociada con la utilidad de keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Este comando crea una clave pública y ajusta en un certificado, que se almacena en el almacén de claves 'keystore.jks' junto con su clave privada asociada autofirmado de X.509. Esta entrada en el almacén de claves se identifica mediante el alias 'AlwaysEncryptedKey'.

Este es un ejemplo de la misma mediante un tipo de almacén PKCS12:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Si el almacén de claves es de tipo PKCS12, la utilidad keytool no solicita una contraseña de clave y la contraseña de clave debe proporcionarse con la opción - keypass como el SQLServerColumnEncryptionJavaKeyStoreProvider requiere que el almacén de claves y la clave tienen el mismo contraseña.

También puede exportar un certificado del almacén de certificados de Windows en formato .pfx y usarlo con la SQLServerColumnEncryptionJavaKeyStoreProvider. El certificado exportado también puede importarse en el almacén de claves de Java como un tipo de almacén de claves de almacén JKS.

Después de crear la entrada de keytool, cree los metadatos de clave maestra de columna en la base de datos que necesita el nombre del proveedor de almacén de claves y la ruta de acceso de clave. Para obtener más información sobre cómo crear metadatos de clave maestra de columna, vea [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Para SQLServerColumnEncryptionJavaKeyStoreProvider, la ruta de acceso de clave es simplemente el alias de la clave y el nombre de la SQLServerColumnEncryptionJavaKeyStoreProvider es 'MSSQL_JAVA_KEYSTORE'. También puede consultar este nombre mediante la API pública de getName() de la clase SQLServerColumnEncryptionJavaKeyStoreProvider. 

La sintaxis de T-SQL para crear la clave maestra de columna es:

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Para el 'AlwaysEncryptedKey' creado anteriormente, la definición de la clave maestra de columna sería:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> La administración de SQL Server integrada funcionalidad Studio no puede crear las definiciones de la clave maestra de columna para el almacén de claves de Java. Comandos de T-SQL se deben usar mediante programación.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Crear una clave de cifrado de columna para el almacén de claves de Java
SQL Server Management Studio o cualquier otra herramienta no puede utilizarse para crear claves de cifrado mediante claves maestras de columna en el almacén de claves de Java de columna. La aplicación cliente debe crear la clave de cifrado de columna mediante programación con la clase SQLServerColumnEncryptionJavaKeyStoreProvider. Para obtener más información, consulte [mediante proveedores de almacén de claves maestras de columna para el aprovisionamiento de claves mediante programación](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementar un proveedor personalizado de almacén de claves maestras de columna
Si desea almacenar claves maestras de columna en un almacén de claves que no es compatible con un proveedor existente, puede implementar un proveedor personalizado extendiendo la clase SQLServerColumnEncryptionKeyStoreProvider y registrando el proveedor mediante el Método Sqlserverconnection.registercolumnencryptionkeystoreproviders ().

```
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

Registrar el proveedor:

```
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Usar proveedores de almacén de claves maestras de columna para el aprovisionamiento de claves mediante programación
Cuando se obtiene acceso a las columnas cifradas, el controlador JDBC de Microsoft para SQL Server busca de forma transparente y llame al proveedor de almacén de clave maestra de columna de la derecha para descifrar las claves de cifrado de columna. Normalmente, el código de aplicación normal no llama directamente a los proveedores de almacenamiento de claves maestras de columna. Sin embargo, puede crear una instancia y llamar a un proveedor mediante programación para aprovisionar y administrar claves de Always Encrypted. Puede realizar este paso para generar una clave de cifrado de columna cifrada y descifrar una clave de cifrado de columna como parte rotación de claves maestras de columna, por ejemplo. Para obtener más información, vea [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

Si usa un proveedor de almacén de claves personalizado, puede ser necesario implementar sus propias herramientas de administración de claves. Al usar claves almacenadas en el almacén de certificados de Windows o en el almacén de claves de Azure, puede usar herramientas existentes, como SQL Server Management Studio o PowerShell, administrar y aprovisionar claves. Al usar claves almacenadas en el almacén de claves de Java, tendrá que aprovisionar claves mediante programación. En el ejemplo siguiente se muestra cómo utilizar la clase SQLServerColumnEncryptionJavaKeyStoreProvider para cifrar la clave con una clave almacenada en el almacén de claves de Java.

```
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider =
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key
                 * For more details on the syntax, see:
                 * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = "
                        + columnMasterKeyName
                        + " , ALGORITHM =  '"
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x"
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {
        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation :
         *      Path where keystore is located, including the keystore file name.
         * 2) keyStoreSecret :
         *      Password of the keystore and the key.
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>Habilitar Always Encrypted para consultas de la aplicación
La manera más fácil de habilitar el cifrado de parámetros y el descifrado de los resultados de la consulta que tienen como destino las columnas cifradas se está estableciendo el valor de la **columnEncryptionSetting** palabra clave de cadena de conexión para **habilitado** .

La siguiente cadena de conexión es un ejemplo de cómo habilitar Always Encrypted en el controlador JDBC:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

El código siguiente es un ejemplo equivalente utilizando el objeto SQLServerDataSource:

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

Always Encrypted también puede habilitarse para las consultas individuales. Para obtener más información, consulte [controlar el impacto de rendimiento de Always Encrypted](#controlling-the-performance-impact-of-always-encrypted). Habilitar Always Encrypted no es suficiente para el cifrado o descifrado se realicen correctamente. También necesita asegurarse de que:
- La aplicación tiene los permisos de base de datos *VIEW ANY COLUMN MASTER KEY DEFINITION* y *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , que se requieren para tener acceso a los metadatos sobre las claves Always Encrypted de la base de datos. Para obtener más información, consulte [permisos en Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- La aplicación puede tener acceso a la clave maestra de columna que protege las claves de cifrado de columna que cifrar las columnas de base de datos consultada. Para usar el proveedor de almacén de claves de Java, deberá proporcionar credenciales adicionales en la cadena de conexión. Para obtener más información, consulte [proveedor de almacén de claves de Java mediante](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurar cómo los valores java.sql.Time se envían al servidor
El **sendTimeAsDatetime** propiedad de conexión se usa para configurar la forma en que el valor java.sql.Time se envía al servidor. Cuando se establece en false, el valor de hora se envía como un tipo en tiempo de SQL Server. Cuando se establece en true, el valor se envía como un tipo de fecha y hora de tiempo. Si se cifra una columna de tiempo, el **sendTimeAsDatetime** propiedad debe ser false, ya que las columnas cifradas no admite la conversión de hora a fecha y hora. También tenga en cuenta que esta propiedad es true de manera predeterminada, por lo que al usar columnas de hora codificadas tendrán que establecer en false. En caso contrario, el controlador iniciará una excepción. A partir de la versión 6.0 del controlador, la clase SQLServerConnection tiene dos métodos para configurar el valor de esta propiedad mediante programación:
 
* setSendTimeAsDatetime void público (boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

Para obtener más información acerca de esta propiedad, vea [java.sql.Time cómo configurar los valores se envían al servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurar cómo se envían los valores de cadena para el servidor
El **sendStringParametersAsUnicode** propiedad de conexión se utiliza para configurar cómo se envían los valores de cadena a SQL Server. Si se establece en true, parámetros de cadena se envía al servidor en formato Unicode. Si establece en false, parámetros de cadena se envían en formato de no Unicode, como MBCS, Unicode o ASCII. El valor predeterminado de esta propiedad es true. Cuando se habilita Always Encrypted y se cifra una columna char/varchar/varchar(max), el valor de **sendStringParametersAsUnicode** debe establecerse en false. Si esta propiedad se establece en true, el controlador iniciará una excepción al descifrar los datos de una columna cifrada char/varchar/varchar(max) con caracteres Unicode. Para obtener más información acerca de esta propiedad, vea [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperar y modificar datos en columnas cifradas
Una vez que habilite Always Encrypted para consultas de la aplicación, puede usar las API de JDBC estándar para recuperar o modificar datos en las columnas de la base de datos cifrada. Si la aplicación tiene los permisos necesarios de la base de datos y puede tener acceso a la clave maestra de columna, el controlador, se cifrarán los parámetros de consulta destinadas a columnas cifradas y descifrar los datos que se recuperan de las columnas cifradas.

Si Always Encrypted no está habilitado, se producirá un error en las consultas con parámetros que tengan como destino las columnas cifradas. Las consultas todavía pueden recuperar datos de las columnas cifradas, siempre y cuando la consulta no tiene ningún parámetro dirigidos a columnas cifradas. Sin embargo, el controlador no intentará descifrar los valores recuperados de columnas cifradas y la aplicación recibirá datos binarios cifrados (como matrices de bytes).

En la tabla siguiente se resume el comportamiento de consultas dependiendo de si Always Encrypted está habilitado o no:

|Característica de las consultas | Always Encrypted está habilitado y la aplicación puede tener acceso a las claves y a los metadatos de clave|Always Encrypted está habilitado y la aplicación no puede tener acceso a las claves ni a los metadatos de clave | Always Encrypted está deshabilitado|
|:---|:---|:---|:---|
| Consultas con parámetros que tienen como destino las columnas cifradas. | Los valores de parámetro se cifran de manera transparente. | Error | Error|
| Consultas que recuperan datos de las columnas cifradas sin parámetros que se dirigen a columnas cifradas.| Los resultados de las columnas cifradas se descifran de manera transparente. La aplicación recibe valores de texto de los tipos de datos JDBC correspondientes a los tipos de SQL Server configurados para las columnas cifradas. | Error | Los resultados de las columnas cifradas no se descifran. La aplicación recibe valores cifrados como matrices de bytes (byte[]).

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Insertar y recuperar los datos cifrados ejemplos 
En el siguiente ejemplo se ilustra la recuperación y la modificación de datos en las columnas cifradas. Los ejemplos supone la tabla de destino con el siguiente esquema y las columnas SSN y BirthDate cifradas. Si ha configurado una clave maestra de columna denominado "MyCMK" y una clave de cifrado de columna habían denominado "MyCEK" (como se describe en las secciones anteriores de los proveedores de almacén de claves), puede crear la tabla mediante esta secuencia de comandos:

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

Para cada ejemplo de código Java, debe insertar código específico del almacén de claves en la ubicación que anotó.

Si está usando un proveedor de almacén de claves de almacén de claves de Azure:

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Si está usando un proveedor de almacén de claves del almacén de certificados de Windows:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Si está usando un proveedor de almacén de claves de almacén de claves de Java:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Ejemplo de inserción de datos
En este ejemplo se inserta una fila en la tabla Patients. Tenga en cuenta los siguientes elementos:
- No existe nada específico al cifrado en el código de ejemplo. El controlador JDBC de Microsoft para SQL Server detecta automáticamente y cifra los parámetros que tienen como destino las columnas cifradas. Este comportamiento realiza cifrado transparente a la aplicación.
- Los valores insertados en las columnas de base de datos, incluidas las columnas cifradas, se pasan como parámetros mediante SQLServerPreparedStatement. Mientras que el uso de parámetros es opcional al enviar valores a columnas sin cifrar (sin embargo, se recomienda encarecidamente porque ayuda a evitar la inyección de código SQL), es necesario para los valores que tienen como destino las columnas cifradas. Si los valores insertados en las columnas cifradas se pasan como literales incrustados en la instrucción de consulta, se producirá un error en la consulta porque el controlador no sería capaz de determinar los valores de las columnas cifradas de destino y que no los cifrará los valores. Como resultado, el servidor los rechazará considerándolos incompatibles con las columnas cifradas.
- Todos los valores impresos por el programa estarán en texto sin formato, como el controlador JDBC de Microsoft para SQL Server descifrar de forma transparente los datos recuperados de las columnas cifradas.
- Si está realizando una búsqueda con una cláusula WHERE, el valor usado en la cláusula WHERE debe pasarse como un parámetro para que el controlador puede cifrarlo de manera transparente antes de enviarlo a la base de datos. En el ejemplo siguiente, la SSN se pasa como un parámetro pero el apellido se pasa como un literal como LastName no está cifrado.
- El método de establecedor usado para el parámetro que se dirige a la columna SSN es setString(), que se asigna al tipo de datos de SQL Server de char o varchar. Si, para este parámetro, el método de establecedor usado era setNString(), que se asigna a nchar o nvarchar, se producirá un error en la consulta, ya que Always Encrypted no admite conversiones de valores cifrados de nchar o nvarchar a valores cifrados char o varchar.

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))
        {
            insertStatement.setString(1, "795-73-9838");
            insertStatement.setString(2, "Catherine");
            insertStatement.setString(3, "Abel");
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));
            insertStatement.executeUpdate();
            System.out.println("1 record inserted.\n");
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>Ejemplo de datos de texto simple de recuperación
En el ejemplo siguiente se muestra el filtrado de datos basándose en los valores cifrados y recuperar datos de texto simple de las columnas cifradas. Tenga en cuenta los siguientes elementos:
- El valor que se utiliza en la cláusula WHERE para filtrar según la columna SSN necesita pasarse como un parámetro para que el controlador JDBC de Microsoft para SQL Server puede cifrar forma transparente antes de enviarlo a la base de datos.
- Todos los valores impresos por el programa estarán en texto sin formato, como el controlador JDBC de Microsoft para SQL Server descifrar de forma transparente los datos recuperados de las columnas SSN y BirthDate.

> [!NOTE]
> Si las columnas se cifran mediante el cifrado determinista, las consultas pueden realizar comparaciones de igualdad en ellos. Para obtener más información, consulte [cifrado seleccionando determinista o aleatorio en Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";
    
        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "795-73-9838");
            ResultSet rs = selectStatement.executeQuery();
            while(rs.next())
            {
                System.out.println("SSN: " +rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName")+
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>Ejemplo de los datos cifrados de recuperación
Si Always Encrypted no está habilitado, una consulta todavía puede recuperar datos de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas.

En el ejemplo siguiente se muestra la recuperación de datos binarios cifrados de las columnas cifradas. Tenga en cuenta los siguientes elementos:
- Puesto que Always Encrypted no está habilitado en la cadena de conexión, la consulta devolverá valores cifrados de SSN y BirthDate como matrices de bytes (el programa convierte los valores en cadenas).
- Una consulta que recupera datos de columnas cifradas con Always Encrypted deshabilitado puede tener parámetros, siempre y cuando ninguno de ellos tenga como destino una columna cifrada. Los siguientes filtros de consulta por LastName, que no está cifrada en la base de datos. Si la consulta ha filtrado por SSN o BirthDate, esta producirá un error.

```
try
{
    String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;";

        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "Abel");
            ResultSet rs = selectStatement.executeQuery();
            while (rs.next())
            {
                System.out.println("SSN: " + rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName") +
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitar problemas comunes al consultar columnas cifradas
Esta sección describen las categorías comunes de errores al consultar columnas cifradas de aplicaciones Java y algunas instrucciones sobre cómo evitarlos.

### <a name="unsupported-data-type-conversion-errors"></a>Errores de conversión de tipos de datos no compatibles
Always Encrypted admite algunas conversiones para los tipos de datos cifrados. Vea [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obtener una lista detallada de las conversiones de tipos compatibles. Aquí es lo que puede hacer para evitar errores de conversión de tipo de datos. Asegúrese de lo siguiente:

- Utilice los métodos establecedor adecuado al pasar valores de parámetros que tienen como destino las columnas cifradas. Asegúrese de que el tipo de datos de SQL Server del parámetro es exactamente el mismo que el tipo de la columna de destino o se admite una conversión del tipo de datos de SQL Server del parámetro al tipo de destino de la columna. Métodos de la API se agregaron a las clases SQLServerPreparedStatement y SQLServerCallableStatement, SQLServerResultSet para pasar parámetros que corresponden a tipos específicos de datos de SQL Server. Por ejemplo, si no se cifra una columna puede utilizar el método setTimestamp() para pasar un parámetro a un datetime2 o a una columna de fecha y hora. Pero cuando se cifra una columna tendrá que utilizar el método exacto que representa el tipo de la columna en la base de datos. Por ejemplo, utilice setTimestamp() para pasar valores a una columna cifrada datetime2 y use setDateTime() para pasar valores a una columna datetime cifrados. Vea [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obtener una lista completa de nuevas API.
- la precisión y la escala de los parámetros que tienen como destino columnas de los tipos de datos numéricos y decimales de SQL Server debe ser la misma que la precisión y la escala configurada para la columna de destino. Métodos de la API se agregaron a las clases SQLServerPreparedStatement y SQLServerCallableStatement, SQLServerResultSet para aceptar la precisión y escala junto con los valores de datos de parámetros o columnas que representan los tipos de datos decimal y numeric. Vea [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obtener una lista completa de API nuevo/sobrecargado.  
- la precisión o escala de fracciones de segundo de parámetros que tienen como destino columnas datetime2, datetimeoffset o tipos de datos de SQL Server de hora no es mayor que la precisión y escala de fracciones de segundo para la columna de destino en las consultas que modifican los valores de la columna de destino . Métodos de la API se agregaron a las clases SQLServerPreparedStatement y SQLServerCallableStatement, SQLServerResultSet para aceptar la precisión de fracciones de segundo/escala junto con los valores de datos de parámetros que representan estos tipos de datos. Para obtener una lista completa de nuevo/sobrecargado API, consulte [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).   

### <a name="errors-due-to-incorrect-connection-properties"></a>Errores debido a las propiedades de conexión incorrecta
En esta sección se describe cómo configurar opciones de conexión correctamente para usar datos Always Encrypted. Puesto que los tipos de datos cifrados admiten conversiones limitadas, la **sendTimeAsDatetime** y **sendStringParametersAsUnicode** configuración de conexión necesita una configuración correcta, si usa las columnas cifradas. Asegúrese de lo siguiente: 
- [sendTimeAsDatetime](setting-the-connection-properties.md) configuración de conexión se establece en false, al insertar datos en columnas de tiempo cifradas. Para obtener más información, consulte [configurar cómo los valores java.sql.Time se envían al servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) configuración de conexión se establece en true (o se deja como el valor predeterminado) al insertar datos en cifrado char/varchar/varchar(max) columnas.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errores debidos a pasar texto sin formato en lugar de valores cifrados
Cualquier valor que tenga como destino una columna cifrada necesita cifrarse dentro de la aplicación. Un intento para insertar, modificar o filtrar por un valor de texto simple en una columna cifrada producirá un error similar a este:

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar dichos errores, asegúrese de que:
- Always Encrypted está habilitado para las consultas de aplicación que se dirigen a columnas cifradas (para la cadena de conexión o para una consulta específica).
- Puede utilizar las instrucciones preparadas y parámetros que se enviarán datos como destino las columnas cifran. En el ejemplo siguiente se muestra una consulta que filtra de manera incorrecta mediante un literal o constante en una columna cifrada (SSN), en lugar de pasar el literal dentro de como un parámetro. Se producirá un error en esta consulta:

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forzar el cifrado en los parámetros de entrada
La característica de forzar el cifrado aplica el cifrado de un parámetro cuando se utiliza Always Encrypted. Si forzar el cifrado se utiliza y SQL Server indica al controlador que no es necesario cifrar el parámetro, se producirá un error en la consulta mediante el parámetro. Esta propiedad confiere una protección adicional frente a ataques contra la seguridad que utilice un servidor SQL Server comprometido que proporcione metadatos de cifrado incorrectos al cliente, lo cual podría provocar la divulgación de datos. Los métodos set * en la actualización de las clases SQLServerPreparedStatement y SQLServerCallableStatement y\* se sobrecargan métodos en la clase SQLServerResultSet para que acepte un argumento booleano para especificar la configuración de cifrado de forzar. Si el valor de este argumento es false, el controlador no forzar el cifrado en los parámetros. Si forzar el cifrado se establece en true, la consulta parámetro sólo se envía si la columna de destino está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción. Uso de esta propiedad proporciona un nivel adicional de seguridad, asegurándose de que el controlador no erróneamente enviar datos a SQL Server como texto sin formato cuando se espera que se cifren.

Para obtener más información sobre los métodos SQLServerPreparedStatement y SQLServerCallableStatement que están sobrecargados con la configuración de cifrado forzado, consulte [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controlar el impacto de rendimiento de Always Encrypted
Como Always Encrypted es una tecnología de cifrado en el cliente, la mayor parte de la sobrecarga de rendimiento se observa en el lado de cliente, no en la base de datos. Además del costo de las operaciones de cifrado y descifrado, otros orígenes de las sobrecargas de rendimiento en el cliente de son:
- Ciclos de ida y vuelta adicionales a la base de datos para recuperar metadatos para los parámetros de consulta.
- Llamadas a un almacén de claves maestras de columna para tener acceso a una clave maestra de columna.

Esta sección describen las optimizaciones de rendimiento integrados en el controlador JDBC de Microsoft para SQL Server y cómo se puede controlar el impacto de los dos factores anteriores en el rendimiento.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlar los ciclos de ida y vuelta para recuperar metadatos para los parámetros de consulta
Si Always Encrypted está habilitado para una conexión, de forma predeterminada el controlador llamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta con parámetros, pasar la instrucción de consulta (sin ningún valor de parámetro) a SQL Server. [Sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analiza la instrucción de consulta para averiguar si algún parámetro necesita cifrarse y si es así, para cada uno devuelva la información relacionada con el cifrado que permitirá que el controlador cifrar los valores de parámetro. Este comportamiento garantiza un alto nivel de transparencia para la aplicación cliente. Siempre y cuando la aplicación utiliza parámetros para pasar los valores que tienen como destino las columnas cifradas en el controlador, la aplicación (y el programador de aplicaciones) no necesitan saber qué consultas acceden a columnas cifradas.

### <a name="setting-always-encrypted-at-the-query-level"></a>Configurar Always Encrypted en el nivel de consulta
Para controlar el impacto en el rendimiento de recuperación de metadatos de cifrado para las consultas parametrizadas, puede habilitar Always Encrypted para consultas individuales en lugar de configurarlo para la conexión. De este modo, puede asegurarse de que sys.sp_describe_parameter_encryption se invoca solo para las consultas que sabe que tienen parámetros que se dirigen a columnas cifradas. Sin embargo, tenga en cuenta que, si lo hace, se reduce la transparencia del cifrado: si cambia las propiedades de cifrado de las columnas de base de datos, deberá cambiar el código de la aplicación para alinearlo con los cambios de esquema.

Para controlar el comportamiento de Always Encrypted de las consultas individuales, debe configurar los objetos de cada instrucción individual si se pasa una enumeración, SQLServerStatementColumnEncryptionSetting, que especifica cómo se enviarán y recibidos al leer y escribir datos columnas cifradas para esa instrucción específica. A continuación se exponen unas directrices prácticas:
- Si la mayoría de las consultas que una aplicación cliente envía a través de una conexión de base de datos acceden a columnas cifradas, siga estas instrucciones:
    - Establecer el **columnEncryptionSetting** palabra clave de cadena de conexión a **habilitado**.
    - Establezca SQLServerStatementColumnEncryptionSetting.Disabled para consultas individuales que no puedan acceder a ninguna columna cifrada. Esta opción se deshabilitará la llamada a sys.sp_describe_parameter_encryption así como un intento para descifrar los valores del conjunto de resultados.
    - Establezca SQLServerStatementColumnEncryptionSetting.ResultSet para consultas individuales que no tiene ningún parámetro que requiera cifrado, pero recuperen datos de columnas cifradas. Esta opción se deshabilitará la llamada a sys.sp_describe_parameter_encryption y el cifrado de parámetros. La consulta podrá descifrar los resultados de las columnas de cifrado.
- Si la mayoría de las consultas que una aplicación cliente envía a través de una conexión de base de datos no obtienen acceso a las columnas cifradas, siga estas instrucciones:
    - Establecer el **columnEncryptionSetting** palabra clave de cadena de conexión a **deshabilitado**.
    - Establezca SQLServerStatementColumnEncryptionSetting.Enabled para consultas individuales que tienen los parámetros que se deben cifrarse. Esta configuración se habilitará la llamada a sys.sp_describe_parameter_encryption así como el descifrado de los resultados de consultas recuperados de columnas cifradas.
    - Establecer SQLServerStatementColumnEncryptionSetting.ResultSet para las consultas que no tiene ningún parámetro que requiera cifrado y recuperen datos de las columnas cifradas. Esta opción se deshabilitará la llamada a sys.sp_describe_parameter_encryption y el cifrado de parámetros. La consulta podrá descifrar los resultados de las columnas de cifrado.

La configuración de SQLServerStatementColumnEncryptionSetting no puede utilizarse para omitir el cifrado y obtener acceso a datos de texto simple. Para obtener más información acerca de cómo configurar el cifrado de columna en una instrucción, vea [siempre cifrados referencia de la API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

En el ejemplo siguiente, Always Encrypted está deshabilitado para la conexión de base de datos. La consulta de los problemas de aplicaciones tiene un parámetro que tiene como destino la columna LastName que no están cifrada. La consulta recupera datos de las columnas SSN y BirthDate que están cifradas. En este caso, no es necesario llamar a sys.sp_describe_parameter_encryption para recuperar los metadatos de cifrado. Sin embargo, el descifrado de los resultados de la consulta debe habilitarse para que la aplicación puede recibir valores de texto de las dos columnas cifradas. La configuración de SQLServerStatementColumnEncryptionSetting.ResultSet se utiliza para asegurarse de que.

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord,
        ResultSet.TYPE_FORWARD_ONLY,
        ResultSet.CONCUR_READ_ONLY,
        connection.getHoldability(),
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");
ResultSet rs = selectStatement.executeQuery();
while(rs.next()) {
    System.out.println("First name: " + rs.getString("FirstName"));
    System.out.println("Last name: " + rs.getString("LastName"));
    System.out.println("SSN: " + rs.getString("SSN"));
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
}
rs.close();
selectStatement.close();
connection.close();
```

### <a name="column-encryption-key-caching"></a>Almacenamiento en memoria caché de claves de cifrado de columnas
Para reducir el número de llamadas a un almacén de claves maestras de columna para descifrar las claves de cifrado de columna, el controlador JDBC de Microsoft para SQL Server almacena en caché las claves de cifrado de columna de texto simple en la memoria. Después de recibir el valor de clave de cifrado de columna cifrada de los metadatos de la base de datos, primero el controlador intenta encontrar la clave de cifrado de columna de texto simple correspondiente al valor de clave cifrado. El controlador llama el almacén de claves que contiene la clave maestra de columna sólo si no encuentra el valor de clave de cifrado de columna cifrada en la memoria caché.

Puede configurar un valor de período de vida de las entradas de clave de cifrado de columna en la memoria caché mediante la API, setColumnEncryptionKeyCacheTtl(), en la clase SQLServerConnection. El valor de período de vida predeterminado para las entradas de clave de cifrado de columna en la memoria caché es de dos horas. Para desactivar el almacenamiento en caché, utilice un valor de 0. Para establecer cualquier valor de período de vida, utilice la siguiente API:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Por ejemplo, para establecer un valor de período de vida de 10 minutos, utilice:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Se admiten sólo días, horas, minutos o segundos como la unidad de tiempo.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copiar datos cifrados con SQLServerBulkCopy
Con SQLServerBulkCopy, puede copiar los datos que ya se cifran y almacenan en una tabla a otra tabla sin descifrar los datos. Para realizar esto:

- Asegúrese de que la configuración de cifrado de la tabla de destino es idéntica a la configuración de la tabla de origen. En particular, ambas tablas deben tener las mismas columnas cifradas y las columnas deben cifrarse con los mismos tipos de cifrado y las mismas claves de cifrado. Si ninguna columna de destino está cifrada de manera diferente a la columna de origen correspondiente, no podrá descifrar los datos en la tabla de destino después de la operación de copia. Los datos estarán dañados.
- Configurar las conexiones de base de datos para la tabla de origen y la tabla de destino sin habilitado para Always Encrypted.
- Establezca la opción allowEncryptedValueModifications. Para obtener más información, consulte [utilizando la copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Tenga precaución al especificar AllowEncryptedValueModifications como esta opción puede provocar daños en la base de datos porque el controlador JDBC de Microsoft para SQL Server no comprueba si realmente se cifran los datos o si se han cifrado correctamente mediante el mismo cifrado tipo de algoritmo y clave como la columna de destino.

## <a name="see-also"></a>Vea también
[Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
