---
title: FUNción SQLSetDescRec ( SQLSetDescRec) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b29879ff7635d6eb7d5a0f7489ff3994758d4a35
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299535"
---
# <a name="sqlsetdescrec-function"></a>Función SQLSetDescRec
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 La función **SQLSetDescRec** establece varios campos descriptores que afectan al tipo de datos y al búfer enlazados a datos de columna o parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Mango del descriptor. Esto no debe ser un identificador IRD.  
  
 *RecNumber*  
 [Entrada] Indica el registro descriptor que contiene los campos que se van a establecer. Los registros de descriptor se numeran desde 0, siendo el número de registro 0 el registro de marcador. Este argumento debe ser igual o mayor que 0. Si *RecNumber* es mayor que el valor de SQL_DESC_COUNT, SQL_DESC_COUNTis cambia al valor de *RecNumber*.  
  
 *Tipo*  
 [Entrada] Valor en el que se va a establecer el campo SQL_DESC_TYPE para el registro descriptor.  
  
 *Subtipo*  
 [Entrada] Para los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL, este es el valor al que se va a establecer el campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Duración*  
 [Entrada] Valor en el que se va a establecer el campo SQL_DESC_OCTET_LENGTH para el registro descriptor.  
  
 *Precisión*  
 [Entrada] Valor en el que se va a establecer el campo SQL_DESC_PRECISION para el registro descriptor.  
  
 *Escala*  
 [Entrada] Valor en el que se va a establecer el campo SQL_DESC_SCALE para el registro descriptor.  
  
 *DataPtr*  
 [Entrada o salida diferida] Valor en el que se va a establecer el campo SQL_DESC_DATA_PTR para el registro descriptor. *DataPtr* se puede establecer en un puntero nulo.  
  
 El *DataPtr* argumento se puede establecer en un puntero nulo para establecer el campo SQL_DESC_DATA_PTR en un puntero nulo. Si el identificador del argumento *DescriptorHandle* está asociado a un ARD, se desenlaza la columna.  
  
 *StringLengthPtr*  
 [Entrada o salida diferida] Valor en el que se va a establecer el campo SQL_DESC_OCTET_LENGTH_PTR para el registro descriptor. *StringLengthPtr* se puede establecer en un puntero nulo para establecer el campo SQL_DESC_OCTET_LENGTH_PTR en un puntero nulo.  
  
 *IndicatorPtr*  
 [Entrada o salida diferida] Valor en el que se va a establecer el campo SQL_DESC_INDICATOR_PTR para el registro descriptor. *IndicatorPtr* se puede establecer en un puntero nulo para establecer el campo SQL_DESC_INDICATOR_PTR en un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetDescRec** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DESC y un *identificador* de *DescriptorHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLSetDescRec** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice de descriptor no válido|El *RecNumber* argumento se estableció en 0, y el *DescriptorHandle* hace referencia a un identificador IPD.<br /><br /> El *argumento RecNumber* era menor que 0.<br /><br /> El *RecNumber* argumento era mayor que el número máximo de columnas o parámetros que el origen de datos puede admitir y el *DescriptorHandle* argumento era un APD, IPD o ARD.<br /><br /> El *RecNumber* argumento era igual a 0, y el *DescriptorHandle* argumento hace referencia a un APD asignado implícitamente. (Este error no se produce con un descriptor de aplicación asignado explícitamente porque no se sabe si un descriptor de aplicación asignado explícitamente es un APD o ARD hasta el tiempo de ejecución.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) el *DescriptorHandle* se asoció con un *StatementHandle* para el que se llamó a una función de ejecución asincrónica (no esta) y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* con el que el *DescriptorHandle* se asoció y devolvió SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *DescriptorHandle*. Esta función anócrona todavía se estaba ejecutando cuando se llamó a la función **SQLSetDescRec** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *DescriptorHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY016|No se puede modificar un descriptor de fila de implementación|El *descriptorHandle* argumento se asoció con un IRD.|  
|HY021|Información de descriptorina incoherente|El campo *Tipo,* o cualquier otro campo asociado con el campo SQL_DESC_TYPE del descriptor, no era válido ni coherente.<br /><br /> La información del descriptor comprobada durante una comprobación de coherencia no era coherente. (Consulte "Comprobaciones de coherencia", más adelante en esta sección.)|  
|HY090|Cadena no válida o longitud de búfer|(DM) el controlador era un controlador ODBC *2.x,* el descriptor era un ARD, el *ColumnNumber* argumento se estableció en 0, y el valor especificado para el argumento *BufferLength* no era igual a 4.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetDescRec** para establecer los siguientes campos para una sola columna o parámetro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Si se produce un error en una llamada a **SQLSetDescRec,** el contenido del registro descriptor identificado por el *RecNumber* argumento es indefinido.  
  
 Al enlazar una columna o parámetro, **SQLSetDescRec** permite cambiar varios campos que afectan al enlace sin llamar a **SQLBindCol** o **SQLBindParameter** o realizar varias llamadas a **SQLSetDescField**. **SQLSetDescRec** puede establecer campos en un descriptor no asociado actualmente a una instrucción. Tenga en cuenta que **SQLBindParameter** establece más campos que **SQLSetDescRec**, puede establecer campos en un APD y un IPD en una llamada y no requiere un identificador de descriptor.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre debe establecerse antes de llamar a **SQLSetDescRec** con un *RecNumber* argumento de 0 para establecer campos de marcador. Aunque esto no es obligatorio, se recomienda encarecidamente.  
  
## <a name="consistency-checks"></a>Comprobaciones de coherencia  
 El controlador realiza automáticamente una comprobación de coherencia cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR de un APD, ARD o IPD. Si alguno de los campos es incoherente con otros campos, **SQLSetDescRec** devolverá SQLSTATE HY021 (información de descriptor incoherente).  
  
 Cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR de un APD, ARD o IPD, el controlador comprueba que el valor del campo SQL_DESC_TYPE y los valores aplicables a ese campo de SQL_DESC_TYPE son válidos y coherentes. Esta comprobación siempre se realiza cuando **SQLBindParameter** o **SQLBindCol** se llama o cuando **SQLSetDescRec** se llama para un APD, ARD o IPD. Esta comprobación de coherencia incluye las siguientes comprobaciones en los campos descriptores:  
  
-   El campo SQL_DESC_TYPE debe ser uno de los tipos ODBC C o SQL válidos o un tipo SQL específico del controlador. El campo SQL_DESC_CONCISE_TYPE debe ser uno de los tipos ODBC C o SQL válidos o un tipo C o SQL específico del controlador, incluidos los tipos concisos datetime e interval.  
  
-   Si el campo de registro SQL_DESC_TYPE es SQL_DATETIME o SQL_INTERVAL, el campo SQL_DESC_DATETIME_INTERVAL_CODE debe ser uno de los códigos de fecha y hora o intervalo válidos. (Consulte la descripción del campo SQL_DESC_DATETIME_INTERVAL_CODE en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Si el campo SQL_DESC_TYPE indica un tipo numérico, se verifica que los campos SQL_DESC_PRECISION y SQL_DESC_SCALE son válidos.  
  
-   Si el campo SQL_DESC_CONCISE_TYPE es un tipo de datos de tiempo o marca de tiempo, un tipo de intervalo con un componente de segundos o uno de los tipos de datos de intervalo con un componente de tiempo, se comprueba que el campo de SQL_DESC_PRECISION es una precisión de segundos válida.  
  
-   Si el SQL_DESC_CONCISE_TYPE es un tipo de datos de intervalo, se comprueba que el campo SQL_DESC_DATETIME_INTERVAL_PRECISION es un valor de precisión inicial de intervalo válido.  
  
 El campo SQL_DESC_DATA_PTR de una IPD no se establece normalmente; sin embargo, una aplicación puede hacerlo para forzar una comprobación de coherencia de los campos IPD. No se puede realizar una comprobación de coherencia en un IRD. El valor en el que se establece el campo SQL_DESC_DATA_PTR de la IPD no se almacena realmente y no se puede recuperar mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**; el ajuste se realiza únicamente para forzar la comprobación de coherencia.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtener un único campo descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtención de varios campos descriptores|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de campos de descriptor único|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
