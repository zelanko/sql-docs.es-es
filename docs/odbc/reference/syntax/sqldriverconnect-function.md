---
title: Función SQLDriverConnect | Documentos de Microsoft
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
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 367a265c33f3c4520b4885524627fca4261829a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-function"></a>Función SQLDriverConnect
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLDriverConnect** es una alternativa a **SQLConnect**. Admite orígenes de datos que requieren más información de conexión que los tres argumentos en **SQLConnect**, cuadros de diálogo para pedir al usuario para toda la información de conexión y orígenes de datos que no estén definidos en el sistema información.  
  
 **SQLDriverConnect** proporciona los siguientes atributos de conexión:  
  
-   Establecer una conexión utilizando una cadena de conexión que contiene el nombre de origen de datos, uno o más identificadores de usuario, una o varias contraseñas y otra información requerida por el origen de datos.  
  
-   Establecer una conexión utilizando una cadena de conexión parcial o no hay información adicional; en este caso, el Administrador de controladores y el controlador pueden cada pedir al usuario información de conexión.  
  
-   Establecer una conexión a un origen de datos que no está definido en la información del sistema. Si la aplicación proporciona una cadena de conexión parcial, el controlador puede pedir al usuario información de conexión.  
  
-   Establecer una conexión con un origen de datos mediante una cadena de conexión que se construyen a partir de la información en un archivo de DSN.  
  
 Una vez establecida una conexión, **SQLDriverConnect** devuelve la cadena de conexión completa. La aplicación puede utilizar esta cadena para las solicitudes de conexión posteriores. Para obtener más información, consulte [conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 *IdentificadorConexión*  
 [Entrada] Identificador de conexión.  
  
 *WindowHandle*  
 [Entrada] Identificador de ventana. La aplicación puede pasar el identificador de la ventana primaria, si procede, o un puntero nulo si el identificador de ventana no es aplicable o **SQLDriverConnect** no presentará los cuadros de diálogo.  
  
 *InConnectionString*  
 [Entrada] Una cadena de conexión completa (vea la sintaxis de "Comentarios"), una cadena de conexión parcial o una cadena vacía.  
  
 *StringLength1*  
 [Entrada] Longitud de **InConnectionString*, en caracteres, si la cadena es Unicode o bytes si cadena es ANSI o DBCS.  
  
 *OutConnectionString*  
 [Salida] Puntero a un búfer para la cadena de conexión completa. Tras una conexión correcta con el origen de datos de destino, este búfer contiene la cadena de conexión completa. Las aplicaciones deben asignar al menos de 1.024 caracteres para este búfer.  
  
 Si *OutConnectionString* es NULL, *StringLength2Ptr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer que señala *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Longitud de la **OutConnectionString* búfer en caracteres.  
  
 *StringLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponible para devolver en \* *OutConnectionString*. Si el número de caracteres disponibles para devolver es mayor o igual que *BufferLength*, el completado de la cadena de conexión en \* *OutConnectionString* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null.  
  
 *DriverCompletion*  
 [Entrada] Marca que indica si el Administrador de controladores o el controlador debe solicitar más información de conexión:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.  
  
 (Para obtener más información, vea "Comentarios".)  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLDriverConnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con una *fHandleType*de SQL_HANDLE_DBC y un *hHandle* de *IdentificadorConexión*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDriverConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|El búfer \* *OutConnectionString* no era lo suficientemente grande como para devolver la cadena de conexión completa, por lo que se trunca la cadena de conexión. Se devuelve la longitud de la cadena de conexión untruncated en **StringLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S00|Atributo de cadena de conexión no válido|Se especificó una palabra clave de atributo no válido en la cadena de conexión (*InConnectionString*), pero el controlador fue capaz de conectarse al origen de datos de todos modos. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02|Ha cambiado el valor de opción|El controlador no admitía el valor especificado que apunta el *ValuePtr* argumento en **SQLSetConnectAttr** y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S08|Error al guardar DSN de archivo|La cadena en  *\*InConnectionString* contiene un **FILEDSN** palabra clave, pero el archivo .dsn no se había guardado. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S09|Palabra clave no válida|(DM) la cadena en  *\*InConnectionString* contiene un **SAVEFILE** palabra clave pero no un **controlador** o un **FILEDSN** palabra clave. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08001|No se puede establecer la conexión de cliente|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de la conexión en uso|(DM) especificado *IdentificadorConexión* ya hubiese utilizado para establecer una conexión con un origen de datos, y la conexión todavía estaba abierta.|  
|08004|Servidor rechazó la conexión|El origen de datos rechazó el establecimiento de la conexión por motivos de definido por la implementación.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que estaba intentando conectar el controlador antes de la **SQLDriverConnect** procesamiento de la función se ha completado.|  
|28000|Especificación de autorización no válido|El identificador de usuario o la cadena de autorización o ambos, según se especifica en la cadena de conexión (*InConnectionString*), han infringido las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*szMessageText* búfer describe el error y su causa.|  
|HY000|Error general: dsn de archivo no válido|(DM) la cadena en **InConnectionString* contiene una palabra clave FILEDSN, pero no se encontró el nombre del archivo DSN.|  
|HY000|Error general: no se puede crear el búfer de archivos|(DM) la cadena en **InConnectionString* contiene una palabra clave FILEDSN, pero el archivo .dsn es ilegible.|  
|HY001|Error de asignación de memoria|El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la **SQLDriverConnect** función.<br /><br /> El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *IdentificadorConexión*. Se llamó a la función y antes que completó la ejecución, el [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en la *IdentificadorConexión*y, a continuación, el **SQLDriverConnect** se llamó a función en la *IdentificadorConexión*.<br /><br /> O bien, el **SQLDriverConnect** se llamó a función y antes que completó la ejecución, **SQLCancelHandle** se llamó en la *IdentificadorConexión* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) otra función ejecuta de forma asincrónica (no **SQLDriverConnect**) se llamó para el *IdentificadorConexión* y aún se estaba ejecutando cuando el **SQLDriverConnect** se llamó la función.|  
|HY013|Error de administración de memoria|El **SQLDriverConnect** no se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *StringLength1* era menor que 0 y no era igual a SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY092|Identificador de opción o atributo no válido|(DM) la *DriverCompletion* argumento era SQL_DRIVER_PROMPT y el *WindowHandle* argumento era un puntero nulo.|  
|HY110|Finalización del controlador no válido|(DM) el valor especificado para el argumento *DriverCompletion* no era igual a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.<br /><br /> (DM) se habilitó la agrupación de conexiones y el valor especificado para el argumento *DriverCompletion* no era igual a SQL_DRIVER_NOPROMPT.|  
|HYC00|Característica opcional no implementada|El controlador no es compatible con la versión de comportamiento ODBC que solicita la aplicación.|  
|HYT00|Se agotó el tiempo de espera|Ha caducado el período de tiempo de espera de inicio de sesión antes de la conexión al origen de datos completado. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente al nombre de origen de datos especificado no es compatible con la función.|  
|IM002|No se encontró el origen de datos y se especificó ningún controlador predeterminado|Nombre especificado en la cadena de conexión del origen de datos (DM) (*InConnectionString*) era no se encuentra en la información del sistema y no había ninguna especificación de controlador de forma predeterminada.<br /><br /> (DM) no se encontró información del controlador de origen y el valor predeterminado de datos ODBC en la información del sistema.|  
|IM003|No se pudo cargar el controlador especificado|(DM) el controlador aparecen en la especificación de origen de datos en la información del sistema o especificado por el **controlador** palabra clave no se encontró o no se puede cargar por alguna otra razón.|  
|IM004|Del controlador **SQLAllocHandle** en SQL_HANDLE_ENV error|(DM) durante la **SQLDriverConnect**, el Administrador de controladores denominado el controlador **SQLAllocHandle** funcionando con una *fHandleType* de SQL_HANDLE_ENV y el controlador devuelve un error.|  
|IM005|Del controlador **SQLAllocHandle** en SQL_HANDLE_DBC error.|(DM) durante la **SQLDriverConnect**, el Administrador de controladores denominado el controlador **SQLAllocHandle** funcionando con una *fHandleType* de SQL_HANDLE_DBC y el controlador devuelve un error.|  
|IM006|Del controlador **SQLSetConnectAttr** error|(DM) durante la **SQLDriverConnect**, el Administrador de controladores denominado el controlador **SQLSetConnectAttr** función y el controlador ha devuelto un error.|  
|IM007|Ningún origen de datos o el controlador especificado; prohibida el diálogo.|Se especificó ningún nombre de origen de datos o el controlador en la cadena de conexión y *DriverCompletion* era SQL_DRIVER_NOPROMPT.|  
|IM008|Error de diálogo.|El controlador ha intentado mostrar el cuadro de diálogo de inicio de sesión y no se pudo.<br /><br /> *WindowHandle* era un puntero nulo, y *DriverCompletion* no era SQL_DRIVER_NO_PROMPT.|  
|IM009|No se puede cargar el archivo DLL de traducción|El controlador no pudo cargar el archivo DLL que se especificó para el origen de datos o para la conexión de traducción.|  
|IM010|Nombre del origen de datos es demasiado largo|(DM) el valor de atributo para la palabra clave DSN era más de SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nombre de controlador demasiado largo|Valor de atributo (DM) para la **controlador** palabra clave tenía más de 255 caracteres.|  
|IM012|Error de sintaxis de palabra clave DRIVER|Pares de palabra clave y valor (DM) para la **controlador** palabra clave contiene un error de sintaxis.<br /><br /> (DM) la cadena en  *\*InConnectionString* contiene un **FILEDSN** palabra clave, pero el archivo .dsn no contenía un **controlador** palabra clave o un  **DSN** palabra clave.|  
|IM014|El DSN especificado contiene un error de coincidencia de arquitectura entre el controlador y la aplicación|Aplicación de 32 bits (DM) usa un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM015|Error SQLDriverConnect del controlador en SQL_HANDLE_DBC_INFO_HANDLE|Si un controlador devuelve SQL_ERROR, el Administrador de controladores devolverá SQL_ERROR a la aplicación y se producirá un error en la conexión.<br /><br /> Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
|S1118|Controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentarios  
 Una cadena de conexión tiene la siguiente sintaxis:  
  
 *cadena de conexión* :: = *cadena vacía*[;] &#124; *atributo*[;] &#124; *atributo*; *cadena de conexión*  
  
 *cadena vacía* :: =*atributo* :: = *palabra clave de atributo*=*atributo-valor* &#124; controlador = [{}] *valor del atributo*[}]  
  
 *palabra clave de atributo* :: = DSN &#124; UID &#124; PWD &#124; *-definido-atributo-palabra clave driver*  
  
 *valor del atributo* :: = *cadena de caracteres*  
  
 *driver-defined-attribute-keyword* ::= *identifier*  
  
 donde *cadena de caracteres* tiene cero o más caracteres; *identificador* tiene uno o más caracteres; *palabra clave de atributo* no distingue mayúsculas de minúsculas; *atributo-valor* puede distinguir mayúsculas de minúsculas; y el valor de la **DSN** palabra clave no contener solamente espacios en blanco.  
  
 ¿Debido a la cadena e inicialización archivo gramática, palabras clave y atributo de valores de conexión que contienen los caracteres **[]{}(),? \*=! @** no se incluye con llaves deberían evitarse. El valor de la **DSN** palabra clave no puede constar únicamente de espacios en blanco y no debe contener espacios en blanco iniciales. Debido a la gramática de la información del sistema, los nombres de origen de datos y palabras clave no pueden contener la barra diagonal inversa (\\) caracteres.  
  
 Las aplicaciones no tienen que agregar llaves alrededor del valor de atributo después de la **controlador** palabra clave a menos que el atributo contiene un punto y coma (;), en cuyo caso las llaves son obligatorias. Si el valor del atributo que recibe el controlador incluye llaves, el controlador no debe quitarlos, pero deben ser parte de la cadena de conexión devuelta.  
  
 ¿Un valor de cadena de conexión o DSN entre llaves ({}) que contiene los caracteres **[]{}(),? \*=! @** se pasa intacto al controlador. Sin embargo, al utilizar estos caracteres en una palabra clave, el Administrador de controladores devuelve un error cuando se trabaja con DSN de archivo, pero pasa la cadena de conexión para el controlador para las cadenas de conexión normal. Evite el uso de llaves incrustadas en un valor de palabra clave.  
  
 La cadena de conexión puede incluir cualquier número de palabras clave definidas por el controlador. Dado que la **controlador** palabra clave no utiliza información de la información del sistema, el controlador debe definir suficientes palabras clave para que un controlador puede conectarse a un origen de datos utilizando únicamente la información de la cadena de conexión. (Para obtener más información, vea "Instrucciones de controlador", más adelante en esta sección). El controlador define qué palabras clave se necesitan para conectarse al origen de datos.  
  
 La tabla siguiente describen los valores de atributo de la **DSN**, **FILEDSN**, **controlador**, **UID**, **PWD**, y **SAVEFILE** palabras clave.  
  
|Palabra clave|Descripción del valor de atributo|  
|-------------|---------------------------------|  
|**DSN**|Nombre de un origen de datos devuelto por **SQLDataSources** o en el cuadro de diálogo de orígenes de datos de **SQLDriverConnect**.|  
|**FILEDSN**|Nombre de un archivo .dsn desde el que se generarán una cadena de conexión del origen de datos. Estos orígenes de datos se denominan orígenes de datos de archivo.|  
|**CONTROLADOR**|Descripción del controlador devuelto por la **SQLDrivers** (función). Por ejemplo, Rdb o SQL Server.|  
|**UID**|Un identificador de usuario.|  
|**PWD**|La contraseña correspondiente para el identificador de usuario o una cadena vacía si no hay ninguna contraseña para el identificador de usuario (PWD =;).|  
|**SAVEFILE**|El nombre de archivo de un archivo de DSN en el que se deben guardar los valores de atributo de palabras clave usados para realizar la conexión está presente, correcta.|  
  
 Para obtener información acerca de cómo una aplicación elige un origen de datos o el controlador, consulte [elegir un origen de datos o el controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si todas las palabras clave se repite en la cadena de conexión, el controlador utiliza el valor asociado a la primera aparición de la palabra clave. Si el **DSN** y **controlador** palabras clave se incluye en la misma cadena de conexión, el Administrador de controladores y el controlador usan la palabra clave aparece en primer lugar.  
  
 El **FILEDSN** y **DSN** palabras clave es mutuamente excluyente: se usa la palabra clave aparece en primer lugar y el que aparece en segundo lugar se pasa por alto. El **FILEDSN** y **controlador** palabras clave, por otro lado, no es mutuamente excluyentes. Si cualquier palabra clave aparece en una cadena de conexión con **FILEDSN**, a continuación, se utiliza el valor del atributo de la palabra clave en la cadena de conexión en lugar del valor de atributo de la misma palabra clave en el archivo de DSN.  
  
 Si el **FILEDSN** se utiliza la palabra clave, las palabras clave especificadas en un archivo .dsn se utilizan para crear una cadena de conexión. (Para obtener más información, consulte "Archivo de orígenes de datos," más adelante en esta sección). El **UID** palabra clave es opcional; puede crearse un archivo .dsn con solo el **controlador** palabra clave. El **PWD** palabra clave no se almacena en un archivo de DSN. El directorio predeterminado para guardar y cargar un archivo .dsn será una combinación de la ruta de acceso especificada por **CommonFileDir** en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion y "ODBC\DataSources". (Si CommonFileDir fuera "Archivos de programa\Archivos C:\Program", el directorio predeterminado sería "C:\Program de programa\Common Files\ODBC\Data Sources").  
  
> [!NOTE]  
>  Un archivo .dsn se puede manipular directamente mediante una llamada a la [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) y [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) funciones en el archivo DLL del instalador.  
  
 Si el **SAVEFILE** se utiliza la palabra clave, los valores de atributo de palabras clave usados para realizar la conexión está presente, correcta se guardará como un archivo .dsn con el nombre del valor del atributo de la **SAVEFILE** palabra clave. El **SAVEFILE** palabra clave debe utilizarse junto con la **controlador** palabra clave, el **FILEDSN** palabra clave, o ambos, o la función devuelve SQL_SUCCESS_WITH_INFO con SQLSTATE 01S09 (palabra clave no válida). El **SAVEFILE** palabra clave debe aparecer antes de la **controlador** palabra clave en la cadena de conexión o los resultados se quedará sin definir.  
  
## <a name="driver-manager-guidelines"></a>Instrucciones de administrador de controladores  
 El Administrador de controladores construye una cadena de conexión para pasar al controlador en el *InConnectionString* argumento del controlador **SQLDriverConnect** función. El Administrador de controladores no modifica la *InConnectionString* argumento pasado a él por la aplicación.  
  
 La acción del Administrador de controladores se basa en el valor de la *DriverCompletion* argumento:  
  
-   SQL_DRIVER_PROMPT: Si la cadena de conexión no contener el **controlador**, **DSN**, o **FILEDSN** palabra clave, el Administrador de controladores muestra el cuadro de diálogo de orígenes de datos. Construye una cadena de conexión desde el nombre de origen de datos devuelto por el cuadro de diálogo y cualquier otra palabra clave que le pasa la aplicación. Si el nombre de origen de datos devuelto por el cuadro de diálogo está vacío, el Administrador de controladores especifica el par de valor de la palabra clave DSN = valor predeterminado. (Este cuadro de diálogo no mostrará un origen de datos con el nombre "Default".)  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: si la cadena de conexión especificada por la aplicación incluye el **DSN** palabra clave, el Administrador de controladores copia la cadena de conexión especificada por la aplicación. En caso contrario, tiene las mismas acciones que lo hace cuando *DriverCompletion* es SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: El Administrador de controladores copia la cadena de conexión especificada por la aplicación.  
  
 Si la cadena de conexión especificada por la aplicación contiene el **controlador** palabra clave, el Administrador de controladores copia la cadena de conexión especificada por la aplicación.  
  
 Con la cadena de conexión que se crea, el Administrador de controladores determina qué controlador debe usar, se conecta a ese controlador y devuelve la cadena de conexión que se crea el controlador; Para obtener más información acerca de la interacción de los controladores y el Administrador de controladores, consulte la sección "Comentarios" en [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md). Si la cadena de conexión no contiene el **controlador** palabra clave, el Administrador de controladores determina qué controlador que se utilizará como se indica a continuación:  
  
1.  Si la cadena de conexión contiene el **DSN** palabra clave, el Administrador de controladores recupera el controlador asociado con el origen de datos de la información del sistema.  
  
2.  Si la cadena de conexión no contiene el **DSN** no se encuentra la palabra clave o el origen de datos, el Administrador de controladores recupera el controlador asociado con el origen de datos predeterminado de la información del sistema. (Para obtener más información, consulte [subclave predeterminado](../../../odbc/reference/install/default-subkey.md).) El Administrador de controladores se cambia el valor de la **DSN** palabra clave en la cadena de conexión en "Predeterminado".  
  
3.  Si el **DSN** palabra clave en la cadena de conexión se establece en "Predeterminado", el Administrador de controladores recupera el controlador asociado con el origen de datos predeterminado de la información del sistema.  
  
4.  Si no se encuentra el origen de datos y no se encuentra el origen de datos de forma predeterminada, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE IM002 (no se encontró el origen de datos y se especificó ningún controlador predeterminado).  
  
## <a name="file-data-sources"></a>Orígenes de datos de archivo  
 Si la cadena de conexión especificada por la aplicación en la llamada a **SQLDriverConnect** contiene el **FILEDSN** palabra clave y esta palabra clave no se ha sustituido, ya sea el **DSN**o **controlador** palabra clave y, a continuación, el Administrador de controladores crea una cadena de conexión según se indica en el archivo .dsn y *InConnectionString* argumento. El Administrador de controladores procede como sigue:  
  
1.  Comprueba si el nombre de archivo del archivo .dsn es válido. Si no es así, devuelve SQL_ERROR con SQLSTATE IM014 (nombre de DSN de archivo no válido). Si el nombre de archivo es una cadena vacía ("") y SQL_DRIVER_NOPROMPT no se especifica, el **archivo / abrir** se muestra el cuadro de diálogo. Si el nombre de archivo contiene una ruta de acceso válida, pero ningún nombre de archivo o un nombre de archivo no válido y no se especifica SQL_DRIVER_NOPROMPT, la **archivo / abrir** cuadro de diálogo se muestra con el directorio actual establecido en el especificado en el nombre de archivo. Si el nombre de archivo es una cadena vacía ("") o el nombre de archivo contiene una ruta de acceso válida, pero ningún nombre de archivo o un nombre de archivo no válido y se especifica SQL_DRIVER_NOPROMPT, a continuación, se devuelve SQL_ERROR con SQLSTATE IM014 (nombre de DSN de archivo no válido).  
  
2.  Lee todas las palabras clave en la sección [ODBC] del archivo DSN. Si el **controlador** palabra clave no está presente, devuelve SQL_ERROR con SQLSTATE IM012 (error de sintaxis de palabra clave Driver), excepto que el archivo .dsn es no se puede compartir y, por tanto, solo contiene el **DSN** palabra clave.  
  
     Si el origen de datos de archivo es no se puede compartir, el Administrador de controladores lee el valor de la **DSN** palabra clave y se conecta según sea necesario para el origen de datos de usuario o sistema que señala el origen de datos de archivo no se puede compartir. No se realizan los pasos del 3 al 5.  
  
3.  Construye una cadena de conexión para el controlador. La cadena de conexión del controlador es la unión de las palabras clave especificadas en el archivo .dsn y aquellas especificadas en la cadena de conexión de aplicación original. Reglas para la construcción de la cadena de conexión de controlador que se superpone a palabras clave son los siguientes:  
  
    -   Si el **controlador** palabra clave existe en la cadena de conexión de la aplicación y los controladores especificados por el **controlador** palabras clave no es los mismos en el archivo .dsn y la cadena de conexión de la aplicación, el se omite la información del controlador en el archivo .dsn y se utiliza la información del controlador en la cadena de conexión de la aplicación. Si los controladores especificados por el **controlador** palabra clave son los mismos en el archivo .dsn y cadena de conexión de la aplicación, a continuación, donde se superponen todas las palabras clave, los especificados en la cadena de conexión de la aplicación tienen prioridad frente a las Si se especifica en el archivo de DSN.  
  
    -   En la nueva cadena de conexión, el **FILEDSN** palabra clave se ha eliminado.  
  
4.  Carga el controlador mediante una búsqueda en la entrada del registro HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\\< nombreDeControlador\>\Driver donde \<nombreDeControlador > se especifica mediante la **controlador** palabra clave.  
  
5.  Pasa al controlador de la nueva cadena de conexión.  
  
 Para obtener ejemplos de archivos .dsn, consulte [conectar orígenes de datos de archivo utilizando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>Palabra clave SAVEFILE  
 Si la cadena de conexión especificada por la aplicación contiene el **SAVEFILE** palabra clave y, a continuación, el Administrador de controladores guarda la cadena de conexión en un archivo de DSN. El Administrador de controladores procede como sigue:  
  
1.  Comprueba si el nombre de archivo del archivo .dsn incluido como el valor del atributo de la **SAVEFILE** palabra clave es válida. Si no es así, devuelve SQL_ERROR con SQLSTATE IM014 (nombre de DSN de archivo no válido). La validez del nombre de archivo está determinada por las reglas de nomenclatura estándar del sistema. Si el nombre de archivo es una cadena vacía ("") y la *DriverCompletion* el argumento no es SQL_DRIVER_NOPROMPT, a continuación, el nombre de archivo es válido. Si el nombre de archivo ya existe, a continuación, si *DriverCompletion* es SQL_DRIVER_NOPROMPT, se sobrescribe el archivo. Si *DriverCompletion* es SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, un cuadro de diálogo pide al usuario que especifique si se debe sobrescribir el archivo. Si No se especifica, el **Guardar archivo** aparece el cuadro de diálogo.  
  
2.  Si el controlador devuelve SQL_SUCCESS y el nombre de archivo no era una cadena vacía, el Administrador de controladores se escribe la información de conexión devuelta en el *OutConnectionString* argumento en el archivo especificado con el formato especificado en la sección "Cadenas de conexión" anteriormente en esta sección.  
  
3.  Si el controlador devuelve SQL_SUCCESS y el nombre de archivo no era una cadena vacía (""), a continuación, el Administrador de controladores llama el **Guardar archivo** cuadro de diálogo común con el *hwnd* especificado y escribe la información de conexión devuelto en *OutConnectionString* en el archivo especificado en el cuadro de diálogo común de archivo guardado con el formato especificado en la sección "Cadenas de conexión" anteriormente en esta sección.  
  
4.  Si el controlador devuelve SQL_SUCCESS, devuelve el *OutConnectionString* argumento que contiene la cadena de conexión a la aplicación.  
  
5.  Si el controlador devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR, el Administrador de controladores devuelve el valor de SQLSTATE a la aplicación.  
  
## <a name="driver-guidelines"></a>Directrices de controlador  
 El controlador comprueba si la cadena de conexión que se pasa por el Administrador de controladores contiene la **DSN** o **controlador** palabra clave. Si la cadena de conexión contiene el **controlador** palabra clave, el controlador no puede recuperar información sobre el origen de datos de la información del sistema. Si la cadena de conexión contiene el **DSN** palabra clave o no contiene el **DSN** o la **controlador** palabra clave, el controlador puede recuperar información sobre el origen de datos de la información del sistema como se indica a continuación:  
  
1.  Si la cadena de conexión contiene el **DSN** palabra clave, el controlador recupera la información del origen de datos especificado.  
  
2.  Si la cadena de conexión no contiene el **DSN** palabra clave, no se encuentra el origen de datos especificado, o la **DSN** palabra clave está establecida en "Predeterminado", el controlador recupera la información de origen de datos predeterminado .  
  
 El controlador utiliza toda la información que recupera de la información del sistema para ampliar la información que se pasa en la cadena de conexión. Si la información de la información del sistema duplica la información en la cadena de conexión, el controlador utiliza la información de la cadena de conexión.  
  
 En función del valor de *DriverCompletion*, el controlador que pide al usuario información de conexión, como el Id. de usuario y la contraseña y se conecta al origen de datos:  
  
-   SQL_DRIVER_PROMPT: El controlador muestra un cuadro de diálogo con los valores de la información de sistema y de cadena de conexión (si existe) como valores iniciales. Cuando el usuario cierra el cuadro de diálogo, el controlador se conecta al origen de datos. También construye una cadena de conexión desde el valor de la **DSN** o **controlador** palabra clave en \* *InConnectionString* y la información devuelta desde el cuadro de diálogo. Coloca esta cadena de conexión en el **OutConnectionString* búfer.  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: si la cadena de conexión contiene información suficiente y que la información es correcta, el controlador se conecta al origen de datos y copias \* *InConnectionString*a \* *OutConnectionString*. Si toda la información que falta o es incorrecto, el controlador tiene las mismas acciones que lo hace cuando *DriverCompletion* es SQL_DRIVER_PROMPT, excepto que si *DriverCompletion* es SQL_DRIVER_COMPLETE_ OBLIGATORIO, el controlador deshabilita los controles de información no necesaria para conectarse al origen de datos.  
  
-   SQL_DRIVER_NOPROMPT: Si la cadena de conexión contiene información suficiente, el controlador se conecta al origen de datos y copias \* *InConnectionString* a \* *OutConnectionString*. En caso contrario, el controlador devuelve SQL_ERROR para **SQLDriverConnect**.  
  
 En una conexión correcta al origen de datos, el controlador también establece \* *StringLength2Ptr* a la longitud de la cadena de conexión de salida que está disponible para devolver en **OutConnectionString*.  
  
 Si el usuario cancela un cuadro de diálogo presentado por el Administrador de controladores o el controlador, **SQLDriverConnect** devuelve SQL_NO_DATA.  
  
 Para obtener información acerca de cómo interactúan el Administrador de controladores y el controlador durante el proceso de conexión, vea [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Si un controlador es compatible con **SQLDriverConnect**, la sección de la palabra clave de controlador de la información del sistema para el controlador debe contener el **ConnectFunctions** palabra clave con el segundo carácter establecido en "Y".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Conectarse cuando se habilita la agrupación de conexiones  
 Agrupación de conexiones permite a reutilizar una conexión que ya se ha creado una aplicación. Cuando **SQLDriverConnect** se llama, el Administrador de controladores intenta realizar la conexión utilizando una conexión que forma parte de un grupo de conexiones en un entorno que se han designado para la agrupación de conexiones. Para obtener más información sobre la agrupación de conexiones, vea [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Una aplicación puede establecer SQL_ATTR_RESET_CONNECTION antes de llamar a SQLDisconnect en una conexión donde está habilitada la agrupación. Para obtener más información, consulte [función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Las restricciones siguientes se aplican cuando una aplicación llama **SQLDriverConnect** para conectarse a una conexión agrupada:  
  
-   No se realizan ningún procesamiento de agrupación de conexiones cuando la **SAVEFILE** se especifica la palabra clave en la cadena de conexión.  
  
-   Si se habilita la agrupación de conexiones, **SQLDriverConnect** se puede llamar solo con un *DriverCompletion* argumento de SQL_DRIVER_NOPROMPT; si **SQLDriverConnect** se llama con cualquier otro *DriverCompletion*, HY110 SQLSTATE se devolverán (finalización del controlador no válido).  
  
## <a name="connection-attributes"></a>Atributos de conexión  
 El atributo de conexión SQL_ATTR_LOGIN_TIMEOUT, que se establecen a través de **SQLSetConnectAttr**, define el número de segundos de espera para que una solicitud de inicio de sesión completar con una conexión correcta con el controlador antes de volver a la aplicación. Si se solicita al usuario que complete la cadena de conexión, un período de espera para cada solicitud de inicio de sesión comienza cuando el controlador inicia el proceso de conexión.  
  
 El controlador, abre la conexión en modo de acceso SQL_MODE_READ_WRITE de forma predeterminada. Para establecer el modo de acceso en SQL_MODE_READ_ONLY, la aplicación debe llamar a **SQLSetConnectAttr** con el atributo SQL_ATTR_ACCESS_MODE antes de llamar a **SQLDriverConnect**.  
  
 Si una biblioteca de traducción predeterminado se especifica en la información del sistema para el origen de datos, el controlador lo carga. Se puede cargar una biblioteca de traducción diferente mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_LIB. Una opción de traducción puede especificarse mediante una llamada a **SQLSetConnectAttr** con la opción SQL_ATTR_TRANSLATE_OPTION.  
  
 Para obtener más información, consulte [conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
```  
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
|Desconectarse de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Devuelve la descripción de los controladores y atributos|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberar un identificador|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
