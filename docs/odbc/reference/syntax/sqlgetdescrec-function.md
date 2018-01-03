---
title: "Sqlgetdescrec, función | Documentos de Microsoft"
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
apiname: SQLGetDescRec
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetDescRec
helpviewer_keywords: SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569a3708c13a4182e651c902ce7e1f1f9c7711dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdescrec-function"></a>Sqlgetdescrec, función
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLGetDescRec** devuelve la configuración actual o los valores de varios campos de un registro del descriptor. Describen los campos que devuelve el nombre, el tipo de datos y el almacenamiento de datos de columna o parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Identificador de descriptor.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de descriptor de la que la aplicación busca información. Registros del descriptor se numeran del 1, con el número de registro 0 es el registro de marcador. El *RecNumber* argumento debe ser menor o igual que el valor de SQL_DESC_COUNT. Si *RecNumber* es menor o igual que SQL_DESC_COUNT, pero la fila no contiene datos de una columna o parámetro, una llamada a **SQLGetDescRec** devolverá los valores predeterminados de los campos. (Para obtener más información, vea "Inicialización de campos de Descriptor" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Nombre*  
 [Salida] Un puntero a un búfer en el que se va a devolver el campo SQL_DESC_NAME para el registro del descriptor.  
  
 Si *nombre* es NULL, *StringLengthPtr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por  *Nombre*.  
  
 *BufferLength*  
 [Entrada] Longitud de la **nombre* búfer en caracteres.  
  
 *StringLengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el número de caracteres de datos disponibles para devolver en el \* *nombre* búfer, excluido el carácter de terminación null. Si el número de caracteres es mayor o igual que *BufferLength*, los datos de \* *nombre* se trunca a *BufferLength* menos la longitud de un carácter de terminación NULL y termina en null el controlador.  
  
 *TypePtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_TYPE para el registro del descriptor.  
  
 *SubTypePtr*  
 [Salida] Para los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL, esto es un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_OCTET_LENGTH para el registro del descriptor.  
  
 *PrecisionPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_PRECISION para el registro del descriptor.  
  
 *ScalePtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_SCALE para el registro del descriptor.  
  
 *NullablePtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_NULLABLE para el registro del descriptor.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 Si se devuelve SQL_NO_DATA *RecNumber* es mayor que el número actual de registros de descriptor.  
  
 Si se devuelve SQL_NO_DATA *DescriptorHandle* es un identificador IRD y la instrucción está en el estado preparado o ejecutado pero no se produjo ningún cursor abierto asociado con él.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetDescRec** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DESC y un *controlar* de *DescriptorHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLGetDescRec** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|El búfer \* *nombre* no era lo suficientemente grande como para devolver el campo descriptor completo. Por lo tanto, el campo se ha truncado. Se devuelve la longitud del campo descriptor untruncated en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07009|Índice de descriptor no válido|El *FieldIdentifier* argumento era un campo de registro, el *RecNumber* argumento se establece en 0 y el *DescriptorHandle* argumento era un identificador IPD.<br /><br /> (DM) la *RecNumber* argumento se establece en 0 y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF y el *DescriptorHandle* argumento era un identificador IRD.<br /><br /> El *RecNumber* argumento era menor que 0.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY007|La instrucción asociada no está preparada|*DescriptorHandle* se asoció con un IRD, y el identificador de instrucción asociado no estaba en estado preparado o ejecutado.|  
|HY010|Error de secuencia de función|(DM) *DescriptorHandle* se asoció una *StatementHandle* para que se llamó a una función que se ejecuta asincrónicamente (no esta uno) y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) *DescriptorHandle* se asoció una *StatementHandle* que **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, o **SQLSetPos** se llama y se devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *DescriptorHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLGetDescRec** se llamó.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLGetDescRec** para recuperar los valores de los siguientes campos de descriptor de una sola columna o parámetro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** no recupera los valores de campos de encabezado.  
  
 Una aplicación puede evitar que la devolución del valor de un campo estableciendo el argumento correspondiente en el campo a un puntero null.  
  
 Cuando una aplicación llama **SQLGetDescRec** para recuperar el valor de un campo que no está definido para un tipo de descriptor determinado, la función devuelve SQL_SUCCESS, pero el valor devuelto para el campo es indefinido. Por ejemplo, al llamar a **SQLGetDescRec** para el campo SQL_DESC_NAME o SQL_DESC_NULLABLE de un APD o descartar devolverá SQL_SUCCESS, pero un valor no definido para el campo.  
  
 Cuando una aplicación llama **SQLGetDescRec** para recuperar el valor de un campo que se define para un tipo de descriptor particular pero que no tiene ningún valor predeterminado y no se ha establecido aún, la función devuelve SQL_SUCCESS, pero el valor devuelto para el campo es indefinido. Para obtener más información, vea "Inicialización de campos de Descriptor" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Los valores de campos también se pueden recuperar individualmente una llamada a **SQLGetDescField**. Para obtener una descripción de los campos de un encabezado de descriptor o el registro, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obtener más información acerca de los descriptores, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtención de un campo de descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Configuración de varios campos de descriptor|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
