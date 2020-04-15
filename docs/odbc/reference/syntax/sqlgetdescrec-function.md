---
title: FUNción SQLGetDescRec ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87d7b971b379f19f8451e924932a5e699e9b9983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285490"
---
# <a name="sqlgetdescrec-function"></a>Función SQLGetDescRec
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLGetDescRec** devuelve la configuración actual o los valores de varios campos de un registro descriptor. Los campos devueltos describen el nombre, el tipo de datos y el almacenamiento de datos de columna o parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Mango del descriptor.  
  
 *RecNumber*  
 [Entrada] Indica el registro descriptor desde el que la aplicación busca información. Los registros de descriptor se numeran desde 1, siendo el número de registro 0 el registro de marcador. El *RecNumber* argumento debe ser menor o igual que el valor de SQL_DESC_COUNT. Si *RecNumber* es menor o igual que SQL_DESC_COUNT pero la fila no contiene datos para una columna o parámetro, una llamada a **SQLGetDescRec** devolverá los valores predeterminados de los campos. (Para obtener más información, vea "Inicialización de campos [descriptores" en SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *Nombre*  
 [Salida] Puntero a un búfer en el que se va a devolver el campo SQL_DESC_NAME para el registro descriptor.  
  
 Si *Name* es NULL, *StringLengthPtr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer al que apunta *Name*.  
  
 *BufferLength*  
 [Entrada] Longitud del búfer **Nombre,* en caracteres.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a \*devolver el número de caracteres de datos disponibles para devolver en el búfer *Name,* excluyendo el carácter de terminación nula. Si el número de caracteres era mayor o igual que *BufferLength*, los datos de \* *Name* se truncan en *BufferLength* menos la longitud de un carácter de terminación nula y el controlador termina en null.  
  
 *TypePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_TYPE para el registro descriptor.  
  
 *SubTypePtr*  
 [Salida] Para los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL, se trata de un puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *LengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_OCTET_LENGTH para el registro descriptor.  
  
 *PrecisionPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_PRECISION para el registro descriptor.  
  
 *ScalePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_SCALE para el registro descriptor.  
  
 *NullablePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor del campo SQL_DESC_NULLABLE para el registro descriptor.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA se devuelve si *RecNumber* es mayor que el número actual de registros descriptores.  
  
 SQL_NO_DATA se devuelve si *DescriptorHandle* es un identificador IRD y la instrucción está en estado preparado o ejecutado, pero no había ningún cursor abierto asociado a él.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetDescRec** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DESC y un *identificador* de *DescriptorHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLGetDescRec** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \* *nombre* del búfer no era lo suficientemente grande como para devolver todo el campo descriptor. Por lo tanto, el campo se truncó. La longitud del campo descriptor no truncado se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice de descriptor no válido|El argumento *FieldIdentifier* era un campo de registro, el argumento *RecNumber* se estableció en 0 y el argumento *DescriptorHandle* era un identificador IPD.<br /><br /> (DM) el *RecNumber* argumento se estableció en 0, y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF y el *DescriptorHandle* argumento era un identificador IRD.<br /><br /> El *argumento RecNumber* era menor que 0.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY007|La declaración asociada no está preparada|*DescriptorHandle* se asoció con un IRD y el identificador de instrucción asociado no estaba en el estado preparado o ejecutado.|  
|HY010|Error de secuencia de funciones|DescriptorHandle *DescriptorHandle* se asoció con un *StatementHandle* para el que se llamó a una función de ejecución asincrónica (no a esta) y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> DescriptorHandle *DescriptorHandle* (DM) se asoció a un *StatementHandle* para el que **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó y devolvió SQL_NEED_DATA . Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *DescriptorHandle*. Esta función asincrónica todavía se estaba ejecutando cuando **SQLGetDescRec** se llamó.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado a *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLGetDescRec** para recuperar los valores de los siguientes campos descriptores para una sola columna o parámetro:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** no recupera los valores de los campos de encabezado.  
  
 Una aplicación puede impedir la devolución de la configuración de un campo estableciendo el argumento que corresponde al campo en un puntero nulo.  
  
 Cuando una aplicación llama a **SQLGetDescRec** para recuperar el valor de un campo que no está definido para un tipo de descriptor determinado, la función devuelve SQL_SUCCESS pero el valor devuelto para el campo es indefinido. Por ejemplo, llamar a **SQLGetDescRec** para el SQL_DESC_NAME o SQL_DESC_NULLABLE campo de un APD o ARD devolverá SQL_SUCCESS pero un valor indefinido para el campo.  
  
 Cuando una aplicación llama a **SQLGetDescRec** para recuperar el valor de un campo que se define para un tipo de descriptor determinado pero que no tiene ningún valor predeterminado y aún no se ha establecido, la función devuelve SQL_SUCCESS pero el valor devuelto para el campo es indefinido. Para obtener más información, vea "Inicialización de campos [descriptores" en SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Los valores de los campos también se pueden recuperar individualmente mediante una llamada a **SQLGetDescField**. Para obtener una descripción de los campos de un encabezado o registro descriptor, vea [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obtener más información acerca de los descriptores, consulte [Descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtener un campo descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Configuración de varios campos descriptores|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
