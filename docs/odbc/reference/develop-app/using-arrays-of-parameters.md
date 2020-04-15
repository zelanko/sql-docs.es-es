---
title: Uso de matrices de parámetros ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 5a28be88-e171-4f5b-bf4d-543c4383c869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b584dc3d635e9fa8ce3228e4e89b0f24451fe165
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306806"
---
# <a name="using-arrays-of-parameters"></a>Utilizar matrices de parámetros
Para usar matrices de parámetros, la aplicación llama a **SQLSetStmtAttr** con un *attribute* argumento de SQL_ATTR_PARAMSET_SIZE para especificar el número de conjuntos de parámetros. Llama a **SQLSetStmtAttr** con un *argumento Attribute* de SQL_ATTR_PARAMS_PROCESSED_PTR para especificar la dirección de una variable en la que el controlador puede devolver el número de conjuntos de parámetros procesados, incluidos los conjuntos de errores. Llama a **SQLSetStmtAttr** con un *argumento Attribute* de SQL_ATTR_PARAM_STATUS_PTR para que apunte a una matriz en la que se va a devolver información de estado para cada fila de valores de parámetro. El controlador almacena estas direcciones en la estructura que mantiene para la instrucción.  
  
> [!NOTE]  
>  En ODBC 2. *x*, **SQLParamOptions** se llamó para especificar varios valores para un parámetro. En ODBC 3. *x*, la llamada a **SQLParamOptions** se ha reemplazado por llamadas a **SQLSetStmtAttr** para establecer los atributos SQL_ATTR_PARAMSET_SIZE y SQL_ATTR_PARAMS_PROCESSED_ARRAY.  
  
 Antes de ejecutar la instrucción, la aplicación establece el valor de cada elemento de cada matriz enlazada. Cuando se ejecuta la instrucción, el controlador utiliza la información que almacenó para recuperar los valores de parámetro y enviarlos al origen de datos; si es posible, el controlador debe enviar estos valores como matrices. Aunque el uso de matrices de parámetros se implementa mejor ejecutando la instrucción SQL con todos los parámetros de la matriz con una sola llamada al origen de datos, esta capacidad no está ampliamente disponible en los DBMS hoy en día. Sin embargo, los controladores pueden simularlo ejecutando una instrucción SQL varias veces, cada una con un único conjunto de parámetros.  
  
 Antes de que una aplicación utilice matrices de parámetros, debe asegurarse de que son compatibles con los controladores utilizados por la aplicación. Existen dos modos para hacer esto:  
  
-   Utilice solo controladores conocidos para admitir matrices de parámetros. La aplicación puede codificar de forma rígida los nombres de estos controladores, o se puede indicar al usuario que utilice solo estos controladores. Las aplicaciones personalizadas y las aplicaciones verticales suelen utilizar un conjunto limitado de controladores.  
  
-   Compruebe la compatibilidad con matrices de parámetros en tiempo de ejecución. Un controlador admite matrices de parámetros si es posible establecer el atributo de instrucción SQL_ATTR_PARAMSET_SIZE en un valor mayor que 1. Las aplicaciones genéricas y las aplicaciones verticales suelen comprobar la compatibilidad con matrices de parámetros en tiempo de ejecución.  
  
 La disponibilidad de los recuentos de filas y los conjuntos de resultados en la ejecución parametrizada se puede determinar llamando a **SQLGetInfo** con las opciones SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS. Para las instrucciones **INSERT**, **UPDATE**y **DELETE,** la opción SQL_PARAM_ARRAY_ROW_COUNTS indica si los recuentos de filas individuales (uno para cada conjunto de parámetros) están disponibles (SQL_PARC_BATCH) o si los recuentos de filas se acumulan en uno (SQL_PARC_NO_BATCH). Para las instrucciones **SELECT,** la opción SQL_PARAM_ARRAY_SELECTS indica si un conjunto de resultados está disponible para cada conjunto de parámetros (SQL_PAS_BATCH) o si solo hay un conjunto de resultados disponible (SQL_PAS_NO_BATCH). Si el controlador no permite que se ejecuten instrucciones de generación de conjuntos de resultados con una matriz de parámetros, SQL_PARAM_ARRAY_SELECTS devuelve SQL_PAS_NO_SELECT. Es específico del origen de datos si las matrices de parámetros se pueden usar con otros tipos de instrucciones, especialmente porque el uso de parámetros en estas instrucciones sería específico del origen de datos y no seguiría la gramática SQL ODBC.  
  
 La matriz a la que apunta el atributo de instrucción SQL_ATTR_PARAM_OPERATION_PTR se puede utilizar para omitir filas de parámetros. Si un elemento de la matriz se establece en SQL_PARAM_IGNORE, el conjunto de parámetros correspondientes a ese elemento se excluye de la **sqlExecute** o **SQLExecDirect** llamada. La aplicación asigna y rellena la matriz señalada por el atributo SQL_ATTR_PARAM_OPERATION_PTR y la lectura del controlador. Si las filas recuperadas se utilizan como parámetros de entrada, los valores de la matriz de estado de fila se pueden utilizar en la matriz de operaciones de parámetros.  
  
## <a name="error-processing"></a>Procesamiento de errores  
 Si se produce un error al ejecutar la instrucción, la función de ejecución devuelve un error y establece la variable de número de fila en el número de la fila que contiene el error. Es específico del origen de datos si se ejecutan todas las filas excepto el conjunto de errores o si se ejecutan todas las filas anteriores (pero no después) del conjunto de errores. Dado que procesa conjuntos de parámetros, el controlador establece el búfer especificado por el atributo de instrucción SQL_ATTR_PARAMS_PROCESSED_PTR en el número de la fila que se está procesando actualmente. Si se ejecutan todos los conjuntos excepto el conjunto de errores, el controlador establece este búfer en SQL_ATTR_PARAMSET_SIZE después de procesar todas las filas.  
  
 Si se ha establecido el atributo de instrucción SQL_ATTR_PARAM_STATUS_PTR, **SQLExecute** o **SQLExecDirect** devuelve la matriz de estado del *parámetro,* que proporciona el estado de cada conjunto de parámetros. La aplicación asigna la matriz de estado del parámetro y la rellena el controlador. Sus elementos indican si la instrucción SQL se ejecutó correctamente para la fila de parámetros o si se produjo un error al procesar el conjunto de parámetros. Si se ha producido un error, el controlador establece el valor correspondiente en la matriz de estado del parámetro en SQL_PARAM_ERROR y devuelve SQL_SUCCESS_WITH_INFO. La aplicación puede comprobar la matriz de estado para determinar qué filas se procesaron. Utilizando el número de fila, la aplicación a menudo puede corregir el error y reanudar el procesamiento.  
  
 El modo en que se utiliza la matriz de estado del parámetro viene determinado por las opciones SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS devueltas por una llamada a **SQLGetInfo**. Para las instrucciones **INSERT**, **UPDATE**y **DELETE,** la matriz de estado del parámetro se rellena con información de estado si se devuelve SQL_PARC_BATCH para SQL_PARAM_ARRAY_ROW_COUNTS, pero no si se devuelve SQL_PARC_NO_BATCH. Para las instrucciones **SELECT,** la matriz de estado del parámetro se rellena si se devuelve SQL_PAS_BATCH para SQL_PARAM_ARRAY_SELECT, pero no si se devuelve SQL_PAS_NO_BATCH o SQL_PAS_NO_SELECT.  
  
## <a name="data-at-execution-parameters"></a>Parámetros de datos en ejecución  
 Si alguno de los valores de la matriz length/indicator se SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*), los datos de esos valores se envían con **SQLPutData** de la manera habitual. Los siguientes aspectos de este proceso llevan un comentario especial porque no son fácilmente obvios:  
  
-   Cuando el controlador devuelve SQL_NEED_DATA, debe establecer la dirección de la variable de número de fila en la fila para la que necesita datos. Como en el caso de un solo valor, la aplicación no puede realizar ninguna suposición sobre el orden en el que el controlador solicitará valores de parámetro dentro de un único conjunto de parámetros. Si se produce un error en la ejecución de un parámetro de datos en ejecución, el búfer especificado por el atributo de instrucción SQL_ATTR_PARAMS_PROCESSED_PTR se establece en el número de la fila en la que se produjo el error, el estado de la fila de la matriz de estado de fila especificada por el atributo de instrucción SQL_ATTR_PARAM_STATUS_PTR se establece en SQL_PARAM_ERROR y la llamada a **SQLExecute**, **SQLExecDirect**, **SQLParamData**o **SQLPutData** devuelve SQL_ERROR. El contenido de este búfer no está definido si **SQLExecute**, **SQLExecDirect**o **SQLParamData** devuelven SQL_STILL_EXECUTING.  
  
-   Dado que el controlador no interpreta el valor en el *ParameterValuePtr* argumento de **SQLBindParameter** para los parámetros de datos en ejecución, si la aplicación proporciona un puntero a una matriz, **SQLParamData** no extrae y devuelve un elemento de esta matriz a la aplicación. En su lugar, devuelve el valor escalar que la aplicación había proporcionado. Esto significa que el valor devuelto por **SQLParamData** no es suficiente para especificar el parámetro para el que la aplicación necesita enviar datos; la aplicación también debe tener en cuenta el número de fila actual.  
  
     Cuando solo algunos de los elementos de una matriz de parámetros son parámetros de datos en ejecución, la aplicación debe pasar la dirección de una matriz en *ParameterValuePtr* que contiene elementos para todos los parámetros. Esta matriz se interpreta normalmente para los parámetros que no son parámetros de datos en ejecución. Para los parámetros de datos en ejecución, el valor que **SQLParamData** proporciona a la aplicación, que normalmente se podría usar para identificar los datos que el controlador está solicitando en esta ocasión, siempre es la dirección de la matriz.
