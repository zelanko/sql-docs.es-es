---
title: Usar Always Encrypted con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f19878f73397b9146765fecd879dad07ebb73dc3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916448"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Usar Always Encrypted con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En esta página se proporciona información sobre cómo desarrollar aplicaciones de Java con [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y Microsoft JDBC driver 6,0 (o superior) para SQL Server.

Always Encrypted permite a los clientes cifrar la información confidencial y nunca revelar los datos ni las claves de cifrado en SQL Server o Azure SQL Database. Un controlador habilitado para Always Encrypted, como Microsoft JDBC Driver 6.0 (o superior) for SQL Server, consigue este comportamiento al cifrar y descifrar de manera transparente la información confidencial en la aplicación cliente. El controlador determina automáticamente qué parámetros de consulta corresponden a Always Encrypted columnas de la base de datos y cifra los valores de esos parámetros antes de enviarlos a SQL Server o Azure SQL Database. De forma similar, el controlador descifra de manera transparente los datos que se han recuperado de las columnas de bases de datos cifradas de los resultados de la consulta. Para obtener más información, consulte [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y [referencia de la API de Always Encrypted para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Prerequisites
- Asegúrese de que Microsoft JDBC driver 6,0 (o posterior) para SQL Server está instalado en el equipo de desarrollo. 
- Descargue e instale los archivos de Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy.  Asegúrese de leer el archivo Léame incluido en el archivo zip para obtener instrucciones de instalación y detalles relevantes sobre los posibles problemas de importación o exportación.  

    - Si usa mssql-jdbc-X.X.X.jre7.jar o sqljdbc41.jar, los archivos de directiva pueden descargarse desde [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 7 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html).

    - Si usa mssql-jdbc-X.X.X.jre8.jar o sqljdbc42.jar, los archivos de directiva pueden descargarse desde [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html).

    - Si usa mssql-jdbc-X. X. X. jre9. jar, no es necesario descargar ningún archivo de directiva. La Directiva de jurisdicción en Java 9 tiene como valor predeterminado el cifrado de nivel ilimitado.

## <a name="working-with-column-master-key-stores"></a>Trabajar con almacenes de claves maestras de columna
Para cifrar o descifrar los datos de las columnas cifradas, SQL Server mantiene las claves de cifrado de columna. Las claves de cifrado de columnas se almacenan con formato cifrado en los metadatos de la base de datos. Cada clave de cifrado de columnas tiene una clave maestra de columna correspondiente que se ha usado para cifrar la clave de cifrado de columnas. Los metadatos de la base de datos no contienen las claves maestras de columna. Estas claves solo las mantiene el cliente. Sin embargo, los metadatos de la base de datos contienen información sobre dónde se almacenan las claves maestras de columna en relación con el cliente. Por ejemplo, los metadatos de la base de datos pueden indicar que el almacén de claves que contiene una clave maestra de columna es el almacén de certificados de Windows y el certificado específico que se usa para cifrar y descifrar se encuentra en una ruta de acceso específica en el almacén de certificados de Windows. Si el cliente tiene acceso a ese certificado en el almacén de certificados de Windows, puede obtener el certificado. El certificado se puede usar para descifrar la clave de cifrado de columna. A continuación, la clave de cifrado se puede usar para descifrar o cifrar los datos de las columnas cifradas que utilizan esa clave de cifrado de columna.

Microsoft JDBC driver para SQL Server se comunica con un almacén de claves mediante un proveedor de almacén de claves maestras de columna, que es una instancia de una clase derivada de **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Usar proveedores integrados de almacenamiento de claves maestras de columna
Microsoft JDBC driver para SQL Server incluye los siguientes proveedores de almacenamiento de claves maestras de columna integrados. Algunos de estos proveedores se registran previamente con los nombres de proveedor específicos (usados para buscar el proveedor) y otros requieren credenciales adicionales o un registro explícito.

| Clase                                                 | Descripción                                        | Nombre del proveedor (búsqueda)  | ¿Está registrado previamente? |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Un proveedor para un almacén de claves para el Azure Key Vault. | AZURE_KEY_VAULT         | No                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Un proveedor para el Almacén de certificados de Windows.      | MSSQL_CERTIFICATE_STORE | Sí                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Un proveedor para el almacén de claves de Java                   | MSSQL_JAVA_KEYSTORE     | Sí                |

En el caso de los proveedores de almacén de claves previamente registrados, no es necesario realizar ningún cambio en el código de aplicación para usar estos proveedores, pero tenga en cuenta los siguientes elementos:

- Usted (o su DBA) necesita asegurarse de que el nombre de proveedor, configurado en los metadatos de clave maestra de columna, sea correcto y que la ruta de acceso de la clave maestra de columna cumpla con un formato de ruta de acceso de la clave que sea válido para un proveedor determinado. Se recomienda que configure las claves mediante herramientas como SQL Server Management Studio, que genera automáticamente las rutas de acceso a la clave y los nombres de proveedor válidos al emitir la instrucción CREATE COLUMN MASTER KEY (Transact-SQL).
- Asegúrese de que la aplicación puede tener acceso a la clave del almacén de claves. Esta tarea puede suponer conceder a la aplicación el acceso a la clave o al almacén de claves, dependiendo de este, o bien realizar cualquier otro paso de configuración específico del almacén de claves. Por ejemplo, para usar SQLServerColumnEncryptionJavaKeyStoreProvider, debe proporcionar la ubicación y la contraseña del almacén de claves en las propiedades de conexión. 

Todos estos proveedores de almacén de claves se describen con más detalle en las secciones siguientes. Solo necesita implementar un proveedor de almacén de claves para utilizar Always Encrypted.

### <a name="using-azure-key-vault-provider"></a>Usar el proveedor de Azure Key Vault
Azure Key Vault es una opción adecuada para almacenar y administrar claves maestras de columna para Always Encrypted (especialmente si sus aplicaciones se hospedan en Azure). Microsoft JDBC driver for SQL Server incluye un proveedor integrado, SQLServerColumnEncryptionAzureKeyVaultProvider, para las aplicaciones que tienen claves almacenadas en Azure Key Vault. El nombre de este proveedor es AZURE_KEY_VAULT. Para usar el proveedor de almacenamiento de Azure Key Vault, un desarrollador de aplicaciones debe crear el almacén y las claves en Azure Key Vault y crear un registro de la aplicación en Azure Active Directory. La aplicación registrada debe tener concedidos los permisos get, Decrypt, Encrypt, Unwrap Key, Wrap Key y Verify en las directivas de acceso definidas para el almacén de claves creado para su uso con Always Encrypted. Para obtener más información sobre cómo configurar el almacén de claves y crear una clave maestra de columna, vea [Azure Key Vault paso a paso](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) y [crear claves maestras de columna en Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

En los ejemplos de esta página, si ha creado una clave maestra de columna basada en Azure Key Vault y una clave de cifrado de columna mediante SQL Server Management Studio, el script T-SQL para volver a crearlos podría ser similar a este ejemplo con sus propias **KEY_PATH** específicas y **ENCRYPTED_VALUE**:

```sql
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

Para usar el Azure Key Vault, las aplicaciones cliente deben crear una instancia del SQLServerColumnEncryptionAzureKeyVaultProvider y registrarlo con el controlador.

Este es un ejemplo de la inicialización de SQLServerColumnEncryptionAzureKeyVaultProvider:  

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**ClientID** es el identificador de aplicación de un registro de aplicación en una instancia de Azure Active Directory. **clientKey** es una contraseña de clave registrada en esa aplicación, que proporciona acceso de API a la Azure Key Vault.

Una vez que la aplicación crea una instancia de SQLServerColumnEncryptionAzureKeyVaultProvider, la aplicación debe registrar la instancia con el controlador mediante el método SQLServerConnection. registerColumnEncryptionKeyStoreProviders (). Se recomienda encarecidamente que la instancia se registre con el nombre de búsqueda predeterminado, AZURE_KEY_VAULT, que se puede obtener llamando a la API SQLServerColumnEncryptionAzureKeyVaultProvider. getName (). El uso del nombre predeterminado le permitirá usar herramientas como SQL Server Management Studio o PowerShell para aprovisionar y administrar claves de Always Encrypted (las herramientas usan el nombre predeterminado para generar el objeto de metadatos para la clave maestra de columna). En el ejemplo siguiente se muestra cómo registrar el proveedor de Azure Key Vault. Para obtener más información sobre el método SQLServerConnection. registerColumnEncryptionKeyStoreProviders (), vea [Always Encrypted referencia de la API del controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Si usa el proveedor de almacén de claves de Azure Key Vault, la implementación de Azure Key Vault del controlador JDBC tiene dependencias en estas bibliotecas (desde GitHub) que deben incluirse en la aplicación:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Para ver un ejemplo de cómo incluir estas dependencias en un proyecto de Maven, consulte descarga de dependencias de [ADAL4J y AKV con Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Uso del proveedor para el Almacén de certificados de Windows
SQLServerColumnEncryptionCertificateStoreProvider, que se puede utilizar para almacenar claves maestras de columna en el almacén de certificados de Windows. Use el Asistente para Always Encrypted de SQL Server Management Studio (SSMS) u otras herramientas compatibles para crear la clave maestra de columna y las definiciones de clave de cifrado de columna en la base de datos. Se puede usar el mismo asistente para generar un certificado autofirmado en el almacén de certificados de Windows que se puede usar como clave maestra de columna para los datos de Always encrypted. Para obtener más información sobre la clave maestra de columna y la sintaxis de T-SQL de clave de cifrado de columna, vea [crear clave maestra](../../t-sql/statements/create-column-master-key-transact-sql.md) de columna y [crear clave](../../t-sql/statements/create-column-encryption-key-transact-sql.md) de cifrado de columna respectivamente.

El nombre de SQLServerColumnEncryptionCertificateStoreProvider es MSSQL_CERTIFICATE_STORE y se puede consultar mediante la API getName () del objeto de proveedor. Lo registra automáticamente el controlador y se puede usar sin problemas sin ningún cambio en la aplicación.

En los ejemplos de esta página, si ha creado una clave maestra de columna basada en el almacén de certificados de Windows y una clave de cifrado de columna mediante SQL Server Management Studio, el script T-SQL para volver a crearlos podría ser similar a este ejemplo con su propio denominarse específico.  **Ruta de acceso** y **ENCRYPTED_VALUE**:

```sql
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
> Aunque los otros proveedores de almacén de claves de este artículo están disponibles en todas las plataformas admitidas por el controlador, la implementación de SQLServerColumnEncryptionCertificateStoreProvider del controlador JDBC solo está disponible en los sistemas operativos Windows. Tiene una dependencia en el archivo sqljdbc_auth. dll que está disponible en el paquete de controladores. Para usar este proveedor, copie el archivo sqljdbc_auth.dll en un directorio de la ruta del sistema de Windows en que esté instalado el controlador JDBC. También puede especificar la propiedad del sistema java.libary.path para especificar el directorio de sqljdbc_auth.dll. Si está ejecutando una máquina virtual Java de (JVM, Java Virtual Machine) 32 bits, utilice el archivo sqljdbc_auth.dll en la carpeta x86, aun cuando la versión del sistema operativo sea la x64. Si está ejecutando una JVM de 64 bits en un procesador x64, utilice el archivo sqljdbc_auth.dll de la carpeta x64. Por ejemplo, si está usando JVM de 32 bits y el controlador JDBC está instalado en el directorio predeterminado, puede especificar la ubicación de la DLL con el siguiente argumento de máquina virtual (VM) si la aplicación de Java se ha iniciado: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Usar el proveedor de almacén de claves de Java
El controlador JDBC incluye una clave integrada para la implementación del proveedor del almacén de claves para el almacén de claves de Java. Si la propiedad de la cadena de conexión **keyStoreAuthentication** está presente en la cadena de conexión y está establecida en "JavaKeyStorePassword", el controlador crea automáticamente instancias y registra el proveedor para el almacén de claves de Java. El nombre del proveedor de almacén de claves de Java es MSSQL_JAVA_KEYSTORE. Este nombre también se puede consultar mediante la API SQLServerColumnEncryptionJavaKeyStoreProvider. getName (). 

Hay tres propiedades de cadena de conexión que permiten que una aplicación cliente especifique las credenciales que el controlador necesita para autenticarse en el almacén de claves de Java. El controlador inicializa el proveedor basándose en los valores de estas tres propiedades en la cadena de conexión.

**keyStoreAuthentication:** Identifica el almacén de claves de Java que se va a usar. Con Microsoft JDBC driver 6,0 y versiones posteriores para SQL Server, solo puede autenticarse en el almacén de claves de Java a través de esta propiedad. Para el almacén de claves de Java, el valor de esta propiedad `JavaKeyStorePassword`debe ser.

**keyStoreLocation:** La ruta de acceso al archivo de almacén de claves de Java que almacena la clave maestra de columna. La ruta de acceso incluye el nombre de archivo del almacén de claves.

**keyStoreSecret:** Secreto y contraseña que se usarán para el almacén de claves, así como para la clave. Para usar el almacén de claves de Java, el almacén de claves y la contraseña de la clave deben ser iguales.

Este es un ejemplo de cómo proporcionar estas credenciales en la cadena de conexión:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

También puede obtener o establecer esta configuración mediante el objeto SQLServerDataSource. Para obtener más información, vea [referencia de la API de Always Encrypted para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

El controlador JDBC crea automáticamente instancias de SQLServerColumnEncryptionJavaKeyStoreProvider cuando estas credenciales están presentes en las propiedades de conexión.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Crear una clave maestra de columna para el almacén de claves de Java
SQLServerColumnEncryptionJavaKeyStoreProvider se puede usar con los tipos de almacén de claves JKS o PKCS12. Para crear o importar una clave que se va a usar con este proveedor, use la utilidad Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) . La clave debe tener la misma contraseña que el propio almacén de claves. Este es un ejemplo de cómo crear una clave pública y su clave privada asociada con la utilidad keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Este comando crea una clave pública y la encapsula en un certificado X. 509 autofirmado, que se almacena en el almacén de claves ' keystore. JKS ' junto con su clave privada asociada. Esta entrada en el almacén de claves se identifica mediante el alias "AlwaysEncryptedKey".

Este es un ejemplo del mismo uso de un tipo de almacén PKCS12:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Si el almacén de claves es de tipo PKCS12, la utilidad keytool no solicita una contraseña de clave y se debe proporcionar la contraseña de clave con la opción-KeyPass, ya que la SQLServerColumnEncryptionJavaKeyStoreProvider requiere que el almacén de claves y la clave tengan el mismo contraseña.

También puede exportar un certificado del almacén de certificados de Windows en formato. pfx y usarlo con el SQLServerColumnEncryptionJavaKeyStoreProvider. El certificado exportado también se puede importar en el almacén de claves de Java como un tipo JKS de keystore.

Después de crear la entrada keytool, cree los metadatos de la clave maestra de columna en la base de datos, que necesita el nombre del proveedor de almacén de claves y la ruta de acceso de la clave. Para obtener más información sobre cómo crear metadatos de clave maestra de columna, vea [Create Column Master Key](../../t-sql/statements/create-column-master-key-transact-sql.md). En el caso de SQLServerColumnEncryptionJavaKeyStoreProvider, la ruta de acceso de la clave es simplemente el alias de la clave y el nombre de la SQLServerColumnEncryptionJavaKeyStoreProvider es ' MSSQL_JAVA_KEYSTORE '. También puede consultar este nombre mediante la API pública getName () de la clase SQLServerColumnEncryptionJavaKeyStoreProvider. 

La sintaxis de T-SQL para crear la clave maestra de columna es la siguiente:

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Para el ' AlwaysEncryptedKey ' creado anteriormente, la definición de la clave maestra de columna sería:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> La funcionalidad integrada de SQL Server Management Studio no puede crear definiciones de clave maestra de columna para el almacén de claves de Java. Los comandos T-SQL deben usarse mediante programación.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Crear una clave de cifrado de columna para el almacén de claves de Java
El SQL Server Management Studio o cualquier otra herramienta no se puede usar para crear claves de cifrado de columna mediante claves maestras de columna en el almacén de claves de Java. La aplicación cliente debe crear la clave de cifrado de columna mediante programación con la clase SQLServerColumnEncryptionJavaKeyStoreProvider. Para obtener más información, vea [uso de proveedores de almacenamiento de claves maestras de columna para el aprovisionamiento de claves mediante programación](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementar un proveedor personalizado de almacén de claves maestras de columna
Si quiere almacenar claves maestras de columna en un almacén de claves que no sea compatible con un proveedor existente, puede implementar un proveedor personalizado mediante la extensión de la clase SQLServerColumnEncryptionKeyStoreProvider y registrando el proveedor mediante el método SQLServerConnection.registerColumnEncryptionKeyStoreProviders().

```java
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

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Usar proveedores de almacén de claves maestras de columna para el aprovisionamiento de claves mediante programación
Al tener acceso a las columnas cifradas, Microsoft JDBC Driver for SQL Server busca y llama de manera transparente al proveedor de almacenamiento de claves maestras de columna adecuado para descifrar las claves de cifrado de columnas. Normalmente, el código de aplicación normal no llama directamente a los proveedores de almacenamiento de claves maestras de columna. No obstante, puede crear instancias de un proveedor y llamarlo mediante programación para aprovisionar y administrar las claves de Always Encrypted. Este paso puede realizarse para generar una clave de cifrado de columna cifrada y descifrar una clave de cifrado de columnas como parte de la rotación de claves maestras de columna, por ejemplo. Para obtener más información, vea [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

Si usa un proveedor de claves personalizado, puede que sea necesario implementar sus propias herramientas de administración de claves. Al usar claves almacenadas en el almacén de certificados de Windows o en Azure Key Vault, puede usar herramientas existentes, como SQL Server Management Studio o PowerShell, para administrar y aprovisionar claves. Cuando se usan claves almacenadas en el almacén de claves de Java, es necesario aprovisionar claves mediante programación. En el ejemplo siguiente se muestra el uso de la clase SQLServerColumnEncryptionJavaKeyStoreProvider para cifrar la clave con una clave almacenada en el almacén de claves de Java.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>Habilitar Always Encrypted para consultas de la aplicación
Establecer el valor de la palabra clave de cadena de conexión **columnEncryptionSetting** en **Enabled** es la manera más sencilla de habilitar el cifrado de parámetros y el descifrado de los resultados de la consulta que tienen como destino las columnas cifradas.

La siguiente cadena de conexión es un ejemplo de cómo habilitar Always Encrypted en el controlador JDBC:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

El código siguiente es un ejemplo equivalente que usa el objeto SQLServerDataSource:

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

Always Encrypted también puede habilitarse para las consultas individuales. Para obtener más información, vea [Controlar el impacto en el rendimiento de Always Encrypted](#controlling-the-performance-impact-of-always-encrypted). Habilitar Always Encrypted no es suficiente para que el cifrado o el descifrado se realicen correctamente. También necesita asegurarse de que:
- La aplicación tiene los permisos de base de datos *VIEW ANY COLUMN MASTER KEY DEFINITION* y *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , que se requieren para tener acceso a los metadatos sobre las claves Always Encrypted de la base de datos. Para obtener más información, vea [Permisos en Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- La aplicación puede tener acceso a la clave maestra de columna que protege las claves de cifrado de columnas, las cuales cifran las columnas de bases de datos consultadas. Para usar el proveedor de almacén de claves de Java, debe proporcionar credenciales adicionales en la cadena de conexión. Para obtener más información, vea [uso del proveedor de almacén de claves de Java](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Configurar el modo en que los valores java.sql.Time se envían al servidor
Puede configurar la forma de enviar el valor java.sql.Time al servidor usando la propiedad de conexión **sendTimeAsDatetime**. Cuando se establece en false, el valor de hora se envía como un tipo de hora de SQL Server. Cuando se establece en true, el valor de hora se envía como un tipo DateTime. Si una columna de hora está cifrada, la propiedad **sendTimeAsDatetime** debe ser false, ya que las columnas cifradas no admiten la conversión de Time a DateTime. Tenga en cuenta también que esta propiedad es true de forma predeterminada, por lo que cuando use columnas de tiempo cifradas tendrá que establecerla en false. De lo contrario, el controlador producirá una excepción. A partir de la versión 6,0 del controlador, la clase SQLServerConnection tiene dos métodos para configurar el valor de esta propiedad mediante programación:
 
* public void setSendTimeAsDatetime (Boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

Para más información sobre esta propiedad, consulte [Configurar el modo en que los valores java.sql.Time se envían al servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Configurar el modo en que se envían los valores de cadena al servidor
La propiedad de conexión **sendStringParametersAsUnicode** se utiliza para configurar cómo se envían los valores de cadena a SQL Server. Si se establece en true, se envían parámetros String al servidor en formato Unicode. Si se establece en false, los parámetros de cadena se envían en formato no Unicode, como ASCII o MBCS, en lugar de Unicode. El valor predeterminado de esta propiedad es true. Cuando Always Encrypted está habilitada y se cifra una columna CHAR/VARCHAR/VARCHAR (Max), el valor de **sendStringParametersAsUnicode** debe establecerse en false. Si esta propiedad se establece en true, el controlador producirá una excepción al descifrar los datos de una columna cifrada CHAR/VARCHAR/VARCHAR (Max) que tenga caracteres Unicode. Para obtener más información sobre esta propiedad, vea [establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperar y modificar los datos de las columnas cifradas
Una vez que habilite Always Encrypted para las consultas de aplicación, puede usar las API de JDBC estándar para recuperar o modificar los datos de las columnas de base de datos cifradas. Si la aplicación tiene los permisos de base de datos necesarios y puede tener acceso a la clave maestra de columna, el controlador cifrará los parámetros de consulta que tengan como destino las columnas cifradas y descifrará los datos recuperados de las columnas cifradas.

Si Always Encrypted no está habilitado, se producirá un error en las consultas con parámetros que tengan como destino las columnas cifradas. Las consultas todavía pueden recuperar datos de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas. Pero el controlador no intentará descifrar ningún valor que se haya recuperado de las columnas cifradas y la aplicación recibirá datos binarios cifrados (como matrices de bytes).

En la tabla siguiente se resume el comportamiento de las consultas, dependiendo de si Always Encrypted está habilitado o no:

| Característica de las consultas                                                                           | Always Encrypted está habilitado y la aplicación puede tener acceso a las claves y a los metadatos de clave                                                                                                                        | Always Encrypted está habilitado y la aplicación no puede tener acceso a las claves ni a los metadatos de clave | Always Encrypted está deshabilitado                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Consultas con parámetros que tienen como destino las columnas cifradas.                                           | Los valores de parámetro se cifran de manera transparente.                                                                                                                                                           | Error                                                                             | Error                                                                                                               |
| Consultas que recuperan datos de las columnas cifradas, sin parámetros que tengan como destino las columnas cifradas. | Los resultados de las columnas cifradas se descifran de manera transparente. La aplicación recibe valores de texto sin formato de los tipos de datos JDBC que corresponden a los tipos de SQL Server configurados para las columnas cifradas. | Error                                                                             | Los resultados de las columnas cifradas no se descifran. La aplicación recibe valores cifrados como matrices de bytes (byte[]). |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Ejemplos de inserción y recuperación de datos cifrados

En el siguiente ejemplo se ilustra la recuperación y la modificación de datos en las columnas cifradas. En los ejemplos se supone que la tabla de destino tiene el esquema siguiente y las columnas SSN y BirthDate cifradas. Si ha configurado una clave maestra de columna denominada "MyCMK" y una clave de cifrado de columna denominada "MyCEK" (como se describe en las secciones anteriores de proveedores de almacén de claves), puede crear la tabla con este script:

```sql
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

Para cada ejemplo de código de Java, deberá insertar código específico del almacén de claves en la ubicación indicada.

Si utiliza un proveedor de almacén de claves Azure Key Vault:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Si utiliza un proveedor de almacén de certificados de Windows:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

Si utiliza un proveedor de almacén de claves de Java:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Ejemplo de inserción de datos

En este ejemplo se inserta una fila en la tabla Patients. Tenga en cuenta los siguientes aspectos:

- No existe nada específico al cifrado en el código de ejemplo. Microsoft JDBC driver para SQL Server detecta y cifra automáticamente los parámetros que tienen como destino las columnas cifradas. Este comportamiento hace que el cifrado se realice de manera transparente en la aplicación.
- Los valores insertados en las columnas de la base de datos, incluidas las columnas cifradas, se pasan como parámetros mediante SQLServerPreparedStatement. Aunque el uso de parámetros es opcional al enviar valores a las columnas no cifradas (aunque es altamente recomendable porque ayuda a evitar la inyección de código SQL), es necesario para los valores que tienen como destino las columnas cifradas. Si los valores insertados en las columnas cifradas se pasaron como literales incrustados en la instrucción de consulta, la consulta produciría un error porque el controlador no podría determinar los valores de las columnas cifradas de destino y no cifraría los valores. Como resultado, el servidor los rechazará considerándolos incompatibles con las columnas cifradas.
- Todos los valores impresos por el programa estarán en texto sin formato, ya que Microsoft JDBC Driver for SQL Server descifrará los datos que se han recuperado de las columnas cifradas.
- Si está realizando una búsqueda con una cláusula WHERE, el valor utilizado en la cláusula WHERE debe pasarse como un parámetro para que el controlador pueda cifrarlo de forma transparente antes de enviarlo a la base de datos. En el ejemplo siguiente, el SSN se pasa como parámetro, pero el apellido se pasa como literal, ya que LastName no está cifrado.
- El método setter usado para el parámetro que tiene como destino la columna SSN es setString (), que se asigna al tipo de datos CHAR/VARCHAR SQL Server. Si el método establecedor que se ha usado para este parámetro es setNString(), que se asigna a nchar o nvarchar, la consulta producirá un error, ya que Always Encrypted no admite conversiones de valores cifrados de nchar o nvarchar a valores cifrados char o varchar.

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>Ejemplo de la recuperación de datos de texto sin formato

En el siguiente ejemplo se muestra el filtrado de datos en función de valores cifrados, así como la recuperación de datos de texto sin formato de las columnas cifradas. Tenga en cuenta los siguientes aspectos:

- El valor que se ha usado en la cláusula WHERE para filtrar por la columna SSN necesita pasarse como un parámetro, de forma que Microsoft JDBC Driver for SQL Server pueda cifrarlo de manera transparente antes de enviarlo a la base de datos.
- Todos los valores impresos por el programa estarán en texto sin formato, ya que Microsoft JDBC Driver for SQL Server descifrará los datos que se han recuperado de las columnas SSN y BirthDate de manera transparente.

> [!NOTE]
> Si las columnas están cifradas mediante el cifrado determinista, las consultas pueden realizar comparaciones de igualdad en ellas. Para obtener más información, vea [Selección del cifrado determinista o aleatorio de Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-encrypted-data-example"></a>Ejemplo de la recuperación de los datos cifrados

Si Always Encrypted no está habilitado, una consulta todavía puede recuperar datos de las columnas cifradas, siempre y cuando la consulta no tenga parámetros que tengan como destino las columnas cifradas.

En el siguiente ejemplo se ilustra la recuperación de datos binarios cifrados de las columnas cifradas. Tenga en cuenta los siguientes aspectos:

- Como Always Encrypted no está habilitado en la cadena de conexión, la consulta devolverá valores cifrados de SSN y BirthDate como matrices de bytes (el programa convierte los valores en cadenas).
- Una consulta que recupera datos de columnas cifradas con Always Encrypted deshabilitado puede tener parámetros, siempre y cuando ninguno de ellos tenga como destino una columna cifrada. La siguiente consulta filtra por LastName, que no está cifrado en la base de datos. Si la consulta ha filtrado por SSN o BirthDate, esta producirá un error.

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitar problemas comunes al consultar columnas cifradas

En esta sección se describen las categorías comunes de errores al consultar columnas cifradas de aplicaciones Java y algunas instrucciones sobre cómo evitarlos.

### <a name="unsupported-data-type-conversion-errors"></a>Errores de conversión de tipos de datos no compatibles

Always Encrypted admite algunas conversiones para los tipos de datos cifrados. Vea [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obtener una lista detallada de las conversiones de tipos compatibles. Esto es lo que puede hacer para evitar los errores de conversión de tipos de datos. Asegúrese de lo siguiente:

- se usan los métodos de establecedor adecuados al pasar valores para los parámetros que tienen como destino las columnas cifradas. Asegúrese de que el tipo de datos SQL Server del parámetro sea exactamente el mismo que el tipo de la columna de destino o una conversión del tipo de datos SQL Server del parámetro al tipo de destino de la columna. Los métodos de API se han agregado a las clases SQLServerPreparedStatement, SQLServerCallableStatement y SQLServerResultSet para pasar parámetros correspondientes a tipos de datos de SQL Server específicos. Por ejemplo, si una columna no está cifrada, puede usar el método setTimestamp () para pasar un parámetro a datetime2 o a una columna DateTime. Pero cuando una columna está cifrada, tendrá que usar el método exacto que representa el tipo de la columna en la base de datos. Por ejemplo, use setTimestamp () para pasar valores a una columna datetime2 cifrada y use setDateTime () para pasar los valores a una columna de fecha y hora cifrada. Consulte [Always Encrypted referencia de API del controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obtener una lista completa de las nuevas API.
- la precisión y la escala de los parámetros que tienen como destino columnas de los tipos de datos numéricos y decimales de SQL Server debe ser la misma que la precisión y la escala configurada para la columna de destino. Los métodos de API se han agregado a las clases SQLServerPreparedStatement, SQLServerCallableStatement y SQLServerResultSet para aceptar la precisión y la escala, junto con los valores de los datos de los parámetros o columnas que representan los tipos de datos decimal y Numeric. Consulte [Always Encrypted referencia de API del controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) para obtener una lista completa de las API nuevas o sobrecargadas.  
- la escala o precisión de fracciones de segundo de los parámetros que tienen como destino las columnas de los tipos de datos datetime2, DateTimeOffset o Time SQL Server no es mayor que la precisión de fracciones de segundo y la escala de la columna de destino en las consultas que modifican los valores de la columna de destino. . Los métodos de API se han agregado a las clases SQLServerPreparedStatement, SQLServerCallableStatement y SQLServerResultSet para aceptar la escala o precisión de fracciones de segundo junto con valores de datos para los parámetros que representan estos tipos de datos. Para obtener una lista completa de las API nuevas o sobrecargadas, consulte [Always Encrypted referencia de la API del controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

### <a name="errors-due-to-incorrect-connection-properties"></a>Errores debidos a propiedades de conexión incorrectas

En esta sección se describe cómo configurar correctamente las opciones de conexión para utilizar datos de Always Encrypted. Dado que los tipos de datos cifrados admiten conversiones limitadas, los valores de conexión **sendTimeAsDatetime** y **sendStringParametersAsUnicode** necesitan una configuración adecuada cuando se usan columnas cifradas. Asegúrese de lo siguiente:

- la opción de conexión [sendTimeAsDatetime](setting-the-connection-properties.md) está establecida en false al insertar datos en las columnas de tiempo cifradas. Para obtener más información, vea [Configurar el modo en que los valores java.sql.Time se envían al servidor](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- la configuración de conexión [sendStringParametersAsUnicode](setting-the-connection-properties.md) se establece en true (o se deja como valor predeterminado) al insertar datos en columnas cifradas CHAR/VARCHAR/VARCHAR (Max).

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Errores debidos a pasar texto sin formato en lugar de valores cifrados

Cualquier valor que tenga como destino una columna cifrada necesita cifrarse dentro de la aplicación. Un intento para insertar, modificar o filtrar mediante un valor de texto sin formato en una columna cifrada producirá un error similar a este:

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Para evitar dichos errores, asegúrese de que:

- Always Encrypted esté habilitado para las consultas de la aplicación que tengan como destino las columnas cifradas (para la cadena de conexión o para una consulta específica).
- los parámetros y las instrucciones preparadas se usan para enviar datos que tienen como destino columnas cifradas. En el ejemplo siguiente se muestra una consulta que filtra de manera incorrecta mediante un literal o constante en una columna cifrada (SSN), en lugar de pasar el literal dentro de un parámetro. Se producirá un error en esta consulta:

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Forzar el cifrado en parámetros de entrada

La característica forzar cifrado aplica el cifrado de un parámetro cuando se usa Always Encrypted. Si se usa Forzar cifrado y SQL Server indica al controlador que no hace falta cifrar el parámetro, la consulta que utilice este último generará un error. Esta propiedad confiere una protección adicional frente a ataques contra la seguridad que utilice un servidor SQL Server comprometido que proporcione metadatos de cifrado incorrectos al cliente, lo cual podría provocar la divulgación de datos. Los métodos set * de las clases SQLServerPreparedStatement y SQLServerCallableStatement y los métodos\* Update de la clase SQLServerResultSet se sobrecargan para aceptar un argumento booleano para especificar la configuración de forzar cifrado. Si el valor de este argumento es false, el controlador no forzará el cifrado en los parámetros. Si forzar cifrado está establecido en true, el parámetro de consulta solo se envía si la columna de destino está cifrada y Always Encrypted está habilitada en la conexión o en la instrucción. El uso de esta propiedad proporciona una capa adicional de seguridad, lo que garantiza que el controlador no envía datos erróneamente a SQL Server como texto no cifrado cuando se espera que esté cifrado.

Para obtener más información sobre los métodos SQLServerPreparedStatement y SQLServerCallableStatement que se sobrecargan con la configuración de forzar cifrado, consulte [Always Encrypted referencia de API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) .  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controlar el impacto en el rendimiento de Always Encrypted

Como Always Encrypted es una tecnología de cifrado del lado cliente, la mayoría de las sobrecargas de rendimiento se observan en el lado cliente y no en la base de datos. Además del costo de las operaciones de cifrado y descifrado, los demás orígenes de las sobrecargas de rendimiento en el lado cliente son:

- Ciclos de ida y vuelta adicionales a la base de datos para recuperar metadatos para los parámetros de consulta.
- Llamadas a un almacén de claves maestras de columna para tener acceso a una clave maestra de columna.

En esta sección se describen las optimizaciones integradas de rendimiento en Microsoft JDBC Driver for SQL Server y la forma en que puede controlar el impacto de los dos factores anteriores en el rendimiento.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controlar los ciclos de ida y vuelta para recuperar metadatos para los parámetros de consulta

De forma predeterminada, si Always Encrypted está habilitado para una conexión, el controlador llamará a [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta con parámetros, al pasar la instrucción de consulta (sin ningún valor de parámetro) a SQL Server. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analiza la instrucción de consulta para averiguar si algún parámetro necesita cifrarse y, de ser así, devuelve la información relacionada con el cifrado que permitirá al controlador cifrar los valores de parámetro para cada uno de ellos. Este comportamiento garantiza un alto nivel de transparencia para la aplicación cliente. Siempre que la aplicación use parámetros para pasar valores que tienen como destino columnas cifradas al controlador, la aplicación (y el desarrollador de aplicaciones) no necesita saber qué consultas tienen acceso a las columnas cifradas.

### <a name="setting-always-encrypted-at-the-query-level"></a>Configurar Always Encrypted en el nivel de consulta

Para controlar el impacto en el rendimiento a la hora de recuperar metadatos de cifrado para las consultas con parámetros, puede habilitar Always Encrypted para las consultas individuales en lugar de configurarlo para la conexión. De esta manera, puede estar seguro de que sys.sp_describe_parameter_encryption se invoca solo para las consultas que sabe que incluyen parámetros que tienen como destino las columnas cifradas. Pero tenga en cuenta que haciendo esto reduce la transparencia del cifrado: si cambia las propiedades de cifrado de las columnas de la base de datos, puede que necesite cambiar el código de la aplicación para alinearlo con los cambios de esquema.

Para controlar el comportamiento de Always Encrypted de las consultas individuales, debe configurar objetos de instrucción individuales pasando una enumeración, SQLServerStatementColumnEncryptionSetting, que especifica cómo se enviarán y recibirán los datos al leer y escribir columnas cifradas para esa instrucción específica. A continuación se exponen unas directrices prácticas:

- Si la mayoría de las consultas que una aplicación cliente envía a través de una conexión de base de datos acceden a columnas cifradas, use las instrucciones siguientes:

    - Establezca la palabra clave de la cadena de conexión **columnEncryptionSetting** en **Enabled**.
    - Establezca SQLServerStatementColumnEncryptionSetting.Disabled para consultas individuales que no tengan acceso a ninguna columna cifrada. Esta opción deshabilitará la llamada a sys.sp_describe_parameter_encryption así como un intento de descifrar cualquier valor del conjunto de resultados.
    - Establezca SQLServerStatementColumnEncryptionSetting.ResultSet para consultas individuales que no cuenten con ningún parámetro que requiera cifrado, pero que recuperen datos de columnas cifradas. Esta opción deshabilitará la llamada a sys.sp_describe_parameter_encryption y el cifrado de parámetros. La consulta podrá descifrar los resultados de las columnas de cifrado.

- Si la mayoría de las consultas que una aplicación cliente envía a través de una conexión de base de datos no acceden a columnas cifradas, use las instrucciones siguientes:

    - Establezca la palabra clave de la cadena de conexión **columnEncryptionSetting** en **Disabled**.
    - Establezca SQLServerStatementColumnEncryptionSetting.Enabled para consultas individuales que no cuenten con ningún parámetro que se tenga que cifrar. Esta opción habilitará la llamada a sys.sp_describe_parameter_encryption así como el descifrado de cualquier resultado de la consulta que se recupere de las columnas cifradas.
    - Establezca SQLServerStatementColumnEncryptionSetting.ResultSet para consultas que no cuenten con ningún parámetro que requiera cifrado, pero que recuperen datos de columnas cifradas. Esta opción deshabilitará la llamada a sys.sp_describe_parameter_encryption y el cifrado de parámetros. La consulta podrá descifrar los resultados de las columnas de cifrado.

La configuración de SQLServerStatementColumnEncryptionSetting no se puede usar para omitir el cifrado y obtener acceso a los datos de texto no cifrado. Para obtener más información sobre cómo configurar el cifrado de columnas en una instrucción, vea [Always Encrypted referencia de API para el controlador JDBC](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

En el ejemplo siguiente, Always Encrypted está deshabilitado para la conexión de base de datos. La consulta que ejecuta la aplicación tiene un parámetro que tiene como destino la columna LastName que no está cifrada. La consulta recupera datos de las columnas SSN y BirthDate que están cifradas. En este caso, no es necesario llamar a sys.sp_describe_parameter_encryption para recuperar los metadatos de cifrado. Pero el descifrado de los resultados de la consulta necesita habilitarse, de forma que la aplicación pueda recibir valores de texto sin formato de las dos columnas cifradas. La configuración SQLServerStatementColumnEncryptionSetting. ResultSet se usa para garantizar que.

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>;" 
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>" 
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="column-encryption-key-caching"></a>Almacenamiento en memoria caché de claves de cifrado de columnas

Para reducir el número de llamadas a un almacén de claves maestras de columna para descifrar las claves de cifrado de columnas, Microsoft JDBC Driver for SQL Server almacena en memoria caché las claves de cifrado de columnas de texto sin formato en la memoria. Después de recibir el valor cifrado de la clave de cifrado de columnas de los metadatos de la base de datos, el controlador primero intenta encontrar la clave de cifrado de columnas de texto sin formato, que corresponde al valor de clave cifrado. El controlador llama al almacén de claves que contiene la clave maestra de columna, solo si no puede encontrar el valor cifrado de la clave de cifrado de columnas en la memoria caché.

Puede configurar un valor de período de vida para las entradas de clave de cifrado de columnas en la memoria caché mediante la API, setColumnEncryptionKeyCacheTtl (), en la clase SQLServerConnection. El valor predeterminado del período de vida de las entradas de clave de cifrado de columnas en la memoria caché es de dos horas. Para desactivar el almacenamiento en caché, use un valor de 0. Para establecer un valor de período de vida, use la siguiente API:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Por ejemplo, para establecer un valor de período de vida de 10 minutos, use:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Solo se admiten días, horas, minutos o segundos como unidad de tiempo.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Copiar datos cifrados con SQLServerBulkCopy

Con SQLServerBulkCopy, puede copiar datos que ya están cifrados y almacenados en una tabla a otra, sin descifrarlos. Para realizar esto:

- Asegúrese de que la configuración de cifrado de la tabla de destino es idéntica a la configuración de la tabla de origen. En particular, ambas tablas debe tener las mismas columnas cifradas y estas deben cifrarse mediante los mismos tipos de cifrado y las mismas claves de cifrado. Si alguna de las columnas de destino se cifra de una manera diferente a la de su columna de origen correspondiente, no podrá descifrar los datos de la tabla de destino después de la operación de copia. Los datos estarán dañados.
- Configure ambas conexiones de base de datos, a la tabla de origen y a la tabla de destino, sin tener habilitado Always Encrypted.
- Establezca la opción allowEncryptedValueModifications. Para obtener más información, vea [uso de la copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Tenga cuidado al especificar AllowEncryptedValueModifications ya que esta opción puede provocar daños en la base de datos dado que Microsoft JDBC Driver for SQL Server no comprueba si los datos están realmente cifrados, o si se han cifrado correctamente mediante la misma clave, algoritmo y tipo de cifrado que la columna de destino.

## <a name="see-also"></a>Consulte también

[Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
