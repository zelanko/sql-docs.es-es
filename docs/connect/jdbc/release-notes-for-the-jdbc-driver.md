---
title: Notas de la versión para el controlador JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8f5f520be226d74c2c6530aacee7916aa381dc06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778153"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Notas de la versión para el controlador JDBC Driver de Microsoft

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se enumeran las versiones del _controlador JDBC Driver de Microsoft para SQL Server_. Se nombran y describen los cambios en cada una de las versiones.

## <a name="722"></a>7.2.2

### <a name="compliance"></a>Cumplimiento

16 de abril de 2019

| Cambio respecto del cumplimiento | Detalles |
| :---------------- | :------ |
| Descargue las actualizaciones más recientes para el controlador JDBC Driver 7.2. | &bull; &nbsp; [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| Totalmente compatible con la especificación 4.2 de la API de JDBC. | Los archivos JAR en el paquete 7.2 adquieren su nombre según la compatibilidad de la versión de Java.<br/><br/>Por ejemplo, el archivo mssql-jdbc-7.2.2.jre11.jar del paquete 7.2 debe usarse con Java 11. |
| Compatible con Java Development Kit (JDK) versión 11.0, además de con JDK 1.8. | Microsoft JDBC Driver 7.2 para SQL Server is compatible con Java Development Kit (JDK) versión 11.0, además de con JDK 1.8. |
| &nbsp; | &nbsp; |

> [!NOTE]
> Se encontró un problema con el análisis de la instrucción SQL del controlador JDBC 7.2 Release To Web (RTW) publicado el 31 de enero de 2019. El cambio se revirtió y se publicaron nuevos archivos JAR (versión 7.2.1) el 11 de febrero de 2019.
>
> Se realizó otra actualización en el controlador para solucionar problemas por los que los ActivityID no se limpiaban correctamente. Los nuevos archivos JAR (versión 7.2.2) se publicaron el 16 de abril de 2019.
> 
> Se recomienda actualizar los proyectos para que usen los archivos JAR de la versión 7.2.2. Para obtener más información, vea las notas de la versión para [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1) y [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2).

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Autenticación de Active Directory _Managed Service Identity_ (MSI)

| Cambio en MSI | Detalles |
| :--------- | :------ |
| Admite el modo de autenticación de Active Directory Managed Service Identity (MSI). | Este modo de autenticación es aplicable en los recursos de Azure con la compatibilidad habilitada para la característica "Identity".<br/><br/>Ambos tipos de identidades de Managed Service Identity (MSI) son compatibles con el controlador para adquirir **accessToken** a fin de establecer una conexión segura. |
| Más información y aplicación de ejemplo para usar este modo de autenticación. | Consulte [Conectarse mediante la autenticación de Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md). |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>Introducción de la compatibilidad con la iniciativa _Open Service Gateway Initiative_ (OSGi)

| Cambio de OSGi | Detalles |
| :---------- | :------ |
| Implementación de **DataSourceFactory** agregada. | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| Implementación de **Activator** agregada. | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>Introducción de las API de _SQLServerError_

| Cambio de la API de error | Detalles |
| :--------------- | :------ |
| Introducción de la API de SQLServerError. | API de captador para recuperar detalles adicionales sobre el error generado en el servidor.<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| Detalles adicionales. | Consulte [Control de errores](../../connect/jdbc/handling-errors.md). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>Se ha actualizado la versión 1.6.3 de _Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java_.

| Cambio en ADAL4J | Detalles |
| :------------ | :------ |
| Actualización de su dependencia de Maven en ADAL4J a la versión 1.6.3. | &nbsp; |
| Introducción de _Java Client Runtime for AutoRest_ como dependencia de Maven, versión 1.6.5. | &nbsp; |
| Detalles adicionales. | Consulte [Feature dependencies of the Microsoft JDBC Driver for SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) (Dependencias de características de Microsoft JDBC Driver para SQL Server). |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>Actualización del _SDK de Microsoft Azure Key Vault para Java_, versión 1.2.0

| Cambio del SDK de Key Vault | Detalles |
| :------------------- | :------ |
| Actualización de su dependencia de Maven del _SDK de Microsoft Azure Key Vault para Java_ a la versión 1.2.0. | &nbsp; |
| Presenta el _SDK de Microsoft Azure para Key Vault WebKey_ como dependencia de Maven, versión 1.2.0. | &nbsp; |
| Detalles adicionales. | Consulte [Feature dependencies of the Microsoft JDBC Driver for SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) (Dependencias de características de Microsoft JDBC Driver para SQL Server). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos

| Problemas conocidos | Detalles |
| :----------- | :------ |
| Consultas parametrizadas en ciertos casos. | Se publicó una actualización de la versión 7.2.0, la 7.2.1, en febrero de 2019 para solucionar este problema. |
| Limpieza de elementos ActivityID. | Se publicó una actualización de la versión 7.2.1, la 7.2.2, en abril de 2019 para solucionar este problema. |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

Microsoft JDBC Driver 7.0 for SQL Server es totalmente compatible con la especificación 4.2 de la API de JDBC. Los archivos JAR en el paquete 7.0 adquieren su nombre según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-7.0.0.jre10.jar del paquete 7.0 debe usarse con Java 10.

### <a name="support-for-jdk-10"></a>Compatibilidad con JDK 10

Microsoft JDBC Driver 7.0 para SQL Server es compatible con Java Development Kit (JDK) versión 10.0, además de con JDK 1.8. Esta actualización también expone el `Automatic-Module-Name` del controlador como `com.microsoft.sqlserver.jdbc` a través de su archivo MANIFEST.

### <a name="support-for-spatial-datatypes"></a>Compatibilidad con tipos de datos espaciales

Microsoft JDBC Driver 7.0 para SQL Server ahora ofrece soporte para los tipos de datos espaciales de SQL Server de geografía y geometría. Para obtener información acerca de las API de tipo de datos espaciales y cómo usarlas, consulte [Utilizar tipos de datos espaciales](../../connect/jdbc/use-spatial-datatypes.md).

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>Implementación de JDBC 4.3 y las API de java.sql.Connection beginRequest() y endRequest()

Microsoft JDBC Driver 7.0 para SQL Server ahora implementa las API `beginRequest()` y `endRequest()` desde la clase `java.sql.Connection`. Estas API se introdujeron con las especificaciones de JDBC 4.3 y JDK 9. Para obtener más información sobre la implementación del controlador de estas API, consulte [Cumplimiento de JDBC 4.3 con el controlador JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).

### <a name="support-for-sql-data-discovery-and-classification"></a>Compatibilidad con Clasificación y detección de datos de SQL

Microsoft JDBC Driver 7.0 para SQL Server proporciona compatibilidad para la detección y clasificación de datos de SQL con cualquier base de datos de destino que admita esta característica. El controlador ahora expone las API de `SQLServerResultSet.getSensitivityClassification()` para extraer esta información del valor `ResultSet` capturado.

Para obtener más información sobre cómo usar esta característica con el controlador JDBC Driver, vea el ejemplo en [Clasificación y detección de datos de SQL](../../connect/jdbc/data-discovery-classification-sample.md).

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>Adición de propiedad de conexión: useBulkCopyForBatchInsert

Microsoft JDBC Driver 7.0 para SQL Server presenta una nueva propiedad de conexión, `useBulkCopyForBatchInsert`. Esta propiedad solo se admite para Azure SQL Data Warehouse.

Esta propiedad está deshabilitada de forma predeterminada. Puede habilitarla para aumentar el rendimiento de las aplicaciones de usuario cuando esté insertando grandes cantidades de datos en Azure SQL Data Warehouse. La habilitación de esta propiedad cambia el comportamiento de las operaciones de inserción por lotes para cambiar a operaciones de copia masiva con datos proporcionados por el usuario. Para obtener más información acerca de esta propiedad y sus limitaciones, consulte [Uso de la API de copia masiva para la operación de inserción por lotes](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md).

### <a name="added-connection-property-cancelquerytimeout"></a>Adición de propiedad de conexión: cancelQueryTimeout

Microsoft JDBC Driver 7.0 para SQL Server presenta una nueva propiedad de conexión, `cancelQueryTimeout` para cancelar `queryTimeout` en objetos `java.sql.Connection` y `java.sql.Statement`.

### <a name="added-azure-key-vault-provider-constructors"></a>Adición de constructores del proveedor de Azure Key Vault

Microsoft JDBC Driver 7.0 para SQL Server vuelve a introducir un constructor previamente eliminado, para `SQLServerColumnEncryptionAzureKeyVaultProvider`. Permite la autenticación a través de un método personalizado que se implementa sobre `SQLServerKeyVaultAuthenticationCallback` para capturar un token de acceso.

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

Microsoft JDBC Driver 7.0 para SQL Server ha actualizado su dependencia de Maven en la "Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java" a la versión 1.6.0. Para obtener más información sobre las dependencias, consulte [Dependencias de características de Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 para SQL Server es totalmente compatible con las especificaciones 4.1 y 4.2 de JDBC. Los archivos JAR en el paquete 6.4 adquieren su nombre según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-6.4.0.jre8.jar del paquete 6.4 debe usarse con Java 8.

### <a name="support-for-jdk-9"></a>Compatibilidad con JDK 9

El controlador admite la versión 9.0 de JDK además de JDK 8.0 y 7.0.

### <a name="jdbc-43-compliance"></a>Compatibilidad de JDBC 4.3

El controlador admite la especificación Java Database Connectivity API 4.3, además de con 4.1 y 4.2. Los métodos de API de JDBC 4.3 se han agregado pero aún no se han implementado. Para obtener más información, vea [JDBC 4.3 Compliance for the JDBC Driver](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md) (Cumplimiento de JDBC 4.3 para JDBC Driver).

### <a name="added-connection-property-sslprotocol"></a>Adición de propiedad de conexión: sslProtocol

Una nueva propiedad de conexión permite a los usuarios especificar la palabra clave del protocolo TLS. Los valores posibles son: "TLS", "TLSv1", "TLSv1.1" y "TLSv1.2". Para obtener más información, consulte [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol).

### <a name="deprecated-connection-property-fipsprovider"></a>Propiedad de conexión en desuso: fipsProvider

La propiedad de conexión `fipsProvider` se ha quitado de la lista de propiedades de conexión aceptadas. Para obtener más información, consulte la [solicitud de incorporación de cambios de GitHub](https://github.com/Microsoft/mssql-jdbc/pull/460) relacionada.

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>Adición de propiedades de conexión para especificar un elemento TrustManager personalizado

El controlador ahora admite la especificación de un elemento TrustManager personalizado con las propiedades de conexión `trustManagerClass` y `trustManagerConstructorArg` agregadas. Puede especificar dinámicamente un conjunto de certificados que son de confianza en cada conexión sin modificar la configuración global para el entorno de la máquina virtual Java.

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>Adición de compatibilidad para datetime/smallDatetime en parámetros con valores de tabla

El controlador ahora admite los tipos de datos `datetime` y `smallDatetime` cuando se usa parámetros con valores de tabla (TVP).

### <a name="added-support-for-the-sqlvariant-datatype"></a>Adición de compatibilidad para el tipo de datos sql_variant

El controlador JDBC Driver ahora admite los tipos de datos `sql_variant` para su uso con SQL Server. El tipo de datos `sql_variant` también se admite con características como los TVP y la copia masiva con las siguientes limitaciones:

* **Para valores de fecha**: 

  Cuando se usa un TVP para rellenar una tabla que contiene valores `datetime`, `smalldatetime`, o `date` almacenados en una columna `sql_variant`, la llamada al método `getDateTime()`, `getSmallDateTime()` o `getDate()` en el conjunto de resultados no funciona e inicia la siguiente excepción:

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  Como solución, utilice el método `getString()` o `getObject()` en su lugar.

* **Uso de TVP con sql_variant para valores nulos**:
  
  Si usa TVP para rellenar una tabla y envía un valor NULL al tipo de columna `sql_variant`, encontrará una excepción. La inserción de un valor NULL con el tipo de columna `sql_variant` en un TVP no se admite actualmente.

### <a name="implemented-prepared-statement-metadata-caching"></a>Implementación del almacenamiento en caché de metadatos de instrucción preparada

El controlador JDBC Driver ha implementado el almacenamiento en caché de metadatos de instrucción preparada para mejorar el rendimiento. El controlador ahora es compatible con almacenamiento en caché de los metadatos de la instrucción preparada en el controlador con las propiedades de conexión `disableStatementPooling` y `statementPoolingCacheSize`. Esta característica está deshabilitada de forma predeterminada. Para obtener más información, consulte [Almacenamiento en caché de metadatos de instrucción preparada para el controlador JDBC](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md).

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>Adición de compatibilidad para la autenticación integrada de Azure AD en Linux o Mac

JDBC Driver ahora admite la autenticación integrada de Azure Active Directory (Azure AD) en todos los sistemas operativos compatibles (Windows/Linux/Mac) con Kerberos. Como alternativa, en sistemas operativos de Windows, los usuarios pueden autenticarse con sqljdbc_auth.dll.

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>Se ha actualizado la versión 1.4.0 de "Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java".

El controlador JDBC Driver ha actualizado su dependencia de Maven en la "Biblioteca de autenticación de Microsoft Azure Active Directory (ADAL4J) para Java" a la versión 1.4.0. Para obtener más información sobre las dependencias, consulte [Dependencias de características de Microsoft JDBC Driver para SQL Server](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md).

## <a name="62"></a>6.2

Microsoft JDBC Driver 6.2 para SQL Server es totalmente compatible con las especificaciones 4.1 y 4.2 de JDBC. Los archivos JAR en el paquete 6.2 adquieren su nombre según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-6.2.2.jre8.jar del paquete 6.2 se recomienda para su uso con Java 8.

> [!NOTE]  
> Se encontró un problema con la mejora del almacenamiento en caché de metadatos en la RTW de JDBC 6.2 publicada el 29 de junio de 2017. La mejora se revirtió y se publicaron nuevos archivos JAR (versión 6.2.1) el 17 de julio de 2017. 
>
> Otra mejora actualizó la versión de la biblioteca dependiente de Azure Key Vault a 1.0.0, y los nuevos archivos jar (versión 6.2.2) se publicaron el 19 de octubre de 2017.
>
> Descargue las actualizaciones más recientes para el controlador JDBC Driver 6.2 del [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) y [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver). Actualice los proyectos para que usen los archivos JAR de la versión 6.2.2. Para obtener más información, vea las notas de la versión para [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) y [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2).

### <a name="azure-ad-support-for-linux"></a>Compatibilidad de Azure AD para Linux

Conecte sus aplicaciones de Linux a Azure SQL Database mediante la autenticación de Azure AD a través de métodos de token de acceso y nombre de usuario/contraseña.

### <a name="fips-enabled-jvms"></a>JMV compatibles con FIPS

El controlador JDBC Driver ahora se puede utilizar en las JVM que se ejecutan en el modo de cumplimiento de Federal Information Processing Standard (FIPS) 140 para cumplir con los estándares federales de cumplimiento.

### <a name="kerberos-authentication-improvements"></a>Mejoras en la autenticación de Kerberos

El controlador JDBC Driver ahora es compatible con:

- Método de entidad de seguridad y contraseña para las aplicaciones donde la configuración de Kerberos no se puede modificar o no puede recuperar un token nuevo o un archivo keytab. Este método puede usarse para la autenticación en una instancia de SQL Server que permite solo la autenticación de Kerberos.
- Autenticación entre dominios que utiliza la autenticación integrada de Kerberos sin configurar explícitamente el SPN del servidor. El controlador ahora calcula automáticamente el dominio Kerberos incluso cuando no se proporciona.
- Delegación restringida de Kerberos mediante la aceptación de credenciales de usuario suplantadas como un objeto de credencial GSS a través del origen de datos. Esta credencial suplantada se usa a continuación para establecer una conexión de Kerberos.

### <a name="added-timeouts"></a>Adición de tiempos de expiración

El controlador JDBC Driver ahora admite los siguientes tiempos de expiración configurables. Puede cambiarlos según las necesidades de su aplicación.

- Tiempo de expiración de consulta para controlar el número de segundos que deben transcurrir antes de que se produzca un error por tiempo de espera al ejecutar una consulta.
- Tiempo de expiración de socket para especificar el número de milisegundos que deben transcurrir antes de que se produzca un error por tiempo de espera en una lectura o aceptación de socket.

## <a name="61"></a>6.1

Microsoft JDBC Driver 6.1 para SQL Server es totalmente compatible con las especificaciones 4.1 y 4.2 de JDBC. Se trata de la versión inicial de código abierto del controlador JDBC Driver. Contiene los archivos mssql-jdbc-6.1.0.jre8.jar y mssql-jdbc-6.1.0.jre7.jar, que corresponden a la compatibilidad de la versión de Java.

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 para SQL Server es totalmente compatible con las especificaciones 4.1 y 4.2 de JDBC. Los archivos JAR en el paquete 6.0 adquieren su nombre según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar del paquete 6.0 es compatible con la API 4.2 de JDBC. De forma similar, el archivo sqljdbc41.jar es compatible con la API 4.1 de JDBC.

Para asegurarse de que tiene el archivo sqljdbc42.jar o sqljdbc41.jar adecuado, ejecute las siguientes líneas de código. Si el resultado es "Driver version: 6.0.7507.100", tiene el paquete 6.0 del controlador JDBC.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

El controlador ya es compatible con la característica Always Encrypted en SQL Server 2016. Esta característica garantiza que los datos confidenciales no se vean nunca en texto sin formato en una instancia de SQL Server. Always Encrypted funciona mediante el cifrado transparente de los datos en la aplicación, de modo que SQL Server solo se ocupará de los datos cifrados y no los valores de texto no cifrado. Aunque la instancia de SQL Server o el equipo host estén en peligro, lo único que el atacante puede obtener es texto cifrado de datos confidenciales. Para información detallada, vea [Usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).

### <a name="internationalized-domain-names"></a>Nombres de dominio internacionalizados

El controlador admite nombres de dominio internacionalizados (IDN) para nombres del servidor. Para obtener más información, vea "Using International Domain Names ("Uso de nombres de dominio internacionales") en el artículo [International Features of the JDBC Driver](../../connect/jdbc/international-features-of-the-jdbc-driver.md) (Características internacionales del controlador JDBC Driver).

### <a name="parameterized-queries"></a>Consultas con parámetros

El controlador ahora admite la recuperación de metadatos de parámetros con instrucciones preparadas para consultas complejas, como subconsultas o combinaciones. Tenga en cuenta que esta mejora solo está disponible cuando se usa SQL Server 2012 y versiones más recientes.

### <a name="azure-active-directory"></a>Azure Active Directory

La autenticación de AAD es un mecanismo que permite conectar con Azure SQL Database v12 mediante identidades en Azure AD. Use la autenticación de Azure AD para administrar identidades de usuarios de base de datos de forma centralizada y como alternativa a la autenticación de SQL Server. 

Puede usar el controlador JDBC Driver 6.0 para especificar las credenciales de Azure AD en la cadena de conexión de JDBC para conectarse a Azure SQL Database. Para obtener más información, vea la propiedad de autenticación en el artículo [Establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).

### <a name="table-valued-parameters"></a>Parámetros con valores de tabla

Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla en la que, a continuación, puede operar mediante el uso de Transact-SQL. Para ver más información, consulte [Usar parámetros con valores de tabla](../../connect/jdbc/using-table-valued-parameters.md).

### <a name="always-on-availability-groups"></a>Grupos de disponibilidad AlwaysOn

El controlador ahora admite conexiones transparentes a grupos de disponibilidad Always On. El controlador detecta rápidamente la topología Always On actual de la infraestructura de servidor y conecta con el servidor activo actual de forma transparente.

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 para SQL Server es totalmente compatible con las especificaciones 4.1 y 4.2 de JDBC. Los archivos JAR en el paquete 4.2 adquieren su nombre según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar del paquete 4.2 es compatible con la API 4.2 de JDBC. De forma similar, el archivo sqljdbc41.jar es compatible con la API 4.1 de JDBC.

Para asegurarse de que tiene el archivo sqljdbc42.jar o sqljdbc41.jar adecuado, ejecute las siguientes líneas de código. Si el resultado es "Driver version: 4.2.6420.100", tiene el paquete 4.2 del controlador JDBC.

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>Compatibilidad con JDK 8

El controlador admite la versión 8.0 de JDK además de JDK 7.0, 6.0 y 5.0.

### <a name="jdbc-41-and-42-compliance"></a>Cumplimiento con JDBC 4.1 y 4.2

El controlador admite las especificaciones de la API Java Database Connectivity 4.1 y 4.2, además de 4.0. Para obtener más información, consulte [Cumplimiento de JDBC 4.1 con el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [Cumplimiento de JDBC 4.2 con el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).

### <a name="bulk-copy"></a>Copia masiva

Se usa la característica de copia masiva para copiar rápidamente grandes cantidades de datos en tablas o vistas en bases de datos de SQL Server. Para obtener más información, vea [Uso de la copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

### <a name="xa-transaction-rollback-option"></a>Opción de reversión de transacción de XA

El controlador dispone de nuevas opciones de tiempo de espera para la reversión automática existente de transacciones no preparadas. Para obtener más información, consulte [Descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md).

### <a name="new-kerberos-principal-connection-property"></a>Nueva propiedad de conexión de entidad de seguridad de Kerberos

El controlador usa una nueva propiedad de conexión para facilitar la flexibilidad con las conexiones de Kerberos. Para obtener más información, vea [Using Kerberos Integrated Authentication to Connect to SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) (Uso de la autenticación integrada de Kerberos para conectar con SQL Server).

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>Compatibilidad con JDK 7

El controlador admite la versión 7.0 de JDK además de JDK 6.0 y 5.0.

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium no es compatible con las aplicaciones de JDBC Driver 6.4, 6.0, 4.2 y 4.1

No se admite la ejecución de Microsoft JDBC Driver 6.4, 6.0, 4.2 y 4.1 para aplicaciones de SQL Server en un equipo Itanium.

## <a name="see-also"></a>Vea también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
