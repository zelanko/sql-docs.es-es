---
title: Función SQLGetDiagField | Documentos de Microsoft
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
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ae1a58454a7ce70f5ae2a33d951a769223fdd1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922800"
---
# <a name="sqlgetdiagfield-function"></a>Función SQLGetDiagField
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLGetDiagField** devuelve el valor actual de un campo de un registro de la estructura de datos de diagnóstico (asociada con un identificador especificado) que contiene el error, advertencia e información de estado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Un identificador de tipo de identificador que describe el tipo de identificador para el que se requieren los diagnósticos. Debe ser una de las siguientes:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN se utiliza únicamente por el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Un identificador para la estructura de datos de diagnóstico, del tipo indicado por *HandleType*. Si *HandleType* es SQL_HANDLE_ENV, *controlar* puede ser compartida o un identificador de entorno no compartido.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de estado desde el que la aplicación busca información. Registros de estado se numeran del 1. Si el *DiagIdentifier* argumento indica cualquier campo del encabezado de diagnóstico, *RecNumber* se omite. De lo contrario, debe ser superior a 0.  
  
 *DiagIdentifier*  
 [Entrada] Indica el campo del diagnóstico cuyo valor es va a devolver. Para obtener más información, consulte la "*DiagIdentifier* argumento" sección "Comentarios".  
  
 *DiagInfoPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la información de diagnóstico. El tipo de datos depende del valor de *DiagIdentifier*. Si *DiagInfoPtr* es de tipo entero, las aplicaciones deben utilizar un búfer de SQLULEN e inicializar el valor en 0 antes de llamar a esta función, como algunos controladores solo puede escribir el menor de 32 bits o de 16 bits de un búfer y dejar el orden superior bits no cambia.  
  
 Si *DiagInfoPtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (sin incluir el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por  *DiagInfoPtr*.  
  
 *BufferLength*  
 [Entrada] Si *DiagIdentifier* es un diagnóstico definida por ODBC y *DiagInfoPtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de \* *DiagInfoPtr* . Si *DiagIdentifier* es un campo definido en ODBC y \* *DiagInfoPtr* es un entero, *BufferLength* se omite. Si el valor de  *\*DiagInfoPtr* es una cadena Unicode (cuando se llama a **SQLGetDiagFieldW**), el *BufferLength* el argumento debe ser un número par.  
  
 Si *DiagIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los valores siguientes:  
  
-   Si *DiagInfoPtr* es un puntero a una cadena de caracteres *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *DiagInfoPtr* es un puntero a un búfer binario, los lugares de la aplicación en el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si *DiagInfoPtr* es un puntero a un valor distinto de una cadena de carácter o cadena binaria, *BufferLength* debería tener el valor SQL_IS_POINTER.  
  
-   Si  *\*DiagInfoPtr* contiene un tipo de datos de longitud fija, *BufferLength* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (sin incluir el número de bytes necesarios para el carácter de terminación null) disponible para devolver en \* *DiagInfoPtr*, para datos de caracteres. Si el número de bytes disponible para devolver es mayor o igual que *BufferLength*, el texto en \* *DiagInfoPtr* se trunca a *BufferLength* menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLGetDiagField** no registra los registros de diagnóstico para sí mismo. Utiliza los siguientes valores devueltos para indicar el resultado de su propio ejecución:  
  
-   SQL_SUCCESS: La función devolvió información de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* era demasiado pequeño para contener el campo de diagnóstico solicitado. Por lo tanto, se truncaron los datos en el campo de diagnóstico. Para determinar que se produjo un truncamiento, la aplicación debe comparar *BufferLength* en el número real de bytes disponibles, que se escribe en **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: El identificador indicado por *HandleType* y *controlar* no es un identificador válido.  
  
-   SQL_ERROR: Producido uno de los siguientes:  
  
    -   *El DiagIdentifier* argumento no es uno de los valores válidos.  
  
    -   *El DiagIdentifier* argumento era SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE o SQL_DIAG_ROW_COUNT, pero *controlar* no era un identificador de instrucción. (El Administrador de controladores devuelve este diagnóstico.)  
  
    -   *El RecNumber* argumento era negativo o 0 cuando *DiagIdentifier* indica un campo de un registro de diagnóstico. *RecNumber* se omite para los campos de encabezado.  
  
    -   El valor solicitado es una cadena de caracteres y *BufferLength* era menor que cero.  
  
    -   Cuando se utiliza la notificación asincrónica, no finalizó la operación asincrónica en el identificador.  
  
-   SQL_NO_DATA: *RecNumber* era mayor que el número de registros de diagnóstico que existían en el identificador especificado en *controlar.* La función también devuelve SQL_NO_DATA para los valores positivos *RecNumber* si no hay ningún registro de diagnóstico para *controlar*.  
  
## <a name="comments"></a>Comentarios  
 Una aplicación suele llamar **SQLGetDiagField** para realizar uno de los tres objetivos:  
  
1.  Para obtener información sobre la advertencia o error específico cuando una llamada de función ha devuelto SQL_ERROR o SQL_SUCCESS_WITH_INFO (o SQL_NEED_DATA para la **SQLBrowseConnect** función).  
  
2.  Para determinar el número de filas del origen de datos que se ven afectados cuando se lleva a cabo operaciones de inserción, eliminación o actualización con una llamada a **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, o **SQLSetPos** (desde el campo de encabezado SQL_DIAG_ROW_COUNT), o para determinar el número de filas que existen en el cursor abierto actual, si el controlador puede proporcionar esta información (desde el Campo de encabezado SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Para determinar qué función se ejecuta mediante una llamada a **SQLExecDirect** o **SQLExecute** (de los campos de encabezado SQL_DIAG_DYNAMIC_FUNCTION y SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Cualquier función ODBC puede registrar registros de diagnóstico de cero o más cada vez que se llama a ese TI, por lo que una aplicación puede llamar a **SQLGetDiagField** después de cualquier llamada a la función ODBC. No hay ningún límite para el número de registros de diagnóstico que se pueden almacenar en cualquier momento. **SQLGetDiagField** recupera sólo la información de diagnóstico más recientemente asociada a la estructura de datos de diagnóstico especificada en la *controlar* argumento. Si la aplicación llama a una función ODBC distinto de **SQLGetDiagField** o **SQLGetDiagRec**, se pierde cualquier información de diagnóstico de una llamada anterior con el mismo identificador.  
  
 Una aplicación puede buscar todos los registros de diagnóstico al incrementar *RecNumber*, siempre y cuando **SQLGetDiagField** devuelve SQL_SUCCESS. El número de registros de estado se indica en el campo de encabezado SQL_DIAG_NUMBER. Las llamadas a **SQLGetDiagField** son destructivos a los campos de encabezado y el registro. La aplicación puede llamar a **SQLGetDiagField** más tarde para recuperar un campo de un registro, como una función que no sea de las funciones de diagnóstico no se ha llamado en el ínterin, que podría registrar registros en el mismo identificador.  
  
 Una aplicación puede llamar a **SQLGetDiagField** para devolver los campos de diagnóstico en cualquier momento, excepto SQL_DIAG_CURSOR_ROW_COUNT o SQL_DIAG_ROW_COUNT, que devuelve SQL_ERROR si *controlar* no es un identificador de instrucción. Si ningún otro campo de diagnóstico no está definido, la llamada a **SQLGetDiagField** devolverá SQL_SUCCESS (siempre y cuando no se encuentra ningún otro diagnóstico) y se devuelve un valor no definido para el campo.  
  
 Para obtener más información, consulte [utilizando SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) y [implementar SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Llamar a una API que no sea el que se está ejecutando de forma asincrónica generará HY010 "Error en la secuencia de función". Sin embargo, no se puede recuperar el registro de error antes de que finalice la operación asincrónica.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador puede tener información de diagnóstico asociada con él. El *HandleType* argumento indica el tipo de control de *controlar*.  
  
 Algunos campos de encabezado y el registro no se puede devolver para el entorno, conexión, instrucción y descriptor de identificadores. Los identificadores para los que un campo no es aplicable se indican en las siguientes secciones "Campos de encabezado" y "Campos de registro".  
  
 Si *HandleType* es SQL_HANDLE_ENV, *controlar* puede ser un identificador de entorno compartido o compartida.  
  
 No hay campos de diagnóstico de encabezado específico del controlador deben estar asociadas a un identificador de entorno.  
  
 Los campos de diagnóstico solo de encabezado que se definen para un identificador de descriptor son SQL_DIAG_NUMBER y SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argumento de DiagIdentifier  
 Este argumento indica el identificador de campo requerido de la estructura de datos de diagnóstico. Si *RecNumber* es mayor que o igual a 1, los datos en el campo describen la información de diagnóstico devuelta por una función. Si *RecNumber* es 0, el campo se encuentra en el encabezado de la estructura de datos de diagnóstico y, por tanto, contiene datos que pertenecen a la llamada de función que devuelve la información de diagnóstico, no a la información específica.  
  
 Controladores pueden definir encabezado específico del controlador y los campos de registro en la estructura de datos de diagnóstico.  
  
 Una aplicación ODBC 3 *.x* aplicación trabajar con una API ODBC 2 *.x* controlador podrá llamar a **SQLGetDiagField** sólo con una *DiagIdentifier* argumento de SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME o SQL_DIAG_SQLSTATE. Todos los demás campos de diagnóstico devolverá SQL_ERROR.  
  
## <a name="header-fields"></a>Campos de encabezado  
 Los campos de encabezado enumerados en la tabla siguiente pueden incluirse en la *DiagIdentifier* argumento.  
  
|DiagIdentifier|Tipo de valor devuelto|Devuelve|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Este campo contiene el número de filas del cursor. Su semántica depende de la **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 y SQL_STATIC_CURSOR_ATTRIBUTES2, lo que indica que los tipos de información recuentos de filas están disponibles para cada tipo de cursor (en los bits SQL_CA2_CRC_EXACT y SQL_CA2_CRC_APPROXIMATE).<br /><br /> El contenido de este campo se define únicamente para los identificadores de instrucciones y sólo después **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se ha llamado. Al llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_CURSOR_ROW_COUNT en que no sea una instrucción identificador devolverá SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Se trata de una cadena que describe la instrucción SQL que ejecuta la función subyacente. (Vea "Valores de los campos de la función dinámica," más adelante en esta sección, determinados valores). El contenido de este campo se define únicamente para los identificadores de instrucciones y solo después de llamar a **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults**. Al llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION en que no sea una instrucción identificador devolverá SQL_ERROR. El valor de este campo se ha definido antes de llamar a **SQLExecute** o **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Se trata de un código numérico que describe la instrucción SQL ejecutada por la función subyacente. (Vea "Valores de la función campos dinámicos," más adelante en esta sección, valor específico). El contenido de este campo se define únicamente para los identificadores de instrucciones y solo después de llamar a **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults**. Al llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION_CODE en que no sea una instrucción identificador devolverá SQL_ERROR. El valor de este campo se ha definido antes de llamar a **SQLExecute** o **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|El número de registros de estado que están disponibles para el identificador especificado.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Código de retorno devuelto por la función. Para obtener una lista de códigos de retorno, vea [códigos de retorno](../../../odbc/reference/develop-app/return-codes-odbc.md). El controlador no tiene que implementar SQL_DIAG_RETURNCODE; siempre se implementa mediante el Administrador de controladores. Si ninguna función se ha llamado todavía en el *controlar*, SQL_SUCCESS se devolverá para SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|El número de filas afectadas por un insert, delete o update realizadas por **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos**. Está definida por el controlador después de un *especificación de cursor* se ha ejecutado. El contenido de este campo se define solo para los identificadores de instrucciones. Al llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_ROW_COUNT en que no sea una instrucción identificador devolverá SQL_ERROR. Los datos de este campo también se devuelven en el *RowCountPtr* argumento de **SQLRowCount**. Los datos de este campo se restablece después de cada llamada de función nondiagnostic, mientras que el recuento de filas devuelto por **SQLRowCount** sigue siendo la misma hasta que la instrucción se vuelve a establecer el estado preparado o asignado.|  
  
## <a name="record-fields"></a>Campos de registro  
 Los campos de registro enumerados en la tabla siguiente pueden incluirse en la *DiagIdentifier* argumento.  
  
|DiagIdentifier|Tipo de valor devuelto|Devuelve|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Una cadena que indica el documento que define la parte de la clase del valor SQLSTATE de este registro. Su valor es "ISO 9075" para todos los SQLSTATE definido por la interfaz de nivel de llamada ISO y Open Group. Para SQLSTATE específicos de ODBC (todos aquellos cuya clase SQLSTATE es "IM"), su valor es "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Si el campo SQL_DIAG_ROW_NUMBER es un número de fila válidas con un conjunto de filas o un conjunto de parámetros, este campo contiene el valor que representa el número de columna del conjunto de resultados o el número de parámetro en el conjunto de parámetros. Los números siempre empiezan en 1; de columna del conjunto de resultados Si este registro de estado pertenece a una columna de marcador, el campo puede ser cero. Parámetro números empiezan en 1. Tiene el valor SQL_NO_COLUMN_NUMBER si el registro de estado no está asociado a un número de columna o parámetro. Si el controlador no puede determinar el número de columna o parámetro que está asociado este registro, este campo tiene el valor SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> El contenido de este campo se define solo para los identificadores de instrucciones.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Una cadena que indica el nombre de la conexión que está relacionado con el registro de diagnóstico. Este campo está definido por el controlador. Para las estructuras de datos de diagnóstico asociadas con el identificador de entorno y diagnósticos que no hacen referencia a las conexiones, este campo es una cadena de longitud cero.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Un mensaje informativo en el error o advertencia. Este campo es con el formato descrito en [mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md). No hay ninguna longitud máxima para el texto del mensaje de diagnóstico.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Un código de error nativo de específico del origen de datos del controlador. Si no hay ningún código de error nativo, el controlador devuelve 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Este campo contiene el número de fila del conjunto de filas, o el número de parámetro en el conjunto de parámetros, que está asociado el registro de estado. Números de fila y parámetro iniciar con 1. Este campo tiene el valor SQL_NO_ROW_NUMBER si este registro de estado no está asociado con un número de fila o un número de parámetro. Si el controlador no puede determinar el número de filas o parámetro que está asociado este registro, este campo tiene el valor SQL_ROW_NUMBER_UNKNOWN.<br /><br /> El contenido de este campo se define solo para los identificadores de instrucciones.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Una cadena que indica el nombre del servidor que está relacionada con el registro de diagnóstico. Es el mismo que el valor devuelto para una llamada a **SQLGetInfo** con la opción SQL_DATA_SOURCE_NAME. Para las estructuras de datos de diagnóstico asociadas con el identificador de entorno y diagnósticos que no hacen referencia a cualquier servidor, este campo es una cadena de longitud cero.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Un código de diagnóstico de SQLSTATE de cinco caracteres. Para obtener más información, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Una cadena con el mismo formato y los valores válidos como SQL_DIAG_CLASS_ORIGIN, que identifica la parte de la definición de la parte de la subclase del código SQLSTATE. El SQLSTATE de ODBC específico para el que se devuelve "ODBC 3.0" es los siguientes:<br /><br /> 01S00, 01S01, 01S02 DE SQLSTATE, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valores de los campos de la función dinámica  
 La tabla siguiente describen los valores de SQL_DIAG_DYNAMIC_FUNCTION y SQL_DIAG_DYNAMIC_FUNCTION_CODE que se aplican a cada tipo de instrucción SQL ejecutada por una llamada a **SQLExecute** o **SQLExecDirect**. El controlador puede agregar valores definidos por el controlador a los que se presentan.  
  
|Instrucción SQL<br /><br /> ejecuta|Valor de<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valor de<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*instrucción ALTER dominio*|"ALTER DOMINIO"|SQL_DIAG_ALTER_DOMAIN|  
|*instrucción ALTER table*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*definición de aserción*|"CREAR ASERCIÓN"|SQL_DIAG_CREATE_ASSERTION|  
|*definición del conjunto de caracteres*|"CREAR EL JUEGO DE CARACTERES"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*definición de intercalación*|"CREAR INTERCALACIÓN"|SQL_DIAG_CREATE_COLLATION|  
|*instrucción Create index*|"CREAR EL ÍNDICE"|SQL_DIAG_CREATE_INDEX|  
|*instrucción CREATE table*|"CREAR TABLA"|SQL_DIAG_CREATE_TABLE|  
|*instrucción Create view*|"CREAR VISTA"|SQL_DIAG_CREATE_VIEW|  
|*especificación de cursor*|"SELECCIONE CURSOR"|SQL_DIAG_SELECT_CURSOR|  
|*posición de instrucción de eliminación*|"ELIMINACIÓN DINÁMICA CURSOR"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*busca en la instrucción de eliminación*|"DELETE WHERE"|SQL_DIAG_DELETE_WHERE|  
n-definición *|"CREAR EL DOMINIO"|SQL_DIAG_CREATE_DOMAIN|  
|*instrucción de aserción de colocación*|"ASERCIÓN COLOCAR"|SQL_DIAG_DROP_ASSERTION|  
|*Colocar-carácter-set-stmt*|"JUEGO DE CARACTERES DE COLOCAR"|SQL_DIAG_DROP_CHARACTER_SET|  
|*instrucción de intercalación DROP*|"INTERCALACIÓN COLOCAR"|SQL_DIAG_DROP_COLLATION|  
|*instrucción de dominio DROP*|"DOMINIO COLOCAR"|SQL_DIAG_DROP_DOMAIN|  
|*instrucción de DROP index*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*declaración de esquema de colocación*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*declaración de tabla de destino*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*instrucción de traducción de DROP*|"TRADUCCIÓN COLOCAR"|SQL_DIAG_DROP_TRANSLATION|  
|*instrucción de vista DROP*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
-instrucción *|"GRANT"|SQL_DIAG_GRANT|  
|*instrucción INSERT*|"INSERTAR"|SQL_DIAG_INSERT|  
|*Extensión de procedimiento de ODBC*|"LLAMADA"|LLAMADA SQL_DIAG_|  
|*instrucción REVOKE*|"REVOKE"|SQL_DIAG_REVOKE|  
|*definición de esquema*|"CREAR ESQUEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*definición de la traducción*|"CREAR TRADUCCIÓN"|SQL_DIAG_CREATE_TRANSLATION|  
|*posición de instrucción de actualización*|"LA ACTUALIZACIÓN DINÁMICA CURSOR"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*búsquedas en la instrucción Update*|"ACTUALIZAR WHERE"|SQL_DIAG_UPDATE_WHERE|  
|Desconocido|*Cadena vacía*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>Secuencia de registros de estado  
 Registros de estado se colocan en una secuencia basándose en el número de fila y el tipo del diagnóstico. El Administrador de controladores determina el orden final en el que se va a devolver registros de estado que genera. El controlador determina el orden final en el que se va a devolver registros de estado que genera.  
  
 Si los registros de diagnóstico se registran mediante el Administrador de controladores y el controlador, el Administrador de controladores es responsable de ordenarlas.  
  
 Si hay dos o más registros de estado, la secuencia de los registros se determina en primer lugar por número de fila. Se aplican las siguientes reglas para determinar la secuencia de registros de diagnóstico por fila:  
  
-   Los registros que no corresponden a ninguna fila aparecen delante de los registros que corresponden a una fila determinada, porque SQL_NO_ROW_NUMBER se define como -1.  
  
-   Registros para los que se desconoce el número de fila aparecen delante de todos los demás registros, porque SQL_ROW_NUMBER_UNKNOWN se define como – 2.  
  
-   Para todos los registros que pertenecen a filas específicas, los registros se ordenan por el valor del campo SQL_DIAG_ROW_NUMBER. Se muestran todos los errores y advertencias de la primera fila afectada y, a continuación, todos los errores y advertencias de la siguiente fila afectada y así sucesivamente.  
  
> [!NOTE]  
>  ODBC 3 *.x* el Administrador de controladores no ordena los registros de estado en la cola de diagnóstico si SQLSTATE 01S01 (Error en la fila) devuelto por una API ODBC 2 *.x* controlador o si SQLSTATE 01S01 (Error en la fila) se devuelve un ODBC 3 *.x* controlador cuando **SQLExtendedFetch** se llama o **SQLSetPos** se llama en un cursor que se ha colocado con **SQLExtendedFetch** .  
  
 Dentro de cada fila, o para todos los registros que no corresponden a una fila o para que se desconoce el número de fila o de todos los registros con un número de filas igual a SQL_NO_ROW_NUMBER, el primer registro enumerado se determina mediante el uso de un conjunto de reglas de ordenación. Después del primer registro, el orden de los demás registros que afectan a una fila es indefinido. Una aplicación no puede suponer que los errores preceden advertencias después del primer registro. Las aplicaciones deben examinar la estructura de datos de diagnóstico completo para obtener información completa sobre una llamada a una función incorrecta.  
  
 Las reglas siguientes se utilizan para determinar el primer registro dentro de una fila. El registro con la clasificación más alta es el primer registro. El origen de un registro (Administrador de controladores, controladores, puerta de enlace etc.) no se considera cuando los registros de categoría.  
  
-   **Errores** registros de estado que se describen los errores tienen la clasificación más alta. Las siguientes reglas se aplican para ordenar los errores:  
  
    -   Los registros que indican un error de transacción o transacciones posible error outrank todos los demás registros.  
  
    -   Si dos o más registros de describen la misma condición de error, SQLSTATE definido por la especificación de CLI de grupo abierto (clases 03 a través de HZ) outrank definidos por el controlador y el ODBC SQLSTATE.  
  
-   **Los valores de datos No definido por la implementación** registros de estado que se describen los valores de datos No definidos por el controlador (clase 02) tienen la segunda clasificación más alta.  
  
-   **Advertencias** registros de estado que describen las advertencias (clase 01) tienen el rango más bajo. Si dos o más registros describen la misma condición de advertencia, a continuación, advertencia SQLSTATE definido por la especificación de CLI de grupo abierto outrank SQLSTATE definida por ODBC y definidos por el controlador.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtener varios campos de una estructura de datos de diagnóstico|[Función SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
