---
title: "SQLConnect, función | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLConnect
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLConnect
helpviewer_keywords: SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
caps.latest.revision: "37"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9f2c2d3e8b60d0a73d1beba4f68148cd956431b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlconnect-function"></a>Función SQLConnect
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLConnect** establece conexiones con un controlador y un origen de datos. El identificador de conexión hace referencia a almacenamiento de toda la información acerca de la conexión al origen de datos, incluido el estado, el estado de la transacción y la información de error.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 *IdentificadorConexión*  
 [Entrada] Identificador de conexión.  
  
 *ServerName*  
 [Entrada] Nombre de origen de datos. Los datos podrían ser ubicados en el mismo equipo que el programa o en otro equipo en algún punto de una red. Para obtener información acerca de cómo una aplicación elige un origen de datos, vea [elegir un origen de datos o el controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Entrada] Longitud de **ServerName* en caracteres.  
  
 *UserName*  
 [Entrada] Identificador de usuario.  
  
 *NameLength2*  
 [Entrada] Longitud de **nombre de usuario* en caracteres.  
  
 *Autenticación*  
 [Entrada] Cadena de autenticación (normalmente la contraseña).  
  
 *NameLength3*  
 [Entrada] Longitud de **autenticación* en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLConnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DBC y un *controlar* de *IdentificadorConexión*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLConnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|El controlador no admitía el valor especificado de la *ValuePtr* argumento en **SQLSetConnectAttr** y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08001|No se puede establecer la conexión de cliente|El controlador no pudo establecer una conexión con el origen de datos.|  
|08002|Nombre de la conexión en uso|(DM) especificado *IdentificadorConexión* ya hubiese utilizado para establecer una conexión con un origen de datos y la conexión todavía estaba abierto o el usuario lo estaba examinando para una conexión.|  
|08004|Servidor rechazó la conexión|El origen de datos rechazó el establecimiento de la conexión por motivos de definido por la implementación.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos a la que estaba intentando conectar el controlador no pudo antes del procesamiento de la función se ha completado.|  
|28000|Especificación de autorización no válido|El valor especificado para el argumento *nombre de usuario* o el valor especificado para el argumento *autenticación* infringió las restricciones definidas por el origen de datos.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El Administrador de controladores (DM) no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *IdentificadorConexión*. El **SQLConnect** se llamó a función y antes que completó la ejecución, [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en la *IdentificadorConexión*y, a continuación, el **SQLConnect** función llamó de nuevo en el *IdentificadorConexión*.<br /><br /> O bien, el **SQLConnect** se llamó a función y antes que completó la ejecución, **SQLCancelHandle** se llamó en la *IdentificadorConexión* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *IdentificadorConexión* y aún se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *NameLength1*, *NameLength2*, o *NameLength3* era menor que 0, pero no es igual a SQL_NTS.<br /><br /> (DM) el valor especificado para el argumento *NameLength1* superó la longitud máxima para un nombre de origen de datos.|  
|HYT00|Se agotó el tiempo de espera|Ha caducado el período de tiempo de espera de consulta antes de la conexión al origen de datos completado. El período de tiempo de espera se establece a través de **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Controlador no admite la ejecución de la función asincrónica de nivel de conexión|(DM) la aplicación habilitada la operación asincrónica en el identificador de conexión antes de realizar la conexión. Sin embargo, el controlador no admite las operaciones asincrónicas en el identificador de conexión.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador especificado por el nombre de origen de datos no admite la función.|  
|IM002|No se encontró el origen de datos y se especificó ningún controlador predeterminado|Nombre especificado en el argumento del origen de datos (DM) *ServerName* no se encontró en la información del sistema, así como tampoco había una especificación de controlador de forma predeterminada.|  
|IM003|Controlador especificado no se pudo conectar a|El controlador de (DM) aparece en los datos de especificación del origen de información del sistema no se encontró o no se pudo conectar a por algún otro motivo.|  
|IM004|Error de SQLAllocHandle del controlador en SQL_HANDLE_ENV|(DM) durante la **SQLConnect**, el Administrador de controladores denominado el controlador **SQLAllocHandle** funcionando con un *HandleType* de SQL_HANDLE_ENV y el controlador ha devuelto un error.|  
|IM005|Error de SQLAllocHandle del controlador en SQL_HANDLE_DBC|(DM) durante la **SQLConnect**, el Administrador de controladores denominado el controlador **SQLAllocHandle** funcionando con un *HandleType* de SQL_HANDLE_DBC y el controlador ha devuelto un error.|  
|IM006|Error de SQLSetConnectAttr del controlador|Durante la **SQLConnect**, el Administrador de controladores denominado el controlador **SQLSetConnectAttr** función y el controlador ha devuelto un error. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|IM009|No puede conectarse al archivo DLL de traducción|El controlador no pudo conectarse a la DLL que se especificó para el origen de datos de traducción.|  
|IM010|Nombre del origen de datos es demasiado largo|(DM)  *\*ServerName* tenía más de SQL_MAX_DSN_LENGTH caracteres.|  
|IM014|El DSN especificado contiene un error de coincidencia de arquitectura entre el controlador y la aplicación|Aplicación de 32 bits (DM) usa un DSN que se conecta a un controlador de 64 bits; o viceversa.|  
|IM015|Error SQLConnect del controlador en SQL_HANDLE_DBC_INFO_HANDLE|Si un controlador devuelve SQL_ERROR, el Administrador de controladores devolverá SQL_ERROR a la aplicación y se producirá un error en la conexión.<br /><br /> Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
|S1118|Controlador no admite la notificación asincrónica|Cuando el controlador no admite la notificación asincrónica, no se puede establecer SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información acerca de por qué se usa una aplicación **SQLConnect**, consulte [conexión con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 El Administrador de controladores no se conecta a un controlador hasta que la aplicación llama a una función (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**) para conectarse a la controlador. Hasta ese momento, el Administrador de controladores funciona con sus propios controladores y administra información de conexión. Cuando la aplicación llama a una función de conexión, el Administrador de controladores comprueba si un controlador está conectado actualmente a para el elemento especificado *IdentificadorConexión*:  
  
-   Si un controlador no está conectado a, el Administrador de controladores se conecta a los controladores y las llamadas **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV, **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC, **SQLSetConnectAttr** (si la aplicación especifica los atributos de conexión) y la función de conexión en el controlador. El Administrador de controladores devuelve SQLSTATE IM006 (del controlador **SQLSetConnectOption** error) y SQL_SUCCESS_WITH_INFO para la función de conexión si el controlador devuelve un error para **SQLSetConnectAttr**. Para obtener más información, consulte [conectarse a un origen de datos o el controlador](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Si el controlador especificado ya está conectado a en el *IdentificadorConexión*, el Administrador de controladores llama a la función de conexión en el controlador. En este caso, el controlador debe asegurarse de que la conexión de todos los atributos para el *IdentificadorConexión* conserven su configuración actual.  
  
-   Si un controlador diferente se conecta a, el Administrador de controladores llama **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC, y, a continuación, si ningún otro controlador se conecta a en el entorno, llama a **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV en el controlador conectado y, a continuación, desconectará a ese controlador. A continuación, realiza las mismas operaciones que cuando un controlador no está conectado a.  
  
 El controlador, a continuación, asigna identificadores e inicializa propio.  
  
 Cuando la aplicación llama **SQLDisconnect**, las llamadas de administrador de controladores **SQLDisconnect** en el controlador. Sin embargo, no desconecta el controlador. Esto evita que el controlador en la memoria para las aplicaciones que se conectan a varias veces y desconectarse de un origen de datos. Cuando la aplicación llama **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_DBC, el Administrador de controladores llama **SQLFreeHandle** con un *HandleType*  de SQL_HANDLE_DBC y, a continuación, **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_ENV en el controlador y, a continuación, se desconecta el controlador.  
  
 Una aplicación ODBC puede establecer más de una conexión.  
  
## <a name="driver-manager-guidelines"></a>Instrucciones de administrador de controladores  
 El contenido de **ServerName* afectan a cómo funcionan conjuntamente el Administrador de controladores y un controlador para establecer una conexión con un origen de datos.  
  
-   Si \* *ServerName* contiene un nombre de origen de datos válido, el Administrador de controladores busca la especificación de origen de datos correspondiente en la información del sistema y se conecta a los controladores asociados. El Administrador de controladores pasa cada **SQLConnect** argumento para el controlador.  
  
-   Si no se encuentra el nombre de origen de datos o *ServerName* es un puntero nulo, el Administrador de controladores busca la especificación del origen de datos predeterminado y se conecta con el controlador asociado. El Administrador de controladores que se pasa al controlador de la *nombre de usuario* y *autenticación* argumentos sin modificar y "DEFAULT" para el *ServerName* argumento.  
  
-   Si el *ServerName* argumento es "DEFAULT", el Administrador de controladores busca la especificación del origen de datos predeterminado y se conecta con el controlador asociado. El Administrador de controladores pasa cada **SQLConnect** argumento para el controlador.  
  
-   Si no se encuentra el nombre de origen de datos o *ServerName* es un puntero nulo y el valor predeterminado no existe la especificación de origen de datos, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE IM002 (origen de datos no se encontró el nombre y no tiene valor predeterminado controlador especificado).  
  
 Después de que está conectado a por el Administrador de controladores, un controlador puede localizar su especificación de origen de datos correspondiente en la información del sistema y utilizar información específica del controlador de la especificación para completar su conjunto de información de conexión necesaria.  
  
 Si una biblioteca de traducción predeterminado se especifica en la información del sistema para el origen de datos, el controlador se conecta a él. Se puede conectar a una biblioteca de traducción diferente mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_LIB. Una opción de traducción puede especificarse mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Si un controlador es compatible con **SQLConnect**, la sección de la palabra clave de controlador de la información del sistema para el controlador debe contener el **ConnectFunctions** palabra clave con el primer carácter establecido en "Y".  
  
### <a name="connection-pooling"></a>Agrupar conexiones  
 Agrupación de conexiones permite a reutilizar una conexión que ya se ha creado una aplicación. Cuando está habilitada la agrupación de conexiones y **SQLConnect** se llama, el Administrador de controladores intentará realizar la conexión utilizando una conexión que forma parte de un grupo de conexiones en un entorno que se han designado para la agrupación de conexiones. Este entorno es un entorno compartido utilizado por todas las aplicaciones que usan las conexiones en el grupo.  
  
 Agrupación de conexiones está habilitada antes de que el entorno se asigna mediante una llamada a **SQLSetEnvAttr** para establecer SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER (que especifica un máximo de un grupo por controlador) o SQL_CP_ONE_PER_HENV (que especifica un máximo de un grupo por cada entorno). **SQLSetEnvAttr** en este caso, se llama con *EnvironmentHandle* establecido en null, lo que hace que el atributo de un atributo de nivel de proceso. Si SQL_ATTR_CONNECTION_POOLING se establece en SQL_CP_OFF, se deshabilita la agrupación de conexiones.  
  
 Después de que se ha habilitado la agrupación de conexiones, **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se llama para asignar un entorno. El entorno asignado por esta llamada es un entorno compartido, porque se ha habilitado la agrupación de conexiones. Sin embargo, no se determina el entorno que se utilizará hasta que **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se denomina.  
  
 **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llama para asignar una conexión. El Administrador de controladores intenta encontrar un entorno compartido existente que coincida con los atributos de entorno establecidos por la aplicación. Si no existe ningún entorno de este tipo, se crea uno como implícita *entorno compartido*. Si se encuentra un entorno compartido coincidente, se devuelve el identificador de entorno a la aplicación y su recuento de referencias se incrementa.  
  
 Sin embargo, no se determina la conexión que se utilizará hasta que **SQLConnect** se llama. En ese momento, el Administrador de controladores intenta buscar una conexión existente en la agrupación de conexiones que coincide con los criterios solicitados por la aplicación. Estos criterios incluyen las opciones de conexión solicitadas en la llamada a **SQLConnect** (los valores de la *ServerName*, *nombre de usuario*, y  *Autenticación* palabras clave) y los atributos de conexión establecen ya que **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC se llamó. El Administrador de controladores comprueba estos criterios frente a palabras clave de conexión correspondiente y los atributos de las conexiones en el grupo. Si se encuentra una coincidencia, se utiliza la conexión en el grupo. Si se encuentra ninguna coincidencia, se crea una nueva conexión.  
  
 Si el atributo de entorno SQL_ATTR_CP_MATCH se establece en SQL_CP_STRICT_MATCH, la coincidencia debe ser exacta de una conexión en el grupo que se usará. Si el atributo de entorno SQL_ATTR_CP_MATCH se establece en SQL_CP_RELAXED_MATCH, opciones de la conexión de la llamada a **SQLConnect** deben coincidir pero no todos los atributos de conexión debe coincidir con.  
  
 Las reglas siguientes se aplican cuando un atributo de conexión, según lo establecido por la aplicación antes de **SQLConnect** se llama, no coincide con el atributo de conexión de la conexión en el grupo:  
  
-   Si el atributo de conexión debe establecerse antes de que se realiza la conexión:  
  
     Si SQL_ATTR_CP_MATCH es SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE en la conexión agrupada debe ser idéntico al atributo establecido por la aplicación. Si SQL_CP_RELAXED_MATCH, los valores de SQL_ATTR_PACKET_SIZE puede ser diferente.  
  
     El valor de SQL_ATTR_LOGIN_VALUE no afecta a la búsqueda de coincidencias.  
  
-   Si el atributo de conexión se puede establecer antes o después de la conexión se realiza:  
  
     Si el atributo de conexión no se ha establecido por la aplicación pero se ha establecido en la conexión en el grupo y no hay valor predeterminado, el atributo de conexión en la conexión agrupada se vuelve a establecer en el valor predeterminado y se declara una coincidencia. Si no hay ningún valor predeterminado, la conexión agrupada no se considera a una coincidencia.  
  
     Si el atributo de conexión se ha establecido por la aplicación, pero no se ha establecido en la conexión en el grupo, se cambia el atributo de conexión en el grupo a ese conjunto de la aplicación y se declara una coincidencia.  
  
     Si el atributo de conexión se ha establecido por la aplicación y también se ha establecido en la conexión en el grupo, pero los valores son distintos, se utiliza el valor del atributo de conexión de la aplicación y se declara una coincidencia.  
  
-   Si los valores de atributos de conexión específicos del controlador no son idénticos y SQL_ATTR_CP_MATCH se establece en SQL_CP_STRICT_MATCH, no se utiliza la conexión en el grupo.  
  
 Cuando la aplicación llama **SQLDisconnect** para desconectar, la conexión se devuelve al grupo de conexiones y está disponible para su reutilización.  
  
### <a name="optimizing-connection-pooling-performance"></a>Optimizar el rendimiento de la agrupación de conexiones  
 Cuando se trate de transacciones distribuidas, es posible optimizar el rendimiento mediante el uso de la agrupación de conexiones **SQL_DTC_TRANSITION_COST**, que es una máscara de bits SQLUINTEGER. Las transiciones mencionadas son las transiciones del atributo de conexión SQL_ATTR_ENLIST_IN_DTC van desde el valor 0 a distinto de cero y viceversa. Se trata de una conexión van desde no da de alta en una transacción distribuida dada de alta en una transacción distribuida y viceversa. Dependiendo de cómo el controlador ha implementado la inscripción (atributo de conexión de configuración SQL_ATTR_ENLIST_IN_DTC), estas transiciones pueden ser costosas y deberían evitarse, por lo tanto, para mejorar el rendimiento.  
  
 El valor devuelto por el controlador contiene cualquier combinación de los bits siguientes:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, cuando establece, implica el cero para realizar la transición es distinto de cero es mucho más cara que una transición de es distinto de cero a otro valor distinto de cero (dar de alta una conexión previamente dada de alta en la transacción siguiente).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, cuando establece, implica la distinto de cero a cero transición es mucho más cara que mediante una conexión cuyo atributo SQL_ATTR_ENLIST_IN_DTC ya está establecido en cero.  
  
 Hay un rendimiento frente a Equilibrio de uso de conexión. Si un controlador indica que una o varias de estas transiciones son costosas, agrupador de conexiones del Administrador de controladores responde a este manteniendo más conexiones en el grupo. Algunas de las conexiones en el grupo se prefieren para su uso no transaccional y algunos son preferibles para su uso transaccional. Sin embargo, si el controlador indica que no sean costosas estas transiciones, menos conexiones pueden utilizarse, alternando quizás no transaccional y el uso transaccional.  
  
 Controladores que no admiten SQL_ATTR_ENLIST_IN_DTC no es necesario admitir SQL_DTC_TRANSITION_COST. Para los controladores que admiten SQL_ATTR_ENLIST_IN_DTC pero no SQL_DTC_TRANSITION_COST, se supone que las transiciones no son costosas, como si el controlador devuelve 0 (ningún conjunto de bits) para este valor.  
  
 Aunque SQL_DTC_TRANSITION_COST se introdujo en ODBC 3.5, una API ODBC 2. *x* controlador también admitirá, porque el Administrador de controladores consultará esta información independientemente de la versión del controlador.  
  
### <a name="code-example"></a>Ejemplo de código  
 En el siguiente ejemplo, una aplicación asigna conexión y entorno de identificadores. A continuación, se conecta con el origen de datos de pedidos de venta con el JohnS de Id. de usuario y la contraseña de la forma de sésamo y procesa los datos. Cuando ha finalizado el procesamiento de datos, se desconecta del origen de datos y libera los identificadores.  
  
```  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Detectar y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Desconectarse de un origen de datos|[Función SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Conectarse a un origen de datos mediante un cuadro de diálogo o la cadena de conexión|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Devolver el valor de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
