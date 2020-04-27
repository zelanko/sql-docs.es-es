---
title: SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 818c136814062c94491cfa02b84d2fff443a1f0a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63128663"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define los atributos de conexión específicos del controlador. Algunos de los atributos están disponibles para `SQLGetConnectAttr`y la función se usa para notificar su configuración actual. Los valores presentados para estos atributos no se garantizan hasta que se haya realizado una conexión o el atributo se haya establecido mediante [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
 En este tema se enumeran los atributos de solo lectura. Para obtener información sobre otros atributos de conexión específicos del controlador de ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, vea [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 El atributo SQL_COPT_SS_CONNECTION_DEAD notifica el estado de una conexión a un servidor. El controlador consulta el estado actual de la conexión en la red.  
  
> [!NOTE]  
>  El atributo de conexión ODBC estándar SQL_ATTR_CONNECTION_DEAD devuelve el estado más reciente de la conexión. Éste podría no ser el estado de la conexión actual.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_CD_TRUE|Se ha perdido la conexión al servidor.|  
|SQL_CD_FALSE|La conexión está abierta y disponible para procesar una instrucción.|  
  
## <a name="sql_copt_ss_client_connection_id"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 El atributo de SQL_COPT_SS_CLIENT_CONNECTION_ID recupera el identificador de conexión del cliente, el cual se puede utilizar para encontrar:  
  
-   Información de diagnóstico en el registro de XEvents, si se ha habilitado.  
  
-   Información sobre errores de conexión en el búfer del anillo de conexión.  
  
-   Información de diagnóstico de los registros de seguimiento de acceso a datos, si se ha habilitado.  
  
 Para obtener más información, vea [acceso a la información de diagnóstico en el registro de eventos extendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_ERROR|Error en la conexión.|  
|SQL_SUCCESS|La conexión se realizó correctamente. El identificador de conexión del cliente se encuentra en el búfer de salida.|  
  
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 El atributo SQL_COPT_SS_PERF_DATA devuelve un puntero a una estructura SQLPERF que contiene las estadísticas de rendimiento del controlador actual. `SQLGetConnectAttr`devolverá NULL si el registro de rendimiento no está habilitado. El controlador no actualiza de manera dinámica las estadísticas en la estructura SQLPERF. Llame `SQLGetConnectAttr` cada vez que sea necesario actualizar las estadísticas de rendimiento.  
  
|Value|Descripción|  
|-----------|-----------------|  
|NULL|El registro de rendimiento no está habilitado.|  
|Cualquier otro valor|Un puntero a una estructura SQLPERF.|  
  
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 El atributo SQL_COPT_SS_PERF_QUERY devuelve TRUE si está habilitado el registro de consultas de larga ejecución. La solicitud devuelve FALSE si el registro de consultas no está activo.  
  
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 El atributo SQL_COPT_SS_USER_DATA recupera el puntero de datos de usuario. Los datos de usuario se almacenan en la memoria propiedad del cliente y se registran por conexión. Si el puntero de datos de usuario no se ha establecido, SQL_UD_NOTSET, se devuelve un puntero NULL.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_UD_NOTSET|No se establece ningún puntero de datos de usuario.|  
|Cualquier otro valor|Un puntero a los datos de usuario.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>Compatibilidad de SQLGetConnectAttr con los Nombres principales de servicio (SPN)  
 SQLGetConnectAttr se puede usar para consultar el valor de los nuevos atributos de conexión SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD. (SQLGetConnectOption también se puede usar para consultar estos valores).  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD solo está disponible para las conexiones abiertas que usan la autenticación de Windows.  
  
 Si no se ha establecido SQL_COPT_SS_SERVER_SPN o SQL_COPT_SS_FAILOVER_PARTNER, se devuelve el valor predeterminado (una cadena vacía).  
  
 Para obtener más información acerca de los SPN, consulte [nombres de entidad de seguridad de servicio &#40;spn&#41; en conexiones de cliente &#40;&#41;ODBC ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLGetConnectAttr función)](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)   
 [ESTABLECER QUOTED_IDENTIFIER &#40;&#41;de Transact-SQL](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [ESTABLECER ANSI_NULLS &#40;&#41;de Transact-SQL](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [ESTABLECER ANSI_PADDING &#40;&#41;de Transact-SQL](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
