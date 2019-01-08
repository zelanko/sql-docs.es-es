---
title: Función SQLAllocHandle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0a075b96e7a29cef4a10f034147732bf03f64b2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538875"
---
# <a name="sqlallochandle-function"></a>Función SQLAllocHandle
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: 92 ISO  
  
 **Resumen**  
 **SQLAllocHandle** asigna un identificador de entorno, conexión, instrucción o descriptor.  
  
> [!NOTE]  
>  Esta función es una función genérica para la asignación de identificadores que reemplaza las funciones ODBC 2.0 **SQLAllocConnect**, **SQLAllocEnv**, y **SQLAllocStmt**. Para permitir que aplicaciones que llaman a **SQLAllocHandle** para trabajar con ODBC 2. *x* controladores, una llamada a **SQLAllocHandle** se asigna en el Administrador de controladores a **SQLAllocConnect**, **SQLAllocEnv**, o  **SQLAllocStmt**, según corresponda. Para obtener más información, vea "Comentarios". Para obtener más información sobre lo que el Administrador de controladores asigna esta función cuando una aplicación ODBC 3. *x* aplicación funciona con un ODBC 2. *x* controladores, consulte [asignación de funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo de identificador que se asignen por **SQLAllocHandle**. Debe ser uno de los siguientes valores:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN se utiliza únicamente por el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar el conocimiento de grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Entrada] El identificador de entrada en cuyo contexto es asignar el nuevo identificador. Si *HandleType* es SQL_HANDLE_ENV, esto es SQL_NULL_HANDLE. Si *HandleType* es SQL_HANDLE_DBC, debe ser un identificador de entorno y, si es SQL_HANDLE_STMT o SQL_HANDLE_DESC, debe ser un identificador de conexión.  
  
 *OutputHandlePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el identificador a la estructura de datos recién asignado.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE o SQL_ERROR.  
  
 Al asignar un identificador que no sea un identificador de entorno, si **SQLAllocHandle** devuelve SQL_ERROR, establece *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT o SQL_NULL_HDESC, dependiendo de la valor de *HandleType*, a menos que el argumento de salida es un puntero nulo. La aplicación, a continuación, puede obtener información adicional de la estructura de datos de diagnóstico asociada con el identificador en el *InputHandle* argumento.  
  
## <a name="environment-handle-allocation-errors"></a>Errores de asignación de identificador de entorno  
 Asignación de entorno se produce tanto en el Administrador de controladores y dentro de cada controlador. El error devuelto por **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV depende del nivel en el que se produjo el error.  
  
 Si el Administrador de controladores no se puede asignar memoria para  *\*OutputHandlePtr* cuando **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se llama, o la aplicación proporciona un puntero nulo para *OutputHandlePtr*, **SQLAllocHandle** devuelve SQL_ERROR. Establece el Administrador de controladores **OutputHandlePtr* a SQL_NULL_HENV (a menos que la aplicación proporciona un puntero nulo, que devuelve SQL_ERROR). No hay ningún identificador con el que se va a asociar la información de diagnóstico adicional.  
  
 El Administrador de controladores no llama a la función de asignación de identificador de entorno de nivel de controlador hasta que la aplicación llama a **SQLConnect**, **SQLBrowseConnect**, o **SQLDriverConnect**. Si se produce un error en el nivel de controlador **SQLAllocHandle** función y, después, en el nivel de administrador de controladores **SQLConnect**, **SQLBrowseConnect**, o  **SQLDriverConnect** función devuelve SQL_ERROR. La estructura de datos de diagnóstico contiene SQLSTATE IM004 (conductor **SQLAllocHandle** error). El error se devuelve en un identificador de conexión.  
  
 Para obtener más información sobre el flujo de llamadas de función entre el Administrador de controladores y un controlador, consulte [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLAllocHandle** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con los valores adecuados *HandleType* y *controlar* establecido en el valor de *InputHandle*. SQL_SUCCESS_WITH_INFO (pero no SQL_ERROR) se pueden devolver para el *OutputHandle* argumento. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLAllocHandle** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) el *HandleType* argumento era SQL_HANDLE_STMT o SQL_HANDLE_DESC, pero la conexión especificada por el *InputHandle* argumento no estaba abierto. Debe completar correctamente el proceso de conexión (y la conexión debe estar abierta) para que el controlador asignar una instrucción o descriptor de controlar.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el **MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El Administrador de controladores (DM) no pudo asignar memoria para el identificador especificado.<br /><br /> El controlador no pudo asignar memoria para el identificador especificado.|  
|HY009|Uso no válido del puntero nulo|(DM) el *OutputHandlePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) el *HandleType* argumento era SQL_HANDLE_DBC, y **SQLSetEnvAttr** no se ha llamado para establecer el atributo de entorno SQL_ODBC_VERSION.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la **InputHandle** y aún se estaba ejecutando cuando el **SQLAllocHandle** llamada a función con **HandleType** establecido SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY013|Error de administración de memoria|El *HandleType* argumento era SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC; y no se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente condiciones.|  
|HY014 SE|El límite de número de identificadores superado|El límite definido por el controlador para el número de identificadores que se pueden asignar para el tipo de identificador indicado por el *HandleType* se ha alcanzado el argumento.|  
|HY092|Identificador de opción o atributo no válido|(DM) el *HandleType* argumento no era: SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT o SQL_HANDLE_DESC.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El *HandleType* argumento era SQL_HANDLE_DESC y el controlador era un ODBC 2. *x* controlador.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el *HandleType* argumento era SQL_HANDLE_STMT y el controlador no era un controlador ODBC válido.<br /><br /> (DM) el *HandleType* argumento era SQL_HANDLE_DESC y el controlador no admite asignar un identificador de descriptor.|  
  
## <a name="comments"></a>Comentarios  
 **SQLAllocHandle** se usa para asignar identificadores para los entornos, las conexiones, instrucciones y los descriptores de, como se describe en las secciones siguientes. Para obtener información general acerca de los identificadores, vea [identificadores](../../../odbc/reference/develop-app/handles.md).  
  
 Más de un identificador de entorno, conexión o la instrucción se puede asignar una aplicación a la vez si varias asignaciones son compatibles con el controlador. En ODBC, no se define ningún límite en el número de entorno, conexión, instrucción o identificadores de descriptor que se pueden asignar en cualquier momento. Los controladores pueden imponer un límite en el número de un determinado tipo de identificador que se puede asignar a la vez; Para obtener más información, consulte la documentación del controlador.  
  
 Si la aplicación llama a **SQLAllocHandle** con  *\*OutputHandlePtr* establecido en un entorno, la conexión, la instrucción o el identificador de descriptor que ya existe, el controlador sobrescribe el información asociada con el *controlar*, a menos que la aplicación está con conexión agrupación (consulte "Asignación de un entorno de atributo de agrupación de conexiones" más adelante en esta sección). El Administrador de controladores no se comprueba para ver si el *controlar* introducido en  *\*OutputHandlePtr* ya está en uso, ni tampoco comprobar el contenido de un controlador anterior antes de sobrescribirlos .  
  
> [!NOTE]  
>  Es incorrecta programación de aplicaciones de ODBC para llamar a **SQLAllocHandle** dos veces con la misma variable de aplicación definida para  *\*OutputHandlePtr* sin llamar a  **SQLFreeHandle** para liberar el identificador antes de reasignación de él. Sobrescribir ODBC controla de manera podría provocar un comportamiento incoherente o errores por parte de los controladores ODBC.  
  
 En sistemas operativos que admiten varios subprocesos, las aplicaciones pueden usar el mismo identificador de entorno, conexión, instrucción o descriptor en subprocesos diferentes. Los controladores, por tanto, deben admitir el acceso multiproceso seguro a esta información; Por ejemplo, una manera de lograr esto, es mediante el uso de un semáforo o una sección crítica. Para obtener más información acerca de los subprocesos, vea [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** no establece el atributo de entorno SQL_ATTR_ODBC_VERSION cuando se llama para asignar un identificador de entorno; debe establecerse el atributo de entorno mediante la aplicación o SQLSTATE HY010 será (error de secuencia de función) devuelve cuando **SQLAllocHandle** se llama para asignar un identificador de conexión.  
  
 Para las aplicaciones compatibles con estándares, **SQLAllocHandle** se asigna a **SQLAllocHandleStd** en tiempo de compilación. Es la diferencia entre estas dos funciones que **SQLAllocHandleStd** establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3 cuando se llama con el *HandleType* argumento establecido en SQL _HANDLE_ENV. Esto se hace porque las aplicaciones compatibles con los estándares son siempre ODBC 3. *x* aplicaciones. Además, los estándares no requieren la versión de la aplicación se registre. Esta es la única diferencia entre estas dos funciones. de lo contrario, son idénticos. **SQLAllocHandleStd** se asigna a **SQLAllocHandle** dentro del Administrador de controladores. Por lo tanto, no es necesario implementar controladores de terceros **SQLAllocHandleStd**.  
  
 Las aplicaciones de ODBC 3.8 deben usar:  
  
-   **SQLAllocHandle y no SQLAllocHandleStd** para asignar un identificador de entorno.  
  
-   **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3_80.  
  
## <a name="allocating-an-environment-handle"></a>Asignar un identificador de entorno  
 Un identificador de entorno proporciona acceso a información global, como identificadores de conexión válida e identificadores de conexión activa. Para obtener información general acerca de los identificadores de entorno, consulte [identificadores de entorno](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Para solicitar un identificador de entorno, una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y un *InputHandle* de SQL_NULL_HANDLE. El controlador asigna memoria para la información del entorno y la pasa el valor del identificador del asociado de nuevo en el  *\*OutputHandlePtr* argumento. Las fases de la aplicación la  *\*OutputHandle* valor en todas las llamadas subsiguientes que requieren un argumento de identificador de entorno. Para obtener más información, consulte [asignar el entorno de controlar](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 En el identificador del entorno de un administrador de controladores, si ya existe el identificador de entorno de un controlador, a continuación, **SQLAllocHandle** con un *HandleType* no se llama en ese controlador de SQL_HANDLE_ENV cuando un conexión se realiza, solo **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC. Si el identificador de un controlador de entorno no existe en el identificador de entorno del Administrador de controladores, SQLAllocHandle con un HandleType SQL_HANDLE_ENV y SQLAllocHandle con un HandleType de SQL_HANDLE_DBC se llaman en el controlador cuando la primera conexión identificador del entorno está conectado al controlador.  
  
 Cuando se procesa el Administrador de controladores del **SQLAllocHandle** funcionando con un *HandleType* de SQL_HANDLE_ENV, comprueba la **seguimiento** palabra clave en la sección [ODBC] del sistema información. Si se establece en 1, el Administrador de controladores habilita el seguimiento de la aplicación actual. Si se establece la marca de seguimiento, seguimiento comienza cuando el primer identificador de entorno se asigna y termina cuando se libera el último identificador del entorno. Para obtener más información, consulte [configurar orígenes de datos](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Después de asignar un identificador de entorno, debe llamar una aplicación **SQLSetEnvAttr** en el identificador del entorno para establecer el atributo de entorno SQL_ATTR_ODBC_VERSION. Si no se establece este atributo antes **SQLAllocHandle** se llama para asignar un identificador de conexión en el entorno, la llamada a asignar la conexión devolverá SQLSTATE HY010 (función de error de secuencia). Para obtener más información, consulte [declarar ODBC versión de la aplicación](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Asignación de entornos compartidos para la agrupación de conexiones  
 Los entornos pueden compartirse entre varios componentes en un único proceso. Un entorno compartido puede usarse por más de un componente al mismo tiempo. Cuando un componente utiliza un entorno compartido, puede usar las conexiones agrupadas, que le permiten asignar y usar una conexión existente sin necesidad de volver a crear dicha conexión.  
  
 Antes de asignar un entorno compartido que puede utilizarse para la agrupación de conexiones, debe llamar una aplicación **SQLSetEnvAttr** para establecer el atributo de entorno SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_ HENV. **SQLSetEnvAttr** en este caso, se llama con *EnvironmentHandle* establecido en null, lo que hace que el atributo de un atributo de nivel de proceso.  
  
 Después de que se ha habilitado la agrupación de conexiones, una aplicación llama a **SQLAllocHandle** con el *HandleType* argumento establecido en SQL_HANDLE_ENV. El entorno asignado por esta llamada será un entorno compartido implícito porque se ha habilitado la agrupación de conexiones.  
  
 Cuando se asigna a un entorno compartido, no se determina el entorno que se utilizará hasta **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama. En ese momento, el Administrador de controladores intenta encontrar un entorno existente que coincide con los atributos de entorno solicitados por la aplicación. Si no existe ningún entorno de este tipo, se crea uno como un entorno compartido. El Administrador de controladores mantiene un recuento de referencias para cada entorno compartido. el recuento se establece en 1 cuando el entorno se crea por primera vez. Si se encuentra un entorno coincidente, se devuelve el identificador de dicho entorno a la aplicación y se incrementa el recuento de referencias. Un identificador de entorno asignado de esta manera puede usarse en cualquier función ODBC que acepta un identificador de entorno como argumento de entrada.  
  
## <a name="allocating-a-connection-handle"></a>Asignar un identificador de conexión  
 Un identificador de conexión proporciona acceso a información como la instrucción en válida y abrir identificadores de descriptor en la conexión y si es actualmente una transacción. Para obtener información general acerca de los identificadores de conexión, consulte [identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Para solicitar un identificador de conexión, una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC. El *InputHandle* argumento está establecido en el identificador de entorno que devolvió la llamada a **SQLAllocHandle** que había asignado ese identificador. El controlador asigna memoria para la información de conexión y la pasa el valor del identificador del asociado de nuevo en  *\*OutputHandlePtr*. Las fases de la aplicación la  *\*OutputHandlePtr* valor en todas las llamadas subsiguientes que requieren un identificador de conexión. Para obtener más información, consulte [asignar un identificador de conexión](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 Procesa el Administrador de controladores del **SQLAllocHandle** de función y llama al controlador **SQLAllocHandle** función cuando la aplicación llama **SQLConnect**, **SQLBrowseConnect**, o **SQLDriverConnect**. (Para obtener más información, consulte [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Si no se establece el atributo de entorno SQL_ATTR_ODBC_VERSION antes **SQLAllocHandle** se llama para asignar un identificador de conexión en el entorno, la llamada a asignar la conexión devolverá SQLSTATE HY010 (función de la secuencia Error).  
  
 Cuando una aplicación llama **SQLAllocHandle** con el *InputHandle* argumento establecido en SQL_HANDLE_DBC y también se establece en un identificador de entorno compartido, el Administrador de controladores intenta encontrar un compartido existente entorno que coincida con los atributos de entorno establecidos por la aplicación. Si no existe ningún entorno de este tipo, se crea uno, con un recuento de referencias (mantenido por el Administrador de controladores) de 1. Si comparte una coincidencia se encuentra el entorno, ese identificador se devuelve a la aplicación y su recuento de referencias se incrementa.  
  
 La conexión real que va a utilizar no viene determinada por el Administrador de controladores hasta **SQLConnect** o **SQLDriverConnect** se llama. El Administrador de controladores utiliza las opciones de conexión en la llamada a **SQLConnect** (o las palabras clave de conexión en la llamada a **SQLDriverConnect**) y establecen los atributos de conexión después de la asignación de la conexión a Determine qué conexión en el grupo debe usarse. Para obtener más información, consulte [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Asignar un identificador de instrucción  
 Un identificador de instrucción proporciona acceso a información de la instrucción, como los mensajes de error, el nombre del cursor y la información de estado para procesar una instrucción SQL. Para obtener información general acerca de identificadores de instrucciones, consulte [identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Para solicitar un identificador de instrucción, una aplicación se conecta a un origen de datos y, a continuación, llama a **SQLAllocHandle** antes de enviar instrucciones SQL. En esta llamada, *HandleType* debe establecerse en SQL_HANDLE_STMT y *InputHandle* debe establecerse en el identificador de conexión que devolvió la llamada a **SQLAllocHandle** que asigna ese identificador. El controlador asigna memoria para la información de la instrucción, se asocia el identificador de instrucción con la conexión especificada y pasa el valor del identificador del asociado de nuevo en  *\*OutputHandlePtr*. Las fases de la aplicación la  *\*OutputHandlePtr* valor en todas las llamadas subsiguientes que requieren un identificador de instrucción. Para obtener más información, consulte [asignar un identificador de instrucciones](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Cuando se asigna el identificador de instrucción, el controlador automáticamente asigna un conjunto de descriptores de cuatro y asigna los identificadores de estos descriptores al SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC y SQL_ATTR_IMP_PARAM_DESC atributos de instrucción. Estos se conocen como *implícitamente* asignado descriptores. Para asignar explícitamente un descriptor de aplicación, consulte la sección siguiente, "Asignar un identificador de Descriptor".  
  
## <a name="allocating-a-descriptor-handle"></a>Asignar un identificador de Descriptor  
 Cuando una aplicación llama **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DESC, el controlador asigna un descriptor de la aplicación. Estos se conocen como *explícitamente* asignado descriptores. La aplicación dirige un controlador para usar un descriptor de aplicación asignados explícitamente en lugar de uno asignado automáticamente para un identificador de instrucción determinada mediante una llamada a la **SQLSetStmtAttr** con el SQL_ATTR_APP_ROW_DESC (función) atributo SQL_ATTR_APP_PARAM_DESC o. No se puede asignar explícitamente un descriptor de implementación, ni puede especificarse un descriptor de implementación en un **SQLSetStmtAttr** llamada de función.  
  
 Descriptores asignados explícitamente se asocian con un identificador de conexión en lugar de un identificador de instrucción (como descriptores asignados automáticamente). Descriptores permanecen asignados solo cuando una aplicación está realmente conectada a la base de datos. Porque descriptores asignados explícitamente están asociados con un identificador de conexión, una aplicación puede asociar un descriptor asignado explícitamente a más de una instrucción dentro de una conexión. Un descriptor de aplicación asignado de forma implícita, por otro lado, no se puede asociar con más de un identificador de instrucción. (No puede asociarse con cualquier identificador de instrucción distinta de la que se asignó.) Se pueden liberar explícitamente los identificadores de descriptor asignado explícitamente por la aplicación o mediante una llamada a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DESC, o implícitamente cuando la conexión es cerrado.  
  
 Cuando se libera el descriptor asignado explícitamente, el descriptor implícitamente asignado nuevo está asociado con la instrucción. (El atributo SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC para esa instrucción nuevo se establece en el identificador de descriptor asignado de forma implícita). Esto es cierto para todas las instrucciones que se asociaron con el descriptor asignado explícitamente en la conexión.  
  
 Para obtener más información acerca de los descriptores, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [programa ODBC de ejemplo](../../../odbc/reference/sample-odbc-program.md), [función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), y [función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberar un identificador de entorno, conexión, instrucción o descriptor|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Configuración de un campo de descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
