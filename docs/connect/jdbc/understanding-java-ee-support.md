---
title: "Descripción de la compatibilidad con Java EE | Documentos de Microsoft"
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
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b878069cb0ddf04d4c8c743795f876b00fef23dc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-java-ee-support"></a>Descripción de la compatibilidad con Java EE
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  La secciones siguientes se documenta cómo el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona compatibilidad para Java Platform, Enterprise Edition (Java EE) y características opcionales de la API de JDBC 3.0. Los ejemplos del código fuente que se proporcionan en este sistema de Ayuda proporcionan una referencia adecuada para comenzar a usar estas características.  
  
 Primero, asegúrese de que el entorno de Java (JDK, JRE) incluye el paquete javax.sql. Es un paquete necesario para cualquier aplicación JDBC que utilice la API opcional. JDK 1.5 y las versiones posteriores ya contienen este paquete, por lo que no tiene que instalarlo por separado.  
  
## <a name="driver-name"></a>Nombre del controlador  
 El nombre de clase de controlador es **com.microsoft.sqlserver.jdbc.SQLServerDriver**. Para los controladores JDBC 4.0, 4.1, 4.2 y 6.0, el controlador se encuentra en el archivo sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar o sqljdbc42.jar. Para 6.2 de controlador JDBC, el controlador se encuentra en mssql-jdbc-6.2.1.jre7.jar o mssql-jdbc-6.2.1.jre8.jar.
  
 El nombre de clase se usa siempre que se carga el controlador con la clase del Administrador de controladores JDBC. Se utiliza también cada vez que deba especificar el nombre de clase del controlador en la configuración de cualquier controlador. Por ejemplo, configurar un origen de datos dentro de un servidor de aplicaciones de Java EE podría requerir que se escribiera el nombre de clase del controlador.  
  
## <a name="data-sources"></a>Orígenes de datos  
 El controlador JDBC proporciona compatibilidad con los orígenes de datos de Java EE / JDBC 3.0. El controlador JDBC [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) clase está implementada por **com.microsoft.sqlserver.jdbc.SQLServerXADataSource**.  
  
### <a name="datasource-names"></a>Nombre de los orígenes de datos  
 Puede realizar conexiones a bases de datos mediante orígenes de datos. Los orígenes de datos disponibles con el controlador JDBC se describen en la tabla siguiente:  
  
|Tipo de origen de datos|Descripción y nombre de clase|  
|---------------|--------------------------|  
|DataSource|com.microsoft.sqlserver.jdbc.SQLServerDataSource <br/> <br/> Origen de datos que no es un grupo.|  
|ConnectionPoolDataSource|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource <br/> <br/> Origen de datos para configurar los grupos de conexiones de servidor de aplicaciones de JAVA EE. Normalmente se usa cuando la aplicación se ejecuta dentro de un servidor de aplicaciones de JAVA EE.|  
|XADataSource|com.microsoft.sqlserver.jdbc.SQLServerXADataSource <br/> <br/> Origen de datos para configurar orígenes de datos de JAVA EE XA. Normalmente se usa cuando la aplicación se ejecuta dentro de un servidor de aplicaciones de JAVA EE y un administrador de transacciones de XA.|  
  
### <a name="data-source-properties"></a>Propiedades de origen de datos  
 Todos los orígenes de datos permiten establecer y obtener cualquier propiedad que esté asociada al conjunto de propiedades del controlador subyacente.  
  
 Ejemplos:  
  
 `setServerName("localhost");`  
  
 `setDatabaseName("AdventureWorks");`  
  
 A continuación se muestra cómo se conecta una aplicación mediante un origen de datos:  
  
```  
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 Para obtener más información acerca de las propiedades del origen de datos, vea [establecer las propiedades de origen de datos](../../connect/jdbc/setting-the-data-source-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

