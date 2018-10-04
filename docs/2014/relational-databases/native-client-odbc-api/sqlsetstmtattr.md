---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edd96f9927a5fe698dd47489beffc738b5456708
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208535"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no admite el modelo de cursor mixto (controlado por conjunto de claves/dinámico). Cualquier intento de establecer el tamaño del conjunto de claves mediante SQL_ATTR_KEYSET_SIZE generará un error si el conjunto de valores no es igual a 0.  
  
 La aplicación establece SQL_ATTR_ROW_ARRAY_SIZE en todas las instrucciones para declarar el número de filas devueltas en un **SQLFetch** o [SQLFetchScroll](sqlfetchscroll.md) llamada de función. En las instrucciones que indican un cursor de servidor, el controlador utiliza SQL_ATTR_ROW_ARRAY_SIZE para determinar el tamaño del bloque de filas que genera el servidor con el fin de satisfacer una solicitud de captura del cursor. Dentro del tamaño de bloque de un cursor dinámico, la pertenencia y el orden de las filas son fijos si el nivel de aislamiento de la transacción es suficiente para asegurar la posibilidad de repetir las lecturas de las transacciones confirmadas. El cursor es completamente dinámico fuera del bloque indicado por este valor. El tamaño del bloque del cursor de servidor es completamente dinámico y se puede cambiar en cualquier punto del procesamiento de captura.  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr y parámetros con valores de tabla  
 SQLSetStmtAttr puede usarse para establecer SQL_SOPT_SS_PARAM_FOCUS en el descriptor de parámetro de la aplicación (APD) antes de acceder a los campos de descriptor para columnas de parámetro con valores de tabla.  
  
 Si se realiza un intento para establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal de un parámetro que es no un parámetro con valores de tabla, SQLSetStmtAttr devuelve SQL_ERROR y un registro de diagnóstico se crea con SQLSTATE = HY024 y el mensaje "valor de atributo no válido". SQL_SOPT_SS_PARAM_FOCUS no cambia cuando se devuelve SQL_ERROR.  
  
 Al establecer SQL_SOPT_SS_PARAM_FOCUS en 0, se restaura acceso a los registros descriptores para parámetros.  
  
 SQLSetStmtAttr también puede utilizarse para establecer SQL_SOPT_SS_NAME_SCOPE. Para obtener más información, vea la sección sobre SQL_SOPT_SS_NAME_SCOPE en este mismo tema.  
  
 Para obtener más información, consulte [los metadatos del parámetro con valores de tabla para instrucciones preparadas](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>Compatibilidad de SQLSetStmtAttr con columnas dispersas  
 SQLSetStmtAttr puede usarse para establecer SQL_SOPT_SS_NAME_SCOPE. Para obtener más información, consulte la sección sobre SQL_SOPT_SS_NAME_SCOPE, más adelante en este tema. Para obtener más información sobre las columnas dispersas, vea [Sparse Columns Support &#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="statement-attributes"></a>Atributos de instrucción  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client también admite los siguientes atributos de instrucción específicos del controlador.  
  
### <a name="sqlsoptsscursoroptions"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 El atributo SQL_SOPT_SS_CURSOR especifica si el controlador utilizará las opciones de rendimiento específicas del controlador en cursores. [SQLGetData](sqlgetdata.md) no se permite cuando se establecen estas opciones. El valor predeterminado es SQL_CO_OFF. El valor de *ValuePtr* es de tipo SQLLEN.  
  
|*ValuePtr* valor|Descripción|  
|----------------------|-----------------|  
|SQL_CO_OFF|Predeterminado: Deshabilita los cursores de solo avance rápido, solo lectura y la captura automática, permite **SQLGetData** en los cursores de solo avance y solo lectura. Si SQL_SOPT_SS_CURSOR_OPTIONS está establecido en SQL_CO_OFF, el tipo de cursor no cambiará. Es decir, el cursor de solo avance rápido seguirá siendo un cursor de solo avance rápido. Para cambiar el tipo de cursor, la aplicación debe establecer ahora un tipo de cursor diferente mediante `SQLSetStmtAttr`/SQL_ATTR_CURSOR_TYPE.|  
|SQL_CO_FFO|Habilita los cursores de solo avance rápido, solo lectura, deshabilita **SQLGetData** en los cursores de solo avance y solo lectura.|  
|SQL_CO_AF|Habilita la opción de captura automática en cualquier tipo de cursor. Cuando esta opción se establece para un identificador de instrucción, **SQLExecute** o **SQLExecDirect** generará implícita **SQLFetchScroll** (SQL_FIRST). El cursor se abre y se devuelve el primer lote de filas en un único viaje de ida y vuelta al servidor.|  
|SQL_CO_FFO_AF|Habilita los cursores de solo avance rápido con la opción de captura automática. Es lo mismo que si se especifican SQL_CO_AF y SQL_CO_FFO.|  
  
 Cuando se establecen estas opciones, el servidor cierra el cursor automáticamente en cuanto detecta que se ha capturado la última fila. La aplicación debe seguir llamando a [SQLFreeStmt](sqlfreestmt.md) (SQL_CLOSE) o [SQLCloseCursor](sqlclosecursor.md), pero el controlador no tiene que enviar la notificación de cierre al servidor.  
  
 Si la lista select contiene un **texto**, **ntext**, o **imagen** columna, el cursor de solo avance rápido se convierte en un cursor dinámico y **SQLGetData** está permitido.  
  
### <a name="sqlsoptssdeferprepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 El atributo SQL_SOPT_SS_DEFER_PREPARE determina si la instrucción se prepara inmediatamente o aplazar hasta que **SQLExecute**, [SQLDescribeCol](sqldescribecol.md) o [SQLDescribeParam](sqldescribeparam.md) se ejecuta. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 y versiones anteriores, esta propiedad se omite (no hay preparación diferida). El valor de *ValuePtr* es de tipo SQLLEN.  
  
|*ValuePtr* valor|Descripción|  
|----------------------|-----------------|  
|SQL_DP_ON|Predeterminado: Después de llamar a [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360), la preparación de instrucciones se difiere hasta que **SQLExecute** se llama o la operación de metapropiedad (**SQLDescribeCol** o **SQLDescribeParam**) se ejecuta.|  
|SQL_DP_OFF|La instrucción se prepara en cuanto **SQLPrepare** se ejecuta.|  
  
### <a name="sqlsoptssregionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 El atributo SQL_SOPT_SS_REGIONALIZE se utiliza para determinar la conversión de datos en el nivel de instrucción. El atributo hace que el controlador respete la configuración regional del cliente al convertir los valores de fecha, hora y moneda en cadenas de caracteres. La conversión solo se hace de tipos de datos nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cadenas de caracteres.  
  
 El valor de *ValuePtr* es de tipo SQLLEN.  
  
|*ValuePtr* valor|Descripción|  
|----------------------|-----------------|  
|SQL_RE_OFF|Predeterminado: El controlador no convierte los datos de fecha, hora y moneda a datos de cadenas de caracteres utilizando la configuración regional del cliente.|  
|SQL_RE_ON|El controlador utiliza la configuración regional del cliente al convertir los datos de fecha, hora y moneda en datos de cadenas de caracteres.|  
  
 La configuración de conversión regional se aplica a los tipos de datos de moneda, numéricos, de fecha y de hora. La configuración de conversión solamente es aplicable a la conversión de salida cuando los valores de moneda, numéricos, de fecha o de hora se convierten en cadenas de caracteres.  
  
> [!NOTE]  
>  Si la opción de instrucción SQL_SOPT_SS_REGIONALIZE está activada, el controlador utiliza la configuración regional del Registro para el usuario actual. El controlador no respeta la configuración regional del subproceso actual si la aplicación establece, por ejemplo, una llamada a **SetThreadLocale**.  
  
 Modificar el comportamiento regional de un origen de datos puede producir errores en la aplicación. Una aplicación que analiza cadenas de fecha y espera que las cadenas de fecha aparezcan tal y como se definen en ODBC, podría verse afectada negativamente por la modificación de este valor.  
  
### <a name="sqlsoptsstextptrlogging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 El atributo SQL_SOPT_SS_TEXTPTR_LOGGING alterna el registro de operaciones en las columnas que contienen **texto** o **imagen** datos. El valor de *ValuePtr* es de tipo SQLLEN.  
  
|*ValuePtr* valor|Descripción|  
|----------------------|-----------------|  
|SQL_TL_OFF|Deshabilita el registro de operaciones realizadas en **texto** y **imagen** datos.|  
|SQL_TL_ON|Predeterminado: Habilita el registro de las operaciones realizadas en **texto** y **imagen** datos.|  
  
### <a name="sqlsoptsshiddencolumns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 El atributo SQL_SOPT_SS_HIDDEN_COLUMNS expone, en el conjunto de resultados, las columnas ocultas en una instrucción SELECT FOR BROWSE de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El controlador no expone estas columnas de forma predeterminada. El valor de *ValuePtr* es de tipo SQLLEN.  
  
|*ValuePtr* valor|Descripción|  
|----------------------|-----------------|  
|SQL_HC_OFF|Predeterminado: Las columnas FOR BROWSE se ocultan del conjunto de resultados.|  
|SQL_HC_ON|Expone las columnas FOR BROWSE.|  
  
### <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 El atributo SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT devuelve el texto del mensaje de la solicitud de notificación de consulta.  
  
### <a name="sqlsoptssquerynotificationoptions"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 El atributo SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS especifica las opciones utilizadas para la solicitud de notificación de consulta. Se especifican en una cadena con sintaxis `name=value` como se indica a continuación. La aplicación es la responsable de la creación del servicio y de la lectura de las notificaciones fuera de la cola.  
  
 La sintaxis de la cadena de opciones de notificación de consulta es la siguiente:  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 Por ejemplo:  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sqlsoptssquerynotificationtimeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 El atributo SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT especifica el número de segundos que va a seguir estando activa la notificación de consulta. El valor predeterminado es de 432000 segundos (5 días). El valor de *ValuePtr* es de tipo SQLLEN.  
  
### <a name="sqlsoptssparamfocus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 El atributo SQL_SOPT_SS_PARAM_FOCUS especifica el foco de SQLBindParameter subsiguientes, SQLGetDescField, SQLSetDescField, SQLGetDescRec y SQLSetDescRec llama.  
  
 El tipo para SQL_SOPT_SS_PARAM_FOCUS es SQLULEN.  
  
 El valor predeterminado es 0, lo que significa que estas llamadas direccionan parámetros que corresponden a marcadores de parámetros en la instrucción SQL. Cuando se establecen en el número de parámetro de un parámetro con valores de tabla, estas llamadas direccionan columnas de ese parámetro con valores de tabla. Cuando se establece en un valor que no es el número de parámetro de un parámetro con valores de tabla, estas llamadas devuelven el error IM020: "El foco del parámetro no hace referencia a un parámetro de valores de tabla".  
  
### <a name="sqlsoptssnamescope"></a>SQL_SOPT_SS_NAME_SCOPE  
 El atributo SQL_SOPT_SS_NAME_SCOPE especifica el ámbito de nombres para las llamadas posteriores a funciones de catálogo. El conjunto de resultados devuelto por SQLColumns depende del valor de SQL_SOPT_SS_NAME_SCOPE.  
  
 El tipo para SQL_SOPT_SS_NAME_SCOPE es SQLULEN.  
  
|*ValuePtr* valor|Descripción|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|Predeterminado:<br /><br /> Cuando se utilizan parámetros con valores de tabla, indica que se deben devolver metadatos para las tablas reales.<br /><br /> Al utilizar la característica de columnas dispersas, SQLColumns solo devolverá columnas que no son miembros de disperso `column_set`.|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|Indica que la aplicación requiere metadatos para un tipo de tabla, en lugar de una tabla real (las funciones de catálogo deben devolver metadatos para los tipos de tabla). La aplicación, a continuación, pasa el TYPE_NAME del parámetro con valores de tabla como el *TableName* parámetro.|  
|SQL_SS_NAME_SCOPE_EXTENDED|Al utilizar la característica de columnas dispersas, SQLColumns devuelve todas las columnas, con independencia de `column_set` pertenencia.|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|Al utilizar la característica de columnas dispersas, SQLColumns devuelve solo las columnas que son miembros de disperso `column_set`.|  
|SQL_SS_NAME_SCOPE_DEFAULT|Igual que SQL_SS_NAME_SCOPE_TABLE.|  
  
 SS_TYPE_CATALOG_NAME y SS_TYPE_SCHEMA_NAME se utilizan con el *CatalogName* y *SchemaName* parámetros, respectivamente, para identificar el catálogo y esquema para el parámetro con valores de tabla. Cuando una aplicación ha terminado de recuperar los metadatos para los parámetros con valores de tabla, debe volver a establecer SQL_SOPT_SS_NAME_SCOPE en su valor predeterminado de SQL_SS_NAME_SCOPE_TABLE.  
  
 Si SQL_SOPT_SS_NAME_SCOPE está establecido en SQL_SS_NAME_SCOPE_TABLE, las consultas a los servidores vinculados producen un error. Se producirá un error en las llamadas a SQLColumns o SQLPrimaryKeys con un catálogo que contiene un componente de servidor.  
  
 Si intenta establecer SQL_SOPT_SS_NAME_SCOPE en un valor no válido, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE HY024 y el mensaje "Valor de atributo no válido".  
  
 Si un catálogo de otra función, a continuación, se llama a SQLTables, SQLColumns o SQLPrimaryKeys SQL_SOPT_SS_NAME_SCOPE tiene un valor distinto de SQL_SS_NAME_SCOPE_TABLE, se devuelve SQL_ERROR. Se genera un registro de diagnóstico con SQLSTATE HY010 y el mensaje "Error en la secuencia de función (SQL_SOPT_SS_NAME_SCOPE no está establecido en SQL_SS_NAME_SCOPE_TABLE)".  
  
## <a name="see-also"></a>Vea también  
 [Función SQLGetStmtAttr](http://go.microsoft.com/fwlink/?LinkId=59355)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
