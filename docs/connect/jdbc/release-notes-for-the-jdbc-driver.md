---
title: Notas de la versión para el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 083eda191d51ec7043f24511d03c90beff9bfe84
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657740"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Notas de la versión para el controlador JDBC de Microsoft

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este artículo enumeran las versiones de la _Microsoft JDBC Driver para SQL Server_. Para cada versión de lanzamiento, los cambios se denominado y se describe.

## <a name="721"></a>7.2.1

### <a name="compliance"></a>Cumplimiento

11 de febrero de 2019

| Cambio de cumplimiento | Detalles |
| :---------------- | :------ |
| Descargue las actualizaciones más recientes para 7.2 del controlador JDBC. | &bull; &nbsp; [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1)<br/>&bull; &nbsp; [Central de maven](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente compatible con la especificación de API de JDBC 4.2. | Los archivos JAR en el paquete 7.2 se denominan según la compatibilidad de la versión de Java.<br/><br/>Por ejemplo, el archivo mssql-jdbc-7.2.1.jre11.jar desde el paquete 7,2 debe utilizarse con Java 11. |
| Compatible con Java Development Kit (JDK) versión 11.0, además de con JDK 1.8. | Ahora es compatible con Java Development Kit (JDK) versión 11.0, además de JDK 1.8 7.2 de Microsoft JDBC Driver para SQL Server. |
| &nbsp; | &nbsp; |

> [!NOTE]
> Se encontró un problema con la instrucción SQL de análisis en el controlador JDBC 7.2 versión para Web (RTW) publicado en el 31 de enero de 2019. Se ha deshecho el cambio y nuevos archivos JAR (versión 7.2.1) publicada el 11 de febrero de 2019.
>
> Actualizar los proyectos para usar el 7.2.1 archivos JAR de versión. Para obtener más información, vea notas de la versión [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1).

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Active Directory _Managed Service Identity_ autenticación (MSI)

| Cambio MSI | Detalles |
| :--------- | :------ |
| Admite el modo de autenticación de Active Directory Managed Service Identity (MSI). | Este modo de autenticación es aplicable en los recursos de Azure con compatibilidad para la característica "Identity" habilitada.<br/><br/>Ambos tipos de identidades de sistema administrada (MSI) son compatibles con el controlador para adquirir **accessToken** para establecer una conexión segura. |
| Obtener más información y una aplicación de ejemplo para usar este modo de autenticación. | Consulte [Conectarse mediante la autenticación de Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md). |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>Presenta _iniciativa Open de puerta de enlace de servicio_ soporte técnico (OSGi)

| Cambio de OSGi | Detalles |
| :---------- | :------ |
| **DataSourceFactory** agregado de implementación. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **Activador** agregado de implementación. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>Presenta _SQLServerError_ API

| Cambio de la API de error | Detalles |
| :--------------- | :------ |
| API de SQLServerError. | Captador de API para recuperar los detalles adicionales sobre el error generado en el servidor.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| Detalles adicionales. | Consulte [Control de errores](../../connect/jdbc/handling-errors.md). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>Se ha actualizado la versión 1.6.3 de _Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java_.

| Cambio en ADAL4J | Detalles |
| :------------ | :------ |
| Actualiza su dependencia de Maven en ADAL4J a versión 1.6.3. | &nbsp; |
| Presenta _en tiempo de ejecución del cliente de Java para AutoRest_ como una dependencia de Maven, versión 1.6.5. | &nbsp; |
| Detalles adicionales. | Consulte [Feature dependencies of the Microsoft JDBC Driver for SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) (Dependencias de características de Microsoft JDBC Driver para SQL Server). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>Actualizar _SDK de Microsoft Azure Key Vault para Java_, versión 1.2.0

| Cambio del SDK de Key Vault | Detalles |
| :------------------- | :------ |
| Actualice su dependencia de Maven en _SDK de Microsoft Azure Key Vault para Java_ a la versión 1.2.0. | &nbsp; |
| Presenta el _SDK de Microsoft Azure para Key Vault WebKey_ como dependencia de Maven, versión 1.2.0. | &nbsp; |
| Detalles adicionales. | Consulte [Feature dependencies of the Microsoft JDBC Driver for SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) (Dependencias de características de Microsoft JDBC Driver para SQL Server). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos

| Problemas conocidos | Detalles |
| :----------- | :------ |
| Consultas parametrizadas en ciertos casos. | Se publicará una actualización de la versión 7.2, que será v7.2.1, en febrero de 2019 para resolver este problema. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

7.0 de Microsoft JDBC Driver para SQL Server es totalmente compatible con la especificación de API de JDBC 4.2. Los archivos JAR en el paquete 7.0 se denominan según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-7.0.0.jre10.jar desde el paquete 7.0 debe utilizarse con Java 10.

### <a name="support-for-jdk-10"></a>Compatibilidad con JDK 10

Ahora es compatible con Java Development Kit (JDK) versión 10.0, además de JDK 1.8 7.0 de Microsoft JDBC Driver para SQL Server. Esta actualización también expone el controlador `Automatic-Module-Name` como `com.microsoft.sqlserver.jdbc` a través de su archivo de manifiesto.

### <a name="support-for-spatial-datatypes"></a>Compatibilidad con tipos de datos espaciales

7.0 de Microsoft JDBC Driver para SQL Server proporciona ahora compatibilidad con tipos de datos espaciales de SQL Server Geography y Geometry. Para obtener más información acerca de las API de tipo de datos espacial y cómo usarlas, vea [mediante los tipos de datos espaciales](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>Implementación de JDBC 4.3 y las API de java.sql.Connection beginRequest() y endRequest()

7.0 de Microsoft JDBC Driver para SQL Server ahora implementa `beginRequest()` y `endRequest()` API desde el `java.sql.Connection` clase. Estas API se introdujeron con las especificaciones de JDBC 4.3 y JDK 9. Para obtener más información sobre la implementación del controlador de estas API, consulte [cumplimiento de JDBC 4.3 para el controlador JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Compatibilidad con Clasificación y detección de datos de SQL

7.0 de Microsoft JDBC Driver para SQL Server proporciona compatibilidad para la detección de datos SQL y clasificación con cualquier base de datos de destino que admita esta característica. El controlador ahora expone `SQLServerResultSet.getSensitivityClassification()` API para extraer esta información de los capturados `ResultSet`.

Para obtener más información sobre cómo usar esta característica con el controlador JDBC, vea el ejemplo en [SQL clasificación y detección de datos](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>Agregar propiedad de conexión: useBulkCopyForBatchInsert

7.0 de Microsoft JDBC Driver para SQL Server presenta una nueva propiedad de conexión, `useBulkCopyForBatchInsert`. Esta propiedad solo se admite para Azure SQL Data Warehouse.

Esta propiedad está deshabilitada de forma predeterminada. Puede habilitarlo aumentar el rendimiento de las aplicaciones de usuario cuando la inserción de grandes cantidades de datos a Azure SQL Data Warehouse. Habilitación de esta propiedad cambia el comportamiento de las operaciones de inserción por lotes para cambiar a las operaciones de copia masiva con los datos proporcionados por el usuario. Para obtener más información acerca de esta propiedad y sus limitaciones, consulte [operación de inserción usando API de copia masiva para lote](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-connection-property-cancelquerytimeout"></a>Agregar propiedad de conexión: cancelQueryTimeout

7.0 de Microsoft JDBC Driver para SQL Server presenta una nueva propiedad de conexión, `cancelQueryTimeout`, cancelar `queryTimeout` en `java.sql.Connection` y `java.sql.Statement` objetos.

### <a name="added-azure-key-vault-provider-constructors"></a>Se ha agregado los constructores de Azure Key Vault Provider

7.0 de Microsoft JDBC Driver para SQL Server vuelve a introducir un constructor que se han quitado previamente, para `SQLServerColumnEncryptionAzureKeyVaultProvider`. Permite la autenticación a través de un método personalizado que se implementa a través de `SQLServerKeyVaultAuthenticationCallback` para capturar un token de acceso.

Los nuevos constructores tienen la siguiente definición:

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>Se ha actualizado la versión 1.6.0 de "Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java".

7.0 de Microsoft JDBC Driver para SQL Server ha actualizado su dependencia de Maven en "Microsoft Azure Active Directory Authentication Library (ADAL4J) para Java" a la versión 1.6.0. Para obtener más información acerca de las dependencias, consulte [dependencias de características de Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete de 6,4 denominación de compatibilidad de la versión de Java. Por ejemplo, se debe usar el archivo mssql-jdbc-6.4.0.jre8.jar desde el paquete de 6,4 con Java 8.

### <a name="support-for-jdk-9"></a>Compatibilidad con JDK 9

El controlador es compatible con JDK versión 9.0, además de JDK 8.0 y 7.0.

### <a name="jdbc-43-compliance"></a>Cumplimiento de JDBC 4.3

El controlador admite la especificación Java Database Connectivity API 4.3, además de con 4.1 y 4.2. Los métodos de API de JDBC 4.3 se agregarán pero aún no implementados. Para obtener más información, vea [JDBC 4.3 Compliance for the JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md) (Cumplimiento de JDBC 4.3 para JDBC Driver).

### <a name="added-connection-property-sslprotocol"></a>Agregar propiedad de conexión: sslProtocol

Una nueva propiedad de conexión permite a los usuarios especificar la palabra clave de protocolo TLS. Los valores posibles son: "TLS", "TLSv1", "TLSv1.1" y "TLSv1.2". Para obtener más información, consulte [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol).

### <a name="deprecated-connection-property-fipsprovider"></a>Propiedad de conexión en desuso: fipsProvider

La propiedad de conexión `fipsProvider` se quita de la lista de propiedades de conexión aceptada. Para obtener más información, consulte relacionado [solicitud de incorporación de cambios de GitHub](https://github.com/Microsoft/mssql-jdbc/pull/460).

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>Propiedades de la conexión se agregó para especificar un elemento TrustManager personalizado

El controlador ahora admite la especificación de un elemento TrustManager personalizado con agregado `trustManagerClass` y `trustManagerConstructorArg` las propiedades de conexión. Puede especificar dinámicamente un conjunto de certificados que son de confianza en cada conexión sin modificar la configuración global para el entorno de Java virtual machine (JVM).

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>Se agregó compatibilidad para datetime/smallDatetime en parámetros con valores de tabla

El controlador ahora admite los tipos de datos `datetime` y `smallDatetime` cuando se usa parámetros con valores de tabla (Tvp).

### <a name="added-support-for-the-sqlvariant-datatype"></a>Se agregó compatibilidad para el tipo de datos sql_variant

El controlador JDBC ahora admite `sql_variant` los tipos de datos para su uso con SQL Server. El `sql_variant` también se admite el tipo de datos con características como los Tvp y copia masiva con las siguientes limitaciones:

* **Para valores de fecha**: 

  Cuando se usa un TVP para rellenar una tabla que contiene `datetime`, `smalldatetime`, o `date` valores almacenados en un `sql_variant` columna, la llamada a la `getDateTime()`, `getSmallDateTime()`, o `getDate()` no funciona el método en el conjunto de resultados y inicia la siguiente excepción:

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  Como alternativa, use el `getString()` o `getObject()` método en su lugar.

* **Uso de TVP con sql_variant para valores nulos**:
  
  Si usas un TVP para rellenar una tabla y enviar un valor nulo a la `sql_variant` tipo de columna, que encontrará una excepción. Insertar un valor NULL con el tipo de columna `sql_variant` en un TVP no se admite actualmente.

### <a name="implemented-prepared-statement-metadata-caching"></a>Implementa el almacenamiento en caché de metadatos de instrucción preparada

Ha implementado el controlador JDBC de almacenamiento en caché de metadatos de instrucción preparada para mejorar el rendimiento. El controlador ahora admite el almacenamiento en caché los metadatos de instrucción preparada en el controlador con `disableStatementPooling` y `statementPoolingCacheSize` las propiedades de conexión. Esta característica está deshabilitada de forma predeterminada. Para obtener más información, consulte [preparado el almacenamiento en caché de metadatos de instrucción para el controlador JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md).

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Se ha agregado compatibilidad para la autenticación integrada de Azure AD en Linux o Mac

JDBC Driver ahora admite la autenticación integrada de Azure Active Directory (Azure AD) en todos los sistemas operativos compatibles (Windows/Linux/Mac) con Kerberos. Como alternativa, en sistemas operativos de Windows, los usuarios pueden autenticarse con sqljdbc_auth.dll.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>Se ha actualizado la versión 1.4.0 de "Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java".

El controlador JDBC actualizó su dependencia de Maven en "Microsoft Azure Active Directory Authentication Library (ADAL4J) para Java" a la versión 1.4.0. Para obtener más información acerca de las dependencias, consulte [dependencias de características de Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="62"></a>6.2

Microsoft JDBC Driver 6.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete 6.2 se denominan según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-6.2.2.jre8.jar desde el paquete 6.2 se recomienda para su uso con Java 8.

> [!NOTE]  
> Se encontró un problema con la mejora del almacenamiento en caché de metadatos en la RTW de 6.2 JDBC publicado el 29 de junio de 2017. Se ha revertido la mejora y de 17 de julio de 2017 se han publicado nuevos archivos JAR (versión 6.2.1). 
>
> Otra mejora había actualizado la versión de biblioteca dependiente de Azure Key Vault a 1.0.0 y 19 de octubre de 2017 se han publicado nuevos archivos JAR (versión 6.2.2).
>
> Descargar las actualizaciones más recientes para JDBC Driver 6.2 desde [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2), y [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver). Actualice sus proyectos para usar el 6.2.2 archivos JAR de versión. Para obtener más información, vea notas de la versión [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) y [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2).

### <a name="azure-ad-support-for-linux"></a>Soporte técnico de Azure AD para Linux

Conectar sus aplicaciones de Linux a Azure SQL Database mediante la autenticación de Azure AD a través de métodos de token de acceso y nombre de usuario/contraseña.

### <a name="fips-enabled-jvms"></a>Máquinas virtuales de Java compatibles con FIPS

Ahora se puede usar el controlador JDBC en JVM que se ejecutan en modo de compatibilidad 140 información procesamiento estándar Federal (FIPS) para cumplir los estándares federales de cumplimiento.

### <a name="kerberos-authentication-improvements"></a>Mejoras de autenticación de Kerberos

El controlador JDBC ahora es compatible con:

- Método de entidad de seguridad y la contraseña para las aplicaciones donde la configuración de Kerberos no se puede modificar o no puede recuperar un token nuevo o una tabla de claves. Este método puede usarse para la autenticación en una instancia de SQL Server que permite solo la autenticación Kerberos.
- Autenticación entre dominios que usa la autenticación integrada de Kerberos sin tener que establecer explícitamente el SPN del servidor. El controlador ahora calcula automáticamente el dominio Kerberos incluso cuando no se proporciona.
- Delegación restringida de Kerberos mediante la aceptación de suplantar las credenciales de usuario como un objeto de credenciales GSS a través del origen de datos. Esta credencial suplantada, a continuación, se usa para establecer una conexión de Kerberos.

### <a name="added-timeouts"></a>Se ha agregado los tiempos de espera

El controlador JDBC ahora admite los siguientes tiempos de espera configurables. Puede cambiarlos según las necesidades de su aplicación.

- Tiempo de espera de consulta para controlar el número de segundos que deben transcurrir antes de que se produce un tiempo de espera al ejecutar una consulta.
- Tiempo de espera de socket para especificar el número de milisegundos que transcurrirán antes de que se produce un tiempo de espera en un socket de lectura o acepta.

## <a name="61"></a>6.1

Microsoft JDBC Driver 6.1 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Se trata de la versión inicial de código abierto del controlador JDBC. Contiene los archivos mssql-jdbc-6.1.0.jre8.jar y mssql-jdbc-6.1.0.jre7.jar, que corresponden a la compatibilidad de versiones de Java.

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete 6.0 se nombran según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar del paquete 6.0 es compatible con JDBC API 4.2. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el archivo de sqljdbc41.jar o sqljdbc42.jar adecuado, ejecute las siguientes líneas de código. Si el resultado es "versión del controlador: 6.0.7507.100", tiene el paquete de JDBC Driver 6.0.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

El controlador admite la característica Always Encrypted en SQL Server 2016. Esta característica garantiza que los datos confidenciales no se ven nunca en texto sin formato en una instancia de SQL Server. Always Encrypted funciona mediante el cifrado transparente de los datos en la aplicación, de modo que SQL Server solo se ocupará de los datos cifrados y no los valores de texto no cifrado. Aunque la instancia de SQL Server o el equipo host estén en peligro, lo único que el atacante puede obtener es texto cifrado de datos confidenciales. Para información detallada, vea [Usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-names"></a>Nombres de dominio internacionalizados

El controlador admite nombres de dominio internacionalizados (IDN) para nombres de servidor. Para obtener más información, vea "Uso de nombres de dominio internacionales" en el [características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md) artículo.

### <a name="parameterized-queries"></a>Consultas con parámetros

El controlador ahora admite la recuperación de metadatos de parámetros con instrucciones preparadas para consultas complejas, como subconsultas o combinaciones. Tenga en cuenta que esta mejora solo está disponible cuando se usa SQL Server 2012 y versiones más recientes.

### <a name="azure-active-directory"></a>Azure Active Directory

Autenticación de Azure AD es un mecanismo de conexión a Azure SQL Database v12 mediante identidades de Azure AD. Use la autenticación de Azure AD para administrar identidades de usuarios de base de datos de forma centralizada y como alternativa a la autenticación de SQL Server. 

Puede utilizar JDBC Driver 6.0 para especificar sus credenciales de Azure AD en la cadena de conexión JDBC para conectarse a Azure SQL Database. Para obtener más información, vea la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) artículo.

### <a name="table-valued-parameters"></a>Parámetros con valores de tabla

Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla que, a continuación, pueden operar en mediante el uso de Transact-SQL. Para obtener más información, consulte [con parámetros con valores de tabla](../../connect/jdbc/using-table-valued-parameters.md).

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

El controlador ahora admite conexiones transparentes a grupos de disponibilidad AlwaysOn. El controlador detecta rápidamente la topología Always On actual de la infraestructura de servidor y conecta con el servidor activo actual de forma transparente.

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR en el paquete de 4.2 se nombran según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar desde el paquete de 4.2 es compatible con JDBC API 4.2. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para garantizar que tiene el derecho sqljdbc42.jar o archivo sqljdbc41.jar, ejecute las siguientes líneas de código. Si el resultado es "versión del controlador: 4.2.6420.100", tiene el paquete de JDBC Driver 4.2.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Compatibilidad con JDK 8

El controlador es compatible con JDK versión 8.0, además de JDK 7.0, 6.0 y 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Cumplimiento con JDBC 4.1 y 4.2

El controlador admite las especificaciones de la API Java Database Connectivity 4.1 y 4.2, además de 4.0. Para obtener más información, consulte [cumplimiento de JDBC 4.1 para el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [cumplimiento de JDBC 4.2 para el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Copia masiva

Se usa la característica de copia masiva para copiar rápidamente grandes cantidades de datos en tablas o vistas en bases de datos de SQL Server. Para obtener más información, vea [Uso de la copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opción de reversión de transacción de XA

El controlador dispone de nuevas opciones de tiempo de espera para la reversión automática existente de transacciones no preparadas. Para obtener más información, consulte [transacciones XA descripción](../../connect/jdbc/understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nueva propiedad de conexión de entidad de seguridad de Kerberos

El controlador usa una nueva propiedad de conexión para facilitar la flexibilidad con las conexiones de Kerberos. Para obtener más información, vea [Using Kerberos Integrated Authentication to Connect to SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) (Uso de la autenticación integrada de Kerberos para conectar con SQL Server).

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>Compatibilidad con JDK 7

El controlador es compatible con JDK versión 7.0, además de JDK 6.0 y 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium no es compatible con las aplicaciones de JDBC Driver 6.4, 6.0, 4.2 y 4.1

No se admite la ejecución de Microsoft JDBC Driver 6.4, 6.0, 4.2 y 4.1 para aplicaciones de SQL Server en un equipo Itanium.

## <a name="see-also"></a>Vea también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
