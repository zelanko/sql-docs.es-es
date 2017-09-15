---
title: Referencia de API del controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c19740d1247fa1fd7fe8036fa2aa557e01e74c82
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-api-reference"></a>Referencia de API del controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona una API que puede usarse en Java código de programación para conectar e interactuar con un [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.  
  
> [!NOTE]  
>  Para obtener información conceptual acerca de cómo utilizar el controlador JDBC, consulte [información general del controlador JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Para JDBC 4.1 y 4.2 de soporte técnico de cumplimiento, use Microsoft JDBC Driver 4.2 (o superior) para SQL Server. Las versiones anteriores de Microsoft JDBC Drivers 4.1 y 4.0 no admiten los nuevos métodos presentados con JDBC 4.1 o 4.2.  
>   
>  En esta sección no se encuentran los detalles de API para el cumplimiento de JDBC 4.1. Vea [JDBC 4.1 compatibilidad para el controlador JDBC](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md).  
>   
>  En esta sección no se incluyen los detalles de la API para el cumplimiento de JDBC 4.2. Vea [JDBC 4.2 compatibilidad para el controlador JDBC](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md).  
>   
>  Detalles de la API de copia masiva, disponible a partir de Microsoft JDBC Driver 4.2 para SQL Server, no se encuentran en esta sección. Vea [utilizando la copia masiva con el controlador JDBC](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).  
>   
>  Detalles de la API de Always Encrypted, disponible a partir de Microsoft JDBC Driver 6.0 para SQL Server, no se encuentran en esta sección. Vea [Always Encrypted referencia de API para el controlador JDBC](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  Detalles de la API para los parámetros de Using Table-Valued, disponible a partir de Microsoft JDBC Driver 6.0 para SQL Server, no se encuentran en esta sección. Consulte [con parámetros con valores de tabla](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Drivers 6.0 y 4.2 admiten la compilación con JDK 5.0, 6.0, 7.0 y 8.0.  
>   
>  El controlador Microsoft JDBC 4.1 admite la compilación con JDK 5.0, 6.0 y 7.0.  
>   
>  El controlador Microsoft JDBC 4.0 admite la compilación con JDK 5.0 y 6.0.  
  
## <a name="interfaces"></a>Interfaces  
  
|Nombre de la interfaz|Description|  
|--------------------|-----------------|  
|[Interfaz ISQLServerCallableStatement](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|Le permite especificar el nombre del procedimiento almacenado que se va a llamar junto con los parámetros de entrada y salida.|  
|[Interfaz ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|Representa una conexión JDBC a una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.|  
|[Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|Representa una lista de propiedades específicas para conectarse a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos mediante un [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|Representa la implementación básica de la funcionalidad de la instrucción preparada de JDBC.|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|Representa un conjunto de resultados JDBC.|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|Representa la implementación básica de la funcionalidad de la instrucción de JDBC.|  
  
## <a name="classes"></a>Clases  
  
|Nombre de clase|Description|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|Representa un objeto de tipo microsoft.sql.DateTimeOffset.|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|Representa un objeto binario grande (BLOB).|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|Implementa ISQLServerCallableStatement.|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|Representa un objeto binario grande de caracteres (CLOB).|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|Implementa ISQLServerConnectopn.|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|Representa las conexiones a bases de datos físicas para los administradores de grupos de conexiones.|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|Representa los metadatos para la base de datos.|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|Representa una lista de propiedades específicas para conectarse a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos mediante un [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|Representa un servicio de generación de objetos para materializar los orígenes de datos de la interfaz Java Naming and Directory Interface (JNDI).|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|Representa el controlador JDBC. Esta clase incluye métodos para conectarse a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos y para obtener información sobre el controlador JDBC.|  
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
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|Representa un generador para [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) objetos que se usa internamente.|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|Representa un XAResource XA administración de transacciones distribuidas.|  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre el controlador JDBC](../../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
