---
title: Función SQLDriverConnect (SQLDriverConnect) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88ec70d68b46beca97fd6b0d758e21aab5d4f4b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302776"
---
# <a name="sqldriverconnect-function"></a>Función SQLDriverConnect
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLDriverConnect** es una alternativa a **SQLConnect**. Admite orígenes de datos que requieren más información de conexión que los tres argumentos de **SQLConnect**, cuadros de diálogo para solicitar al usuario toda la información de conexión y orígenes de datos que no están definidos en la información del sistema.  
  
 **SQLDriverConnect** proporciona los siguientes atributos de conexión:  
  
-   Establezca una conexión mediante una cadena de conexión que contenga el nombre del origen de datos, uno o varios ID de usuario, una o varias contraseñas y otra información requerida por el origen de datos.  
  
-   Establecer una conexión mediante una cadena de conexión parcial o ninguna información adicional; en este caso, el Administrador de controladores y el controlador pueden solicitar al usuario información de conexión.  
  
-   Establezca una conexión a un origen de datos que no esté definido en la información del sistema. Si la aplicación proporciona una cadena de conexión parcial, el controlador puede solicitar al usuario información de conexión.  
  
-   Establezca una conexión a un origen de datos mediante una cadena de conexión construida a partir de la información de un archivo .dsn.  
  
 Después de establecer una conexión, **SQLDriverConnect** devuelve la cadena de conexión completada. La aplicación puede usar esta cadena para las solicitudes de conexión posteriores. Para obtener más información, consulte [Conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
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
 [Entrada] Mango de la ventana. La aplicación puede pasar el identificador de la ventana primaria, si procede, o un puntero nulo si el identificador de ventana no es aplicable o **SQLDriverConnect** no presentará ningún cuadro de diálogo.  
  
 *InConnectionString*  
 [Entrada] Una cadena de conexión completa (consulte la sintaxis en "Comentarios"), una cadena de conexión parcial o una cadena vacía.  
  
 *StringLength1*  
 [Entrada] Longitud de **InConnectionString*, en caracteres si la cadena es Unicode, o bytes si la cadena es ANSI o DBCS.  
  
 *OutConnectionString*  
 [Salida] Puntero a un búfer para la cadena de conexión completada. Tras la conexión correcta con el origen de datos de destino, este búfer contiene la cadena de conexión completada. Las aplicaciones deben asignar al menos 1.024 caracteres para este búfer.  
  
 Si *OutConnectionString* es NULL, *StringLength2Ptr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Longitud del búfer **OutConnectionString,* en caracteres.  
  
 *StringLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número \*total de caracteres (excluyendo el carácter de terminación nula) disponibles para devolver en *OutConnectionString*. Si el número de caracteres disponibles para devolver es mayor \*o igual que *BufferLength*, la cadena de conexión completada en *OutConnectionString* se trunca en *BufferLength* menos la longitud de un carácter de terminación nula.  
  
 *DriverCompletion*  
 [Entrada] Marca que indica si el Administrador de controladores o el controlador deben solicitar más información de conexión:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.  
  
 (Para obtener información adicional, consulte "Comentarios.")  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDriverConnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *fHandleType* de SQL_HANDLE_DBC y un *hHandle* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLDriverConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *OutConnectionString* no era lo suficientemente grande como para devolver toda la cadena de conexión, por lo que la cadena de conexión se truncó. La longitud de la cadena de conexión no truncada se devuelve en **StringLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S00|Atributo de cadena de conexión no válido|Se especificó una palabra clave de atributo no válida en la cadena de conexión (*InConnectionString*), pero el controlador pudo conectarse al origen de datos de todos modos. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|El controlador no admitía el valor especificado al que apunta el *valuePtr* argumento en **SQLSetConnectAttr** y sustituyó un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S08|Error al guardar el archivo DSN|La cadena * \*de InConnectionString* contenía una palabra clave **FILEDSN,** pero el archivo .dsn no se guardó. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S09|Palabra clave no válida|(DM) La cadena * \*de InConnectionString* contenía una palabra clave **SAVEFILE,** pero no una palabra clave **DRIVER** o **FILEDSN.** (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de establecer conexión|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de conexión en uso|(DM) el *ConnectionHandle* especificado ya se había utilizado para establecer una conexión con un origen de datos y la conexión seguía abierta.|  
|08004|El servidor rechazó la conexión|El origen de datos rechazó el establecimiento de la conexión por razones definidas por la implementación.|  
|08S01|Fallo del enlace de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que el controlador intentaba conectarse ha fallado antes de que la función **SQLDriverConnect** completara el procesamiento.|  
|28000|Especificación de autorización no válida|El identificador de usuario o la cadena de autorización, o ambos, como se especifica en la cadena de conexión (*InConnectionString*), infringió las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*búfer szMessageText* describe el error y su causa.|  
|HY000|Error general: archivo no válido dsn|(DM) La cadena de **InConnectionString* contenía una palabra clave FILEDSN, pero no se encontró el nombre del archivo .dsn.|  
|HY000|Error general: No se puede crear el búfer de archivos|(DM) La cadena de **InConnectionString* contenía una palabra clave FILEDSN, pero el archivo .dsn era ilegible.|  
|HY001|Error de asignación de memoria|El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función **SQLDriverConnect.**<br /><br /> El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *ConnectionHandle*. Se llamó a la función y, antes de completar la ejecución, se llamó a la [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) en *ConnectionHandle*y, a continuación, se llamó de nuevo a la función **SQLDriverConnect** en *ConnectionHandle*.<br /><br /> O bien, se llamó a la función **SQLDriverConnect** y, antes de completar la ejecución, **sqlCancelHandle** se llamó en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) Se llamó a otra función de ejecución asincrónica (no **SQLDriverConnect**) para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a la función **SQLDriverConnect.**|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada a la función **SQLDriverConnect** porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *StringLength1* era menor que 0 y no era igual a SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY092|Identificador de atributo/opción no válido|(DM) el *DriverCompletion* argumento se SQL_DRIVER_PROMPT y el *WindowHandle* argumento era un puntero nulo.|  
|HY110|Finalización del controlador no válido|(DM) el valor especificado para el argumento *DriverCompletion* no era igual a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.<br /><br /> (DM) Se habilitó la agrupación de conexiones y el valor especificado para el argumento *DriverCompletion* no era igual a SQL_DRIVER_NOPROMPT.|  
|HYC00|Característica opcional no implementada|El controlador no admite la versión del comportamiento ODBC que solicitó la aplicación.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de inicio de sesión expiró antes de que se completara la conexión con el origen de datos. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador correspondiente al nombre de origen de datos especificado no admite la función.|  
|IM002|Origen de datos no encontrado y no se especificó ningún controlador predeterminado|(DM) El nombre del origen de datos especificado en la cadena de conexión (*InConnectionString*) no se encontró en la información del sistema y no había ninguna especificación de controlador predeterminada.<br /><br /> (DM) El origen de datos ODBC y la información predeterminada del controlador no se pudo encontrar en la información del sistema.|  
|IM003|No se pudo cargar el controlador especificado|(DM) El controlador que aparece en la especificación del origen de datos en la información del sistema o especificado por la palabra clave **DRIVER** no se encontró o no se pudo cargar por algún otro motivo.|  
|IM004|**SqlAllocHandle** del controlador en SQL_HANDLE_ENV error|(DM) Durante **SQLDriverConnect**, el Administrador de controladores llamó a la función **SQLAllocHandle** del controlador con un *fHandleType* de SQL_HANDLE_ENV y el controlador devolvió un error.|  
|IM005|**SQLAllocHandle** del controlador en SQL_HANDLE_DBC error.|(DM) Durante **SQLDriverConnect**, el Administrador de controladores llamó a la función **SQLAllocHandle** del controlador con un *fHandleType* de SQL_HANDLE_DBC y el controlador devolvió un error.|  
|IM006|Error del controlador **SQLSetConnectAttr**|(DM) Durante **SQLDriverConnect**, el Administrador de controladores llamó a la función **SQLSetConnectAttr** del controlador y el controlador devolvió un error.|  
|IM007|No se especificó ningún origen de datos o controlador; diálogo prohibido|No se especificó ningún nombre de origen de datos o controlador en la cadena de conexión y *DriverCompletion* se SQL_DRIVER_NOPROMPT.|  
|IM008|Error en el diálogo|El controlador intentó mostrar su cuadro de diálogo de inicio de sesión y falló.<br /><br /> *WindowHandle* era un puntero nulo y *DriverCompletion* no era SQL_DRIVER_NO_PROMPT.|  
|IM009|No se puede cargar DLL de traducción|El controlador no pudo cargar el archivo DLL de traducción que se especificó para el origen de datos o para la conexión.|  
|IM010|Nombre del origen de datos demasiado largo|(DM) el valor de atributo de la palabra clave DSN era más largo que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nombre del conductor demasiado largo|(DM) el valor del atributo de la palabra clave **DRIVER** tenía más de 255 caracteres.|  
|IM012|Error de sintaxis de palabra clave DRIVER|(DM) El par palabra clave-valor de la palabra clave **DRIVER** contenía un error de sintaxis.<br /><br /> (DM) La cadena * \*de InConnectionString* contenía una palabra clave **FILEDSN,** pero el archivo .dsn no contenía una palabra clave **DRIVER** ni una palabra clave **DSN.**|  
|IM014|El DSN especificado contiene una discordancia de arquitectura entre el controlador y la aplicación|(DM) aplicación de 32 bits utiliza un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM015|Error en SQLDriverConnect del controlador en SQL_HANDLE_DBC_INFO_HANDLE|Si un controlador devuelve SQL_ERROR, el Administrador de controladores devolverá SQL_ERROR a la aplicación y se producirá un error en la conexión.<br /><br /> Para obtener más información acerca de SQL_HANDLE_DBC_INFO_TOKEN, vea Desarrollar el reconocimiento de grupos [de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
|S1118|El controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT ni SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentarios  
 Una cadena de conexión tiene la sintaxis siguiente:  
  
 *connection-string* ::- *empty-string*[;] &#124; *atributo*[;] &#124; *attribute*; *conexión-cadena*  
  
 *empty-string* ::-*atributo* ::- *atributo-palabra clave*=*atributo-valor* &#124; DRIVER-[-]*atributo-valor*[-]  
  
 *attribute-keyword* ::- DSN &#124; UID &#124; PWD &#124; *driver-defined-attribute-keyword*  
  
 *valor-atributo* ::- *carácter-cadena*  
  
 *identificador definido por el conductor-atributo::-* *identifier*  
  
 donde *la cadena de caracteres* tiene cero o más caracteres; *identificador* tiene uno o más caracteres; *attribute-keyword* no distingue mayúsculas de minúsculas; *atributo-valor* puede distinguir entre mayúsculas y minúsculas; y el valor de la palabra clave **DSN** no consiste únicamente en espacios en blanco.  
  
 Debido a la cadena de conexión y la gramática del archivo de inicialización, palabras clave y valores de atributo que contienen los caracteres **[]{}(),;? Se \*** debe evitar que no se incluyan llaves con llaves. El valor de la palabra clave **DSN** no puede constar únicamente de espacios en blanco y no debe contener espacios en blanco iniciales. Debido a la gramática de la información del sistema, las\\palabras clave y los nombres de origen de datos no pueden contener el carácter de barra diagonal inversa ( ).  
  
 Las aplicaciones no tienen que agregar llaves alrededor del valor del atributo después de la palabra clave **DRIVER** a menos que el atributo contenga un punto y coma (;), en cuyo caso se requieren las llaves. Si el valor de atributo que recibe el controlador incluye llaves, el controlador no debe quitarlas, pero deben formar parte de la cadena de conexión devuelta.  
  
 Un Valor de cadena dSN o{}de conexión entre llaves ( ) que contiene cualquiera de los caracteres **[]{}(),;? El \*controlador** se pasa intacto. Sin embargo, cuando se usan estos caracteres en una palabra clave, el Administrador de controladores devuelve un error al trabajar con DSN de archivo, pero pasa la cadena de conexión al controlador para cadenas de conexión normales. Evite el uso de llaves incrustadas en un valor de palabra clave.  
  
 La cadena de conexión puede incluir cualquier número de palabras clave definidas por el controlador. Dado que la palabra clave **DRIVER** no utiliza información de la información del sistema, el controlador debe definir suficientes palabras clave para que un controlador pueda conectarse a un origen de datos utilizando solo la información de la cadena de conexión. (Para obtener más información, consulte "Directrices del conductor", más adelante en esta sección.) El controlador define qué palabras clave son necesarias para conectarse al origen de datos.  
  
 En la tabla siguiente se describen los valores de atributo de las palabras clave **DSN**, **FILEDSN**, **DRIVER**, **UID**, **PWD**y **SAVEFILE** .  
  
|Palabra clave|Descripción del valor del atributo|  
|-------------|---------------------------------|  
|**Dsn**|Nombre de un origen de datos devuelto por **SQLDataSources** o el cuadro de diálogo de orígenes de datos de **SQLDriverConnect**.|  
|**FILEDSN**|Nombre de un archivo .dsn desde el que se creará una cadena de conexión para el origen de datos. Estos orígenes de datos se denominan orígenes de datos de archivo.|  
|**Conductor**|Descripción del controlador devuelto por la función **SQLDrivers.** Por ejemplo, Rdb o SQL Server.|  
|**Uid**|Un id. de usuario.|  
|**Pwd**|La contraseña correspondiente al ID de usuario, o una cadena vacía si no hay ninguna contraseña para el ID de usuario (PWD-;).|  
|**SAVEFILE**|El nombre de archivo de un archivo .dsn en el que se deben guardar los valores de atributo de las palabras clave utilizadas para realizar la conexión actual y correcta.|  
  
 Para obtener información sobre cómo una aplicación elige un origen de datos o un controlador, vea Elegir un origen de [datos o un controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si se repite alguna palabra clave en la cadena de conexión, el controlador utiliza el valor asociado con la primera aparición de la palabra clave. Si las palabras clave **DSN** y **DRIVER** se incluyen en la misma cadena de conexión, el Administrador de controladores y el controlador usan la palabra clave que aparezca primero.  
  
 Las palabras clave **FILEDSN** y **DSN** son mutuamente excluyentes: se utiliza la palabra clave que aparece primero y la que aparece en segundo lugar. Las palabras clave **FILEDSN** y **DRIVER,** por otro lado, no son mutuamente excluyentes. Si aparece alguna palabra clave en una cadena de conexión con **FILEDSN**, se utiliza el valor de atributo de la palabra clave en la cadena de conexión en lugar del valor de atributo de la misma palabra clave en el archivo .dsn.  
  
 Si se utiliza la palabra clave **FILEDSN,** las palabras clave especificadas en un archivo .dsn se utilizan para crear una cadena de conexión. (Para obtener más información, consulte "Origen de datos de archivo", más adelante en esta sección.) La palabra clave **UID** es opcional; un archivo .dsn se puede crear con sólo la palabra clave **DRIVER.** La palabra clave **PWD** no se almacena en un archivo .dsn. El directorio predeterminado para guardar y cargar un archivo .dsn será una combinación de la ruta de acceso especificada por **CommonFileDir** en HKEY_LOCAL_MACHINE. (Si CommonFileDir fuera "C:-Archivos de programa-Archivos comunes", el directorio predeterminado sería "C:-Archivos de programa-Archivos comunes-ODBC-Orígenes de datos".)  
  
> [!NOTE]  
>  Un archivo .dsn se puede manipular directamente llamando a las funciones [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) y [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) en el archivo DLL del instalador.  
  
 Si se utiliza la palabra clave **SAVEFILE,** los valores de atributo de las palabras clave utilizadas para realizar la conexión correcta actual se guardarán como un archivo .dsn con el nombre del valor de atributo de la palabra clave **SAVEFILE.** La palabra clave **SAVEFILE** debe utilizarse junto con la palabra clave **DRIVER,** la palabra clave **FILEDSN** o ambas, o la función devuelve SQL_SUCCESS_WITH_INFO con SQLSTATE 01S09 (palabra clave no válida). La palabra clave **SAVEFILE** debe aparecer antes de la palabra clave **DRIVER** en la cadena de conexión, o los resultados serán indefinidos.  
  
## <a name="driver-manager-guidelines"></a>Pautas del administrador del conductor  
 El Administrador de controladores construye una cadena de conexión para pasar al controlador en el *InConnectionString* argumento de la función **SQLDriverConnect** del controlador. El Administrador de controladores no modifica el *Argumento InConnectionString* que le pasa la aplicación.  
  
 La acción del Administrador de controladores se basa en el valor del argumento *DriverCompletion:*  
  
-   SQL_DRIVER_PROMPT: si la cadena de conexión no contiene la palabra clave **DRIVER**, **DSN**o **FILEDSN,** el Administrador de controladores muestra el cuadro de diálogo Orígenes de datos. Construye una cadena de conexión a partir del nombre del origen de datos devuelto por el cuadro de diálogo y cualquier otra palabra clave que le pase la aplicación. Si el nombre del origen de datos devuelto por el cuadro de diálogo está vacío, el Administrador de controladores especifica el par palabra clave-valor DSN-Predeterminado. (Este cuadro de diálogo no mostrará un origen de datos con el nombre "Predeterminado".)  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: si la cadena de conexión especificada por la aplicación incluye la palabra clave **DSN,** el Administrador de controladores copia la cadena de conexión especificada por la aplicación. De lo contrario, realiza las mismas acciones que cuando *DriverCompletion* se SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: el Administrador de controladores copia la cadena de conexión especificada por la aplicación.  
  
 Si la cadena de conexión especificada por la aplicación contiene la palabra clave **DRIVER,** el Administrador de controladores copia la cadena de conexión especificada por la aplicación.  
  
 Mediante la cadena de conexión que ha construido, el Administrador de controladores determina qué controlador usar, se conecta a ese controlador y pasa la cadena de conexión que ha construido al controlador; Para obtener más información acerca de la interacción del Administrador de controladores y el controlador, vea la sección "Comentarios" en [SQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md). Si la cadena de conexión no contiene la palabra clave **DRIVER,** el Administrador de controladores determina qué controlador utilizar de la siguiente manera:  
  
1.  Si la cadena de conexión contiene la palabra clave **DSN,** el Administrador de controladores recupera el controlador asociado al origen de datos de la información del sistema.  
  
2.  Si la cadena de conexión no contiene la palabra clave **DSN** o no se encuentra el origen de datos, el Administrador de controladores recupera el controlador asociado con el origen de datos predeterminado de la información del sistema. (Para obtener más información, consulte [Subclave predeterminada](../../../odbc/reference/install/default-subkey.md).) El Administrador de controladores cambia el valor de la palabra clave **DSN** de la cadena de conexión a "DEFAULT".  
  
3.  Si la palabra clave **DSN** de la cadena de conexión se establece en "DEFAULT", el Administrador de controladores recupera el controlador asociado con el origen de datos predeterminado de la información del sistema.  
  
4.  Si no se encuentra el origen de datos y no se encuentra el origen de datos predeterminado, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE IM002 (no se encontró el origen de datos y no se ha especificado ningún controlador predeterminado).  
  
## <a name="file-data-sources"></a>Orígenes de datos de archivo  
 Si la cadena de conexión especificada por la aplicación en la llamada a **SQLDriverConnect** contiene la palabra clave **FILEDSN** y esta palabra clave no se reemplaza por la palabra clave **DSN** o **DRIVER,** el Administrador de controladores crea una cadena de conexión con la información del archivo .dsn y el argumento *InConnectionString.* El Administrador de controladores procede de la siguiente manera:  
  
1.  Comprueba si el nombre de archivo del archivo .dsn es válido. Si no es así, devuelve SQL_ERROR con SQLSTATE IM014 (nombre no válido del archivo DSN). Si el nombre de archivo es una cadena vacía ("") y no se especifica SQL_DRIVER_NOPROMPT, se muestra el cuadro de diálogo **Abrir archivo.** Si el nombre de archivo contiene una ruta de acceso válida pero no hay un nombre de archivo o un nombre de archivo no válido y no se especifica SQL_DRIVER_NOPROMPT, el cuadro de diálogo **Abrir** archivo se muestra con el directorio actual establecido en el especificado en el nombre de archivo. Si el nombre de archivo es una cadena vacía ("") o el nombre de archivo contiene una ruta de acceso válida pero ningún nombre de archivo o un nombre de archivo no válido, y se especifica SQL_DRIVER_NOPROMPT, SQL_ERROR se devuelve con SQLSTATE IM014 (nombre no válido del archivo DSN).  
  
2.  Lee todas las palabras clave de la sección [ODBC] del archivo .dsn. Si la palabra clave **DRIVER** no está presente, devuelve SQL_ERROR con SQLSTATE IM012 (error de sintaxis de palabra clave Driver), excepto cuando el archivo .dsn no se puede compartir y, por lo tanto, contiene solo la palabra clave **DSN.**  
  
     Si el origen de datos del archivo no se puede compartir, el Administrador de controladores lee el valor de la palabra clave **DSN** y se conecta según sea necesario al usuario o al origen de datos del sistema al que apunta el origen de datos de archivo no compartible. Los pasos 3 a 5 no se realizan.  
  
3.  Construye una cadena de conexión para el controlador. La cadena de conexión del controlador es la unión de las palabras clave especificadas en el archivo .dsn y las especificadas en la cadena de conexión de la aplicación original. Las reglas para la construcción de la cadena de conexión del controlador donde las palabras clave se superponen son las siguientes:  
  
    -   Si la palabra clave **DRIVER** existe en la cadena de conexión de la aplicación y los controladores especificados por las palabras clave **DRIVER** no son los mismos en el archivo .dsn y la cadena de conexión de la aplicación, se omite la información del controlador en el archivo .dsn y se utiliza la información del controlador en la cadena de conexión de la aplicación. Si los controladores especificados por la palabra clave **DRIVER** son los mismos en el archivo .dsn y en la cadena de conexión de la aplicación, donde todas las palabras clave se superponen, las especificadas en la cadena de conexión de la aplicación tienen prioridad sobre las especificadas en el archivo .dsn.  
  
    -   En la nueva cadena de conexión, se elimina la palabra clave **FILEDSN.**  
  
4.  Carga el controlador buscando en la entrada del Registro HKEY_LOCAL_MACHINE, SOFTWARE, ODBC, ODBCINST. INI\\<\>nombre del \<controlador : Controlador, donde la palabra clave **DRIVER** especifica el nombre del controlador>.  
  
5.  Pasa al controlador la nueva cadena de conexiones.  
  
 Para ver ejemplos de archivos .dsn, consulte [Conexión mediante orígenes](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)de datos de archivo .  
  
## <a name="savefile-keyword"></a>Palabra clave SAVEFILE  
 Si la cadena de conexión especificada por la aplicación contiene la palabra clave **SAVEFILE,** el Administrador de controladores guarda la cadena de conexión en un archivo .dsn. El Administrador de controladores procede de la siguiente manera:  
  
1.  Comprueba si el nombre de archivo del archivo .dsn incluido como valor de atributo de la palabra clave **SAVEFILE** es válido. Si no es así, devuelve SQL_ERROR con SQLSTATE IM014 (nombre no válido del archivo DSN). La validez del nombre de archivo viene determinada por las reglas de nomenclatura estándar del sistema. Si el nombre de archivo es una cadena vacía ("") y el argumento *DriverCompletion* no es SQL_DRIVER_NOPROMPT, el nombre de archivo es válido. Si el nombre de archivo ya existe, si *DriverCompletion* es SQL_DRIVER_NOPROMPT, el archivo se sobrescribe. Si *DriverCompletion* es SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, un cuadro de diálogo solicita al usuario que especifique si se debe sobrescribir el archivo. Si se introduce No, aparece el cuadro de diálogo **Guardar archivo.**  
  
2.  Si el controlador devuelve SQL_SUCCESS y el nombre de archivo no era una cadena vacía, el Administrador de controladores escribe la información de conexión devuelta en el argumento *OutConnectionString* en el archivo especificado con el formato especificado en la sección "Cadenas de conexión" anteriormente en esta sección.  
  
3.  Si el controlador devuelve SQL_SUCCESS y el nombre de archivo era una cadena vacía (""), el Administrador de controladores llama al cuadro de diálogo común **Guardar archivo** con el *hwnd* especificado y escribe la información de conexión devuelta en *OutConnectionString* en el archivo especificado en el cuadro de diálogo común Guardar archivo con el formato especificado en la sección "Cadenas de conexión" anteriormente en esta sección.  
  
4.  Si el controlador devuelve SQL_SUCCESS, devuelve el argumento *OutConnectionString* que contiene la cadena de conexión a la aplicación.  
  
5.  Si el controlador devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR, el Administrador de controladores devuelve SQLSTATE a la aplicación.  
  
## <a name="driver-guidelines"></a>Pautas del conductor  
 El controlador comprueba si la cadena de conexión que le ha pasado el Administrador de controladores contiene la palabra clave **DSN** o **DRIVER.** Si la cadena de conexión contiene la palabra clave **DRIVER,** el controlador no puede recuperar información sobre el origen de datos de la información del sistema. Si la cadena de conexión contiene la palabra clave **DSN** o no contiene la palabra clave **DSN** o **DRIVER,** el controlador puede recuperar información sobre el origen de datos de la información del sistema de la siguiente manera:  
  
1.  Si la cadena de conexión contiene la palabra clave **DSN,** el controlador recupera la información del origen de datos especificado.  
  
2.  Si la cadena de conexión no contiene la palabra clave **DSN,** no se encuentra el origen de datos especificado o la palabra clave **DSN** se establece en "DEFAULT", el controlador recupera la información del origen de datos predeterminado.  
  
 El controlador utiliza cualquier información que recupera de la información del sistema para aumentar la información que se le pasa en la cadena de conexión. Si la información de la información del sistema duplica la información de la cadena de conexión, el controlador utiliza la información de la cadena de conexión.  
  
 En función del valor de *DriverCompletion*, el controlador solicita al usuario información de conexión, como el ID de usuario y la contraseña, y se conecta al origen de datos:  
  
-   SQL_DRIVER_PROMPT: el controlador muestra un cuadro de diálogo, utilizando los valores de la cadena de conexión y la información del sistema (si existe) como valores iniciales. Cuando el usuario sale del cuadro de diálogo, el controlador se conecta al origen de datos. También construye una cadena de conexión a partir **DRIVER** del valor \*de la palabra clave **DSN** o DRIVER en *InConnectionString* y la información devuelta desde el cuadro de diálogo. Coloca esta cadena de conexión en el **OutConnectionString* búfer.  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: si la cadena de conexión contiene suficiente información y esa \*información es \*correcta, el controlador se conecta al origen de datos y copia *InConnectionString* en *OutConnectionString*. Si falta alguna información o es incorrecta, el controlador realiza las mismas acciones que cuando *DriverCompletion* está SQL_DRIVER_PROMPT, excepto que si *DriverCompletion* es SQL_DRIVER_COMPLETE_REQUIRED, el controlador deshabilita los controles para cualquier información que no sea necesaria para conectarse al origen de datos.  
  
-   SQL_DRIVER_NOPROMPT: si la cadena de conexión contiene suficiente información, \*el controlador \*se conecta al origen de datos y copia *InConnectionString* en *OutConnectionString*. De lo contrario, el controlador devuelve SQL_ERROR para **SQLDriverConnect**.  
  
 En la conexión correcta al origen \*de datos, el controlador también establece *StringLength2Ptr* en la longitud de la cadena de conexión de salida que está disponible para devolver en **OutConnectionString*.  
  
 Si el usuario cancela un cuadro de diálogo presentado por el Administrador de controladores o el controlador, **SQLDriverConnect** devuelve SQL_NO_DATA.  
  
 Para obtener información sobre cómo interactúan el Administrador de controladores y el controlador durante el proceso de conexión, vea [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Si un controlador admite **SQLDriverConnect**, la sección de palabraclave del controlador de la información del sistema para el controlador debe contener la palabra clave **ConnectFunctions** con el segundo juego de caracteres en "Y".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Conexión cuando se habilita la agrupación de conexiones  
 La agrupación de conexiones permite a una aplicación reutilizar una conexión que ya se ha creado. Cuando **SQLDriverConnect** se llama, el Administrador de controladores intenta realizar la conexión mediante una conexión que forma parte de un grupo de conexiones en un entorno que se ha designado para la agrupación de conexiones. Para obtener más información sobre la agrupación de conexiones, vea [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Una aplicación puede establecer SQL_ATTR_RESET_CONNECTION antes de llamar a SQLDisconnect en una conexión donde está habilitada la agrupación. Para obtener más información, vea [Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Las siguientes restricciones se aplican cuando una aplicación llama a **SQLDriverConnect** para conectarse a una conexión agrupada:  
  
-   No se realiza ningún procesamiento de agrupación de conexiones cuando se especifica la palabra clave **SAVEFILE** en la cadena de conexión.  
  
-   Si la agrupación de conexiones está habilitada, **SQLDriverConnect** solo se puede llamar con un *argumento DriverCompletion* de SQL_DRIVER_NOPROMPT; si se llama a **SQLDriverConnect** con cualquier otro *DriverCompletion*, se devolverá SQLSTATE HY110 (finalización del controlador no válido).  
  
## <a name="connection-attributes"></a>Atributos de conexión  
 El atributo de conexión SQL_ATTR_LOGIN_TIMEOUT, establecido mediante **SQLSetConnectAttr**, define el número de segundos que se debe esperar a que se complete una solicitud de inicio de sesión con una conexión correcta por parte del controlador antes de volver a la aplicación. Si se solicita al usuario que complete la cadena de conexión, se inicia un período de espera para cada solicitud de inicio de sesión cuando el controlador inicia el proceso de conexión.  
  
 El controlador abre la conexión en SQL_MODE_READ_WRITE modo de acceso de forma predeterminada. Para establecer el modo de acceso en SQL_MODE_READ_ONLY, la aplicación debe llamar a **SQLSetConnectAttr** con el atributo SQL_ATTR_ACCESS_MODE antes de llamar a **SQLDriverConnect**.  
  
 Si se especifica una biblioteca de traducción predeterminada en la información del sistema para el origen de datos, el controlador la carga. Se puede cargar una biblioteca de traducción diferente llamando a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_LIB. Se puede especificar una opción de traducción llamando a **SQLSetConnectAttr** con la opción SQL_ATTR_TRANSLATE_OPTION.  
  
 Para obtener más información, consulte [Conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
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
  
 Consulte también [Programa ODBC de ejemplo](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descubrir y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectarse de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Devolver las descripciones y atributos del controlador|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberar un mango|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
