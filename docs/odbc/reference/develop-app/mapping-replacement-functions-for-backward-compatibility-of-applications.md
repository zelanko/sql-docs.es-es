---
title: Funciones de reemplazo de asignación para la compatibilidad de aplicaciones - ODBC - ODBC Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18669fe9b6edbd39859166e382ad18d1b04a99a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301095"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Asignación de funciones de reemplazo para mantener la compatibilidad de aplicaciones
Una aplicación ODBC *3.x* que trabaje a través del Administrador de controladores ODBC *3.x* funcionará con un controlador ODBC *2.x* siempre que no se utilicen nuevas características. Sin embargo, tanto la funcionalidad duplicada como los cambios de comportamiento afectan a la forma en que funciona la aplicación ODBC *3.x* en un controlador ODBC *2.x.* Cuando se trabaja con un controlador ODBC *2.x,* el Administrador de controladores asigna las siguientes funciones ODBC *3.x,* que han reemplazado una o más funciones ODBC *2.x,* en las funciones ODBC *2.x* correspondientes.  
  
|Función ODBC *3.x*|Función ODBC *2.x*|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**o **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] También se podrían tomar otras medidas, dependiendo del atributo que se solicite.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 El Administrador de controladores asigna esto a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt**, según corresponda. La siguiente llamada a **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 dará lugar al Administrador de controladores a realizar la siguiente asignación (conceptual, sin comprobación de errores):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 El Administrador de controladores asigna esto a **SQLSetPos**. La siguiente llamada a **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Si el Operación argumento es SQL_ADD, el Administrador de controladores llama a **SQLSetPos** de la siguiente manera:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Si el operación argumento no es SQL_ADD, el controlador devuelve SQLSTATE HY092 (identificador de atributo/opción no válido).  
  
3.  Si la aplicación intenta cambiar el SQL_ATTR_ROW_STATUS_PTR entre llamadas a **SQLFetch** o **SQLFetchScroll** y **SQLBulkOperations**, el Administrador de controladores devolverá SQLSTATE HY011 (atributo no se puede establecer ahora).  
  
4.  Si el Operación argumento está SQL_ADD, la aplicación debe llamar a **SQLBindCol** para enlazar los datos que se van a insertar. No puede llamar a **SQLSetDescField** o **SQLSetDescRec** para enlazar los datos que se van a insertar.  
  
5.  Si el Operación argumento es SQL_ADD y el número de filas que se van a insertar no es el mismo que el tamaño actual del conjunto de filas, **SQLSetStmtAttr** debe llamarse para establecer el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se insertarán antes de llamar a **SQLBulkOperations**. Para volver al tamaño del conjunto de filas anterior, la aplicación debe establecer el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE antes de **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** se llama.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 El Administrador de controladores asigna esto a **SQLColAttributes**. La siguiente llamada a **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Si *FieldIdentifier* es uno de los siguientes:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX o SQL_DESC_LOCAL_TYPE_NAME  
  
     el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY091 (identificador de campo descriptor no válido). No se aplican más reglas de esta sección.  
  
2.  El Administrador de controladores asigna SQL_COLUMN_COUNT, SQL_COLUMN_NAME o SQL_COLUMN_NULLABLE a SQL_DESC_COUNT, SQL_DESC_NAME o SQL_DESC_NULLABLE, respectivamente. (Un controlador ODBC *2.x* solo necesita admitir SQL_COLUMN_COUNT, SQL_COLUMN_NAME y SQL_COLUMN_NULLABLE, no SQL_DESC_COUNT, SQL_DESC_NAME y SQL_DESC_NULLABLE.) La llamada a SQLColAttribute se asigna a:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Todos los demás valores *FieldIdentifier* se pasan al controlador, con **SQLColAttribute** asignado a **SQLColAttributes** como se muestra anteriormente.  
  
4.  Si *BufferLength* es menor que 0, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY090 (cadena no válida o longitud de búfer). No se aplican más reglas de esta sección.  
  
5.  Si *FieldIdentifier* es SQL_DESC_CONCISE_TYPE y el tipo devuelto es un tipo de datos datetime conciso, el Administrador de controladores asigna los valores devueltos para los códigos de fecha, hora y marca de tiempo.  
  
6.  El Administrador de controladores realiza las comprobaciones necesarias para ver si es necesario generar SQLSTATE HY010 (error de secuencia de funciones). Si es así, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de funciones). No se aplican más reglas de esta sección.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 El Administrador de controladores asigna esto a **SQLTransact**. La siguiente llamada a **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 dará lugar al Administrador de controladores a realizar la siguiente asignación (conceptual, sin comprobación de errores):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 El Administrador de controladores asigna esto a **SQLExtendedFetch** con un *FetchOrientation* argumento de SQL_FETCH_NEXT. La siguiente llamada a **SQLFetch:**  
  
```  
SQLFetch (StatementHandle);  
```  
  
 dará como resultado que el Administrador de controladores llame a **SQLExtendedFetch**, como se indica a continuación:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 En esta llamada, el argumento *pcRow* se establece en el valor al que la aplicación establece el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR mediante una llamada a **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Cuando la aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR para que apunte a una matriz de estado, el Administrador de controladores almacena en caché el puntero. *RowStatusArray* puede ser igual a un puntero nulo.  
  
 Si el controlador no admite **SQLExtendedFetch** y se carga la biblioteca de cursores, el Administrador de controladores utiliza **SQLExtendedFetch** de la biblioteca de cursores para asignar **SQLFetch** a **SQLExtendedFetch**. Si el controlador no admite **SQLExtendedFetch** y no se carga la biblioteca de cursores, el Administrador de controladores pasa la llamada a **SQLFetch** al controlador. Si la aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR, el Administrador de controladores se asegura de que se rellena la matriz. Si la aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROWS_FETCHED_PTR, el Administrador de controladores establece este campo en 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 El Administrador de controladores asigna esto a **SQLExtendedFetch**. La siguiente llamada a **SQLFetchScroll:**  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Cuando la aplicación llama a **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR (que establece el campo SQL_DESC_ARRAY_STATUS_PTR en el IRD) para que apunte a una matriz de estado, el Administrador de controladores almacena en caché este puntero. Deje que este puntero sea *RowStatusArray*; de lo contrario, deje que *RowStatusArray* sea igual a un puntero nulo. Si el *RowStatusArray* argumento se establece en un puntero nulo, el Administrador de controladores genera una matriz de estado de fila.  
  
2.  Si *FetchOrientation* no es uno de SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST o SQL_FETCH_BOOKMARK, el Administrador de controladores vuelve con SQL_ERROR y SQLSTATE HY106 (tipo de captura fuera del intervalo). No se aplican más reglas de esta sección.  
  
3.  Caso:  
  
-   Si *FetchOrientation* es igual a SQL_FETCH_BOOKMARK, entonces:  
  
    -   Si **SQLSetStmtAttr** se llamó anteriormente para establecer el valor de SQL_ATTR_FETCH_BOOKMARK_PTR, deje *Bmk* ser el valor obtenido mediante la desreferenciación del puntero SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   De lo contrario, devuelva SQL_ERROR con SQLSTATE HY111 (valor de marcador no válido). No se aplican más reglas de esta sección.  
  
     El Administrador de controladores ahora llama a **SQLExtendedFetch**, como se indica a continuación:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   De lo contrario, el Administrador de controladores llama a **SQLExtendedFetch**, como se indica a continuación:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     En estas llamadas, el argumento *pcRow* se establece en el valor al que la aplicación establece el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR mediante una llamada a **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE se asigna a SQL_ROWSET_SIZE.  
  
-   Si *rc* es igual a SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, y si *FetchOrientation* es igual a SQL_FETCH_BOOKMARK y *FetchOffset* no es igual a 0, el Administrador de controladores publica una advertencia, SQLSTATE 01S10 (Intento de capturar mediante un desplazamiento de marcador, el valor de desplazamiento ignorado) y devuelve SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 El Administrador de controladores asigna esto a **SQLFreeEnv**, **SQLFreeConnect**o **SQLFreeStmt** según corresponda. La siguiente llamada a **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 dará lugar al Administrador de controladores a realizar la siguiente asignación (conceptual, sin comprobación de errores):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 El Administrador de controladores asigna esto a **SQLGetConnectOption**. La siguiente llamada a **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Si *Attribute* no es una conexión definida por el controlador o un atributo de instrucción y no es un atributo definido en ODBC *2.x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido). No se aplican más reglas en esta sección.  
  
2.  Si *Attribute* es igual a SQL_ATTR_AUTO_IPD o SQL_ATTR_METADATA_ID, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido).  
  
3.  El Administrador de controladores realiza las comprobaciones necesarias para ver si es necesario generar SQLSTATE 08003 (Conexión no abierta) o SQLSTATE HY010 (error de secuencia de funciones). Si es así, el Administrador de controladores devuelve SQL_ERROR y publica el mensaje de error adecuado. No se aplican más reglas de esta sección.  
  
4.  El Administrador de controladores llama a **SQLGetConnectOption** de la siguiente manera:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Tenga en cuenta que el *BufferLength* y *StringLengthPtr* se omiten.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* llama a **SQLGetData** con el *ColumnNumber* argumento igual a 0, el Administrador de controladores ODBC *3.x* asigna esto a una llamada a **SQLGetStmtOption** con el *Option* atributo establecido en SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 El Administrador de controladores asigna esto a **SQLGetStmtOption**. La siguiente llamada a **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Si *Attribute* no es una conexión definida por el controlador o un atributo de instrucción y no es un atributo definido en ODBC *2.x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido). No se aplican más reglas en esta sección.  
  
2.  Si *Atributo* es uno de los siguientes:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido). No se aplican más reglas de esta sección.  
  
3.  El Administrador de controladores realiza las comprobaciones necesarias para ver si es necesario generar SQLSTATE HY010 (error de secuencia de funciones). Si es así, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de funciones). No se aplican más reglas de esta sección.  
  
4.  Si *Attribute* es igual a SQL_ATTR_ROWS_FETCHED_PTR, el Administrador de controladores devuelve un puntero a la variable interna del Administrador de controladores *cRow*, que ha utilizado o usará en una llamada a **SQLExtendedFetch**. No se aplican más reglas de esta sección.  
  
5.  Si *Attribute* es igual a SQL_DESC_FETCH_BOOKMARK_PTR, el Administrador de controladores devuelve el puntero adecuado que había almacenado en caché durante una llamada a **SQLSetStmtAttr**.  
  
6.  Si *Attribute* es igual a SQL_ATTR_ROW_STATUS_PTR, el Administrador de controladores devuelve el puntero adecuado que había almacenado en caché durante una llamada a **SQLSetStmtAttr**.  
  
7.  El Administrador de controladores llama a **SQLGetStmtOption** de la siguiente manera:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     donde *hstmt*, *fOption*y *pvParam* se establecerán en los valores de *StatementHandle*, *Attribute*y *ValuePtr*, respectivamente. El *BufferLength* y *StringLengthPtr* se omiten.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 El Administrador de controladores asigna esto a **SQLSetConnectOption**. La siguiente llamada a **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Si *Attribute* no es una conexión definida por el controlador o un atributo de instrucción y no es un atributo definido en ODBC *2.x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido). No se aplican más reglas en esta sección.  
  
2.  Si *Attribute* es igual a SQL_ATTR_AUTO_IPD, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido).  
  
3.  El Administrador de controladores realiza las comprobaciones necesarias para ver si es necesario generar SQLSTATE 08003 (conexión no abierta) o SQLSTATE HY010 (error de secuencia de funciones). Si es necesario generar uno de estos errores, el Administrador de controladores devuelve SQL_ERROR y publica el mensaje de error adecuado. No se aplican más reglas de esta sección.  
  
4.  El Administrador de controladores llama a **SQLSetConnectOption** de la siguiente manera:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     donde *hdbc*, *fOption*y *vParam* se establecerán en los valores de *ConnectionHandle*, *Attribute*y *ValuePtr*, respectivamente. *StringLengthPtr* se omite.  
  
> [!NOTE]  
>  La capacidad de establecer atributos de instrucción en el nivel de conexión ha quedado en desuso. Los atributos de instrucción nunca deben establecerse en el nivel de conexión mediante una aplicación ODBC *3.x.*  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 El Administrador de controladores asigna esto a **SQLSetStmtOption**. La siguiente llamada a **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 dará lugar a la siguiente secuencia de pasos:  
  
1.  Si *Attribute* no es una conexión definida por el controlador o un atributo de instrucción y no es un atributo definido en ODBC *2.x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido). No se aplican más reglas en esta sección.  
  
2.  Si *Atributo* es uno de los siguientes:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo/opción no válido). No se aplican más reglas de esta sección.  
  
3.  El Administrador de controladores realiza las comprobaciones necesarias para ver si es necesario generar SQLSTATE HY010 (error de secuencia de funciones). Si es así, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de funciones). No se aplican más reglas de esta sección.  
  
4.  Si *Attribute* es igual a SQL_ATTR_PARAMSET_SIZE o SQL_ATTR_PARAMS_PROCESSED_PTR, vea la sección "Mappings for Handling Parameter Arrays", más adelante en este tema. No se aplican más reglas de esta sección.  
  
5.  Si *Attribute* es igual a SQL_ATTR_ROWS_FETCHED_PTR, el Administrador de controladores almacena en caché el valor del puntero para su uso posterior con **SQLFetchScroll**.  
  
6.  Si *Attribute* es igual a SQL_ATTR_ROW_STATUS_PTR, el Administrador de controladores almacena en caché el valor del puntero para su uso posterior con **SQLFetchScroll** o **SQLSetPos**. No se aplican más reglas de esta sección.  
  
7.  Si *Attribute* es igual a SQL_ATTR_FETCH_BOOKMARK_PTR, el Administrador de controladores almacena en caché *ValuePtr* y usará el valor almacenado en caché más adelante en una llamada a **SQLFetchScroll**. No se aplican más reglas de esta sección.  
  
8.  El Administrador de controladores llama a **SQLSetStmtOption** de la siguiente manera:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     donde *hstmt*, *fOption*y *vParam* se establecerán en los valores de *StatementHandle*, *Attribute*y *ValuePtr*, respectivamente. Se omite el argumento *StringLength.*  
  
     Si un controlador ODBC *2.x* admite opciones de instrucción específica de controlador de cadena de caracteres, una aplicación ODBC *3.x* debe llamar a **SQLSetStmtOption** para establecer esas opciones.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Asignaciones para el manejo de matrices de parámetros  
 Cuando la aplicación llama:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 el Administrador de conductores llama:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 Más adelante, el Administrador de controladores devuelve un puntero a esta variable cuando la aplicación llama a **SQLGetStmtAttr** para recuperar SQL_ATTR_PARAMS_PROCESSED_PTR. El Administrador de controladores no puede cambiar esta variable interna hasta que el identificador de instrucción se devuelve al estado preparado o asignado.  
  
 Una aplicación ODBC *3.x* puede llamar a **SQLGetStmtAttr** para obtener el valor de SQL_ATTR_PARAMS_PROCESSED_PTR aunque no ha establecido explícitamente el campo de SQL_DESC_ARRAY_SIZE en el APD. Esta situación podría surgir, por ejemplo, si la aplicación tiene una rutina genérica que comprueba la "fila" actual de los parámetros que se procesan cuando **SQLExecute** devuelve SQL_NEED_DATA. Esta rutina se invoca independientemente de si el SQL_DESC_ARRAY_SIZE es 1 o es mayor que 1. Para tener en cuenta esto, el Administrador de controladores tendrá que definir esta variable interna si la aplicación ha llamado **SQLSetStmtAttr** para establecer el campo de SQL_DESC_ARRAY_SIZE en APD. Si no se ha establecido SQL_DESC_ARRAY_SIZE, el Administrador de controladores tiene que asegurarse de que esta variable contiene el valor 1 antes de devolver desde **SQLExecDirect** o **SQLExecute**.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 En ODBC *3.x*, llamar a **SQLFetch** o **SQLFetchScroll** rellena el SQL_DESC_ARRAY_STATUS_PTR en el IRD y el campo SQL_DIAG_ROW_NUMBER de un registro de diagnóstico determinado contiene el número de la fila del conjunto de filas que pertenece a este registro. Con esto, la aplicación puede correlacionar un mensaje de error con una posición de fila determinada.  
  
 Un controlador ODBC *2.x* no podrá proporcionar esta funcionalidad. Sin embargo, proporcionará demarcación de errores con SQLSTATE 01S01 (Error en la fila). Una aplicación ODBC *3.x* que usa **SQLFetch** o **SQLFetchScroll** mientras va en contra de un controlador ODBC *2.x* debe ser consciente de este hecho. Tenga en cuenta también que una aplicación de este tipo no podrá llamar a **SQLGetDiagField** para obtener realmente el campo SQL_DIAG_ROW_NUMBER de todos modos. Una aplicación ODBC *3.x* que trabaje con un controlador ODBC *2.x* podrá llamar a **SQLGetDiagField** solo con un *DiagIdentifier* argumento de SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE o SQL_DIAG_SQLSTATE. El Administrador de controladores ODBC *3.x* mantiene la estructura de datos de diagnóstico cuando se trabaja con un controlador ODBC *2.x,* pero el controlador ODBC *2.x* devuelve solo estos cuatro campos.  
  
 Cuando una aplicación ODBC *2.x* está trabajando con un controlador ODBC *2.x,* si una operación puede provocar que el Administrador de controladores devuelva varios errores, el Administrador de controladores ODBC *3.x* puede devolver errores diferentes que el Administrador de controladores ODBC *2.x.*  
  
## <a name="mappings-for-bookmark-operations"></a>Asignaciones para operaciones de marcadores  
 El Administrador de controladores ODBC *3.x* realiza las siguientes asignaciones cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* realiza operaciones de marcador.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* llama a **SQLBindCol** para enlazar a la columna 0 con *fCType* igual a SQL_C_VARBOOKMARK, el Administrador de controladores ODBC *3.x* comprueba si el *BufferLength* argumento es menor que 4 o mayor que 4 y, si es así, devuelve SQLSTATE HY090 (cadena no válida o longitud de búfer). Si el *BufferLength* argumento es igual a 4, el Administrador de controladores llama **sqlBindCol** en el controlador, después de reemplazar *fCType* con SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* llama a **SQLColAttribute** con el *ColumnNumber* argumento establecido en 0, el Administrador de controladores devuelve el *FieldIdentifier* valores enumerados en la tabla siguiente.  
  
|*FieldIdentifier*|Value|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (cadena vacía)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|El mismo valor devuelto por **SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (cadena vacía)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (cadena vacía)|  
|SQL_DESC_LITERAL_SUFFIX|"" (cadena vacía)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (cadena vacía)|  
|SQL_DESC_NAME|"" (cadena vacía)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (cadena vacía)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (cadena vacía)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (cadena vacía)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* llama a **SQLDescribeCol** con el *ColumnNumber* argumento establecido en 0, el Administrador de controladores devuelve los valores enumerados en la tabla siguiente.  
  
|Buffer|Value|  
|------------|-----------|  
|ColumnName|"" (cadena vacía)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* realiza la siguiente llamada a **SQLGetData** para recuperar un marcador:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 la llamada se asigna a **SQLGetStmtOption** con un *fOption* de SQL_GET_BOOKMARK, como se indica a continuación:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 donde *hstmt* y *pvParam* se establecen en los valores *de StatementHandle* y *TargetValuePtr*, respectivamente. El marcador se devuelve en el búfer al que apunta el argumento *pvParam* (*TargetValuePtr*). El valor del búfer al que apunta el *StrLen_or_IndPtr* argumento en la llamada a **SQLGetData** se establece en 4.  
  
 Esta asignación es necesaria para tener en cuenta el caso en el que **sqlFetch** se llamó antes de la llamada a **SQLGetData** y el controlador ODBC *2.x* no admitía **SQLExtendedFetch**. En este caso, **SQLFetch** se pasaría a través del controlador ODBC *2.x,* en cuyo caso no se admite la recuperación de marcadores.  
  
 **SQLGetData** no se puede llamar varias veces en un controlador ODBC *2.x* para recuperar un marcador en partes, por lo que llamar a **SQLGetData** con el *BufferLength* argumento establecido en un valor menor que 4 y el *ColumnNumber* argumento establecido en 0 devolverá SQLSTATE HY090 (cadena no válida o longitud de búfer). **SQLGetData,** sin embargo, se puede llamar varias veces para recuperar el mismo marcador.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* llama a **SQLSetStmtAttr** para establecer el atributo SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE, el Administrador de controladores establece el atributo en SQL_UB_ON en el controlador ODBC *2.x* subyacente.
