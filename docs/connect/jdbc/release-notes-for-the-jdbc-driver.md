---
title: "Notas de la versión para el controlador JDBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 49710c98aad4af9373dd35ebf50960f32d999c10
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de la versión para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.4 para SQL Server
Microsoft JDBC Driver 6.4 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Lo archivos JAR incluido en el paquete 6.4 se asignan en función de la compatibilidad de versiones de Java. Por ejemplo, el archivo mssql-jdbc-6.4.0.jre8.jar desde el paquete 6.4 se recomienda para su uso con Java 8. 

**Compatibilidad con JDK 9**  
  
Compatibilidad para Java Development Kit (JDK) versión 9.0, además de JDK 8.0 y 7.0.
  
**Cumplimiento de JDBC 4.3**  
  
Compatibilidad con la especificación de 4.3 de API de conectividad de base de datos de Java, además de 4.1 y 4.2. Los métodos API de JDBC 4.3 se agregarán pero todavía no ha implementado. Para obtener más información, consulte [JDBC 4.3 compatibilidad para el controlador JDBC](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md).
 
**Agrega la nueva propiedad de conexión: sslProtocol**

Agrega una nueva propiedad de conexión que permite a los usuarios especificar la palabra clave de protocolo TLS. Los valores posibles son: "TLS", "TLSv1", "TLSv1.1", "TLSv1.2". Vea [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol) para obtener más información.

**Propiedad de conexión en desuso: fipsProvider**

Propiedad de conexión "fipsProvider" se quita de la lista de propiedades de conexión aceptada. Ver los detalles [aquí](https://github.com/Microsoft/mssql-jdbc/pull/460).

**Propiedades de conexión agregado para especificar TrustManager personalizado**

Controlador ahora admite la especificación de TrustManager personalizado con propiedades de conexión de "trustManagerConstructorArg" y "trustManagerClass" agregado. Esto permite la especificación dinámica de un conjunto de certificados de confianza en cada conexión sin modificar la configuración global para el entorno de JVM.

**Se agregó compatibilidad para datetime o smallDatetime en parámetros con valores de tabla (TVP)**

Controlador ahora admite tipos de datos DATETIME y SMALLDATETIME al utilizar parámetros con valores de tabla (TVP).

**Se agregó compatibilidad para el tipo de datos sql_variant**

El controlador JDBC ahora admite tipos de datos sql_variant para su uso con SQL Server. Sql_variant también es compatible con características como parámetros con valores de tabla (TVP) y BulkCopy con debajo de limitaciones:

1. Para valores de fecha: al usar TVP para rellenar una tabla que contiene los valores de datetime, smalldatetime o fecha almacenados en la columna sql_variant, llamadas a métodos de getDateTime()/getSmallDateTime()/getDate() en resultset no funciona y se produce la excepción siguiente:
    ```
    java.lang.String cannot be cast to java.sql.Timestamp
    ```
    Solución alternativa: use "getString()" o "getObject()" métodos en su lugar.

2. Uso de TVP con SQL Variant para valores null

Si usas TVP para rellenar una tabla y enviar un valor NULL al tipo de columna de sql_variant, se producirá una excepción como Insertar valor NULL con tipo de columna sql_variant en TVP no se admite actualmente.

**Implementa la instrucción preparada almacenamiento en caché de metadatos**

El controlador JDBC ha implementado la caché de metadatos de instrucción preparado para mejorar el rendimiento. Controlador ahora admite el almacenamiento en caché de los metadatos de instrucción preparado en el controlador con propiedades de conexión "disableStatementPooling" y "statementPoolingCacheSize". Esta característica está deshabilitada de forma predeterminada. Puede encontrar más información [aquí](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)

**Ha agregado compatibilidad con la autenticación integrada de AAD en Linux/Mac**

El controlador JDBC ahora también admite la autenticación integrada con Azure Active Directory en todos los sistemas operativos (Windows/Linux/Mac) con Kerberos. O bien, en sistemas operativos, los usuarios pueden autenticarse con sqljdbc_auth.dll.

**Versión actualizada de ADAL4J a 1.4.0**

El controlador JDBC actualizó su dependencia de maven con azure Active Directory-biblioteca-de-de java (ADAL4J) a la versión 1.4.0. Para obtener más información acerca de las dependencias, consulte [aquí](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.2 para SQL Server
El 6.2 de controlador JDBC de Microsoft para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Lo archivos JAR incluido en el paquete 6.0 se asignan en función de la compatibilidad de versiones de Java. Por ejemplo, el archivo mssql-jdbc-6.2.1.jre8.jar desde el paquete 6.2 se recomienda para su uso con Java 8. 

> [!NOTE]  
>  Se encontró un problema con la mejora del almacenamiento en caché de metadatos en la RTW de 6.2 JDBC publicada el 29 de junio de 2017. Se revirtió la mejora y nuevos archivos JAR (versión 6.2.1) se publicaron en 17 de julio de 2017 en el [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), y [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Actualice sus proyectos para que usen el 6.2.1 archivos JAR de la versión. Consulte [notas de la versión](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) para obtener más detalles.

**Soporte técnico de Azure Active Directory (AAD) para Linux**

Conectar las aplicaciones de Linux para la base de datos de SQL de Azure mediante la autenticación de AAD a través de métodos de token de acceso y nombre de usuario/contraseña.

**Information Processing Standard (FIPS) federal habilitado JVMs**

Ahora se puede usar el controlador JDBC en JVMs que se ejecutan en modo de cumplimiento de FIPS 140 para cumplir estándares federales y cumplimiento de normas. 

**Mejoras de la autenticación de Kerberos** 

El controlador JDBC ahora es compatible con: 
* Método de entidad de seguridad y la contraseña para las aplicaciones donde la configuración de Kerberos no puede ser modificado o no se puede recuperar un nuevo símbolo (token) o la tabla de claves. Este método se puede utilizar para autenticar a un servidor de SQL que solo permite la autenticación Kerberos. 
* Autenticación entre dominios mediante la autenticación integrada de Kerberos sin establecer explícitamente el SPN del servidor. El controlador ahora calcula automáticamente el dominio KERBEROS incluso cuando no se ha proporcionado.
* Delegación limitada de Kerberos aceptando suplantar las credenciales de usuario como un objeto de credencial de GSS a través del origen de datos. Esta credencial suplantada, a continuación, se usa para establecer una conexión Kerberos. 

**Tiempos de espera agregado**

El controlador JDBC ahora admite los siguientes tiempos de espera configurables que puede cambiar en función de las necesidades de su aplicación: 
* Tiempo de espera de consulta para controlar el número de segundos que deben transcurrir antes de que se produce un tiempo de espera cuando se ejecuta una consulta. 
* Tiempo de espera de socket para especificar el número de milisegundos que transcurrirán antes de que se produce un tiempo de espera en un socket de lectura o Aceptar. 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.1 para SQL Server

La 6.1 de controlador JDBC de Microsoft para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Es la versión inicial de código abierto del controlador JDBC y contiene los archivos de mssql-jdbc-6.1.0.jre7.jar mssql-jdbc-6.1.0.jre8.jar, que corresponden a la compatibilidad de versiones de Java. 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.0 para SQL Server

Microsoft JDBC Driver 6.0 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Lo archivos JAR incluido en el paquete 6.0 se asignan en función de su compatibilidad con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar desde el paquete 6.0 es la API de JDBC 4.2 compatible. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el derecho sqljdbc42.jar o sqljdbc41.jar, ejecute las siguientes líneas de código. Si la salida es la "versión del controlador: 6.0.7507.100", que tiene el paquete de JDBC Driver 6.0.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **Always Encrypted**  
  
 Compatibilidad con la característica Always Encrypted recientemente publicada en SQL Server 2016, una nueva característica de seguridad que garantiza que los datos confidenciales no se ven nunca en texto sin formato en una instancia de SQL Server. Always Encrypted funciona mediante el cifrado transparente de los datos en la aplicación, de modo que SQL Server solo se ocupará de los datos cifrados y no los valores de texto no cifrado. Incluso si la instancia de SQL o el equipo host está en peligro, todo lo que un atacante puede obtener es el texto cifrado de datos confidenciales. Para obtener más información, consulte [usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
 **Nombre de dominio internacionalizado (IDN)**  
  
 Compatibilidad con nombres de dominio internacionalizados (IDN) para nombres del servidor. Para obtener más información, consulte usar nombres de dominio internacionales en el [características internacionales del controlador JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md) página.  
  
 **Consulta parametrizada**  
  
 Ahora se admite la recuperación de metadatos de parámetros con instrucciones preparadas para consultas complejas, como subconsultas o combinaciones. Tenga en cuenta que esta mejora solo está disponible cuando se usa SQL Server 2012 y versiones más recientes.  
  
 **Azure Active Directory (AAD)**  
  
 Autenticación de AAD es un mecanismo de conectarse a la base de datos de SQL Azure v12 mediante identidades en AAD. Utilizar autenticación de AAD para administrar de forma centralizada las identidades de usuarios de base de datos y como una alternativa a la autenticación de SQL Server. El controlador JDBC 6.0 le permite especificar las credenciales AAD en la cadena de conexión de JDBC para conectarse a la base de datos de SQL Azure.  Para obtener más información, consulte la propiedad de autenticación en el [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md) página.  
  
 **Parámetros con valores de tabla**  
  
 Los parámetros con valores de tabla proporcionan una manera fácil de serializar varias filas de datos desde una aplicación cliente a SQL Server sin necesidad de varios viajes de ida y vuelta o lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos de entrada se almacenan en una variable de tabla que, a continuación, puede tratarse mediante Transact-SQL. Para obtener más información, consulte [Using Table-Valued parámetros](../../connect/jdbc/using-table-valued-parameters.md).  
  
 **Grupos de disponibilidad AlwaysOn (AG)**  
  
 El controlador ahora admite conexiones transparentes a grupos de disponibilidad AlwaysOn. El controlador detecta la topología AlwaysOn actual de su infraestructura de servidor y se conecta al servidor activo actual forma transparente rápidamente.  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.2 para SQL Server y versiones posteriores  
Microsoft JDBC Driver 4.2 para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Lo archivos JAR incluido en el paquete 4.2 se asignan en función de su compatibilidad con la versión de API de JDBC. Por ejemplo, el archivo sqljdbc42.jar desde el paquete 4.2 es la API de JDBC 4.2 compatible. De forma similar, el archivo sqljdbc41.jar es compatible con la API de JDBC 4.1.

Para asegurarse de que tiene el derecho sqljdbc42.jar o sqljdbc41.jar, ejecute las siguientes líneas de código. Si la salida es la "versión del controlador: 4.2.6420.100", que tiene el paquete de JDBC Driver 4.2.
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **Compatibilidad con JDK 8**  
  
 Compatibilidad para Java Development Kit (JDK) versión 8.0, además de JDK 7.0, 6.0 y 5.0.  
  
 **Cumplimiento JDBC 4.1 y 4.2**  
  
 Compatibilidad con las especificaciones de la API Java Database Connectivity 4.1 y 4.2, además de 4.0. Para obtener más información, consulte [JDBC 4.1 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [JDBC 4.2 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
  
 **Copia masiva**  
  
 Se usa la característica de copia masiva para copiar rápidamente grandes cantidades de datos en tablas o vistas en bases de datos de SQL Server. Para obtener más información, consulte [utilizando la copia masiva con el controlador JDBC](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
  
 **Opción de reversión de transacciones XA**  
  
 Se han agregado nuevas opciones de tiempo de espera para la reversión automática existente de transacciones no preparadas. Para obtener información detallada, vea [descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
 **Nueva propiedad de conexión de entidad de seguridad de Kerberos**  
  
 Se ha agregado una nueva propiedad de conexión para facilitar la flexibilidad con las conexiones de Kerberos. Para obtener información detallada, vea [utilizando la autenticación integrada Kerberos para conectarse a SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.1 para SQL Server y versiones posteriores  
 **Compatibilidad con JDK 7**  
  
 Compatibilidad para Java Development Kit (JDK) versión 7.0, además de JDK 6.0 y 5.0.  
  
## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>No se admite Itanium para las aplicaciones JDBC Driver 6.4, 6.0, 4.2 y 4.1  
  
 No se admiten Microsoft JDBC Drivers 6.4, 6.0, 4.2 y 4.1 para aplicaciones de SQL Server para ejecutarse en un equipo Itanium.  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

