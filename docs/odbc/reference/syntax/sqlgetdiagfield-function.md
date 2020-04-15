---
title: FUNción SQLGetDiagField ( SQLGetDiagField) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285435"
---
# <a name="sqlgetdiagfield-function"></a>Función SQLGetDiagField

**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLGetDiagField** devuelve el valor actual de un campo de un registro de la estructura de datos de diagnóstico (asociado a un identificador especificado) que contiene información de error, advertencia y estado.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp

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
 [Entrada] Identificador de tipo de identificador que describe el tipo de identificador para el que se requieren diagnósticos. Debe ser una de las siguientes:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN identificador solo lo utilizan el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información acerca de SQL_HANDLE_DBC_INFO_TOKEN, vea Desarrollar el reconocimiento de grupos [de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Identificador de la estructura de datos de diagnóstico, del tipo indicado por *HandleType*. Si *HandleType* es SQL_HANDLE_ENV, *Handle* puede ser un identificador de entorno compartido o no compartido.  
  
 *RecNumber*  
 [Entrada] Indica el registro de estado del que la aplicación solicita información. Los registros de estado se numeran desde 1. Si el *Argumento DiagIdentifier* indica cualquier campo del encabezado de diagnóstico, se omite *RecNumber.* Si no, debe ser más de 0.  
  
 *DiagIdentifier*  
 [Entrada] Indica el campo del diagnóstico cuyo valor se va a devolver. Para obtener más información, vea la sección "*Argumento DiagIdentifier"* en "Comentarios."  
  
 *DiagInfoPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la información de diagnóstico. El tipo de datos depende del valor de *DiagIdentifier*. Si *DiagInfoPtr* es un tipo entero, las aplicaciones deben usar un búfer de SQLULEN e inicializar el valor en 0 antes de llamar a esta función, ya que algunos controladores solo pueden escribir los 32 bits o 16 bits inferiores de un búfer y dejar el bit de orden superior sin cambios.  
  
 Si *DiagInfoPtr* es NULL, *StringLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *DiagInfoPtr*.  
  
 *BufferLength*  
 [Entrada] Si *DiagIdentifier* es un diagnóstico definido por ODBC y *DiagInfoPtr* apunta a una cadena \*de caracteres o un búfer binario, este argumento debe ser la longitud de *DiagInfoPtr*. Si *DiagIdentifier* es un campo \*definido por ODBC y *DiagInfoPtr* es un entero, *BufferLength* se omite. Si el valor de * \*DiagInfoPtr* es una cadena Unicode (al llamar a **SQLGetDiagFieldW**), el argumento *BufferLength* debe ser un número par.  
  
 Si *DiagIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores estableciendo el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si *DiagInfoPtr* es un puntero a una cadena de caracteres, *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *DiagInfoPtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si *DiagInfoPtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si * \*DiagInfoPtr* contiene un tipo de datos de longitud fija, *BufferLength* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes \*(excluyendo el número de bytes necesarios para el carácter de terminación nula) disponible para devolver en *DiagInfoPtr*, para los datos de caracteres. Si el número de bytes disponibles para devolver es mayor o igual que *BufferLength*, el texto de \* *DiagInfoPtr* se trunca en *BufferLength* menos la longitud de un carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLGetDiagField** no publica registros de diagnóstico por sí mismo. Utiliza los siguientes valores devueltos para informar del resultado de su propia ejecución:  
  
-   SQL_SUCCESS: la función devolvió correctamente la información de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* era demasiado pequeño para contener el campo de diagnóstico solicitado. Por lo tanto, los datos del campo de diagnóstico se truncaron. Para determinar que se ha producido un truncamiento, la aplicación debe comparar *BufferLength* con el número real de bytes disponibles, que se escribe en **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: el identificador indicado por *HandleType* y *Handle* no era un identificador válido.  
  
-   SQL_ERROR: Se ha producido una de las siguientes situaciones:  
  
    -   *El argumento DiagIdentifier* no era uno de los valores válidos.  
  
    -   *El Argumento DiagIdentifier* se SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE o SQL_DIAG_ROW_COUNT, pero *Handle* no era un identificador de instrucción. (El Administrador de controladores devuelve este diagnóstico.)  
  
    -   *El Argumento RecNumber* era negativo o 0 cuando *DiagIdentifier* indicaba un campo de un registro de diagnóstico. *RecNumber* se omite para los campos de encabezado.  
  
    -   El valor solicitado era una cadena de caracteres y *BufferLength* era menor que cero.  
  
    -   Cuando se usa la notificación asincrónica, la operación asincrónica en el identificador no se completó.  
  
-   SQL_NO_DATA: *RecNumber* era mayor que el número de registros de diagnóstico que existían para el identificador especificado en *Handle.* La función también devuelve SQL_NO_DATA para cualquier *RecNumber* positivo si no hay registros de diagnóstico para *Handle*.  
  
## <a name="comments"></a>Comentarios  
 Normalmente, una aplicación llama a **SQLGetDiagField** para lograr uno de los tres objetivos:  
  
1.  Para obtener información específica de error o advertencia cuando una llamada de función ha devuelto SQL_ERROR o SQL_SUCCESS_WITH_INFO (o SQL_NEED_DATA para la función **SQLBrowseConnect).**  
  
2.  Para determinar el número de filas en el origen de datos que se vieron afectadas al insertar, eliminar o actualizar las operaciones se realizaron con una llamada a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** (desde el campo de encabezado SQL_DIAG_ROW_COUNT), o para determinar el número de filas que existen en el cursor abierto actual, si el controlador puede proporcionar esta información (desde el campo de encabezado SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Para determinar qué función se ejecutó mediante una llamada a **SQLExecDirect** o **SQLExecute** (desde los campos de encabezado SQL_DIAG_DYNAMIC_FUNCTION y SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Cualquier función ODBC puede registrar cero o más registros de diagnóstico cada vez que se llama, por lo que una aplicación puede llamar a **SQLGetDiagField** después de cualquier llamada a la función ODBC. No hay límite en el número de registros de diagnóstico que se pueden almacenar a la vez. **SQLGetDiagField** recupera solo la información de diagnóstico asociada más recientemente con la estructura de datos de diagnóstico especificada en el *Handle* argumento. Si la aplicación llama a una función ODBC distinta de **SQLGetDiagField** o **SQLGetDiagRec**, se pierde cualquier información de diagnóstico de una llamada anterior con el mismo identificador.  
  
 Una aplicación puede examinar todos los registros de diagnóstico incrementando *RecNumber*, siempre y cuando **SQLGetDiagField** devuelve SQL_SUCCESS. El número de registros de estado se indica en el campo de encabezado de SQL_DIAG_NUMBER. Las llamadas a **SQLGetDiagField** no son destructivas para los campos de encabezado y registro. La aplicación puede llamar a **SQLGetDiagField** de nuevo más adelante para recuperar un campo de un registro, siempre y cuando no se ha llamado a una función distinta de las funciones de diagnóstico en el intermedio, que registraría registros en el mismo identificador.  
  
 Una aplicación puede llamar a **SQLGetDiagField** para devolver cualquier campo de diagnóstico en cualquier momento, excepto SQL_DIAG_CURSOR_ROW_COUNT o SQL_DIAG_ROW_COUNT, que devolverá SQL_ERROR si *Handle* no es un identificador de instrucción. Si cualquier otro campo de diagnóstico es indefinido, la llamada a **SQLGetDiagField** devolverá SQL_SUCCESS (siempre que no se encuentre ningún otro diagnóstico) y se devuelva un valor indefinido para el campo.  
  
 Para obtener más información, vea Uso de [SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [Implementación de SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Llamar a una API distinta de la que se ejecuta de forma asincrónica generará HY010 "Error de secuencia de funciones". Sin embargo, el registro de error no se puede recuperar antes de que se complete la operación asincrónica.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador puede tener información de diagnóstico asociada. El *argumento HandleType* indica el tipo *de*identificador Handle .  
  
 Algunos campos de encabezado y registro no se pueden devolver para los identificadores de entorno, conexión, instrucción y descriptor. Los identificadores para los que un campo no es aplicable se indican en las secciones "Campos de encabezado" y "Campos de registro" siguientes.  
  
 Si *HandleType* es SQL_HANDLE_ENV, *Handle* puede ser un identificador de entorno compartido o no compartido.  
  
 No se debe asociar ningún campo de diagnóstico de encabezado específico del controlador a un identificador de entorno.  
  
 Los únicos campos de encabezado de diagnóstico que se definen para un identificador de descriptor son SQL_DIAG_NUMBER y SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argumento DiagIdentifier  
 Este argumento indica el identificador del campo necesario de la estructura de datos de diagnóstico. Si *RecNumber* es mayor o igual que 1, los datos del campo describen la información de diagnóstico devuelta por una función. Si *RecNumber* es 0, el campo está en el encabezado de la estructura de datos de diagnóstico y, por lo tanto, contiene datos pertenecientes a la llamada de función que devolvió la información de diagnóstico, no a la información específica.  
  
 Los controladores pueden definir campos de encabezado y registro específicos del controlador en la estructura de datos de diagnóstico.  
  
 Una aplicación ODBC 3 *.x* que trabaje con un controlador ODBC 2 *.x* solo podrá llamar a **SQLGetDiagField** con un argumento *DiagIdentifier* de SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME o SQL_DIAG_SQLSTATE. Todos los demás campos de diagnóstico devolverán SQL_ERROR.  
  
## <a name="header-fields"></a>Campos de encabezado  
 Los campos de encabezado enumerados en la tabla siguiente se pueden incluir en el *Argumento DiagIdentifier.*  
  
|DiagIdentifier|Tipo de valor devuelto|Devuelve|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Este campo contiene el recuento de filas en el cursor. Su semántica depende de los tipos de información **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 y SQL_STATIC_CURSOR_ATTRIBUTES2, que indican qué recuentos de filas están disponibles para cada tipo de cursor (en los bits SQL_CA2_CRC_EXACT y SQL_CA2_CRC_APPROXIMATE).<br /><br /> El contenido de este campo se define solo para los identificadores de instrucción y solo después de **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se ha llamado. Llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_CURSOR_ROW_COUNT en otro identificador de instrucción devolverá SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Se trata de una cadena que describe la instrucción SQL que ejecutó la función subyacente. (Consulte "Valores de los campos Función dinámica", más adelante en esta sección, para obtener valores específicos.) El contenido de este campo se define solo para identificadores de instrucción y solo después de una llamada a **SQLExecute**, **SQLExecDirect**o **SQLMoreResults**. Llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION en otro identificador de instrucción devolverá SQL_ERROR. El valor de este campo es indefinido antes de una llamada a **SQLExecute** o **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Se trata de un código numérico que describe la instrucción SQL ejecutada por la función subyacente. (Consulte "Valores de los campos de función dinámica", más adelante en esta sección, para obtener un valor específico.) El contenido de este campo se define solo para identificadores de instrucción y solo después de una llamada a **SQLExecute**, **SQLExecDirect**o **SQLMoreResults**. Llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_DYNAMIC_FUNCTION_CODE en otro que un identificador de instrucción devolverá SQL_ERROR. El valor de este campo es indefinido antes de una llamada a **SQLExecute** o **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|El número de registros de estado que están disponibles para el identificador especificado.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Código de retorno devuelto por la función. Para obtener una lista de códigos de retorno, consulte [Códigos](../../../odbc/reference/develop-app/return-codes-odbc.md)de devolución . El controlador no tiene que implementar SQL_DIAG_RETURNCODE; siempre es implementado por el Administrador de controladores. Si todavía no se ha llamado a ninguna función en el *controlador*, se devolverá SQL_SUCCESS para SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|Número de filas afectadas por una inserción, eliminación o actualización realizada por **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos**. Se define por controlador después de ejecutar una especificación de *cursor.* El contenido de este campo se define solo para los identificadores de instrucción. Llamar a **SQLGetDiagField** con un *DiagIdentifier* de SQL_DIAG_ROW_COUNT en otro identificador de instrucción devolverá SQL_ERROR. Los datos de este campo también se devuelven en el argumento *RowCountPtr* de **SQLRowCount**. Los datos de este campo se restablecen después de cada llamada de función no diagnostica, mientras que el recuento de filas devuelto por **SQLRowCount** sigue siendo el mismo hasta que la instrucción se establece de nuevo en el estado preparado o asignado.|  
  
## <a name="record-fields"></a>Campos de registro  
 Los campos de registro enumerados en la tabla siguiente se pueden incluir en el *Argumento DiagIdentifier.*  
  
|DiagIdentifier|Tipo de valor devuelto|Devuelve|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Cadena que indica el documento que define la parte de clase del valor SQLSTATE en este registro. Su valor es "ISO 9075" para todos los SQLSTATEs definidos por Open Group e ISO interfaz de nivel de llamada. Para SQLSTATEs específicos de ODBC (todos aquellos cuya clase SQLSTATE es "IM"), su valor es "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Si el campo SQL_DIAG_ROW_NUMBER es un número de fila válido en un conjunto de filas o un conjunto de parámetros, este campo contiene el valor que representa el número de columna en el conjunto de resultados o el número de parámetro en el conjunto de parámetros. Los números de columna del conjunto de resultados siempre comienzan en 1; si este registro de estado pertenece a una columna de marcador, el campo puede ser cero. Los números de parámetro comienzan en 1. Tiene el valor SQL_NO_COLUMN_NUMBER si el registro de estado no está asociado a un número de columna o número de parámetro. Si el controlador no puede determinar el número de columna o el número de parámetro al que está asociado este registro, este campo tiene el valor SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> El contenido de este campo se define solo para los identificadores de instrucción.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Cadena que indica el nombre de la conexión con la que se relaciona el registro de diagnóstico. Este campo está definido por el controlador. Para las estructuras de datos de diagnóstico asociadas con el identificador de entorno y para los diagnósticos que no se relacionan con ninguna conexión, este campo es una cadena de longitud cero.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Un mensaje informativo sobre el error o advertencia. Este campo tiene el formato descrito en [Mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md). No hay una longitud máxima para el texto del mensaje de diagnóstico.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Código de error nativo específico del controlador/origen de datos. Si no hay ningún código de error nativo, el controlador devuelve 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Este campo contiene el número de fila del conjunto de filas o el número de parámetro del conjunto de parámetros con el que está asociado el registro de estado. Los números de fila y los números de parámetro comienzan con 1. Este campo tiene el valor SQL_NO_ROW_NUMBER si este registro de estado no está asociado a un número de fila o número de parámetro. Si el controlador no puede determinar el número de fila o el número de parámetro al que está asociado este registro, este campo tiene el valor SQL_ROW_NUMBER_UNKNOWN.<br /><br /> El contenido de este campo se define solo para los identificadores de instrucción.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Cadena que indica el nombre del servidor con el que se relaciona el registro de diagnóstico. Es el mismo que el valor devuelto para una llamada a **SQLGetInfo** con la opción SQL_DATA_SOURCE_NAME. Para las estructuras de datos de diagnóstico asociadas con el identificador de entorno y para los diagnósticos que no se relacionan con ningún servidor, este campo es una cadena de longitud cero.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Un código de diagnóstico SQLSTATE de cinco caracteres. Para obtener más información, vea [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Una cadena con el mismo formato y valores válidos que SQL_DIAG_CLASS_ORIGIN, que identifica la parte de definición de la parte de subclase del código SQLSTATE. Los SQLSTATES específicos de ODBC para los que se devuelve "ODBC 3.0" incluyen lo siguiente:<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY0999, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM01, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valores de los campos de función dinámica  
 En la tabla siguiente se describen los valores de SQL_DIAG_DYNAMIC_FUNCTION y SQL_DIAG_DYNAMIC_FUNCTION_CODE que se aplican a cada tipo de instrucción SQL ejecutada por una llamada a **SQLExecute** o **SQLExecDirect**. El controlador puede agregar valores definidos por el controlador a los enumerados.  
  
|Instrucción SQL<br /><br /> Ejecutado|Valor de <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valor de <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain-statement*|"ALTER DOMAIN"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table-statement*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*aserción-definición*|"CREAR ASERCIÓN"|SQL_DIAG_CREATE_ASSERTION|  
|*caracterización de juego de caracteres*|"CREAR JUEGO DE PERSONAJES"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*cotelación-definición*|"CREAR COLLATION"|SQL_DIAG_CREATE_COLLATION|  
|*domainn-definition*|"CREAR DOMINIO"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-statement*|"CREAR ÍNDICE"|SQL_DIAG_CREATE_INDEX|  
|*create-table-statement*|"CREAR TABLA"|SQL_DIAG_CREATE_TABLE|  
|*create-view-statement*|"CREAR VISTA"|SQL_DIAG_CREATE_VIEW|  
|*cursor-especificación*|"SELECCIONAR CURSOR"|SQL_DIAG_SELECT_CURSOR|  
|*delete-statement-positioned*|"CURSOR DE ELIMINACIÓN DINÁMICA"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete-statement-searched*|"ELIMINAR DONDE"|SQL_DIAG_DELETE_WHERE|  
|*drop-assertion-statement*|"DROP ASSERTION"|SQL_DIAG_DROP_ASSERTION|  
|*drop-character-set-stmt*|"DROP CHARACTER SET"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation-statement*|"DROP COLLATION"|SQL_DIAG_DROP_COLLATION|  
|*drop-domain-statement*|"DOMINIO DE DROP"|SQL_DIAG_DROP_DOMAIN|  
|*drop-index-statement*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop-schema-statement*|"ESQUEMA DE GOTA"|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-statement*|"TABLA DE DROP"|SQL_DIAG_DROP_TABLE|  
|*drop-translation-statement*|"DROP TRANSLATION"|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-statement*|"VISTA DE GOTA"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|"GRANT"|SQL_DIAG_GRANT|
|*insert-statement*|"INSERTAR"|SQL_DIAG_INSERT|  
|*ODBC-procedimiento-extensión*|"LLAMADA"|SQL_DIAG_ LLAMADA|  
|*revocar-declaración*|"REVOKE"|SQL_DIAG_REVOKE|  
|*definición de esquema*|"CREAR ESQUEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*traducción-definición*|"CREATE TRANSLATION"|SQL_DIAG_CREATE_TRANSLATION|  
|*update-statement-positioned*|"CURSOR DE ACTUALIZACIÓN DINÁMICA"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update-statement-searched*|"ACTUALIZAR DONDE"|SQL_DIAG_UPDATE_WHERE|  
|Desconocido|*cadena vacía*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>Secuencia de registros de estado

 Los registros de estado se colocan en una secuencia basada en el número de fila y el tipo de diagnóstico. El Administrador de controladores determina el orden final en el que se devuelven los registros de estado que genera. El controlador determina el orden final en el que se devuelven los registros de estado que genera.  
  
 Si el Administrador de controladores y el controlador registran los registros de diagnóstico, el Administrador de controladores es responsable de ordenarlos.  
  
 Si hay dos o más registros de estado, la secuencia de los registros se determina primero por número de fila. Las siguientes reglas se aplican a la determinación de la secuencia de registros de diagnóstico por fila:  
  
-   Los registros que no corresponden a ninguna fila aparecen delante de los registros que corresponden a una fila determinada, porque SQL_NO_ROW_NUMBER se define como -1.  
  
-   Los registros para los que se desconoce el número de fila aparecen delante de todos los demás registros, porque SQL_ROW_NUMBER_UNKNOWN se define como -2.  
  
-   Para todos los registros que pertenecen a filas específicas, los registros se ordenan por el valor del campo SQL_DIAG_ROW_NUMBER. Se enumeran todos los errores y advertencias de la primera fila afectada y, a continuación, todos los errores y advertencias de la siguiente fila afectados, etc.  
  
> [!NOTE]
>  El Administrador de controladores ODBC 3 *.x* no ordena registros de estado en la cola de diagnóstico si SQLSTATE 01S01 (Error en fila) es devuelto por un controlador ODBC 2 *.x* o si SQLSTATE 01S01 (Error en fila) es devuelto por un controlador ODBC 3 *.x* cuando **sqlExtendedFetch** se llama o **SQLSetPos** se llama en un cursor que se ha colocado con **SQLExtendedFetch**.  
  
 Dentro de cada fila, o para todos aquellos registros que no corresponden a una fila o para los que se desconoce el número de fila, o para todos aquellos registros con un número de fila igual a SQL_NO_ROW_NUMBER, el primer registro enumerado se determina mediante un conjunto de reglas de ordenación. Después del primer registro, el orden de los demás registros que afectan a una fila es indefinido. Una aplicación no puede suponer que los errores preceden a las advertencias después del primer registro. Las aplicaciones deben examinar la estructura de datos de diagnóstico completa para obtener información completa sobre una llamada incorrecta a una función.  
  
 Las siguientes reglas se utilizan para determinar el primer registro dentro de una fila. El registro con el rango más alto es el primer registro. El origen de un registro (Administrador de controladores, controlador, puerta de enlace, etc.) no se tiene en cuenta al clasificar registros.  
  
-   **Errores** Los registros de estado que describen los errores tienen el rango más alto. Las siguientes reglas se aplican a los errores de ordenación:  
  
    -   Los registros que indican un error de transacción o un posible error de transacción sube a todos los demás registros.  
  
    -   Si dos o más registros describen la misma condición de error, los SQLSTATEs definidos por la especificación de la CLI de grupo abierto (clases 03 a HZ) superaron a SQLSTATEs definidos por ODBC y controlador.  
  
-   **Valores sin datos definidos por la implementación** Los registros de estado que describen los valores sin datos definidos por el controlador (clase 02) tienen el segundo rango más alto.  
  
-   **Advertencias** Los registros de estado que describen las advertencias (clase 01) tienen el rango más bajo. Si dos o más registros describen la misma condición de advertencia, la advertencia de SQLSTATEs definidas por la especificación de la CLI de grupo abierto supera a SQLSTATEs definidos por ODBC y definidos por controladores.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de múltiples campos de una estructura de datos de diagnóstico|[Función SQLGetDiagRec](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
