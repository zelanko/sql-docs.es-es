---
title: Notas de la versión para el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
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
ms.openlocfilehash: 1ec71defcba0a6f122d3c3ff9a098e163f07079c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38021135"
---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de la versión del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.4 para SQL Server
Microsoft JDBC Driver 6.4 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR incluidos en el paquete de 6,4 denominación de compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-6.4.0.jre8.jar desde el paquete de 6,4 se recomienda para su uso con Java 8. 

**Compatibilidad con JDK 9**  
  
Compatibilidad con Java Development Kit (JDK) versión 9.0, además de con JDK 8.0 y 7.0.
  
**Cumplimiento de JDBC 4.3**  
  
Compatibilidad con la especificación Java Database Connectivity API 4.3, además de con 4.1 y 4.2. Los métodos de API de JDBC 4.3 se agregarán pero aún no implementados. Para obtener información detallada, consulte [cumplimiento de JDBC 4.3 para el controlador JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).
 
**Agrega la nueva propiedad de conexión: sslProtocol**

Agrega una nueva propiedad de conexión que permite a los usuarios especificar la palabra clave de protocolo TLS. Los valores posibles son: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2". Consulte [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) para obtener más información.

**Propiedad de conexión en desuso: fipsProvider**

Propiedad de conexión "fipsProvider" se quita de la lista de propiedades de conexión aceptada. Ver los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).

**Propiedades de conexión se ha agregado para la especificación de TrustManager personalizado**

Controlador ahora admite la especificación de TrustManager personalizado con propiedades de conexión de "propiedades de conexión" y "trustManagerClass" se ha agregado. Esto permite la especificación dinámica de un conjunto de certificados que son de confianza en cada conexión sin modificar la configuración global para el entorno de JVM.

**Se agregó compatibilidad para datetime/smallDatetime en parámetros de valores de tabla (TVP)**

El controlador ahora es compatible con los tipos de datos DATETIME y SMALLDATETIME al usar parámetros con valores de tabla (TVP).

**Se agregó compatibilidad para el tipo de datos sql_variant**

El controlador JDBC ahora admite los tipos de datos sql_variant para su uso con SQL Server. Sql_variant también es compatible con características como parámetros con valores de tabla (TVP) y BulkCopy con siguientes limitaciones:

1. Para los valores de fecha: al usar TVP para rellenar una tabla que contiene los valores de datetime/smalldatetime/date almacenados en la columna sql_variant, llamar a métodos getDateTime()/getSmallDateTime()/getDate() en resultset no funciona y se produce la excepción siguiente:
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    Solución alternativa: use los métodos "getString()" o "getObject()" en su lugar.

2. Uso de TVP con sql_variant para valores null

Si usa TVP para rellenar una tabla y enviar el valor NULL al tipo de columna sql_variant, se producirá una excepción como Insertar valor NULL con tipo de columna sql_variant en TVP no se admite actualmente.

**Implementa la instrucción preparada almacenamiento en caché de metadatos**

Ha implementado el controlador JDBC de caché de metadatos de instrucción preparado para mejorar el rendimiento. Controlador ahora admite el almacenamiento en caché los metadatos de instrucción preparado en el controlador de propiedades de conexión "disableStatementPooling" y "valor de statementPoolingCacheSize". Esta característica está deshabilitada de forma predeterminada. Puede obtener más información [aquí](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

**Se ha agregado compatibilidad para la autenticación integrada de AAD en Linux o Mac**

El controlador JDBC ahora además admite la autenticación integrada de Azure Active Directory en todos los sistemas operativos compatibles (Windows/Linux/Mac) con Kerberos. Como alternativa, en sistemas de operativos Windows, los usuarios pueden autenticarse con sqljdbc_auth.dll.

**Versión actualizada de ADAL4J para 1.4.0**

El controlador JDBC actualizó su dependencia de maven de azure-activedirectory-library-for-java (ADAL4J) a la versión 1.4.0. Para obtener más información sobre las dependencias, consulte [aquí](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.2 para SQL Server
Microsoft JDBC Driver 6.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR incluidos en el paquete 6.0 se denominan según la compatibilidad de la versión de Java. Por ejemplo, el archivo mssql-jdbc-6.2.1.jre8.jar desde el paquete 6.2 se recomienda para su uso con Java 8. 

> [!NOTE]  
>  Se encontró un problema con la mejora del almacenamiento en caché de metadatos en la RTW de 6.2 JDBC publicado el 29 de junio de 2017. Se ha revertido la mejora y nuevos archivos JAR (versión 6.2.1) publicada en 17 de julio de 2017 de las [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), y [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Actualice sus proyectos para usar el 6.2.1 archivos JAR de versión. Vea [notas de la versión](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) para obtener más detalles.

**Soporte técnico de Azure Active Directory (AAD) para Linux**

Conectar sus aplicaciones de Linux a Azure SQL Database mediante autenticación de AAD a través de métodos de token de acceso y nombre de usuario/contraseña.

**Información de procesamiento estándar federal (FIPS) habilitado JVM**

Ahora se puede usar el controlador JDBC en JVM que se ejecutan en modo de cumplimiento de FIPS 140 para satisfacer el cumplimiento de normas y estándares federales. 

**Mejoras de autenticación de Kerberos** 

El controlador JDBC ahora es compatible con: 
* Método de entidad de seguridad y la contraseña para las aplicaciones donde la configuración de Kerberos no puede ser modificado o no se puede recuperar un token nuevo o una tabla de claves. Este método puede usarse para autenticar a un servidor de SQL que solo permite la autenticación Kerberos. 
* Autenticación entre dominios Kerberos mediante la autenticación integrada de Kerberos sin tener que establecer explícitamente el SPN del servidor. El controlador ahora calcula automáticamente el dominio KERBEROS incluso cuando no se ha proporcionado.
* Delegación restringida de Kerberos mediante la aceptación de suplantar las credenciales de usuario como un objeto de credenciales de GSS a través del origen de datos. Esta credencial suplantada, a continuación, se usa para establecer una conexión de Kerberos. 

**Se ha agregado los tiempos de espera**

El controlador JDBC ahora admite los siguientes tiempos de espera configurables que se pueden cambiar según las necesidades de su aplicación: 
* Tiempo de espera de consulta para controlar el número de segundos que deben transcurrir antes de que se produce un tiempo de espera cuando se ejecuta una consulta. 
* Tiempo de espera de socket para especificar el número de milisegundos que transcurrirán antes de que se produce un tiempo de espera en un socket de lectura o acepta. 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.1 para SQL Server

La 6.1 de Microsoft JDBC Driver para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Esto es la versión inicial de código abierto del controlador JDBC y contiene los archivos de mssql-jdbc-6.1.0.jre7.jar mssql-jdbc-6.1.0.jre8.jar, que corresponden a la compatibilidad de versiones de Java. 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.0 para SQL Server

Microsoft JDBC Driver 6.0 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR incluidos en el paquete 6.0 se nombran según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar del paquete 6.0 es compatible con JDBC API 4.2. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el derecho sqljdbc42.jar o sqljdbc41.jar, ejecute las siguientes líneas de código. Si el resultado es "versión del controlador: 6.0.7507.100", tiene el paquete de JDBC Driver 6.0.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **Always Encrypted**  
  
 Compatibilidad con la característica Always Encrypted publicada recientemente en SQL Server 2016, una nueva característica de seguridad que garantiza que los datos confidenciales no se vean nunca como texto no cifrado en una instancia de SQL Server. Always Encrypted funciona mediante el cifrado transparente de los datos en la aplicación, de modo que SQL Server solo se ocupará de los datos cifrados y no los valores de texto no cifrado. Aunque la instancia de SQL o el equipo host estén en peligro, lo único que el atacante puede obtener es texto cifrado de datos confidenciales. Para obtener información detallada, vea [Uso de Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
 **Nombre de dominio internacionalizado (IDN)**  
  
 Compatibilidad con nombres de dominio internacionalizados (IDN) para nombres del servidor. Para obtener información detallada, consulte utilizando nombres de dominio internacionales en el [características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md) página.  
  
 **Consulta con parámetros**  
  
 Ahora se admite la recuperación de metadatos de parámetros con instrucciones preparadas para consultas complejas, como subconsultas o combinaciones. Tenga en cuenta que esta mejora solo está disponible cuando se usa SQL Server 2012 y versiones más recientes.  
  
 **Azure Active Directory (AAD)**  
  
 Autenticación de AAD es un mecanismo de conexión a Azure SQL Database v12 mediante identidades en AAD. Use la autenticación de AAD para administrar identidades de usuarios de base de datos de forma centralizada y como alternativa a la autenticación de SQL Server. El controlador JDBC 6.0 permite especificar las credenciales de AAD en la cadena de conexión de JDBC para conectarse a Azure SQL DB.  Para obtener información detallada, consulte la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) página.  
  
 **Parámetros con valores de tabla**  
  
 Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla puede operar utilizando Transact-SQL. Para obtener información detallada, consulte [Using Table-Valued parámetros](../../connect/jdbc/using-table-valued-parameters.md).  
  
 **Grupos de disponibilidad (AG) Always On**  
  
 El controlador ahora admite conexiones transparentes a grupos de disponibilidad AlwaysOn. El controlador detecta rápidamente la topología Always On actual de la infraestructura de servidor y conecta con el servidor activo actual de forma transparente.  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.2 para SQL Server y versiones posteriores  
Microsoft JDBC Driver 4.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Los archivos JAR incluidos en el paquete de 4.2 se nombran según su cumplimiento con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar desde el paquete de 4.2 es compatible con JDBC API 4.2. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el derecho sqljdbc42.jar o sqljdbc41.jar, ejecute las siguientes líneas de código. Si el resultado es "versión del controlador: 4.2.6420.100", tiene el paquete de JDBC Driver 4.2.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **Compatibilidad con JDK 8**  
  
 Compatibilidad con Java Development Kit (JDK) versión 8.0, además de con JDK 7.0, 6.0 y 5.0.  
  
 **Conformidad con JDBC 4.1 y 4.2**  
  
 Compatibilidad con las especificaciones de la API Java Database Connectivity 4.1 y 4.2, además de 4.0. Para obtener información detallada, consulte [JDBC 4.1 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [JDBC 4.2 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
  
 **Copia masiva**  
  
 Se usa la característica de copia masiva para copiar rápidamente grandes cantidades de datos en tablas o vistas en bases de datos de SQL Server. Para obtener información detallada, consulte [utilizando copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
  
 **Opción de reversión de transacción de XA**  
  
 Se han agregado nuevas opciones de tiempo de espera para la reversión automática existente de transacciones no preparadas. Para obtener información detallada, consulte [descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
 **Nueva propiedad de conexión de entidad de seguridad de Kerberos**  
  
 Se ha agregado una nueva propiedad de conexión para facilitar la flexibilidad con las conexiones de Kerberos. Para obtener información detallada, vea [Usar la autenticación integrada de Kerberos para conectar con SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.1 para SQL Server y versiones posteriores  
 **Compatibilidad con JDK 7**  
  
 Compatibilidad para Java Development Kit (JDK) versión 7.0, además de JDK 6.0 y 5.0.  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium no es compatible con las aplicaciones de JDBC Driver 6.4, 6.0, 4.2 y 4.1  
  
 No se admite la ejecución de Microsoft JDBC Driver 6.4, 6.0, 4.2 y 4.1 para aplicaciones de SQL Server en un equipo Itanium.  
  
## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

