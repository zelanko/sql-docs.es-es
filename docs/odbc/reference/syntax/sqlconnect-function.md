---
title: Función SQLConnect (SQLConnect) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab0a31845efeb484c554a9c9cf1afeaeab1a8bea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301221"
---
# <a name="sqlconnect-function"></a>Función SQLConnect
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLConnect** establece conexiones con un controlador y un origen de datos. El identificador de conexión hace referencia al almacenamiento de toda la información sobre la conexión al origen de datos, incluido el estado, el estado de la transacción y la información de error.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *nombreDeServidor*  
 [Entrada] Nombre del origen de datos. Los datos pueden estar ubicados en el mismo equipo que el programa, o en otro equipo en algún lugar de una red. Para obtener información sobre cómo una aplicación elige un origen de datos, vea Elegir un origen de [datos o un controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Longitud de **ServerName* en caracteres.  
  
 *nombre de usuario*  
 [Entrada] Identificador de usuario.  
  
 *NameLength2*  
 [Entrada] Longitud de **UserName* en caracteres.  
  
 *Autenticación*  
 [Entrada] Cadena de autenticación (normalmente la contraseña).  
  
 *NameLength3*  
 [Entrada] Longitud de **Autenticación* en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLConnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *control* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|El controlador no admitía el valor especificado del argumento *ValuePtr* en **SQLSetConnectAttr** y sustituyó un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08001|Cliente incapaz de establecer conexión|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de conexión en uso|(DM) El *ConnectionHandle* especificado ya se había utilizado para establecer una conexión con un origen de datos, y la conexión seguía abierta o el usuario estaba buscando una conexión.|  
|08004|El servidor rechazó la conexión|El origen de datos rechazó el establecimiento de la conexión por razones definidas por la implementación.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que el controlador intentaba conectarse antes de que la función completara el procesamiento.|  
|28000|Especificación de autorización no válida|Valor especificado para el argumento *UserName* o el valor especificado para el argumento *Authentication* infringió las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|(DM) El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *ConnectionHandle*. Se llamó a la función **SQLConnect** y, antes de completar la ejecución, se llamó a [la función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) en *ConnectionHandle*y, a continuación, se llamó de nuevo a la función **SQLConnect** en *ConnectionHandle*.<br /><br /> O bien, se llamó a la función **SQLConnect** y, antes de completar la ejecución, **sqlCancelHandle** se llamó en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica (no esta) para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *NameLength1*, *NameLength2*o *NameLength3* era menor que 0 pero no igual que SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *NameLength1* superó la longitud máxima de un nombre de origen de datos.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que se completara la conexión con el origen de datos. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|El controlador no admite la ejecución de funciones asincrónicas de nivel de conexión|(DM) La aplicación habilitó la operación asincrónica en el identificador de conexión antes de realizar la conexión. Sin embargo, el controlador no admite operaciones asincrónicas en el identificador de conexión.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador especificado por el nombre del origen de datos no admite la función.|  
|IM002|Origen de datos no encontrado y no se especificó ningún controlador predeterminado|(DM) El nombre del origen de datos especificado en el argumento *ServerName* no se encontró en la información del sistema, ni había una especificación de controlador predeterminada.|  
|IM003|El controlador especificado no se pudo conectar a|(DM) El controlador que aparece en la especificación del origen de datos en la información del sistema no se encontró o no se pudo conectar por alguna otra razón.|  
|IM004|Error del controlador SQLAllocHandle en SQL_HANDLE_ENV|(DM) Durante **SQLConnect**, el Administrador de controladores llamó a la función **SQLAllocHandle** del controlador con un *HandleType* de SQL_HANDLE_ENV y el controlador devolvió un error.|  
|IM005|SqlAllocHandle del controlador en SQL_HANDLE_DBC error|(DM) Durante **SQLConnect**, el Administrador de controladores llamó a la función **SQLAllocHandle** del controlador con un *HandleType* de SQL_HANDLE_DBC y el controlador devolvió un error.|  
|IM006|Error del controlador SQLSetConnectAttr|Durante **SQLConnect**, el Administrador de controladores llamó a la función **SQLSetConnectAttr** del controlador y el controlador devolvió un error. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|IM009|No se puede conectar a DLL de traducción|El controlador no pudo conectarse al archivo DLL de traducción que se especificó para el origen de datos.|  
|IM010|Nombre del origen de datos demasiado largo|(DM) * \*ServerName* era más largo que SQL_MAX_DSN_LENGTH caracteres.|  
|IM014|El DSN especificado contiene una discordancia de arquitectura entre el controlador y la aplicación|(DM) aplicación de 32 bits utiliza un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM015|Error en SQLConnect del controlador en SQL_HANDLE_DBC_INFO_HANDLE|Si un controlador devuelve SQL_ERROR, el Administrador de controladores devolverá SQL_ERROR a la aplicación y se producirá un error en la conexión.<br /><br /> Para obtener más información acerca de SQL_HANDLE_DBC_INFO_TOKEN, vea Desarrollar el reconocimiento de grupos [de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
|S1118|El controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT ni SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información sobre por qué una aplicación utiliza **SQLConnect**, consulte [Conexión con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 El Administrador de controladores no se conecta a un controlador hasta que la aplicación llama a una función (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**) para conectarse al controlador. Hasta ese momento, el Administrador de controladores funciona con sus propios identificadores y administra la información de conexión. Cuando la aplicación llama a una función de conexión, el Administrador de controladores comprueba si un controlador está conectado actualmente para el *ConnectionHandle*especificado:  
  
-   Si un controlador no está conectado a, el Administrador de controladores se conecta al controlador y llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV, **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC, **SQLSetConnectAttr** (si la aplicación especificó atributos de conexión) y la función de conexión en el controlador. El Administrador de controladores devuelve SQLSTATE IM006 (error del controlador **SQLSetConnectOption)** y SQL_SUCCESS_WITH_INFO para la función de conexión si el controlador devuelve un error para **SQLSetConnectAttr**. Para obtener más información, consulte [Conexión a un origen](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)de datos o controlador .  
  
-   Si el controlador especificado ya está conectado en *ConnectionHandle*, el Administrador de controladores llama solo a la función de conexión en el controlador. En este caso, el controlador debe asegurarse de que todos los atributos de conexión para *ConnectionHandle* mantienen su configuración actual.  
  
-   Si se conecta un controlador diferente, el Administrador de controladores llama a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC y, a continuación, si no hay ningún otro controlador conectado en ese entorno, llama a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV en el controlador conectado y, a continuación, desconecta ese controlador. A continuación, realiza las mismas operaciones que cuando un controlador no está conectado.  
  
 A continuación, el controlador asigna identificadores e inicializase a sí mismo.  
  
 Cuando la aplicación llama a **SQLDisconnect**, el Administrador de controladores llama a **SQLDisconnect** en el controlador. Sin embargo, no desconecta el controlador. Esto mantiene el controlador en la memoria para las aplicaciones que se conectan y se desconectan repetidamente de un origen de datos. Cuando la aplicación llama **a SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC, el Administrador de controladores llama **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC y, a continuación, **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV en el controlador y, a continuación, desconecta el controlador.  
  
 Una aplicación ODBC puede establecer más de una conexión.  
  
## <a name="driver-manager-guidelines"></a>Pautas del administrador del conductor  
 El contenido de **ServerName* afecta a cómo el Administrador de controladores y un controlador trabajan juntos para establecer una conexión a un origen de datos.  
  
-   Si \* *ServerName* contiene un nombre de origen de datos válido, el Administrador de controladores busca la especificación de origen de datos correspondiente en la información del sistema y se conecta al controlador asociado. El Administrador de controladores pasa cada **argumento SQLConnect** al controlador.  
  
-   Si no se encuentra el nombre del origen de datos o *ServerName* es un puntero nulo, el Administrador de controladores busca la especificación de origen de datos predeterminada y se conecta al controlador asociado. El Administrador de controladores pasa al controlador los argumentos *UserName* y *Authentication* sin modificar y "DEFAULT" para el argumento *ServerName.*  
  
-   Si el *argumento ServerName* es "DEFAULT", el Administrador de controladores busca la especificación de origen de datos predeterminada y se conecta al controlador asociado. El Administrador de controladores pasa cada **argumento SQLConnect** al controlador.  
  
-   Si no se encuentra el nombre del origen de datos o *ServerName* es un puntero nulo y no existe la especificación de origen de datos predeterminada, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE IM002 (no se encuentra el nombre del origen de datos y no se especifica ningún controlador predeterminado).  
  
 Después de que el Administrador de controladores lo conecte, un controlador puede localizar su especificación de origen de datos correspondiente en la información del sistema y utilizar información específica del controlador de la especificación para completar su conjunto de información de conexión necesaria.  
  
 Si se especifica una biblioteca de traducción predeterminada en la información del sistema para el origen de datos, el controlador se conecta a ella. Se puede conectar una biblioteca de traducción diferente llamando a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_LIB. Se puede especificar una opción de traducción llamando a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Si un controlador admite **SQLConnect**, la sección de palabra clave del controlador de la información del sistema para el controlador debe contener la palabra clave **ConnectFunctions** con el primer conjunto de caracteres en "Y."  
  
### <a name="connection-pooling"></a>Agrupar conexiones  
 La agrupación de conexiones permite a una aplicación reutilizar una conexión que ya se ha creado. Cuando se habilita la agrupación de conexiones y se llama a **SQLConnect,** el Administrador de controladores intenta realizar la conexión mediante una conexión que forma parte de un grupo de conexiones en un entorno que se ha designado para la agrupación de conexiones. Este entorno es un entorno compartido que usan todas las aplicaciones que usan las conexiones del grupo.  
  
 La agrupación de conexiones está habilitada antes de que se asigne el entorno llamando a **SQLSetEnvAttr** para establecer SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER (que especifica un máximo de un grupo por controlador) o SQL_CP_ONE_PER_HENV (que especifica un máximo de un grupo por entorno). **SQLSetEnvAttr** en este caso se llama con *EnvironmentHandle* establecido en null, lo que convierte el atributo en un atributo de nivel de proceso. Si SQL_ATTR_CONNECTION_POOLING se establece en SQL_CP_OFF, la agrupación de conexiones está deshabilitada.  
  
 Una vez habilitada la agrupación de conexiones, **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se llama para asignar un entorno. El entorno asignado por esta llamada es un entorno compartido porque se ha habilitado la agrupación de conexiones. Sin embargo, el entorno que se usará no se determina hasta **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama.  
  
 **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama para asignar una conexión. El Administrador de controladores intenta encontrar un entorno compartido existente que coincida con los atributos de entorno establecidos por la aplicación. Si no existe tal entorno, se crea uno como un *entorno compartido*implícito. Si se encuentra un entorno compartido coincidente, el identificador de entorno se devuelve a la aplicación y se incrementa su recuento de referencias.  
  
 Sin embargo, la conexión que se usará no se determina hasta que se llama a **SQLConnect.** En ese momento, el Administrador de controladores intenta encontrar una conexión existente en el grupo de conexiones que coincida con los criterios solicitados por la aplicación. Estos criterios incluyen las opciones de conexión solicitadas en la llamada a **SQLConnect** (los valores de las palabras clave *ServerName*, *UserName*y *Authentication)* y los atributos de conexión establecidos desde **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llamó. El Administrador de controladores comprueba estos criterios con respecto a las palabras clave y atributos de conexión correspondientes en las conexiones del grupo. Si se encuentra una coincidencia, se utiliza la conexión en el grupo. Si no se encuentra ninguna coincidencia, se crea una nueva conexión.  
  
 Si el atributo de entorno SQL_ATTR_CP_MATCH se establece en SQL_CP_STRICT_MATCH, la coincidencia debe ser exacta para que se utilice una conexión en el grupo. Si el atributo de entorno SQL_ATTR_CP_MATCH se establece en SQL_CP_RELAXED_MATCH, las opciones de conexión de la llamada a **SQLConnect** deben coincidir, pero no todos los atributos de conexión deben coincidir.  
  
 Las reglas siguientes se aplican cuando un atributo de conexión, según lo establecido por la aplicación antes de llamar a **SQLConnect,** no coincide con el atributo de conexión de la conexión en el grupo:  
  
-   Si el atributo de conexión debe establecerse antes de realizar la conexión:  
  
     Si SQL_ATTR_CP_MATCH es SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE de la conexión agrupada debe ser idéntica al atributo establecido por la aplicación. Si SQL_CP_RELAXED_MATCH, los valores de SQL_ATTR_PACKET_SIZE pueden ser diferentes.  
  
     El valor de SQL_ATTR_LOGIN_VALUE no afecta a la coincidencia.  
  
-   Si el atributo de conexión se puede establecer antes o después de realizar la conexión:  
  
     Si la aplicación no ha establecido el atributo de conexión pero se ha establecido en la conexión del grupo y hay un valor predeterminado, el atributo de conexión en la conexión agrupada se establece de nuevo en el valor predeterminado y se declara una coincidencia. Si no hay ningún valor predeterminado, la conexión agrupada no se considera una coincidencia.  
  
     Si la aplicación ha establecido el atributo de conexión pero no se ha establecido en la conexión del grupo, el atributo de conexión del grupo se cambia al establecido por la aplicación y se declara una coincidencia.  
  
     Si la aplicación ha establecido el atributo de conexión y también se ha establecido en la conexión del grupo, pero los valores son diferentes, se utiliza el valor del atributo de conexión de la aplicación y se declara una coincidencia.  
  
-   Si los valores de los atributos de conexión específicos del controlador no son idénticos y SQL_ATTR_CP_MATCH se establece en SQL_CP_STRICT_MATCH, no se utiliza la conexión en el grupo.  
  
 Cuando la aplicación llama a **SQLDisconnect** para desconectarse, la conexión se devuelve al grupo de conexiones y está disponible para su reutilización.  
  
### <a name="optimizing-connection-pooling-performance"></a>Optimización del rendimiento de la agrupación de conexiones  
 Cuando se trata de transacciones distribuidas, es posible optimizar el rendimiento de agrupación de conexiones mediante **SQL_DTC_TRANSITION_COST**, que es una máscara de bits SQLUINTEGER. Las transiciones a las que se hace referencia son las transiciones del atributo de conexión SQL_ATTR_ENLIST_IN_DTC pasar del valor 0 a distinto de cero y viceversa. Se trata de una conexión que pasa de no dar de alta en una transacción distribuida a dar de alta en una transacción distribuida y viceversa. Dependiendo de cómo el controlador ha implementado la inscripción (establecer el atributo de conexión SQL_ATTR_ENLIST_IN_DTC), estas transiciones pueden ser costosas y, por lo tanto, deben evitarse para obtener el mejor rendimiento.  
  
 El valor devuelto por el controlador contiene cualquier combinación de los siguientes bits:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, cuando se establece, implica que la transición de cero a distinto de cero es significativamente más costosa que una transición de distinto a cero a otro valor distinto de cero (dar de alta una conexión previamente inscrita en su siguiente transacción).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, cuando se establece, implica que la transición de cero a cero es significativamente más caro que usar una conexión cuyo atributo SQL_ATTR_ENLIST_IN_DTC ya está establecido en cero.  
  
 Hay una compensación de uso de rendimiento frente a conexión. Si un controlador indica que una o varias de estas transiciones son costosas, el agrupador de conexiones del administrador de controladores responde a esto manteniendo más conexiones en el grupo. Algunas de las conexiones del grupo se prefieren para uso no transaccional y otras para uso transaccional. Sin embargo, si el controlador indica que estas transiciones no son costosas, se pueden utilizar menos conexiones, tal vez alternando entre el uso no transaccional y transaccional.  
  
 Los controladores que no admiten SQL_ATTR_ENLIST_IN_DTC no necesitan admitir SQL_DTC_TRANSITION_COST. Para los controladores que admiten SQL_ATTR_ENLIST_IN_DTC pero no SQL_DTC_TRANSITION_COST, se supone que las transiciones no son costosas, como si el controlador devolviera 0 (sin bits establecidos) para este valor.  
  
 Aunque SQL_DTC_TRANSITION_COST se introdujo en ODBC 3.5, un ODBC 2. *x* controlador también puede admitirlo porque el administrador de controladores consultará esta información independientemente de la versión del controlador.  
  
### <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación asigna identificadores de entorno y conexión. A continuación, se conecta al origen de datos SalesOrders con el ID de usuario JohnS y la contraseña Sesame y procesa los datos. Cuando ha terminado de procesar los datos, se desconecta del origen de datos y libera los identificadores.  
  
```cpp  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
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
  
### <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Descubrir y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Desconectarse de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conexión a un origen de datos mediante una cadena de conexión o un cuadro de diálogo|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Devolver la configuración de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
