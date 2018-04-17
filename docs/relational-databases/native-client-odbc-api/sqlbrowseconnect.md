---
title: SQLBrowseConnect | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBrowseConnect function
ms.assetid: 57faf388-c7ca-4696-9845-34e0a10cc5f7
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c198f349a962f8ba27a408960c3651fbf73fe34
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbrowseconnect"></a>SQLBrowseConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBrowseConnect** usa palabras clave que se pueden clasificar en tres niveles de información de conexión. Para cada palabra clave, la tabla siguiente indica si se devuelve una lista de valores válidos y si la palabra clave es opcional.  
  
## <a name="level-1"></a>Nivel 1  
  
|Palabra clave|¿Se devuelve una lista?|¿Es opcional?|Description|  
|-------------|--------------------|---------------|-----------------|  
|DSN|N/D|No|Nombre del origen de datos devuelto por **SQLDataSources**. No se puede utilizar la palabra clave DSN si se utiliza la palabra clave DRIVER.|  
|DRIVER|N/D|No|Microsoft® [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre del controlador ODBC de Native Client es {[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11}. No se puede utilizar la palabra clave DRIVER si se utiliza la palabra clave DSN.|  
  
## <a name="level-2"></a>Nivel 2  
  
|Palabra clave|¿Se devuelve una lista?|¿Es opcional?|Description|  
|-------------|--------------------|---------------|-----------------|  
|SERVER|Sí|No|Nombre del servidor en la red en la que reside el origen de datos. El término"(local)" se puede escribir como el servidor, en cuyo caso se puede utilizar una copia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluso cuando se trata de una versión que no está en red.|  
|UID|No|Sí|Id. de inicio de sesión de usuario.|  
|PWD|No|Sí (depende del usuario)|Contraseña especificada por el usuario.|  
|APP|No|Sí|Nombre de la aplicación llama a **SQLBrowseConnect**.|  
|WSID|No|Sí|Id. de estación de trabajo. Normalmente, éste es el nombre de red del equipo en el que se ejecuta la aplicación.|  
  
## <a name="level-3"></a>Nivel 3  
  
|Palabra clave|¿Se devuelve una lista?|¿Es opcional?|Description|  
|-------------|--------------------|---------------|-----------------|  
|DATABASE|Sí|Sí|Nombre de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|LANGUAGE|Sí|Sí|Lenguaje nacional utilizado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 **SQLBrowseConnect** omite los valores de las palabras clave de base de datos y de idioma almacenados en las definiciones de origen de datos ODBC. Si la base de datos o el idioma especificado en la cadena de conexión que se pasa a **SQLBrowseConnect** no es válida, **SQLBrowseConnect** devuelve SQL_NEED_DATA y los atributos de conexión de nivel 3.  
  
 Los atributos siguientes, que se establecen mediante una llamada a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), determinar el conjunto de resultados devuelto por **SQLBrowseConnect**.  
  
|Attribute|Description|  
|---------------|-----------------|  
|SQL_COPT_SS_BROWSE_CONNECT|Si está establecido en sql_more_info_yes en **SQLBrowseConnect** devuelve una cadena extendida de propiedades del servidor.<br /><br /> El siguiente es un ejemplo de una cadena extendida devuelta por **SQLBrowseConnect**:<br /><br /> <br /><br /> `ServerName\InstanceName;Clustered:No;Version:8.00.131`<br /><br /> <br /><br /> En esta cadena, se utilizan signos de punto y coma para separar distintas partes de información acerca del servidor. Use comas para separar distintas instancias del servidor.|  
|SQL_COPT_SS_BROWSE_SERVER|Si se especifica un nombre de servidor, **SQLBrowseConnect** devolverá información para el servidor especificado. Si SQL_COPT_SS_BROWSE_SERVER está establecido en NULL, **SQLBrowseConnect** devuelve información para todos los servidores del dominio.<br /><br /> <br /><br /> Tenga en cuenta que debido a problemas de red, **SQLBrowseConnect** puede que no reciba una respuesta puntual de todos los servidores. Por lo tanto, la lista de servidores devuelta puede variar para cada solicitud.|  
|SQL_COPT_SS_BROWSE_CACHE_DATA|Cuando el atributo SQL_COPT_SS_BROWSE_CACHE_DATA está establecido en SQL_CACHE_DATA_YES, es posible para capturar los datos en fragmentos si la longitud del búfer no es lo suficientemente grande como para albergar el resultado. Esta longitud se especifica en el argumento BufferLength SQLBrowseConnect.<br /><br /> SQL_NEED_DATA se devuelve cuando hay más datos disponibles. SQL_SUCCESS se devuelve cuando no hay más datos que recuperar.<br /><br /> El valor predeterminado es SQL_CACHE_DATA_NO.|  
  
## <a name="sqlbrowseconnect-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQLBrowseConnect para la alta disponibilidad con recuperación de desastres  
 Para obtener más información sobre el uso de **SQLBrowseConnect** para conectarse a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] de clúster, consulte [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqlbrowseconnect-support-for-service-principal-names-spns"></a>Compatibilidad de SQLBrowseConnect con los Nombres principales de servicio (SPN)  
 Cuando se abre una conexión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establece SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD en el método de autenticación que se utiliza para abrir la conexión.  
  
 Para obtener más información acerca de los SPN, vea [nombres principales de servicio & #40; SPN & #41; en las conexiones de cliente & #40; ODBC & #41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se ha documentado SQL_COPT_SS_BROWSE_CACHE_DATA.|  
  
## <a name="see-also"></a>Vea también  
 [SQLBrowseConnect, función](http://go.microsoft.com/fwlink/?LinkId=59329)   
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
