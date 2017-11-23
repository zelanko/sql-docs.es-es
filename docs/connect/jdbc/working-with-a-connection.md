---
title: "Trabajar con una conexión | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0c1f696dda8f0d784b412446f3c8fa8d9dc45859
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-a-connection"></a>Trabajar con una conexión
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Las secciones siguientes proporcionan ejemplos de las diferentes formas para conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
> [!NOTE]  
>  Si tiene problemas para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] utilizando el controlador JDBC, consulte [solución de problemas de conectividad](../../connect/jdbc/troubleshooting-connectivity.md) para obtener sugerencias sobre cómo corregirlos.  
  
## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>Creación de una conexión con la clase DriverManager  
 El enfoque más sencillo para crear una conexión a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos consiste en cargar el controlador JDBC y llamar al método getConnection de la clase DriverManager, como en el siguiente ejemplo:  
  
```  
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 Este técnica creará una conexión a una base de datos usando el primer controlador disponible de la lista de controladores que se pueda conectar correctamente con la URL dada.  
  
> [!NOTE]  
>  Cuando se utiliza la biblioteca de clases sqljdbc4.jar, las aplicaciones no es necesario registrar o cargar el controlador mediante el método Class.forName explícitamente. Cuando se llama al método getConnection de la clase DriverManager, un controlador adecuado se encuentra en el conjunto de controladores JDBC registrados. Para obtener más información, vea Usar el controlador JDBC  
  
## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>Crear una conexión con la clase SQLServerDriver   
 Si tiene que especificar un controlador en particular en la lista de controladores para el Administrador de controladores, puede crear una conexión de base de datos mediante la [conectar](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) método de la [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) (clase), como en el siguiente ejemplo:  
  
```  
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```  
  
## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>Crear una conexión con la clase SQLServerDataSource  
 Si tiene que crear una conexión mediante el [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) (clase), puede utilizar distintos métodos de establecedor de la clase antes de llamar a la [getConnection](../../connect/jdbc/reference/getconnection-method.md) método, como en el siguiente ejemplo:  
  
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
  
 Para obtener más ejemplos de dirección URL de conexión, vea [generar URL de conexión](../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="creating-a-connection-with-a-custom-login-time-out"></a>Crear una conexión con tiempo de espera de inicio de sesión personalizado  
 Si tiene que ajustarse a la carga del servidor o el tráfico de la red, puede crear una conexión que tenga un valor de tiempo de espera de inicio de sesión en segundos, como en el siguiente ejemplo:  
  
 `String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"`  
  
## <a name="create-a-connection-with-application-level-identity"></a>Crear una conexión con identidad a nivel de la aplicación  
 Si tiene que crear perfiles y registros, tendrá que identificar la conexión como originaria de una aplicación específica, como en el siguiente ejemplo:  
  
 `String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"`  
  
## <a name="closing-a-connection"></a>Cerrar una conexión  
 Puede cerrar explícitamente una conexión de base de datos mediante una llamada a la [cerrar](../../connect/jdbc/reference/close-method-sqlserverconnection.md) método de la clase SQLServerConnection, como en el siguiente ejemplo:  
  
 `con.close();`  
  
 Esto se liberar los recursos de base de datos que usa el objeto SQLServerConnection o devolver la conexión al grupo de conexiones en situaciones de agrupamiento.  
  
> [!NOTE]  
>  Llama al método close también revertirá todas las transacciones pendientes.  
  
## <a name="see-also"></a>Vea también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
