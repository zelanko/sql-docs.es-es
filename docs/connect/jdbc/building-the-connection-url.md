---
title: Generar URL de conexión | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18ed8477e6fc7c276db1842dba4f8856629bd29a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028452"
---
# <a name="building-the-connection-url"></a>Generar URL de conexión
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El formato general de la URL de conexión es  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 donde:  
  
-   **jdbc:sqlserver://** (obligatorio) es el subprotocolo y es constante.  
  
-   **serverName** (opcional) es la dirección del servidor con el que se establece la conexión. Puede ser un DNS o una dirección IP o bien un host local o 127.0.0.1 para el equipo local. Si no se especifica en la URL de conexión, es necesario especificar el nombre del servidor en la colección de propiedades.  
  
-   **instanceName** (opcional) es la instancia para establecer la conexión con serverName. Si no se especifica, se establece una conexión con la instancia predeterminada.  
  
-   **portNumber** (opcional) es el puerto para establecer la conexión con serverName. El valor predeterminado es 1433. Si usa el valor predeterminado, no es necesario especificar el puerto ni el signo ":" precedente en la dirección URL.  
  
    > [!NOTE]  
    >  Para obtener un rendimiento óptimo de la conexión, debe establecer portNumber al conectar con una instancia con nombre. De este modo se evita un ciclo de ida y vuelta en el servidor para determinar el número de puerto. Si se usan portNumber e instanceName, portNumber tiene prioridad e instanceName se omite.  
  
-   **property** (opcional) es una o más propiedades de conexión de la opción. Para obtener más información, vea [Establecimiento de las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md). Se puede especificar cualquier propiedad de la lista. Las propiedades solo se pueden delimitar mediante punto y coma (";") y no se pueden duplicar.  
  
> [!CAUTION]  
>  Por motivos de seguridad, debe evitar la generación de direcciones URL de conexión basadas en la entrada del usuario. Debe especificar solo el nombre del servidor y el controlador de la URL. Para los valores de nombre y contraseña, utilice las colecciones de propiedades de conexión. Para obtener más información acerca de la seguridad de las aplicaciones JDBC, consulte [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md).  
  
## <a name="connection-examples"></a>Ejemplos de conexión  
 Conexión a la base de datos predeterminada del equipo local con un nombre de usuario y una contraseña:  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  Aunque en el ejemplo anterior se usan un nombre de usuario y una contraseña en la cadena de conexión, debe usar la seguridad integrada dado que resulta más seguro. Para más información, vea la sección [Conexión con la autenticación integrada](#Connectingintegrated) más adelante en este tema.  
  
 La siguiente cadena de conexión muestra un ejemplo de cómo realizar la conexión a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una autenticación integrada y Kerberos desde una aplicación que se ejecuta en cualquier sistema operativo compatible con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]:  
  
```java
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 Conexión con la base de datos predeterminada del equipo local con autenticación integrada:  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 Conexión a la base de datos con nombre de un servidor remoto:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Conexión en el puerto predeterminado con el servidor remoto:  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Conectar mediante la especificación de un nombre de aplicación personalizada:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>Instancias de SQL Server múltiples y con nombre  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite la instalación de varias instancias de base de datos por servidor. Cada instancia se identifica con un nombre concreto. Para conectarse a una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar el número de puerto de la instancia con nombre (opción preferida) o bien el nombre de instancia como propiedad de URL de JDBC o propiedad **datasource**. Si no se especifica ningún nombre de instancia o propiedad de número de puerto, se crea una conexión a la instancia predeterminada. Consulte los siguientes ejemplos:  
  
 Para usar un número de puerto, haga lo siguiente:  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 Para usar una propiedad URL de JDBC, haga lo siguiente:  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>Escape de valores en la dirección URL de conexión  
 Puede que tenga que aplicar un escape a determinadas partes de los valores URL de conexión debido a la inclusión de caracteres especiales como espacios, puntos y comas, y comillas. El controlador JDBC admite el escape de estos caracteres si se incluyen entre llaves. Por ejemplo, {;} aplica el escape al punto y coma.  
  
 Los valores de escape pueden contener caracteres especiales (sobre todo "=", ";", "[]'" y espacio), pero no pueden contener llaves. Los valores a los que se debe aplicar el escape y contengan llaves se deben agregar a la colección de propiedades.  
  
> [!NOTE]  
>  El espacio en blanco dentro de las llaves es literal y no se reduce.  
  
##  <a name="Connectingintegrated"></a> Conexión con autenticación integrada en Windows  
 El controlador JDBC admite el uso de la autenticación integrada de tipo 2 en los sistemas operativos Windows mediante la propiedad de cadena de conexión integratedSecurity. Para usar la autenticación integrada, copie el archivo sqljdbc_auth.dll en un directorio de la ruta del sistema de Windows en que esté instalado el controlador JDBC.  
  
 Los archivos sqljdbc_auth.dll se instalan en la siguiente ubicación:  
  
 \<*installation directory*>\sqljdbc_\<*version*>\\<*language*>\auth\  
  
 Para cualquier sistema operativo compatible con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], consulte [Empleo de autenticación integrada de Kerberos para conectar con SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) para obtener una descripción de una característica agregada en [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] que permita a una aplicación conectarse a una base de datos con la autenticación integrada con Kerberos de tipo 4.  
  
> [!NOTE]  
>  Si está ejecutando una máquina virtual Java de (JVM, Java Virtual Machine) 32 bits, utilice el archivo sqljdbc_auth.dll en la carpeta x86, aun cuando la versión del sistema operativo sea la x64. Si está ejecutando una JVM de 64 bits en un procesador x64, utilice el archivo sqljdbc_auth.dll de la carpeta x64.  
  
 También puede especificar la propiedad del sistema java.libary.path para especificar el directorio de sqljdbc_auth.dll. Por ejemplo, si el controlador JDBC está instalado en el directorio predeterminado, puede especificar la ubicación de la DLL con el siguiente argumento de máquina virtual (VM) si la aplicación de Java se ha iniciado:  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>Conectar con direcciones IPv6  
 El controlador JDBC admite el uso de direcciones IPv6 con la colección de propiedades de conexión y con la propiedad de cadena de conexión serverName. El valor serverName inicial, como jdbc:*sqlserver*://*serverName*, no se admite para las direcciones IPv6 de las cadenas de conexión. El uso de un nombre para *serverName* en lugar de una dirección IPv6 sin formato funciona en todos los casos en la conexión. En los siguientes ejemplos se proporciona más información.  
  
 **Para usar la propiedad serverName**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **Para usar la colección de propiedades**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>Consulte también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
