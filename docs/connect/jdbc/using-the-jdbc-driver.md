---
title: Usar el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03ea3e895fb7d70b392e0c25372536770308049d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015826"
---
# <a name="using-the-jdbc-driver"></a>Usar el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En esta sección se proporciona una serie de instrucciones rápidas para establecer una conexión sencilla a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Antes de establecer la conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se debe instalar en el equipo local o en un servidor, y el controlador JDBC se debe instalar en el equipo local.  
  
## <a name="choosing-the-right-jar-file"></a>Elegir el archivo JAR adecuado  
 Microsoft JDBC Driver 6.4 para SQL Server proporciona **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar**, y **mssql-jdbc-6.4.0.jre9.jar** biblioteca de clases archivos que se usan según su configuración preferida de Java Runtime Environment (JRE).  
 
 Microsoft JDBC Driver 6.2 para SQL Server proporciona **mssql-jdbc-6.2.1.jre7.jar**, y **mssql-jdbc-6.2.1.jre8.jar** archivos que se usan según el tiempo de ejecución de Java preferido de la biblioteca de clases Configuración del entorno (JRE).  
  
  Microsoft JDBC Drivers 6.0 y 4.2 para SQL Server proporcionan los archivos de la biblioteca de clases **sqljdbc41.jar** y **sqljdbc42.jar** que se usan en función de la configuración preferida de Java Runtime Environment (JRE).  
  
 Microsoft JDBC Driver 4.1 para SQL Server proporciona el archivo de biblioteca de clases **sqljdbc41.jar** que se usa según la configuración preferida de Java Runtime Environment (JRE).  
    
 Su elección también determinará las características disponibles. Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="setting-the-classpath"></a>Establecer la ruta de clase  
 El controlador JDBC no forma parte del SDK de Java. Si quiere usarlo, debe establecer la ruta de acceso de modo que incluya los archivos **sqljdbc.jar**, **sqljdbc4.jar**, **sqljdbc41.jar** o **sqljdbc42.jar**. Si usar JDBC Driver 6.2, Establece la ruta de clase para incluir el **mssql-jdbc-6.2.1.jre7.jar** o **mssql-jdbc-6.2.1.jre8.jar**. Si usar JDBC Driver 6.4, Establece la ruta de clase para incluir el **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** o **mssql-jdbc-6.4.0.jre9.jar**. Si falta una entrada en la ruta de clases, la aplicación lanzará la excepción común "Clase no encontrada".  
  
### <a name="for-microsoft-jdbc-driver-64"></a>De Microsoft JDBC Driver 6.4
 El **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** o **mssql-jdbc-6.4.0.jre9.jar** archivos se instalan en la siguiente ubicación:  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \mssql-jdbc-6.4.0.jre7.jar 
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \mssql-jdbc-6.4.0.jre8.jar
 
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \mssql-jdbc-6.4.0.jre9.jar
  
 El siguiente es un ejemplo de la instrucción CLASSPATH usada para una aplicación Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
 El siguiente es un ejemplo de la instrucción CLASSPATH usada para una aplicación de Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
 Debe asegurarse de que la instrucción CLASSPATH contiene solamente un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], por ejemplo, mssql-jdbc-6.4.0.jre7.jar, mssql-jdbc-6.4.0.jre8.jar o mssql-jdbc-6.4.0.jre9.jar.   

### <a name="for-microsoft-jdbc-driver-62"></a>De Microsoft JDBC Driver 6.2
 El **mssql-jdbc-6.2.1.jre7.jar** o **mssql-jdbc-6.2.1.jre8.jar** archivos se instalan en la siguiente ubicación:  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \mssql-jdbc-6.2.1.jre8.jar
  
 El siguiente es un ejemplo de la instrucción CLASSPATH usada para una aplicación Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 El siguiente es un ejemplo de la instrucción CLASSPATH usada para una aplicación de Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 Debe asegurarse de que la instrucción CLASSPATH contiene solamente un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], por ejemplo, mssql-jdbc-6.2.1.jre7.jar o mssql-jdbc-6.2.1.jre8.jar.  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>De Microsoft JDBC Driver 4.1, 4.2 y 6.0
 El archivo sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar se instalan en la siguiente ubicación:  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \sqljdbc.jar  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \sqljdbc4.jar  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \sqljdbc41.jar  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \sqljdbc42.jar  
  
 El siguiente es un ejemplo de la instrucción CLASSPATH usada para una aplicación Windows:  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
 El siguiente es un ejemplo de la instrucción CLASSPATH usada para una aplicación de Unix/Linux:  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
 Debe asegurarse de que la instrucción CLASSPATH contiene solamente un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], como por ejemplo, sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar.  
  
> [!NOTE]  
>  En los sistemas de Windows, los nombres de directorio superiores a 8.3 o los nombres de carpetas con espacios pueden causar problemas con las rutas de clase. Si sospecha estos tipos de problemas, debería mover temporalmente el archivo sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar a un directorio de nombre simple, tal como `C:\Temp`, cambiar la ruta de clases y determinar si el problema se resuelve.  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>Aplicaciones que se ejecutan directamente en el símbolo del sistema  
 La ruta de clase se configura en el sistema operativo. Anexe sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar a la ruta de clase del sistema. Además, puede especificar la ruta de clase en la línea de comandos de Java que ejecuta la aplicación con la opción `java -classpath`.  
  
### <a name="applications-that-run-in-an-ide"></a>Aplicaciones que se ejecutan en un IDE  
 Cada proveedor de IDE ofrece un método distinto para establecer la ruta de clase en el IDE. Establecer sin más la ruta de clase en el sistema operativo no funciona. Debe agregar sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar a la ruta de clase IDE.  
  
### <a name="servlets-and-jsps"></a>Servlets y JSP  
 Los servlets y JSP se ejecutan en un motor de servlet/JSP, como Tomcat. La ruta de clase se debe establecer de acuerdo con la documentación del motor de servlet/JSP. Establecer sin más la ruta de clase en el sistema operativo no funciona. Algunos motores de servlet/JSP incluyen pantallas de configuración que puede utilizar para establecer la ruta de clase del motor. En este caso, debe adjuntar el archivo JAR del controlador JDBC correcto a la ruta de clase del motor y reiniciar el motor. En otras situaciones, puede configurar el controlador copiando sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar en un directorio específico, como lib, durante la instalación del motor. La ruta de clase del controlador del motor también se puede especificar en un archivo de configuración específico del motor.  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Beans  
 Enterprise Java Beans (EJB) se ejecuta en un contenedor EJB. Los contenedores EJB son distribuidos por varios proveedores. Los applets Java se ejecutan en un explorador, pero se descargan desde un servidor web. Copie sqljdbc.jar, sqljdbc4.jar o sqljdbc41.jar en la raíz del servidor web y especifique el nombre del archivo JAR en la pestaña del archivo HTML del applet, por ejemplo, `<applet ... archive=sqljdbc.jar>`.  
  
## <a name="making-a-simple-connection-to-a-database"></a>Establecer una conexión sencilla con una base de datos  
 Mediante la biblioteca de clases sqljdbc.jar, primero las aplicaciones deben registrar el controlador del modo siguiente:  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 Cuando se carga el controlador, puede establecer una conexión con una dirección URL de conexión y el método getConnection de la clase DriverManager:  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 En la API de JDBC 4.0, el método DriverManager.getConnection se ha mejorado para cargar los controladores JDBC automáticamente. Por tanto, las aplicaciones no tienen que llamar al método Class.forName para registrar o cargar el controlador cuando se usa la biblioteca de clases sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar.  
  
 Cuando se llama al método getConnection de la clase DriverManager, un controlador adecuado se encuentra en el conjunto de controladores JDBC registrados. archivo sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar incluye el archivo "META-INF/services/java.sql.Driver", que contiene el **com.microsoft.sqlserver.jdbc.SQLServerDriver** como controlador registrado. Las aplicaciones existentes, que actualmente cargan los controladores usando el método Class.forName, seguirán trabajando sin modificación.  
  
> [!NOTE]  
>  La biblioteca de clases sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar no se puede utilizar con versiones anteriores de Java Runtime Environment (JRE). Consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para obtener la lista de versiones JRE compatibles con la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Para obtener más información sobre cómo conectar con orígenes de datos y use una dirección URL de conexión, consulte [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md) y [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
