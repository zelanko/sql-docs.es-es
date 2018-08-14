---
title: Notas de la versión para el controlador JDBC
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10f14eedb1a74f74cb1ee055a247a96671224ce0
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662467"
---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de la versión para el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-70-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 7.0 para SQL Server

La 7.0 de Microsoft JDBC Driver para SQL Server es totalmente compatible con la especificación de API de JDBC 4.2. Los archivos JAR en el paquete 7.0 se denominan según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-7.0.0.jre10.jar desde el paquete 7.0 debe utilizarse con Java 10.

### <a name="support-for-jdk-10"></a>Compatibilidad con JDK 10

Ahora es compatible con Java Development Kit (JDK) versión 10.0, además de JDK 1.8 la 7.0 de Microsoft JDBC Driver para SQL Server. Esta actualización también expone el conductor 'Automatic-Module-Name"como `com.microsoft.sqlserver.jdbc` a través de su archivo de manifiesto.

### <a name="support-for-spatial-datatypes"></a>Compatibilidad con tipos de datos espaciales

Ahora, la 7.0 de Microsoft JDBC Driver para SQL Server proporciona compatibilidad con tipos de datos de SQL Server espacial 'Geography' y 'Geometry'. Para obtener información acerca de las propiedades de celda y su uso, vea [aquí](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>Implementación de JDBC 4.3 y las API de java.sql.Connection beginRequest() y endRequest()

La 7.0 de Microsoft JDBC Driver para SQL Server ahora implementa `beginRequest()` y `endRequest()` API desde `java.sql.Connection` clase. Estas API se introdujeron con las especificaciones de JDBC 4.3 y JDK 9. Para obtener más información sobre la implementación del controlador de estas API, consulte [aquí](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Compatibilidad con Clasificación y detección de datos de SQL

La 7.0 de Microsoft JDBC Driver para SQL Server proporciona compatibilidad con la característica 'clasificación y detección de datos SQL' con cualquier base de datos de destino que admita esta característica. El controlador ahora expone `SQLServerResultSet.getSensitivityClassification()` API para extraer esta información desde el conjunto de resultados capturado.

Para obtener más información sobre cómo usar esta característica con el controlador JDBC, consulte el ejemplo [aquí](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-new-connection-property-usebulkcopyforbatchinsert"></a>Agrega la nueva propiedad de conexión: useBulkCopyForBatchInsert

La 7.0 de Microsoft JDBC Driver para SQL Server presenta una nueva propiedad de conexión, 'useBulkCopyForBatchInsert', que solo se admite para **Azure Data Warehouse**.

Esta propiedad es **deshabilitado** forma predeterminada y puede habilitarse para aumentar el rendimiento de las aplicaciones de usuario al insertar grandes cantidades de datos en Azure Data Warehouse. Habilitación de esta propiedad cambia el comportamiento de las operaciones de inserción por lotes para cambiar a las operaciones de copia masiva con los datos de proporcionada por el usuario. Para obtener más información acerca de esta propiedad y de las opciones disponibles, consulte [aquí](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-new-connection-property-cancelquerytimeout"></a>Agrega la nueva propiedad de conexión: cancelQueryTimeout

Nueva propiedad de conexión, se presentan la 7.0 de Microsoft JDBC Driver para SQL Server `cancelQueryTimeout`, cancelar `queryTimeout` en `java.sql.Connection` y `java.sql.Statement` objetos.

### <a name="added-azure-key-vault-provider-constructors"></a>Constructores de proveedor de almacén de claves de Azure se ha agregado

La 7.0 de Microsoft JDBC Driver para SQL Server vuelve a introducir un constructor que se han quitado previamente, para `SQLServerColumnEncryptionAzureKeyVaultProvider`, mediante un método personalizado que se implementa a través de autenticación permitido `SQLServerKeyVaultAuthenticationCallback` para capturar un token de acceso.

Los nuevos constructores tienen el debajo de definición:

```java
/* This constructor is added to provide backwards compatibility with 6.0
* version of the driver. It is marked deprecated for removal in next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New Constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-adal4j-version-to-160"></a>Versión actualizada de ADAL4J a la versión 1.6.0

La 7.0 de Microsoft JDBC Driver para SQL Server ha actualizado su dependencia de maven de azure-activedirectory-library-for-java (ADAL4J) a la versión 1.6.0. Para obtener más información sobre las dependencias, consulte [esta página](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.4 para SQL Server

Microsoft JDBC Driver 6.4 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete de 6,4 denominación de compatibilidad de la versión de Java. Por ejemplo, se debe usar el archivo mssql-jdbc-6.4.0.jre8.jar desde el paquete de 6,4 con Java 8.

### <a name="support-for-jdk-9"></a>Compatibilidad con JDK 9

Compatibilidad con Java Development Kit (JDK) versión 9.0, además de con JDK 8.0 y 7.0.

### <a name="jdbc-43-compliance"></a>Cumplimiento

Compatibilidad con la especificación Java Database Connectivity API 4.3, además de con 4.1 y 4.2. Los métodos de API de JDBC 4.3 se agregarán pero aún no implementados. Para detalles, vea [JDBC 4.3 Compliance for the JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md) (Cumplimiento de JDBC 4.3 para el controlador JDBC).

### <a name="added-new-connection-property-sslprotocol"></a>Agrega la nueva propiedad de conexión: sslProtocol

Agrega una nueva propiedad de conexión que permite a los usuarios especificar la palabra clave de protocolo TLS. Los valores posibles son: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2". Consulte [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) para obtener más información.

### <a name="deprecated-connection-property-fipsprovider"></a>Propiedad de conexión en desuso: fipsProvider

Propiedad de conexión "fipsProvider" se quita de la lista de propiedades de conexión aceptada. Ver los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).

### <a name="added-connection-properties-for-specifying-custom-trustmanager"></a>Propiedades de conexión se ha agregado para la especificación de TrustManager personalizado

- El controlador ahora admite la especificación de TrustManager personalizado con las propiedades de conexión "trustManagerClass" y Esto permite la especificación dinámica de un conjunto de certificados que son de confianza en cada conexión sin modificar la configuración global para el entorno de JVM.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters-tvp"></a>- Se ha agregado compatibilidad con tipos de datos DATETIME y SMALLDATETIME al utilizar parámetros con valores de tabla (TVP).

El controlador ahora es compatible con los tipos de datos DATETIME y SMALLDATETIME al usar parámetros con valores de tabla (TVP).

### <a name="added-support-for-sqlvariant-datatype"></a>Se agregó compatibilidad para el tipo de datos sql_variant

El controlador JDBC ahora admite los tipos de datos sql_variant para su uso con SQL Server. Sql_variant también es compatible con características como parámetros con valores de tabla (TVP) y BulkCopy con siguientes limitaciones:

1. Para los valores de fecha: al usar TVP para rellenar una tabla que contiene los valores de datetime/smalldatetime/date almacenados en la columna sql_variant, llamar a métodos getDateTime()/getSmallDateTime()/getDate() en resultset no funciona y se produce la excepción siguiente:  `java java.lang.String cannot be cast to java.sql.Timestamp` Solución alternativa: use los métodos "getString()" o "getObject()" en su lugar.

2. Uso de TVP con sql_variant para valores null

Si usa TVP para rellenar una tabla y enviar el valor NULL al tipo de columna sql_variant, encontrará una excepción como Insertar valor NULL con tipo de columna sql_variant en TVP no se admite actualmente.

### <a name="implemented-prepared-statement-metadata-caching"></a>Almacenamiento en caché de metadatos de instrucción preparado para el controlador JDBC

Ha implementado el controlador JDBC de caché de metadatos de instrucción preparado para mejorar el rendimiento. - El controlador ahora es compatible con almacenamiento en caché de los metadatos de la instrucción preparada en el controlador con las propiedades de conexión "disableStatementPooling" y Esta característica está deshabilitada de forma predeterminada. Puede obtener más información [aquí](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

### <a name="added-support-for-aad-integrated-authentication-on-linuxmac"></a>Se ha agregado compatibilidad para la autenticación integrada de AAD en Linux o Mac

El controlador JDBC ahora además admite la autenticación integrada de Azure Active Directory en todos los sistemas operativos compatibles (Windows/Linux/Mac) con Kerberos. Como alternativa, en sistemas de operativos Windows, los usuarios pueden autenticarse con sqljdbc_auth.dll.

### <a name="updated-adal4j-version-to-140"></a>Versión actualizada de ADAL4J para 1.4.0

El controlador JDBC actualizó su dependencia de maven de azure-activedirectory-library-for-java (ADAL4J) a la versión 1.4.0. Para más información sobre las dependencias, consulte [aquí](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.2 para SQL Server

Microsoft JDBC Driver 6.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete 6.2 se denominan según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-6.2.2.jre8.jar desde el paquete 6.2 se recomienda para su uso con Java 8.

> [!NOTE]  
> Se encontró un problema con la mejora del almacenamiento en caché de metadatos en la RTW de 6.2 JDBC publicado el 29 de junio de 2017. Se ha revertido la mejora y de 17 de julio de 2017 se han publicado nuevos archivos JAR (versión 6.2.1). 
>
> Se realizó otra mejora para actualizar la versión de la biblioteca dependiente de Azure Key Vault a 1.0.0, y se han publicado nuevos archivos JAR (versión 6.2.2) de 19 de octubre de 2017.
>
> Descargar las actualizaciones más recientes en JDBC Driver 6.2 en [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), y [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Actualice sus proyectos para usar el 6.2.2 archivos JAR de versión. Vea notas de la versión [v6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) y [v6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) para obtener más detalles.

### <a name="azure-active-directory-aad-support-for-linux"></a>Soporte técnico de Azure Active Directory (AAD) para Linux

Conectar sus aplicaciones de Linux a Azure SQL Database mediante autenticación de AAD a través de métodos de token de acceso y nombre de usuario/contraseña.

### <a name="federal-information-processing-standard-fips-enabled-jvms"></a>Información de procesamiento estándar federal (FIPS) habilitado JVM

Ahora se puede usar el controlador JDBC en JVM que se ejecutan en modo de cumplimiento de FIPS 140 para satisfacer el cumplimiento de normas y estándares federales.

### <a name="kerberos-authentication-improvements"></a>Autenticación Kerberos

El controlador JDBC ahora es compatible con:

- Método de entidad de seguridad y la contraseña para las aplicaciones donde la configuración de Kerberos no puede ser modificado o no se puede recuperar un token nuevo o una tabla de claves. Este método puede usarse para autenticar a un servidor de SQL que solo permite la autenticación Kerberos.
- Autenticación entre dominios Kerberos mediante la autenticación integrada de Kerberos sin tener que establecer explícitamente el SPN del servidor. El controlador ahora calcula automáticamente el dominio KERBEROS incluso cuando no ha facilitado.
- Delegación restringida de Kerberos mediante la aceptación de suplantar las credenciales de usuario como un objeto de credenciales de GSS a través del origen de datos. Esta credencial suplantada, a continuación, se usa para establecer una conexión de Kerberos.

### <a name="added-timeouts"></a>Tiempo agregado

El controlador JDBC ahora admite los siguientes tiempos de espera configurables que se pueden cambiar según las necesidades de su aplicación:

- Tiempo de espera de consulta para controlar el número de segundos que deben transcurrir antes de que se produce un tiempo de espera cuando se ejecuta una consulta.
- Tiempo de espera de socket para especificar el número de milisegundos que transcurrirán antes de que se produce un tiempo de espera en un socket de lectura o acepta.

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.1 para SQL Server

La 6.1 de Microsoft JDBC Driver para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Esta es la versión inicial de código abierto del controlador JDBC y contiene los archivos de mssql-jdbc-6.1.0.jre7.jar mssql-jdbc-6.1.0.jre8.jar, que corresponden a la compatibilidad de versiones de Java.

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.0 para SQL Server

Microsoft JDBC Driver 6.0 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete 6.0 se nombran según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar del paquete 6.0 es compatible con JDBC API 4.2. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el derecho sqljdbc42.jar o sqljdbc41.jar, ejecute las siguientes líneas de código. Si el resultado es "versión del controlador: 6.0.7507.100", tiene el paquete de JDBC Driver 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

Compatibilidad con la característica Always Encrypted publicada recientemente en SQL Server 2016, una nueva característica de seguridad que garantiza que los datos confidenciales no se vean nunca como texto no cifrado en una instancia de SQL Server. Always Encrypted funciona mediante el cifrado transparente de los datos en la aplicación, de modo que SQL Server solo se ocupará de los datos cifrados y no los valores de texto no cifrado. Aunque la instancia de SQL o el equipo host estén en peligro, lo único que el atacante puede obtener es texto cifrado de datos confidenciales. Para información detallada, vea [Usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-name-idn"></a>Nombre de dominio internacionalizado (IDN)

Compatibilidad con nombres de dominio internacionalizados (IDN) para nombres del servidor. Para obtener información detallada, consulte utilizando nombres de dominio internacionales en el [características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md) página.

### <a name="parameterized-query"></a>Consulta con parámetros

Ahora se admite la recuperación de metadatos de parámetros con instrucciones preparadas para consultas complejas, como subconsultas o combinaciones. Tenga en cuenta que esta mejora solo está disponible cuando se usa SQL Server 2012 y versiones más recientes.

### <a name="azure-active-directory-aad"></a>Azure Active Directory (AAD)

Nueva característica: Azure Active Directory (AAD). La autenticación de AAD es un mecanismo que permite conectar con Azure SQL Database v12 mediante identidades en AAD. Use la autenticación de AAD para administrar identidades de usuarios de base de datos de forma centralizada y como alternativa a la autenticación de SQL Server. El controlador JDBC 6.0 permite especificar las credenciales de AAD en la cadena de conexión de JDBC para conectarse a Azure SQL DB. Para obtener información detallada, consulte la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) página.

### <a name="table-valued-parameters"></a>Parámetros con valores de tabla

Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla puede operar utilizando Transact-SQL. Vea [Usar parámetros con valores de tabla](../../connect/jdbc/using-table-valued-parameters.md)

### <a name="alwayson-availability-groups-ag"></a>Grupos de disponibilidad (AG) AlwaysOn

Mejora: grupos de disponibilidad Always On (AG). El controlador ahora admite conexiones transparentes a grupos de disponibilidad El controlador detecta rápidamente la topología Always On actual de la infraestructura de servidor y conecta con el servidor activo actual de forma transparente.

## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.2 para SQL Server y versiones posteriores

Microsoft JDBC Driver 4.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete de 4.2 se nombran según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar desde el paquete de 4.2 es compatible con JDBC API 4.2. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el derecho sqljdbc42.jar o sqljdbc41.jar, ejecute las siguientes líneas de código. Si el resultado es "versión del controlador: 4.2.6420.100", tiene el paquete de JDBC Driver 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Compatibilidad con JDK 8

Compatibilidad con Java Development Kit (JDK) versión 8.0, además de con JDK 7.0, 6.0 y 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Cumplimiento con JDBC 4.1 y 4.2

Compatibilidad con las especificaciones de la API Java Database Connectivity 4.1 y 4.2, además de 4.0. Para obtener más información, consulte [JDBC 4.1 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [JDBC 4.2 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Copia masiva

Se usa la característica de copia masiva para copiar rápidamente grandes cantidades de datos en tablas o vistas en bases de datos de SQL Server. Vea [Uso de la copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opción de reversión de transacción de XA

Se han agregado nuevas opciones de tiempo de espera para la reversión automática existente de transacciones no preparadas. [Descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md)

### <a name="new-kerberos-principal-connection-property"></a>Nueva propiedad de conexión de entidad de seguridad de Kerberos

Se ha agregado una nueva propiedad de conexión para facilitar la flexibilidad con las conexiones de Kerberos. Para información detallada, vea [Using Kerberos Integrated Authentication to Connect to SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) (Uso de la autenticación integrada de Kerberos para conectar con SQL Server).

## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.1 para SQL Server y versiones posteriores

### <a name="support-for-jdk-7"></a>Compatibilidad con JDK 7

Compatibilidad para Java Development Kit (JDK) versión 7.0, además de JDK 6.0 y 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium no es compatible con las aplicaciones de JDBC Driver 6.4, 6.0, 4.2 y 4.1

No se admite la ejecución de Microsoft JDBC Driver 6.4, 6.0, 4.2 y 4.1 para aplicaciones de SQL Server en un equipo Itanium.

## <a name="see-also"></a>Ver también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
