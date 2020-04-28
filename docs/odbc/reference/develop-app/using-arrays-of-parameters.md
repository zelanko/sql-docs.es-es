---
title: Usar matrices de parámetros | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306806"
---
# <a name="using-arrays-of-parameters"></a>Utilizar matrices de parámetros
Para usar matrices de parámetros, la aplicación llama a **SQLSetStmtAttr** con un argumento de *atributo* de SQL_ATTR_PARAMSET_SIZE para especificar el número de conjuntos de parámetros. Llama a **SQLSetStmtAttr** con un argumento de *atributo* de SQL_ATTR_PARAMS_PROCESSED_PTR para especificar la dirección de una variable en la que el controlador puede devolver el número de conjuntos de parámetros procesados, incluidos los conjuntos de errores. Llama a **SQLSetStmtAttr** con un argumento de *atributo* de SQL_ATTR_PARAM_STATUS_PTR para apuntar a una matriz en la que se va a devolver información de estado para cada fila de valores de parámetro. El controlador almacena estas direcciones en la estructura que mantiene para la instrucción.  
  
> [!NOTE]  
>  En ODBC 2. *x*se llamó a **SQLParamOptions** para especificar varios valores para un parámetro. En ODBC 3. *x*, la llamada a **SQLParamOptions** se ha reemplazado por llamadas a **SQLSetStmtAttr** para establecer los atributos SQL_ATTR_PARAMSET_SIZE y SQL_ATTR_PARAMS_PROCESSED_ARRAY.  
  
 Antes de ejecutar la instrucción, la aplicación establece el valor de cada elemento de cada matriz enlazada. Cuando se ejecuta la instrucción, el controlador usa la información almacenada para recuperar los valores de parámetro y enviarlos al origen de datos. Si es posible, el controlador debe enviar estos valores como matrices. Aunque el uso de matrices de parámetros se implementa mejor mediante la ejecución de la instrucción SQL con todos los parámetros de la matriz con una sola llamada al origen de datos, esta funcionalidad no está ampliamente disponible en DBMS en la actualidad. Sin embargo, los controladores pueden simularla mediante la ejecución de una instrucción SQL varias veces, cada una con un único conjunto de parámetros.  
  
 Antes de que una aplicación use matrices de parámetros, debe asegurarse de que son compatibles con los controladores utilizados por la aplicación. Existen dos modos para hacer esto:  
  
-   Use solo los controladores que se sabe que admiten matrices de parámetros. La aplicación puede codificar de forma rígida los nombres de estos controladores o se puede indicar al usuario que use solo estos controladores. Las aplicaciones personalizadas y las aplicaciones verticales suelen usar un conjunto limitado de controladores.  
  
-   Comprobar la compatibilidad de matrices de parámetros en tiempo de ejecución. Un controlador admite matrices de parámetros si es posible establecer el atributo de instrucción SQL_ATTR_PARAMSET_SIZE en un valor mayor que 1. Las aplicaciones genéricas y las aplicaciones verticales comprueban normalmente la compatibilidad de matrices de parámetros en tiempo de ejecución.  
  
 La disponibilidad de los recuentos de filas y los conjuntos de resultados en la ejecución parametrizada se puede determinar mediante una llamada a **SQLGetInfo** con las opciones SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS. En el caso de las instrucciones **Insert**, **Update**y **Delete** , la opción SQL_PARAM_ARRAY_ROW_COUNTS indica si los recuentos de filas individuales (uno para cada conjunto de parámetros) están disponibles (SQL_PARC_BATCH) o si los recuentos de filas se acumulan en uno (SQL_PARC_NO_BATCH). En el caso de las instrucciones **Select** , la opción SQL_PARAM_ARRAY_SELECTS indica si un conjunto de resultados está disponible para cada conjunto de parámetros (SQL_PAS_BATCH) o si solo hay un conjunto de resultados disponible (SQL_PAS_NO_BATCH). Si el controlador no permite que se ejecuten las instrucciones que generan conjuntos de resultados con una matriz de parámetros, SQL_PARAM_ARRAY_SELECTS devuelve SQL_PAS_NO_SELECT. Es específico del origen de datos si se pueden usar matrices de parámetros con otros tipos de instrucciones, especialmente porque el uso de parámetros en estas instrucciones sería específico del origen de datos y no seguiría la gramática de SQL de ODBC.  
  
 La matriz a la que señala el atributo de instrucción SQL_ATTR_PARAM_OPERATION_PTR se puede utilizar para omitir las filas de parámetros. Si un elemento de la matriz se establece en SQL_PARAM_IGNORE, el conjunto de parámetros correspondiente a ese elemento se excluye de la llamada **SQLExecute** o **SQLExecDirect** . La aplicación a la que señala el atributo SQL_ATTR_PARAM_OPERATION_PTR es asignada y rellenada por la aplicación y leída por el controlador. Si se usan filas capturadas como parámetros de entrada, los valores de la matriz de estado de fila se pueden usar en la matriz de operaciones de parámetros.  
  
## <a name="error-processing"></a>Procesamiento de errores  
 Si se produce un error al ejecutar la instrucción, la función de ejecución devuelve un error y establece la variable de número de fila en el número de la fila que contiene el error. Es específico del origen de datos si se ejecutan todas las filas, excepto el conjunto de errores, o si se ejecutan todas las filas anteriores (pero no después) del conjunto de errores. Dado que procesa los conjuntos de parámetros, el controlador establece el búfer especificado por el atributo de instrucción SQL_ATTR_PARAMS_PROCESSED_PTR en el número de la fila que se está procesando actualmente. Si se ejecutan todos los conjuntos excepto el conjunto de errores, el controlador establece este búfer en SQL_ATTR_PARAMSET_SIZE una vez procesadas todas las filas.  
  
 Si se ha establecido el atributo de instrucción SQL_ATTR_PARAM_STATUS_PTR, **SQLExecute** o **SQLExecDirect** devuelve la matriz de *Estado de parámetro,* que proporciona el estado de cada conjunto de parámetros. La aplicación asigna la matriz de estado del parámetro y la rellena el controlador. Sus elementos indican si la instrucción SQL se ha ejecutado correctamente para la fila de parámetros o si se ha producido un error al procesar el conjunto de parámetros. Si se produce un error, el controlador establece el valor correspondiente en la matriz de estado de parámetro en SQL_PARAM_ERROR y devuelve SQL_SUCCESS_WITH_INFO. La aplicación puede comprobar la matriz de estado para determinar qué filas se procesaron. Con el número de fila, la aplicación a menudo puede corregir el error y reanudar el procesamiento.  
  
 La forma en que se usa la matriz de estado de parámetro se determina mediante las opciones SQL_PARAM_ARRAY_ROW_COUNTS y SQL_PARAM_ARRAY_SELECTS devueltas por una llamada a **SQLGetInfo**. En el caso de las instrucciones **Insert**, **Update**y **Delete** , la matriz de estado de parámetro se rellena con información de estado si se devuelve SQL_PARC_BATCH para SQL_PARAM_ARRAY_ROW_COUNTS, pero no si se devuelve SQL_PARC_NO_BATCH. En el caso de las instrucciones **Select** , la matriz de estado de parámetro se rellena si se devuelve SQL_PAS_BATCH para SQL_PARAM_ARRAY_SELECT, pero no si se devuelve SQL_PAS_NO_BATCH o SQL_PAS_NO_SELECT.  
  
## <a name="data-at-execution-parameters"></a>Parámetros de datos en ejecución  
 Si alguno de los valores de la matriz de longitud/indicador es SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC (*longitud*), los datos de esos valores se envían con **SQLPutData** de la manera habitual. Los siguientes aspectos de este proceso llevan un comentario especial porque no son muy obvios:  
  
-   Cuando el controlador devuelve SQL_NEED_DATA, debe establecer la dirección de la variable de número de fila en la fila para la que necesita datos. Como en el caso de un solo valor, la aplicación no puede hacer ninguna suposición sobre el orden en el que el controlador solicitará los valores de parámetro dentro de un único conjunto de parámetros. Si se produce un error en la ejecución de un parámetro de datos en ejecución, el búfer especificado por el atributo de instrucción SQL_ATTR_PARAMS_PROCESSED_PTR se establece en el número de la fila en la que se produjo el error, el estado de la fila en la matriz de estado de fila especificado por el atributo de instrucción SQL_ATTR_PARAM_STATUS_PTR se establece en SQL_PARAM_ERROR y la llamada a **SQLExecute**, **SQLExecDirect**, **SQLParamData**o **SQLPutData** devuelve SQL_ERROR. El contenido de este búfer no está definido si **SQLExecute**, **SQLExecDirect**o **SQLParamData** devuelven SQL_STILL_EXECUTING.  
  
-   Dado que el controlador no interpreta el valor del argumento *ParameterValuePtr* de **SQLBindParameter** para los parámetros de datos en ejecución, si la aplicación proporciona un puntero a una matriz, **SQLParamData** no extrae y devuelve un elemento de esta matriz a la aplicación. En su lugar, devuelve el valor escalar proporcionado por la aplicación. Esto significa que el valor devuelto por **SQLParamData** no es suficiente para especificar el parámetro para el que la aplicación necesita enviar datos; la aplicación también debe tener en cuenta el número de fila actual.  
  
     Cuando solo algunos de los elementos de una matriz de parámetros son parámetros de datos en ejecución, la aplicación debe pasar la dirección de una matriz en *ParameterValuePtr* que contiene elementos para todos los parámetros. Esta matriz se interpreta normalmente para los parámetros que no son parámetros de datos en ejecución. En el caso de los parámetros de datos en ejecución, el valor que **SQLParamData** proporciona a la aplicación, que normalmente podría usarse para identificar los datos que el controlador solicita en esta ocasión, siempre es la dirección de la matriz.
