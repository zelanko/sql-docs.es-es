---
title: Función SQLBrowseConnect (SQLBrowseConnect) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301345"
---
# <a name="sqlbrowseconnect-function"></a>Función SQLBrowseConnect
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLBrowseConnect** admite un método iterativo para detectar y enumerar los atributos y valores de atributo necesarios para conectarse a un origen de datos. Cada llamada a **SQLBrowseConnect** devuelve niveles sucesivos de atributos y valores de atributo. Cuando se han enumerado todos los niveles, se completa una conexión con el origen de datos y **SQLBrowseConnect**devuelve una cadena de conexión completa. Un código de retorno de SQL_SUCCESS o SQL_SUCCESS_WITH_INFO indica que se ha especificado toda la información de conexión y que la aplicación está conectada al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *InConnectionString*  
 [Entrada] Examine la cadena de conexión de solicitud (consulte "*InConnectionString* Argument" en "Comments").  
  
 *StringLength1*  
 [Entrada] Longitud de **InConnectionString* en caracteres.  
  
 *OutConnectionString*  
 [Salida] Puntero a un búfer de caracteres en el que se va a devolver la cadena de conexión de resultado de exploración (consulte "*OutConnectionString* Argument" en "Comments").  
  
 Si *OutConnectionString* es NULL, *StringLength2Ptr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Longitud, en caracteres, del búfer **OutConnectionString.*  
  
 *StringLength2Ptr*  
 [Salida] El número total de caracteres (excluyendo la \*terminación nula) disponibles para devolver en *OutConnectionString*. Si el número de caracteres disponibles para devolver es mayor \*o igual que *BufferLength*, la cadena de conexión de *OutConnectionString* se trunca en *BufferLength* menos la longitud de un carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLBrowseConnect** devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO o SQL_NEED_DATA, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control de ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLBrowseConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *OutConnectionString* no era lo suficientemente grande como para devolver toda la cadena de conexión de resultados de exploración, por lo que la cadena se truncó. El búfer **StringLength2Ptr* contiene la longitud de la cadena de conexión de resultados de exploración no truncada. (La función devuelve SQL_NEED_DATA.)|  
|01S00|Atributo de cadena de conexión no válido|Se especificó una palabra clave de atributo no válida en la cadena de conexión de solicitud de exploración (*InConnectionString*). (La función devuelve SQL_NEED_DATA.)<br /><br /> Se especificó una palabra clave de atributo en la cadena de conexión de solicitud de exploración (*InConnectionString*) que no se aplica al nivel de conexión actual. (La función devuelve SQL_NEED_DATA.)|  
|01S02|Valor cambiado|El controlador no admitía el valor especificado del argumento *ValuePtr* en **SQLSetConnectAttr** y sustituyó un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de establecer conexión|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de conexión en uso|(DM) La conexión especificada ya se había utilizado para establecer una conexión con un origen de datos y la conexión estaba abierta.|  
|08004|El servidor rechazó la conexión|El origen de datos rechazó el establecimiento de la conexión por razones definidas por la implementación.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que el controlador intentaba conectarse antes de que la función completara el procesamiento.|  
|28000|Especificación de autorización no válida|El identificador de usuario o la cadena de autorización o ambos, como se especifica en la cadena de conexión de solicitud de exploración (*InConnectionString*), infringió las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|(DM) El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.<br /><br /> El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|Se canceló una operación asincrónica llamando a [SQLCancelHandle (función).](../../../odbc/reference/syntax/sqlcancelhandle-function.md) A continuación, se volvió a llamar a la función original en *ConnectionHandle*.<br /><br /> Una operación se canceló mediante una llamada a **SQLCancelHandle** en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica (no esta) para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *StringLength1* era menor que 0 y no era igual a SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY114|El controlador no admite la ejecución de funciones asincrónicas de nivel de conexión|(DM) La aplicación habilitó la operación asincrónica en el identificador de conexión antes de realizar la conexión. Sin embargo, el controlador no admite la operación asincrónica en el identificador de conexión.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de inicio de sesión expiró antes de que se completara la conexión con el origen de datos. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador correspondiente al nombre de origen de datos especificado no admite la función.|  
|IM002|Origen de datos no encontrado y no se especificó ningún controlador predeterminado|(DM) El nombre del origen de datos especificado en la cadena de conexión de solicitud de exploración (*InConnectionString*) no se encontró en la información del sistema, ni había una especificación de controlador predeterminada.<br /><br /> (DM) El origen de datos ODBC y la información predeterminada del controlador no se pudo encontrar en la información del sistema.|  
|IM003|No se pudo cargar el controlador especificado|(DM) El controlador que aparece en la especificación del origen de datos en la información del sistema o especificado por la palabra clave **DRIVER** no se encontró o no se pudo cargar por algún otro motivo.|  
|IM004|Error del controlador **SQLAllocHandle** en SQL_HANDLE _ENV|(DM) Durante **SQLBrowseConnect**, el Administrador de controladores llamó a la función **SQLAllocHandle** del controlador con un *HandleType* de SQL_HANDLE_ENV y el controlador devolvió un error.|  
|IM005|**SqlAllocHandle** del controlador en SQL_HANDLE_DBC ha fallado|(DM) Durante **SQLBrowseConnect**, el Administrador de controladores llamó a la función **SQLAllocHandle** del controlador con un *HandleType* de SQL_HANDLE_DBC y el controlador devolvió un error.|  
|IM006|Error del controlador **SQLSetConnectAttr**|(DM) Durante **SQLBrowseConnect**, el Administrador de controladores llamó a la función **SQLSetConnectAttr** del controlador y el controlador devolvió un error.|  
|IM009|No se puede cargar DLL de traducción|El controlador no pudo cargar el archivo DLL de traducción que se especificó para el origen de datos o para la conexión.|  
|IM010|Nombre del origen de datos demasiado largo|(DM) el valor de atributo de la palabra clave DSN era más largo que SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nombre del conductor demasiado largo|(DM) el valor del atributo de la palabra clave DRIVER tenía más de 255 caracteres.|  
|IM012|Error de sintaxis de palabra clave DRIVER|(DM) El par palabra clave-valor de la palabra clave DRIVER contenía un error de sintaxis.|  
|IM014|El DSN especificado contiene una discordancia de arquitectura entre el controlador y la aplicación|(DM) aplicación de 32 bits utiliza un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
|S1118|El controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT ni SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argumento InConnectionString  
 Una cadena de conexión de solicitud de exploración tiene la sintaxis siguiente:  
  
 *connection-string* ::-`;` *attribute*[ ] &#124; *atributo* `;` *connection-string*;<br>
 *atributo* ::- *atributo-palabra*`=`clave `DRIVER=``{`*atributo-valor* &#124;`}`[ ]*atributo-valor*[ ]<br>
 *atributo-palabra clave* `DSN` ::- &#124; &#124; `UID` &#124; `PWD` *driver-defined-attribute-keyword*<br>
 *valor-atributo* ::- *carácter-cadena*<br>
 *identificador definido por el conductor-atributo::-* *identifier*<br>
  
 donde *la cadena de caracteres* tiene cero o más caracteres; *identificador* tiene uno o más caracteres; *attribute-keyword* no distingue mayúsculas de minúsculas; *atributo-valor* puede distinguir entre mayúsculas y minúsculas; y el valor de la palabra clave **DSN** no consiste únicamente en espacios en blanco. Debido a la cadena de conexión y la gramática del archivo de inicialización, palabras clave y valores de atributo que contienen los caracteres **[]{}(),;? Debe \*** evitarse. Debido a la gramática de la información del sistema, las\\palabras clave y los nombres de origen de datos no pueden contener el carácter de barra diagonal inversa ( ). Para un ODBC 2. *x* controlador, se requieren llaves alrededor del valor de atributo para la palabra clave DRIVER.  
  
 Si se repite alguna palabra clave en la cadena de conexión de solicitud de exploración, el controlador utiliza el valor asociado con la primera aparición de la palabra clave. Si las palabras clave **DSN** y **DRIVER** se incluyen en la misma cadena de conexión de solicitud de exploración, el Administrador de controladores y el controlador usan la palabra clave que aparezca primero.  
  
 Para obtener información sobre cómo una aplicación elige un origen de datos o un controlador, vea Elegir un origen de [datos o un controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argumento OutConnectionString  
 La cadena de conexión de resultados de exploración es una lista de atributos de conexión. Un atributo de conexión consta de una palabra clave de atributo y un valor de atributo correspondiente. La cadena de conexión de resultados de exploración tiene la sintaxis siguiente:  
  
 *connection-string* ::-`;` *atributo*[ ] &#124; *atributo* `;` *connection-string*<br>
 *atributo* ::-`*`[ ]*atributo-palabra clave*`=`*atributo-valor*<br>
 *attribute-keyword* ::- *ODBC-attribute-keyword* &#124; *driver-defined-attribute-keyword*<br>
 *ODBC-attribute-keyword* á`UID` `PWD`á`:`&#124; á[*localized-identifier*] *driver-defined-attribute-keyword* ::- *identificador*`:`[ `{` *localized-identifier*] *attribute-value* ::- *attribute-value-list* `}` &#124; `?` (Las llaves son literales; son devueltas por el controlador.)<br>
 *attribute-value-list* ::- *character-string* `:`[*localized-character string*] &#124; *character-string* [`:`*localized-character string*] `,` *attribute-value-list*<br>
  
 donde *la cadena de caracteres* y la cadena de *caracteres localizados* tienen cero o más caracteres; *identificador* y *identificador localizado* tienen uno o más caracteres; *attribute-keyword* no distingue mayúsculas de minúsculas; y *atributo-valor* puede distinguir entre mayúsculas y minúsculas. Debido a la gramática de la cadena de conexión y del archivo de inicialización, las palabras clave, los identificadores localizados y los valores de atributo que contienen los caracteres **[]{}(),;? Debe \*** evitarse. Debido a la gramática de la información del sistema, las\\palabras clave y los nombres de origen de datos no pueden contener el carácter de barra diagonal inversa ( ).  
  
 La sintaxis de cadena de conexión de resultado de exploración se utiliza de acuerdo con las siguientes reglas semánticas:  
  
-   Si un\*asterisco ( ) precede a una *palabra clave de atributo*, el *atributo* es opcional y se puede omitir en la siguiente llamada a **SQLBrowseConnect**.  
  
-   Las palabras clave de atributo **UID** y **PWD** tienen el mismo significado que se define en **SQLDriverConnect**.  
  
-   Un *driver-defined-attribute-keyword* nombra el tipo de atributo para el que se puede proporcionar un valor de atributo. Por ejemplo, puede ser **SERVER**, **DATABASE**, **HOST**o **DBMS**.  
  
-   *ODBC-attribute-keywords* y *driver-defined-attribute-keywords* incluyen una versión localizada o fácil de usar de la palabra clave. Esto puede ser utilizado por las aplicaciones como una etiqueta en un cuadro de diálogo. Sin embargo, **UID**, **PWD**o el *identificador* solo se deben usar al pasar una cadena de solicitud de exploración al controlador.  
  
-   La lista de*valores-atributo*es una enumeración de valores reales válidos para la *palabra clave de atributo*correspondiente. Tenga en cuenta{}que las llaves ( ) no indican una lista de opciones; son devueltos por el conductor. Por ejemplo, podría ser una lista de nombres de servidor o una lista de nombres de base de datos.  
  
-   Si el *valor-atributo* es un único signo de interrogación (?), un único valor corresponde a la *palabra clave de atributo*. Por ejemplo, UID-JohnS; PWD-Sesame.  
  
-   Cada llamada a **SQLBrowseConnect** devuelve solo la información necesaria para satisfacer el siguiente nivel del proceso de conexión. El controlador asocia la información de estado con el identificador de conexión para que el contexto siempre se pueda determinar en cada llamada.  
  
## <a name="using-sqlbrowseconnect"></a>Uso de SQLBrowseConnect  
 **SQLBrowseConnect** requiere una conexión asignada. El Administrador de controladores carga el controlador que se especificó o que corresponde al nombre del origen de datos especificado en la cadena de conexión de solicitud de exploración inicial; para obtener información sobre cuándo ocurre esto, consulte la sección "Comentarios" en [SqlConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md). El controlador puede establecer una conexión con el origen de datos durante el proceso de exploración. Si **SQLBrowseConnect** devuelve SQL_ERROR, se terminan las conexiones pendientes y la conexión se devuelve a un estado no conectado.  
  
> [!NOTE]  
>  **SQLBrowseConnect** no admite la agrupación de conexiones. Si se llama a **SQLBrowseConnect** mientras la agrupación de conexiones está habilitada, se devolverá SQLSTATE HY000 (error general).  
  
 Cuando **SQLBrowseConnect** se llama por primera vez en una conexión, la cadena de conexión de solicitud de exploración debe contener la palabra clave **DSN** o la palabra clave **DRIVER.** Si la cadena de conexión de solicitud de exploración contiene la palabra clave **DSN,** el Administrador de controladores localiza una especificación de origen de datos correspondiente en la información del sistema:  
  
-   Si el Administrador de controladores encuentra la especificación de origen de datos correspondiente, carga el archivo DLL del controlador asociado; el controlador puede recuperar información sobre el origen de datos de la información del sistema.  
  
-   Si el Administrador de controladores no puede encontrar la especificación de origen de datos correspondiente, busca la especificación de origen de datos predeterminada y carga el archivo DLL del controlador asociado; el controlador puede recuperar información sobre el origen de datos predeterminado de la información del sistema. "DEFAULT" se pasa al controlador para el DSN.  
  
-   Si el Administrador de controladores no puede encontrar la especificación de origen de datos correspondiente y no hay ninguna especificación de origen de datos predeterminada, devuelve SQL_ERROR con SQLSTATE IM002 (origen de datos no encontrado y no se especifica ningún controlador predeterminado).  
  
 Si la cadena de conexión de solicitud de exploración contiene la palabra clave **DRIVER,** el Administrador de controladores carga el controlador especificado; no intenta localizar un origen de datos en la información del sistema. Dado que la palabra clave **DRIVER** no utiliza información de la información del sistema, el controlador debe definir suficientes palabras clave para que un controlador pueda conectarse a un origen de datos utilizando solo la información de las cadenas de conexión de solicitud de exploración.  
  
 En cada llamada a **SQLBrowseConnect**, la aplicación especifica los valores de atributo de conexión en la cadena de conexión de solicitud de exploración. El controlador devuelve niveles sucesivos de atributos y valores de atributo en la cadena de conexión de resultados de exploración; devuelve SQL_NEED_DATA siempre que haya atributos de conexión que aún no se han enumerado en la cadena de conexión de solicitud de exploración. La aplicación utiliza el contenido de la cadena de conexión de resultados de exploración para compilar la cadena de conexión de solicitud de exploración para la siguiente llamada a **SQLBrowseConnect**. Todos los atributos obligatorios (los que no van precedidos por un asterisco en el argumento *OutConnectionString)* deben incluirse en la siguiente llamada a **SQLBrowseConnect**. Tenga en cuenta que la aplicación no puede utilizar el contenido de cadenas de conexión de resultados de exploración anteriores al compilar la cadena de conexión de solicitud de exploración actual; es decir, no puede especificar valores diferentes para los atributos establecidos en los niveles anteriores.  
  
 Cuando se han enumerado todos los niveles de conexión y sus atributos asociados, el controlador devuelve SQL_SUCCESS, la conexión al origen de datos se completa y se devuelve una cadena de conexión completa a la aplicación. La cadena de conexión es adecuada para su uso, junto con **SQLDriverConnect**, con la opción SQL_DRIVER_NOPROMPT para establecer otra conexión. Sin embargo, la cadena de conexión completa no se puede utilizar en otra llamada a **SQLBrowseConnect;** si SE llamara de nuevo **a SQLBrowseConnect,** tendría que repetirse toda la secuencia de llamadas.  
  
 **SQLBrowseConnect** también devuelve SQL_NEED_DATA si hay errores recuperables y no fatales durante el proceso de exploración; por ejemplo, una palabra clave de contraseña o atributo no válida proporcionada por la aplicación. Cuando se devuelve SQL_NEED_DATA y la cadena de conexión de resultado de exploración no cambia, se ha producido un error y la aplicación puede llamar a **SQLGetDiagRec** para devolver SQLSTATE para errores de tiempo de exploración. Esto permite que la aplicación corrija el atributo y continúe la exploración.  
  
 Una aplicación puede finalizar el proceso de exploración en cualquier momento llamando a **SQLDisconnect**. El controlador finalizará las conexiones pendientes y devolverá la conexión a un estado desconectado.  
  
 Si las operaciones asincrónicas están habilitadas en el identificador de conexión, **SQLBrowseConnect** también podría devolver SQL_STILL_EXECUTING. Cuando devuelve SQL_NEED_DATA, una aplicación debe usar **SQLDisconnect** para cancelar el proceso de exploración. Si **SQLBrowseConnect** devuelve SQL_STILL_EXECUTING, una aplicación debe usar **SQLCancelHandle** para cancelar la operación en curso. Llamar a **SQLCancelHandle** después de que la función devuelve SQL_NEED_DATA no tiene ningún efecto.  
  
 Para obtener más información, consulte [Conexión con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Si un controlador admite **SQLBrowseConnect**, la sección de palabraclave del controlador en la información del sistema para el controlador debe contener la palabra clave **ConnectFunctions** con el tercer conjunto de caracteres en "Y."  
  
## <a name="code-example"></a>Ejemplo de código  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de `Trusted_Connection=yes` datos que admite la autenticación de Windows, debe especificar en lugar de la información de ID de usuario y contraseña en la cadena de conexión.  
  
 En el ejemplo siguiente, una aplicación llama a **SQLBrowseConnect** repetidamente. Cada vez que **SQLBrowseConnect** devuelve SQL_NEED_DATA, devuelve información \*sobre los datos que necesita en *OutConnectionString*. La aplicación pasa *OutConnectionString* a su rutina **GetUserInput** (no se muestra). **GetUserInput** analiza la información, compila y muestra un cuadro de diálogo \*y devuelve la información introducida por el usuario en *InConnectionString*. La aplicación pasa la información del usuario al controlador en la siguiente llamada a **SQLBrowseConnect**. Después de que la aplicación ha proporcionado toda la información necesaria para que el controlador se conecte al origen de datos, **SQLBrowseConnect** devuelve SQL_SUCCESS y la aplicación continúa.  
  
 Para obtener un ejemplo más detallado de cómo conectarse a un controlador de SQL Server mediante una llamada a **SQLBrowseConnect**, vea Ejemplo de [exploración](../../../odbc/reference/develop-app/sql-server-browsing-example.md)de SQL Server .  
  
 Por ejemplo, para conectarse al origen de datos Sales, pueden producirse las siguientes acciones. En primer lugar, la aplicación pasa la siguiente cadena a **SQLBrowseConnect:**  
  
```  
"DSN=Sales"  
```  
  
 El Administrador de controladores carga el controlador asociado con el origen de datos Sales. A continuación, llama a la función **SQLBrowseConnect** del controlador con los mismos argumentos que recibió de la aplicación. El controlador devuelve la siguiente cadena en **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 La aplicación pasa esta cadena a su rutina **GetUserInput,** que crea un cuadro de diálogo que solicita al usuario que seleccione el servidor rojo, azul o verde e introduzca un ID de usuario y una contraseña. La rutina devuelve la siguiente información especificada \*por el usuario en *InConnectionString*, que la aplicación pasa a **SQLBrowseConnect:**  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** utiliza esta información para conectarse al servidor rojo como Smith con la contraseña Sesame y, a continuación, devuelve la siguiente cadena en **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 La aplicación pasa esta cadena a su rutina **GetUserInput,** que crea un cuadro de diálogo que solicita al usuario que seleccione una base de datos. El usuario selecciona empdata y la aplicación llama a **SQLBrowseConnect** una última vez con esta cadena:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Esta es la información final que el controlador necesita para conectarse al origen de datos; **SQLBrowseConnect** devuelve SQL_SUCCESS y **OutConnectionString* contiene la cadena de conexión completada:  
  
```cpp  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un controlador de conexión|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectarse de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conexión a un origen de datos mediante una cadena de conexión o un cuadro de diálogo|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Devolver las descripciones y atributos del controlador|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberar un asa de conexión|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
