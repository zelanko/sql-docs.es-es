---
title: Función SQLBrowseConnect | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66daf3ce016b8688ada1d584865a97675a7dbc01
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbrowseconnect-function"></a>Función SQLBrowseConnect
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLBrowseConnect** es compatible con un método iterativo de detectar y enumerar los atributos y valores de atributo necesarios para conectarse a un origen de datos. Cada llamada a **SQLBrowseConnect** devuelve niveles sucesivos de atributos y valores de atributo. Cuando se han enumerado todos los niveles, se realiza una conexión al origen de datos y se devuelve una cadena de conexión completa mediante **SQLBrowseConnect**. Un código de retorno de SQL_SUCCESS o SQL_SUCCESS_WITH_INFO indica que se ha especificado toda la información de conexión y la aplicación está ahora conectada al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *IdentificadorConexión*  
 [Entrada] Identificador de conexión.  
  
 *InConnectionString*  
 [Entrada] Examinar la cadena de conexión de la solicitud (vea "*InConnectionString* argumento" en "Comentarios").  
  
 *StringLength1*  
 [Entrada] Longitud de **InConnectionString* en caracteres.  
  
 *OutConnectionString*  
 [Salida] Puntero a un búfer de caracteres en el que se va a devolver la cadena de conexión de resultados de exploración (consulte "*OutConnectionString* argumento" en "Comentarios").  
  
 Si *OutConnectionString* es NULL, *StringLength2Ptr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer que señala *OutConnectionString*.  
  
 *BufferLength*  
 [Entrada] Longitud, en caracteres, de la **OutConnectionString* búfer.  
  
 *StringLength2Ptr*  
 [Salida] El número total de caracteres (excluyendo-finalización en null) disponible para devolver en \* *OutConnectionString*. Si el número de caracteres disponibles para devolver es mayor o igual que *BufferLength*, la cadena de conexión en \* *OutConnectionString* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLBrowseConnect** devuelve SQL_NEED_DATA, un valor SQLSTATE asociado, SQL_SUCCESS_WITH_INFO o SQL_ERROR puede obtenerse mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *identificador de IdentificadorConexión*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLBrowseConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|El búfer \* *OutConnectionString* no era lo suficientemente grande como para devolver la cadena de conexión de resultados de exploración completa, por lo que la cadena se truncó. El búfer **StringLength2Ptr* contiene la longitud de la cadena de conexión de resultados de exploración untruncated. (La función devuelve SQL_NEED_DATA.)|  
|01S00|Atributo de cadena de conexión no válido|Se especificó una palabra clave de atributo no válido en la cadena de conexión de la solicitud de exploración (*InConnectionString*). (La función devuelve SQL_NEED_DATA.)<br /><br /> Se especificó una palabra clave de atributo en la cadena de conexión de la solicitud de exploración (*InConnectionString*) que no se aplica al nivel de conexión actual. (La función devuelve SQL_NEED_DATA.)|  
|01S02|Valor ha cambiado|El controlador no admitía el valor especificado de la *ValuePtr* argumento en **SQLSetConnectAttr** y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08001|No se puede establecer la conexión de cliente|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de la conexión en uso|(DM) la conexión especificada ya hubiese utilizada para establecer una conexión con un origen de datos y estuvo abierta la conexión.|  
|08004|Servidor rechazó la conexión|El origen de datos rechazó el establecimiento de la conexión por motivos de definido por la implementación.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos a la que estaba intentando conectar el controlador no pudo antes del procesamiento de la función se ha completado.|  
|28000|Especificación de autorización no válido|El identificador de usuario, la cadena de autorización o ambos, según se especifica en el botón Examinar solicitan la cadena de conexión (*InConnectionString*), han infringido las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El Administrador de controladores (DM) no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.<br /><br /> El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Se canceló una operación asincrónica mediante una llamada a [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md). A continuación, se llamó a la función original en el *IdentificadorConexión*.<br /><br /> Se canceló una operación mediante una llamada a **SQLCancelHandle** en el *IdentificadorConexión* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *IdentificadorConexión* y aún se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *StringLength1* era menor que 0 y no era igual a SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY114|Controlador no admite la ejecución de la función asincrónica de nivel de conexión|(DM) la aplicación habilitada la operación asincrónica en el identificador de conexión antes de realizar la conexión. Sin embargo, el controlador no es compatible con la operación asincrónica en el identificador de conexión.|  
|HYT00|Se agotó el tiempo de espera|Ha caducado el período de tiempo de espera de inicio de sesión antes de la conexión al origen de datos completado. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente al nombre de origen de datos especificado no es compatible con la función.|  
|IM002|No se encontró el origen de datos y se especificó ningún controlador predeterminado|Nombre especificado en la cadena de conexión de la solicitud de examen del origen de datos (DM) (*InConnectionString*) no se encontró en la información del sistema, así como tampoco había una especificación de controlador de forma predeterminada.<br /><br /> (DM) no se encontró información del controlador de origen y el valor predeterminado de datos ODBC en la información del sistema.|  
|IM003|No se pudo cargar el controlador especificado|(DM) el controlador aparecen en la especificación de origen de datos en la información del sistema o especificado por el **controlador** palabra clave no se encontró o no se puede cargar por alguna otra razón.|  
|IM004|Del controlador **SQLAllocHandle** en _ENV SQL_HANDLE error|(DM) durante la **SQLBrowseConnect**, el Administrador de controladores denominado el controlador **SQLAllocHandle** funcionando con un *HandleType* de SQL_HANDLE_ENV y el controlador devuelve un error.|  
|IM005|Del controlador **SQLAllocHandle** en SQL_HANDLE_DBC error|(DM) durante la **SQLBrowseConnect**, el Administrador de controladores denominado el controlador **SQLAllocHandle** funcionando con un *HandleType* de SQL_HANDLE_DBC y el controlador devuelve un error.|  
|IM006|Del controlador **SQLSetConnectAttr** error|(DM) durante la **SQLBrowseConnect**, el Administrador de controladores denominado el controlador **SQLSetConnectAttr** función y el controlador ha devuelto un error.|  
|IM009|No se puede cargar el archivo DLL de traducción|El controlador no pudo cargar el archivo DLL que se especificó para el origen de datos o para la conexión de traducción.|  
|IM010|Nombre del origen de datos es demasiado largo|(DM) el valor de atributo para la palabra clave DSN era más de SQL_MAX_DSN_LENGTH caracteres.|  
|IM011|Nombre de controlador demasiado largo|(DM) el valor de atributo para la palabra clave DRIVER era más de 255 caracteres.|  
|IM012|Error de sintaxis de palabra clave DRIVER|(DM) el par de palabra clave y valor para la palabra clave DRIVER contenía un error de sintaxis.|  
|IM014|El DSN especificado contiene un error de coincidencia de arquitectura entre el controlador y la aplicación|Aplicación de 32 bits (DM) usa un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
|S1118|Controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argumento de InConnectionString  
 Una cadena de conexión de la solicitud de exploración tiene la siguiente sintaxis:  
  
 *cadena de conexión* :: = *atributo*[`;`] &#124; *atributo* `;` *cadena de conexión*;<br>
 *atributo* :: = *palabra clave de atributo*`=`*atributo-valor* &#124; `DRIVER=`[`{`]*atributo-valor*[`}`]<br>
 *attribute-keyword* ::= `DSN` &#124; `UID` &#124; `PWD` &#124; *driver-defined-attribute-keyword*<br>
 *valor del atributo* :: = *cadena de caracteres*<br>
 *driver-defined-attribute-keyword* ::= *identifier*<br>
  
 donde *cadena de caracteres* tiene cero o más caracteres; *identificador* tiene uno o más caracteres; *palabra clave de atributo* no distingue mayúsculas de minúsculas; *atributo-valor* puede distinguir mayúsculas de minúsculas; y el valor de la **DSN** palabra clave no contener solamente espacios en blanco. ¿Debido a la cadena e inicialización archivo gramática, palabras clave y atributo de valores de conexión que contienen los caracteres **[]{}(),? \*=! @** debería evitarse. Debido a la gramática de la información del sistema, los nombres de origen de datos y palabras clave no pueden contener la barra diagonal inversa (\\) caracteres. Para un ODBC 2. *x* controlador, las llaves son necesarias alrededor del valor de atributo para la palabra clave DRIVER.  
  
 Si todas las palabras clave se repite en la cadena de conexión de la solicitud de examen, el controlador utiliza el valor asociado a la primera aparición de la palabra clave. Si el **DSN** y **controlador** palabras clave se incluye en la misma cadena de conexión de la solicitud de exploración, el Administrador de controladores y el controlador usan la palabra clave aparece en primer lugar.  
  
 Para obtener información acerca de cómo una aplicación elige un origen de datos o el controlador, consulte [elegir un origen de datos o el controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argumento de OutConnectionString  
 La cadena de conexión de resultados de exploración es una lista de atributos de conexión. Un atributo de conexión consta de una palabra clave de atributo y un valor de atributo correspondiente. La cadena de conexión de resultados de exploración tiene la siguiente sintaxis:  
  
 *cadena de conexión* :: = *atributo*[`;`] &#124; *atributo* `;` *cadena de conexión*<br>
 *atributo* :: = [`*`]*palabra clave de atributo*`=`*valor de atributo*<br>
 *attribute-keyword* ::= *ODBC-attribute-keyword* &#124; *driver-defined-attribute-keyword*<br>
 *ODBC-attribute-keyword* = {`UID` &#124; `PWD`}[`:`*localized-identifier*] *driver-defined-attribute-keyword* ::= *identifier*[`:`*localized-identifier*] *attribute-value* ::= `{` *attribute-value-list* `}` &#124; `?` (The braces are literal; they are returned by the driver.)<br>
 *lista de valores de atributo* :: = *cadena de caracteres* [`:`*cadena de caracteres localizados*] &#124; *cadena de caracteres* [`:` *cadena de caracteres localizados*] `,` *lista de valores de atributo*<br>
  
 donde *cadena de caracteres* y *cadena de caracteres localizados* tiene cero o más caracteres; *identificador* y *identificador adaptado* tiene uno o más caracteres; *palabra clave de atributo* no distingue mayúsculas de minúsculas; y *atributo-valor* puede distinguir mayúsculas de minúsculas. ¿Debido a la conexión de cadena e inicialización gramática, palabras clave, localizados identificadores de archivos y valores de atributo que contienen los caracteres **[]{}(),? \*=! @** debería evitarse. Debido a la gramática de la información del sistema, los nombres de origen de datos y palabras clave no pueden contener la barra diagonal inversa (\\) caracteres.  
  
 Se utiliza la sintaxis de cadena de conexión de resultados de exploración según las siguientes reglas semánticas:  
  
-   Si un asterisco (\*) precede a un *palabra clave de atributo*, *atributo* es opcional y puede omitirse en la siguiente llamada a **SQLBrowseConnect**.  
  
-   Las palabras clave de atributo **UID** y **PWD** tienen el mismo significado, tal como se define en **SQLDriverConnect**.  
  
-   A *-definido-atributo-palabra clave driver* nombres del tipo de atributo para el que se puede proporcionar un valor de atributo. Por ejemplo, podría ser **SERVER**, **base de datos**, **HOST**, o **DBMS**.  
  
-   *Palabras clave de atributo de ODBC* y *controlador--atributo-palabras clave definidas por* incluyen una versión localizada o fácil de usar de la palabra clave. Esto podría utilizarse en aplicaciones como una etiqueta en un cuadro de diálogo. Sin embargo, **UID**, **PWD**, o la *identificador* por sí solo debe utilizarse cuando se pasa una cadena de solicitud de exploración para el controlador.  
  
-   El {*lista de valores de atributo*} es una enumeración de los valores reales válidos para el correspondiente *palabra clave de atributo*. Tenga en cuenta que las llaves ({}) no indican una lista de opciones; son devueltos por el controlador. Por ejemplo, puede obtener una lista de nombres de servidor o una lista de nombres de base de datos.  
  
-   Si el *atributo-valor* es un único signo de interrogación (?), un único valor corresponde a la *palabra clave de atributo*. Por ejemplo, UID = JohnS; PWD = forma de sésamo.  
  
-   Cada llamada a **SQLBrowseConnect** devuelve únicamente la información necesaria para satisfacer el nivel siguiente del proceso de conexión. El controlador asocia información de estado con el identificador de conexión para que siempre se puede determinar el contexto en cada llamada.  
  
## <a name="using-sqlbrowseconnect"></a>Usar SQLBrowseConnect  
 **SQLBrowseConnect** requiere una conexión a la asignación. El Administrador de controladores se carga el controlador que se especificó en o que corresponde al nombre del origen de datos especificado en la cadena de conexión de solicitud de exploración inicial; Para obtener información sobre cuando esto ocurre, vea la sección "Comentarios" en [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md). El controlador puede establecer una conexión con el origen de datos durante el proceso de exploración. Si **SQLBrowseConnect** devuelve SQL_ERROR, pendientes se terminan las conexiones y la conexión se devuelve a un estado no conectado.  
  
> [!NOTE]  
>  **SQLBrowseConnect** no admite la agrupación de conexiones. Si **SQLBrowseConnect** se llama mientras está habilitada la agrupación de conexiones, SQLSTATE HY000 (error General) se devolverá.  
  
 Cuando **SQLBrowseConnect** se llama por primera vez en una conexión, debe contener la cadena de conexión de la solicitud de examinar el **DSN** palabra clave o el **controlador** palabra clave. Si contiene la cadena de conexión de la solicitud de examinar el **DSN** palabra clave, el Administrador de controladores busca una especificación de origen de datos correspondiente en la información del sistema:  
  
-   Si el Administrador de controladores se encuentra la especificación de origen de datos correspondiente, carga el controlador asociado DLL; el controlador puede recuperar información sobre el origen de datos de la información del sistema.  
  
-   Si el Administrador de controladores no se puede encontrar la especificación de origen de datos correspondiente, busca la especificación del origen de datos de forma predeterminada y se carga el controlador asociado DLL; el controlador puede recuperar información sobre el origen de datos predeterminado de la información del sistema. "DEFAULT" se pasa al controlador para el DSN.  
  
-   Si el Administrador de controladores no se puede encontrar la especificación de origen de datos correspondiente y no hay ninguna especificación de origen de datos de forma predeterminada, devuelve SQL_ERROR con SQLSTATE IM002 (no se encontró el origen de datos y se especificó ningún controlador predeterminado).  
  
 Si contiene la cadena de conexión de la solicitud de examinar el **controlador** palabra clave, el Administrador de controladores, carga el controlador especificado; no intenta buscar un origen de datos en la información del sistema. Dado que la **controlador** palabra clave no utiliza información de la información del sistema, el controlador debe definir suficientes palabras clave para que un controlador puede conectarse a un origen de datos utilizando únicamente la información de las cadenas de conexión de la solicitud de exploración.  
  
 En cada llamada a **SQLBrowseConnect**, la aplicación especifica los valores de atributo de conexión en la cadena de conexión de la solicitud de exploración. El controlador devuelve niveles sucesivos de atributos y valores de atributo en la cadena de conexión de resultados de exploración; devuelve SQL_NEED_DATA mientras hay atributos de conexión que aún no se han enumerado en la cadena de conexión de la solicitud de exploración. La aplicación utiliza el contenido de la cadena de conexión de resultados de exploración para generar la cadena de conexión de la solicitud de exploración para la siguiente llamada a **SQLBrowseConnect**. Todos los atributos obligatorios (las que no va precedido por un asterisco en el *OutConnectionString* argumento) deben incluirse en la siguiente llamada a **SQLBrowseConnect**. Tenga en cuenta que la aplicación no puede usar el contenido de las cadenas de conexión de resultados de exploración anterior al generar la cadena de conexión de solicitud de exploración actual; es decir, no puede especificar valores diferentes para los atributos establecidos en los niveles anteriores.  
  
 Cuando se han enumerado todos los niveles de conexión y sus atributos asociados, el controlador devuelve SQL_SUCCESS, la conexión al origen de datos está completa y se devuelve una cadena de conexión completa a la aplicación. La cadena de conexión es adecuada para usarlo en junto con **SQLDriverConnect**, con la opción SQL_DRIVER_NOPROMPT para establecer otra conexión. No se puede usar la cadena de conexión completa en otra llamada a **SQLBrowseConnect**, sin embargo, si **SQLBrowseConnect** se llama de nuevo toda la secuencia de llamadas que se repite.  
  
 **SQLBrowseConnect** también devuelve SQL_NEED_DATA si hay errores recuperables, recuperables durante el proceso de exploración; por ejemplo, una contraseña no válida o la palabra clave de atributo suministrada por la aplicación. Cuando se devuelve SQL_NEED_DATA, la cadena de conexión de resultados de exploración se no ha cambiado, se ha producido un error y la aplicación puede llamar a **SQLGetDiagRec** para devolver el valor de SQLSTATE de errores en tiempo de exploración. Esto permite que la aplicación para corregir el atributo y continuar con el botón Examinar.  
  
 Una aplicación puede finalizar el proceso de examinar en cualquier momento mediante una llamada a **SQLDisconnect**. El controlador finalizará las conexiones pendientes y devuelva la conexión a un estado no conectado.  
  
 Si se habilitan las operaciones asincrónicas en el identificador de conexión, **SQLBrowseConnect** también podrían devolver SQL_STILL_EXECUTING. Cuando devuelve SQL_NEED_DATA, debe usar una aplicación **SQLDisconnect** cancelar el proceso de exploración. Si **SQLBrowseConnect** devuelve SQL_STILL_EXECUTING, una aplicación debe utilizar **SQLCancelHandle** para cancelar la operación en curso. Al llamar a **SQLCancelHandle** después de la función devuelve SQL_NEED_DATA no tiene ningún efecto.  
  
 Para obtener más información, consulte [conectarse con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Si un controlador es compatible con **SQLBrowseConnect**, la sección de la palabra clave driver en la información del sistema para el controlador debe contener el **ConnectFunctions** palabra clave con el tercer carácter establecido en "Y".  
  
## <a name="code-example"></a>Ejemplo de código  
  
> [!NOTE]  
>  Si se conecta a un proveedor de origen de datos que admita la autenticación de Windows, debe especificar `Trusted_Connection=yes` en lugar de la información de identificador y la contraseña de usuario en la cadena de conexión.  
  
 En el siguiente ejemplo, una aplicación llama **SQLBrowseConnect** repetidamente. Cada vez que **SQLBrowseConnect** devuelve SQL_NEED_DATA, pasa devuelve información acerca de los datos que necesita en \* *OutConnectionString*. Las fases de la aplicación *OutConnectionString* a su rutina **GetUserInput** (no se muestra). **GetUserInput** analiza la información, crea y muestra un cuadro de diálogo y devuelve la información introducida por el usuario en \* *InConnectionString*. La aplicación pasa la información del usuario para el controlador en la siguiente llamada a **SQLBrowseConnect**. Después de que la aplicación ha proporcionado toda la información necesaria para conectarse al origen de datos, el controlador **SQLBrowseConnect** devuelve SQL_SUCCESS y la aplicación continúa.  
  
 Para obtener un ejemplo más detallado de conectarse a un controlador de SQL Server mediante una llamada a **SQLBrowseConnect**, consulte [ejemplo de exploración de SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Por ejemplo, para conectarse a los datos de ventas de origen, podrían aparecer las siguientes acciones. En primer lugar, la aplicación pasa la cadena siguiente para **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 El Administrador de controladores se carga el controlador asociado con el origen de datos Sales. A continuación, llama el controlador **SQLBrowseConnect** función con los mismos argumentos que recibió de la aplicación. El controlador devuelve la cadena siguiente en **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 La aplicación pasa esta cadena a su **GetUserInput** rutinarias, que genera un cuadro de diálogo que pide al usuario seleccionar el servidor de rojo, azul o verde y para especificar un Id. de usuario y una contraseña. Las fases de rutina de la siguiente información especificada por el usuario nuevo en \* *InConnectionString*, que la aplicación pasa a **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** usa esta información para conectarse al servidor de red como Smith con la forma de sésamo de contraseña y, a continuación, devuelve la cadena siguiente en **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 La aplicación pasa esta cadena a su **GetUserInput** rutinarias, que genera un cuadro de diálogo que pide al usuario que seleccione una base de datos. El empdata de instrucciones SELECT del usuario y la aplicación llama **SQLBrowseConnect** una hora final con esta cadena:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Este es el último fragmento de información que el controlador necesita para conectarse al origen de datos; **SQLBrowseConnect** devuelve SQL_SUCCESS, y **OutConnectionString* contiene la cadena de conexión completada:  
  
```  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador de conexión|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Desconectarse de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectarse a un origen de datos mediante un cuadro de diálogo o la cadena de conexión|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Devuelve la descripción de los controladores y atributos|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberar un identificador de conexión|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
