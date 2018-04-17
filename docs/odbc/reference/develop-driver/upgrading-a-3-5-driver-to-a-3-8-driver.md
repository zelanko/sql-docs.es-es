---
title: Actualizar un controlador de 3,5 a un controlador 3.8 | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 577fd4f157c67c80c666f988e1ced40cdd8d084d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Actualizar un controlador de 3,5 a un controlador 3.8
Este tema proporciona instrucciones y consideraciones para actualizar un controlador de ODBC 3.5 a un controlador de ODBC 3.8.  
  
##### <a name="version-numbers"></a>Números de versión  
 Las instrucciones siguientes se relacionan con números de versión:  
  
-   Un controlador debe admitir SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION, devuelve SQL_ERROR para los valores que no sean SQL_OV_ODBC2, SQL_OV_ODBC3 y SQL_OV_ODBC3_80. Las versiones futuras del Administrador de controladores se presupone que un controlador admite un nivel de compatibilidad de ODBC si el controlador devuelve SQL_SUCCESS de [función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Un controlador de la versión 3.8 debe devolver 03.80 de **SQLGetInfo** cuando se pasa SQL_DRIVER_ODBC_VER a *tipo de información*. Sin embargo, administradores de controlador anterior, que se incluyeron en versiones anteriores de Microsoft Windows, trate al controlador como un controlador de la versión 3.5 y se generará una advertencia.  
  
     En Windows 7, la versión del Administrador de controladores es 03.80. En Windows 8, la versión del Administrador de controladores es 03.81 a través de la SQL_DM_VER SQLGetInfo (*tipo de información* parámetro). SQL_ODBC_VER informa de la versión como 03.80 en Windows 7 y Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipos de datos C específicos del controlador  
 Un controlador puede ha personalizado los tipos de datos de C cuando funciona con una aplicación de ODBC versión 3.8. (Para obtener más información, consulte [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) Sin embargo, no hay ningún requisito para un controlador 3.8 implementar cualquier tipo de C específicos del controlador. Pero el controlador debe seguir la comprobación del intervalo de tipos de C; el Administrador de controladores no hará 3.8 controladores. Para facilitar el desarrollo del controlador, se puede definir el valor del tipo de datos C específico, controlador en el formato siguiente:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos  
 Al desarrollar un controlador nuevo, debe usar el intervalo específicos del controlador para tipos de datos, tipos de descriptor, tipos de información, tipos de diagnóstico y atributos. Intervalos específicos del controlador y sus valores de tipo base se tratan en [tipos de datos específicos del controlador, Descriptor de tipos, información de tipos, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Agrupar conexiones  
 Para una mejor administración de la agrupación de conexiones, ODBC 3.8 presenta el atributo de conexión SQL_ATTR_RESET_CONNECTION en **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES es el único valor válido para este atributo. Se establecerá SQL_ATTR_RESET_CONNECTION justo antes de que el Administrador de controladores coloca una conexión en la agrupación de conexiones, lo que permite el controlador restablecer los demás atributos de conexión a sus valores predeterminados.  
  
 Para evitar las comunicaciones innecesarias con el servidor, un controlador puede diferir el atributo de conexión restablecer hasta la próxima comunicación con el servidor remoto, cuando se vuelve a usar la conexión del grupo.  
  
 Tenga en cuenta que SQL_ATTR_RESET_CONNECTION solo se usa en la comunicación entre el Administrador de controladores y un controlador. Una aplicación no puede establecer este atributo directamente. Todos los controladores de versión 3.8 deben implementar este atributo de conexión.  
  
##### <a name="streamed-output-parameters"></a>Parámetros de salida transmitidos  
 ODBC versión 3.8 presenta los parámetros de salida transmitidos, una forma más escalable para recuperar parámetros de salida. (Para obtener más información, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Para admitir esta característica, un controlador debe establecer SQL_GD_OUTPUT_PARAMS en el valor devuelto cuando se SQL_GETDATA_EXTENSIONS el *tipo de información* en un **SQLGetInfo** llamar. Compatibilidad para un tipo SQL con parámetros de salida transmitidos debe implementarse en el controlador. El Administrador de controladores no se generará un error para un tipo SQL no válido. Los tipos SQL que admiten parámetros de salida transmitidos se define en el controlador.  
  
 Un controlador debería devolver SQL_ERROR si la aplicación usa **SQLGetData** para recuperar un parámetro que no es el mismo que el parámetro devuelto por **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Ejecución asincrónica de las operaciones de conexión (método de sondeo)  
 Un controlador puede habilitar la compatibilidad asincrónica para realizar diversas operaciones de conexión.  
  
 A partir de Windows 7, ODBC admite el método de sondeo (para obtener más información, consulte [ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). No hay ningún requisito para un controlador ODBC versión 3.8 implementar operaciones asincrónicas en identificadores de conexión. Incluso si un controlador no implementa las operaciones asincrónicas en identificadores de conexión, el controlador debe implementar la SQL_ASYNC_DBC_FUNCTIONS *tipo de información* y devolver **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Cuando se habilitan las operaciones de conexión asincrónica, el tiempo de ejecución de una operación de conexión es el tiempo total de todas las llamadas repetidas. Si se repite la última llamada se produce después de que el tiempo total ha superado el valor establecido por el atributo de conexión de SQL_ATTR_CONNECTION_TIMEOUT y no ha terminado la operación, el controlador devuelve SQL_ERROR y se registra un registro de diagnóstico con SQLState HYT01 y mensaje de "tiempo de espera de conexión expirado". No hay ningún tiempo de espera si finaliza la operación.  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle (función)  
 Es compatible con ODBC 3.8 [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md), que se utiliza para cancelar las operaciones de conexión y de instrucción. Un controlador que admita **SQLCancelHandle** debe exportar la función. Un controlador no debe cancelar cualquier función de conexión sincrónica o asincrónica que está en curso, si la aplicación llama **SQLCancel** o **SQLCancelHandle** en un identificador de instrucción. De forma similar, un controlador no debe cancelar cualquier función de instrucción sincrónico o asincrónico que está en curso, si una aplicación llama **SQLCancelHandle** en el identificador de conexión. Además, un controlador no debe cancelar la operación de exploración (**SQLBrowseConnect** devuelve SQL_NEED_DATA) si la aplicación llama **SQLCancelHandle** en el identificador de conexión. En estos casos, un controlador debe devolver HY010, "error de secuencia de función".  
  
 No es necesario para admitir ambos **SQLCancelHandle** y las operaciones de conexión asincrónica al mismo tiempo. Un controlador puede admitir las operaciones de conexión asincrónica, pero no **SQLCancelHandle**, o viceversa.  
  
##### <a name="suspended-connections"></a>Conexiones suspendidas  
 El Administrador de controladores de ODBC 3.8 puede poner una conexión en estado suspendido. Una aplicación llamará **SQLDisconnect** para liberar los recursos asociados con la conexión. En este caso, un controlador debe intentar liberar recursos tantas como sea posible sin comprobar el estado de la conexión. Para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Agrupación de conexiones dependientes del controlador  
 ODBC en Windows 8 permite que los controladores personalizar el comportamiento de agrupación de conexiones. Para obtener más información, consulte [agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Ejecución asincrónica (método de notificación)  
 ODBC 3.8 admite el método de notificación para operaciones asincrónicas, disponibles a partir de Windows 8. Para obtener más información, consulte [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Controladores ODBC proporcionados por Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
