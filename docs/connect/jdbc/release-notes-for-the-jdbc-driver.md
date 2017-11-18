---
title: "Notas de la versión para el controlador JDBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
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
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd65725237fd625c40f8755e636bb4f6fa2c55ea
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-jdbc-driver"></a>Notas de la versión para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Actualizaciones de Microsoft JDBC Driver 6.2 para SQL Server
El 6.2 de controlador JDBC de Microsoft para SQL Server es totalmente compatible con las especificaciones de JDBC 4.1 y 4.2. Lo archivos JAR incluido en el paquete 6.0 se asignan en función de la compatibilidad de versiones de Java. Por ejemplo, el archivo mssql-jdbc-6.2.1.jre8.jar desde el paquete 6.2 se recomienda para su uso con Java 8. 

**Nota:** se encontró un problema con los metadatos de almacenamiento en caché para la mejora en la RTW de 6.2 JDBC publicada el 29 de junio de 2017. Se revirtió la mejora y nuevos archivos JAR (versión 6.2.1) se publicaron en 17 de julio de 2017 en el [Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460), [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1), y [Maven Central](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22). Actualice sus proyectos para que usen el 6.2.1 archivos JAR de la versión. Consulte [notas de la versión](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) para obtener más detalles.

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
  
## <a name="updates-in-microsoft-jdbc-driver-40-for-sql-server-and-later"></a>Actualizaciones de Microsoft JDBC Driver 4.0 para SQL Server y versiones posteriores  
 **Obtener información sobre cómo conectarse a una base de datos SQL Azure**  
  
 Ahora hay un tema con información sobre cómo conectarse a una base de datos SQL de Azure. Vea [conectarse a una base de datos de SQL Azure](../../connect/jdbc/connecting-to-an-azure-sql-database.md) para obtener más información.  
  
 **Compatibilidad con alta disponibilidad, recuperación ante desastres**  
  
 Compatibilidad con conexiones de recuperación ante desastres de alta disponibilidad y a los grupos de disponibilidad AlwaysOn en [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. Vea [compatibilidad del controlador JDBC con alta disponibilidad y recuperación ante desastres](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) para obtener más información.  
  
 **Mediante la autenticación integrada de Kerberos para conectarse a SQL Server**  
  
 Compatibilidad con autenticación integrada de Kerberos de tipo 4 para las aplicaciones se conecten a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. Para obtener más información, consulte [utilizando la autenticación integrada Kerberos para conectarse a SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md). (Kerberos de tipo 2 está disponible en la autenticación integrada de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] las versiones anteriores a 4.0.)  
  
 **Obtener acceso a información de diagnóstico en el registro de eventos extendidos**  
  
 Puede tener acceso a la información en el registro de eventos extendidos del servidor para comprender los errores de conexión. Para obtener más información, consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
 **Compatibilidad adicional para columnas dispersas**  
  
 Si la aplicación ya tiene acceso a datos de una tabla que usa columnas dispersas, debería ver un aumento del rendimiento. Puede obtener información acerca de las columnas (incluida la información de columnas dispersas) con [getColumns método &#40; SQLServerDatabaseMetaData &#41; ](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md). Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] columnas dispersas, vea [usar columnas dispersas](http://go.microsoft.com/fwlink/?LinkId=224244).  
  
 **Xid.getFormatId**  
  
 A partir de [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], el controlador JDBC pasará el identificador de formato de la aplicación en el servidor de base de datos. Para obtener el comportamiento actualizado, asegúrese de que se actualiza sqljdbc_xa.dll en el servidor. Para obtener más información acerca de cómo copiar una versión actualizada de sqljdbc_xa.dll en el servidor, consulte [descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="itanium-not-supported-for-jdbc-driver-60-42-41-and-40-applications"></a>No se admite Itanium para las aplicaciones JDBC Driver 6.0, 4.2, 4.1 y 4.0  
  
 No se admiten Microsoft JDBC Drivers 6.0, 4.2, 4.1 y 4.0 para las aplicaciones de SQL Server para ejecutarse en un equipo Itanium.  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

