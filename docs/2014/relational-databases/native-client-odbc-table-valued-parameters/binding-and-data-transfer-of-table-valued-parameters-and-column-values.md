---
title: Enlace y transferencia de datos de con valores de tabla de parámetros y valores de columna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26bcf31c2d4e0d188e93587dd9bdec1a9ff382e0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199957"
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>Enlace y transferencia de datos de valores de columnas y parámetros con valores de tabla
  Los parámetros con valores de tabla, al igual que otros parámetros, deben enlazarse antes de pasarse al servidor. La aplicación enlaza los parámetros con valores de tabla del mismo modo enlaza otros parámetros: con SQLBindParameter o llamadas equivalentes a SQLSetDescField o SQLSetDescRec. El tipo de datos del servidor para un parámetro con valores de tabla es SQL_SS_TABLE. El tipo de C puede especificarse como SQL_C_DEFAULT o SQL_C_BINARY.  
  
 En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior, solo se admiten parámetros con valores de tabla de entrada. Por lo tanto, cualquier intento de establecer SQL_DESC_PARAMETER_TYPE en un valor distinto de SQL_PARAM_INPUT devolverá SQL_ERROR con SQLSTATE = HY105 y el mensaje "Tipo de parámetro no válido".  
  
 Es posible asignar valores predeterminados a columnas completas de parámetros con valores de tabla mediante el atributo SQL_CA_SS_COL_HAS_DEFAULT_VALUE. Valores de columna del parámetro con valores de tabla individual, sin embargo, no se puede asignar valores predeterminados mediante el uso de SQL_DEFAULT_PARAM en *StrLen_or_IndPtr* con SQLBindParameter. No se puede establecer los parámetros con valores de tabla como un todo en un valor predeterminado mediante el uso de SQL_DEFAULT_PARAM en *StrLen_or_IndPtr* con SQLBindParameter. Si no se siguen estas reglas, SQLExecute o SQLExecDirect devolverá SQL_ERROR. Se generará un registro de diagnóstico con SQLSTATE = 07S01 y el mensaje "uso no válido de parámetro predeterminado para el parámetro \<p >", donde \<p > es el ordinal del TVP en la instrucción de consulta.  
  
 Después de enlazar el parámetro con valores de tabla, la aplicación debe enlazar cada una de las columnas de parámetros con valores de tabla. Para ello, la aplicación llama primero a SQLSetStmtAttr para establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal de un parámetro con valores de tabla. A continuación, la aplicación enlaza las columnas del parámetro con valores de tabla mediante llamadas a las rutinas siguientes: SQLBindParameter, SQLSetDescRec y SQLSetDescField. Al establecer SQL_SOPT_SS_PARAM_FOCUS en 0, se restaura el efecto usual de SQLBindParameter, SQLSetDescRec y SQLSetDescField de operar en los parámetros normales de nivel superior.  
  
 No se envían ni se reciben datos reales para el propio parámetro con valores de tabla, sino que los datos se envían y se reciben para cada una de sus columnas constitutivas. Dado que el parámetro con valores de tabla es una pseudocolumna, los parámetros de SQLBindParameter se usan para hacer referencia a atributos que otros tipos de datos, como se indica a continuación:  
  
|Parámetro|Atributo relacionado para tipos de parámetro que no son valores de tabla, incluidas las columnas|Atributo relacionado para parámetros con valores de tabla|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|SQL_DESC_PARAMETER_TYPE en IPD.<br /><br /> En el caso de las columnas de parámetros con valores de tabla, debe ser igual que el valor del propio parámetro con valores de tabla.|SQL_DESC_PARAMETER_TYPE en IPD.<br /><br /> Debe ser SQL_PARAM_INPUT.|  
|*ValueType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE en APD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE en APD.<br /><br /> Debe ser SQL_C_DEFAULT o SQL_C_BINARY.|  
|*ParameterType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE en IPD.|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE en IPD.<br /><br /> Debe ser SQL_SS_TABLE.|  
|*ColumnSize*|SQL_DESC_LENGTH o SQL_DESC_PRECISION en IPD.<br /><br /> Esto depende del valor de *ParameterType*.|SQL_DESC_ARRAY_SIZE<br /><br /> También puede establecerse mediante el uso de SQL_ATTR_PARAM_SET_SIZE cuando el foco del parámetro está establecido en el parámetro con valores de tabla.<br /><br /> En el caso de un parámetro con valores de tabla, se trata del número de filas de los búferes de columna del parámetro con valores de tabla.|  
|*DecimalDigits*|SQL_DESC_PRECISION o SQL_DESC_SCALE en IPD.|Sin usar. Esto debe ser 0.<br /><br /> Si este parámetro será no 0, SQLBindParameter generará retorno SQL_ERROR y un registro de diagnóstico con SQLSTATE = HY104 y el mensaje "no válida precisión o escala".|  
|*ParameterValuePtr*|SQL_DESC_DATA_PTR en APD.|SQL_CA_SS_TYPE_NAME.<br /><br /> Es opcional para las llamadas a procedimientos almacenados y puede especificarse NULL si no se requiere. Debe especificarse para las instrucciones SQL que no sean llamadas a procedimientos.<br /><br /> Este parámetro también actúa como un valor único que la aplicación puede usar para identificar este parámetro con valores de tabla cuando se usa el enlace de filas variable. Para obtener más información, consulte la sección "Enlace de filas variable de parámetros con valores de tabla" más adelante en este mismo tema.<br /><br /> Cuando se especifica un nombre de tipo de parámetro con valores de tabla en una llamada a SQLBindParameter, se debe especificar como un valor Unicode, incluso en las aplicaciones que se crean como aplicaciones ANSI. El valor utilizado para el parámetro *StrLen_or_IndPtr* debería ser SQL_NTS o la longitud de cadena del nombre multiplicada por sizeof (WCHAR).|  
|*BufferLength*|SQL_DESC_OCTET_LENGTH en APD.|Longitud en bytes del nombre de tipo de parámetro con valores de tabla.<br /><br /> Puede ser SQL_NTS si el nombre de tipo termina en NULL, o 0 si no se requiere el nombre de tipo de parámetro con valores de tabla.|  
|*StrLen_or_IndPtr*|SQL_DESC_OCTET_LENGTH_PTR en APD.|SQL_DESC_OCTET_LENGTH_PTR en APD.<br /><br /> En el caso de los parámetros con valores de tabla, es un recuento de filas en lugar de una longitud de datos.|  
  
 Se admiten dos modos de transferencia de datos para los parámetros con valores de tabla: enlace de filas fijo y enlace de filas variable.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>Enlace de filas fijo de parámetros con valores de tabla  
 En el caso del enlace de filas fijo, una aplicación asigna búferes (o matrices de búferes) suficientemente grandes para todos los valores posibles de columnas de entrada. La aplicación hace lo siguiente:  
  
1.  Enlaza todos los parámetros mediante llamadas SQLBindParameter, SQLSetDescRec o SQLSetDescField.  
  
    1.  Establece SQL_DESC_ARRAY_SIZE en el número máximo de filas que pueden transferirse para cada parámetro con valores de tabla. Esto puede hacerse en la llamada de SQLBindParameter.  
  
2.  Llama a SQLSetStmtAttr para establecer SQL_SOPT_SS_PARAM_FOCUS en el ordinal de cada parámetro con valores de tabla.  
  
    1.  Para cada parámetro con valores de tabla, enlaza las columnas de parámetros con valores de tabla mediante llamadas SQLBindParameter, SQLSetDescRec o SQLSetDescField.  
  
    2.  Para cada columna de parámetro con valores de tabla que va a tener valores predeterminados, llama a SQLSetDescField para establecer SQL_CA_SS_COL_HAS_DEFAULT_VALUE en 1.  
  
3.  Llama a SQLSetStmtAttr para establecer SQL_SOPT_SS_PARAM_FOCUS en 0. Esto debe hacerse antes de SQLExecute o SQLExecDirect se llama. De lo contrario, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE=HY024 y el mensaje "Valor de atributo no válido, SQL_SOPT_SS_PARAM_FOCUS (debe ser cero en el tiempo de ejecución)".  
  
4.  Conjuntos de *StrLen_or_IndPtr* o SQL_DESC_OCTET_LENGTH_PTR en SQL_DEFAULT_PARAM para un parámetro con valores de tabla con ninguna fila, o el número de filas que se transfieren en la siguiente llamada de SQLExecute o SQLExecDirect si los valores de tabla el parámetro tiene filas. *StrLen_or_IndPtr* o SQL_DESC_OCTET_LENGTH_PTR no puede establecerse en SQL_NULL_DATA para un parámetro con valores de tabla como parámetros con valores de tabla no admiten valores null (aunque columnas constituyentes del parámetro con valores de tabla pueden ser que acepta valores NULL). Si se establece en un valor no válido, SQLExecute o SQLExecDirect devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE = HY090 y el mensaje "longitud de búfer o cadena no válida para el parámetro \<p >", donde p es el número de parámetro.  
  
5.  Llama a SQLExecute o SQLExecDirect.  
  
 Entrada de valores de columna del parámetro con valores de tabla pueden pasarse por partes si *StrLen_or_IndPtr* está establecido en SQL_LEN_DATA_AT_EXEC (*longitud*) o SQL_DATA_AT_EXEC para la columna. Es similar a pasar valores por partes cuando se utilizan matrices de parámetros. Como con todos los parámetros de datos en ejecución, SQLParamData no indican qué fila de la matriz el controlador solicita datos para: la aplicación debe tener cuidado de este. La aplicación no puede hacer ninguna suposición sobre el orden en que el controlador solicitará los valores.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>Enlace de filas variable de parámetros con valores de tabla  
 En el caso del enlace de filas variable, las filas se transfieren en lotes en tiempo de ejecución y la aplicación pasa las filas al controlador a petición. Es similar a los datos en ejecución para los valores de parámetro individuales. En el caso del enlace de filas variable, la aplicación hace lo siguiente:  
  
1.  Enlaza parámetros y columnas de parámetros con valores de tabla tal y como se ha descrito en la sección anterior, "Enlace de filas fijo de parámetros con valores de tabla", en los pasos del 1 al 3.  
  
2.  Conjuntos de *StrLen_or_IndPtr* o sql_desc_octet_length_ptr en sql_data_at_exec para cualquier parámetro con valores de tabla que deben pasarse en tiempo de ejecución en SQL_DATA_AT_EXEC. Si no se establece ninguno de estos valores, el parámetro se procesará tal y como se describe en la sección anterior.  
  
3.  Llama a SQLExecute o SQLExecDirect. Esto devolverá SQL_NEED_DATA si hay algún parámetro SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_INPUT que deba controlarse como parámetro de datos en ejecución. En este caso, la aplicación hace lo siguiente:  
  
    -   Llama a SQLParamData. Esto devuelve el *ParameterValuePtr* valor para un parámetro de datos en ejecución y un código de retorno SQL_NEED_DATA. Cuando todos los datos de parámetro se ha pasado al controlador, SQLParamData devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Para los parámetros de datos en ejecución, *ParameterValuePtr*, que es el mismo que el descriptor de campo SQL_DESC_DATA_PTR, puede considerar como un token para identificar de forma única un parámetro para el que se requiere un valor. Este "token" se pasa de la aplicación al controlador en el momento del enlace y, después, vuelve a pasarse a la aplicación en tiempo de ejecución.  
  
4.  Para enviar datos de fila de parámetro con valores de tabla para los parámetros con valores de tabla null, si el parámetro con valores de tabla no tiene filas, una aplicación llama a SQLPutData con *StrLen_or_Ind* establecido en SQL_DEFAULT_PARAM.  
  
     Para los TVP que no son NULL, una aplicación hace lo siguiente:  
  
    -   Conjuntos de *Str_Len_or_Ind* para todas las columnas de parámetro con valores de tabla en los valores correspondientes y rellena los búferes de datos para las columnas de parámetro con valores de tabla que no deben ser parámetros de datos en ejecución. Puede usar los datos en ejecución para las columnas de parámetros con valores de tabla de forma similar al modo en que los parámetros ordinarios pueden pasarse por partes al controlador.  
  
    -   Llama a SQLPutData con *Str_Len_or_Ind* establecido al número de filas que se envíe al servidor. Cualquier valor que se encuentre fuera del intervalo de 0 a SQL_DESC_ARRAY_SIZE o SQL_DEFAULT_PARAM es un error y devolverá SQLSTATE HY090 con el mensaje "Longitud de búfer o cadena no válida". 0 indica que todas las filas se han enviado y que no hay más datos para un parámetro con valores de tabla (tal y como se indica en el segundo elemento de viñeta de esta lista). SQL_DEFAULT_PARAM solamente puede utilizarse la primera vez que el controlador solicita datos para un parámetro con valores de tabla (tal y como se describe en el primer elemento de viñeta de esta lista).  
  
5.  Cuando se han enviado todas las filas, llama a SQLPutData para el parámetro con valores de tabla con un *Str_Len_or_Ind* valor de 0, a continuación, continúa en el paso 3a anterior.  
  
6.  Llama a SQLParamData de nuevo. Si hay parámetros entre las columnas del parámetro con valores de tabla de datos en ejecución, éstas se identificarán mediante el valor *ValuePtrPtr* devuelto por SQLParamData. Cuando están disponibles todos los valores de columna, SQLParamData devolverá nuevamente el *ParameterValuePtr* valor para el parámetro con valores de tabla y la aplicación comienza de nuevo.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
