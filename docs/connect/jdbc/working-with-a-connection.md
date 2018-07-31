---
title: Trabajar con una conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbcd46cd9da1ab189aeafe77c7275aa103ea51f6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060276"
---
# <a name="working-with-a-connection"></a>Trabajar con una conexión
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En las siguientes secciones se proporcionan ejemplos de las diferentes formas de conectar con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
> [!NOTE]  
>  Si tiene problemas para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con el controlador JDBC, vea [Solución de problemas de conectividad](../../connect/jdbc/troubleshooting-connectivity.md), donde encontrará sugerencias sobre cómo corregirlos.  
  
## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>Creación de una conexión con la clase DriverManager  
 El enfoque más sencillo para crear una conexión a una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es cargar el controlador JDBC y llamar al método getConnection de la clase DriverManager, como en el siguiente ejemplo:  
  
```  
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 Este técnica creará una conexión a una base de datos usando el primer controlador disponible de la lista de controladores que se pueda conectar correctamente con la URL dada.  
  
> [!NOTE]  
>  Al usar la biblioteca de clases sqljdbc4.jar, las aplicaciones no necesitan registrar o cargar explícitamente el controlador usando el método Class.forName. Cuando se llama al método getConnection de la clase DriverManager, un controlador adecuado se encuentra en el conjunto de controladores JDBC registrados. Para obtener más información, vea Usar el controlador JDBC  
  
## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>Crear una conexión con la clase SQLServerDriver   
 Si tiene que especificar un controlador en particular de la lista de controladores para DriverManager, puede crear una conexión a una base de datos con el método [connect](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) de la clase [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md), como en el siguiente ejemplo:  
  
```  
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```  
  
## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>Crear una conexión con la clase SQLServerDataSource  
 Si tiene que crear una conexión mediante la clase [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), puede usar diversos métodos de establecimiento de la clase antes de llamar al método [getConnection](../../connect/jdbc/reference/getconnection-method.md), como en el siguiente ejemplo:  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);   
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```  
  
## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>Crear una conexión cuyo destino sea un origen de datos muy específico  
 Si tiene que hacer una conexión a una base de datos cuyo destino sea un origen de datos muy específico, hay varios enfoques posibles. Cada enfoque depende de las propiedades que configure mediante la URL de conexión.  
  
 Para conectarse a la instancia predeterminada de un servidor remoto, use lo siguiente:  
  
 `String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"`  
  
 Para conectarse a un puerto específico de un servidor, use lo siguiente:  
  
 `String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"`  
  
 Para conectarse a una instancia con nombre de un servidor, use lo siguiente:  
  
 `String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"`  
  
 Para conectarse a una base de datos específica de un servidor, use lo siguiente:  
  
 `String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"`  
  
 Para obtener más ejemplos de dirección URL de conexión, consulte [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="creating-a-connection-with-a-custom-login-time-out"></a>Crear una conexión con tiempo de espera de inicio de sesión personalizado  
 Si tiene que ajustarse a la carga del servidor o el tráfico de la red, puede crear una conexión que tenga un valor de tiempo de espera de inicio de sesión en segundos, como en el siguiente ejemplo:  
  
 `String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"`  
  
## <a name="create-a-connection-with-application-level-identity"></a>Crear una conexión con identidad a nivel de la aplicación  
 Si tiene que crear perfiles y registros, tendrá que identificar la conexión como originaria de una aplicación específica, como en el siguiente ejemplo:  
  
 `String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"`  
  
## <a name="closing-a-connection"></a>Cerrar una conexión  
 Puede cerrar explícitamente una conexión a una base de datos llamando al método [close](../../connect/jdbc/reference/close-method-sqlserverconnection.md) de la clase SQLServerConnection, como en el siguiente ejemplo:  
  
 `con.close();`  
  
 De esta forma se liberarán los recursos de la base de datos que está usando el objeto SQLServerConnection, o devolver la conexión al grupo de conexiones en situaciones de agrupamiento.  
  
> [!NOTE]  
>  Si llama al método close, también se revertirán todas las transacciones pendientes.  
  
## <a name="see-also"></a>Ver también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
