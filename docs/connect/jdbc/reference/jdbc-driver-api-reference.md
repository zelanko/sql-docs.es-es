---
title: Referencia de API del controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f311458a8fb6b58f22a1ca4c23fa8d1f36dddc51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773799"
---
# <a name="jdbc-driver-api-reference"></a>Referencia de API del controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona una API que se puede usar en el código de programación Java para conectarse a una base de datos de [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e interactuar con ella.



### <a name="javadocio-website-is-primary"></a>Sitio Web de JavaDoc.io es principal

La documentación de referencia de API de JDBC de Microsoft está hospedada para su visualización en el sitio Web de JavaDoc.io. JavaDoc.io es ahora nuestro sitio Web principal de documentación de referencia JDBC. La documentación de referencia JDBC en JavaDoc.io está disponible en el siguiente vínculo directo:

- [https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/](https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/)

JavaDoc.io tiene la documentación de referencia JDBC comenzando con la versión 6.0.

#### <a name="only-legacy-jdbc-documentation-is-here-on-docs"></a>Documentación de JDBC heredado solo está aquí en Docs

La documentación de referencia de API de JDBC aquí artículos sobre **https://docs.microsoft.com/sql/connect/jdbc/reference/** ya no se actualizan cuando se actualizan las clases JDBC para las nuevas versiones. Sin embargo, aquí los artículos contienen toda la referencia para las versiones JDBC 4.1 y 4.2.

Documentación de JDBC versión 6.0 y versiones posteriores, también está aquí. Pero, para cualquier versión 6.0 o posterior, utilice el sitio Web de JavaDoc.io.



### <a name="important-notes"></a>Notas importantes

> [!NOTE]  
>  Para obtener información conceptual sobre cómo usar el controlador JDBC, consulte [información general del controlador JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Para el cumplimiento de JDBC 4.1 y 4.2, use Microsoft JDBC Driver 4.2 (o superior) para SQL Server. Las versiones anteriores de Microsoft JDBC Drivers 4.1 y 4.0 no admiten los nuevos métodos presentados con JDBC 4.1 o 4.2.  
>   
>  En esta sección no se encuentran los detalles de API para el cumplimiento de JDBC 4.1. Vea [Cumplimiento de JDBC 4.1 con el controlador JDBC](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md).  
>   
>  En esta sección no se incluyen los detalles de la API para el cumplimiento de JDBC 4.2. Vea [Cumplimiento de JDBC 4.2 con el controlador JDBC](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
>   
>  En esta sección no se incluyen detalles de la API para copia masiva, disponible a partir de Microsoft JDBC Driver 4.2 para SQL Server. Vea [Uso de la copia masiva con el controlador JDBC](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
>   
>  En esta sección no se incluyen los detalles de la API de Always Encrypted, disponible a partir de Microsoft JDBC Driver 6.0 para SQL Server. Vea [Always Encrypted referencia de API para el controlador JDBC](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  Detalles de la API para los parámetros Using Table-Valued, disponible a partir de Microsoft JDBC Driver 6.0 para SQL Server, no se encuentran en esta sección. Vea [Usar parámetros con valores de tabla](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.4 admite la compilación con JDK 7.0, 8.0 y 9.0.  
>   
>  Microsoft JDBC Driver 6.2 admite la compilación con JDK 7.0 y 8.0.  
>   
>  Microsoft JDBC Driver 6.0 y 4.2 admiten la compilación con JDK 5.0, 6.0, 7.0 y 8.0.  
>   
>  El controlador Microsoft JDBC 4.1 admite la compilación con JDK 5.0, 6.0 y 7.0.  



## <a name="interfaces"></a>Interfaces  
  
|Nombre de la interfaz|Descripción|  
|--------------------|-----------------|  
|[Interfaz ISQLServerCallableStatement](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|Le permite especificar el nombre del procedimiento almacenado que se va a llamar junto con los parámetros de entrada y salida.|  
|[Interfaz ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|Representa una conexión JDBC a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|Representa una lista de propiedades concretas para efectuar la conexión a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con un objeto [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|Representa la implementación básica de la funcionalidad de la instrucción preparada de JDBC.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|Representa un conjunto de resultados JDBC.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|Representa la implementación básica de la funcionalidad de la instrucción de JDBC.|
| &nbsp; | &nbsp; |


  
## <a name="classes"></a>Clases  
  
|Nombre de clase|Descripción|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|Representa un objeto de tipo microsoft.sql.DateTimeOffset.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|Representa un objeto binario grande (BLOB).|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|Implementa ISQLServerCallableStatement.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|Representa un objeto binario grande de caracteres (CLOB).|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|Implementa ISQLServerConnectopn.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|Representa las conexiones a bases de datos físicas para los administradores de grupos de conexiones.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|Representa los metadatos para la base de datos.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|Representa una lista de propiedades concretas para efectuar la conexión a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con un objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|Representa un servicio de generación de objetos para materializar los orígenes de datos de la interfaz Java Naming and Directory Interface (JNDI).|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|Representa el controlador JDBC. Esta clase incluye métodos para efectuar una conexión a una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y para obtener información sobre el controlador JDBC.|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|Representa una ejecución de una instrucción SQL que se ha realizado de forma incorrecta o incompleta.|  
|[Clase SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)|Representa un objeto binario grande de caracteres, para lo cual utiliza el juego de caracteres nacionales.|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|Representa los metadatos para los parámetros de instrucción preparados.|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|Representa una conexión a bases de datos físicas en un grupo de conexiones.|  
|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|Implementa ISQLServerPreparedStatement.|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|Representa un recurso de cadena de error localizado. Esta clase es solamente para uso interno.|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|Implementa ISQLServerResultSet.|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|Representa los metadatos de las columnas que se incluyen en un conjunto de resultados.|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|Representa el punto de comprobación hasta el que se puede revertir una transacción.|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|Implementa ISQLServerStatement.|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|Representa las conexiones JDBC que pueden participar en transacciones distribuidas (XA).|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|Representa un generador para objetos [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) que se usa internamente.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|Representa un XAResource para la administración de transacciones distribuidas XA.|
| &nbsp; | &nbsp; |



## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md)

