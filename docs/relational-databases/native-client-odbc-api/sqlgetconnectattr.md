---
title: SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 153b5f73ea753639a7617f5de6d942dae40fadda
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63014484"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define los atributos de conexión específicos del controlador. Algunos de los atributos están disponibles para **SQLGetConnectAttr**, y la función se usa para notificar sus valores actuales. Los valores presentados para estos atributos no se garantizan hasta que se haya realizado una conexión o el atributo se haya establecido mediante [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 En este tema se enumeran los atributos de solo lectura. Para obtener información sobre otros atributos de conexión específicos del controlador de ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, vea [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 El atributo SQL_COPT_SS_CONNECTION_DEAD notifica el estado de una conexión a un servidor. El controlador consulta el estado actual de la conexión en la red.  
  
> [!NOTE]  
>  El atributo de conexión ODBC estándar SQL_ATTR_CONNECTION_DEAD devuelve el estado más reciente de la conexión. Éste podría no ser el estado de la conexión actual.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|SQL_CD_TRUE|Se ha perdido la conexión al servidor.|  
|SQL_CD_FALSE|La conexión está abierta y disponible para procesar una instrucción.|  
  
## <a name="sqlcoptssclientconnectionid"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 El atributo de SQL_COPT_SS_CLIENT_CONNECTION_ID recupera el identificador de conexión del cliente, el cual se puede utilizar para encontrar:  
  
-   Información de diagnóstico en el registro de XEvents, si se ha habilitado.  
  
-   Información sobre errores de conexión en el búfer del anillo de conexión.  
  
-   Información de diagnóstico de los registros de seguimiento de acceso a datos, si se ha habilitado.  
  
 Para obtener más información, consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
|Valor|Descripción|  
|-----------|-----------------|  
|SQL_ERROR|Error en la conexión.|  
|SQL_SUCCESS|La conexión se realizó correctamente. El identificador de conexión del cliente se encuentra en el búfer de salida.|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 El atributo SQL_COPT_SS_PERF_DATA devuelve un puntero a una estructura SQLPERF que contiene las estadísticas de rendimiento del controlador actual. **SQLGetConnectAttr** devolverá NULL si el registro de rendimiento no está habilitado. El controlador no actualiza de manera dinámica las estadísticas en la estructura SQLPERF. Llama a **SQLGetConnectAttr** cada vez que se actualicen las estadísticas de rendimiento.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|NULL|El registro de rendimiento no está habilitado.|  
|Cualquier otro valor|Un puntero a una estructura SQLPERF.|  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 El atributo SQL_COPT_SS_PERF_QUERY devuelve TRUE si está habilitado el registro de consultas de larga ejecución. La solicitud devuelve FALSE si el registro de consultas no está activo.  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 El atributo SQL_COPT_SS_USER_DATA recupera el puntero de datos de usuario. Los datos de usuario se almacenan en la memoria propiedad del cliente y se registran por conexión. Si el puntero de datos de usuario no se ha establecido, SQL_UD_NOTSET, se devuelve un puntero NULL.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|SQL_UD_NOTSET|No se establece ningún puntero de datos de usuario.|  
|Cualquier otro valor|Un puntero a los datos de usuario.|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>Compatibilidad de SQLGetConnectAttr con los Nombres principales de servicio (SPN)  
 SQLGetConnectAttr puede usarse para consultar el valor de los nuevos atributos de conexión SQL_COPT_SS_SERVER_SPN, SQL_COPT_SS_FAILOVER_PARTNER_SPN, SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD. (SQLGetConnectOption también se puede usar para consultar estos valores.)  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD solo está disponible para las conexiones abiertas que usan la autenticación de Windows.  
  
 Si no se ha establecido SQL_COPT_SS_SERVER_SPN o SQL_COPT_SS_FAILOVER_PARTNER, se devuelve el valor predeterminado (una cadena vacía).  
  
 Para obtener más información acerca de los SPN, vea [Service Principal Names &#40;SPN&#41; en conexiones cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Función SQLGetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
