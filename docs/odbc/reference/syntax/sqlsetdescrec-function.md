---
title: "Sqlsetdescrec, función | Documentos de Microsoft"
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
apiname: SQLSetDescRec
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetDescRec
helpviewer_keywords: SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c817bad04757820b7c8ee83905fbc0fad08b4e26
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetdescrec-function"></a>Sqlsetdescrec, función
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 El **SQLSetDescRec** función establece varios campos de descriptor que influyen en el tipo de datos y búfer enlazado a una columna o parámetro de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Identificador de descriptor. No debe ser un identificador IRD.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de descriptor que contiene los campos que se va a establecer. Registros del descriptor se numeran de 0, con el número de registro 0 es el registro de marcador. Este argumento debe ser igual o mayor que 0. Si *RecNumber* es mayor que el valor de SQL_DESC_COUNT, SQL_DESC_COUNTis cambiado al valor de *RecNumber*.  
  
 *Tipo*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_TYPE para el registro del descriptor.  
  
 *Subtipo*  
 [Entrada] Para los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL, este es el valor que se va a establecer el campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Longitud*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_OCTET_LENGTH para el registro del descriptor.  
  
 *Precisión*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_PRECISION para el registro del descriptor.  
  
 *Escala*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_SCALE para el registro del descriptor.  
  
 *DataPtr*  
 [Diferida entrada o salida] El valor que se va a establecer el campo SQL_DESC_DATA_PTR para el registro del descriptor. *DataPtr* se puede establecer en un puntero nulo.  
  
 El *DataPtr* argumento se puede establecer en un puntero nulo para establecer el campo SQL_DESC_DATA_PTR a un puntero null. Si el identificador en el *DescriptorHandle* argumento está asociado con un descartar, este modo desenlaza la columna.  
  
 *StringLengthPtr*  
 [Diferida entrada o salida] El valor que se va a establecer el campo SQL_DESC_OCTET_LENGTH_PTR para el registro del descriptor. *StringLengthPtr* puede establecerse en un puntero nulo para establecer el campo SQL_DESC_OCTET_LENGTH_PTR en un puntero nulo.  
  
 *IndicatorPtr*  
 [Diferida entrada o salida] El valor que se va a establecer el campo SQL_DESC_INDICATOR_PTR para el registro del descriptor. *IndicatorPtr* puede establecerse en un puntero nulo para establecer el campo SQL_DESC_INDICATOR_PTR a un puntero null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetDescRec** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DESC y un *controlar* de *DescriptorHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetDescRec** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07009|Índice de descriptor no válido|El *RecNumber* argumento se establece en 0 y el *DescriptorHandle* hace referencia a un identificador de IPD.<br /><br /> El *RecNumber* argumento era menor que 0.<br /><br /> El *RecNumber* argumento era mayor que el número máximo de columnas o parámetros que el origen de datos puede admitir, y el *DescriptorHandle* argumento era un APD, IPD o descartar.<br /><br /> El *RecNumber* argumento era igual a 0 y el *DescriptorHandle* argumento hace referencia a un APD implícitamente asignado. (Este error no se produce con un descriptor de aplicación asignado explícitamente porque no se sabe si un descriptor de aplicación asignado explícitamente es un APD o descartar hasta el tiempo de ejecución.)|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) la *DescriptorHandle* se asoció una *StatementHandle* para que se llamó a una función que se ejecuta asincrónicamente (no esta uno) y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* con la que el *DescriptorHandle* se ha asociado y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *DescriptorHandle*. Esta función asincrónicas aún estaba ejecutando cuando el **SQLSetDescRec** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llama para uno de los identificadores de instrucción asociados a la *DescriptorHandle* y devuelve SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY016|No se puede modificar un descriptor de fila de implementación|El *DescriptorHandle* argumento estaba asociado con un IRD.|  
|HY021|Información de descriptor incoherente|El *tipo* campo o cualquier otro campo asociado con el campo SQL_DESC_TYPE en el descriptor, no era válido o coherente.<br /><br /> Información del descriptor de comprobarse durante una comprobación de coherencia no era coherente. (Vea "Comprobaciones de coherencia," más adelante en esta sección).|  
|HY090|Longitud de búfer o cadena no válida|(DM) el controlador fue un ODBC 2*.x* controlador, el descriptor fue un descartar la *ColumnNumber* argumento se establece en 0 y el valor especificado para el argumento *BufferLength* era no es igual a 4.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetDescRec** para establecer los siguientes campos de una sola columna o parámetro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Si una llamada a **SQLSetDescRec** se produce un error, el contenido del registro de descriptor identificado por la *RecNumber* argumento son indefinidos.  
  
 Al enlazar una columna o parámetro, **SQLSetDescRec** permite cambiar varios campos que afectan al enlace sin llamar a **SQLBindCol** o **SQLBindParameter** o realizar varias llamadas a **SQLSetDescField**. **SQLSetDescRec** pueden establecer los campos en un descriptor que no estén asociado con una instrucción. Tenga en cuenta que **SQLBindParameter** establece más campos que **SQLSetDescRec**, puede establecer los campos en un APD y un IPD en una llamada y no requiere un identificador de descriptor.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre se debe establecer antes de llamar a **SQLSetDescRec** con un *RecNumber* argumento de 0 para establecer campos de marcador. Aunque esto no es obligatorio, se recomienda encarecidamente.  
  
## <a name="consistency-checks"></a>Comprobaciones de coherencia  
 Se realiza una comprobación de coherencia con el controlador automáticamente cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR de APD, descartar o IPD. Si cualquiera de los campos no es coherente con otros campos, **SQLSetDescRec** devolverá SQLSTATE HY021 (información de descriptor incoherente).  
  
 Cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR de APD, descartar o IPD, el controlador comprueba que el valor del campo SQL_DESC_TYPE y los valores aplicables a ese campo SQL_DESC_TYPE son válidos y coherentes. Esta comprobación no es siempre realizan cuando **SQLBindParameter** o **SQLBindCol** se llama o cuando **SQLSetDescRec** se llama para APD, descartar o IPD. Esta comprobación de coherencia incluye las siguientes comprobaciones en campos de descriptor:  
  
-   El campo SQL_DESC_TYPE debe ser uno de los C de ODBC válido o tipos SQL o un tipo SQL específico del controlador. El campo SQL_DESC_CONCISE_TYPE debe ser uno de los tipos de C de ODBC o SQL válidos o un tipo específico del controlador C o SQL, incluidos los tipos datetime e interval concisos.  
  
-   Si el campo de registro SQL_DESC_TYPE es SQL_DATETIME o SQL_INTERVAL, el campo SQL_DESC_DATETIME_INTERVAL_CODE debe ser uno de los datetime válido o códigos de intervalo. (Vea la descripción del campo SQL_DESC_DATETIME_INTERVAL_CODE en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Si el campo SQL_DESC_TYPE indica un tipo numérico, se comprueban los campos SQL_DESC_PRECISION y SQL_DESC_SCALE sea válida.  
  
-   Si el campo SQL_DESC_CONCISE_TYPE es un tipo de datos de hora o marca de tiempo, un intervalo de tipo con un componente de segundos, o uno de los tipos de datos de intervalo con un componente de tiempo, se comprueba el campo SQL_DESC_PRECISION sea una precisión de segundos válida.  
  
-   Si la SQL_DESC_CONCISE_TYPE es un tipo de datos de intervalo, se comprueba el campo SQL_DESC_DATETIME_INTERVAL_PRECISION debe para ser un valor de precisión inicial del intervalo válido.  
  
 El campo SQL_DESC_DATA_PTR de una IPD no se establece normalmente; Sin embargo, una aplicación puede hacerlo para forzar una comprobación de coherencia de los campos IPD. No se puede realizar una comprobación de coherencia en un IRD. El valor que el campo SQL_DESC_DATA_PTR de la IPD se establece en no está almacenado realmente y no se puede recuperar mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**; la configuración se realiza solo para forzar la comprobación de coherencia.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtención de un campo único descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtener varios campos de descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Establecer campos de descriptor único|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
