---
title: Función SQLAllocHandle ( SQLAllocHandle Function) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 178e3fad1ec062dd7f812125da66b7e21a7a4f4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290217"
---
# <a name="sqlallochandle-function"></a>Función SQLAllocHandle
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLAllocHandle** asigna un entorno, conexión, instrucción o identificador de descriptor.  
  
> [!NOTE]  
>  Esta función es una función genérica para asignar identificadores que reemplaza las funciones ODBC 2.0 **SQLAllocConnect**, **SQLAllocEnv**y **SQLAllocStmt**. Para permitir que las aplicaciones que llaman a **SQLAllocHandle** funcionen con ODBC 2. *x* controladores, una llamada a **SQLAllocHandle** se asigna en el Administrador de controladores a **SQLAllocConnect**, **SQLAllocEnv**o **SQLAllocStmt**, según corresponda. Para obtener más información, consulte "Comentarios." Para obtener más información acerca de lo que el Administrador de controladores asigna esta función a cuando un ODBC 3. *x* aplicación está trabajando con un ODBC 2. *x* driver, consulte Asignación de [funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo de identificador que va a asignar **SQLAllocHandle**. Debe ser uno de los siguientes valores:   
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN identificador solo lo utilizan el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información acerca de SQL_HANDLE_DBC_INFO_TOKEN, vea Desarrollar el reconocimiento de grupos [de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Entrada] El identificador de entrada en cuyo contexto se va a asignar el nuevo identificador. Si *HandleType* está SQL_HANDLE_ENV, se trata de SQL_NULL_HANDLE. Si *HandleType* es SQL_HANDLE_DBC, debe ser un identificador de entorno y, si es SQL_HANDLE_STMT o SQL_HANDLE_DESC, debe ser un identificador de conexión.  
  
 *OutputHandlePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el identificador a la estructura de datos recién asignada.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE o SQL_ERROR.  
  
 Al asignar un identificador distinto de un identificador de entorno, si **SQLAllocHandle** devuelve SQL_ERROR, establece *OutputHandlePtr* en SQL_NULL_HDBC, SQL_NULL_HSTMT o SQL_NULL_HDESC, dependiendo del valor de *HandleType*, a menos que el argumento de salida sea un puntero nulo. A continuación, la aplicación puede obtener información adicional de la estructura de datos de diagnóstico asociada con el identificador en el *InputHandle* argumento.  
  
## <a name="environment-handle-allocation-errors"></a>Errores de asignación de manejo del entorno  
 La asignación de entorno se produce tanto en el Administrador de controladores como dentro de cada controlador. El error devuelto por **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV depende del nivel en el que se produjo el error.  
  
 Si el Administrador de controladores no puede asignar memoria para * \*OutputHandlePtr* cuando **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se llama, o la aplicación proporciona un puntero nulo para *OutputHandlePtr*, **SQLAllocHandle** devuelve SQL_ERROR. El Administrador de controladores establece **OutputHandlePtr* en SQL_NULL_HENV (a menos que la aplicación proporciona un puntero nulo, que devuelve SQL_ERROR). No hay ningún identificador con el que asociar información de diagnóstico adicional.  
  
 El Administrador de controladores no llama a la función de asignación de identificador de entorno de nivel de controlador hasta que la aplicación llama a **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**. Si se produce un error en la función **SQLAllocHandle** de nivel de controlador, la función **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect** de nivel de controlador devuelve SQL_ERROR. La estructura de datos de diagnóstico contiene SQLSTATE IM004 (error del controlador **SQLAllocHandle).** El error se devuelve en un identificador de conexión.  
  
 Para obtener más información sobre el flujo de llamadas de función entre el Administrador de controladores y un controlador, vea [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLAllocHandle** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con el *HandleType* y *Handle* adecuado establecido en el valor de *InputHandle*. SQL_SUCCESS_WITH_INFO (pero no SQL_ERROR) se puede devolver para el *OutputHandle* argumento. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLAllocHandle** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexión no abierta|(DM) el *HandleType* argumento se SQL_HANDLE_STMT o SQL_HANDLE_DESC, pero la conexión especificada por el *InputHandle* argumento no estaba abierta. El proceso de conexión debe completarse correctamente (y la conexión debe estar abierta) para que el controlador asigne una instrucción o un identificador de descriptor.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el **MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|(DM) El Administrador de controladores no pudo asignar memoria para el identificador especificado.<br /><br /> El controlador no pudo asignar memoria para el identificador especificado.|  
|HY009|Uso no válido de puntero nulo|(DM) el *OutputHandlePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) el *HandleType* argumento se SQL_HANDLE_DBC y **SQLSetEnvAttr** no se ha llamado para establecer el SQL_ODBC_VERSION atributo de entorno.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para **el InputHandle** y todavía se estaba ejecutando cuando el **SQLAllocHandle** función se llamó con **HandleType** establecido en SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY013|Error de administración de memoria|El *HandleType* argumento era SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC; y no se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de memoria baja.|  
|HY014|Límite en el número de asas excedidas|Se ha alcanzado el límite definido por el controlador para el número de identificadores que se pueden asignar para el tipo de identificador indicado por el *HandleType* argumento.|  
|HY092|Identificador de atributo/opción no válido|(DM) El *HandleType* argumento no era: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT, o SQL_HANDLE_DESC.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El *HandleType* argumento era SQL_HANDLE_DESC y el controlador era un ODBC 2. *x* conductor.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) el *HandleType* argumento era SQL_HANDLE_STMT y el controlador no era un controlador ODBC válido.<br /><br /> (DM) el *HandleType* argumento se SQL_HANDLE_DESC y el controlador no admite la asignación de un identificador de descriptor.|  
  
## <a name="comments"></a>Comentarios  
 **SQLAllocHandle** se utiliza para asignar identificadores para entornos, conexiones, instrucciones y descriptores, como se describe en las secciones siguientes. Para obtener información general acerca de los identificadores, vea [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Una aplicación puede asignar más de un identificador de entorno, conexión o instrucción a la vez si el controlador admite varias asignaciones. En ODBC, no se define ningún límite en el número de identificadores de entorno, conexión, instrucción o descriptor que se pueden asignar en cualquier momento. Los controladores pueden imponer un límite en el número de un determinado tipo de identificador que se puede asignar a la vez; Para obtener más información, consulte la documentación del controlador.  
  
 Si la aplicación llama a **SQLAllocHandle** con * \*OutputHandlePtr* establecido en un entorno, conexión, instrucción o identificador de descriptor que ya existe, el controlador sobrescribe la información asociada con el *identificador,* a menos que la aplicación esté utilizando la agrupación de conexiones (consulte "Asignación de un atributo de entorno para la agrupación de conexiones" más adelante en esta sección). El Administrador de controladores no comprueba si el *identificador* especificado en * \*OutputHandlePtr* ya se está utilizando, ni comprueba el contenido anterior de un identificador antes de sobrescribirlos.  
  
> [!NOTE]  
>  Es incorrecto la programación de aplicaciones ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para * \*OutputHandlePtr* sin llamar a **SQLFreeHandle** para liberar el identificador antes de reasignarlo. Sobrescribir identificadores ODBC de tal manera podría dar lugar a un comportamiento incoherente o errores por parte de los controladores ODBC.  
  
 En sistemas operativos que admiten varios subprocesos, las aplicaciones pueden usar el mismo entorno, conexión, instrucción o identificador de descriptor en subprocesos diferentes. Por lo tanto, los controladores deben admitir un acceso seguro y multiproceso a esta información; una manera de lograr esto, por ejemplo, es mediante el uso de una sección crítica o un semáforo. Para obtener más información sobre el subproceso, vea [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** no establece el atributo de entorno SQL_ATTR_ODBC_VERSION cuando se llama para asignar un identificador de entorno; el atributo de entorno debe establecerse por la aplicación o SQLSTATE HY010 (error de secuencia de funciones) se devolverá cuando **SQLAllocHandle** se llama para asignar un identificador de conexión.  
  
 Para las aplicaciones compatibles con estándares, **SQLAllocHandle** se asigna a **SQLAllocHandleStd** en tiempo de compilación. La diferencia entre estas dos funciones es que **SQLAllocHandleStd** establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3 cuando se llama con el *HandleType* argumento establecido en SQL_HANDLE_ENV. Esto se hace porque las aplicaciones compatibles con estándares siempre son ODBC 3. *x* aplicaciones. Además, las normas no requieren que se registre la versión de la aplicación. Esta es la única diferencia entre estas dos funciones; de lo contrario, son idénticos. **SQLAllocHandleStd** se asigna a **SQLAllocHandle** dentro del administrador de controladores. Por lo tanto, los controladores de terceros no tienen que implementar **SQLAllocHandleStd**.  
  
 Las aplicaciones ODBC 3.8 deben utilizar:  
  
-   **SQLAllocHandle y no SQLAllocHandleStd** para asignar un identificador de entorno.  
  
-   **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Asignar un identificador de entorno  
 Un identificador de entorno proporciona acceso a información global, como identificadores de conexión válidos y identificadores de conexión activos. Para obtener información general sobre los identificadores de entorno, consulte [Identificadores](../../../odbc/reference/develop-app/environment-handles.md)de entorno .  
  
 Para solicitar un identificador de entorno, una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y un *InputHandle* de SQL_NULL_HANDLE. El controlador asigna memoria para la información del entorno y pasa el valor del identificador asociado en el * \*OutputHandlePtr* argumento. La aplicación pasa * \** el valor OutputHandle en todas las llamadas posteriores que requieren un argumento de identificador de entorno. Para obtener más información, consulte [Asignación del controlador](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)de entorno .  
  
 En un identificador de entorno del Administrador de controladores, si ya existe un identificador de entorno de controlador, a continuación, **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV no se llama en ese controlador cuando se realiza una conexión, sólo **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC. Si el identificador de entorno de un controlador no existe en el identificador de entorno del Administrador de controladores, SQLAllocHandle con un HandleType de SQL_HANDLE_ENV y SQLAllocHandle con un HandleType de SQL_HANDLE_DBC se llama en el controlador cuando el primer identificador de conexión del entorno está conectado al controlador.  
  
 Cuando el Administrador de controladores procesa la función **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV, comprueba la palabra clave **Trace** en la sección [ODBC] de la información del sistema. Si se establece en 1, el Administrador de controladores habilita el seguimiento de la aplicación actual. Si se establece la marca de seguimiento, el seguimiento se inicia cuando se asigna el primer identificador de entorno y finaliza cuando se libera el último identificador de entorno. Para obtener más información, consulte [Configuración de orígenes](../../../odbc/reference/install/configuring-data-sources.md)de datos .  
  
 Después de asignar un identificador de entorno, una aplicación debe llamar a **SQLSetEnvAttr** en el identificador de entorno para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION. Si este atributo no se establece antes **de SQLAllocHandle** se llama para asignar un identificador de conexión en el entorno, la llamada para asignar la conexión devolverá SQLSTATE HY010 (error de secuencia de funciones). Para obtener más información, consulte [Declarar la versión ODBC de la aplicación](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Asignación de entornos compartidos para la agrupación de conexiones  
 Los entornos se pueden compartir entre varios componentes en un único proceso. Un entorno compartido puede ser utilizado por más de un componente al mismo tiempo. Cuando un componente utiliza un entorno compartido, puede utilizar conexiones agrupadas, que le permiten asignar y utilizar una conexión existente sin volver a crear esa conexión.  
  
 Antes de asignar un entorno compartido que se puede usar para la agrupación de conexiones, una aplicación debe llamar a **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. **SQLSetEnvAttr** en este caso se llama con *EnvironmentHandle* establecido en null, lo que convierte el atributo en un atributo de nivel de proceso.  
  
 Una vez habilitada la agrupación de conexiones, una aplicación llama a **SQLAllocHandle** con el *HandleType* argumento establecido en SQL_HANDLE_ENV. El entorno asignado por esta llamada será un entorno compartido implícito porque se ha habilitado la agrupación de conexiones.  
  
 Cuando se asigna un entorno compartido, el entorno que se usará no se determina hasta **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama. En ese momento, el Administrador de controladores intenta encontrar un entorno existente que coincida con los atributos de entorno solicitados por la aplicación. Si no existe tal entorno, se crea uno como un entorno compartido. El Administrador de controladores mantiene un recuento de referencias para cada entorno compartido; el recuento se establece en 1 cuando se crea el entorno por primera vez. Si se encuentra un entorno coincidente, el identificador de ese entorno se devuelve a la aplicación y se incrementa el recuento de referencias. Un identificador de entorno asignado de esta manera se puede usar en cualquier función ODBC que acepte un identificador de entorno como argumento de entrada.  
  
## <a name="allocating-a-connection-handle"></a>Asignar un identificador de conexión  
 Un identificador de conexión proporciona acceso a información como la instrucción válida y los identificadores descriptores de la conexión y si una transacción está abierta actualmente. Para obtener información general sobre los identificadores de conexión, consulte [Controladores](../../../odbc/reference/develop-app/connection-handles.md)de conexión .  
  
 Para solicitar un identificador de conexión, una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC. El *InputHandle* argumento se establece en el identificador de entorno devuelto por la llamada a **SQLAllocHandle** que asignó ese identificador. El controlador asigna memoria para la información de conexión y devuelve el valor del identificador asociado en * \*OutputHandlePtr*. La aplicación pasa el * \*Valor OutputHandlePtr* en todas las llamadas posteriores que requieren un identificador de conexión. Para obtener más información, consulte [Asignación](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)de un controlador de conexión .  
  
 El Administrador de controladores procesa la función **SQLAllocHandle** y llama a la función **SQLAllocHandle** del controlador cuando la aplicación llama a **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect**. (Para obtener más información, vea [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Si el SQL_ATTR_ODBC_VERSION atributo de entorno no se establece antes **de SQLAllocHandle** se llama para asignar un identificador de conexión en el entorno, la llamada para asignar la conexión devolverá SQLSTATE HY010 (error de secuencia de funciones).  
  
 Cuando una aplicación llama a **SQLAllocHandle** con el *InputHandle* argumento establecido en SQL_HANDLE_DBC y también establecido en un identificador de entorno compartido, el Administrador de controladores intenta encontrar un entorno compartido existente que coincida con los atributos de entorno establecidos por la aplicación. Si no existe tal entorno, se crea uno, con un recuento de referencias (mantenido por el Administrador de controladores) de 1. Si se encuentra un entorno compartido coincidente, ese identificador se devuelve a la aplicación y se incrementa su recuento de referencias.  
  
 El Administrador de controladores no determina la conexión real que se usará hasta que se llame a **SQLConnect** o **SQLDriverConnect.** El Administrador de controladores utiliza las opciones de conexión en la llamada a **SQLConnect** (o las palabras clave de conexión en la llamada a **SQLDriverConnect**) y los atributos de conexión establecidos después de la asignación de conexión para determinar qué conexión en el grupo se debe usar. Para obtener más información, vea [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Asignar un identificador de instrucción  
 Un identificador de instrucción proporciona acceso a la información de la instrucción, como los mensajes de error, el nombre del cursor y la información de estado para el procesamiento de instrucciones SQL. Para obtener información general acerca de los identificadores de instrucción, vea [Identificadores de instrucción](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Para solicitar un identificador de instrucción, una aplicación se conecta a un origen de datos y, a continuación, llama a **SQLAllocHandle** antes de enviar instrucciones SQL. En esta llamada, *HandleType* debe establecerse en SQL_HANDLE_STMT y *InputHandle* debe establecerse en el identificador de conexión devuelto por la llamada a **SQLAllocHandle** que asignó ese identificador. El controlador asigna memoria para la información de instrucción, asocia el identificador de instrucción con la conexión especificada y devuelve el valor del identificador asociado en * \*OutputHandlePtr*. La aplicación pasa el * \*valor OutputHandlePtr* en todas las llamadas posteriores que requieren un identificador de instrucción. Para obtener más información, consulte Asignación de un identificador de [instrucción](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Cuando se asigna el identificador de instrucción, el controlador asigna automáticamente un conjunto de cuatro descriptores y asigna los identificadores de estos descriptores a los atributos de SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC e SQL_ATTR_IMP_PARAM_DESC instrucción. Estos se conocen como descriptores asignados *implícitamente.* Para asignar explícitamente un descriptor de aplicación, consulte la sección siguiente, "Asignación de un identificador de descriptor."  
  
## <a name="allocating-a-descriptor-handle"></a>Asignación de un controlador de descriptor  
 Cuando una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DESC, el controlador asigna un descriptor de aplicación. Estos se conocen como descriptores asignados *explícitamente.* La aplicación indica a un controlador que utilice un descriptor de aplicación asignado explícitamente en lugar de uno asignado automáticamente para un identificador de instrucción determinado mediante una llamada a la función **SQLSetStmtAttr** con el atributo SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC. Un descriptor de implementación no se puede asignar explícitamente, ni se puede especificar un descriptor de implementación en una llamada a la función **SQLSetStmtAttr.**  
  
 Los descriptores asignados explícitamente se asocian a un identificador de conexión en lugar de a un identificador de instrucción (como lo son los descriptores asignados automáticamente). Los descriptores permanecen asignados solo cuando una aplicación está realmente conectada a la base de datos. Dado que los descriptores asignados explícitamente están asociados a un identificador de conexión, una aplicación puede asociar un descriptor asignado explícitamente con más de una instrucción dentro de una conexión. Un descriptor de aplicación asignado implícitamente, por otro lado, no se puede asociar a más de un identificador de instrucción. (No se puede asociar con ningún identificador de instrucción que no sea el que se asignó.) Los identificadores de descriptor asignados explícitamente se pueden liberar explícitamente por la aplicación o mediante una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC o implícitamente cuando se cierra la conexión.  
  
 Cuando se libera el descriptor asignado explícitamente, el descriptor asignado implícitamente se asocia de nuevo a la instrucción. (El atributo SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC de esa instrucción se establece de nuevo en el identificador de descriptor asignado implícitamente.) Esto es cierto para todas las instrucciones que se asociaron con el descriptor asignado explícitamente en la conexión.  
  
 Para obtener más información acerca de los descriptores, consulte [Descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [Programa ODBC](../../../odbc/reference/sample-odbc-program.md)de ejemplo , [Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)y [Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberar un identificador de entorno, conexión, instrucción o descriptor|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparación de una declaración para la ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un campo descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
