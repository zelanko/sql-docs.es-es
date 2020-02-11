---
title: Actualización de un controlador 3,5 a un controlador 3,8 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97b100b1ade97e1e88cf1421f09a7723412c8b76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915495"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Actualizar un controlador de 3,5 a un controlador 3.8
En este tema se proporcionan directrices y consideraciones para actualizar un controlador ODBC 3,5 a un controlador ODBC 3,8.  
  
##### <a name="version-numbers"></a>Números de versión  
 Las instrucciones siguientes se refieren a los números de versión:  
  
-   Un controlador debe admitir SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION, devolviendo SQL_ERROR para valores distintos de SQL_OV_ODBC2, SQL_OV_ODBC3 y SQL_OV_ODBC3_80. Las versiones futuras del administrador de controladores supondrán que un controlador admite un nivel de cumplimiento ODBC si el controlador devuelve SQL_SUCCESS de la [función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Un controlador de la versión 3,8 debe devolver 03,80 de **SQLGetInfo** cuando SQL_DRIVER_ODBC_VER se pasa a *InfoType*. Sin embargo, los administradores de controladores más antiguos, que se incluyeron en versiones anteriores de Microsoft Windows, tratarán el controlador como un controlador de la versión 3,5 y emitirán una advertencia.  
  
     En Windows 7, la versión del administrador de controladores es 03,80. En Windows 8, la versión del administrador de controladores es 03,81 a través del SQL_DM_VER SQLGetInfo (parámetro*InfoType* ). SQL_ODBC_VER notifica la versión como 03,80 en Windows 7 y Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipos de datos de C específicos del controlador  
 Un controlador puede tener tipos de datos de C personalizados cuando funciona con una aplicación ODBC de la versión 3,8. (Para obtener más información, vea [tipos de datos de C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)). Sin embargo, no hay ningún requisito para que un controlador 3,8 implemente cualquier tipo de C específico del controlador. Pero el controlador todavía debe realizar la comprobación de intervalo de tipos de C. el administrador de controladores no lo hará para los controladores 3,8. Para facilitar el desarrollo de controladores, el valor del tipo de datos de C específico del controlador se puede definir en el siguiente formato:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de datos específicos del controlador, tipos de descriptores, tipos de información, tipos de diagnóstico y atributos  
 Al desarrollar un nuevo controlador, debe utilizar el intervalo específico del controlador para tipos de datos, tipos de descriptores, tipos de información, tipos de diagnóstico y atributos. Los intervalos específicos del controlador y sus valores de tipo base se describen en [tipos de datos específicos del controlador, tipos de descriptores, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Agrupar conexiones  
 Para una mejor administración de la agrupación de conexiones, ODBC 3,8 presenta el atributo de conexión SQL_ATTR_RESET_CONNECTION en **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES es el único valor válido para este atributo. SQL_ATTR_RESET_CONNECTION se establecerán justo antes de que el administrador de controladores Coloque una conexión en el grupo de conexiones, lo que permite al controlador restablecer los valores predeterminados de los demás atributos de conexión.  
  
 Para evitar la comunicación innecesaria con el servidor, un controlador puede diferir el atributo de conexión restablecido hasta la siguiente comunicación con el servidor remoto, después de que la conexión se vuelva a usar desde el grupo.  
  
 Tenga en cuenta que SQL_ATTR_RESET_CONNECTION solo se utiliza en la comunicación entre el administrador de controladores y un controlador. Una aplicación no puede establecer este atributo directamente. Todos los controladores de la versión 3,8 deben implementar este atributo de conexión.  
  
##### <a name="streamed-output-parameters"></a>Parámetros de salida transmitidos  
 La versión 3,8 de ODBC presenta parámetros de salida transmitidos, una manera más escalable de recuperar parámetros de salida. (Para obtener más información, vea [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)). Para admitir esta característica, un controlador debe establecer SQL_GD_OUTPUT_PARAMS en el valor devuelto cuando SQL_GETDATA_EXTENSIONS es *InfoType* en una llamada a **SQLGetInfo** . La compatibilidad con un tipo SQL con parámetros de salida transmitidos debe implementarse en el controlador. El administrador de controladores no generará un error para un tipo SQL no válido. Los tipos de SQL que admiten parámetros de salida transmitidos se definen en el controlador.  
  
 Un controlador debe devolver SQL_ERROR si la aplicación usó **SQLGetData** para recuperar un parámetro que no es igual que el parámetro devuelto por **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Ejecución asincrónica de las operaciones de conexión (método de sondeo)  
 Un controlador puede habilitar la compatibilidad asincrónica para varias operaciones de conexión.  
  
 A partir de Windows 7, ODBC admite el método de sondeo (para obtener más información, vea [ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). No hay ningún requisito para que un controlador ODBC de la versión 3,8 implemente operaciones asincrónicas en los identificadores de conexión. Incluso si un controlador no implementa operaciones asincrónicas en identificadores de conexión, el controlador todavía debe implementar el SQL_ASYNC_DBC_FUNCTIONS *InfoType* y devolver **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Cuando se habilitan las operaciones de conexión asincrónicas, el tiempo de ejecución de una operación de conexión es el tiempo total de todas las llamadas repetidas. Si la última llamada repetida se produce después de que el tiempo total supere el valor establecido por el atributo de conexión SQL_ATTR_CONNECTION_TIMEOUT y la operación no ha finalizado, el controlador devuelve SQL_ERROR y registra un registro de diagnóstico con SQLState HYT01 y el valor de mensaje "tiempo de espera de conexión agotado". No hay tiempo de espera si la operación ha finalizado.  
  
##### <a name="sqlcancelhandle-function"></a>Función SQLCancelHandle  
 ODBC 3,8 admite la [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), que se usa para cancelar las operaciones de conexión y de instrucción. Un controlador que admita **SQLCancelHandle** debe exportar la función. Un controlador no debe cancelar ninguna función de conexión sincrónica o asincrónica que esté en curso si la aplicación llama a **SQLCancel** o **SQLCancelHandle** en un identificador de instrucción. Del mismo modo, un controlador no debe cancelar ninguna función de instrucción sincrónica o asincrónica que esté en curso si una aplicación llama a **SQLCancelHandle** en el identificador de conexión. Además, un controlador no debe cancelar la operación de exploración (**SQLBrowseConnect** devuelve SQL_NEED_DATA) si la aplicación llama a **SQLCancelHandle** en el identificador de conexión. En estos casos, un controlador debe devolver HY010, "function Sequence error".  
  
 No es necesario admitir las operaciones de conexión asincrónica y **SQLCancelHandle** al mismo tiempo. Un controlador puede admitir operaciones de conexión asincrónicas pero no **SQLCancelHandle**, o viceversa.  
  
##### <a name="suspended-connections"></a>Conexiones suspendidas  
 El administrador de controladores ODBC 3,8 puede poner una conexión en estado suspendido. Una aplicación llamará a **SQLDisconnect** para liberar los recursos asociados a la conexión. En este caso, un controlador debe intentar liberar tantos recursos como sea posible sin comprobar el estado de la conexión. Para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
 ODBC en Windows 8 permite a los controladores personalizar el comportamiento del grupo de conexiones. Para obtener más información, consulte [agrupación de conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)  
 ODBC 3,8 admite el método de notificación para las operaciones asincrónicas, disponible a partir de Windows 8. Para obtener más información, vea [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Controladores ODBC proporcionados por Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
