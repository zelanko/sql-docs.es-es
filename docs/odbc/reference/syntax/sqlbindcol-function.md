---
title: Función SQLBindCol (SQLBindCol) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90bb1c1aa4dbfa2614f689faa47eb0c41a6cecd6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298745"
---
# <a name="sqlbindcol-function"></a>SQLBindCol (función)
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLBindCol** enlaza los búferes de datos de aplicación a las columnas del conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ColumnNumber*  
 [Entrada] Número de la columna del conjunto de resultados que se va a enlazar. Las columnas se numeran en orden de columna creciente a partir de 0, donde la columna 0 es la columna de marcador. Si no se utilizan marcadores - es decir, el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se establece en SQL_UB_OFF - a continuación, los números de columna comienzan en 1.  
  
 *TargetType*  
 [Entrada] Identificador del tipo de datos \*C del búfer *TargetValuePtr.* Cuando recupera datos del origen de datos con **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**o **SQLSetPos**, el controlador convierte los datos a este tipo; Cuando envía datos al origen de datos con **SQLBulkOperations** o **SQLSetPos**, el controlador convierte los datos de este tipo. Para obtener una lista de tipos de datos C válidos e identificadores de tipo, consulte la sección Tipos de [datos de C](../../../odbc/reference/appendixes/c-data-types.md) en Apéndice D: Tipos de datos.  
  
 Si el argumento *TargetType* es un tipo de datos de intervalo, se utilizan para los datos la precisión inicial del intervalo predeterminado (2) y la precisión de segundos de intervalo predeterminada (6), tal como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION de la ARD, respectivamente. Si el *TargetType* argumento es SQL_C_NUMERIC, la precisión predeterminada (definida por el controlador) y la escala predeterminada (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de la ARD, se utilizan para los datos. Si alguna precisión o escala predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor adecuado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Entrada/salida diferida] Puntero al búfer de datos para enlazar a la columna. **SQLFetch** y **SQLFetchScroll** devuelven datos en este búfer. **SQLBulkOperations** devuelve datos en este búfer cuando *Operation* se SQL_FETCH_BY_BOOKMARK; recupera datos de este búfer cuando *Operation* está SQL_ADD o SQL_UPDATE_BY_BOOKMARK. **SQLSetPos** devuelve datos en este búfer cuando *Operation* se SQL_REFRESH; recupera datos de este búfer cuando *Operation* está SQL_UPDATE.  
  
 Si *TargetValuePtr* es un puntero nulo, el controlador desenlaza el búfer de datos para la columna. Una aplicación puede desenlazar todas las columnas llamando a **SQLFreeStmt** con la opción SQL_UNBIND. Una aplicación puede desenlazar el búfer de datos para una columna, pero todavía tiene un búfer de longitud/indicador enlazado para la columna, si el *TargetValuePtr* argumento en la llamada a **SQLBindCol** es un puntero nulo, pero el *StrLen_or_IndPtr* argumento es un valor válido.  
  
 *BufferLength*  
 [Entrada] Longitud del \*búfer *TargetValuePtr* en bytes.  
  
 El controlador utiliza *BufferLength* para evitar \*escribir más allá del final del búfer *TargetValuePtr* cuando devuelve datos de longitud variable, como datos binarios o de caracteres. Observe que el controlador cuenta el carácter de \*terminación nula cuando devuelve datos de caracteres a *TargetValuePtr*. \*Por lo tanto, *TargetValuePtr* debe contener espacio para el carácter de terminación nula o el controlador truncará los datos.  
  
 Cuando el controlador devuelve datos de longitud fija, como un entero o una estructura de fecha, el controlador omite *BufferLength* y supone que el búfer es lo suficientemente grande como para contener los datos. Por lo tanto, es importante que la aplicación asigne un búfer lo suficientemente grande para los datos de longitud fija o el controlador escribirá más allá del final del búfer.  
  
 **SQLBindCol** devuelve SQLSTATE HY090 (longitud de cadena o búfer no válida) cuando *BufferLength* es menor que 0 pero no cuando *BufferLength* es 0. Sin embargo, si *TargetType* especifica un tipo de carácter, una aplicación no debe establecer *BufferLength* en 0, porque los controladores compatibles con la CLI de ISO devuelven SQLSTATE HY090 (cadena no válida o longitud de búfer) en ese caso.  
  
 *StrLen_or_IndPtr*  
 [Entrada/salida diferida] Puntero al búfer de longitud/indicador que se va a enlazar a la columna. **SQLFetch** y **SQLFetchScroll** devuelven un valor en este búfer. **SQLBulkOperations** recupera un valor de este búfer cuando *Operation* está SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** devuelve un valor en este búfer cuando *Operation* se SQL_FETCH_BY_BOOKMARK. **SQLSetPos** devuelve un valor en este búfer cuando *Operation* es SQL_REFRESH; recupera un valor de este búfer cuando *Operation* está SQL_UPDATE.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**y **SQLSetPos** pueden devolver los siguientes valores en el búfer de longitud/indicador:  
  
-   La longitud de los datos disponibles para devolver  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 La aplicación puede colocar los siguientes valores en el búfer de longitud/indicador para su uso con **SQLBulkOperations** o **SQLSetPos:**  
  
-   La longitud de los datos que se envían  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   El resultado de la macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Si el búfer del indicador y el búfer de longitud son búferes independientes, el búfer del indicador solo puede devolver SQL_NULL_DATA, mientras que el búfer de longitud puede devolver todos los demás valores.  
  
 Para obtener más información, vea [SqlBulkOperations (Función)](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLFetch (Función)](../../../odbc/reference/syntax/sqlfetch-function.md), [SQLSetPos (Función)](../../../odbc/reference/syntax/sqlsetpos-function.md)y Uso de valores [de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Si *StrLen_or_IndPtr* es un puntero nulo, no se utiliza ningún valor de longitud o indicador. Se trata de un error al capturar datos y los datos son NULL.  
  
 Consulte Información de [ODBC de 64 bits,](../../../odbc/reference/odbc-64-bit-information.md)si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLBindCol** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLBindCol** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|(DM) el *ColumnNumber* argumento era 0, y el *TargetType* argumento no era SQL_C_BOOKMARK ni SQL_C_VARBOOKMARK.|  
|07009|Indice de descriptor no válido|El valor especificado para el argumento *ColumnNumber* superó el número máximo de columnas en el conjunto de resultados.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY003|Tipo de búfer de aplicación no válido|El argumento *TargetType* no era un tipo de datos válido ni SQL_C_DEFAULT.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando **SQLBindCol** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> (DM) El controlador era un ODBC 2. *x* driver, el *columnNumber* argumento se estableció en 0, y el valor especificado para el argumento *BufferLength* no era igual a 4.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la conversión especificada por la combinación del argumento *TargetType* y el tipo de datos SQL específico del controlador de la columna correspondiente.<br /><br /> El argumento *ColumnNumber* era 0 y el controlador no admite marcadores.<br /><br /> El controlador solo admite ODBC 2. *x* y el argumento *TargetType* fue uno de los siguientes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y cualquiera de los tipos de datos de intervalo C enumerados en [C Tipos](../../../odbc/reference/appendixes/c-data-types.md) de datos en el Apéndice D: Tipos de datos.<br /><br /> El controlador solo admite versiones ODBC anteriores a 3.50 y el argumento *TargetType* se SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 **SQLBindCol** se utiliza para asociar o *enlazar* columnas del conjunto de resultados a búferes de datos y búferes de longitud/indicador en la aplicación. Cuando la aplicación llama a **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** para capturar datos, el controlador devuelve los datos de las columnas enlazadas en los búferes especificados; Para obtener más información, vea [SqlFetch (Función).](../../../odbc/reference/syntax/sqlfetch-function.md) Cuando la aplicación llama a **SQLBulkOperations** para actualizar o insertar una fila o **SQLSetPos** para actualizar una fila, el controlador recupera los datos de las columnas enlazadas de los búferes especificados; Para obtener más información, vea [SQLBulkOperations (función)](../../../odbc/reference/syntax/sqlbulkoperations-function.md) o [SQLSetPos (función).](../../../odbc/reference/syntax/sqlsetpos-function.md) Para obtener más información sobre el enlace, vea [Recuperar resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Tenga en cuenta que las columnas no tienen que estar enlazadas para recuperar datos de ellas. Una aplicación también puede llamar a **SQLGetData** para recuperar datos de columnas. Aunque es posible enlazar algunas columnas de una fila y llamar a **SQLGetData** para otros, esto está sujeto a algunas restricciones. Para obtener más información, vea [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Enlazar, desvincular y volver a enlazar columnas  
 Una columna se puede enlazar, desenlazar o rebotar en cualquier momento, incluso después de que los datos se hayan obtenido del conjunto de resultados. El nuevo enlace surten efecto la próxima vez que se llama a una función que usa enlaces. Por ejemplo, supongamos que una aplicación enlaza las columnas de un conjunto de resultados y llama a **SQLFetch**. El controlador devuelve los datos en los búferes enlazados. Ahora supongamos que la aplicación enlaza las columnas a un conjunto diferente de búferes. El controlador no coloca los datos de la fila recién capturada en los búferes recién enlazados. En su lugar, espera hasta que **sqlFetch** se llama de nuevo y, a continuación, coloca los datos de la fila siguiente en los búferes recién enlazados.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre debe establecerse antes de enlazar una columna a la columna 0. Esto no es necesario, pero se recomienda encarecidamente.  
  
## <a name="binding-columns"></a>Enlazar columnas  
 Para enlazar una columna, una aplicación llama a **SQLBindCol** y pasa el número de columna, tipo, dirección y longitud de un búfer de datos y la dirección de un búfer de longitud/indicador. Para obtener información sobre cómo se utilizan estas direcciones, consulte "Direcciones de búfer", más adelante en esta sección. Para obtener más información acerca del enlace de columnas, vea Uso de [SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 El uso de estos buffers se aplaza; es decir, la aplicación los enlaza en **SQLBindCol** pero el controlador tiene acceso a ellos desde otras funciones, a saber, **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**. Es responsabilidad de la aplicación asegurarse de que los punteros especificados en **SQLBindCol** siguen siendo válidos mientras el enlace permanezca en vigor. Si la aplicación permite que estos punteros den a ser no válidos (por ejemplo, libera un búfer) y, a continuación, llama a una función que espera que sean válidos, las consecuencias son indefinidas. Para obtener más información, consulte [Zonas de influencia diferidas](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 El enlace permanece en vigor hasta que se reemplaza por un nuevo enlace, la columna no está enlazada o la instrucción se libera.  
  
## <a name="unbinding-columns"></a>Desvinculación de columnas  
 Para desenlazar una sola columna, una aplicación llama **a SQLBindCol** con *ColumnNumber* establecido en el número de esa columna y *TargetValuePtr* establecido en un puntero nulo. Si *ColumnNumber* hace referencia a una columna sin enlazar, **SQLBindCol** todavía devuelve SQL_SUCCESS.  
  
 Para desenlazar todas las columnas, una aplicación llama a **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND. Esto también se puede lograr estableciendo el campo SQL_DESC_COUNT del ARD en cero.  
  
## <a name="rebinding-columns"></a>Volver a enlazar columnas  
 Una aplicación puede realizar cualquiera de las dos operaciones para cambiar un enlace:  
  
-   Llame a **SQLBindCol** para especificar un nuevo enlace para una columna que ya está enlazada. El controlador sobrescribe el enlace antiguo con el nuevo.  
  
-   Especifique un desplazamiento que se agregará a la dirección de búfer especificada por la llamada de enlace a **SQLBindCol**. Para obtener más información, vea la siguiente sección, "Desfases de enlace."  
  
## <a name="binding-offsets"></a>Desplazamientos de encuadernación  
 Un desplazamiento de enlace es un valor que se agrega a las direcciones de los búferes de datos y longitud/indicador (como se especifica en el *TargetValuePtr* y *StrLen_or_IndPtr* argumento) antes de que se desreferencian. Cuando se utilizan desplazamientos, los enlaces son una "plantilla" de cómo se distribuyen los búferes de la aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Dado que se agrega el mismo desplazamiento a cada dirección en cada enlace, los desplazamientos relativos entre búferes para columnas diferentes deben ser los mismos dentro de cada conjunto de búferes. Esto siempre es cierto cuando se usa el enlace de fila; la aplicación debe establecer cuidadosamente sus búferes para que esto sea cierto cuando se utiliza el enlace de columna.  
  
 El uso de un desplazamiento de enlace tiene básicamente el mismo efecto que volver a enlazar una columna llamando a **SQLBindCol**. La diferencia es que una nueva llamada a **SQLBindCol** especifica nuevas direcciones para el búfer de datos y el búfer de longitud/indicador, mientras que el uso de un desplazamiento de enlace no cambia las direcciones, sino que simplemente agrega un desplazamiento a ellas. La aplicación puede especificar un nuevo desplazamiento siempre que lo desee, y este desplazamiento siempre se agrega a las direcciones enlazadas originalmente. En particular, si el desplazamiento se establece en 0 o si el atributo de instrucción se establece en un puntero nulo, el controlador utiliza las direcciones enlazadas originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR en la dirección de un búfer SQLINTEGER. Antes de que la aplicación llama a una función que usa enlaces, coloca un desplazamiento en bytes en este búfer. Para determinar la dirección del búfer que se va a usar, el controlador agrega el desplazamiento a la dirección en el enlace. La suma de la dirección y el desplazamiento debe ser una dirección válida, pero la dirección a la que se agrega el desplazamiento no tiene que ser válida. Para obtener más información acerca de cómo se usan los desplazamientos de enlace, vea "Direcciones de búfer", más adelante en esta sección.  
  
## <a name="binding-arrays"></a>Matrizs de enlace  
 Si el tamaño del conjunto de filas (el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE) es mayor que 1, la aplicación enlaza matrices de búferes en lugar de búferes únicos. Para obtener más información, consulte [Cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md).  
  
 La aplicación puede enlazar matrices de dos maneras:  
  
-   Enlazar una matriz a cada columna. Esto se conoce como *enlace de columna* porque cada estructura de datos (matriz) contiene datos para una sola columna.  
  
-   Defina una estructura para contener los datos de una fila completa y enlazar una matriz de estas estructuras. Esto se conoce como *enlace de fila* porque cada estructura de datos contiene los datos de una sola fila.  
  
 Cada matriz de búferes debe tener al menos tantos elementos como el tamaño del conjunto de filas.  
  
> [!NOTE]  
>  Una aplicación debe comprobar que la alineación es válida. Para obtener más información acerca de las consideraciones de alineación, consulte [Alineación](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>El enlace  
 En el enlace de columna, la aplicación enlaza datos independientes y matrices de longitud/indicador a cada columna.  
  
 Para usar el enlace de columna, la aplicación establece primero el atributo de instrucción SQL_ATTR_ROW_BIND_TYPE en SQL_BIND_BY_COLUMN. (Este es el valor predeterminado.) Para cada columna que se va a enlazar, la aplicación realiza los pasos siguientes:  
  
1.  Asigna una matriz de búfer de datos.  
  
2.  Asigna una matriz de búferes de longitud/indicador.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente en descriptores cuando se utiliza el enlace de columna, se pueden utilizar matrices independientes para los datos de longitud e indicador.  
  
3.  Llama a **SQLBindCol** con los argumentos siguientes:  
  
    -   *TargetType* es el tipo de un único elemento en la matriz de búfer de datos.  
  
    -   *TargetValuePtr* es la dirección de la matriz de búfer de datos.  
  
    -   *BufferLength* es el tamaño de un único elemento en la matriz de búfer de datos. El *BufferLength* argumento se omite cuando los datos son datos de longitud fija.  
  
    -   *StrLen_or_IndPtr* es la dirección de la matriz de longitud/indicador.  
  
 Para obtener más información acerca de cómo se usa esta información, consulte "Direcciones de búfer", más adelante en esta sección. Para obtener más información sobre el enlace de columna, vea [Enlace de columna-sabio](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>El enlace  
 En el enlace de fila, la aplicación define una estructura que contiene datos y búferes de longitud/indicador para cada columna que se va a enlazar.  
  
 Para usar el enlace de fila, la aplicación realiza los pasos siguientes:  
  
1.  Define una estructura para contener una sola fila de datos (incluidos los búferes de datos y de longitud/indicador) y asigna una matriz de estas estructuras.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente en descriptores cuando se utiliza el enlace de fila, se pueden utilizar campos independientes para los datos de longitud e indicador.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_BIND_TYPE en el tamaño de la estructura que contiene una sola fila de datos o en el tamaño de una instancia de un búfer en el que se enlazarán las columnas de resultados. La longitud debe incluir espacio para todas las columnas enlazadas y cualquier relleno de la estructura o búfer, para asegurarse de que cuando la dirección de una columna enlazada se incrementa con la longitud especificada, el resultado apuntará al principio de la misma columna en la fila siguiente. Cuando se utiliza el operador *sizeof* en ANSI C, este comportamiento está garantizado.  
  
3.  Llama a **SQLBindCol** con los argumentos siguientes para cada columna que se va a enlazar:  
  
    -   *TargetType* es el tipo del miembro de búfer de datos que se va a enlazar a la columna.  
  
    -   *TargetValuePtr* es la dirección del miembro del búfer de datos en el primer elemento de matriz.  
  
    -   *BufferLength* es el tamaño del miembro del búfer de datos.  
  
    -   *StrLen_or_IndPtr* es la dirección del miembro de la longitud/indicador que se va a enlazar.  
  
 Para obtener más información acerca de cómo se usa esta información, consulte "Direcciones de búfer", más adelante en esta sección. Para obtener más información sobre el enlace de columna, vea Enlace de [fila.](../../../odbc/reference/develop-app/row-wise-binding.md)  
  
## <a name="buffer-addresses"></a>Direcciones de búfer  
 La *dirección del búfer* es la dirección real de los datos o del búfer de longitud/indicador. El controlador calcula la dirección del búfer justo antes de escribir en los búferes (por ejemplo, durante el tiempo de recuperación). Se calcula a partir de la siguiente fórmula, que utiliza las direcciones especificadas en los argumentos *TargetValuePtr* y *StrLen_or_IndPtr,* el desplazamiento de enlace y el número de fila:  
  
 *Desplazamiento* + de*enlace* de dirección enlazada + (( Número de*fila* - 1) x Tamaño *del elemento*)  
  
 donde las variables de la fórmula se definen como se describe en la tabla siguiente.  
  
|Variable|Descripción|  
|--------------|-----------------|  
|*Dirección enlazada*|Para los búferes de datos, la dirección especificada con el *TargetValuePtr* argumento en **SQLBindCol**.<br /><br /> Para los búferes de longitud/indicador, la dirección especificada con el argumento *StrLen_or_IndPtr* en **SQLBindCol**. Para obtener más información, vea "Comentarios adicionales" en la sección "Descriptores y SQLBindCol".<br /><br /> Si la dirección enlazada es 0, no se devuelve ningún valor de datos, incluso si la dirección calculada por la fórmula anterior es distinta de cero.|  
|*Desplazamiento de enlace*|Si se utiliza el enlace de fila, el valor almacenado en la dirección especificada con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Si se utiliza el enlace de columna o si el valor del atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR es un puntero nulo, *Desplazamiento de enlace* es 0.|  
|*Row Number*|El número basado en 1 de la fila del conjunto de filas. Para las capturas de una sola fila, que son el valor predeterminado, este es 1.|  
|*Tamaño del elemento*|El tamaño de un elemento de la matriz enlazada.<br /><br /> Si se utiliza el enlace de columna, se trata de **sizeof(SQLINTEGER)** para los búferes de longitud/indicador. Para los búferes de datos, es el valor de la *BufferLength* argumento en **SQLBindCol** si el tipo de datos es de longitud variable y el tamaño del tipo de datos si el tipo de datos es de longitud fija.<br /><br /> Si se utiliza el enlace de fila, este es el valor del atributo de instrucción SQL_ATTR_ROW_BIND_TYPE para los búferes de datos y de longitud/indicador.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descriptores y SQLBindCol  
 En las secciones siguientes se describe cómo **SQLBindCol** interactúa con descriptores.  
  
> [!CAUTION]  
>  Llamar a **SQLBindCol** para una instrucción puede afectar a otras instrucciones. Esto ocurre cuando el ARD asociado a la instrucción se asigna explícitamente y también está asociado con otras instrucciones. Dado que **SQLBindCol** modifica el descriptor, las modificaciones se aplican a todas las instrucciones con las que está asociado este descriptor. Si este no es el comportamiento necesario, la aplicación debe disociar este descriptor de las otras instrucciones antes de llamar a **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Asignaciones de argumentos  
 Conceptualmente, **SQLBindCol** realiza los siguientes pasos en secuencia:  
  
1.  Llama a **SQLGetStmtAttr** para obtener el identificador ARD.  
  
2.  Llama a **SQLGetDescField** para obtener el campo SQL_DESC_COUNT de este descriptor y, si el valor del argumento *ColumnNumber* supera el valor de SQL_DESC_COUNT, llama a **SQLSetDescField** para aumentar el valor de SQL_DESC_COUNT *a ColumnNumber*.  
  
3.  Llama a **SQLSetDescField** varias veces para asignar valores a los siguientes campos de la ARD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *TargetType*, excepto que si *TargetType* es uno de los identificadores concisos de un subtipo datetime o interval, establece SQL_DESC_TYPE en SQL_DATETIME o SQL_INTERVAL, respectivamente; establece SQL_DESC_CONCISE_TYPE en el identificador conciso; y establece SQL_DESC_DATETIME_INTERVAL_CODE en el subcódigo datetime o interval correspondiente.  
  
    -   Establece uno o varios de SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_DATETIME_INTERVAL_PRECISION, según corresponda para *TargetType*.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH en el valor de *BufferLength*.  
  
    -   Establece el campo SQL_DESC_DATA_PTR en el valor de *TargetValue*.  
  
    -   Establece el campo SQL_DESC_INDICATOR_PTR en el valor de *StrLen_or_Ind*. (Véase el párrafo siguiente.)  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH_PTR en el valor de *StrLen_or_Ind*. (Véase el párrafo siguiente.)  
  
 La variable a la que hace referencia el argumento *StrLen_or_Ind* se utiliza tanto para la información de indicador como de longitud. Si una captura encuentra un valor nulo para la columna, almacena SQL_NULL_DATA en esta variable; de lo contrario, almacena la longitud de los datos en esta variable. Pasar un puntero nulo como *StrLen_or_Ind* evita que la operación de captura devuelva la longitud de los datos, pero hace que la captura falle si encuentra un valor nulo y no tiene forma de devolver SQL_NULL_DATA.  
  
 Si se produce un error en la llamada a **SQLBindCol,** el contenido de los campos descriptores que habría establecido en el ARD son indefinidos y el valor del SQL_DESC_COUNT campo de la ARD no cambia.  
  
## <a name="implicit-resetting-of-count-field"></a>Restablecimiento implícito del campo COUNT  
 **SQLBindCol** establece SQL_DESC_COUNT en el valor de la *ColumnNumber* argumento solo cuando esto aumentaría el valor de SQL_DESC_COUNT. Si el valor de la *TargetValuePtr* argumento es un puntero nulo y el valor de la *ColumnNumber* argumento es igual a SQL_DESC_COUNT (es decir, al desvincular la columna enlazada más alta), SQL_DESC_COUNT se establece en el número de la columna enlazada restante más alta.  
  
## <a name="cautions-regarding-sql_default"></a>Precauciones con respecto a SQL_DEFAULT  
 Para recuperar los datos de columna correctamente, la aplicación debe determinar correctamente la longitud y el punto inicial de los datos en el búfer de aplicación. Cuando la aplicación especifica un *TargetType*explícito, los conceptos erróneos de la aplicación se detectan fácilmente. Sin embargo, cuando la aplicación especifica un *TargetType* de SQL_DEFAULT, **SQLBindCol** se puede aplicar a una columna de un tipo de datos diferente del previsto por la aplicación, ya sea desde cambios en los metadatos o aplicando el código a una columna diferente. En este caso, es posible que la aplicación no siempre determine el inicio o la longitud de los datos de columna capturados. Esto puede dar lugar a errores de datos no notificados o infracciones de memoria.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación ejecuta una instrucción **SELECT** en la tabla Customers para devolver un conjunto de resultados de los identificadores de cliente, los nombres y los números de teléfono, ordenados por nombre. A continuación, llama a **SQLBindCol** para enlazar las columnas de datos a búferes locales. Por último, la aplicación recupera cada fila de datos con **SQLFetch** e imprime el nombre, el identificador y el número de teléfono de cada cliente.  
  
 Para obtener más ejemplos de código, vea [SQLBulkOperations (Función),](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLColumns (Función)](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLFetchScroll (Función)](../../../odbc/reference/syntax/sqlfetchscroll-function.md)y [SQLSetPos (Función) y SQLSetPos (Función).](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 60
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
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
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_WCHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_WCHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_WCHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (int i=0 ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                     {
                        //replace wprintf with printf
                        //%S with %ls
                        //warning C4477: 'wprintf' : format string '%S' requires an argument of type 'char *'
                        //but variadic argument 2 has type 'SQLWCHAR *'
                        //wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                        printf("%d: %ls %ls %ls\n", i + 1, sCustID, szName, szPhone);  
                    }    
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
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
|Devolver información sobre una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Liberación de búferes de columna en la instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtención de parte o la totalidad de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Devolver el número de columnas del conjunto de resultados|[SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
