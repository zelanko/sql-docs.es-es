---
title: Función SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9528280514be2eb2424b15a39ded3206aaca112f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104705"
---
# <a name="sqldriverconnect-function"></a>Función SQLDriverConnect
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLDriverConnect** es una alternativa a **SQLConnect**. Admite los orígenes de datos que requieren más información de conexión que los tres argumentos en **SQLConnect**, cuadros de diálogo para preguntar al usuario para toda la información de conexión y orígenes de datos que no estén definidos en el sistema información.  
  
 **SQLDriverConnect** proporciona los siguientes atributos de conexión:  
  
-   Establezca una conexión mediante una cadena de conexión que contiene el nombre del origen de datos, uno o más identificadores de usuario, una o varias de las contraseñas y otra información requerida por el origen de datos.  
  
-   Establezca una conexión mediante una cadena de conexión parcial o no hay información adicional; en este caso, el Administrador de controladores y el controlador pueden cada pedir al usuario información de conexión.  
  
-   Establecer una conexión a un origen de datos que no está definido en la información del sistema. Si la aplicación proporciona una cadena de conexión parcial, el controlador puede solicitar al usuario información de conexión.  
  
-   Establecer una conexión a un origen de datos mediante una cadena de conexión que se construye a partir de la información en un archivo DSN.  
  
 Una vez establecida una conexión, **SQLDriverConnect** devuelve la cadena de conexión completa. La aplicación puede usar esta cadena para las solicitudes de conexión posteriores. Para obtener más información, consulte [conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *WindowHandle*  
 [Entrada] Identificador de ventana. La aplicación puede pasar el identificador de la ventana primaria, si procede, o un puntero nulo si el identificador de ventana no es aplicable o **SQLDriverConnect** no presentará los cuadros de diálogo.  
  
 *InConnectionString*  
 [Entrada] Una cadena de conexión completa (vea la sintaxis de "Comentarios"), una cadena de conexión parcial o una cadena vacía.  
  
 *StringLength1*  
 [Entrada] Longitud de **InConnectionString*, en caracteres, si la cadena es Unicode o bytes si es de cadena ANSI o DBCS.  
  
 *OutConnectionString*  
 [Salida] Puntero a un búfer para la cadena de conexión completa. En la conexión correcta al origen de datos de destino, este búfer contiene la cadena de conexión completa. Las aplicaciones deben asignar al menos de 1.024 caracteres para este búfer.  
  
 Si *OutConnectionString* es NULL, *StringLength2Ptr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer apunta a *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Longitud de la **OutConnectionString* búfer en caracteres.  
  
 *StringLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponibles para devolver en \* *OutConnectionString*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength*, el completado de la cadena de conexión en \* *OutConnectionString* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null.  
  
 *DriverCompletion*  
 [Entrada] Marca que indica si el Administrador de controladores o el controlador debe pedir para obtener más información de conexión:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.  
  
 (Para obtener más información, vea "Comentarios".)  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDriverConnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *fHandleType*de SQL_HANDLE_DBC y un *hHandle* de *ConnectionHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDriverConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El búfer \* *OutConnectionString* no era lo suficientemente grande como para devolver la cadena de conexión completa, por lo que se truncó la cadena de conexión. Se devuelve la longitud de la cadena de conexión sin truncar en **StringLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S00|Atributo de cadena de conexión no válido|Se especificó una palabra clave de atributo no válido en la cadena de conexión (*InConnectionString*), pero el controlador fue capaz de conectarse al origen de datos de todos modos. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02|Valor de opción cambiado|El controlador no eran compatibles con el valor especificado que apunta el *ValuePtr* argumento en **SQLSetConnectAttr** y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S08|Error al guardar DSN de archivo|La cadena en  *\*InConnectionString* contiene un **FILEDSN** palabra clave, pero el archivo DSN no se ha guardado. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S09|Palabra clave no válida|(DM) en la cadena de  *\*InConnectionString* contiene un **SAVEFILE** palabra clave pero no un **controlador** o un **FILEDSN** palabra clave. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08001|No se puede establecer la conexión de cliente|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de la conexión en uso|(DM) especificado *ConnectionHandle* ya habían utilizado para establecer una conexión con un origen de datos y la conexión todavía estaba abierta.|  
|08004|El servidor rechazó la conexión|El origen de datos rechaza el establecimiento de la conexión por motivos de implementación.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que estaba intentando conectar el controlador antes de la **SQLDriverConnect** procesamiento de la función se ha completado.|  
|28000|Especificación de autorización no válido|El identificador de usuario o la cadena de autorización o ambos, como se especifica en la cadena de conexión (*InConnectionString*), han infringido las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*szMessageText* búfer describe el error y su causa.|  
|HY000|Error general: Dsn de archivo no válido|(DM) la cadena en **InConnectionString* contenía una palabra clave FILEDSN, pero no se encontró el nombre del archivo DSN.|  
|HY000|Error general: No se puede crear el búfer de archivo|(DM) la cadena en **InConnectionString* contenía una palabra clave FILEDSN, pero el archivo .dsn era ilegible.|  
|HY001|Error de asignación de memoria|El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la **SQLDriverConnect** función.<br /><br /> El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *ConnectionHandle*. Se llamó a la función, y antes que completó la ejecución, el [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se ha llamado en el *ConnectionHandle*y, a continuación, el **SQLDriverConnect** función se llamó de nuevo en el *ConnectionHandle*.<br /><br /> O bien, el **SQLDriverConnect** se llamó a la función, y antes que completó la ejecución, **SQLCancelHandle** se ha llamado en el *ConnectionHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) otra función ejecuta de forma asincrónica (no **SQLDriverConnect**) se llamó para el *ConnectionHandle* y aún se estaba ejecutando cuando el **SQLDriverConnect** se llamó a la función.|  
|HY013|Error de administración de memoria|El **SQLDriverConnect** no se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *StringLength1* era menor que 0 y no es igual a SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY092|Identificador de opción o atributo no válido|(DM) el *DriverCompletion* argumento era SQL_DRIVER_PROMPT y el *WindowHandle* argumento era un puntero nulo.|  
|HY110|Finalización del controlador no válido|(DM) el valor especificado para el argumento *DriverCompletion* no es igual a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_NOPROMPT o SQL_DRIVER_COMPLETE_REQUIRED.<br /><br /> (DM) se ha habilitado la agrupación de conexiones y el valor especificado para el argumento *DriverCompletion* no era igual en SQL_DRIVER_NOPROMPT.|  
|HYC00|Característica opcional no implementada|El controlador no es compatible con la versión de comportamiento ODBC que solicitó la aplicación.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de inicio de sesión antes de la conexión al origen de datos completado. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador que corresponda al nombre del origen de datos especificado no es compatible con la función.|  
|IM002|No se encuentra el origen de datos y se especificó ningún controlador predeterminado|Nombre especificado en la cadena de conexión del origen de datos (DM) (*InConnectionString*) fue no se encuentra en la información del sistema y no había ninguna especificación del controlador predeterminado.<br /><br /> (DM) no se encontró información del controlador de origen y el valor predeterminado de datos ODBC en la información del sistema.|  
|IM003|No se pudo cargar el controlador especificado|(DM) el controlador aparecen en la especificación del origen de datos en la información del sistema o especificado por el **controlador** palabra clave no se encontró o no se puede cargar por alguna otra razón.|  
|IM004|Conductor **SQLAllocHandle** en SQL_HANDLE_ENV error|(DM) durante **SQLDriverConnect**, el Administrador de controladores llama el controlador **SQLAllocHandle** funcionando con un *fHandleType* de SQL_HANDLE_ENV y el controlador devuelve un error.|  
|IM005|Conductor **SQLAllocHandle** en SQL_HANDLE_DBC error.|(DM) durante **SQLDriverConnect**, el Administrador de controladores llama el controlador **SQLAllocHandle** funcionando con un *fHandleType* de SQL_HANDLE_DBC y el controlador devuelve un error.|  
|IM006|Conductor **SQLSetConnectAttr** error|(DM) durante **SQLDriverConnect**, el Administrador de controladores llama el controlador **SQLSetConnectAttr** función y el controlador devolvían un error.|  
|IM007|Ningún origen de datos o el controlador especificado; cuadro de diálogo restringido|No se especificó ningún nombre de origen de datos o el controlador en la cadena de conexión y *DriverCompletion* era SQL_DRIVER_NOPROMPT.|  
|IM008|Error de diálogo.|El controlador intentó mostrar su cuadro de diálogo de inicio de sesión y no se pudo.<br /><br /> *WindowHandle* era un puntero nulo, y *DriverCompletion* no era SQL_DRIVER_NO_PROMPT.|  
|IM009|No se puede cargar el archivo DLL de traducción|El controlador no pudo cargar la DLL que se especificó para el origen de datos o para la conexión de traducción.|  
|IM010|Nombre de origen de datos es demasiado largo|(DM) el valor del atributo para la palabra clave DSN era más de SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nombre del controlador es demasiado largo|Valor de atributo (DM) para el **controlador** palabra clave era más de 255 caracteres.|  
|IM012|Error de sintaxis de la palabra clave DRIVER|Par de la palabra clave y valor (DM) para el **controlador** palabra clave contenía un error de sintaxis.<br /><br /> (DM) en la cadena de  *\*InConnectionString* contiene un **FILEDSN** palabra clave, pero el archivo DSN no contenía un **controlador** palabra clave o un  **DSN** palabra clave.|  
|IM014|El DSN especificado contiene un error de coincidencia de arquitectura entre el controlador y la aplicación|Aplicación de 32 bits (DM) usa un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM015|Error SQLDriverConnect del controlador en SQL_HANDLE_DBC_INFO_HANDLE|Si un controlador devuelve SQL_ERROR, el Administrador de controladores se devolverá SQL_ERROR a la aplicación y se producirá un error en la conexión.<br /><br /> Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar el conocimiento de grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
|S1118|Controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentarios  
 Una cadena de conexión tiene la siguiente sintaxis:  
  
 *cadena de conexión* :: = *cadena vacía*[;] &#124; *atributo*[;] &#124; *atributo*; *cadena de conexión*  
  
 *cadena vacía* :: =*atributo* :: = *palabra clave de atributo*=*atributo-valor* &#124; DRIVER = [{}] *valor del atributo*[}]  
  
 *attribute-keyword* ::= DSN &#124; UID &#124; PWD &#124; *driver-defined-attribute-keyword*  
  
 *attribute-value* ::= *character-string*  
  
 *driver-defined-attribute-keyword* ::= *identifier*  
  
 donde *cadena de caracteres* tiene cero o más caracteres; *identificador* tiene uno o más caracteres; *palabra clave de atributo* no distingue mayúsculas de minúsculas; *atributo-valor* puede distinguir mayúsculas de minúsculas; y el valor de la **DSN** palabra clave no consta únicamente de espacios en blanco.  
  
 ¿Debido a cadena e inicialización archivo gramática, palabras clave y atributo de valores de conexión que contienen los caracteres **[]{}(),? \*=! @** no estén entre llaves se deben evitar. El valor de la **DSN** palabra clave no puede constar sólo de espacios en blanco y no debe contener espacios en blanco iniciales. Debido a la gramática de la información del sistema, los nombres de origen de datos y las palabras clave no pueden contener la barra diagonal inversa (\\) caracteres.  
  
 Las aplicaciones no es necesario que agregue llaves alrededor del valor de atributo tras el **controlador** palabra clave a menos que el atributo contiene un punto y coma (;), en cuyo caso las llaves son obligatorias. Si el valor del atributo que recibe el controlador incluye llaves, el controlador no debe quitar, pero deben formar parte de la cadena de conexión devuelta.  
  
 ¿Un valor de cadena de conexión o DSN entre llaves ({}) que contiene los caracteres **[]{}(),? \*=! @** se pasa intacto al controlador. Sin embargo, al utilizar estos caracteres en una palabra clave, el Administrador de controladores devuelve un error cuando se trabaja con DSN de archivo, pero pasa la cadena de conexión para el controlador para las cadenas de conexión normal. Evite el uso de llaves incrustadas en un valor de palabra clave.  
  
 La cadena de conexión puede incluir cualquier número de palabras clave definidas por el controlador. Dado que el **controlador** palabra clave no utiliza información de la información del sistema, el controlador debe definir suficientes palabras clave para que un controlador puede conectarse a un origen de datos usando solo la información de la cadena de conexión. (Para obtener más información, consulte "Instrucciones de controlador", más adelante en esta sección). El controlador define qué palabras clave es necesarias para conectarse al origen de datos.  
  
 En la tabla siguiente se describe los valores de atributo de la **DSN**, **FILEDSN**, **controlador**, **UID**, **PWD**, y **SAVEFILE** palabras clave.  
  
|Palabra clave|Descripción del valor de atributo|  
|-------------|---------------------------------|  
|**DSN**|Nombre de un origen de datos devuelto por **SQLDataSources** o el cuadro de diálogo orígenes de datos de **SQLDriverConnect**.|  
|**FILEDSN**|Nombre de un archivo de DSN desde el que se generará una cadena de conexión del origen de datos. Estos orígenes de datos se denominan orígenes de datos de archivo.|  
|**CONTROLADOR**|Descripción del controlador tal como lo devuelve el **SQLDrivers** función. Por ejemplo, Rdb o SQL Server.|  
|**UID**|Identificador de usuario.|  
|**PWD**|La contraseña correspondiente para el identificador de usuario o una cadena vacía si no hay ninguna contraseña para el identificador de usuario (PWD =;).|  
|**SAVEFILE**|El nombre de archivo de un archivo de DSN en el que se deben guardar los valores de atributo de palabras clave utilizadas en realizar la conexión correcta, está presente.|  
  
 Para obtener información acerca de cómo una aplicación elige un origen de datos o un controlador, vea [elegir un origen de datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si todas las palabras clave se repite en la cadena de conexión, el controlador utiliza el valor asociado a la primera aparición de la palabra clave. Si el **DSN** y **controlador** palabras clave se incluyen en la misma cadena de conexión, el Administrador de controladores y el controlador usan cualquier palabra clave aparece en primer lugar.  
  
 El **FILEDSN** y **DSN** palabras clave son mutuamente excluyentes: cualquier palabra clave aparece en primer lugar se usa y se omitirá aquella que aparece el segundo. El **FILEDSN** y **controlador** palabras clave, por otro lado, no son mutuamente excluyentes. Si cualquier palabra clave aparece en una cadena de conexión con **FILEDSN**, a continuación, se usa el valor del atributo de la palabra clave en la cadena de conexión en lugar del valor de atributo de la misma palabra clave en el archivo DSN.  
  
 Si el **FILEDSN** se usa la palabra clave, las palabras clave especificadas en un archivo DSN se utilizan para crear una cadena de conexión. (Para obtener más información, consulte "Archivo de orígenes de datos," más adelante en esta sección). El **UID** palabra clave es opcional; puede crearse un archivo DSN con solo el **controlador** palabra clave. El **PWD** palabra clave no se almacena en un archivo DSN. El directorio predeterminado para guardar y cargar un archivo .dsn será una combinación de la ruta de acceso especificada por **CommonFileDir** en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion y "ODBC\DataSources". (Si CommonFileDir fuera "C:\Program Files\Common archivos", el directorio predeterminado sería "C:\Program programa\Common Files\ODBC\Data Sources").  
  
> [!NOTE]  
>  Un archivo DSN se puede manipular directamente mediante una llamada a la [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) y [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) funciones en el archivo DLL de instalador.  
  
 Si el **SAVEFILE** se usa la palabra clave, los valores de atributo de palabras clave utilizadas en realizar la conexión correcta, presente se guardará como un archivo DSN con el nombre del valor del atributo de la **SAVEFILE** palabra clave. El **SAVEFILE** palabra clave debe usarse junto con el **controlador** palabra clave, el **FILEDSN** palabra clave, o ambos, o la función devuelve SQL_SUCCESS_WITH_INFO con SQLSTATE 01S09 (palabra clave no válida). El **SAVEFILE** palabra clave debe aparecer antes de la **controlador** palabra clave en la cadena de conexión o los resultados se quedará sin definir.  
  
## <a name="driver-manager-guidelines"></a>Directrices de administrador de controladores  
 El Administrador de controladores se construye una cadena de conexión para pasar al controlador en el *InConnectionString* argumento de que el controlador **SQLDriverConnect** función. El Administrador de controladores no modifica el *InConnectionString* argumento pasado a él por la aplicación.  
  
 La acción del Administrador de controladores se basa en el valor de la *DriverCompletion* argumento:  
  
-   SQL_DRIVER_PROMPT: Si la cadena de conexión no contiene el **controlador**, **DSN**, o **FILEDSN** palabra clave, el Administrador de controladores muestra el cuadro de diálogo orígenes de datos. Construye una cadena de conexión desde el nombre del origen de datos devuelto por el cuadro de diálogo y cualquier otra palabra clave pasado por la aplicación. Si el nombre del origen de datos devuelto por el cuadro de diálogo está vacío, el Administrador de controladores especifica el par de valor de la palabra clave DSN = Default. (Este cuadro de diálogo no mostrará un origen de datos con el nombre "Default".)  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: Si la cadena de conexión especificada por la aplicación incluye el **DSN** palabra clave, el Administrador de controladores copia la cadena de conexión especificada por la aplicación. En caso contrario, toma las mismas acciones como lo hace cuando *DriverCompletion* es SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: El Administrador de controladores se copia la cadena de conexión especificada por la aplicación.  
  
 Si la cadena de conexión especificada por la aplicación contiene el **controlador** palabra clave, el Administrador de controladores copia la cadena de conexión especificada por la aplicación.  
  
 Uso de la cadena de conexión que ha construido, el Administrador de controladores determina qué controlador usar, se conecta a ese controlador y pasa la cadena de conexión que ha construido para el controlador; Para obtener más información acerca de la interacción de los controladores y el Administrador de controladores, consulte la sección "Comentarios" en [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Si la cadena de conexión no contiene el **controlador** palabra clave, el Administrador de controladores determina qué controlador usar como sigue:  
  
1.  Si la cadena de conexión contiene el **DSN** palabra clave, el Administrador de controladores recupera el controlador asociado con el origen de datos de la información del sistema.  
  
2.  Si la cadena de conexión no contiene el **DSN** no se encuentra la palabra clave o el origen de datos, el Administrador de controladores recupera el controlador asociado con el origen de datos predeterminado de la información del sistema. (Para obtener más información, consulte [subclave predeterminada](../../../odbc/reference/install/default-subkey.md).) El Administrador de controladores se cambia el valor de la **DSN** palabra clave en la cadena de conexión en "DEFAULT".  
  
3.  Si el **DSN** palabra clave en la cadena de conexión se establece en "DEFAULT", el Administrador de controladores recupera el controlador asociado con el origen de datos predeterminado de la información del sistema.  
  
4.  Si no se encuentra el origen de datos y no se encuentra el origen de datos de forma predeterminada, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE IM002 (no se encuentra el origen de datos y se especificó ningún controlador predeterminado).  
  
## <a name="file-data-sources"></a>Orígenes de datos de archivo  
 Si la cadena de conexión especificado por la aplicación en la llamada a **SQLDriverConnect** contiene el **FILEDSN** no se ha sustituido la palabra clave y esta palabra clave, ya sea por la **DSN**o **controlador** palabra clave y, a continuación, el Administrador de controladores se crea una cadena de conexión con la información en el archivo DSN y la *InConnectionString* argumento. El Administrador de controladores procede como sigue:  
  
1.  Comprueba si el nombre de archivo del archivo DSN es válido. Si no, devuelve SQL_ERROR con SQLSTATE IM014 (nombre del DSN de archivo no válido). Si el nombre de archivo es una cadena vacía ("") y SQL_DRIVER_NOPROMPT no se especifica, el **File-Open** se muestra el cuadro de diálogo. Si el nombre de archivo contiene una ruta de acceso válida, pero ningún nombre de archivo o un nombre de archivo no válido y no se especifica SQL_DRIVER_NOPROMPT, el **File-Open** se muestra el cuadro de diálogo con el directorio actual establecido con la especificada en el nombre de archivo. Si el nombre de archivo es una cadena vacía ("") o el nombre de archivo contiene una ruta de acceso válida, pero ningún nombre de archivo o un nombre de archivo no válido y se especifica SQL_DRIVER_NOPROMPT, a continuación, se devuelve SQL_ERROR con SQLSTATE IM014 (nombre del DSN de archivo no válido).  
  
2.  Lee todas las palabras clave en la sección [ODBC] del archivo DSN. Si el **controlador** palabra clave no está presente, devuelve SQL_ERROR con SQLSTATE IM012 (error de sintaxis de palabra clave Driver), excepto que el archivo DSN es no se puede compartir y, por tanto, solo contiene el **DSN** palabra clave.  
  
     Si el origen de datos de archivo es no se puede compartir, el Administrador de controladores lee el valor de la **DSN** palabra clave y se conecta según sea necesario para el origen de datos de usuario o sistema que señala el origen de datos de archivo no se puede compartir. No se realizan los pasos 3 a 5.  
  
3.  Construye una cadena de conexión para el controlador. La cadena de conexión del controlador es la unión de las palabras clave especificadas en el archivo DSN y aquellas especificadas en la cadena de conexión de aplicación original. Reglas para la construcción de la cadena de conexión del controlador que se superponen a las palabras clave son los siguientes:  
  
    -   Si el **controlador** palabra clave existe en la cadena de conexión de la aplicación y los controladores especificados por el **controlador** palabras clave no son los mismos en el archivo de DSN y la cadena de conexión de la aplicación, el información del controlador en el archivo DSN se omite y se usa la información del controlador en la cadena de conexión de la aplicación. Si los controladores especificados por el **controlador** palabra clave son los mismos en el archivo DSN y la cadena de conexión de la aplicación y, después, donde se superponen todas las palabras clave, los especificados en la cadena de conexión de la aplicación tienen prioridad sobre las Si se especifica en el archivo de DSN.  
  
    -   En la nueva cadena de conexión, el **FILEDSN** se elimina la palabra clave.  
  
4.  Carga el controlador mediante una búsqueda en la entrada del registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\\< nombreDeControlador\>\Driver donde \<nombreDeControlador > especificado por el **controlador** palabra clave.  
  
5.  Pasa al controlador de la cadena de conexiones nuevo.  
  
 Para obtener ejemplos de archivos .dsn, consulte [conecta orígenes de datos de archivo utilizando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>Palabra clave SAVEFILE  
 Si la cadena de conexión especificada por la aplicación contiene el **SAVEFILE** palabra clave y, a continuación, el Administrador de controladores se guarda la cadena de conexión en un archivo de DSN. El Administrador de controladores procede como sigue:  
  
1.  Comprueba si el nombre de archivo del archivo .dsn incluido como el valor del atributo de la **SAVEFILE** palabra clave es válida. Si no, devuelve SQL_ERROR con SQLSTATE IM014 (nombre del DSN de archivo no válido). La validez del nombre de archivo viene determinada por las reglas de nomenclatura estándar del sistema. Si el nombre de archivo es una cadena vacía ("") y el *DriverCompletion* argumento no es SQL_DRIVER_NOPROMPT, a continuación, el nombre de archivo es válido. Si el nombre de archivo ya existe, a continuación, si *DriverCompletion* es SQL_DRIVER_NOPROMPT, se sobrescribe el archivo. Si *DriverCompletion* es SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, un cuadro de diálogo pide al usuario que especifique si se debe sobrescribir el archivo. Si No se especifica, el **archivo-Guardar** aparece el cuadro de diálogo.  
  
2.  Si el controlador devuelve SQL_SUCCESS y el nombre de archivo no era una cadena vacía, el Administrador de controladores se escribe la información de conexión devuelta en el *OutConnectionString* argumento en el archivo especificado con el formato especificado en la sección "Cadenas de conexión" anteriormente en esta sección.  
  
3.  Si el controlador devuelve SQL_SUCCESS y el nombre de archivo es una cadena vacía (""), a continuación llama el Administrador de controladores del **archivo-Guardar** cuadro de diálogo común con el *hwnd* especificado y escribe la información de conexión devuelto en *OutConnectionString* al archivo especificado en el cuadro de diálogo común de archivo-guardar con el formato especificado en la sección "Cadenas de conexión" anteriormente en esta sección.  
  
4.  Si el controlador devuelve SQL_SUCCESS, devuelve el *OutConnectionString* argumento que contiene la cadena de conexión a la aplicación.  
  
5.  Si el controlador devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR, el Administrador de controladores devuelve el valor de SQLSTATE a la aplicación.  
  
## <a name="driver-guidelines"></a>Directrices de controlador  
 El controlador comprueba si la cadena de conexión que se le pasada por el Administrador de controladores contiene la **DSN** o **controlador** palabra clave. Si la cadena de conexión contiene el **controlador** palabra clave, el controlador no puede recuperar información sobre el origen de datos de la información del sistema. Si la cadena de conexión contiene el **DSN** palabra clave o no contiene el **DSN** o **controlador** palabra clave, el controlador puede recuperar información sobre el origen de datos desde la información del sistema como sigue:  
  
1.  Si la cadena de conexión contiene el **DSN** palabra clave, el controlador recupera la información del origen de datos especificado.  
  
2.  Si la cadena de conexión no contiene el **DSN** palabra clave, no se encuentra el origen de datos especificado, o el **DSN** palabra clave está establecida en "DEFAULT", el controlador recupera la información de origen de datos predeterminado .  
  
 El controlador utiliza toda la información que recupera de la información del sistema para aumentar la información pasada en la cadena de conexión. Si la información de la información del sistema duplica la información en la cadena de conexión, el controlador utiliza la información de la cadena de conexión.  
  
 En función del valor de *DriverCompletion*, el controlador solicita al usuario información de conexión, como el Id. de usuario y la contraseña y se conecta al origen de datos:  
  
-   SQL_DRIVER_PROMPT: El controlador muestra un cuadro de diálogo con los valores de la información del sistema y de cadena de conexión (si existe) como valores iniciales. Cuando el usuario cierra el cuadro de diálogo, el controlador se conecta al origen de datos. También construye una cadena de conexión desde el valor de la **DSN** o **controlador** palabra clave en \* *InConnectionString* y la información devuelta desde el cuadro de diálogo. Coloca esta cadena de conexión en el **OutConnectionString* búfer.  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: Si la cadena de conexión contiene información suficiente y esa información es correcta, el controlador se conecta al origen de datos y copias \* *InConnectionString* a \* *OutConnectionString* . Si cualquier información que falta o es incorrecta, el controlador tiene las mismas acciones como lo hace cuando *DriverCompletion* es SQL_DRIVER_PROMPT, excepto si *DriverCompletion* es SQL_DRIVER_COMPLETE_ Es necesario, el controlador desactiva los controles de información no es necesaria para conectarse al origen de datos.  
  
-   SQL_DRIVER_NOPROMPT: Si la cadena de conexión contiene información suficiente, el controlador se conecta al origen de datos y copias \* *InConnectionString* a \* *OutConnectionString*. En caso contrario, el controlador devuelve SQL_ERROR para **SQLDriverConnect**.  
  
 En una conexión correcta al origen de datos, el controlador también establece \* *StringLength2Ptr* a la longitud de la cadena de conexión de salida que está disponible para devolver en **OutConnectionString*.  
  
 Si el usuario cancela un cuadro de diálogo presentado por el Administrador de controladores o el controlador, **SQLDriverConnect** devuelve SQL_NO_DATA.  
  
 Para obtener información acerca de cómo interactúan el Administrador de controladores y el controlador durante el proceso de conexión, vea [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Si un controlador es compatible con **SQLDriverConnect**, la sección de la palabra clave de controlador de la información del sistema para el controlador debe contener el **ConnectFunctions** palabra clave con el segundo carácter establecida en "S".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Conectarse cuando la agrupación de conexiones está habilitada.  
 Agrupación de conexiones permite a reutilizar una conexión que ya se ha creado una aplicación. Cuando **SQLDriverConnect** se llama, el Administrador de controladores intenta realizar la conexión mediante una conexión que forma parte de un grupo de conexiones en un entorno que se ha designado para la agrupación de conexiones. Para obtener más información sobre la agrupación de conexiones, vea [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Una aplicación puede establecer SQL_ATTR_RESET_CONNECTION antes de llamar a SQLDisconnect en una conexión donde está habilitada la agrupación. Para obtener más información, consulte [función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Las restricciones siguientes se aplican cuando una aplicación llama a **SQLDriverConnect** para conectarse a una conexión agrupada:  
  
-   No se realizan ningún procesamiento de agrupación de conexiones cuando la **SAVEFILE** se especifica la palabra clave en la cadena de conexión.  
  
-   Si está habilitada la agrupación de conexiones, **SQLDriverConnect** se puede llamar solo con un *DriverCompletion* argumento de SQL_DRIVER_NOPROMPT; si **SQLDriverConnect** se denomina con cualquier otro *DriverCompletion*, HY110 SQLSTATE se devolverán (finalización del controlador no válido).  
  
## <a name="connection-attributes"></a>Atributos de conexión  
 El atributo de conexión SQL_ATTR_LOGIN_TIMEOUT, establecer mediante **SQLSetConnectAttr**, define el número de segundos de espera para que una solicitud de inicio de sesión para completar con una conexión correcta con el controlador antes de volver a la aplicación. Si el usuario se le pide para completar la cadena de conexión, un período de espera para cada solicitud de inicio de sesión comienza cuando el controlador inicia el proceso de conexión.  
  
 El controlador abre la conexión en modo de acceso SQL_MODE_READ_WRITE de forma predeterminada. Para establecer el modo de acceso a SQL_MODE_READ_ONLY, la aplicación debe llamar a **SQLSetConnectAttr** con el atributo SQL_ATTR_ACCESS_MODE antes de llamar a **SQLDriverConnect**.  
  
 Si una biblioteca de traducción predeterminado está especificada en la información del sistema para el origen de datos, el controlador lo carga. Puede cargar una biblioteca de traducción diferente mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_LIB. Se puede especificar una opción de conversión mediante una llamada a **SQLSetConnectAttr** con la opción SQL_ATTR_TRANSLATE_OPTION.  
  
 Para obtener más información, consulte [conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Consulte también [programa de ejemplo ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Detectar y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconexión de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Devuelve la descripción de los controladores y atributos|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberar un identificador|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
