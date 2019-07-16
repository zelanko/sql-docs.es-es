---
title: Función SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a733c2b88954c9937e8a170b949535ffa118bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039733"
---
# <a name="sqlsetdescrec-function"></a>Función SQLSetDescRec
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ISO 92  
  
 **Resumen**  
 El **SQLSetDescRec** función establece varios campos de descriptor que afectan al tipo de datos y búfer a una columna o parámetro de datos enlazados.  
  
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
 [Entrada] Identificador de descriptor. No debe ser un identificador IRD.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de descriptor que contiene los campos que se puede establecer. Registros de descriptor se numeran de 0, con el número de registro 0 es el registro del marcador. Este argumento debe ser igual o mayor que 0. Si *RecNumber* es mayor que el valor de SQL_DESC_COUNT, SQL_DESC_COUNTis cambiado al valor de *RecNumber*.  
  
 *Tipo*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_TYPE para el registro del descriptor.  
  
 *SubType*  
 [Entrada] Los registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL, este es el valor que se va a establecer el campo SQL_DESC_DATETIME_INTERVAL_CODE.  
  
 *Longitud*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_OCTET_LENGTH para el registro del descriptor.  
  
 *Precisión*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_PRECISION para el registro del descriptor.  
  
 *Escala*  
 [Entrada] El valor que se va a establecer el campo SQL_DESC_SCALE para el registro del descriptor.  
  
 *DataPtr*  
 [Diferido entrada o salida] El valor que se va a establecer el campo SQL_DESC_DATA_PTR para el registro del descriptor. *DataPtr* se puede establecer en un puntero nulo.  
  
 El *DataPtr* argumento se puede establecer en un puntero nulo para establecer el campo SQL_DESC_DATA_PTR en un puntero nulo. Si el identificador en el *DescriptorHandle* argumento está asociado con un descartar, esto desenlaza la columna.  
  
 *StringLengthPtr*  
 [Diferido entrada o salida] El valor que se va a establecer el campo SQL_DESC_OCTET_LENGTH_PTR para el registro del descriptor. *StringLengthPtr* se puede establecer en un puntero nulo para establecer el campo SQL_DESC_OCTET_LENGTH_PTR en un puntero nulo.  
  
 *IndicatorPtr*  
 [Diferido entrada o salida] El valor que se va a establecer el campo SQL_DESC_INDICATOR_PTR para el registro del descriptor. *IndicatorPtr* se puede establecer en un puntero nulo para establecer el campo SQL_DESC_INDICATOR_PTR a un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetDescRec** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DESC y un *controlar* de *DescriptorHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetDescRec** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07009|Índice de descriptor no válido|El *RecNumber* argumento se establece en 0 y el *DescriptorHandle* hace referencia a un identificador de IPD.<br /><br /> El *RecNumber* argumento era menor que 0.<br /><br /> El *RecNumber* argumento era mayor que el número máximo de columnas o parámetros que puede admitir el origen de datos, y el *DescriptorHandle* argumento era un APD, IPD o descartar.<br /><br /> El *RecNumber* argumento era igual a 0 y el *DescriptorHandle* argumento hace referencia a un APD implícitamente asignado. (Este error no se produce con un descriptor de aplicación asignados explícitamente porque no se sabe si un descriptor de aplicación asignados explícitamente es un APD o descartar hasta el tiempo de ejecución.)|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) el *DescriptorHandle* asoció un *StatementHandle* para que se llamó a una función que se ejecuta asincrónicamente (no esta uno) y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* con el que el *DescriptorHandle* se ha asociado y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *DescriptorHandle*. Esta función asincrónicas aún estaba ejecutando cuando el **SQLSetDescRec** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *DescriptorHandle* y devuelve SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY016|No se puede modificar un descriptor de fila de implementación|El *DescriptorHandle* argumento estaba asociado con un IRD.|  
|HY021|Información de descriptor incoherente|El *tipo* campo, o cualquier otro campo asociado con el campo SQL_DESC_TYPE en el descriptor, no era válido o coherente.<br /><br /> Información del descriptor de comprobar durante una comprobación de coherencia no era coherente. (Vea "Comprobaciones de coherencia," más adelante en esta sección).|  
|HY090|Longitud de búfer o cadena no válida|(DM) el controlador fue un ODBC *2.x* controlador, el descriptor era un descartar la *ColumnNumber* argumento se establece en 0 y el valor especificado para el argumento *BufferLength* era no es igual a 4.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetDescRec** para establecer los siguientes campos de una sola columna o parámetro:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (para registros cuyo tipo es SQL_DATETIME o SQL_INTERVAL)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  Si una llamada a **SQLSetDescRec** produce un error, el contenido del registro de descriptor identificado por el *RecNumber* argumento son indefinidos.  
  
 Al enlazar una columna o parámetro, **SQLSetDescRec** le permite cambiar varios campos que afectan al enlace sin llamar a **SQLBindCol** o **SQLBindParameter** o realizar varias llamadas a **SQLSetDescField**. **SQLSetDescRec** puede establecer los campos en un descriptor que no estén asociado con una instrucción. Tenga en cuenta que **SQLBindParameter** establece más campos que **SQLSetDescRec**, puede establecer los campos en un APD y un IPD en una llamada y no requiere un identificador de descriptor.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre se debe establecer antes de llamar a **SQLSetDescRec** con un *RecNumber* argumento de 0 para establecer los campos de marcador. Aunque esto no es obligatorio, se recomienda encarecidamente.  
  
## <a name="consistency-checks"></a>Comprobaciones de coherencia  
 Se realiza una comprobación de coherencia por el controlador automáticamente cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR de IPD, descartar o APD. Si cualquiera de los campos no es coherente con otros campos, **SQLSetDescRec** devolverá SQLSTATE HY021 (información de descriptor incoherente).  
  
 Cada vez que una aplicación establece el campo SQL_DESC_DATA_PTR de APD, descartar o IPD, el controlador comprueba que el valor del campo SQL_DESC_TYPE y los valores aplicables a ese campo SQL_DESC_TYPE son válidos y coherentes. Esta comprobación es siempre realiza cuando **SQLBindParameter** o **SQLBindCol** se denomina o cuando **SQLSetDescRec** se llama para APD, descartar o IPD. Esta comprobación de coherencia incluye las siguientes comprobaciones en los campos de descriptor:  
  
-   El campo SQL_DESC_TYPE debe ser uno de la C de ODBC válida o tipos de SQL o un tipo SQL específicas del controlador. El campo SQL_DESC_CONCISE_TYPE debe ser uno de los tipos válidos de C de ODBC o SQL o un tipo específico del controlador C o SQL, incluidos los tipos datetime e interval concisos.  
  
-   Si el campo SQL_DESC_TYPE de registro es SQL_DATETIME o SQL_INTERVAL, el campo SQL_DESC_DATETIME_INTERVAL_CODE debe ser uno de los datetime válido o códigos de intervalo. (Vea la descripción del campo en SQL_DESC_DATETIME_INTERVAL_CODE [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
-   Si el campo SQL_DESC_TYPE indica un tipo numérico, se comprueban los campos de SQL_DESC_PRECISION y SQL_DESC_SCALE sea válido.  
  
-   Si el campo SQL_DESC_CONCISE_TYPE es un tipo de datos de hora o marca de tiempo, un intervalo de tipo con un componente de segundos, o uno de los tipos de datos de intervalo con un componente de tiempo, se comprueba el campo SQL_DESC_PRECISION sea una precisión de segundos válido.  
  
-   Si el SQL_DESC_CONCISE_TYPE es un tipo de datos de intervalo, se comprueba el campo SQL_DESC_DATETIME_INTERVAL_PRECISION para ser un valor de precisión inicial del intervalo válido.  
  
 El campo SQL_DESC_DATA_PTR de un IPD no se establece normalmente; Sin embargo, una aplicación puede hacerlo para forzar una comprobación de coherencia de los campos IPD. No se puede realizar una comprobación de coherencia en un IRD. El valor establecido en el campo SQL_DESC_DATA_PTR de la IPD no se almacena realmente y no se puede recuperar mediante una llamada a **SQLGetDescField** o **SQLGetDescRec**; la configuración se realiza solo para forzar la comprobación de coherencia.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Un parámetro de enlace|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtención de un campo único descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Introducción a varios campos de descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Campos de descriptor solo configuración|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
